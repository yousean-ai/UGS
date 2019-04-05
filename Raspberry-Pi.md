As of version 1.0.6 Universal Gcode Sender should work out of the box on Raspberry Pi (or Asus Tinker Board).

## Install Java
First of all we need to install Java, run these commands from the terminal: 
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

## Download and start UGS
Download one of the versions of UGS from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads

Classic version:
```bash
wget -O UniversalGcodeSender.zip http://bit.ly/2ErycR3
unzip -o UniversalGcodeSender.zip -d ugs
chmod +x ugs/start.sh
./ugs/start.sh
```

Platform version:
```
wget -O ugsplatform.zip http://bit.ly/2R5zw2F
unzip -o ugsplatform.zip
./ugsplatform/bin/ugsplatform
```

## Change the connection driver
Make sure UGS uses the **JSSC** connection driver, otherwise the connection to the CNC controller will be unpredictable.

![Connection driver](https://user-images.githubusercontent.com/8962024/40659348-4a279b84-634e-11e8-91f6-19bcc6f0e16e.png)