# Troubleshooting

## Is the problem UGS, the controller, or CAM?

Many issues and requests for help are not actually specific to UGS, some of these are related to connecting to the controller, while others are CAM related.

UGS has three simple primary missions:
1. Take G-code from your computer and send it to your controller.
1. Send signals to your controller for setting up jobs. Examples: jogging and setting WCS manually.
1. Displaying and changing controller status. Examples: seeing alarm statuses and clearing them, toggling coolant, or adjusting speed+feed overrides, or pausing the program.

UGS does have additional secondary missions through plugins. Some of these are:
1. Dowel pin creation.
1. Probe wizard to automatically set WCS.
1. Workflow manager to help with tool changes between separate programs.

If your problem doesn't fit into the above, it may be that the problem is actually outside of UGS. Things like the WCS moves mysteriously between restarts of the machine could be a controller issue. If the WCS moves between programs, this could be a CAM issue, particularly if you program multiple multiple work setups. This also assumes that the work is adequately secured to the machine and has not physically shifted. Markers/setup or gauge blocks/ruler/calipers and a cameraphone can be a great sanity check for this sort of thing depending on the scale one operates at.

## UGS Issues
TODO: writeme. Maybe link to an FAQ page.

## Controller Issues
### Connecting UGS to a controller such as Grbl / TinyG / Smoothie for the first time?
Be sure you have selected the correct serial port and speed.

If you don't know what this is, generally, it can be determined by [downloading Arduino](https://www.arduino.cc/en/main/software), and then selecting each port (Tools -> Port) then going to the serial monitor (Tools -> Serial Monitor), until you get a screen that shows some output that looks like coordinates, some help text, or some version information.

This process can also be used to rule out damaged or faulty boards, however, each type of board will have its own troubleshooting instructions for that. Board handling must be done with extreme care. Modern circuit boards have many components easily destroyed through static electricity.

### Grbl
#### Grbl + USB
The following information assumes connection to an official Arduino Uno board via a USB port, with a standard Grbl hex file. Some low cost Arduino clones have trouble, notably those using a `CH340` type chip. The official boards use a different chip which typically works straight away. Unofficial Grbl downloads and custom builds may use different speed settings.

Port: Varies slightly for each OS and style of Arduino board.
* Windows: Try `COMx` where `x` is a number. Examples: `COM6` or `COM12` for example. You may see `COM1` is often a dedicated serial port on the PC's motherboard. Very old Arduino boards use this style of connected, "D-sub 9", though incredibly rare.
* Linux: Try `/dev/ttyACMx` or `/dev/ttyAMAx` where `x` is a number (usually `0`). Example: `/dev/ttyAMA0`. You may see `/dev/ttyS0` as an option, this is the same as `COM1` in Windows.
* Mac OS X: Try `/dev/tty.usbmodemfdxxxx` where `xxxx` are some numbers.

Speed: for `v0.9` and newer speed: `115200`; for older than `v0.9` use `9600`.

If you are still having problems and you have a clone board, the `CH340` chip may be to blame. Some users have trouble, while others report success. It may be a certain combination of drivers and/or circuit layout that is to blame, and using a different Arduino board may be the answer. If you have a `CH340` chip and are running Windows or Mac OS X, check you have the drivers installed. `CH340` [Drivers for Windows](https://www.google.com/search?q=ch340+drivers+windows). `CH340` [Drivers for Mac OS X](https://www.google.com/search?q=ch340+driver+mac+os+x).

The [Grbl Wiki](https://github.com/grbl/grbl/wiki/Using-Grbl) has additional information.

#### Grbl + Network
The following assumes you have some sort of network to USB serial port sharing (such as `socat` on a Raspberry Pi), or a Grbl board that has an ethernet port, and that it is set up and tested to connect to the serial port already.

To configure UGS for Grbl + Network:
In UGS go to
1. `Tools` -> `Options`.
1. Click `UGS`.
1. Open the `Sender Options` tab.
1. For `Connection Driver` choose `TCPDriver` and click `OK`.
1. Back in the main page, under `Firmware` at the top choose `Grbl`.
1. For `Port`, type the IP address or hostname of your smoothie board.
1. For `Baud` type `23`.

### TinyG
TinyG has excellent and detailed [setup documentation](https://github.com/synthetos/TinyG/wiki/Connecting-TinyG#establish-usb-connection).

### Smoothie
Smoothie support is still open per issue [#204](/winder/Universal-G-Code-Sender/issues/204). Your mileage may vary.

#### Smoothie + USB
The process for connecting over USB remains the same for Grbl. The official Smoothie Wiki [USB page](http://smoothieware.org/usb) will help provide some specific details for the driver.

#### Smoothie + Network
There is also support for connecting over a network. The official Smoothie Wiki [network page](http://smoothieware.org/network) has instructions for setting up the configuration file. The main values you need under the network settings are:

```
network.enable                               true             # enable the ethernet network services
network.telnet.enable                        true             # enable the telnet server
```
The remaining network settings in Smoothie should be confirmed from the Smoothie wiki or sample configuration and checked against your local network. It is recommended to enable the webserver and check you can access it before configuring UGS.

To configure UGS for Smoothie + Network:
In UGS go to
1. `Tools` -> `Options`.
1. Click `UGS`.
1. Open the `Sender Options` tab.
1. For `Connection Driver` choose `TCPDriver` and click `OK`.
1. Back in the main page, under `Firmware` at the top choose `Smoothie`.
1. For `Port`, type the IP address or hostname of your smoothie board.
1. For `Baud` type `23`.

## CAM Issues
TODO: Writeme!
