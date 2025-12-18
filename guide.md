# BLTouch on Alfawise U20 (V07 board / TS_V12) — Marlin 2.1.x

This document is a **concise reminder / cheat-sheet** for installing and configuring a **BLTouch** on an **Alfawise U20** using **Marlin 2.1.x**.

The final install will support BLTouch and allow you to modify offset through G-Code if needed.

---

## Hardware (MANDATORY for V06 / V07 / V08 boards)

### 1. Z-min signal connector
- Use the **white 3-pin JST-XH** connector.
- **Clip off the unused 3rd pin** so it fits correctly into the Z-min socket.

---

### 2. Servo connector (black JST)
- Remove the **red (+5V)** wire from the black 3-pin connector.
- Keep:
  - **Brown** → GND  
  - **Orange** → Signal
- Clip the unused 3rd pin → convert it to a **2-pin connector**.

---

### 3. Remove capacitor C29 (CRITICAL)
- **Desolder or carefully remove capacitor C29** from the motherboard.
- This capacitor causes **BLTouch trigger failures** and random behavior.
- Without this step, BLTouch will often **not respond to commands**.

---

### 4. Provide stable 5V power
- Solder the **red (+5V)** BLTouch wire to **capacitor D7** on the motherboard.
- Do **NOT** rely on the original servo 5V rail.

---

## Firmware — Marlin 2.1.x

You must edit **both** files:
- `Configuration.h`
- `Marlin/src/pins/stm32f1/pins_LONGER3D_LK.h`

---

## Configuration.h

### Printer & screen
```cpp
#define U20
#define TS_V12
#define MOTHERBOARD BOARD_LONGER3D_LK
```

---

### Enable BLTouch + Servo
```cpp
#define BLTOUCH
#define Z_PROBE_SERVO_NR 0
#define NUM_SERVOS 1
#define SERVO_DELAY { 300 }
#define BLTOUCH_FORCE_5V_MODE
```

---

### Use probe for Z homing
```cpp
#define USE_PROBE_FOR_Z_HOMING
#define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN
#define Z_SAFE_HOMING
```

---

### Probe offsets (example)
```cpp
#define NOZZLE_TO_PROBE_OFFSET { -36.5, -14, -0.5 }
```

Adapt the values depending on the actual distance between your bltouch and your hotend.

---

### Auto Bed Leveling
```cpp
#define AUTO_BED_LEVELING_BILINEAR
#define RESTORE_LEVELING_AFTER_G28
#define ENABLE_LEVELING_FADE_HEIGHT
```

---

### EEPROM (REQUIRED)
```cpp
#define EEPROM_SETTINGS
```

---

## pins_LONGER3D_LK.h (CRITICAL FIX)

For board before VG0 (V07, V08, ...), you must modify this file to set the correct servo PIN for the bltouch.
If you dont do it, your bltouch will turn on when powering on the printer, but it will not be able to deploy/retract.

```cpp
//#define SERVO0_PWM_OD
#define SERVO0_PIN PE5
```

---

## Compilation 

Use "Auto Build Marlin" with VScode, **make sure to use STM32F103VE_longer_maple**, if you dont use maple the pritner will not start, you will stay stuck on the loading screen when flashing.

---

## Flashing

- Copy `project.bin` to SD card (FAT32)
- Insert SD → power on → wait → if flash worked the printer start automatically

---
