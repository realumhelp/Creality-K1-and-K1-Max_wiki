You can use official Timelapse functionalities.

This process installs a version of Timelapse compatible with K1 Series.

<br />

**<u>Note:</u> This procedure must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Installation

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Moonraker Timelapse`:

  <img width="900" alt="Capture d’écran 2023-10-04 à 00 47 54" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/07001d68-0df0-4ec1-be67-e7342ce8282b">

<br />

## Configuration

-  Open `moonraker.conf` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Enable this lines by removing `#` before like this (or add this lines if you don't have them):

  ```
  # Remove '#' to enable Timelapse function and replace port '4408' by '4409' in snapshoturl if you use Mainsail
  [timelapse]
  output_path: /usr/data/printer_data/timelapse/
  frame_path: /usr/data/printer_data/frames/
  snapshoturl: http://localhost:4408/webcam/?action=snapshot
  ```

  <u>Note:</u> Replace port `4408` to `4409` in `snapshoturl` if you only use Mainsail.

- Then, click on `SAVE & RESTART` button in the top right corner.

- Open `printer.cfg` file and add this line to include Timelapse:

  ```
  [include timelapse.cfg]
  ```

- You can now configure Timelapse settings:

  - On original Fluidd Web Interface go to `Settings` icon on the left side then to `Timelapse`.
  - On original Mainsail Web Interface go to `Settings` on the top right corner then to `Timelapse`.

    <img width="900" alt="Capture d’écran 2023-09-17 à 13 20 18" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/12c1c1f8-1fc3-4666-b4d3-fca0f84ea0d4">

- Your Slicer must be configured too, see this to configure it: [Github](https://github.com/mainsail-crew/moonraker-timelapse/blob/main/docs/configuration.md#slicer-setup)

<br />

More info about Moonraker Timelapse here: [Github](https://github.com/mainsail-crew/moonraker-timelapse)

<br />