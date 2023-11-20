**20/11/2023**
- Added support for M191 to control chamber fan in [Improve Fans Control](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Improve-Fans-Control) section.

**18/11/2023**
- Updated script to v3.6 to install OctoEverywhere in /usr/data/ folder (before /usr/share/). Please remove and reinstall it.

**17/11/2023**
- Updated script to v3.5 to fix IP address in System menu.
- Updated [Improve Fans Control](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Improve-Fans-Control) section to control motherboard fan.

**15/11/2023**
- Added new 1.3.2.20 official firmware.
- Added support for hotsname with Creality CR-10 SE.
- Updated script to v3.4 to add support for OctoEverywhere.

**05/11/2023**
- Added new [Change Wi-Fi location](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Change-Wi%E2%80%90Fi-location) section.

**03/11/2023**
- Added new [Fix printing Gcode from folder](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Fix-printing-Gcode-from-folder) section.

**02/11/2023**
- Fixed KAMP warning in Update Manager

**01/11/2023 #2**
- Updated script to v3.3. KAMP for K1 Series have now a repository (https://github.com/Guilouz/KAMP-for-K1-Series). It can be included in update manager for future updates. Please uninstall and reinstall KAMP.
- Updated [Use KAMP](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-KAMP) section with new configuration.
- Added new [Update Manager](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Update-Manager) section.

**01/11/2023**
- Updated script to v3.2 to fix out of range error with KAMP. Please uninstall and reinstall it.
- Updated [Use KAMP](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-KAMP) section with new configuration.
- Added firmware 1.3.2.14 provided by Creality which fixes issues related to version 1.3.2.8. Not yet published, use at your own risk!

**27/10/2023**
- Removed 1.3.2.8 firmware. Creality has removed the firmware from their servers due to several issues.

**23/10/2023**
- Updated script to v3.1:
  - Updated KAMP to latest version. Please uninstall and reinstall it.
  - Added changelog when new script version is available.

**22/10/2023**
- Updated [Change Hostname](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Change-Hostname) section.
- Updated script to v3.0 with new hostname service file for older firmwares than 1.3.2.8.

**21/10/2023**
- Added new [Reset Factory Settings](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Reset-Factory-Settings) section.

**19/10/2023**
- Updated for new 1.3.2.8 firmware.

**18/10/2023**
- Updated [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section.
- Updated [Fix issue with Input Shaper](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Fix-issue-with-Input-Shaper) section.

**11/10/2023**
- Updated script to v2.9 for another Entware install fix.

**10/10/2023**
- Updated script to v2.8 to fix Entware install issue.
- Improved Timelapse render.

**09/10/2023**
- Updated script to v2.7:
  - Added a new system menu to display some system information.
  - Fixed typo.

**08/10/2023**
- Added [Useful Links](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Useful-Links) section.
- Updated script to v2.6:
  - It's now possible to update the script to the latest version directly from the script.
  - Now allow lower and upper case for inputs.
  - Fixed KAMP folder path.

**07/10/2023**
- Updated script to v2.5:
  - Simplified KAMP installation. Updated [Use KAMP](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-KAMP) section.
  - Klipper Gcode Shell Command can now be installed alone.

**06/10/2023**
- Updated script to v2.4 to allow to remove Entware and all installed packages.

**05/10/2023**
- Updated script to v2.3 to allow to control camera settings.
- Added new [Camera Settings Control](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Camera-Settings-Control) section.

**02/10/2023**
- Updated script to v2.2:
  - Improved script code.
  - Added fix for KAMP mesh issue (please remove and reinstall it) and not needed anymore to edit manually custom_macro.py file.
  - Added informations menu to know what is installed or not.
  - Other fixes.

**29/09/2023**
- Fixed "TLS error from peer" in script (thanks to [MuaiyadTSB](https://github.com/MuaiyadTSB)).
- Updated script to v2.1 to allow control fans when cleaning the nozzle.
- Added new [Improve Fans Control](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Improve-Fans-Control) section.

**28/09/2023**
- Updated script to v1.9 to remove TLS certificate validation when downloading files.
- Updated script to v2.0 to add support for motherboard buzzer.
- Added new [Use Motherboard Buzzer](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-Motherboard-Buzzer) section.

**23/09/2023**
- Updated Custom Boot Display for K1.

**22/09/2023**
- Updated script to v1.8 with more warnings.
- Moonraker.tar file updated to allow uploading files larger than 98MB to Web Interface (The /tmp folder used by Moonraker has a size of 98.1M, it has been moved to the /usr/data/moonraker/tmp folder). Please remove and reinstall Moonraker from Helper Script.

**21/09/2023**
- Updated script to v1.7 to install Custom Boot Display and restore stock one.

**18/09/2023**
- Updated [Use KAMP](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-KAMP) section.
- Updated script to v1.6 to install/remove Hostname Service and add user confirmation before install/remove.
- Added new [Change Hostname](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Change-Hostname) section.
- Updated [Boards Layout](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Boards-Layout) section.

**17/09/2023**
- Updated script to v1.5 to install/remove Moonraker Timelapse.
- Reworked script with menus.
- Add new [Use Timelapse](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-Timelapse) section.
- Add new [Use KAMP](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Use-KAMP) section.

**16/09/2023:**
- Fix multiple instances when installing Moonraker.
- Updated script to v1.3 to install/remove Mobileraker Companion.
- Updated script to v1.4 to install/remove KAMP.

**15/09/2023:**
- Updated Wiki to use latest Creality Rooted firmware .

**04/09/2023:**
- Fixed macros indentation.

**03/09/2023:**
- Updated macros.

**02/09/2023:**
- Added new [Useful Macros](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Useful-Macros) section.

**31/08/2023:**
- Added new rooted firmware v1.3.1.28 for K1.

**27/08/2023:**
- Added new [Install Entware](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Entware) section.
- Added profiles for OrcaSlicer and Creality K1.

**20/08/2023:**
  - Updated OrcaSlicer profiles.

**18/08/2023:**
- Added new rooted firmware v1.3.1.19 for K1 Max.
- Added [Update Moonraker](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Update-Moonraker) section.
- Added [Install Mainsail](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Install-Mainsail) section.

**10/08/2023:**
- Added [Permanent Moonraker Configuration](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Permanent-Moonraker-Configuration) section.

**08/08/2023:**
- Improved [Fix issue with Input Shaper](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Fix-issue-with-Input-Shaper) section.
- Updated OrcaSlicer profile to roll back wall generator to classic mode.

**06/08/2023:**
  - Updated OrcaSlicer profile to shutdown fans after print.

**04/08/2023:**
  - Starting repo.