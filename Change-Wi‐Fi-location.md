By default, Wi-Fi location is not set to your own country. Mine is set to GB (Great Britain) while I am in France.

This can be disturbing in some cases because not all countries use the same Wi-Fi frequencies.

Only make these changes if you are experiencing stability issues with your printer's Wi-Fi.

<br />

**<u>Note:</u> This procedure must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Configuration

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)).

- Enter the following command to check all available locations:

  ```
  cat /usr/share/zoneinfo/zone.tab
  ```

- Locate the two letters specific to your location in the list that appears.

- On the left part of the window, go to the `/usr/data/` folder and right-click on the `wpa_supplicant.conf` file then select `Open with default text editor`:

  <img width="900" alt="Capture d’écran 2023-11-05 à 18 00 copie" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/bf19f018-249f-4a71-8cf3-49fcca56f186">

- In the new editing window that appears, modify the country line by replacing the two letters corresponding to your location, like this:

  <img width="900" alt="Capture d’écran 2023-11-05 à 18 05 41" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/82151547-7493-4db5-a63e-798d9b03515b">

- Then click on `Save file` button on the top:

  <img width="900" alt="Capture d’écran 2023-11-05 à 18 05 41 2" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/b663a0f4-c398-4321-9298-ec0c34e09f5e">

- And confirm the file replacement by clicking `Yes` button:

  <img width="600" alt="Capture d’écran 2023-11-05 à 18 12 46" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/debc1082-c9bf-4c5a-8470-c70a9bbd5e65">

- On the right part of the window, in SSH command prompt, enter this command to reboot your printer:

  ```
  reboot
  ```

- After restarting, the printer's Wi-Fi will be set to your own country.

<br />