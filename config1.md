Tham khảo cách cấu hình 

https://www.reddit.com/r/ender3/comments/e894j7/marlin_20x_guide_for_ender_3_using_skr_mini_e3_v12/



default_envs = STM32F103RC_bigtree_512K

Configuration.h:

#define SHOW_CUSTOM_BOOTSCREEN

#define CUSTOM_STATUS_SCREEN_IMAGE

        (For these to be able to work, you will need to copy the _Bootscreen.h, _Statusscreen.h file from Marlin\config\examples\Creality\Ender-3\ to Marlin\Marlin folder)

        You can download the example configuration files from the Marlin GitHub.

#define SERIAL_PORT 2

#define SERIAL_PORT_2 -1

#define BAUDRATE 115200

        (BigTreeTech default baudrate)

#define MOTHERBOARD BOARD_BTT_SKR_MINI_E3_V1_2

    E&C	#define CUSTOM_MACHINE_NAME "Ender-3"

#define DEFAULT_NOMINAL_FILAMENT_DIA 1.75

#define TEMP_SENSOR_BED 1

#define BED_MAXTEMP 125 (Mine is set to 65 for a magnetic bed surface that works to max. 70 °C)

#define PIDTEMPBED

        (Do a PID autotune after you update your firmware, because it will trigger Thermal Runaway Protection when heating the bed up. Help is later in this post.)

#define EXTRUDE_MAXLENGTH 100 (Measure the length from the extruder gear to the nozzle)

#define Z_MIN_PROBE_ENDSTOP_INVERTING true

#define X_DRIVER_TYPE TMC2209

#define Y_DRIVER_TYPE TMC2209

#define Z_DRIVER_TYPE TMC2209

#define E0_DRIVER_TYPE TMC2209

#define DEFAULT_AXIS_STEPS_PER_UNIT { 80, 80, 400, 93 }

#define DEFAULT_MAX_FEEDRATE { 500, 500, 20, 60 }

#define DEFAULT_ACCELERATION 500

#define DEFAULT_RETRACT_ACCELERATION 500

#define DEFAULT_TRAVEL_ACCELERATION 500

#define CLASSIC_JERK

        (Use Classic Jerk instead junction deviation, until bug is fixed)

        (How to calculate Junction Deviation)

#define S_CURVE_ACCELERATION

#define INVERT_X_DIR true

#define INVERT_E0_DIR true

#define X_BED_SIZE 235

#define Y_BED_SIZE 235

#define Z_MAX_POS 250

#define HOMING_FEEDRATE_Z (20*60)

        (Set it to the Hybrid Threshold Z value (3*60) if you want to home quietly in Z direction)

#define EEPROM_SETTINGS

#define NOZZLE_PARK_FEATURE

#define NOZZLE_PARK_POINT { 0, (Y_MAX_POS - 10), 20 }

#define DISPLAY_CHARSET_HD44780

#define SDSUPPORT

#define CR10_STOCKDISPLAY

#define FAN_SOFT_PWM

Configuration_adv.h:

#define QUICK_HOME

#define MANUAL_FEEDRATE { 50*60, 50*60, 4*60, 2*60 }

        (Change (4*60) to the Hybrid Threshold Z value (3*60) for quiet manual Z movement)

#define STATUS_MESSAGE_SCROLLING

#define PRINT_PROGRESS_SHOW_DECIMALS

#define SHOW_REMAINING_TIME

#define USE_M73_REMAINING_TIME

#define ROTATE_PROGRESS_DISPLAY

#define LONG_FILENAME_HOST_SUPPORT

#define SCROLL_LONG_FILENAMES

    E&C	#define SDCARD_CONNECTION ONBOARD

#define STATUS_CHAMBER_ANIM

#define STATUS_HEAT_PERCENT

#define LIN_ADVANCE

#define LIN_ADVANCE_K 0.00

        (Calibrate your K value after you update your firmware, links later in this post.)

#define BLOCK_BUFFER_SIZE 32

#define BLOCK_BUFFER_SIZE 32

#define BUFSIZE 32

#define TX_BUFFER_SIZE 32

#define X_CURRENT 580

#define Y_CURRENT 580

#define Z_CURRENT 580

#define E0_CURRENT 650

#define CHOPPER_TIMING CHOPPER_DEFAULT_24V

#define MONITOR_DRIVER_STATUS

#define HYBRID_THRESHOLD

#define TMC_DEBUG

#define CANCEL_OBJECTS

PID autotune

