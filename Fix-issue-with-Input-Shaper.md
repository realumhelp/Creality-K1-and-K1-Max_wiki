After finding, Creality blocked the Input Shaper results on the 'ei' shaper via a macro in latest firmwares.

This therefore means that regardless of the measured resonances, the 'ei' shaper will always be selected.

Moreover the resonances of the X axis are never measured.
The resonance test is performed on the Y axis and the same result is also applied to the X axis.

<br />

## Explanations

Here are the tests that demonstrate this:

- Running `SHAPER_CALIBRATE AXIS=X` command, this is the result:

  <img width="800" alt="Capture d’écran 2023-08-04 à 13 00 01" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/cae17790-b0f3-44e8-aa56-0463959ce68b">

- And result for X axis have been saved in `printer.cfg` file:

  <img width="693" alt="Capture d’écran 2023-08-04 à 13 01 47" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/ee025a7f-8866-428b-9f99-72d0b47a01de">

- Now running `SHAPER_CALIBRATE AXIS=Y` command, this is the result:

  <img width="1000" alt="Capture d’écran 2023-08-04 à 13 07 19" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/13e8bf05-c448-4e5c-82d6-fea0d573d4e4">

- We see here that the result of the Y axis is also applied to the X axis and result have been saved in `printer.cfg` file:

  <img width="679" alt="Capture d’écran 2023-08-04 à 13 09 49" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/57c2c996-a01b-4d15-938d-4b99f2589da8">

- The X axis shaper measured just before was overwritten by the value measured on Y axis.

<br />

## How to fix that

- On original Fluidd Web Interface go to `Configuration` and open `gcode_macro.cfg` file.

- Search macro named `[gcode_macro AUTOTUNE_SHAPERS]` and comment line `variable_autotune_shapers: 'ei'` like that:

  ```
  [gcode_macro AUTOTUNE_SHAPERS]
  #variable_autotune_shapers: 'ei'
  gcode:
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- I have added `extra_macro.cfg` file available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/Stock%20Config%20Files/extra_macro.cfg) that contains macros to start a Bed Leveling manually, to start Input Shaper for X and Y axis and to start PID for Hotend and Bed.

- Download this file and just drag and drop it in `Configuration Files` on Fluidd, like that:

  <img width="700" alt="Capture d’écran 2023-08-04 à 13 40 59" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/8c027c82-b63f-433a-bb63-a0da2988d70d">

- Open `printer.cfg` file and add this line:

  ```
  [include extra_macro.cfg]
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- Now run `INPUT_SHAPPER_Y` macro, this will measure the Y axis resonances.

- This is the result:

  <img width="900" alt="Capture d’écran 2023-08-04 à 13 55 33" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/b706605a-a579-4605-bb46-01b55eb3d6a3">

  And the result in the `printer.cfg` file:

  <img width="679" alt="Capture d’écran 2023-08-04 à 13 56 33" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/b1940959-4205-4e33-885b-5527dd9d01f6">

- When it's done, run `INPUT_SHAPPER_X` macro, this will measure the X axis resonances.

- This is the result:

  <img width="850" alt="Capture d’écran 2023-08-04 à 14 02 54" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/e521de26-377b-4213-bcdd-9630024a19ff">

  And the result in the `printer.cfg` file:

  <img width="679" alt="Capture d’écran 2023-08-04 à 14 03 42" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/0292e301-94be-4206-9619-8accc2a4f627">

  Performing the Y axis resonance test first avoids overwriting the X axis result.

  <u>Note:</u> When updating to a new firmware version, the `extra_macro.cfg` file will be deleted and changes made to the `gcode_macro.cfg` and `printer.cfg` files will also be deleted, only the settings are kept.
  Creality has set up a swap system that replaces any modifications made at startup.

<br />