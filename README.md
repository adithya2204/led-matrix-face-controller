# Nova Robot LED Face Controller

Arduino sketch that drives the LED face of the **Nova Robot**, an interactive 3D-printed robot built as a team course project at Amrita Vishwa Vidyapeetham. Five chained MAX7219 8×8 LED matrices form two eyes and a three-panel mouth. The face changes when you send it emoticon-style characters over serial, for example `:)`, `;)`, `8D` or `:P`.

---

## Hardware

| Part | Notes |
|---|---|
| Arduino UNO | any ATmega328P board works |
| 5 × MAX7219 8×8 LED matrix modules | daisy-chained (DOUT of one → DIN of the next) |
| 5 V supply | five matrices at low brightness run from USB; use an external 5 V supply at higher brightness |

**Wiring** (first module in the chain):

| MAX7219 pin | Arduino pin |
|---|---|
| DIN | D13 |
| CLK | D12 |
| CS / LOAD | D11 |
| VCC / GND | 5 V / GND |

**Panel order in the chain:**

| Chain index | Shows |
|---|---|
| 0 | left eye |
| 1 | right eye |
| 2, 3, 4 | mouth: rows 1–8, 9–16 and 17–24 of the 24-row mouth bitmap |

The face bitmaps are stored rotated 90° counter-clockwise, because the sketch writes them with `setRow()` (faster than `setColumn()`). If a panel looks sideways or mirrored, rotate that module rather than editing the bitmaps.

---

## Setup

1. Install the **LedControl** library (by Eberhard Fahle) from the Arduino IDE Library Manager.
2. Open `led_control/led_control.ino`, select your board and port, and upload.
3. Open the Serial Monitor at **19200 baud**.

All panels start cleared at brightness 1 (of 15).

---

## Serial commands

Each character changes either the eyes or the mouth, so you can send them as emoticons: `:)` sets neutral eyes and then a happy mouth.

| Character | Changes | Result |
|---|---|---|
| `:` | eyes | both neutral |
| `;` | eyes | wink (right open, left closed) |
| `8` | eyes | both wide ("spooky") |
| `)` | mouth | happy |
| `(` | mouth | sad |
| `D` / `d` | mouth | very happy (open smile) |
| `P` / `p` | mouth | tongue out |
| `O` / `o` | mouth | open ("surprised") |
| `\|` | mouth | neutral (straight line) |

Any other character is ignored. Anything that can write to a serial port can drive the face: the Serial Monitor, a Python script on a PC, or another microcontroller.

**Adding an expression:** define a new `byte` array (8 rows for an eye, 24 rows for the mouth across three panels), then add a character for it in `loop()` that calls `display_eyes()` or `display_mouth()`. A `closed_eye_down` bitmap is already defined but not mapped to any character yet.

---

## Project context

The Nova Robot was a fifth-semester project for *21ARE302 Microcontrollers and Embedded Systems* (B.Tech Automation and Robotics Engineering, Amrita Vishwa Vidyapeetham, Amritapuri). The robot combined a 3D-printed body, servo-driven arms and shoulders, Bluetooth motion control, a mobile-app interface with a chatbot, and this LED face. The full write-up, including the hardware problems the team ran into, is in [`docs/nova-robot-project-report.pdf`](docs/nova-robot-project-report.pdf).

## Repository layout

```
led-matrix-face-controller/
├── led_control/
│   └── led_control.ino                 # the sketch
└── docs/
    └── nova-robot-project-report.pdf   # course project report
```

## Credits

- The sketch is adapted from **LED display v1.0** by Igor Fonseca Albuquerque, Thiago Farrauche, Diego Augustus and Yhan Christian (credited in the sketch header).
- Nova Robot LED face integration: **Adithya Pothula** and **Siddanth Bhogoju**.
