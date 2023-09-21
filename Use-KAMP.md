Klipper Adaptive Meshing & Purging is an extension that allows you to generate a mesh only in the area you really need it: where you print!

Since the mesh area will be smaller, the mesh can be much more dense. Imagine making a 3x3 mesh, but the size of a [3DBenchy](https://www.3dbenchy.com/)!

KAMP also works if prints are started directly through the printer screen by checking the `Calibration` box before starting printing.

More info about KAMP here: [Github](https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging)

<br />

**<u>Note:</u> This procedure must be repeated if you update the firmware or if you restore the printer to default settings.**

<br />

## Installation

- Make sure you have followed this [Installation Helper Script](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/Installation-Helper-Script) section before.

- In the script, enter in `[Install Menu]` by typing `1` and validate with `Enter` and install `Klipper Adaptive Meshing & Purging`:

  <img width="900" alt="Capture d’écran 2023-09-18 à 23 14 51" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/ca710b1d-ac38-460a-99d3-6b31fbb5ee90">

<br />

## Configuration

-  Open `moonraker.conf` file:

   - On original Fluidd Web Interface go to `Configuration` icon on the left side.
   - On original Mainsail Web Interface go to `Machine` tab on the left side.

- Search `[file_manager]` section and change value of `enable_object_processing` setting to `True` like this:

  ```
  # Set to 'True' if you use KAMP
  enable_object_processing: True
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Open `printer.cfg` file and add this line to enable KAMP:

    ```
    [include KAMP_Settings.cfg]
    ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- You can now open `KAMP_Settings.cfg` file and enable **Adaptive Meshing** by removing `#` like this:

  ```
  [include ./KAMP/Adaptive_Meshing.cfg]       # Include to enable adaptive meshing configuration.
  # [include ./KAMP/Line_Purge.cfg]             # Include to enable adaptive line purging configuration.
  # [include ./KAMP/Voron_Purge.cfg]            # Include to enable adaptive Voron logo purging configuration.
  # [include ./KAMP/Smart_Park.cfg]             # Include to enable the Smart Park function, which parks the printhead near the print area for final heating.
  ```

  ⚠ **Other features don't work properly due to `CX_PRINT_DRAW_ONE_LINE` macro embedded in firmware.**
    
    **If you also want to activate the Line Purge and Smart Park functions, see the next section.**

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Open `gcode_macro.cfg` file, search macro named `[gcode_macro START_PRINT]` and disable `CX_PRINT_LEVELING_CALIBRATION` command by adding a `#` and add `BED_MESH_CLEAR` and `BED_MESH_CALIBRATE` commands like this: 

  ```
  [gcode_macro START_PRINT]
  variable_prepare: 0
  gcode:
    WAIT_TEMP_END
    CLEAR_PAUSE
    {% set g28_extruder_temp = printer.custom_macro.g28_ext_temp %}
    {% set bed_temp = printer.custom_macro.default_bed_temp %}
    {% set extruder_temp = printer.custom_macro.default_extruder_temp %}
    {% if 'BED_TEMP' in params|upper and (params.BED_TEMP|float) %}
    {% set bed_temp = params.BED_TEMP %}
    {% endif %}
    {% if 'EXTRUDER_TEMP' in params|upper and (params.EXTRUDER_TEMP|float) %}
    {% set extruder_temp = params.EXTRUDER_TEMP %}
    {% endif %}
  
    {% if printer['gcode_macro START_PRINT'].prepare|int == 0 %}
      {action_respond_info("not prepare.\n")}
      PRINT_PREPARE_CLEAR
      CX_ROUGH_G28 EXTRUDER_TEMP={extruder_temp} BED_TEMP={bed_temp}
      CX_NOZZLE_CLEAR
      ACCURATE_G28
      #CX_PRINT_LEVELING_CALIBRATION
      BED_MESH_CLEAR
      BED_MESH_CALIBRATE
    {% else %}
      PRINT_PREPARE_CLEAR
    {% endif %}
  
    CX_PRINT_DRAW_ONE_LINE
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Open `moonraker.conf` file and enable this lines by removing `#` before like this (or add this lines if you don't have them):

  ```
  [update_manager Klipper Adaptive Meshing Purging]
  type: git_repo
  channel: dev
  path: /usr/data/Klipper-Adaptive-Meshing-Purging
  origin: https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging.git
  managed_services: klipper
  primary_branch: main
  ```

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Also make sure `Label Objects` setting is enabled in your slicer.

- It's done. You have now **Adaptive Meshing** when printing starting.

⚠ **In some cases, printing may fail to start with some large models. To get around this, you can either try to start printing from the screen rather than via the Web interface.**

<br />

## Enable Line Purging and Smart Park functions

- Open `KAMP_Settings.cfg` file and configure it like this:

  <img width="900" alt="Capture d’écran 2023-09-18 à 02 21 25" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/b18f6118-7a9f-4b67-9c34-8cebc6ef57a5">

- Then, click on `SAVE AND RESTART` button in the top right corner.

- Connect to SSH (Guide is available [here](https://github.com/Guilouz/Creality-K1-and-K1-Max/wiki/SSH-Connection)).

- On the left panel, in File Manager go to this folder:

  ```
  /usr/share/klipper/klippy/extras/
  ```

- Then right click on `custom_macro.py` file and click on `Open with default text editor`:

  <img width="900" alt="Capture d’écran 2023-09-18 à 02 24 06" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/0503fd2a-f020-43d9-bc07-85d29c6b767d">

- Replace existing `cmd_CX_PRINT_DRAW_ONE_LINE_help` command by this one:

  ```
  cmd_CX_PRINT_DRAW_ONE_LINE_help = "Draw one line before printing"
  def cmd_CX_PRINT_DRAW_ONE_LINE(self, gcmd):
    self.gcode.run_script_from_command('M83')
    self.gcode.run_script_from_command('SMART_PARK')
    self.gcode.run_script_from_command('G91')
    self.gcode.run_script_from_command('G1 Y-10 F600')
    self.gcode.run_script_from_command('G90')
    self.gcode.run_script_from_command('G1 Z0.8 F600')
    self.pheaters = self.printer.lookup_object('heaters')
    self.heater_hot = self.printer.lookup_object('extruder').heater
    self.gcode.respond_info("can_break_flag = %d" % (self.pheaters.can_break_flag))
    self.gcode.run_script_from_command('M104 S%d' % (self.extruder_temp))
    self.gcode.run_script_from_command('M140 S%d' % (self.bed_temp))
    self.pheaters.set_temperature(self.heater_hot, self.extruder_temp, True)
    self.gcode.respond_info("can_break_flag = %d" % (self.pheaters.can_break_flag))
    while self.pheaters.can_break_flag == 1:
       time.sleep(1)
    self.gcode.respond_info("can_break_flag = %d" % (self.pheaters.can_break_flag))
    if self.pheaters.can_break_flag == 3:
        self.pheaters.can_break_flag = 0
        self.gcode.respond_info("can_break_flag is 3")
        self.gcode.run_script_from_command('M220 S100')
        self.gcode.run_script_from_command('M221 S100')
        self.gcode.run_script_from_command('LINE_PURGE')
    pass
  ```

  ⚠ **Be careful to respect the indentation of the file!**

  <img width="900" alt="268537895-2dc7e40d-70b0-4202-8153-c523580105ee copie" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/b1c61ef7-724f-41e2-8004-7bb4a8ab3139">

- Then click on `Save file` icon:

  <img width="900" alt="Capture d’écran 2023-09-18 à 02 59 40" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/ba26eae9-004a-4dd7-b101-e91045760310">

- And click on `Yes` button to save file:

  <img width="600" alt="Capture d’écran 2023-09-18 à 03 00 26" src="https://github.com/Guilouz/Creality-K1-and-K1-Max/assets/12702322/57eb5d05-dcba-429e-8f45-0b5e3638b813">

- When it's done, on the right panel, in SSH command prompt window enter this command to restart Klipper service:

  ```
  /etc/init.d/S55klipper_service restart
  ```

- It's done. You have now **Adaptive Meshing** when printing starting, the hotend which is parked next to the printing area during heating and the optimized purge line next to the printing area.

<br />

<u>Note:</u> This is the original `cmd_CX_PRINT_DRAW_ONE_LINE_help` command if you need to restore it.

  ```
  cmd_CX_PRINT_DRAW_ONE_LINE_help = "Draw one line before printing"
  def cmd_CX_PRINT_DRAW_ONE_LINE(self, gcmd):
      self.gcode.run_script_from_command('M83')
      self.gcode.run_script_from_command('G1 X10 Y10 Z2 F6000')
      self.gcode.run_script_from_command('G1 Z0.1 F600')
      self.pheaters = self.printer.lookup_object('heaters')
      self.heater_hot = self.printer.lookup_object('extruder').heater
      self.gcode.respond_info("can_break_flag = %d" % (self.pheaters.can_break_flag))
      self.gcode.run_script_from_command('M104 S%d' % (self.extruder_temp))
      self.gcode.run_script_from_command('M140 S%d' % (self.bed_temp))
      self.pheaters.set_temperature(self.heater_hot, self.extruder_temp, True)
      self.gcode.respond_info("can_break_flag = %d" % (self.pheaters.can_break_flag))
      while self.pheaters.can_break_flag == 1:
          time.sleep(1)
      self.gcode.respond_info("can_break_flag = %d" % (self.pheaters.can_break_flag))
      if self.pheaters.can_break_flag == 3:
          self.pheaters.can_break_flag = 0
          self.gcode.respond_info("can_break_flag is 3")
          self.gcode.run_script_from_command('G21')
          self.gcode.run_script_from_command('G1 F2400 E-0.5')
          self.gcode.run_script_from_command('SET_VELOCITY_LIMIT SQUARE_CORNER_VELOCITY=5')
          self.gcode.run_script_from_command('M204 S12000')
          self.gcode.run_script_from_command('G21')
          self.gcode.run_script_from_command('SET_VELOCITY_LIMIT ACCEL_TO_DECEL=6000')
          # self.gcode.run_script_from_command('SET_PRESSURE_ADVANCE ADVANCE=0.04')
          # self.gcode.run_script_from_command('SET_PRESSURE_ADVANCE SMOOTH_TIME=0.04')
          self.gcode.run_script_from_command('M220 S100')
          self.gcode.run_script_from_command('M221 S100')
          self.gcode.run_script_from_command('G1 Z2.0 F1200')
          self.gcode.run_script_from_command('G1 X0.1 Y20 Z0.3 F6000.0')
          self.gcode.run_script_from_command('G1 X0.1 Y180.0 Z0.3 F3000.0 E10.0')
          self.gcode.run_script_from_command('G1 X0.4 Y180.0 Z0.3 F3000.0')
          self.gcode.run_script_from_command('G1 X0.4 Y20.0 Z0.3 F3000.0 E10.0')
          self.gcode.run_script_from_command('G1 Y10.0 F3000.0')
          self.gcode.run_script_from_command('G1 Z2.0 F600.0')
          self.gcode.run_script_from_command('G1 Z0.3 F600.0')
          self.gcode.run_script_from_command('G1 Z2.0 F600.0')
          # self.gcode.run_script_from_command('G1 X0.4 Y10.0 Z0.3 F6000.0')
          self.gcode.run_script_from_command('M82')
          self.gcode.run_script_from_command('G92 E0')
          # self.gcode.run_script_from_command('G1 Z2.0 F600')
          self.gcode.run_script_from_command('G1 F12000')
          self.gcode.run_script_from_command('G21')
      pass
  ```

<br />