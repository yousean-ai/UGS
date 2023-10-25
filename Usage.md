* [UGS Platform](#ugs-platform)
  * [Connecting to the machine](#connecting-to-the-machine)
  * [Actions](#actions)
    * [Machine actions](#machine-actions)
    * [Program actions](#program-actions)
    * [Editor](#editor-actions)
  * [Visualizer](#visualizer)
  * [Toolbox](#toolbox)
  * [Toolbar](#toolbar)
  * [Digital read-out](#digital-read-out)
  * [Overrides](#overrides)
  * [Resizing windows](#resizing-windows)
  * [GCode Editor](#gcode-editor)
    * [Error highlighting](#error-highlighting)
    * [Run from a selected line](#run-from-a-selected-line)
    * [Settings](#editor-settings)
  * [Designer](#designer)
    * [Adding shapes from clipart library](#adding-shapes-from-clipart-library)
    * [Importing SVG, DXF or Carbide Create files](#importing-svg--dxf--or-carbide-create-files)
    * [Trace bitmap images](#trace-bitmap-images)
    * [Adding text](#adding-text)
  * [Gamepad and Joystick](#gamepad-and-joystick)
  * [Pendant](#pendant)

# UGS Platform
The UGS Platform is the next generation of Universal Gcode Sender. It is built on top of the Netbeans Platform which allows us to leverage its mature modular framework. This platform allows more features to be added without compromising on code quality, or being bogged down by a home grown framework. The Classic GUI is used as a library, so core features benefit both interfaces.

## Connecting to the machine
The first thing you will do after powering up your machine is connecting to your controller using the toolbar at the top of the program.

Select the correct hardware in the firmware combo box:

![Firmware combo box](https://winder.github.io/ugs_website/img/guide/platform/connect_firmware.png)

In older versions of UGS you need to manually refresh the serial ports list and select the correct port for your hardware. If you can't find the correct port in the list, make sure you have the drivers installed.

![Serial port](https://winder.github.io/ugs_website/img/guide/platform/connect_serial_port.png)

The ports are usually named like this:
- **MacOSX**: /dev/tty.usbmodem* or /dev/tty.usbserial*
- **Linux**: /dev/ttyUSB* or /dev/ttyACM* (you might have to [assign your account to a group](https://docs.arduino.cc/software/ide-v1/tutorials/Linux#please-read) to be able to access the serial port)
- **Windows**: COM1, COM2 and so on.

Select the correct baud rate for your controller.
- **GRBL** - version 0.9 or later use 115200, earlier versions use 9600.
- **TinyG/g2core** will adapt to the baud rate you are connecting with so it really doesn't matter.

## Actions
Actions are small commands that can be either sent to the controller or for controlling specific parts of a loaded gcode program. Most actions can be assigned to a keyboard short cut or be added to the toolbar or [Toolbox](#toolbox).

### Machine actions
Machine actions are used for sending specific commands to the controller. This could be for resetting alarms or setting the controller work position. These actions will be enabled/disabled depending on the state of the controller. For instance, most actions will be disabled when running a gcode program, or some actions will not be available when in an alarm state. Below are some of the most important actions to know about.

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-ugscore/src/main/resources/resources/icons/resetzero.svg"/>&nbsp;&nbsp;<b>Reset zero</b></summary><br/>

This will zero the current work coordinate to point [X0, Y0, Z0]. 

For detailed instructions on how CNC coordinate systems work, check out this video:
[Understanding G-code Coordinate Systems](https://youtu.be/fGtbkVJBXyE)

</details>

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-ugscore/src/main/resources/resources/icons/zero.svg"/>&nbsp;&nbsp;<b>Return to zero</b></summary><br/>

An action that will move the machine to the zero location [X0, Y0, Z0] in the current work coordinates. 
If the current Z position is equal to or below a _safe height_ it will first be moved to the Z safe height to avoid scratching the work piece. The safe height can be set in the "Sender settings".
![Sender settings](https://user-images.githubusercontent.com/8962024/147445951-83785274-8a1c-4ed7-b0d1-a0724c8eed13.png)
</details>

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-ugscore/src/main/resources/resources/icons/reset.svg"/>&nbsp;&nbsp;<b>Soft Reset</b></summary><br/>

An action that will reset the controller without switching off its power. This can be needed on some controllers to resolve a specific alarm.
</details>

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-ugscore/src/main/resources/resources/icons/lock.svg"/>&nbsp;&nbsp;<b>Unlock</b></summary><br/>

An action that will resolve a specific alarm state, for instance if the machine has been triggered with a hard limit which would indicate that the controller no longer know its current position and it would be unsafe to continue further movement. In this case it needs the user intervention.
</details>

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-ugscore/src/main/resources/resources/icons/home.svg"/>&nbsp;&nbsp;<b>Home</b></summary><br/>

An action that will perform a homing sequence by moving the machine to its absolute zero position, triggering the homing/hard limit switches. After this the machine reference coordinates are zeroed.
</details>

### Program actions
Program actions is generally only available when there is an loaded gcode file and allows for basic manipulation of the program.

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-ugscore/src/main/resources/resources/icons/outline.svg"/>&nbsp;&nbsp;<b>Outline</b></summary><br/>

This will move the machine around the currently loaded model outlining the work to be done. This can be useful if you want to check if the material is correctly positioned or if the tool will clear the fixtures. This action will only move the machine in X and Y coordinates at the current set Z height.
![Outline example](https://user-images.githubusercontent.com/8962024/71783552-96f86200-2fe8-11ea-95cc-55d10e38bda3.gif)
</details>

### Editor<a id="editor-actions"></a>
Editor actions will be shown in the editor toolbar for a currently loaded gcode file.

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-gcode-editor/src/main/resources/icons/follow.svg"/>&nbsp;&nbsp;<b>Follow gcode</b></summary><br/>

A toggle button which is available in the editor and used to toggle if the editor should select the currently sent gcode.

![Follow gcode](https://user-images.githubusercontent.com/8962024/212558669-a3139273-20bb-4bec-9cb3-f7d33139be6f.gif)
</details>


<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-gcode-editor/src/main/resources/icons/mirror.svg"/>&nbsp;&nbsp;<b>Mirror</b></summary><br/>

This will invert the currently loaded gcode and mirror it. Note that any commands that uses arcs (G2/G3) will be converted to small line segments.
</details>


<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-gcode-editor/src/main/resources/icons/rotate_left.svg"/>&nbsp;&nbsp;<b>Rotate left</b></summary><br/>

This will rotate the currently loaded gcode by 90 degrees counter clockwise. Note that any commands that uses arcs (G2/G3) will be converted to small line segments.
</details>


<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-gcode-editor/src/main/resources/icons/rotate_right.svg"/>&nbsp;&nbsp;<b>Rotate right</b></summary><br/>

This will rotate the currently loaded gcode by 90 degrees clockwise. Note that any commands that uses arcs (G2/G3) will be converted to small line segments.
</details>


<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-gcode-editor/src/main/resources/icons/translate.svg"/>&nbsp;&nbsp;<b>Translate to zero</b></summary><br/>

This will move the currently loaded gcode so that it starts at zero position. Note that any commands that uses arcs (G2/G3) will be converted to small line segments.
</details>

<details>
<summary>&nbsp;<img src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/ugs-platform/ugs-platform-gcode-editor/src/main/resources/icons/position.svg"/>&nbsp;&nbsp;<b>Insert position</b></summary><br/>

This action will insert the current work position to the currently loaded gcode file at the given position. This action is useful when for instance you want to "teach" the machine to move in a certain pattern. The user needs to make sure that the correct gcode state (G0/G1) is used.
</details>

## Visualizer
The visualizer will display the loaded gcode file and how it is positioned relative to the machine. To orient the visualizer you can rotate, pan and zoom  with the following methods.

* **Rotating** the model is done by pressing the left mouse button anywhere on the work area.
* **Panning** is done by pressing the SHIFT and the left mouse button anywhere on the work area.
* **Zooming** is done by scrolling the mouse wheel.

<img src="https://github.com/winder/Universal-G-Code-Sender/assets/8962024/85e8ca84-16d5-42be-83fc-9a925e815bca" alt="Image of the vizualiser" width=800/>

The machine tool position is represented with a yellow cone and displays its relative position to your work zero position.

![image](https://github.com/winder/Universal-G-Code-Sender/assets/8962024/98a82265-4074-42c7-947b-00a6094091dc)

## Toolbox
The toolbox is a window with common actions needed to operate the machine. The actions displayed are customizable so that only the buttons you use are available. If an action can't be used at the moment it will be greyed out, ie when no machine is connected or a file loaded.

![Toolbox](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/toolbox.gif)

## Toolbar
The toolbar can be configured by right clicking in the toolbar and choose `Customize`. From there new actions can be added and removed by dragging them out the desired position. New toolbars can be added or hidden.

![Toolbar customization](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/customize_toolbar.gif)

## Digital read-out
The Digital read-out (or Controller state) panel displays the current status of your machine such as the work/machine coordinates, machine/spindle speeds and gcode states.

![Controller state (DRO)](https://winder.github.io/ugs_website/img/guide/platform/controller_state.png)

* Shows both the machine and work coordinates
* It has buttons for zeroing the work coordinates for each axis
* Changeable work coordinates using simple mathematical expressions<br>You can either set an exact coordinate or, as an example, use the following # / 2 to divide the current position in half. The #-character will be replaced with current position. If you start your expression with * or / the current position is prepended.
* Shows the current machine state (Idle, Run, Jog, Alarm, etc.)
* Shows the current feed rate and spindle speed
* Shows the current GCode state (eg. the units currently being used G20/G21)
* Shows a alarm with the triggered limit switches

## Overrides
With the overrides plugin you can tweak the running session of a gcode program in real time. You can speed up/down the feed rate, spindle and the fast movement. To use, open the menu `Window -> Overrides`.

<img src="https://user-images.githubusercontent.com/8962024/220111717-e2a6b93c-c193-44f9-9bfe-105c8436f46f.png" alt="Overrides" width=400/>

## Resizing windows
All windows and modules can be resized and moved to different locations.

![Resizing windows](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/2.0_platform_resizing_windows.gif)

By default the layout should look something like this and consist of five default containers. Mostly you can drag windows around and place them where you like. New containers might get created depending how you dock the windows. And the windows should remember their positions.

![image](https://user-images.githubusercontent.com/8962024/230756199-30131bfd-129b-4046-9121-9ff63ff5d63e.png)

There are some restrictions though. The "Editor"-container can not be moved or removed. This houses the windows for any gcode or design file you open (along with the Welcome page). The editor will not remember its position if you try to move them. And any new file will load into the Editor container again. So unlike the other containers, the "Editor" container can never be removed, instead a gray empty area will be shown instead.

If your windows gets messed up you can allways revert to the default by using the menu option `Windows -> Reset windows`

## GCode Editor

UGS has a built in editor that allows you to open and edit a GCode files.

![Open editor](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/editor-open.gif)

The editor window can be moved around and changes to the gcode file can be viewed directly in the visualizer window. The selected lines in the editor will also be highlighted.

![Move editor window](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/editor-with-visualizer.gif)

### Error highlighting
When connected to a controller it can also highlight and display warnings for gcode commands that may not be compatible with the current controller. It will also highlight commands that contains errors. 

![GCode compatibility with connected controller](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/editor-syntax-highlight.gif)

### Run from a selected line

If a job has failed or needs to be rerun from a certain point in the gcode file you can simply select the line in the gcode file and choose "Run From...". The gcode model will be rerendered excluding the skipped lines. 

![Run from](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/run_from.gif)

### Editor settings
The editor will be shown by default when opening gcode files, this behavior can be disabled in the settings by unchecking the option ```Show editor when opening g-code files```:

<img alt="Disable editor" src="https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/editor-disable-settings.png" width="600"/>

## Designer
The designer is a really simple CAD/CAM tool which allows you to draw simple vector graphics or import SVG, DXF or [Carbide Create](https://cutrocket.com/)-files. The shapes can then be assigned to a tool path operation. The designer is intended to be a quick way to generate gcode and to get started with your machine.

<img alt="Designer" src="https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/2.0_platform_designer.png" width="800"/>

### Adding shapes from clipart library
The clipart library contains hundreds of symbols and pictures that can be easily added to your design:

<img alt="Importing clipart" src="https://user-images.githubusercontent.com/8962024/171702760-d597b30f-1646-459e-8b02-4ae086af4af9.gif" width="800"/>

### Importing SVG-, DXF- or Carbide Create files
With a design open, click the import button and select a file to import it:

<img alt="Importing SVG, DXF or Carbide Create files" src="https://user-images.githubusercontent.com/8962024/171700736-7ff10991-9d71-42c1-bca3-6dab14720d2e.gif" width="800"/>

### Trace bitmap images
With the trace tool, bitmap images can be imported into vector graphics

<img alt="Trace bitmap images" src="https://user-images.githubusercontent.com/8962024/171716179-a8074351-569a-4483-8439-59c78028b8d7.gif" width="800"/>

### Adding text
Adding text can be done using the text tool:

<img alt="Adding text" src="https://user-images.githubusercontent.com/8962024/171719053-779ec67c-2dbd-415e-a685-33ee832e0e57.gif" width="800"/>

## Gamepad and Joystick

Gamepads and joysticks are supported in UGS Platform. Note that in MacOSX you need a special driver to use a gamepad: https://github.com/360Controller/360Controller.

Connect your controller device and go to `Preferences -> UGS -> Joystick` and choose `Activate joystick`. If you now press your controller device inputs they will light up green in the settings screen. You can change any input mapping to an action in UGS:

<img alt="Gamepad settings" src="https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/gamepad-settings.png" width="500"/>

### Analog controls
For the analog controls there is a setting which will allow you to set a zero offset threshold. This is useful when you have a controller device input that doesn't return a zero value when not being touched. For some controllers the axises are inverted which can be fixed by enabling the `Reverse`-checkbox.

<img alt="Gamepad settings zero threshold" src="https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/gamepad-settings-zero.png" width="300"/>

### Gamepad layout
Different gamepads have slightly different layouts. This is an example of how the buttons are placed and a table with the buttons and their default mapping. Please test your controller in the settings dialog before using.

![Gamepad illustration](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/gamepad.png)

| Button    | Description   | Default mapping |
| --------- | ------------- | --------------- |
| A         |               | Z-              |
| B         |               |                 |
| X         |               |                 |
| Y         |               | Z+              |
| Back      |               | Stop            |
| Select    |               |                 |
| Start     |               | Start           |
| L1        |               | Divide jog feed rate |
| L2        | Analog button |
| L3        | Digital button|
| R1        |               | Multiply jog feed rate |
| R2        | Analog button | |
| R3        | Digital button| |
| Pad up    |               | Y+ |
| Pad down  |               | Y- |
| Pad left  |               | X- |
| Pad right |               | X+ |
| Left stick X | Analog button | Analog jog X |
| Left stick Y | Analog button | Analog jog Y |
| Right stick X | Analog button |             |
| Right stick Y | Analog button | Analog jog Z |

## Pendant
There is a web based pendant which allows you to control the machine via a web browser.<br/>It is normally accessible through [http://localhost:8080/](http://localhost:8080/) and looks like this:<br/>
![Pendant](https://user-images.githubusercontent.com/8962024/52661473-702dca80-2f02-11e9-8c4c-b0578b3eb58e.png)

We do not activate the feature by default and you need to start it by either pressing the pendant button each time you start UGS.<br/>
![Start pendant](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/2.0_platform_pendant.png)

You can also make it auto start each time you start UGS by activating it in the settings:<br/>
![Autostart pendant](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/2.0_platform_pendant_autostart.png)


