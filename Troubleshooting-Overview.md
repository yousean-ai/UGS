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

The exact path varies between the major operating systems because of where they keep user data. The [Official UGS website](http://winder.github.io/ugs_website) lists the [locations of property and preference files](http://winder.github.io/ugs_website/guide/troubleshooting/#property-files).

### Java Version
Currently UGS Platform requires Java 8. More recent versions of Java may or may not work. Ticket [#1151](https://github.com/winder/Universal-G-Code-Sender/issues/1151) shows how to change Java versions for several operating systems.

### Other problems
If UGS is still not starting properly, we encourage gathering and looking through the `messages.log` file for clues, then asking for help on the Google Group, attaching the most recent log / post them to somewhere like Pastebin or create a Github Gist. `messages.log` [can be found at these locations](http://winder.github.io/ugs_website/guide/troubleshooting/#property-files) depending on your OS.

# Open Issues
Found a problem? Check the [list of open issues](https://github.com/winder/Universal-G-Code-Sender/issues) and see if someone is already working on it.