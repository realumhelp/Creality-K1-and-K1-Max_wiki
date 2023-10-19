This guide explain how to install firmware and enable Root access.

## Download Links

**Official Rooted Firmwares for Creality K1 Series:**

  - [1.3.2.1](https://drive.google.com/file/d/1-hD7gfqsY3cuEoSbo1h7D2EJTM5Njihk/view?usp=share_link) ([Changelog](https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Changelogs/Changelog_1.3.2.1.txt))

  - [1.3.2.8](https://drive.google.com/file/d/1E7lPZyGdIBAcshr9Ivz-4JR23cSM9dmM/view?usp=share_link) ([Changelog](https://raw.githubusercontent.com/Guilouz/Creality-K1-and-K1-Max/main/Changelogs/Changelog_1.3.2.8.txt))

<br />

<u>Note:</u> The K1 firmwares works without issue on the K1 Max, the detection of the correct printer being carried out by the firmware.

<br />

## Installation

- You need USB drive formatted in FAT32 with 4096 allocation size (or exFAT on some USB drives).

- Copy the desired `.img` firmware file to the root of your USB drive and remove it from your computer.

- Turn on the printer.

- When your are on home screen, plug USB drive on the front of the printer.

- A popup should appear indicating the presence of a new update.

- Press `Upgrade` and wait during the update process.

- When it's done, the printer restarts.

- When you are on the home screen, you can remove the USB drive.

- On the screen UI, go to `Settings` -> on `System` tab in `Self-check` -> check `Input Shaping` and `Auto Leveling` and click on `Start detecting`.

- When self-check is complete, you can now use the printer.

<br />

## Enable Root access

- On the screen UI, go to `Settings` -> `Root account information`:

  <img width="600" alt="01" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/030d49df-de42-4d3d-a91f-cc1127399040">

- Carefully review the disclaimer, check the agreement box, wait 30 seconds and click on `OK` button:

  <img width="600" alt="02" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/3d0f0292-bbad-420a-aeba-6f5a902649f7">

- Root access is now enabled, you can click on `OK` button:

  <img width="600" alt="03" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/a327bd05-6db0-464f-9b4c-7b333651bafd">

- You can now connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)) with:

  - User: `root`
  - Password: `creality_2023`

<br />

<u>Note:</u> Root access must be re-enabled if you restore the printer to default settings.

<br />