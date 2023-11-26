It's possible to use the buzzer integrated into the motherboard to play a sound during certain actions.

<br />

> [!NOTE]
> **This procedure must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Installation

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Buzzer Support files`:

  <img width="900" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/blob/main/images/Installation-Helper-Script/Installation-Helper-Script.png">

- Then reboot your printer.

<br />

## Configuration

-  Open `gcode_macro.cfg` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- And add this lines:

  ```
  [gcode_shell_command beep]
  command: aplay /usr/data/beep.mp3
  timeout: 2.
  verbose: False

  [gcode_macro BEEP]
   gcode:
     RUN_SHELL_COMMAND CMD=beep
     RUN_SHELL_COMMAND CMD=beep
     RUN_SHELL_COMMAND CMD=beep
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Test the buzzer and make sure you hear the sound by running the `BEEP` macro.

- You can now use `BEEP` command where you want in macros to play a sound.

  Here is an example to play a sound when printing is complete:

  ```
  [gcode_macro END_PRINT]
  gcode:
    PRINT_PREPARE_CLEAR
    M220 S100
    M204 S500
    TURN_OFF_HEATERS
    M107 P1
    M107 P2
    END_PRINT_POINT
    BEEP
    WAIT_TEMP_START
    M84
  ```

<br />
