## MacOSX
TBD

## Linux

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

## Raspberry PI (with raspbian)
Refer to this page: [[Raspberry Pi]]

## Windows
TBD