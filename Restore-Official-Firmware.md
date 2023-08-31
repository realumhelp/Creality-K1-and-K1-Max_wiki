You can easily restore Custom Firmware to Official Firmware.

<br />

## Download Links

**Official Firmwares Creality K1:**

  - [1.3.1.14](https://drive.google.com/file/d/1bBI3zHbTUC9k4fL1csL5UeDjJXGb0jL4/view?usp=drive_link) ([Changelog](https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Changelogs/Changelog_1.3.1.14.txt))

  - [1.3.1.28](https://drive.google.com/file/d/1K_puuzls05acWpUCoj7X0X3TL9UsiDV2/view?usp=drive_link) ([Changelog](https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Changelogs/Changelog_1.3.1.14.txt))

**Official Firmwares Creality K1 Max:**

  - [1.3.0.39](https://drive.google.com/file/d/1sAQEguCromdUTqxiB6xMNPTFfYuo-Joj/view?usp=drive_link) ([Changelog](https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Changelogs/Changelog_1.3.0.39.txt))
  - [1.3.1.19](https://drive.google.com/file/d/1RgF_MVfBl-j2EqPCftSEQtwtOOCf6YeA/view?usp=drive_link) ([Changelog](https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Changelogs/Changelog_1.3.1.19.txt))

<br />

## Restoration

- You need USB drive formatted in FAT32.

- Copy the desired `.img` firmware file you want to restore to the root of your USB drive and remove it from your computer.

  ⚠ **Make sure there is no other file present on the USB drive except the firmware file.**

- Turn on the printer.

- When your are on home screen, plug USB drive on the front of the printer.

- Connect over SSH to the printer (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)) and run this command:

  ```
  /etc/ota_bin/local_ota_update.sh /tmp/udisk/sda1/*.img
  ```

- You should then see the progress status as you go in the console.

- When the process is complete, if it says it's successful, just turn off the printer and turn it back on to boot into the new firmware.

- On the screen UI, go to `Settings` -> on `System` tab in `Self-check` -> check `Input Shaping` and `Auto Leveling` and click on `Start detecting`.

<br />