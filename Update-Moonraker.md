The version of Moonraker present in the firmware is not the latest.

<br />

To have permanent configuration, make sure you have followed this [Permanent Moonraker Configuration](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Permanent-Moonraker-Configuration) section before.

**<u>Note:</u> This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

## Update to the latest version

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)) and enter this commands (one by one):

  ```
  /etc/init.d/S56moonraker_service stop
  ```

  ```
  cd /usr/share
  ```

  ```
  mv moonraker moonraker.old
  ```

  ```
  git clone --depth 1 https://github.com/Arksine/moonraker
  ```

  ```
  cp moonraker.old/moonraker.conf moonraker/moonraker.conf
  ```

  ```
  /etc/init.d/S56moonraker_service start
  ```

- Once the Moonraker service has restarted, go on Fluidd Web Interface.

- You will see a warning message:
  
  <img width="1467" alt="Capture d’écran 2023-08-18 à 02 44 04" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/95d3934b-ef70-4ac5-a4f2-b944c29665d1">

- Go to `Configuration`, open `moonraker.conf` and remove this line:

  ```
  enable_inotify_warnings: True
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- You now have the latest version of Moonraker installed.

  <img width="900" alt="Capture d’écran 2023-08-18 à 02 49 04" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/cba404f4-a3d0-4c60-85e5-b2b92d71847a">

  <u>Note:</u> Disregard the version number displayed on the interface.


<br />