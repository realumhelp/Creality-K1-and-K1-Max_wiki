The version of Fluidd present in the firmware is not the latest.

<br />

To have permanent configuration, make sure you have followed this [Permanent Moonraker Configuration](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Permanent-Moonraker-Configuration) section before.

**<u>Note:</u> This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

## Update to the latest version

- On original Fluidd Web Interface go to `Configuration`, open `moonraker.conf` file and add this lines at the bottom:

  ```
  [update_manager]
  enable_auto_refresh: True
  enable_system_updates: False

  [update_manager fluidd]
  type: web
  channel: beta
  repo: fluidd-core/fluidd
  path: /usr/share/fluidd
  ```

- Then, click on `SAVE` button in the top right corner.

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)) and on command prompt window, enter the following command to restart Moonraker service:

  ```
  /etc/init.d/S56moonraker_service restart
  ```
- Once Moonraker is reconnected on Fluidd go to `Settings` -> `Software Updates` and click to update fluidd:

  <img width="900" alt="Capture d’écran 2023-08-04 à 14 49 19" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/f16b9c09-1f8b-4191-bad2-8f6372eb01ff">

  ⚠ **DO NOT UPDATE KLIPPER VERSION AND DO NOT RECOVER MOONRAKER VERSION, ONLY FLUIDD!**

- When it's done Fluidd is up to date:

  <img width="900" alt="Capture d’écran 2023-08-04 à 14 53 25" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/3239e180-b850-425a-831a-551ee20b5d23">

<br />