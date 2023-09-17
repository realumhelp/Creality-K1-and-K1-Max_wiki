You can improve Bed Mesh just changing the interpolation from lagrange to bicubic.

<br />

- Open `printer.conf` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Search macro named `[bed_mesh]` setting and add this lines at the end:

  ```
  algorithm: bicubic
  bicubic_tension: 0.1
  ```

  Like that:

  ```
  [bed_mesh]
  speed: 150
  mesh_min: 5,5
  mesh_max: 295,295
  probe_count: 6,6
  fade_start: 3.0
  fade_end: 10.0
  algorithm: bicubic
  bicubic_tension: 0.1
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- Start a new bed leveling with `BED_LEVELING` macro.

  This is my result:

  <img width="1385" alt="Capture d’écran 2023-08-04 à 15 45 27" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/963d1a06-b4ad-4ce8-8ebe-74170c9d9ccc">

  <img width="2545" alt="Capture d’écran 2023-08-04 à 15 19 16" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/c0ad53f3-da62-45c9-a85a-57336a39036f">


- If you want to run Bed Leveling manually, add this macros at the bottom of `gcode_macro.cfg` file:

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
    M84
  ```

  <u>Note:</u> Some K1 printers don't have `filament_sensor_2`, so you can remove this lines of the macro above:

  ```
    SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=0

    SET_FILAMENT_SENSOR SENSOR=filament_sensor_2 ENABLE=1
  ```

<br />