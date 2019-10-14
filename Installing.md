Generally all you need is to install [Java 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) or later, then download the binary distribution of Universal Gcode Sender from [here](https://github.com/winder/Universal-G-Code-Sender#downloads). For specific instructions for different operating systems see below.

### MacOSX
* Download and install Java from [here](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html):
* Download UGS (either classic or platform edition) from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads
* Unpack the Universal Gcode Sender package and run the start script

Classic version: 
```bash
unzip -o UniversalGcodeSender.zip -d ugs
chmod +x ugs/start.sh
./ugs/start.sh
```

Platform version:
```
unzip -o ugs-platform-app-2.0-SNAPSHOT.zip
./ugsplatform/bin/ugsplatform
```

### Linux

Make sure your system is up to date:
```bash
sudo apt-get update
sudo apt-get upgrade
```

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

Download UGS (either classic or platform edition) from the download link: https://github.com/winder/Universal-G-Code-Sender#downloads

Classic version:
```bash
unzip -o UniversalGcodeSender.zip -d ugs
chmod +x ugs/start.sh
./ugs/start.sh
```

Platform version:
```
unzip -o ugsplatform.zip
./ugsplatform/bin/ugsplatform
```

### Raspberry PI (with raspbian)
Refer to this page: [[Raspberry Pi]]

### Windows
TBD