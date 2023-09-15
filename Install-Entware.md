Entware is a software repository for devices which use the Linux kernel.

Installing Entware allows packages to be added to your printer to perform new tasks or provide other functionality than what it was marketed for, or simply to perform those functions better.

<br />

**<u>Note:</u> This procedure must be repeated if you update the firmware.**

<br />

## Installation

- If it's not already done, download and unzip this script package: [creality_installer.zip](https://github.com/Guilouz/Creality-K1-and-K1-Max/raw/main/Downloads/creality_installer.zip)

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)) and drap and drop `creality` folder in `/root/` folder on the left side of the window:

  <img width="900" alt="01" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/99f7a4e4-bb1c-4b6f-a559-b9a4a566c905">

- When it's done, enter the following command to run the script:

  ```
  sh .creality/installer.sh
  ```

- You can now install Entware by typing `4` and validate with `Enter` keyboard button:

  <img width="900" alt="Capture d’écran 2023-09-15 à 03 18 53" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/1c9115c1-000c-4cc6-b25a-7ad41c9c724a">

- When it's done, log out of the current SSH session and log in again.

- You can now install packages with this command by replacing `<packagename>` by the name of the package:

  ```
  opkg install <packagename>
  ```

  Example to install Nano (Nano is a small and simple text editor for use on the terminal):

  ```
  opkg install nano
  ```

- The list of available packages can be found [here](https://bin.entware.net/mipselsf-k3.4/Packages.html).

- You can also remove packages with this command by replacing `<packagename>` by the name of the package:

  ```
  opkg remove <packagename>
  ```

- If you want to check available updates from your packages, enter this this commands (one by one):

  ```
  opkg update
  ```

  ```
  opkg upgrade
  ```

<br />

## Add SFTP protocol support

By default, SFTP protocol is not allowed on your printer. This can be useful with some software that only works with SFTP.

- An example with Cyberduck on macOS:

  <img width="700" alt="Capture d’écran 2023-08-27 à 13 07 34" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/2a1f9680-be50-468d-8e5b-1c24874e264c">

- To add support, enter this command:

  ```
  opkg install openssh-sftp-server; ln -s /opt/libexec/sftp-server /usr/libexec/sftp-server
  ```

- SFTP protocol is now allowed:

  <img width="700" alt="Capture d’écran 2023-08-27 à 13 10 01" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/f0d09db9-7ad9-4f6e-b271-d6ef25b64118">
