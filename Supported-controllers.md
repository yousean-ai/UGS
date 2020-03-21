Different controllers and their versions are supported differently in UGS. We strive to make the user experience similar for different hardware. This is a list of some of the basic features and how they are supported.

| Controller     | File | G-states | Mco | Wco | Jog | Home | Settings | Overrides |
| -------------- |------|----------|-----|-----|-----|------|----------|-----------|
| GRBL 1.1+      | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| GRBL 0.9       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| GRBL 0.8       | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | |
| TinyG          | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | |
| g2core 101.03+ | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  | :heavy_check_mark: |
| Smoothieware   |  |  |  |  |  |  |  |  |

* **Controller** - the controller firmware and its version number
* **File** - if streaming a file, pausing and stopping is supported
* **G-states** - the controller is a big state machine storing a bunch of parameters such as current units (mm/inch), work offsets, coordinate system. To visualise these properly in UGS we need to store the same states. This tells if we support storing the Gcode state for the controller.
* **Mco** - Machine coordinate system is coordinates the absolute coordinates of the machine.
* **Wco** - Work coordinate system or offset can be configured by the user to have a relative coordinate space to work in. These are needed for positioning the tools around the material.
* **Jog** - If manually moving the machine by stepping/jogging is supported.
* **Home** - Homing will determine the absolute zero for the machine position
* **Settings** - If firmware settings can be altered through the machine
* **Overrides** - If runtime overrides are supported for feed and spindle speeds.