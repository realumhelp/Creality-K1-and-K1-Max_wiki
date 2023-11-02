It's possible to update Klipper extensions using Moonraker.

<img width="900" alt="Capture d’écran 2023-11-01 à 19 18 08" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/3a01e7a4-1b3f-4d1e-9ea7-7998ae51e1dd">


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

  - If you use **Fluidd**, enable this lines by removing `#` before (or add this lines if you don't have them) like this:

    ```
    # Remove '#' from the lines below if you use Fluidd
    [update_manager fluidd]
    type: web
    channel: beta
    repo: fluidd-core/fluidd
    path: /usr/data/fluidd
    ```

  - If you use **Mainsail**, enable this lines by removing `#` before (or add this lines if you don't have them) like this:

    ```
    # Remove '#' from the lines below if you use Mainsail
    [update_manager mainsail]
    type: web
    channel: beta
    repo: mainsail-crew/mainsail
    path: /usr/data/mainsail
    ```

  - If you use **KAMP**, enable this lines by removing `#` before (or add this lines if you don't have them) like this:

    ```
    # Remove '#' from the lines below if you use KAMP
    [update_manager KAMP for K1 Series]
    type: git_repo
    channel: dev
    path: /usr/data/KAMP-for-K1-Series
    origin: https://github.com/Guilouz/KAMP-for-K1-Series.git
    primary_branch: main
    is_system_service: False
    ```

<br />