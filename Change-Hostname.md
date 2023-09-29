Changing the hostname can be useful if you have multiple K1 printers to give them each a different hostname.

<br />

## Installation

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Hostname Service file`:

  <img width="900" alt="Capture d’écran 2023-09-29 à 22 07 08" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/d3c433e5-532c-4e67-abfb-ab53ac4df3ce">

<br />

## Configuration

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)).

- On the left panel, in File Manager go to this folder:

  ```
  /etc/
  ```

- Then right click on `hotsname` file and click on `Open with default text editor`:

  <img width="900" alt="Capture d’écran 2023-09-18 à 23 25 29" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/f0dac650-a76e-4dc7-8e08-b4ed67ce9ba8">

- Replace `creality` name by name you want.
  
  ⚠ **Be careful to the name, a hostname must not contain spaces, you can replace spaces with hyphens!**

- Then click on `Save file` icon:

  <img width="900" alt="Capture d’écran 2023-09-18 à 23 29 30" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/e59c74c1-e86e-4a75-8019-83d58282533a">

- And click on `Yes` button to save file:

  <img width="600" alt="Capture d’écran 2023-09-18 à 23 33 12" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/d235c76b-506d-4283-a2e2-7a9b941cb444">

- When it's done, on the right panel, in SSH command prompt window enter this command to reboot:

  ```
  reboot
  ```

- It's done, your hostname have been changed.

<br />
