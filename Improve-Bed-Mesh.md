You can improve Bed Mesh just changing the interpolation from lagrange to bicubic.

- On original Fluidd Web Interface go to `Configuration` and open `printer.conf` file.

- Search macro named `[bed_mesh]` setting and add this lines at the end:

  ```
  algorithm: bicubic
  bicubic_tension: 0.1
  ```

  Like that:

  ```
  [bed_mesh]
  speed: 150
  mesh_min: 5,5
  mesh_max: 295,295
  probe_count: 6,6
  fade_start: 3.0
  fade_end: 10.0
  algorithm: bicubic
  bicubic_tension: 0.1
  ```

- Then, click on `SAVE & RESTART` button in the top right corner.

- Start a new bed leveling with `BED_LEVELING` macro.

  This is my result:

  <img width="1385" alt="Capture d’écran 2023-08-04 à 15 45 27" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/963d1a06-b4ad-4ce8-8ebe-74170c9d9ccc">

  <img width="2545" alt="Capture d’écran 2023-08-04 à 15 19 16" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/c0ad53f3-da62-45c9-a85a-57336a39036f">

<br />