The version of Moonraker, Fluidd and Mainsail provided by Creality are not the latest.

With this guide and my script you can install latest official builds.

<br />

**<u>Note:</u> This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

⚠ **ONLY USE THIS SCRIPT WITH FIRMWARE 1.3.2.1 AND ABOVE!**

<br />

**Current script version:** v2.2

## Install 'Installation Helper Script'

If you have already installed Moonraker, Fluidd or Mainsail provided by Creality, please uninstall them first using `[Remove Menu]`.

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)).

- Enter the following command to install script in `/root` folder:

  ```
  cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
  ```

  <u>Note:</u> To update the script when a new version is available, enter this command:

  ```
  cd && rm -rf /root/installer.sh && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
  ```

- And enter this command to run the script:

  ```
  cd && sh ./installer.sh
  ```

- You can now select what you want to install or remove by typing your choice and validate with Enter keyboard button:

  <img width="900" alt="Capture d’écran 2023-10-04 à 00 47 54" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/07001d68-0df0-4ec1-be67-e7342ce8282b">

<br />

- With my script you can do this:

  - `Install Moonraker and Nginx` -> To install official and upgradable build of Moonraker
  - `Install Fluidd (port 4408)` -> To install on port 4408 latest official and upgradable build of Fluidd
  - `Install Mainsail (port 4409)` -> To install on port 4409 latest official and upgradable build of Mainsail
  - `Install Moonraker Timelapse` -> To install necessary for using Timelapse
  - `Install Entware` -> To install Entware (more info in [Install Entware](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Entware) section)
  - `Install Mobileraker Companion` -> To install Mobileraker Companion (see usage here: [Github](https://github.com/Clon1998/mobileraker_companion#how-it-works))
  - `Install Klipper Adaptive Meshing & Purging` -> To install KAMP (more info in [Use KAMP](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-KAMP) section)
  - `Install Hostname Service file` -> To install Hostname Service file needed to change hostname
  - `Install Custom Boot Display` -> To install a Custom Boot Display
  - `Install Buzzer Support files` -> To install files needed to use motherboard buzzer (more info in [Use Motherboard Buzzer](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-Motherboard-Buzzer))
  - `Install Nozzle Cleaning Fan Control files` -> To install files needed to control fans during nozzle cleaning (more info in [Improve Fans Control](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Improve-Fans-Control))
  - `Remove Fluidd` -> To remove Fluidd
  - `Remove Mainsail` -> To remove Mainsail
  - `Remove Moonraker Timelapse` -> To remove Timelapse
  - `Remove Moonraker and Nginx` -> To remove Moonraker and Nginx
  - `Remove Mobileraker Companion` -> To remove Mobileraker Companion
  - `Remove Klipper Adaptive Meshing & Purging` -> To remove KAMP
  - `Remove Hostname Service file` -> To remove Hostname Service file
  - `Remove Custom Boot Display` -> To remove Custom Boot Display and reinstall the stock one
  - `Remove Buzzer Support files` -> To remove Buzzer Support files
  - `Remove Nozzle Cleaning Fan Control files` -> To remove Nozzle Cleaning Fan Control files
  - `Backup configuration files` -> To backup the Klipper configuration folder
  - `Restore configuration files` -> To restore a backup of the Klipper configuration folder
  - `Reload Moonraker and Nginx` -> To reload Moonraker and Nginx services if needed

<br />
