## Is the problem UGS, the controller, or CAM?

Many issues and requests for help are not actually specific to UGS, some of these are related to connecting to the controller, while others are CAM related.

UGS has three simple primary missions:
1. Take G-code from your computer and send it to your controller.
1. Send signals to your controller for setting up jobs. Examples: Homing, Jogging and setting Work Coordinate System (WCS) manually.
1. Displaying and changing controller status. Examples: seeing alarm statuses and clearing them, toggling coolant, or adjusting speed+feed overrides, or pausing the program.

UGS does have additional secondary missions through plugins. Some of these are:
1. Dowel pin creation.
1. Probe wizard to automatically set WCS.
1. Workflow manager to help with tool changes between separate programs.

If your problem doesn't fit into the above, it may be that the problem is actually outside of UGS. The following table can help you figure out where to look:

| Description | Likely Components |
| --- | --- |
| Strange motion | Controller |
| Work Coordinate System changes between restarts of controller | Controller |
| Work Coordinate System changes between programs | CAM or Controller |
| [Unable to connect to controller](/winder/Universal-G-Code-Sender/wiki/Connecting-the-Controller) | Controller |

## UGS is not starting properly
### Recent Upgrade - Reset Preferences
If you have recently upgraded UGS and it has been a long time since the previous upgrade, sometimes the preference files need to be reset. Preferences are kept in a user directory called `.ugsplatform` for `v2.0` and `.ugs` for `v1.0`, and deleting (or renaming) this directory will reset UGS back to the defaults.

The exact path varies between the major operating systems because of where they keep user data. Check out these pages for where the settings are located:
* [UGS Platform](Configuration#configuring-ugs-platform)
* [UGS Classic](Configuration#configuring-ugs-classic)

### Java Version
Currently UGS Platform requires Java 8. More recent versions of Java may or may not work. Ticket [#1151](https://github.com/winder/Universal-G-Code-Sender/issues/1151) shows how to change Java versions for several operating systems.

### Other problems
If UGS is still not starting properly, we encourage gathering and looking through the `messages.log` file for clues, then asking for help on the Google Group, attaching the most recent log / post them to somewhere like Pastebin or create a Github Gist. `messages.log` [can be found at these locations](http://winder.github.io/ugs_website/guide/troubleshooting/#property-files) depending on your OS.

## "Grbl has not finished booting."
This happens when UGS connects to a serial port and does not receive the GRBL startup string. Typically this is caused by a configuration problem and can be solved by one of the following:

* Check the baud rate is 115200, or 9600 for very old versions of grbl.
* Make sure you are connecting to the correct port.
* Make sure you have installed any drivers required for your controller.
* Make sure GRBL is properly flashed on your controller.

## Program Slows Down and Send Freezes
If you notice slowness while running your program, it may mean UGS is running out of available memory. There are a couple things to try:

* Check the controller settings, and make sure "Arc Expander" is not enabled. This can take a small program and turn it into a very large one by converting arcs into many small movements.
* Increase the memory allocated to UGS by navigating the the installation directory. There is a folder named etc containing ugsplatform.conf, open this file with a simple text editor and modify the value of Xms to something like -J-Xms256m, or larger. [Additional details can be found here](http://wiki.netbeans.org/FaqSettingHeapSize)

# Open Issues
Found a problem? Check the [list of open issues](https://github.com/winder/Universal-G-Code-Sender/issues) and see if someone is already working on it.