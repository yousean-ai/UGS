* [Installing on a Raspberry Pi](#installing-on-a-raspberry-pi)
  * [Activate OpenGL driver](#activate-opengl-driver)
  * [Download and start UGS Platform](#download-and-start-ugs-platform)
  * [Download and start UGS Classic](#download-and-start-ugs-classic)
* [Building on Raspberry Pi](#building-on-raspberry-pi)
  * [Install Java and Maven](#install-java-and-maven)
  * [Download the source and build](#download-the-source-and-build)

## Installing on a Raspberry Pi
As of version 1.0.6 Universal Gcode Sender should work on Raspberry Pi running [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) if you apply a couple of tweaks in your RPi settings.

### Activate OpenGL driver
Raspbian comes with the proprietary video driver VC4 which is not supported by the OpenGL-library that UGS is using. To use the visualizer you need to activate one of the other drivers and remove/move the vc4-libraries.

Make sure your system is up to date:
```bash
sudo apt-get update
sudo apt-get dist-upgrade
```

Configure the video driver:
```bash
sudo raspi-config
```
* Choose "7 Advanced Options"
* Choose "A7 GL Driver"
  * Choose "G2 GL (Fake KMS)" if you are using a touch screen otherwise the pi will crash on startup, could be related to this bug: https://github.com/raspberrypi/firmware/issues/1204).
  * Choose "G3 GL (Full KMS)" if you are using an external screen.
* Then Finish and reboot

Remove/Move the old video driver
```bash
sudo mv /opt/vc /opt/vc.old
sudo reboot
```

### Download and start UGS Platform

Download UGS Platform for RaspberryPI from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads

```
# Makes sure you have the permission to connect to the USB controller
sudo usermod -a -G dialout pi

mkdir ugs
cd ugs

# Use command below with link address from downloads page for your platform
wget https://ugs.jfrog.io/ugs/UGS/v2.0.7/ugs-platform-app-pi.tar.gz   

# Use command below to unzip the file downloaded above
tar zxvf ugs-platform-app-pi.tar.gz
```
Navigate in file explorer to: /home/pi/ugs/ugsplatform-pi/bin/ugsplatform and run 'ugsplatform'.
Create a desktop shortcut by selecting the file and clicking 'create link' from the edit menu.

Open the preferences and change the connection driver to **JSSC**, otherwise the connection to the CNC controller will be unpredictable.

![Connection driver](https://user-images.githubusercontent.com/8962024/40659348-4a279b84-634e-11e8-91f6-19bcc6f0e16e.png)


### Download and start UGS Classic

Start with installing Java, run these commands from the terminal: 
```bash
apt-get update
apt-get install openjdk-8-jdk
```

Make sure your system is using Java 8 (1.8.xx):
```bash
java -version
```

```
java version "1.8.0_65"
Java(TM) SE Runtime Environment (build 1.8.0_65-b17)
Java HotSpot(TM) Client VM (build 25.65-b01, mixed mode)
```

Download UGS classic from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads

Unpack it and start:
```bash
unzip -o UniversalGcodeSender.zip -d ugs
chmod +x ugs/start.sh
./ugs/start.sh
```

Open the preferences and change the connection driver to JSSC, otherwise the connection to the CNC controller will be unpredictable.



## Building on Raspberry Pi
Building UGS on a Raspberry Pi is slow but is possible. But there is a limitation in the pendant UI module build script which can't be built on Raspberry Pi and needs to be disabled. Follow the instructions as follows. 

### Install Java and Maven
Then we need to install Java, run these commands from the terminal: 
```bash
apt-get update
apt-get install openjdk-8-jdk maven
```

Make sure your system is using the correct JDK:
```bash
java -version
```

```
java version "1.8.0_65"
Java(TM) SE Runtime Environment (build 1.8.0_65-b17)
Java HotSpot(TM) Client VM (build 25.65-b01, mixed mode)
```

### Download the source and build

Download the latest source and unzip it
```
wget https://github.com/winder/Universal-G-Code-Sender/archive/master.zip
unzip -o master.zip 
```

Build without the pendant UI module by disabling the profile:
```
cd master
mvn install -P '!create-pendant-web-ui'
```