# BLTouch on Alfawise U20 (V07 board / TS_V12)

This works for V07 board and probably any board before VG0

---

## Firmware — Marlin 2.1.x

You must edit **both** files:
- `Configuration.h`
- `Marlin/src/pins/stm32f1/pins_LONGER3D_LK.h`

You must start by replacing the configurations files in Marlin with the file examples for Alfawise U20 Bltouch from marlin repository (https://github.com/MarlinFirmware/Configurations).

---

## Configuration.h



### Printer & screen

Set the proper name for the printer, select the correct touch screen version (1.2 if blue PCB, 1.1 if green), and the proper board.

```cpp
#define U20
#define TS_V12
#define MOTHERBOARD BOARD_LONGER3D_LK
```

---

### Enable BLTouch + Servo

Enable BLTOUCH by uncommenting it if not done, enable the servo so the BLTouch can be used, 

```cpp
#define BLTOUCH
#define Z_PROBE_SERVO_NR 0
#define NUM_SERVOS 1
#define SERVO_DELAY { 300 }
#define BLTOUCH_FORCE_5V_MODE // Comment if not using a genuine BLTouch but a clone
```

---

Configure Z homing to use BLTouch instead of interruptor.

### Use probe for Z homing
```cpp
#define USE_PROBE_FOR_Z_HOMING
#define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN
#define Z_SAFE_HOMING
```

---

### Probe offsets (example)

Define the position of your BLTouch relative to your nozzle.

```cpp
#define NOZZLE_TO_PROBE_OFFSET { -36.5, -14, -0.5 }
```

Thoses values (36.5mm to the left, 14mm to the front, 0.5mm from the tip) are example, based on my own config with the 3D model in this repository.

Adapt the values depending on the actual distance between your bltouch and your hotend.


---

### Auto Bed Leveling

Enables automatic bed leveling using a bilinear mesh, automatically enable leveling after homing (if not printer might not take into account your leveling steps), gradually ignore bed leveling to avoid distortion of print, test with and without and see if you want it or not.

```cpp
#define AUTO_BED_LEVELING_BILINEAR
#define RESTORE_LEVELING_AFTER_G28
#define ENABLE_LEVELING_FADE_HEIGHT
```

---

### EEPROM (REQUIRED)

Enable storing of parameters on the printer memory (in our case the SDCard is used as we dont have any internal memory).

```cpp
#define EEPROM_SETTINGS
```

---

## pins_LONGER3D_LK.h (CRITICAL FIX)

For board before VG0 (V07, V08, ...), you must modify this file to set the correct servo PIN for the bltouch.
If you dont do it, your bltouch will turn on when powering on the printer (it does so whenever getting current), but then it will not be able to deploy/retract once started.

```cpp
//#define SERVO0_PWM_OD
#define SERVO0_PIN PE5
```

---

## Compilation 

Use "Auto Build Marlin" with VScode, **make sure to use STM32F103VE_longer_maple**, if you dont use maple the pritner will not start, you will stay stuck on the loading screen when flashing.