(Highly recommended, as sometimes with the default values the heated bed will trigger the thermal runaway protection on heat up, if so than you need to autotune your bed PID)

    Connect the printer to the PC via USB

    Use any software that can send gcode commands to a printer via USB ( Pronterface , Simplify3D, etc.)

    Connect to the printer if not done automatically

    Send an M301 to the printer to get the PID values for the HOTEND and take a note of the values

    Send an M304 to the printer to get the PID values for the HEATED BED and take a note of the values

    Send an M303 C < count > E < index > S < temp > U to the printer

        For the hotend I used M303 C25 E0 S205 U ( C5 should be enough, but C25 doesn't take too long either, S < temp > should be the 5-10 more than the printing temperature you usually use)

        For the heated bed I used M303 C25 E-1 S60 U ( C5 should be enough, but if I did 25 for the hotend might as well do it to the bed too, S < temp > should be the bed temperature you usually use)

    Wait for the operation to complete (when it's done the temperature will drop)

    Take a not of the new P, I, D values (they will most likely be different from the original ones)

    Send an M500 to the printer to save the changes in the PID values

    To make sure that all the values are saved, send an M301 and M304 to the printer

    If the PID values match the new ones, then you are good to go, if not then you need to do it manually:- Hotend: Send an M301 P< value > I < value > D< value > to the printer- Heated bed: Send an M304 P< value > I < value > D< value > to the printer- Send an M500 to the printer

    In Configuration.h update the PID values for future firmware updates (DEFAULT_Kp, ...Ki, ...Kd, DEFAULT_bedKp, ...bedKi, ...bedKd)

BLTOUCH

Configuration.h:

#define BLTOUCH

#define NOZZLE_TO_PROBE_OFFSET { -44.5, -10, -1.00 }

        (Edit these values according to your setup)

#define XY_PROBE_SPEED 10000

        Set it to 6000, for silent X/Y probing

#define Z_MIN_PROBE_REPEATABILITY_TEST

#define SOFT_ENDSTOPS_MENU_ITEM

#define AUTO_BED_LEVELING_BILINEAR

        (or use UBL, links down in the post)

#define RESTORE_LEVELING_AFTER_G28

#define Z_SAFE_HOMING

Configuration_adv.h:

#define BLTOUCH_DELAY 500

        (increase it, if you are experiencing failed probing, it might help. Mine is at 900)

#define BABYSTEPPING

#define BABYSTEP_MULTIPLICATOR_Z 8

        (By setting it to 8, it will raise the Z-axis by 0.02 which is half of the magic number, so it can give more consistent result)

#define DOUBLECLICK_FOR_Z_BABYSTEPPING

        (Double-click on the Status Screen for Z Babystepping during prints)

#define BABYSTEP_ZPROBE_OFFSET

Measure NOZZLE_TO_PROBE_OFFSET

    Mount your BLTouch to the printer

    Take rough measurements from the probe pin to the nozzle in X and Y directions

    Change the NOZZLE_TO_PROBE_OFFSET values to the ones you measured

    Compile - flash - boot ...

    Home the printer

    Take a note of the X and Y coordinates (you can do that in the printer move axis menu)

    Move the Z axis down slowly by 1 - 0.1 mm increments until the nozzle touches or almost touches the print bed

    Mark that point where the nozzle touches the bed (make sure that your mark won't move on the bed)

    Move the X and Y axis in the printer menu until the probe pin is spot on to the mark

    Take a note of the X and Y coordinates

    Subtract the X/Y coordinates from the original X/Y coordinates to get the NOZZLE_TO_PROBE_OFFSET

BLTouch wiring

    Teaching Tech guide for SKR mini E3 v1.2 + BLTouch

    Wiring diagram from GitHub

Unified Bed Leveling (UBL)

    Marlin UBL guide

    Chris Riley UBL video guide

Manual Mesh Bed Leveling

Configuration.h

#define PROBE_MANUALLY

#define NOZZLE_TO_PROBE_OFFSET { 0, 0, 0 }

#define MESH_BED_LEVELING

#define RESTORE_LEVELING_AFTER_G28

#define GRID_MAX_POINTS_X 5 (Or change it accordingly to your needs)

#define LCD_BED_LEVELING

Leveling:

Heat up your bed to the temperature you usually print on (e.g. 60°C) (Make sure that there are no plastic on the nozzle, that would alter the nozzles distance to the bed)

    Select: Prepare - Bed Leveling - Level Bed

    Wait for Homing XYZ to complete

    When Click to Begin appears, press the controller button to move to the first point

    Use the controller wheel to adjust Z so that a piece of paper can just pass under the nozzle

    Press the controller button to save the Z value and move to the next point

    Repeat steps 4-5 until completed

    Select: Configuration - Store settings to save the mesh to the EEPROM

    Select: Motion - Fade height: Set it to 20

    Select: Motion - Store settings

    Make a test print, and as it prints you can change the nozzle distance to the bed in Motion - Bed Z with the controller wheel

    Select: Configuration - Store settings


    Marlin Bed Leveling (Manual)

    Teaching Tech Manual Mesh Bed Levelling

    Crosslink Ender 3 Mesh Bed Leveling

Filament Runout Detection and Filament Change

pins_BTT_SKR_MINI_E3.h	(Found it in Marlin\Marlin\src\pins\stm32\)

#define Z_MIN_PROBE_PIN

Switch with 2 pin connector:

#define FIL_RUNOUT_PIN PC14 // "PROBE"

Switch with 3 pin connector:

#define FIL_RUNOUT_PIN PC12 // "PT-DET"

Configuration.h

#define FILAMENT_RUNOUT_SENSOR

    E&C #define FILAMENT_RUNOUT_DISTANCE_MM 5

(Filament Runout detection and M600 - Filament Change part)

#define EXTRUDE_MAXLENGTH 100 (Length from the extruder gear to the nozzle + 10)

#define NOZZLE_PARK_FEATURE

#define NOZZLE_PARK_Z_FEEDRATE 5 (Change it to 3 for quiet z movement)

Configuration_adv.h

#define ADVANCED_PAUSE_FEATURE

#define PAUSE_PARK_RETRACT_FEEDRATE 60 (Change it to your retraction speed)

#define PAUSE_PARK_RETRACT_LENGTH 2 (Change it to your retraction length)

#define FILAMENT_CHANGE_UNLOAD_LENGTH 100 (Length from the extruder gear to the nozzle OR set it to 0 for manual filament extraction)

#define FILAMENT_CHANGE_FAST_LOAD_LENGTH 0 (Length from the extruder gear to the nozzle OR set it to 0 for manual filament insertion)

#define ADVANCED_PAUSE_FANS_PAUSE

#define FILAMENT_CHANGE_ALERT_BEEPS 10 (10 might be too much/annoying, if so lover it to your liking)

#define PARK_HEAD_ON_PAUSE

#define FILAMENT_LOAD_UNLOAD_GCODES

        (Adds M701/M702 Load/Unload G-code, and Load/Unload in the LCD Prepare menu.)

Connect your Runout switch with 2 pin connector to the "PROBE" (PC14) and with 3 pin connector to the "PT-DET" connector on either side of the "SERVOS" (BLTouch) connector. (I use the Z-endstop switch with 2 pin connector for runout sensor)

To change the filament, you can send M600 to the printer manually or insert it directly into your gcode.

Teaching Tech

    DIY filament runout sensor + M600 colour changing

    SKR mini E3 V1.2 guide

Chris Riley

    Marlin Filament Change M600

    Filament Runout Sensor

Linear Advance

    Linear Advance K-factor Calibration

    Teaching Tech Linear advance video guide

    Chris Riley Linear advance video guide

Junction Deviation

    (Use Classic Jerk instead of JD, until the bug (issues/16184, issues/12491) is fixed, the problem is still present in 2020.02.23.)

    Computing Junction Deviation for Marlin Firmware

All in one Retraction testing

    KARL JOHNSON How to Easily Calibrate Retraction in 3D Printers

Z axis StealthChop

Apply these changes to your START/END gcode, if you have problems like this or this.

    Add M569 S1 Z to the start of your START gcode (enable Z stealthchop for quiet homing)

    Add M569 S0 Z to the end of your START gcode (disable Z stealthchop for the print)

    Add M569 S1 Z to the start of your END gcode (enable Z stealthchop for quiet END gcode execution)

Compiling firmware

I used VSCode with the PlatformIO extension and Git GUI.

VSCode installation guide for Marlin 2.0 from Chris Riley.

You can find the firmware file in Marlin/.pio/build/STM32F103RC_bigtree_512K/firmware.bin
Flashing firmware

Place the firmware.bin file onto your SD card, put the card in your printer and turn your printer on. After a short 10-20 sec blank screen your printer should be ready.

If after ~30-40 sec there is still a blank screen, don't worry just turn off your printer. A long blank screen could mean that the firmware you just tried is bad in some way. You could try recompiling it to see if it works.
Reflashing/Updating firmware

Not all changes will be applied on a firmware update, for that you will need to reset your printer settings by going in the printer menu - Configuration - Restore failsafe, or by sending an M502 to the printer. It will reset your settings to your firmware defaults.

When switching to a newer/different version of marlin, you should start from a fresh marlin build and re edit the files, because it can have changes in the configuration files.
Printable Direct Drive mod

Printable Direct Drive extruder mount for Ender 3, Ender 5, CR-10 etc.
