Here you can find different tips to improve fans control.

<br />

**<u>Note:</u> This procedures must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Improve hotend cooling at the end of printing

By default at the end of a print, the hotend is cooled by its fan which runs at 100%.

By making this change, the hotend fan speed will be reduced to 80% and the side fan will also be enabled at 80%. This allows faster and quieter cooling.

<br />

-  Open `gcode_macro.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Search macro named `[gcode_macro WAIT_TEMP_START]` and replace it by this one:

  ```
  [gcode_macro WAIT_TEMP_START]
  gcode:
    UPDATE_DELAYED_GCODE ID=wait_temp DURATION=1
    M106 P0 S200
    SET_PIN PIN=fan2 VALUE=80
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

## Control chamber fan

It's possible to trigger the back fan depending on the chamber temperature.

<br />

-  Open `printer.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- And add this lines:

  ```
  [duplicate_pin_override]
  pins: PC0, PC5

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
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- Open `gcode_macro.cfg` file and add this macro:

  ```
  [gcode_macro M141]
  description: Set Chamber Temperature with slicers
  gcode:
    SET_TEMPERATURE_FAN_TARGET TEMPERATURE_FAN=chamber_fan TARGET={params.S|default(35)}
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- You can now change the chamber fan trigger temperature here:

  <img width="700" alt="Capture d’écran 2023-09-29 à 12 18 46" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/1159f580-00ef-4b1b-a8e4-a009852e57a4">

- You can also use `M141 Sxx` command in your slicer to define the chamber fan trigger temperature by replacing `xx` by temperature value (range between 0 and 70 °C).

<br />

## Control fans when cleaning the nozzle

It's possible to control hotend and side fans during nozzle cleaning process. This allows quieter cooling.

<br />

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Nozzle Cleaning Fan Control files`:

  <img width="900" alt="Capture d’écran 2023-09-29 à 22 07 08" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/d3c433e5-532c-4e67-abfb-ab53ac4df3ce">

-  Open `printer_params.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- And add this lines:

  ```
  [prtouch_v2_fan]
  max_speed: 0.5
  ```

  <u>Note:</u> You can change the `max_speed` value knowing that the max value is 1.0 (which corresponds to a speed of 100%).

- Then, click on `SAVE & RESTART` button in the top right corner.

- During the nozzle cleaning process, the fans will now operate at the defined value.


<br />