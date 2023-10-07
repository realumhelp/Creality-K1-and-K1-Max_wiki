Klipper Adaptive Meshing & Purging is an extension that allows you to generate a mesh only in the area you really need it: where you print!

Since the mesh area will be smaller, the mesh can be much more dense. Imagine making a 3x3 mesh, but the size of a [3DBenchy](https://www.3dbenchy.com/)!

KAMP also works if prints are started directly through the printer screen by checking the `Calibration` box before starting printing.

More info about KAMP here: [Github](https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging)

<br />

**<u>Note:</u> This procedure must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Installation

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Klipper Adaptive Meshing & Purging`:

  <img width="900" alt="Capture d’écran 2023-10-07 à 16 56 23" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/5406f40c-1ed3-43c6-a361-131ad65ae218">

<br />

## Configuration

-  Open `moonraker.conf` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Search `[file_manager]` section and change value of `enable_object_processing` setting to `True` like this:

  ```
  # Set to 'True' if you use KAMP
  enable_object_processing: True
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Open `printer.cfg` file and add this line to enable KAMP:

    ```
    [include KAMP_Settings.cfg]
    ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Open `gcode_macro.cfg` file, search macro named `[gcode_macro START_PRINT]` and disable `CX_PRINT_LEVELING_CALIBRATION` command by adding a `#` and add `BED_MESH_CLEAR` and `BED_MESH_CALIBRATE` commands like this: 

  ```
  [gcode_macro START_PRINT]
  variable_prepare: 0
  gcode:
    WAIT_TEMP_END
    CLEAR_PAUSE
    {% set g28_extruder_temp = printer.custom_macro.g28_ext_temp %}
    {% set bed_temp = printer.custom_macro.default_bed_temp %}
    {% set extruder_temp = printer.custom_macro.default_extruder_temp %}
    {% if 'BED_TEMP' in params|upper and (params.BED_TEMP|float) %}
    {% set bed_temp = params.BED_TEMP %}
    {% endif %}
    {% if 'EXTRUDER_TEMP' in params|upper and (params.EXTRUDER_TEMP|float) %}
    {% set extruder_temp = params.EXTRUDER_TEMP %}
    {% endif %}
  
    {% if printer['gcode_macro START_PRINT'].prepare|int == 0 %}
      {action_respond_info("not prepare.\n")}
      PRINT_PREPARE_CLEAR
      CX_ROUGH_G28 EXTRUDER_TEMP={extruder_temp} BED_TEMP={bed_temp}
      CX_NOZZLE_CLEAR
      ACCURATE_G28
      #CX_PRINT_LEVELING_CALIBRATION
      BED_MESH_CLEAR
      BED_MESH_CALIBRATE
    {% else %}
      PRINT_PREPARE_CLEAR
    {% endif %}
  
    CX_PRINT_DRAW_ONE_LINE
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Also make sure `Label Objects` setting is enabled in your slicer.

- It's done. You have now **Adaptive Meshing** when printing starting, the hotend which is parked next to the printing area during heating and the optimized purge line next to the printing area.

<br />