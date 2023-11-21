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

### Configure Camera in Moonraker

If you want to configure camera for Fluidd and Mainsail you can also configure it in Moonraker.


-  Open `moonraker.conf` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Add this lines (if you don't have them) by replacing `xxx.xxx.xxx.xxx` by your local IP address:

  ```
  [webcam Camera]
  location: printer
  enabled: True
  service: mjpegstreamer
  target_fps: 15
  target_fps_idle: 5
  stream_url: http://xxx.xxx.xxx.xxx:8080/?action=stream
  snapshot_url: http://xxx.xxx.xxx.xxx:8080/?action=snapshot
  flip_horizontal: False
  flip_vertical: False
  rotation: 0
  aspect_ratio: 4:3
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- Your camera will be automatically configured for Fluidd and Mainsail.

<br />