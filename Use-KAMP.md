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

  <img width="900" alt="Capture d’écran 2023-10-09 à 01 58 59" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/bac35dd7-6a81-4ada-a711-6f6d2b2c566d">

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

- Open `gcode_macro.cfg` file, search macro named `[gcode_macro START_PRINT]` and:

  - Replace `CX_PRINT_LEVELING_CALIBRATION` command by these:
    ```
    BED_MESH_CLEAR
    BED_MESH_CALIBRATE
    ```
  - Replace `CX_PRINT_DRAW_ONE_LINE` command by these:
    ```
    _SMART_PARK
    M109 S{extruder_temp}
    M190 S{bed_temp}
    _LINE_PURGE
    ```

  Like this:

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
      BED_MESH_CLEAR
      BED_MESH_CALIBRATE
    {% else %}
      PRINT_PREPARE_CLEAR
    {% endif %}
    _SMART_PARK
    M109 S{extruder_temp}
    M190 S{bed_temp}
    _LINE_PURGE
  ```

  <u>Note:</u> In case you don't define acceleration values in your slicer, it's necessary to add this command under the line `_LINE_PURGE` to load the default acceleration from the `printer.cfg` file:

  ```
  SET_VELOCITY_LIMIT ACCEL={printer.configfile.settings.printer.max_accel}
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Open the `moonraker.conf` file and enable this lines by removing `#` before (or add this lines if you don't have them) to have future updates, like this:

  ```
  # Remove '#' from the lines below if you use KAMP
  [update_manager KAMP for K1 Series]
  type: git_repo
  channel: dev
  path: /usr/data/KAMP-for-K1-Series
  origin: https://github.com/Guilouz/KAMP-for-K1-Series.git
  primary_branch: main
  is_system_service: False
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Also make sure `Label Objects` setting is enabled in your slicer.

  - For OrcaSlicer: In `Others` tab, check `Exclude objets` setting
  - For Creality Print: Under `Parameter Config`, check `Exclude Objets` setting in `Experimental` tab

- It's done. You have now **Adaptive Meshing** when printing starting, the hotend which is parked next to the printing area during heating and the optimized purge line next to the printing area.

<br />

In case you use Prusa Slicer, it's also needed to add more macros in your `gcode_macro.cfg` file:

  ```
  [gcode_macro DEFINE_OBJECT]
  gcode:
    EXCLUDE_OBJECT_DEFINE {rawparams}

  [gcode_macro START_CURRENT_OBJECT]
  gcode:
    EXCLUDE_OBJECT_START NAME={params.NAME}

  [gcode_macro END_CURRENT_OBJECT]
  gcode:
    EXCLUDE_OBJECT_END {% if params.NAME %}NAME={params.NAME}{% endif %}

  [gcode_macro LIST_OBJECTS]
  gcode:
    EXCLUDE_OBJECT_DEFINE

  [gcode_macro LIST_EXCLUDED_OBJECTS]
  gcode:
    EXCLUDE_OBJECT

  [gcode_macro REMOVE_ALL_EXCLUDED]
  gcode:
    EXCLUDE_OBJECT RESET=1
  ```

<br />