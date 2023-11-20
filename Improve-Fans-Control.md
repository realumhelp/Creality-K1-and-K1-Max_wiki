Here you can find different tips to improve fans control.

<br />

> [!NOTE]
> **This procedures must be repeated if you update the firmware or if you restore the printer to default settings.**

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

  [temperature_fan cpu_fan]
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
  target_temp: 45.0
  max_speed: 1.0
  min_speed: 0.0

  [output_pin cpu_fan]
  pin: PB2
  pwm: True
  cycle_time: 0.0100
  hardware_pwm: false
  value: 0.00
  scale: 255
  shutdown_value: 0.0
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- Open `gcode_macro.cfg` file and add this macros:

  ```
  [gcode_macro M141]
  description: Set Chamber Temperature with slicers
  gcode:
    {% set s = params.S|float %}
    SET_TEMPERATURE_FAN_TARGET TEMPERATURE_FAN=chamber_fan TARGET={s}
    { action_respond_info("Chamber fan target temperature: %s°C" % (s)) }

  [gcode_macro M191]
  description: Set Chamber Temperature with slicers
  gcode:
    {% set s = params.S|float %}
    SET_TEMPERATURE_FAN_TARGET TEMPERATURE_FAN=chamber_fan TARGET={s}
    { action_respond_info("Chamber fan target temperature: %s°C" % (s)) }
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- You can now change the trigger temperature of the chamber and motherboard fans here:

  <img width="615" alt="Capture d’écran 2023-11-17 à 19 43 23" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/4838e182-03a3-46a9-95b1-027e485887d2">

- You can also change the motherboard fan speed manually here:

  <img width="617" alt="Capture d’écran 2023-11-17 à 19 44 03" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/a8982efd-fcfa-46ee-ade4-6c7cb2330ab7">

- You can also use `M141 Sxx` command in your slicer to define the chamber fan trigger temperature by replacing `xx` by temperature value (range between 0 and 70 °C).

<br />

## Control fans when cleaning the nozzle

It's possible to control hotend and side fans during nozzle cleaning process. This allows quieter cooling.

<br />

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Nozzle Cleaning Fan Control files`:

  <img width="900" alt="Capture d’écran 2023-10-09 à 01 58 59" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/bac35dd7-6a81-4ada-a711-6f6d2b2c566d">

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