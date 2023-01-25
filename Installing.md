## Installing UGS Platform

### Windows

* Download `UGS Platform` for Windows from [here](https://github.com/winder/Universal-G-Code-Sender#downloads). 
* Unpack the `.zip`-package
* Start the program ```bin/ugsplatform64.exe```

![install-ugs-windows](https://user-images.githubusercontent.com/8962024/214525130-2151fa86-0798-4bf4-a8d9-58c8ab0770f9.gif)


### Linux

* Download `UGS Platform` for Linux from [here](https://github.com/winder/Universal-G-Code-Sender#downloads). 
* Unpack the `.tar.gz`-package
* Start the program ```bin/ugsplatform```

![install-ugs-linux](https://user-images.githubusercontent.com/8962024/210969002-cd873040-ff47-4638-a0b5-ff1709390017.gif)

### Raspberry PI
Use `Raspberry Pi OS 32-bit`, version Bullseye or later found [here](https://www.raspberrypi.com/software/operating-systems/).<br>
Note that `Raspberry Pi OS 64-bit` **will not work.**

* Download `UGS Platform` for Raspberry PI from [here](https://github.com/winder/Universal-G-Code-Sender#downloads). 
* Unpack the `.tar.gz`-package
* Start the program ```bin/ugsplatform```

### Mac OSX
* Download `UGS Platform` for MacOSX from [here](https://github.com/winder/Universal-G-Code-Sender#downloads). 
* Double click the `.dmg`-file.
* Drag the "Universal Gcode Platform" to your applications folder.
* Find the application in the Application folder and right click to open.<br/>There might be a warning that the application is not signed which you need to ignore.

![install-ugs-macosx](https://user-images.githubusercontent.com/8962024/210966015-bab21f42-1ad1-422f-98a4-d05c4735b02f.gif)


## Installing UGS Classic
<img alt="UGS Classic" src="https://raw.githubusercontent.com/winder/Universal-G-Code-Sender/master/pictures/1.0.6_command_table.png" width="400" />

### Windows
* Download and install **Java 8** from [here](https://java.com/en/download/)
* Download **UGS Classic** from [here](https://github.com/winder/Universal-G-Code-Sender#downloads)
* Unpack the zip package
* Run the start script ```start.bat```

### MacOSX
* Download and install **Java 8** from [here](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html):
* Download **UGS Classic** from [here](https://github.com/winder/Universal-G-Code-Sender#downloads)
* Unpack the zip package
* Run the start script ```start.sh```

### Linux Debian or Ubuntu

* Make sure your system is up to date:
```bash
sudo apt-get update
sudo apt-get upgrade
```

* Install Java: 
```bash
apt-get update
apt-get install openjdk-8-jdk
```

* Make sure your system is using Java 8 (1.8.xx):
```bash
java -version
```
```
java version "1.8.0_65"
Java(TM) SE Runtime Environment (build 1.8.0_65-b17)
Java HotSpot(TM) Client VM (build 25.65-b01, mixed mode)
```

* Download **UGS Classic** from [here](https://github.com/winder/Universal-G-Code-Sender#downloads)
* Run the start script ```start.sh```


