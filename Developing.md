# Getting Started
Universal Gcode Sender uses [Maven](http://maven.apache.org/) to build the project. It is using maven modules to separate the core library / classic GUI and the UGS Platform project. At the top level a UGS target defines the `ugs-core` and `ugs-platform-parent` modules which can be built separately or all at once.

The classic gui is part of the core project in the `ugs-core` module. The `maven-shade-plugin` and `maven-assembly-plugin` are generate the self-executing JAR and distribution zip.

UGS Platform is built on the [NetBeans Platform](https://netbeans.apache.org/front/main/). It is also using maven.

Development is done using any IDE that can handle maven projects such NetBeans or IntelliJ.

## Development with an IDE
Any IDE supporting Maven should be able to open the UGS project directory. Once opened it should show you the `ugs-core` and `ugs-platform-parent` modules which correspond to the Classic and Platform interfaces.

Development is done using NetBeans, and for some project development NetBeans is almost required. But for tweaking the UI and experimenting with the backend any IDE which supports maven can be used.

## Classic GUI
In the ugs-core module, you can run the `MainWindow.java` file to start the Classic GUI.

There is a helper script named run_classic.sh, or you can use the commands below.

**Running the UI**
```
mvn install
mvn exec:java -Dexec.mainClass="com.willwinder.universalgcodesender.MainWindow" -pl ugs-core
```

**Executing tests**
```
mvn install
mvn test -pl ugs-core
```

**Building the self-executing JAR**
```
mvn install
mvn package -pl ugs-core
```

**Building a UniversalGcodeSender.zip release file**
```
mvn package assembly:assembly
```


## UGS Platform
The platform build has a number of submodules. Load the suite of modules by running the ugs-platform-app module.

There is a helper script named `run_platform.sh`, or you can use the commands below.

**Running the UI**
```
mvn install
mvn nbm:run-platform -pl ugs-platform/application
```

# Backend
Similar to the front-end there are more layers on the backend to help with supporting differences between different gcode controllers and the different ways to communicate with these controllers. Because UGS depends on serial events from CNC devices, the communication between layers is also event driven. This is implemented using a series of **Listener** classes which pass messages from the lower levels to the upper levels whenever data is detected on the serial port (USB).

## Controller
A controller is primarily responsible for implementing controller-specific features. Different features can be things like what happens when a **Perform Homing** command is requested, or how to issue status requests and parse their results. GRBL and TinyG are both supported, they share a lot of code with the `AbstractController.java` abstract class.

Internally the **AbstractController** class implements several important things. It manages the stream lifecycle, keeping track of which commands have been sent, which have been completed and in some cases which are queued for sending. The controller also figures out when the stream has finished. Finally the **AbstractController** implements the **SerialCommunicatorListener**, which how its able to detect all of this state information (and allows commands to be sent to the CNC controller).

The controller provides a `ControllerListener` interface which is used to provide real time status.

Finally, the **AbstractController** defines a number of abstract methods which can be used by device specific controllers as needed to hook into important lifecycle events:
```java
    abstract protected void closeCommBeforeEvent();
    abstract protected void closeCommAfterEvent();
    protected void openCommAfterEvent() throws Exception {}
    abstract protected void cancelSendBeforeEvent();
    abstract protected void cancelSendAfterEvent();
    abstract protected void pauseStreamingEvent() throws Exception;
    abstract protected void resumeStreamingEvent() throws Exception;
    abstract protected void isReadyToSendCommandsEvent() throws Exception;
    abstract protected void statusUpdatesEnabledValueChanged(boolean enabled);
    abstract protected void statusUpdatesRateValueChanged(int rate);

    // This one is special, because it is responsible for parsing device
    // responses, such as a command complete, status string, or parsing a
    // status event. In the case of a command complete, it must call
    // `commandComplete` to push the stream lifecycle along.
    abstract protected void rawResponseHandler(String response);
```

Here is the public interface which controlles conform to:

```java
public interface IController {
    /*
    Observable
    */
    public void addListener(ControllerListener cl);

    /*
    Actions
    */
    public void performHomingCycle() throws Exception;
    public void returnToHome() throws Exception;
    public void resetCoordinatesToZero() throws Exception;
    public void resetCoordinateToZero(final char coord) throws Exception;
    public void killAlarmLock() throws Exception;
    public void toggleCheckMode() throws Exception;
    public void viewParserState() throws Exception;
    public void issueSoftReset() throws Exception;

    /*
    Behavior
    */
    public void setSingleStepMode(boolean enabled);
    public boolean getSingleStepMode();

    public void setStatusUpdatesEnabled(boolean enabled);
    public boolean getStatusUpdatesEnabled();

    public void setStatusUpdateRate(int rate);
    public int getStatusUpdateRate();

    public GcodeCommandCreator getCommandCreator();
    public long getJobLengthEstimate(File gcodeFile);

    /*
    Serial
    */
    public Boolean openCommPort(String port, int portRate) throws Exception;
    public Boolean closeCommPort() throws Exception;
    public Boolean isCommOpen();

    /*
    Stream information
    */
    public Boolean isReadyToStreamFile() throws Exception;
    public Boolean isStreamingFile();
    public long getSendDuration();
    public int rowsInSend();
    public int rowsSent();
    public int rowsRemaining();

    /*
    Stream control
    */
    public void beginStreaming() throws Exception;
    public void pauseStreaming() throws Exception;
    public void resumeStreaming() throws Exception;
    public void cancelSend();

    /*
    Stream content
    */
    public GcodeCommand createCommand(String gcode) throws Exception;
    public void sendCommandImmediately(GcodeCommand cmd) throws Exception;
    public void queueCommand(GcodeCommand cmd) throws Exception;
    public void queueStream(GcodeStreamReader r);
    public void queueRawStream(Reader r);
}
```

## Communicator
A communicator handles all levels of sending data to the device. Raw responses are returned to any listeners via the `SerialCommunicatorListener`.

The `AbstractCommunicator` implements several listener utilities which are used by implementing classes.

The `BufferedCommunicator` abstract class handles the process of buffering multiple commands at once in order to keep a constant stream of commands available to the CNC device. It does this in the **streamCommands** method by maintaining a list of active commands, and the current size of those commands. A method named **processedCommand** must be implemented in a subclass to determine whether a raw response indicates a command has completed. This notifies the **BufferedCommunicator** that it should attempt to send more commands.

`GrblCommunicator` and `TinyGCommunicator` are two concrete implementations of the **BufferedCommunicator**.

## Connection
This is a very thin layer which provides a way to write and receive data:

```
    abstract public boolean openPort(String name, int baud) throws Exception;
    abstract public void closePort() throws Exception;
    abstract public boolean isOpen();
    abstract public void sendByteImmediately(byte b) throws Exception;
    abstract public void sendStringToComm(String command) throws Exception;
```

## Streaming strategy
UGS attempts to use a fixed amount of memory when streaming a file. In this way it can send gcode files of any size. Files are preprocessed at the BackendAPI level using the GcodeStreamWriter class. This will serialize all the required metadata into a file. Later on that file can be opened with the GcodeStreamReader class, the **Controller** and **Communicator** classes use this. Using the reader, the **Communicator** class can pull out commands one at a time and send them to the **Connection**.

# Frontend
UGS uses a Model-View-Presenter architecture. What this means is that at a high level there are three layers which each serve different purposes. A *Model* for all backend logic, a *View* displayed to the user and a *Presenter* which serves as a buffer between the model and one or more views.

## Model
The model contains all backend logic. Things like opening a connection, listing serial ports, streaming a file, and handling firmware specific nuances. All of this is hidden from the front end as much as possible.

## View
The view only has access to the presenter. It is responsible for all user interaction and feedback. The main logic in here should be things like enabling or disabling components based on the current state of the model.

### Classic GUI
The **Classic GUI** is built using NetBeans. There are a number of custom Swing components, and they are all initialized with the NetBeans GUI builder. The vast majority of the **Classic GUI** code is contained in `MainWindow.java`. There isn't a lot to expand on here, this front end has grown organically over the years and is fairly rigid. The `Visualizer` component is a standalone JOGL window which is updated using events from the backend (it was a model for many of the improvements in the current applications architecture).

### UGS Platform
The **UGS Platform** build is also built using NetBeans. It is a built ontop of the NetBeans Platform which provides it a robust set of tools like flexible windows, a plugin framework, and a suite of tools for module communications. At the core of this is a module named `UGSLib` which is a simple wrapper to the standard UGS JAR file. There is a suite of modules named `UGSCore` which provides many of the standard UI elements seen in the **Classic GUI**, in addition there are other modules that provide new functionality.

Extending the GUI is now a matter of creating a new plugin, for details on how to do this see the [Plugin Tutorial](https://universalgcodesender.com/dev/plugin/).

## Presenter
The presenter serves as an API for the model. All the heavy lifting needed for the GUI should happen here. For example the controller model object knows how to stream a processed file, but it doesn't know how to process the file. So the presenter will pass data to the gcode processor and generate a processed object which can be passed to the controller.

Similarly, all notifications from the model are reinterpreted for the view with a simpler message strategy.

In this way, all updates to the backend code can be leveraged by all front ends which utilize UGS.

## BackendAPI
In UGS interfaces named BackendAPI and BackendAPIReadOnly provide the presenter layer. The read only methods are split off into a sub-interface in case a developer wants to be sure they don't change any state. For instance a widget that displays the current machine location probably has no need for pausing a stream.

These APIs are used by all front ends (Classic GUI, PendantUI and UGS Platform).

# Plugin
The UGS Platform is built ontop of the NetBeans Platform. This gives us powerful tools to work with, including a robust plugin system. The heart of the UGS Platform is a module which wraps and exposes the Universal Gcode Sender JAR file - the same jar you could execute to run the Classic GUI! Other than using the UGSLib module, developing a plugin for the UGS Platform is exactly the same as developing any other NetBeans Platform plugin. And there is lots of great documentation for that, here is the [NetBeans Platform Plugin Quick Start](https://netbeans.apache.org/tutorial/main/tutorials/nbm-google/) guide.

See this tutorial on how to create a new module: [Developing a new module](Developing-a-new-module)


# Gcode processor
The UGS core library has a flexible gcode processor plugin system. It is designed as a processing pipeline to convert one line of code at a time by passing it through multiple **Command Processor** plugins. Some advanced features in UGS, like the Auto Leveler, take advantage of this feature to inject a special processor module into the gcode processing pipeline. Other processors are simpler, such as the **M30Processor** which simply removes unwanted 
**M30** commands, or the **CommandLengthProcessor** which causes an error if the final processed line has too much data for your controller.

This process is configured using a JSON file which holds processor configuration, order in which processors should appear in the pipeline, and whether or not they are enabled. All of this is configurable in UGS and UGP in a **Gcode Processor Configuration** menu.
