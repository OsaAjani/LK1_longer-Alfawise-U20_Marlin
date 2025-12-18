# BLTouch on Alfawise U20 (V07 board / TS_V12) — Marlin 2.1.x

This works for V07 board and probably any board before VG0

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
