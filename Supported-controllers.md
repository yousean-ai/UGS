
| Controller     | Streaming file | GCode states | Mco | Wco | Jogging | Homing | Settings | Overrides |
| -------------- |----------------|--------------|-----|-----|---------|--------|----------|-----------|
| GRBL 1.1+      | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| GRBL 0.9       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| GRBL 0.8       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| TinyG          | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | |
| g2core 101.03+ | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | :heavy_check_mark: |
| Smoothieware   |  |  |  |  |  |  |  |  |

* **Controller** - the controller firmware and its version number
* **Streaming file** - if streaming a file, pausing and stopping is supported
* **GCode** - the controller is a big state machine storing a bunch of parameters such as current units (mm/inch), work offsets, coordinate system. To visualise these in UGS we need to store the same states.
* **Mco** - Machine coordinate system is coordinates the absolute coordinates of the machine.
* **Wco** - Work coordinate system or offset can be configured by the user to have a relative coordinate space to work in. These are needed for positioning the tools around the material.
* **Jogging** - If manually moving the machine by stepping/jogging is supported.
* **Homing** - Homing will determine the absolute zero for the machine position
* **Settings** - If firmware settings can be altered through the machine
* **Overrides** - If runtime overrides are supported for feed and spindle speeds.