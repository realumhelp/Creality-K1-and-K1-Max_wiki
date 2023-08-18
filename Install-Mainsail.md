Fluidd is installed by default and use 4408 port but you can also install Mainsail with another port (4409 here).

This allows to have the web interface of Fluidd and Mainsail that coexist together.

<br />

To have permanent configuration, make sure you have followed this [Permanent Moonraker Configuration](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Permanent-Moonraker-Configuration) section before.

Make sure you have also followed this [Update Moonraker](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Update-Moonraker) section to have all features of Mainsail.

<br />

**<u>Note:</u> This procedure must be repeated if you restore the printer to default settings or if you update the firmware.**

<br />

## Install Mainsail

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)) and enter this commands (one by one):

  ```
  mkdir /usr/share/mainsail
  ```

  ```
  cd /usr/share/mainsail
  ```

  ```
  wget -q -O mainsail.zip https://github.com/mainsail-crew/mainsail/releases/latest/download/mainsail.zip && unzip mainsail.zip && rm mainsail.zip
  ```

- When it's done, go to the folder `/etc/nginx/` on the left side of the window:

  <img width="900" alt="Capture d’écran 2023-08-18 à 03 00 07" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/048ac682-3bd2-4bfe-a9ee-739d0eb34a0f">

- Download this `nginx.conf` file and unzip it:

  <u>Download link:</u> [nginx.conf.zip](https://github.com/Guilouz/Creality-K1-and-K1-Max/files/12374493/nginx.conf.zip)

- Then drag and drop it on the left panel to replace existing one:

  <img width="900" alt="Sans titre-1 copie" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/8c885c37-a410-4f67-9a38-05a44035864a">

- On command prompt window, enter the following command to restart nginx:

  ```
  /etc/init.d/S50nginx restart
  ```

- You can now access to Mainsail Web interface, just use your printer's IP address with port 4409 in your Web browser such as: `http://xxx.xxx.xxx.xxx:4409/` (replacing xxx.xxx.xxx.xxx by your local IP address).

  Fluidd Web interface remains accessible on port 4408.

  <img width="1100" alt="Sans titre-1 copie" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/cc4611c8-e3da-45f2-b215-20fa32e5526c">

<br />

## Configure Camera

- Go to `Interface Settings` at the top right of the window and in `WEBCAMS` section.

- Configure your webcam like this:

  <img width="899" alt="Capture d’écran 2023-08-18 à 03 48 15" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/0f025309-845b-4e88-9d79-6e63574d840f">

<br />

- Replacing xxx.xxx.xxx.xxx by your local IP address:

    - **URL Stream:** `http://xxx.xxx.xxx.xxx:4409/webcam/?action=stream`
    - **URL Snapshot:** `http://xxx.xxx.xxx.xxx:4409/webcam/?action=snapshot`
    - **Service:** `MJPEG-Streamer` or `Adaptative MJPEG-Streamer (experimental)`

<br />

## Update Mainsail

- Go on `Machine` tab on the left, open `moonraker.conf` file and add the following lines at the end of the file:

  ```
  [update_manager mainsail]
  type: web
  channel: beta
  repo: mainsail-crew/mainsail
  path: /usr/share/mainsail
  ```

- Once done, click on `SAVE & RESTART` at the top right to save the file.

- You can now click the refresh button (still in the Machine tab) on the `Update Manager` tile.

- You will see a new Mainsail line appear and you can update when a new version will be available:

  <img width="800" alt="Capture d’écran 2023-08-18 à 03 57 46" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/d57b2861-9695-420d-9bd1-893d01b863c7">

<br />

## Timelapse

If you want to use Timelapse function in Mainsail you can follow guide from Mike Constantino available here: [Github](https://github.com/mikebcbc/creality-k1-moonraker-timelapse)

<br />