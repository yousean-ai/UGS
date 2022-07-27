* [Configuring the Controller](#configuring-the-controller)
  * [Firmware settings](#firmware-settings)
  * [Setup Wizard](#setup-wizard)
* [UGS Platform](#configuring-ugs-platform)
  * [Configuration files](#configuration-files)
  * [Log files](#log-files)
  * [Toolbar](#configuring-the-toolbar)
  * [Panels and windows](#configuring-panels-and-windows)
  * [Visualizer colors](#configuring-the-visualizer-colors)
  * [Macros](#configuring-macros)
  * [Using dark theme](#using-dark-theme)
  * [Gamepad and joystick](#gamepad-and-joystick)
* [UGS Classic](#configuring-ugs-classic)
  * [Configuration files](#configuration-files-1)

## Configuring the Controller

### Firmware settings
> The firmware settings is available for GRBL, TinyG and g2core

Your controller firmware settings is available in a configuration dialog and will let you tweak the inner workings of your hardware. It is available in both the UGS Classic and UGS Platform edition:
* UGS Classic - Open the menu `Settings → Firmware Settings`
* UGS Platform - Open the menu `Machine → Firmware Settings`

### Setup Wizard
> The setup wizard is currently only available in the UGS Platform edition and GRBL. 

Setting up your controller firmware configuration by hand can be challenging and may require a lot of documentation reading. The **Setup Wizard** will help you set up your controller without the need to know how to _create bitmasks_ and what features are dependent on another. 

* To start the wizard open the menu `Machine -> Setup wizard...` <br/><br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-1.png" alt="Start the setup wizard"/>
* If you aren't connected to your controller a connection dialog will be presented: <br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-2.png" width="80%" alt="Connect to controller"/>
* The version of the controller will be shown after connecting and the available setup steps will be loaded for your controller:<br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-3.png" width="80%" alt="Connected controller"/>
* If you have a settings file from your machine manufacturer or if you have a backup of your settings you may import it here:<br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-4.png" width="80%" alt="Import settings"/>
* On the motor wiring configuration page you can test the direction of your motors and change its direction if needed. <br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-5.png" width="80%" alt="Motor wiring configuration"/>
* On the step calibration page you can move the machine and measure the actual distance. It will then recommend a step setting for your machine: <br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-6.png" width="80%" alt="Step calibration"/>
* If you have limit switches you may enable them on this page and test if they are firing correctly: <br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-7.png" width="80%" alt="Limit switches"/>
* If limit switches are enabled you may enable homing as well. This page helps you figuring out in which direction the homing should be made: <br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-8.png" width="80%" alt="Homing setup"/>
* If homing is enabled you may also configure soft limits so that the controller knows if it can process a command without triggering limit switches: <br/><img src="http://winder.github.io/ugs_website/img/guide/platform/setup_wizard-9.png" width="80%" alt="Soft limits setup"/>





## Configuring UGS Platform

### Configuration files
The configuration for UGS Platform is divided into two types; the UGS specific settings and one for the user interface (ex. describing how the different windows should be placed and so on).

The UGS specific settings (which is also common with the UGS Classic edition) is located in your home directory. 
It contains `UniversalGcodeSender.json` which holds the settings such as: jog feed rates, your macros, your file history and so on. There is also the directory `firmware_config` which contains several configurations for different types firmwares.
* **Windows**: c:/users/[your username]/.ugs
* **Mac**: ~/Library/Preferences/ugs
* **Linux**: ~/.ugs 

The UGS platform settings is located in your home directory. These settings contains the positions of the windows, and which modules you have loaded:
* **Windows**: C:/users/[your username>]/.ugsplatform
* **Mac**: ~/Library/Application Support/ugsplatform
* **Linux**: ~/.ugsplatform

### Log files
When creating an issue it is often helpful for us to trace the error in your log file. These are located here:
* **Windows 7 and higher**: C:/Users/[your username>]/.ugsplatform/2.X/dev/var/log/messages.log
* **Windows XP**: C:/Documents and Settings/[your username>]/.ugsplatform/2.X/dev/var/log/messages.log
* **Mac**: ~/Library/Application Support/ugsplatform/2.X/dev/var/log/messages.log
* **Linux**: ~/.ugsplatform/2.X/dev/var/log/messages.log

### Configuring the toolbar
See [Usage / Toolbar](Usage#toolbar)

### Configuring panels and windows
All panels and windows can be resized and moved to different locations by dragging and dropping them:

![Resizing windows](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/2.0_platform_resizing_windows.gif)

### Disable the Welcome tab
To disable the welcome tab you need to uncheck this checkbox:
![image](https://user-images.githubusercontent.com/8962024/181166725-f1366424-3d2d-4ec3-afcd-1e4f4c4bd790.png)

### Configuring the visualizer colors
TBD

### Configuring Macros
TBD

### Using dark theme
There is a dark theme (Look and Feel) in UGS that can be enabled through the settings:
* Open the preferences:<br/>
![Open preferences](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/dark_laf1.png)
* Go to `Apperance -> Look and feel` and choose *FlatLaf Dark*:<br/>
![Select FlatLaf dark](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/dark_laf2.png)
* Restart and the dark themed UGS is used:<br/>
![UGS with FlatLaf dark](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/dark_laf3.png)

### Gamepad and joystick
See [Usage / Gamepad and joystick](Usage#gamepad-and-joystick)

## Configuring UGS Classic

### Configuration files
The UGS settings (which is also common with the UGS Platform edition) is located in your home directory. It contains `UniversalGcodeSender.json` which holds the settings such as: jog feed rates, your macros, your file history and so on. There is also the directory `firmware_config` which contains several configurations for different types firmwares.
* **Windows**: c:/users/[your username]/.ugs
* **Mac**: ~/Library/Preferences/ugs
* **Linux**: ~/.ugs 
