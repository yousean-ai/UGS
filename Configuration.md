* [Controller](#configuring-the-controller)
  * [Firmware settings](#firmware-settings)
  * [Setup Wizard](#setup-wizard)
* [UGS Platform](#configuring-ugs-platform)
  * [Configuration files](#configuration-files)
  * [Configuring the toolbar](#configuring-the-toolbar)
  * [Configuring panels and windows](#configuring-panels-and-windows)
  * [Configuring the visualizer colors](#configuring-the-visualizer-colors)
  * [Configuring Macros](#configuring-macros)
* [UGS Classic](#configuring-ugs-classic)
  * [Configuring Macros](#configuration-files-1)

## Configuring the Controller

### Firmware settings
> The firmware settings is available for GRBL, TinyG and g2core

Your controller firmware settings is available in a configuration dialog and will let you tweak the inner workings of your hardware. It is available in both the UGS Classic and UGS Platform edition:
* UGS Classic - Open the menu `Settings → Firmware Settings`
* UGS Platform - Open the menu `Machine → Firmware Settings`

### Setup Wizard
> The setup wizard is currently only available in the UGS Platform edition and GRBL. 

Setting up your controller firmware configuration by hand can be challenging and may require a lot of documentation reading. The **Setup Wizard** will help you set up your controller without the need to know how to _create bitmasks_ and what features are dependent on another. 

To access it, open the menu `Machine ➞ Setup Wizard...`

These are the settings the setup wizard can help you with:
 * Import saved settings from file
 * Setup motor wiring to make sure motors run in the right direction
 * Calibrate your motor steps
 * Configure and test your limit switches
 * Configure and test homing
 * Configure the software limits creating a safe work area for your machine

## Configuring UGS Platform

### Configuration files
The configuration for UGS Platform is divided into two types; the UGS specific settings and one for the user interface (ex. describing how the different windows should be placed and so on).

The UGS specific settings (which is also common with the UGS Classic edition) is located in your home directory. 
* **Windows**: /home/user/ugs
* **Mac**: ~/Library/Preferences/ugs
* **Linux**: ~/ugs 

It contains `UniversalGcodeSender.json` which holds the settings such as: jog feed rates, your macros, your file history and so on. There is also the directory `firmware_config` which contains several configurations for different types firmwares.

### Configuring the toolbar
The toolbar can be configured by right clicking in the toolbar and choose `Customize`. From there new icons can be added and removed. New toolbars can be added or hidden.

![Toolbar customization](https://github.com/winder/Universal-G-Code-Sender/blob/master/pictures/customize_toolbar.gif)

### Configuring panels and windows
TBD

### Configuring the visualizer colors
TBD

### Configuring Macros
TBD

## Configuring UGS Classic

### Configuration files
The UGS settings (which is also common with the UGS Platform edition) is located in your home directory. 
* **Windows**: /home/user/ugs
* **Mac**: ~/Library/Preferences/ugs
* **Linux**: ~/ugs 

It contains `UniversalGcodeSender.json` which holds the settings such as: jog feed rates, your macros, your file history and so on. There is also the directory `firmware_config` which contains several configurations for different types firmwares.
