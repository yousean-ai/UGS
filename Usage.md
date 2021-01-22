* [UGS Platform](#ugs-platform)
  * [Resizing windows](#resizing-windows)
  * [Toolbox](#toolbox)
  * [Connecting to the machine](#connecting-to-the-machine)
  * [Digital read-out](#digital-read-out)
  * [GCode Editor](#gcode-editor)
  * [Gamepad and Joystick](#gamepad-and-joystick)
  * [Outline](#outline)

# UGS Platform
The UGS Platform is the next generation of Universal Gcode Sender. It is built ontop of the Netbeans Platform which allows us to leverage its mature modular framework. This platform allows more features to be added without compromising on code quality, or being bogged down by a home grown framework. The Classic GUI is used as a library, so core features benefit both interfaces.

## Resizing windows
All windows and modules can be resized and moved to different locations.

![Resizing windows](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/2.0_platform_resizing_windows.gif)

## Toolbox
The toolbox is a window with common actions needed to operate the machine. The actions displayed are customizable so that only the buttons you use are available. If an action can't be used at the moment it will be greyed out, ie when no machine is connected or a file loaded.

![Toolbar](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/toolbox.gif)

## Connecting to the machine
The first thing you will do after powering up your machine is connecting to your controller using the toolbar at the top of the program.

Select the correct hardware in the firmware combo box:

![Firmware combo box](https://winder.github.io/ugs_website/img/guide/platform/connect_firmware.png)

Refresh the serial ports list and select the correct port for your hardware. If you can't find the correct port in the list, make sure you have the drivers installed.

![Serial port](https://winder.github.io/ugs_website/img/guide/platform/connect_serial_port.png)

The ports are usually named like this:
- **MacOSX**: /dev/tty.usbmodem* or /dev/tty.usbserial*
- **Linux**: /dev/ttyUSB* or /dev/ttyACM*
- **Windows**: COM1, COM2 and so on.

Select the correct baud rate for your controller.
- **GRBL** - version 0.9 or later are using 115200, earlier versions are using 9600.
- **TinyG/g2core** will adapt to the baud rate you are connecting with so it really doesn't matter.

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

## GCode Editor

UGS has a built in editor that allows you to open and edit a GCode file:

![Open editor](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/editor-open.gif)

The editor window can be moved around and changes to the gcode file can be viewed directly in the visualizer window. The selected lines in the editor will also be highlighted.

![Move editor window](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/editor-with-visualizer.gif)

When connected to a controller it can also highlight and display warnings for gcode commands that may not be compatible with the current controller. It will also highlight commands that contains errors. 

![GCode compatibility with connected controller](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/editor-syntax-highlight.gif)

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

## Outline
Outline will move the tool around the gcode model to make sure that the program can be runned properly. It will only move the XY-positions at the current set Z-height.

![Outline](https://user-images.githubusercontent.com/8962024/71760967-826f7900-2ec5-11ea-8395-b89c074d6d25.gif)

