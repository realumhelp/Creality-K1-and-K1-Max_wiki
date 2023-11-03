From Fluidd or Mainsail it's possible to classify your Gcode in folders but Creality introduced an issue in its code and it prevents printing a Gcode contained in a folder.

This returns **_code:"key514", "msg":"Malformed command args..._** error.

<br />

**<u>Note:</u> This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

## How to fix that

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)).

- Enter the following commands (one by one):

  ```
  cd /usr/share/klipper/klippy/
  ```
 
  ```
  rm -f gcode.py gcode.pyc
  ```
 
  ```
  wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/files/fixes/gcode.py
  ```

  ```
  reboot
  ```

- Once the printer is restarted, you can now print a Gcode from a folder.

<br />
