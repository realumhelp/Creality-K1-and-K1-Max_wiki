Here you can find different tips to improve fans control.

<br />

> [!NOTE]
> **This procedures must be repeated if you update the firmware or if you restore the printer to default settings.**

> [!IMPORTANT]
> **Make sure you have [[respond]](https://www.klipper3d.org/G-Codes.html#respond) Klipper function in your configuration files, some macros use it.**

<br />

## Improve hotend cooling at the end of printing

By default at the end of a print, the hotend is cooled by its fan which runs at 100%.

By making this change, the hotend fan speed will be reduced to 80% and the side fan will also be enabled at 40%. This allows faster and quieter cooling.

<br />

-  Open `gcode_macro.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Search macro named `[gcode_macro WAIT_TEMP_START]` and replace it by this one:

  ```
  [gcode_macro WAIT_TEMP_START]
  gcode:
    UPDATE_DELAYED_GCODE ID=wait_temp DURATION=1
    SET_PIN PIN=fan0 VALUE=210
    SET_PIN PIN=fan2 VALUE=210
  ```

- Then, search macro named `[gcode_macro WAIT_TEMP_END]` and replace it by this one:

  ```
  [gcode_macro WAIT_TEMP_END]
  gcode:
    UPDATE_DELAYED_GCODE ID=wait_temp DURATION=0
    M106 P0 S0
    M106 P2 S0
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

<br />

## Control chamber and motherboard fans

It's possible to trigger the back fan depending on the chamber temperature and the motherboard fan depending on the CPU temperature..

<br />

-  Open `printer.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- And add this lines:

  ```
  [duplicate_pin_override]
  pins: PC0, PC5, PB2, ADC_TEMPERATURE

  [temperature_fan chamber_fan]
  pin: PC0
  cycle_time: 0.0100
  hardware_pwm: false
  max_power: 1
  shutdown_speed: 0
  sensor_type: EPCOS 100K B57560G104F
  sensor_pin: PC5
  min_temp: 0
  max_temp: 70
  control: watermark
  max_delta: 2
  target_temp: 35.0
  max_speed: 1.0
  min_speed: 0.0

  [temperature_fan mcu_fan]
  pin: PB2
  cycle_time: 0.0100
  hardware_pwm: false
  max_power: 1
  shutdown_speed: 0
  sensor_type: temperature_mcu
  min_temp: 0
  max_temp: 100
  control: watermark
  max_delta: 2
  target_temp: 50.0
  max_speed: 1.0
  min_speed: 0.0

  [output_pin mcu_fan]
  pin: PB2
  pwm: True
  cycle_time: 0.0100
  hardware_pwm: false
  value: 0.00
  scale: 255
  shutdown_value: 0.0
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- You can now change the trigger temperature of the chamber and motherboard fans here:

  <img width="615" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Improve-Fans-Control/Fan_01.png">

- You can also change the motherboard fan speed manually here:

  <img width="617" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Improve-Fans-Control/Fan_02.png">

- Open `gcode_macro.cfg` file and add this macros:

  ```
  [gcode_macro M141]
  description: Set Chamber Temperature with slicers
  gcode:
    {% set s = params.S|float %}
    SET_TEMPERATURE_FAN_TARGET TEMPERATURE_FAN=chamber_fan TARGET={s}
    { action_respond_info("Chamber target temperature: %s°C" % (s)) }

  [gcode_macro M191]
  description: Wait for Chamber Temperature to heat up
  gcode:
    {% set s = params.S|float %}
    {% set chamber_temp = printer["temperature_sensor chamber_temp"].temperature|float %}
    {% if s > 0 %}
      M141 S{s}
    {% endif %}
    {% if s > chamber_temp and s <= 90 %}
      M140 S100
      { action_respond_info("Waiting for the bed to heat up the chamber...") }
      TEMPERATURE_WAIT SENSOR="temperature_fan chamber_fan" MINIMUM={s-1}
      { action_respond_info("Chamber target temperature reached: %s°C" % (s)) }
      M140 S{s}
    {% endif %}
  ```

  This macros allow to use `Print chamber temperature` function in OrcaSlicer with **M141 Sxx** and **M191 Sxx** commands:

  <img width="600" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Improve-Fans-Control/M191.png">

- Then, find macro named `[gcode_macro M106]` and replace it with this one:

  ```
  [gcode_macro M106]
  gcode:
    {% set fans = printer["gcode_macro PRINTER_PARAM"].fans|int %}
    {% set fan = 0 %}
    {% set value = 0 %}
    {% if params.P is defined %}
      {% set tmp = params.P|int %}
      {% if tmp < fans %}
        {% set fan = tmp %}
      {% endif %}
    {% endif %}
    {% if params.S is defined %}
      {% set tmp = params.S|float %}
    {% else %}
      {% set tmp = 255 %}
    {% endif %}
    {% if tmp > 0 %}
      {% if fan == 0 %}
        {% set value = printer["gcode_macro PRINTER_PARAM"].fan0_min + (255 - printer["gcode_macro PRINTER_PARAM"].fan0_min) / 255 * tmp %}
      {% endif %}
      {% if fan == 1 %}
        {% set value = printer["gcode_macro PRINTER_PARAM"].fan1_min + (255 - printer["gcode_macro PRINTER_PARAM"].fan1_min) / 255 * tmp %}
      {% endif %}
      {% if fan == 2 %}
        {% set value = printer["gcode_macro PRINTER_PARAM"].fan2_min + (255 - printer["gcode_macro PRINTER_PARAM"].fan2_min) / 255 * tmp %}
      {% endif %}
    {% endif %}
    {% if value >= 255 %}
      {% set value = 255 %}
    {% endif %}
    {% if params.P is defined and params.P|int == 3 %}
      {% set fan = 1 %}
    {% endif %}
    SET_PIN PIN=fan{fan} VALUE={value}
  ```

  This macros allow to use `Exhaust fan` function in OrcaSlicer with **M106 P3 Sxx** command:

  <img width="600" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Improve-Fans-Control/FM106.png">


- Then, click on `SAVE & RESTART` button in the top right corner.

<br />

## Control fans when cleaning the nozzle

It's possible to control hotend and side fans during nozzle cleaning process. This allows quieter cooling.

<br />

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Nozzle Cleaning Fan Control files`:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Installation-Helper-Script/Installation-Helper-Script.png">

-  Open `printer_params.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- And add this lines:

  ```
  [prtouch_v2_fan]
  max_speed: 0.5
  ```

> [!NOTE]
> You can change the `max_speed` value knowing that the max value is 1.0 (which corresponds to a speed of 100%).

- Then, click on `SAVE & RESTART` button in the top right corner.

- During the nozzle cleaning process, the fans will now operate at the defined value.


<br />