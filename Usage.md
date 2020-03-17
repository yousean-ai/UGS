* [Platform](#platform)
  * [Connecting to the machine](#connecting-to-the-machine)
  * [Digital read-out](#digital-read-out)

## Platform
The UGS Platform is the next generation of Universal Gcode Sender. It is built ontop of the Netbeans Platform which allows us to leverage its mature modular framework. This platform allows more features to be added without compromising on code quality, or being bogged down by a home grown framework. The Classic GUI is used as a library, so core features benefit both interfaces.

### Connecting to the machine
The first thing you will do after powering up your machine is connecting to your controller hardware using the toolbar at the top of the program.

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

### Digital read-out
The Digital read-out (or Controller state) panel displays the current status of your machine such as the work/machine coordinates, machine/spindle speeds and gcode states.

![Controller state (DRO)](https://winder.github.io/ugs_website/img/guide/platform/controller_state.png)

* Shows both the machine and work coordinates
* It has buttons for zeroing the work coordinates for each axis
* Changeable work coordinates using simple mathematical expressions<br>You can either set an exact coordinate or, as an example, use the following # / 2 to divide the current position in half. The #-character will be replaced with current position. If you start your expression with * or / the current position is prepended.
* Shows the current machine state (Idle, Run, Jog, Alarm, etc.)
* Shows the current feed rate and spindle speed
* Shows the current GCode state (eg. the units currently being used G20/G21)
* Shows a alarm with the triggered limit switches