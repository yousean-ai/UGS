Different controllers and their versions are supported differently in UGS. We strive to make the user experience similar across different hardware/firmwares. This is a list of some of the basic capabilities and how they are supported in UGS.

| Controller | [File](#file) | [G-states](#g-states) | [Mco](#mco) | [Wco](#wco) | [Jog](#jog) | [Home](#home) | [Settings](#settings) | [Overrides](#overrides) |
| -------------- |------|----------|-----|-----|-----|------|----------|-----------|
| GRBL 1.1+      | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| GRBL 0.9       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| GRBL 0.8       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| [grblHAL](https://github.com/terjeio/grblHAL) | ? | ? | ? | ? | ? | ? | ? | ? |
| [Grbl_Esp32](https://github.com/bdring/Grbl_Esp32) | ? | ? | ? | ? | ? | ? | ? | ? |
| [FluidNC](https://github.com/bdring/FluidNC) | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | :heavy_check_mark: |
| TinyG          | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | |
| g2core 101.03+ | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | :heavy_check_mark: |
| Smoothieware   | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  |  |
| Marlin | | | | | | | | |


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
Homing will move the machine to determine the absolute zero machine position which will be available in UGS as a homing button.

## Settings
If firmware settings can be altered through the machine

## Overrides
Overrides will allow the machine operator to increase or decrease the feed rate or spindle speed of the machine when a Gcode program is running. 