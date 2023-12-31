Here you can fin useful macros can be used. Copy them in `gcode_macro.cfg` file.

<br />

## Input Shaper

This macros are already mentioned in [Fix issue with Input Shaper](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Fix-issue-with-Input-Shaper) section.

  ```
  [gcode_macro INPUT_SHAPER]
  description: Measure X and Y axis resonances
  gcode:
    G90
    {% if printer.toolhead.homed_axes != "xyz" %}
      G28
    {% endif %}
    SHAPER_CALIBRATE
    {% set y_park = printer.toolhead.axis_maximum.y/2 %}
    {% set x_park = printer.toolhead.axis_maximum.x|float - 10.0 %}
    G1 X{x_park} Y{y_park} F20000
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
    G1 Z10 F600
    M106
    PID_CALIBRATE HEATER=heater_bed TARGET={params.BED_TEMP|default(70)}
    M107
    {% set y_park = printer.toolhead.axis_maximum.y/2 %}
    {% set x_park = printer.toolhead.axis_maximum.x|float - 10.0 %}
    G1 X{x_park} Y{y_park} F20000
  ```

  You can select Bed temperature you want for PID calibration:

  <img width="600" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Useful-Macros/Macro_01.png">

<br /><br />

  ```
  [gcode_macro PID_HOTEND]
  description: Start Hotend PID
  gcode:
    G90
    {% if printer.toolhead.homed_axes != "xyz" %}
      G28
    {% endif %}
    G1 Z10 F600
    M106
    PID_CALIBRATE HEATER=extruder TARGET={params.HOTEND_TEMP|default(250)}
    M107
    {% set y_park = printer.toolhead.axis_maximum.y/2 %}
    {% set x_park = printer.toolhead.axis_maximum.x|float - 10.0 %}
    G1 X{x_park} Y{y_park} F20000
    WAIT_TEMP_START
  ```

  You can select Hotend temperature you want for PID calibration:

  <img width="600" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Useful-Macros/Macro_02.png">


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
    G1 X{x_park} Y{y_park} F20000
    TURN_OFF_HEATERS
    SET_FILAMENT_SENSOR SENSOR=filament_sensor ENABLE=1
    SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=1
  ```

  You can define some parameters for Bed Leveling like Hotend and Bed temperatures or Probe count:

  <img width="600" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Useful-Macros/Macro_03.png">

<br /><br />

  > [!NOTE]
  > Some K1 don't have a second filament sensor defined. If you encounter this error when running some macros: <br />
  > **!! {"code":"key69", "msg": "The value 'filament_sensor_2' is not valid for SENSOR", "values": ["filament_sensor_2", "SENSOR"]}** <br />
  > Just remove or comment this lines:
  > ```  
  > SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=0
  > ```
  > and
  > ```
  > SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=1
  > ```

<br /><br />

## Automatic saving and loading Z-Offset

If you adjust Gcode Offset (aka Z Baby Stepping) during print it's necessary to save it after print to be used next time.

However, sometimes we forget to save it. With these macros you will never need to save it again and it will be automatically reloaded each time Klipper starts.

- In your `printer.cfg` file, add this lines:

  ```
  [save_variables]
  filename: /usr/data/printer_data/config/variables.cfg

  [respond]
  ```

- In your `gcode_macro.cfg` file, add this lines:

  ```
  [gcode_macro SET_GCODE_OFFSET]
  description: Saving Z-Offset
  rename_existing: _SET_GCODE_OFFSET
  gcode:
    {% if printer.save_variables.variables.zoffset %}
    {% set zoffset = printer.save_variables.variables.zoffset %}
    {% else %}
    {% set zoffset = {'z': None} %}
    {% endif %}
    {% set ns = namespace(zoffset={'z': zoffset.z}) %}
    _SET_GCODE_OFFSET {% for p in params %}{'%s=%s '% (p, params[p])}{% endfor %}
    {%if 'Z' in params %}{% set null = ns.zoffset.update({'z': params.Z}) %}{% endif %}
    {%if 'Z_ADJUST' in params %}
    {%if ns.zoffset.z == None %}{% set null = ns.zoffset.update({'z': 0}) %}{% endif %}
    {% set null = ns.zoffset.update({'z': (ns.zoffset.z | float) + (params.Z_ADJUST | float)}) %}
    {% endif %}
    SAVE_VARIABLE VARIABLE=zoffset VALUE="{ns.zoffset}"


  [delayed_gcode LOAD_GCODE_OFFSETS]
  initial_duration: 2
  gcode:
    {% if printer.save_variables.variables.zoffset %}
    {% set zoffset = printer.save_variables.variables.zoffset %}
    _SET_GCODE_OFFSET {% for axis, offset in zoffset.items() if zoffset[axis] %}{ "%s=%s " % (axis, offset) }{% endfor %}
    { action_respond_info("Loaded Z-Offset from variables.cfg file: %s" % (zoffset)) }
    {% endif %}
  ```

<br />