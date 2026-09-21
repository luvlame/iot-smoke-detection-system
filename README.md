# iot-smoke-detection-system
IoT smoke detection system using Arduino Uno, MQ-2 gas sensor, LED/buzzer alarm, LCD display, and pushbutton reset. Simulated in TinkerCAD.
This system detects dangerous smoke levels using an MQ-2 gas sensor. When smoke is detected above a threshold, it activates a red LED and piezo buzzer alarm while displaying a warning on a 16x2 LCD. The alarm remains active until the user presses the reset button.

## Features

- **Smoke Detection** — MQ-2 gas sensor reads analog values (0–1023) and triggers an alarm above threshold
- **Visual Alarm** — Red LED flashes when smoke is detected
- **Audio Alarm** — Piezo buzzer sounds at 523 Hz
- **LCD Feedback** — 16x2 display shows live system status
- **Manual Reset** — Pushbutton (INPUT_PULLUP) clears the alarm state
- **Serial Monitoring** — Real-time sensor values printed to Serial Monitor

## Hardware Components

| Component | Quantity |
|-----------|----------|
| Arduino Uno R3 | 1 |
| MQ-2 Gas Sensor | 1 |
| 16x2 LCD Display | 1 |
| Piezo Buzzer | 1 |
| Red LED | 1 |
| Pushbutton | 1 |
| Potentiometer (250 kΩ) | 1 |
| Resistor (220 Ω) | 2 |
| Breadboard | 1 |

## Wiring Summary

| Component | Arduino Pin |
|-----------|-------------|
| MQ-2 Gas Sensor | A0 |
| LED | 13 (via 220Ω resistor) |
| Buzzer | 8 |
| Pushbutton | Input (INPUT_PULLUP) |
| LCD | 7, 6, 5, 4, 3, 2 |

## How It Works

1. The MQ-2 sensor continuously reads air quality and sends an analog signal to pin A0.
2. The Arduino converts this to a value between 0 and 1023.
3. If the value exceeds the threshold (900), the alarm state activates.
4. In alarm state: LED turns on, buzzer sounds at 523 Hz, LCD shows "SMOKE DETECTED / PRESS RESET".
5. Pressing the pushbutton clears the alarm and returns the system to "SYSTEM NORMAL / NO SMOKE".

## Code

The full Arduino sketch is in [`smoke_detection.ino`](smoke_detection.ino).

```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(7, 6, 5, 4, 3, 2);
bool alarmActive = false;
