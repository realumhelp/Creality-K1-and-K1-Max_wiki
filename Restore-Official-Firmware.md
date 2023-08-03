You can easily restore Custom Firmware to Official Firmware.

<br />

## Download Links

**Official Firmwares Creality K1:**

  - [1.3.1.14](https://drive.google.com/file/d/1bBI3zHbTUC9k4fL1csL5UeDjJXGb0jL4/view?usp=drive_link)
  - [1.3.1.17](https://drive.google.com/file/d/1su1AYxMEVwH11iteAPxSd_4kpJVI9pCm/view?usp=drive_link)
  - [1.3.1.18](https://drive.google.com/file/d/1mgGfbz8nbU8n2UCXNgQCT6aPTHPgn99r/view?usp=drive_link)

**Official Firmwares Creality K1 Max:**

  - [1.3.0.39](https://drive.google.com/file/d/1sAQEguCromdUTqxiB6xMNPTFfYuo-Joj/view?usp=drive_link)
  - [1.3.1.17](https://drive.google.com/file/d/1BFF9GXpCfQW-z_d4nJZgjc2UOY3KTW5S/view?usp=drive_link)
  - [1.3.1.18](https://drive.google.com/file/d/1NnVGyoz21YsibocyXShKSa5A72f68rAU/view?usp=drive_link)

<br />

## Restoration

- You need USB drive formatted in FAT32.

- Copy the desired `.img` firmware file you want to restore to the root of your USB drive and remove it from your computer.

  ⚠ Make sure there are no other files present on the USB drive.

- Turn on the printer.

- When your are on home screen, plug USB drive on the front of the printer.

- Connect over SSH to the printer, with `root` user and `creality` password and run this command:

  ```
  /etc/ota_bin/local_ota_update.sh /tmp/udisk/sda1/*.img
  ```

- You should then see the progress status as you go in the console.

- When the process is complete, if it says it's successful, just turn off the printer and turn it back on to boot into the new firmware.

<br />