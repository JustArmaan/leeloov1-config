# ZMK Split Keyboard Config

Personal **ZMK firmware configuration** for a split keyboard using a **QWERTY layout** with three layers.

## Layers

### Default (QWERTY)

Main typing layer.

Features:

* Standard QWERTY layout
* Modifier keys (Shift, Ctrl, Alt, GUI)
* Layer-tap keys for quick access to other layers
* Volume control via rotary encoder

Thumb keys:

* `RET` → tap for Enter, hold for Lower layer
* `SPACE` → tap for Space, hold for Lower layer
* `-` and `=` → tap for symbol, hold for Raise layer
* `BSPC` and `DEL`

---

### Lower Layer

Utility and navigation layer.

Includes:

* Function keys `F1–F12`
* Arrow keys
* Navigation keys:

  * Home
  * End
  * Page Up
  * Page Down

Transparent keys fall back to the default layer.

---

### Raise Layer

System and Bluetooth control layer.

Includes:

* Bluetooth profile switching:

  * `BT_SEL 0–4`
* Bluetooth clear (`BT_CLR`)
* Reset (`sys_reset`)
* Bootloader mode for flashing firmware

---

## Rotary Encoder

The encoder controls system volume:

* Clockwise → Volume Up
* Counterclockwise → Volume Down

---

## Key Behaviors

Uses standard ZMK behaviors:

* `&kp` → key press
* `&lt` → layer-tap (tap for key, hold for layer)
* `&trans` → transparent (falls back to lower layer)

Example:

```dts
&lt 1 RET
```

Tap → `Enter`
Hold → activate **Lower layer**

---

## Bluetooth Profiles

The keyboard supports **5 Bluetooth profiles**.

| Key      | Function            |
| -------- | ------------------- |
| BT_SEL 0 | Connect to device 1 |
| BT_SEL 1 | Connect to device 2 |
| BT_SEL 2 | Connect to device 3 |
| BT_SEL 3 | Connect to device 4 |
| BT_SEL 4 | Connect to device 5 |
| BT_CLR   | Clear all pairings  |

---

## Optional nice!view Display

Support for **nice!view OLED displays** is included but commented out.

To enable:

1. Connect the display CS pin to **P0.22 / D4**
2. Uncomment the `nice_view_spi` section in the config.

---

## Building Firmware

Typical ZMK workflow:

```bash
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=<your_keyboard>
```

Flash the firmware to both halves of the keyboard.
