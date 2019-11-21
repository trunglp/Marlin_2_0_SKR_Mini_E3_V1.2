Tham khảo:

https://www.reddit.com/r/ender3/comments/dojh3v/guide_for_those_upgrading_to_an_skr_e3_mini_v12/

https://github.com/morningreis/Marlin-SKR-E3-Mini-1.2

**Cấu hình firmware SKR Mini E3** 

  ```
  #define SERIAL_PORT 2
  
  #define SERIAL_PORT_2 -1
  
  #define MOTHERBOARD BOARD_BTT_SKR_MINI_E3_V1_2
  
  #define DEFAULT_Kp 16.65
  #define DEFAULT_Ki 1.02
  #define DEFAULT_Kd 67.65
```

- **Bed Leveling (LJC18A3-H-Z/BX 1-10mm Capacitance Proximity Sensor Switch NPN NO DC 6-36V 300mA)** 

![image](https://user-images.githubusercontent.com/38026441/69208082-d37d1500-0b84-11ea-84b3-9ad97b7f2e6d.png)

```
#define ENDSTOPPULLUP_ZMIN_PROBE
#define Z_MIN_ENDSTOP_INVERTING true // Set to true to invert the logic of the endstop.
#define Z_MIN_PROBE_ENDSTOP_INVERTING true // Set to true to invert the logic of the probe.
#define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN
#define FIX_MOUNTED_PROBE
#define NOZZLE_TO_PROBE_OFFSET { 10, 10, 0 }
#define MIN_PROBE_EDGE 10
#define AUTO_BED_LEVELING_BILINEAR
#define RESTORE_LEVELING_AFTER_G28
#define GRID_MAX_POINTS_X 3
#define Z_SAFE_HOMING
```

- **S-Curve Acceleration** 
```
#define S_CURVE_ACCELERATION
```

- **Configuration_adv.h** 

```
#define BABYSTEP_ZPROBE_OFFSET
 ```

- **pins_BTT_SKR_MINI_E3_V1_2.h** 

![image](https://user-images.githubusercontent.com/38026441/69303653-5fa83e80-0c50-11ea-96b0-f5c408921d3f.png)

```
#define EEPROM_START_ADDRESS uint32(0x8000000 + 256 * 2048 - 2 * EEPROM_PAGE_SIZE)
```

Sensorless Homing
    SD Card Support

    StealthChop

    Hybrid Threshold

Features not enabled, but can be:

    Linear Advance

    M122 Command
