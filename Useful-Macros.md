Here you can fin useful macros can be used. Copy them in `gcode_macro.cfg` file.

<br />

<u>Note:</u> Some K1 don't have a second filament sensor defined. If you encounter this error when running some macros:

**!! {"code":"key69", "msg": "The value 'filament_sensor_2' is not valid for SENSOR", "values": ["filament_sensor_2", "SENSOR"]}**

Just remove or comment this lines in all macros:
  ```  
  SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=0
  ```
and
  ```
  SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=1
  ```

<br />

## Input Shaper

This macros are already mentioned in [Fix issue with Input Shaper](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Fix-issue-with-Input-Shaper) section.

  ```
  [gcode_macro INPUT_SHAPPER_X]
  description: Measure X axis resonances
  gcode:
    SET_FILAMENT_SENSOR SENSOR=filament_sensor ENABLE=0
    SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=0
    G90
    {% if printer.toolhead.homed_axes != "xyz" %}
    G28
    {% endif %}
    {% set POSITION_X = printer.configfile.settings['stepper_x'].position_max/2 %}
    {% set POSITION_Y = printer.configfile.settings['stepper_y'].position_max/2 %}
    G1 X{POSITION_X} Y{POSITION_Y} F6000
    G1 Z10 F600
    SHAPER_CALIBRATE AXIS=X
    SET_FILAMENT_SENSOR SENSOR=filament_sensor ENABLE=1
    SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=1
    END_PRINT_POINT_WITHOUT_LIFTING
    M84
  ```
  ```
  [gcode_macro INPUT_SHAPPER_Y]
  description: Measure Y axis resonances
  gcode:
    SET_FILAMENT_SENSOR SENSOR=filament_sensor ENABLE=0
    SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=0
    G90
    {% if printer.toolhead.homed_axes != "xyz" %}
    G28
    {% endif %}
    {% set POSITION_X = printer.configfile.settings['stepper_x'].position_max/2 %}
    {% set POSITION_Y = printer.configfile.settings['stepper_y'].position_max/2 %}
    G1 X{POSITION_X} Y{POSITION_Y} F6000
    G1 Z10 F600
    SHAPER_CALIBRATE AXIS=Y
    SET_FILAMENT_SENSOR SENSOR=filament_sensor ENABLE=1
    SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=1
    END_PRINT_POINT_WITHOUT_LIFTING
    M84
  ```

<br />

## PID Calibration

  ```
  [gcode_macro PID_BED]
  description: Start Bed PID
  gcode:
  G90
  {% if printer.toolhead.homed_axes != "xyz" %}
  G28
  {% endif %}
  {% set POSITION_X = printer.configfile.settings['stepper_x'].position_max/2 %}
  {% set POSITION_Y = printer.configfile.settings['stepper_y'].position_max/2 %}
  G1 X{POSITION_X} Y{POSITION_Y} F6000
  G1 Z10 F600
  M106
  PID_CALIBRATE HEATER=heater_bed TARGET={params.BED_TEMP|default(70)}
  M107
  END_PRINT_POINT_WITHOUT_LIFTING
  M84
  ```

  You can select Bed temperature you want for PID calibration:

  <img width="600" alt="Capture d’écran 2023-09-02 à 14 31 04" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/c081e460-2dc6-439c-84ce-0beb503ee01e">

<br /><br />

  ```
  [gcode_macro PID_HOTEND]
  description: Start Hotend PID
  gcode:
  G90
  {% if printer.toolhead.homed_axes != "xyz" %}
  G28
  {% endif %}
  {% set POSITION_X = printer.configfile.settings['stepper_x'].position_max/2 %}
  {% set POSITION_Y = printer.configfile.settings['stepper_y'].position_max/2 %}
  G1 X{POSITION_X} Y{POSITION_Y} F6000
  G1 Z10 F600
  M106
  PID_CALIBRATE HEATER=extruder TARGET={params.HOTEND_TEMP|default(250)}
  M107
  END_PRINT_POINT_WITHOUT_LIFTING
  WAIT_TEMP_START
  M84
  ```

  You can select Hotend temperature you want for PID calibration:

  <img width="600" alt="Capture d’écran 2023-09-02 à 14 31 17" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/2b1148d1-b90a-46d4-8cd2-99feb7f71e98">


<br />

## Bed Leveling

  In case you want to start a Bed Leveling manually.

  ```
  [gcode_macro BED_LEVELING]
  description: Start Bed Leveling
  gcode:
  {% if 'PROBE_COUNT' in params|upper %}
  {% set get_count = ('PROBE_COUNT=' + params.PROBE_COUNT) %}
  {%else %}
  {% set get_count = "" %}
  {% endif %}
  {% set bed_temp = params.BED_TEMP|default(50)|float %}
  {% set hotend_temp = params.HOTEND_TEMP|default(140)|float %}
  {% set nozzle_clear_temp = params.NOZZLE_CLEAR_TEMP|default(240)|float %}
  SET_FILAMENT_SENSOR SENSOR=filament_sensor ENABLE=0
  SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=0
  {% if printer.toolhead.homed_axes != "xyz" %}
  G28
  {% endif %}
  BED_MESH_CLEAR
  NOZZLE_CLEAR HOT_MIN_TEMP={hotend_temp} HOT_MAX_TEMP={nozzle_clear_temp} BED_MAX_TEMP={bed_temp}
  ACCURATE_G28
  M204 S5000
  SET_VELOCITY_LIMIT ACCEL_TO_DECEL=5000
  BED_MESH_CALIBRATE {get_count}
  BED_MESH_OUTPUT
  {% set y_park = printer.toolhead.axis_maximum.y/2 %}
  {% set x_park = printer.toolhead.axis_maximum.x|float - 10.0 %}
  G1 X{x_park} Y{y_park} F2000
  TURN_OFF_HEATERS
  SET_FILAMENT_SENSOR SENSOR=filament_sensor ENABLE=1
  SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=1
  END_PRINT_POINT_WITHOUT_LIFTING
  M84
  ```

  You can define some parameters for Bed Leveling like Hotend and Bed temperatures or Probe count:

  <img width="600" alt="Capture d’écran 2023-09-02 à 14 36 18" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/f4315ff3-dafd-4187-b9c3-f1db32d2f6b7">

<br />