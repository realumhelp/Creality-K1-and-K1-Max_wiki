It's possible to update Klipper extensions using Moonraker.

<br />

## Configuration

-  Open `moonraker.conf` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Add this lines to enable Update Manager:

  ```
  [update_manager]
  enable_auto_refresh: True
  refresh_interval: 24
  enable_system_updates: False
  ```

  - If you use **Fluidd**, enable this lines by removing `#` before (or add this lines if you don't have them):

    ```
    # Remove '#' if you use Fluidd
    [update_manager fluidd]
    type: web
    channel: beta
    repo: fluidd-core/fluidd
    path: /usr/data/fluidd
    ```

  - If you use **Mainsail**, enable this lines by removing `#` before (or add this lines if you don't have them):

    ```
    # Remove '#' if you use Mainsail
    [update_manager mainsail]
    type: web
    channel: beta
    repo: mainsail-crew/mainsail
    path: /usr/data/mainsail
    ```

  - If you use **KAMP**, enable this lines by removing `#` before (or add this lines if you don't have them):

    ```
    # Remove '#' if you use KAMP
    [update_manager KAMP for K1 Series]
    type: git_repo
    channel: dev
    path: /usr/data/KAMP-for-K1-Series
    origin: https://github.com/Guilouz/KAMP-for-K1-Series.git
    primary_branch: main
    ```

  - If you use **Timelapse** function, enable this lines by removing `#` before (or add this lines if you don't have them):

    ```
    # Remove '#' if you use Timelapse function and replace port '4408' by '4409' in snapshoturl if you use Mainsail
    [timelapse]
    output_path: /usr/data/printer_data/timelapse/
    frame_path: /usr/data/printer_data/frames/
    snapshoturl: http://localhost:4408/webcam/?action=snapshot
    ```