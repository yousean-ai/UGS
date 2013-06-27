### Overview
Universal G-Code Sender has three layers: **GUI**, **controller**, and **communicator**. The GUI is a visual representation of the CNC machine and contains a controller object which it uses to control the machine. The controller object contains a communicator object which it uses for sending data to the CNC firmware. The controller is also responsible for encapsulating commands for the communication layer and interpreting responses, then re-encapsulating results for return to the GUI. Finally the communication layer is responsible for maintaining a connection with the CNC machine and transmitting/retrieving data.

###  API Headers
These layers communicate from top to bottom by implementing a set of API interfaces, see [AbstractController.java](https://github.com/winder/Universal-G-Code-Sender/blob/master/src/com/willwinder/universalgcodesender/AbstractController.java) and [AbstractCommunicator](https://github.com/winder/Universal-G-Code-Sender/blob/master/src/com/willwinder/universalgcodesender/AbstractCommunicator.java) for those APIs. From the bottom back up to the top an object listener API is used, for that refer to [SerialCommunicationListener.java](https://github.com/winder/Universal-G-Code-Sender/blob/master/src/com/willwinder/universalgcodesender/listeners/SerialCommunicatorListener.java) and [ControllerListener.java](https://github.com/winder/Universal-G-Code-Sender/blob/master/src/com/willwinder/universalgcodesender/listeners/ControllerListener.java) which define the status messages returned from the lower level classes.

### Top-to-bottom communication
An example of top to bottom communication can be seen in the code to send a command to GRBL:
```java
GrblController controller = new GrblController();
controller.openCommPort(port, portRate);
controller.queueStringForComm("G0 X20 Y15 Z0");
```
openCommPort and queueStringForComm are defined in the controller API, so if another firmware were to be implemented (such as TinyG) a new class named TinyGController could be created and will work exactly the same.

### Bottom-to-top communication
An example of bottom to top communication can be seen in the code which listens for console style messages from the controller class:
```java
controller.addListener(this);

 ...

public void messageForConsole(String msg, Boolean verbose) {
    if (verbose == false || this.showVerboseMessages == true) {
        this.consoleTextArea.append((verbose ? "[verbose]" : "") + msg);
    }
}
```

In this manner any firmware can implement the same listener API and communicate back to the GUI. This is exactly how the visualizer window works. The new window is added as a listener to the controller object and it automatically gets the same status messages as the main GUI window without adding any dependencies.

A connection between the control layer and the communication layer is done in exactly the same way, thus if a new serial library were to be implemented it could be swapped in without effecting the control layer.