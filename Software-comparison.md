To be able to build your own CNC machine you need three softwares for your tool chain. On this page we have attempted to create a comparison table with different options:

1. [CAD/CAM](#cadcam) - A software for drawing or designing the model and generate GCode files with machine code.
2. [Gcode sender](#gcode-sender) - A software that will connect to your hardware controller and send Gcode files or commands to it.
3. [CNC controller](#cnc-controllers) - A firmware and hardware that will control the motion of the stepper motors based on Gcode commands

## CAD/CAM
Gcode is a CNC machine programming language. To generate such instructions you could write the code yourself ([code reference](http://linuxcnc.org/docs/html/gcode.html)) or use a CAD/CAM-software which generates it from a 3D or 2D model. Here is a list with 
different softwares and their support for different file formats.

| Name                                                           | OS    | License     |  DWG | DXF| STL | Gcode | SVG | Bitmap trace |
| -------------------------------------------------------------- | ------| ----------- |  --- | ---| --- | ----- | ----- | ------ |
| [UGS Platform](http://winder.github.io/ugs_website/)           | M,W,L | GPLv3       | | :heavy_check_mark: | | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| [Fusion 360](https://www.autodesk.se/products/fusion-360/)     | M,W   | Commercial  | :heavy_check_mark: | :heavy_check_mark: | | :heavy_check_mark: ||
| [FreeCad](https://www.freecadweb.org/)                         | M,W,L | LGPLv2+     | :heavy_check_mark: | :heavy_check_mark: | | :heavy_check_mark: ||
| [Inventables Easel](http://easel.inventables.com/)             | Web   | Free to use | :heavy_check_mark: | :heavy_check_mark: | | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| [Kiri:Moto](https://grid.space/kiri/)                          | Web   | MIT         | | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: ||
| [Carbide Create](https://carbide3d.com/carbidecreate/)         |       |             | | | | | | |
| MakerCAM                                                       |       |             | | | | | | |
| [F-Engrave](https://www.scorchworks.com/Fengrave/fengrave.html)| W     | ?           | | | | | | |
| EstlCAM                                                        |       |             | | | | | | |
| CamBAM                                                         |       |             | | | | | | |
| [Templatemaker](https://www.templatemaker.nl/)                 | Web   | Free to use | | :heavy_check_mark: | | | :heavy_check_mark:| |
      
_* **OS:** L=Linux, M=MacOSX, W=Windows_ <br/>

## Gcode sender

A Gcode sender is a software that connects with your controller (GRBL, TinyG, G2core, Smoothieware, Marlin or FluidNC) and is able to stream a gcode file to it. There are many different awesome senders out there, here we've tried to create a comparison table. Please feel free to correct any errors.

| Name                                                 | OS    | Controllers | Language   | License | CLI | WebUI | Gamepad | Overrides | Editor |
| ---------------------------------------------------- | ------| ----------- | ---------- | ------- | --- | ----- | ------- | --------- | ------- |
| [UGS Platform](http://winder.github.io/ugs_website/) | L,M,W | G,T,G2,S    | Java       | GPLv3   | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| [UGS Classic](http://winder.github.io/ugs_website/)  | L,M,W | G,T,G2,S    | Java       | GPLv3   | :heavy_check_mark: | :heavy_check_mark: | :x: | :x: | :x: |
| [gSender](https://sienci.com/gsender/)               | L,M,W | G           | Javascript | GPLv3   |     | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| [bCNC](https://github.com/vlachoudis/bCNC)           | L,M,W | G,S         | Python     | GPLv2   |     | :heavy_check_mark: | | :heavy_check_mark: | :heavy_check_mark: | 
| [Chilipeppr](http://chilipeppr.com/)                 | L,M,W | G,T         | Javascript | GPLv2   |     | :heavy_check_mark: | | :heavy_check_mark: | :x: |
| [cnc.js](https://github.com/cncjs/cncjs)             | L,M,W | G,T,G2,S,M  | Javascript | MIT     |     | :heavy_check_mark: | :x: | :heavy_check_mark: | :x: |
| [Goko](https://goko.fr/)                             | L,M,W | G,T,G2      | Java       | GPLv3   |     |  | | |
| [CNC-GCode-Controller](https://github.com/pknoe3lh/cncgcodecontroller) | W?    | M | Java | MIT   |     |  | | |
| [SourceRabbit](https://github.com/nsiatras/sourcerabbit-gcode-sender)  | L,M,W | G | Java | GPLv2 | :x: | :x: | :x: | :x: | :x: |
| [Candle](https://github.com/Denvi/Candle)            | L,W   | G           | C++        | GPLv3   |     |  | | |
| [GRBLWeb](http://xyzbots.com/grblweb.html)           | L,M,W | G           | Javascript | AGPL    |     | :heavy_check_mark: | | |
| [Pronterface](http://www.pronterface.com/)           | L,M,W | M           | Python     | GPLv3   |     |  | | |
| [UCCNC](https://cncdrive.com/UCCNC.html)             | W     | ?           | ?          | ?       |     |  | | |
| [g2coregui](https://github.com/talpadk/g2coregui)    | L,M?  | G2          | Python     | ?       |     |  | | |
| [GrblGru](https://www.grblgru.com/)                  | W     | G,T,G2      | ?          | ?       |     |  | | |
| [Grbl Panel](https://github.com/gerritv/Grbl-Panel/) | W     | G           | VB.Net     | MIT     |     |  | | |
| [Planet CNC](https://planet-cnc.com/software/)       | W,M,L |             | ?          | ?       |     |  | | |
| [Grbl-GCode-Sender](https://github.com/terjeio/Grbl-GCode-Sender) | W | G  | C#         |  BSD-3-Clause License | | | | |
| [FabMo](http://gofabmo.org/)                         | W,M,L | G2          | Javascript | Apache-2.0 |  |  | | |
| [GridBot](https://github.com/GridSpace/grid-bot)     | L,M   | M           | Javascript | MIT     | :heavy_check_mark: | :heavy_check_mark: | | |
| [GRBL-Plotter](https://github.com/svenhb/GRBL-Plotter)| W    | G           | C#         | GPLv3   |     |  | | :heavy_check_mark: | :heavy_check_mark: |                    

_* **OS:** L=Linux, M=MacOSX, W=Windows_ <br/>
_* **Controllers:** G=GRBL, T=TinyG, G2=g2core, S=Smoothieware, M=Marlin_ <br/>
_* **CLI:** Command Line Interface for interacting with the software without a GUI_


## CNC controllers

| Name                                                         | License | Axises | Overrides          |
| ------------------------------------------------------------ | ------- | ------ | ------------------ |
| [GRBL](https://github.com/gnea/grbl)                         | GPLv3   | 3      | :heavy_check_mark: |
| [grblHAL](https://github.com/gnea/grbl)                      | GPLv3   | 6      | :heavy_check_mark: |
| [Grbl_Esp32](https://github.com/bdring/Grbl_Esp32)           | GPLv3   | 6      | :heavy_check_mark: |
| [FluidNC](https://github.com/bdring/FluidNC)                 | GPLv3   | 6      | :heavy_check_mark: |
| [TinyG](https://github.com/synthetos/TinyG)                  | GPLv2   | 4      | :x: |
| [g2core](https://github.com/synthetos/g2)                    | GPLv2   | 6      | :heavy_check_mark: |
| [Smoothieware](https://github.com/Smoothieware/Smoothieware) | GPLv3   | 4      | |
| [Marlin](https://github.com/MarlinFirmware/Marlin)           | GPLv3   | 3      | |

_* **Overrides** Ability to adjust feed rate, spindle speed in runtime_ <br/>
