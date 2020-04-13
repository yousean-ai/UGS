## Installing on a Raspberry Pi
As of version 1.0.6 Universal Gcode Sender should work out of the box on Raspberry Pi running [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) (just a couple of tweaks).

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

### Download and start

#### Download and start UGS Platform

Download UGS Platform for RaspberryPI from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads

```
unzip -o ugsplatform.zip
./ugsplatform/bin/ugsplatform
```

Open the preferences and change the connection driver to **JSSC**, otherwise the connection to the CNC controller will be unpredictable.

![Connection driver](https://user-images.githubusercontent.com/8962024/40659348-4a279b84-634e-11e8-91f6-19bcc6f0e16e.png)


#### Download and start UGS Classic

Start with installing Java, run these commands from the terminal: 
```bash
apt-get update
apt-get install openjdk-11-jdk
```

Make sure your system is using the correct JDK:
```bash
java -version
```

```
openjdk 11.0.5 2019-10-15
OpenJDK Runtime Environment (build 11.0.5....)
OpenJDK Server VM (build 11.0.5...)
```

Download UGS classic from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads

Unpack it and start:
```bash
unzip -o UniversalGcodeSender.zip -d ugs
chmod +x ugs/start.sh
./ugs/start.sh
```

## Building on Raspberry Pi
Building UGS on a Raspberry Pi is slow but is possible. But there is a limitation in the pendant UI module build script which can't be built on Raspberry Pi and needs to be disabled. Follow the instructions as follows. 

### Install Java and Maven
Then we need to install Java, run these commands from the terminal: 
```bash
apt-get update
apt-get install openjdk-11-jdk maven
```

Make sure your system is using the correct JDK:
```bash
java -version
```

```
openjdk 11.0.5 2019-10-15
OpenJDK Runtime Environment (build 11.0.5....)
OpenJDK Server VM (build 11.0.5...)
```

### Download the source for UGS

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