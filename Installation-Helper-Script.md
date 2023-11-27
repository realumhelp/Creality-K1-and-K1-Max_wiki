The version of Moonraker, Fluidd and Mainsail provided by Creality are not the latest.

With this guide and my script you can install latest official builds.

<br />

> [!NOTE]
> **This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

> [!WARNING]
> **ONLY USE THIS SCRIPT WITH FIRMWARE 1.3.2.1 AND ABOVE!**

<br />

**Current script version:** v3.7.1

## Install 'Installation Helper Script'

If you have already installed Moonraker, Fluidd or Mainsail provided by Creality, please uninstall them first using `[Remove Menu]`.

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)).

- Enter the following command to install script in `/root` folder:

  ```
  cd && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
  ```

  <u>Note:</u> You can update the script directly on the script but if you need to update it manually, enter this command:

  ```
  cd && rm -f installer.sh && wget --no-check-certificate https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Scripts/installer.sh
  ```

- And enter this command to run the script:

  ```
  cd && sh ./installer.sh
  ```

- You can now select what you want to install or remove by typing your choice and validate with Enter keyboard button:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Installation-Helper-Script/Installation-Helper-Script.png">

<br />

- In case you get this kind of error while installing some packages:

  ```
  Connecting to github.com (20.248.137.48:443)
  wget: TLS error from peer (alert code 80): 80
  wget: error getting response: Connection reset by peer
  Download failed. Exit code: 1
  ```
  
  - Install Entware by following this [Install Entware](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Entware) section.

  - Once installed, in SSH command prompt, enter this command:

    ```
    opkg install wget-ssl
    ```

<br />

## Features

- **Install & Remove `Moonraker and Nginx` (official build)**
  - Moonraker is a Python 3 based web server that exposes APIs with which client applications may use to interact with Klipper firmware.

- **Install & Remove `Fluidd` on port 4408 (official build)**
  - Fluidd is a free and open-source Klipper web interface for managing your 3d printer.

- **Install & Remove `Mainsail` on port 4409 (official build)**
  - Mainsail is the popular web interface for managing and controlling 3D printers with Klipper.

- **Install & Remove `OctoEverywhere` - More info here: [Github](https://github.com/QuinnDamerell/OctoPrint-OctoEverywhere)**
  - Cloud empower your Klipper printers with free, private, and unlimited remote access to your full web control portal from anywhere!

- **Install & Remove `Obico` - More info here: [Github](https://github.com/TheSpaghettiDetective/moonraker-obico)**
  - This is a Moonraker plugin that enables the Klipper-based 3D printers to connect to Obico. Obico is a community-built, open-source smart 3D printing platform used by makers, enthusiasts, and tinkerers around the world.

- **Install & Remove `Moonraker Timelapse` (modified build for K1 Series)**
  - A 3rd party Moonraker component to create timelapse of 3D prints.

- **Install & Remove `Entware` - More info in [Install Entware](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Entware) section**

  - Entware is a software repository for devices which use the Linux kernel. It allows packages to be added to your printer to perform new tasks or provide other functionality than what it was marketed for, or simply to perform those functions better.

- **Install & Remove `Mobileraker Companion` (modified build for K1 Series) - More info here: [Github](https://github.com/Clon1998/mobileraker_companion#how-it-works)**
  - Companion for Mobileraker phone App, enabling push notification for Klipper using Moonraker.

- **Install & Remove `Klipper Adaptive Meshing & Purging` (modified build for K1 Series) - More info in [Use KAMP](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-KAMP) section)**
  - Klipper Adaptive Meshing & Purging is an extension that allows you to generate a mesh only in the area you really need it: where you print!

- **Install & Remove 'Hostname Service file` - More info in [Change Hostname](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Change-Hostname) section**
  - Allows you to change the hostname of the machine (firmwares < 1.3.2.8)

- **Install & Remove `Klipper Gcode Shell Command` (official build)**
  - Allows execute linux commands or even scripts from within Klipper with custom commands defined in your printer.cfg.

- **Install & Remove `Custom Boot Display`**
  - To install a custom Creality-themed boot display.

- **Install & Remove `Buzzer Support files` - More info in [Use Motherboard Buzzer](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-Motherboard-Buzzer) section**
  - Allows to use motherboard buzzer.

- **Install & Remove `Nozzle Cleaning Fan Control files` - More info in [Improve Fans Control](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Improve-Fans-Control) section**
  - Allows to control fans during nozzle cleaning.

- **Install & Remove `Camera settings Control files` - More info in [Camera Settings Control](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Camera-Settings-Control) section**
  - Allows to install macros needed to control camera setting.

- **Backup & restore `Klipper configuration files`**
  - Allows to backup and restore a saved backup of the Klipper configuration folder.

- **Reload `Moonraker and Nginx`**
  - To reload Moonraker and Nginx services if needed.

<br />