By default, Creality has set up a replacement for the Moonraker configuration file on startup, which prevents any permanent modifications.

<br />

**<u>Note:</u> This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

##  Make permanent Moonraker configuration

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)) and go to the folder `/etc/init.d/` on the left side of the window:

  <img width="900" alt="Capture d’écran 2023-08-10 à 22 39 58" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/9cf35429-5a59-45c6-8bcc-9ffb97a13ffd">

- Locate the `S56moonraker_service` file and right click on it and select `Open with default text editor`:

  <img width="900" alt="Capture d’écran 2023-08-10 à 22 15 copie" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/d3a4385e-db60-4c7f-96d3-45487eedc52a">

- Comment out the following lines (by adding a # symbol in front):

  ```
  #[ -s $PRINTER_CONFIG_DIR/moonraker.conf ] || cp $DEFAULT_CFG $PRINTER_CONFIG_DIR/moonraker.conf
  ```

  ```
  #CONFIG_FILE="/usr/data/printer_data/config/moonraker.conf"
  #if [ ! -x $CONFIG_FILE ]; then
    #cp /usr/share/moonraker/moonraker.conf $CONFIG_FILE
  #fi
  ```

  Like this (green lines):

  <img width="900" alt="Capture d’écran 2023-08-10 à 22 32 58" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/286e37ef-d630-4268-b904-c37935ec1f84">

- When it's done, click the save button at the top of the window:

  <img width="688" alt="Capture d’écran 2023-08-10 à 22 49 31" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/0eca3bd8-e834-4d42-9a4f-a3ce75b9a2e7">

- Then click on `Yes` button on the new window to upload file to printer:

  <img width="756" alt="Capture d’écran 2023-08-10 à 22 52 04" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/304cc7c6-b524-4099-821a-7449f39e7292">

- You can now make changes to the `moonraker.conf` file without it being overwritten every time the printer starts.

<br />