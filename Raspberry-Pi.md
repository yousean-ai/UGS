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
* Choose "A6 GL Driver"
* Choose "G1 GL (Full KMS)"
* Then Finish and reboot

Remove/Move the old video driver
```bash
sudo mv /opt/vc /opt/vc.old
sudo reboot
```

### Install Java
Then we need to install Java, run these commands from the terminal: 
```bash
apt-get update
apt-get install openjdk-8-jdk
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

### Download and start UGS
Download UGS (either classic or platform edition) from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads

Classic version:
```bash
wget -O UniversalGcodeSender.zip http://bit.ly/2GGgNF7
unzip -o UniversalGcodeSender.zip -d ugs
chmod +x ugs/start.sh
./ugs/start.sh
```

Platform version:
```
wget -O ugsplatform.zip http://bit.ly/2XANF7B
unzip -o ugsplatform.zip
./ugsplatform/bin/ugsplatform
```

### Change the connection driver
Make sure UGS uses the **JSSC** connection driver, otherwise the connection to the CNC controller will be unpredictable.

![Connection driver](https://user-images.githubusercontent.com/8962024/40659348-4a279b84-634e-11e8-91f6-19bcc6f0e16e.png)

## Building on Raspberry Pi
Due to a limitation in the pendant UI module build script, the software can't be completely built on an RaspberryPi. 

You would need to inactivate the pendant UI module by disabling the profile:
`mvn install -P '!create-pendant-web-ui'`