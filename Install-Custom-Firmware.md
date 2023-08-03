The changes to the Custom Firmware are quite simple, it's just stock firmware with a modified shadow file setting the root password to "creality" and restoring the Creality version of fluidd and Moonraker which were disabled on early versions firmware up to version 1.2.9.15.

⚠ **Use these completely at your own risk. There are no promises that it won't brick your printer. Several people have tested it so far and no one has yet, but you could be the first.**

<br />

## Download Links

**Custom Firmwares Creality K1:**

  - [5.3.1.14](https://drive.google.com/file/d/1Lu5qVSBVaqp3WWV529CrqF93ClSYGKX8/view?usp=drive_link)
  - [5.3.1.17](https://drive.google.com/file/d/1228bKE0FFBkAwOwh-yepYnttJXWZOZUT/view?usp=drive_link)
  - [5.3.1.18](https://drive.google.com/file/d/1TKOrBOegbK_GmWaTa1nsBdePvJXftugk/view?usp=drive_link)

**Custom Firmwares Creality K1 Max:**

  - [5.3.0.39](https://drive.google.com/file/d/1hfRpwwpoywF0RelFWjGc6ZhDJMC5ZASJ/view?usp=drive_link)
  - [5.3.1.17](https://drive.google.com/file/d/10IArVHTFPJDEYv7RGAUCQhuuhGwcvR4g/view?usp=drive_link)
  - [5.3.1.18](https://drive.google.com/file/d/1veuCzwSbpQV3tOU4Boz--DzgEyadRtiB/view?usp=drive_link)

<u>Note:</u> The 5 instead of a 1 at the beginning is normal, it's to enable restoration or reinstallation on top of the same version.

Also note that the K1 firmwares works without issue on the K1 Max, the detection of the correct printer being carried out by the firmware.

<br />

## Installation

- You need USB drive formatted in FAT32.

- Copy the desired `.img` firmware file to the root of your USB drive and remove it from your computer.

- Turn on the printer.

- When your are on home screen, plug USB drive on the front of the printer.

- A popup should appear indicating the presence of a new update.

- Press `Upgrade` and wait during the update process.

- When it's done, the printer restarts.

- When you are on the home screen, you can remove the USB drive.

- That's all! You are now on Custom Firmware with root access.

- To connect over SSH, use `root` user and `creality` password.

<br />

## Access to Web Interface

- To access to the classic Creality Web Interface, just use `Creality Print` slicer as usual.

  <img width="2560" alt="Capture d’écran 2023-08-04 à 00 40 52" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/78bfd1f1-34f7-4816-8e6b-2036f0aee2e0">

- To access to the original Fluidd Web Interface, just use your printer's IP address with port 4408 in your Web browser such as: `http://xxx.xxx.xxx.xxx:4408/` (replacing xxx.xxx.xxx.xxx by your local IP address).

  <img width="2543" alt="Capture d’écran 2023-08-04 à 00 39 38" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/9f55ef96-995d-4568-9a8b-7c6971b83af0">

<br />

## Needed Changes

- **<u>Fix camera issue:</u>**

  When you first go to the original Fluidd Web Interface, the camera will not be detected.

  It's necessary to go to `Settings` -> `Cameras`, delete the existing camera and recreate it with these settings:

  <img width="400" alt="Capture d’écran 2023-08-04 à 00 46 48" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/2aeafdb2-67b9-4c5b-9fe2-635dd2875512">

<br />

- **<u>Fix START_PRINT macro issue:</u>**

  The classic Creality Web Interface should work normally. However if you want to use the original Fluidd Web Interface, you need to fix a issue that seems to have been introduced by Creality since firmware 1.3.x.x.

  - To do this, on original Fluidd Web Interface go to `Configuration` and open `gcode_macro.cfg` file.

  - Search macro named `[gcode_macro START_PRINT]` and add these three lines before the existing line `CX_PRINT_DRAW_ONE_LINE`:

    ```
    CX_ROUGH_G28 EXTRUDER_TEMP={extruder_temp} BED_TEMP={bed_temp}
    CX_NOZZLE_CLEAR
    CX_PRINT_LEVELING_CALIBRATION
    ```

    Like that:

    ```
    [gcode_macro START_PRINT]
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

      CX_ROUGH_G28 EXTRUDER_TEMP={extruder_temp} BED_TEMP={bed_temp}
      CX_NOZZLE_CLEAR
      CX_PRINT_LEVELING_CALIBRATION
      CX_PRINT_DRAW_ONE_LINE
    ```
  - Then, click on `SAVE & RESTART` button in the top right corner.

<br />