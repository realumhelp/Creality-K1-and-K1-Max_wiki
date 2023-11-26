By default, Wi-Fi location is not set to your own country. Mine is set to GB (Great Britain) while I am in France.

This can be disturbing in some cases because not all countries use the same Wi-Fi frequencies.

Only make these changes if you are experiencing stability issues with your printer's Wi-Fi.

<br />

> [!NOTE]
> **This procedure must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Configuration

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)).

- Enter the following command to check all available locations:

  ```
  cat /usr/share/zoneinfo/zone.tab
  ```

- Locate the two letters specific to your location in the list that appears.

- On the left part of the window, go to the `/usr/data/` folder and right-click on the `wpa_supplicant.conf` file then select `Open with default text editor`:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Change-Wi‐Fi-location/Wifi_01.png">

- In the new editing window that appears, modify the country line by replacing the two letters corresponding to your location, like this:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Change-Wi‐Fi-location/Wifi_02.png">

- Then click on `Save file` button on the top:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Change-Wi‐Fi-location/Wifi_03.png">

- And confirm the file replacement by clicking `Yes` button:

  <img width="600" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Change-Wi‐Fi-location/Wifi_04.png">

- On the right part of the window, in SSH command prompt, enter this command to reboot your printer:

  ```
  reboot
  ```

- After restarting, the printer's Wi-Fi will be set to your own country.

<br />