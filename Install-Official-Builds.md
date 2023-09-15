The version of Moonraker, Fluidd and Mainsail provided by Creality are not the latest. With this guide you can install latest official builds.

<br />

**<u>Note:</u> This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

## Install the latest builds

If you have already installed Moonraker, Fluidd or Mainsail provided by Creality, please uninstall them first.

- Enter the following command to install script in `/root` folder:

  ```
  cd && wget https://github.com/Guilouz/Creality-K1-and-K1-Max/raw/main/Scripts/installer.sh
  ```

  <u>Note:</u> To update the script when a new version is available, enter this command:

  ```
  cd && rm -rf /root/installer.sh && wget https://github.com/Guilouz/Creality-K1-and-K1-Max/raw/main/Scripts/installer.sh
  ```

- And enter this command to run the script:

  ```
  cd && sh ./installer.sh
  ```

- You can now select what you want to install or remove by typing your choice and validate with Enter keyboard button:

  <img width="900" alt="Capture d’écran 2023-09-15 à 23 54 58" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/9d6cf3e7-6411-41c8-9f22-fb8a7d84c2e4">

<br />

  - `Install Moonraker and Nginx` -> To install official and upgradable build of Moonraker
  - `Install Fluidd (port 4408)` -> To install on port 4408 latest official and upgradable build of Fluidd
  - `Install Mainsail (port 4409)` -> To install on port 4409 latest official and upgradable build of Mainsail
  - `Install Entware` -> To install Entware (more info in [Install Entware](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Entware) section)
  - `Remove Fluidd` -> To remove Fluidd
  - `Remove Mainsail` -> To remove Mainsail
  - `Remove Moonraker and Nginx` -> To remove Moonraker and Nginx
  - `Backup configuration files` -> To backup Klipper config folder
  - `restore configuration files` -> To restore a backup up Klipper config folder
  - `Reload Moonraker and Nginx` -> To reload Moonraker and Nginx services if needed

<br />

## Access to Web Interface

- To access to the classic Creality Web Interface, just use `Creality Print` slicer as usual.

  <img width="2500" alt="Capture d’écran 2023-08-04 à 00 40 52" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/78bfd1f1-34f7-4816-8e6b-2036f0aee2e0">

- To access to the original Fluidd Web Interface, just use your printer's IP address with port 4408 in your Web browser such as: `http://xxx.xxx.xxx.xxx:4408/` (replacing xxx.xxx.xxx.xxx by your local IP address).

  <img width="2500" alt="Capture d’écran 2023-08-04 à 15 19 57" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/0595b4a7-c4e4-407a-8efb-e1f95cc47c42">

- To access to the original Mainsail Web Interface, just use your printer's IP address with port 4409 in your Web browser such as: `http://xxx.xxx.xxx.xxx:4409/` (replacing xxx.xxx.xxx.xxx by your local IP address).

  <img width="2500" alt="Sans titre-1 copie" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/cc4611c8-e3da-45f2-b215-20fa32e5526c">

<br />

## Configure Camera

### Configure Camera in Fluidd

  When you first go to the original Fluidd Web Interface, the camera will not be detected because it's disabled by default.

  It's necessary to go to `Settings` -> `Cameras` and enable it.

- If not working, delete the existing camera and recreate it with these settings:

  <img width="400" alt="Capture d’écran 2023-08-04 à 00 46 48" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/2aeafdb2-67b9-4c5b-9fe2-635dd2875512">

<br />

### Configure Camera in Mainsail

- Go to `Interface Settings` at the top right of the window and in `WEBCAMS` section.

- Configure your webcam like this:

  <img width="899" alt="Capture d’écran 2023-08-18 à 03 48 15" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/0f025309-845b-4e88-9d79-6e63574d840f">

<br />

- Replacing xxx.xxx.xxx.xxx by your local IP address:

    - **URL Stream:** `http://xxx.xxx.xxx.xxx:4409/webcam/?action=stream`
    - **URL Snapshot:** `http://xxx.xxx.xxx.xxx:4409/webcam/?action=snapshot`
    - **Service:** `MJPEG-Streamer` or `Adaptative MJPEG-Streamer (experimental)`

<br />

## Timelapse

If you want to use Timelapse function in Fluidd or Mainsail you can follow guide from Mike Constantino available here: [Github](https://github.com/mikebcbc/creality-k1-moonraker-timelapse)

<br />