It's possible to control camera settings with macros.

<br />

> [!NOTE]
> **This procedure must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Installation

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Camera Settings Control files`:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Installation-Helper-Script/Installation-Helper-Script.png">

<br />

## Configuration

-  Open `printer.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- And add this lines:

  ```
  [include camera-settings.cfg]
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Now you can use the different macros starting with `CAM_` to configure your camera settings:

  <img width="725" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Camera-Settings-Control/Camera_01.png">


  `CAM_SETTINGS` macro can be used to show all current camera settings:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Camera-Settings-Control/Camera_02.png">

- When restarting the printer your camera settings will not be preserved, to correct this open `camera-settings.cfg` and add this lines by modifying the desired values:

  ```
  [delayed_gcode LOAD_CAM_SETTINGS]
  initial_duration: 2
  gcode:
    CAM_BRIGHTNESS BRIGHTNESS=0
    CAM_CONTRAST CONTRAST=32
    CAM_SATURATION SATURATION=56
    CAM_SHARPNESS SHARPNESS=3
    CAM_HUE HUE=0
    CAM_WHITE_BALANCE_TEMPERATURE_AUTO WHITE_BALANCE_TEMPERATURE_AUTO=1
    CAM_WHITE_BALANCE_TEMPERATURE WHITE_BALANCE_TEMPERATURE=4600
    CAM_GAMMA GAMMA=80
    CAM_GAIN GAIN=0
    CAM_POWER_LINE_FREQUENCY POWER_LINE_FREQUENCY=1
    CAM_BACKLIGHT_COMPENSATION BACKLIGHT_COMPENSATION=1
    CAM_EXPOSURE_AUTO EXPOSURE_AUTO=3
    CAM_EXPOSURE_ABSOLUTE EXPOSURE_ABSOLUTE=156
    CAM_EXPOSURE_AUTO_PRIORITY EXPOSURE_AUTO_PRIORITY=0
  ```

  > [!NOTE]
  > Here all macros are configured with their default value, you can remove unmodified ones if they don't need to be loaded when Klipper starts.

- Then, click on `SAVE AND RESTART` button in the top right corner.

<br />