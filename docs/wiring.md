# Wiring and GPIO Mapping (Raspberry Pi Pico W)

## Scope

This document explains hardware wiring and GPIO usage for this project.

> **Assumption notice:** `diagram.json` was not available in this repository snapshot. The component list and connection matrix below are a safe template you should update directly from your Wokwi diagram.

## Components List (Template)

Populate from `diagram.json` `parts` entries:

| Ref | Component | Notes |
|---|---|---|
| U1 | Raspberry Pi Pico W | RP2040 + CYW43439 Wi-Fi |
| D1 | LED (external, optional) | If used in diagram |
| R1 | Resistor (e.g., 220Ω) | LED current limiting |
| S1 | Pushbutton (optional) | User input |
| X1 | Sensor/Peripheral (optional) | Fill exact model |

## Pico W Pin Reference (Common Logical Mapping)

| Pico Label | RP2040 GPIO | Typical Use |
|---|---:|---|
| GP0 | GPIO0 | UART0 TX / GPIO |
| GP1 | GPIO1 | UART0 RX / GPIO |
| GP2..GP22 | GPIO2..GPIO22 | Digital IO / buses |
| GP26 | GPIO26 / ADC0 | Analog input |
| GP27 | GPIO27 / ADC1 | Analog input |
| GP28 | GPIO28 / ADC2 | Analog input |
| 3V3(OUT) | - | Peripheral supply |
| VSYS | - | Main input supply |
| GND | - | Ground return |

## Project GPIO Mapping (Fill from Firmware + Diagram)

| Signal | Pico W Pin | Direction | Connected Part Pin | Purpose |
|---|---|---|---|---|
| STATUS_LED | GP25 or external GPx | Output | LED anode (via resistor) | Status indication |
| USER_BUTTON | GPx | Input (pull-up/down) | Button terminal | User interaction |
| I2C_SDA | GPx | Bidirectional | Peripheral SDA | I2C data |
| I2C_SCL | GPx | Output | Peripheral SCL | I2C clock |
| UART_TX | GP0 (example) | Output | Peripheral RX | Debug/data |
| UART_RX | GP1 (example) | Input | Peripheral TX | Debug/data |

## Wokwi Notes

- Confirm each `connections` net in `diagram.json` maps 1:1 with firmware pin constants.
- Keep power rails explicit (`3V3`, `GND`) to avoid ambiguous simulation behavior.

## Real Hardware Notes

- Verify voltage compatibility (Pico W GPIO is 3.3V logic).
- Include pull-up resistors where protocol requires (e.g., I2C if peripheral board lacks them).
- Keep wiring short for high-speed signals and noisy environments.
