# Cấu hình 

```M92 X80.00 Y80.00 Z400.00 E95.50
M203 X500.00 Y500.00 Z20.00 E120.00
M201 X500.00 Y500.00 Z100.00 E5000.00
M204 P500.00 R500.00 T500.00
Recv: echo:; Advanced: B<min_segment_time_us> S<min_feedrate> T<min_travel_feedrate> X<max_x_jerk> Y<max_y_jerk> Z<max_z_jerk> E<max_e_jerk>
M205 B20000.00 S0.00 T0.00 X10.00 Y10.00 Z0.30 E15.00
M145 S0 H200 B60 F0
M851 X48.00 Y-2.00 Z-0.8
M603 L20.00 U100.00
```

```
Fix

Hello, please confirm “tone.cpp” file in “C:\Users\Administrator.platformio\packages\framework-arduinoststm32-maple\STM32F1\cores\maple” folder is set correctly. If not, please modify it manually and then compile the test.
What needs to be changed is line 34
should be change from

    #define TONE_CHANNEL 8
to

    #define TONE_CHANNEL 4
```
    
    
#define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN

#define ENDSTOPPULLUP_ZMIN_PROBE

#define Z_MIN_ENDSTOP_INVERTING true 

#define Z_MIN_PROBE_ENDSTOP_INVERTING true

#define FIX_MOUNTED_PROBE

#define NOZZLE_TO_PROBE_OFFSET { 48, -2, -1.75 }

#define PROBING_MARGIN 35

#define XY_PROBE_SPEED 10000 //8000

#define Z_PROBE_SPEED_FAST (HOMING_FEEDRATE_Z * 4)

#define Z_CLEARANCE_DEPLOY_PROBE   0 // Z Clearance for Deploy/Stow

#define Z_CLEARANCE_BETWEEN_PROBES  2 // Z Clearance between probe points

#define Z_CLEARANCE_MULTI_PROBE     2 // Z Clearance between multiple probes

#define AUTO_BED_LEVELING_BILINEAR

#define RESTORE_LEVELING_AFTER_G28

#define GRID_MAX_POINTS_X 4

#define Z_SAFE_HOMING

#define Z_MIN_PROBE_REPEATABILITY_TEST

#define ENDSTOP_INTERRUPTS_FEATURE



#define BABYSTEPPING

#define BABYSTEP_ZPROBE_OFFSET

#define STEALTHCHOP_XY

#define STEALTHCHOP_Z

#define STEALTHCHOP_E
