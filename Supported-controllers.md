Different controllers and their versions are supported differently in UGS. We strive to make the user experience similar for different hardware but not all features are possible to implement. This is a list of some of the basic capabilities and how they are supported in UGS.

| Controller | [File](#file) | [G-states](#g-states) | [Mco](#mco) | [Wco](#wco) | [Jog](#jog) | [Home](#home) | [Settings](#settings) | [Overrides](#overrides) |
| -------------- |------|----------|-----|-----|-----|------|----------|-----------|
| GRBL 1.1+      | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| GRBL 0.9       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| GRBL 0.8       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| TinyG          | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | |
| g2core 101.03+ | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | :heavy_check_mark: |
| Smoothieware   | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  |  |

## File
The minimum feature for sending, pausing and stopping a gcode file transfer to the controller.

## G-states
the controller is a big state machine storing a bunch of parameters such as current units (mm/inch), work offsets, coordinate system. To visualise these properly in UGS we need to store the same states. This tells if we support storing the Gcode state for the controller.

## Mco
Machine coordinate system is coordinates the absolute coordinates of the machine and is closely dependent on homing to be able to determine the machines zero position. The machine coordinate system is visible in the [DRO](Usage#digital-read-out).

## Wco
Work coordinate system or offsets can be configured by the user to have a relative coordinate space to work in. This coordinate system required for dynamic positioning of the tools around the material. The work coordinate system is visible in the [DRO](Usage#digital-read-out).

## Jog
Jogging or stepping makes it possible to position the machine and the tool around a material. Some controllers also enables continuous jogging.

## Home
Homing will determine the absolute zero for the machine position

## Settings
If firmware settings can be altered through the machine

## Overrides
If runtime overrides are supported for feed and spindle speeds.