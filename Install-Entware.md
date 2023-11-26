Entware is a software repository for devices which use the Linux kernel.

Installing Entware allows packages to be added to your printer to perform new tasks or provide other functionality than what it was marketed for, or simply to perform those functions better.

<br />

> [!NOTE]
> **This procedure must be repeated if you update the firmware.**

<br />

## Installation

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Entware`:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Installation-Helper-Script/Installation-Helper-Script.png">


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

- If you want to check available updates from your packages, enter this commands (one by one):

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

  <img width="700" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Install-Entware/sftp_01.png">

- To add support, enter this command:

  ```
  opkg install openssh-sftp-server; ln -s /opt/libexec/sftp-server /usr/libexec/sftp-server
  ```

- SFTP protocol is now allowed:

  <img width="700" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Install-Entware/sftp_02.png">

<br />