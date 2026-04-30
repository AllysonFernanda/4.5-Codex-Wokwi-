# Raspberry Pi Pico W Project Template (Documentation-First)

This repository has been normalized into a clean Raspberry Pi Pico W layout focused on maintainability and documentation, while preserving firmware logic files as-is.

> **Current status:** The original firmware source code and `diagram.json` content were not present in this repository at the time of generation. The structure and docs below are prepared so you can drop in your existing files without changing behavior.

## Repository Structure

For a **MicroPython** Pico W project:

```text
.
├── README.md
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── lib/
└── src/
    └── main.py
```

If you use **Pico SDK C/C++** instead, use this variant:

```text
.
├── CMakeLists.txt
├── README.md
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── include/
└── src/
    └── main.cpp
```

## Features (Documentation Scaffold)

- Clean project layout aligned with Pico W best practices.
- Separate wiring and architecture documentation.
- Ready-to-fill GPIO mapping and component inventory.
- Wokwi and real-hardware run instructions.
- Wi-Fi credential handling guidance that avoids committing secrets.

## How to Add Your Existing Firmware (No Logic Changes)

1. Place your current firmware entry file in:
   - `src/main.py` (MicroPython), or
   - `src/main.cpp` (Pico SDK C/C++).
2. Keep your logic unchanged.
3. Place dependencies in:
   - `lib/` for MicroPython modules, or
   - `include/` + `src/` for C/C++.
4. Add your Wokwi hardware file as `diagram.json` at repository root.

## Running in Wokwi

1. Add/confirm these files in the project root:
   - `diagram.json`
   - `src/main.py` (or `src/main.cpp` for SDK builds)
2. In Wokwi, open/import the repository.
3. Ensure the diagram board is set to **Raspberry Pi Pico W**.
4. Start simulation and monitor serial output.

## Running on Real Pico W Hardware

### MicroPython Flow

1. Flash MicroPython UF2 for **Raspberry Pi Pico W**.
2. Copy project files to the board filesystem:
   - `src/main.py` should become `/main.py` on-device (or use a small launcher).
   - copy required files from `lib/`.
3. Reset board and monitor UART/USB serial.

### C/C++ Pico SDK Flow

1. Install Pico SDK toolchain.
2. Configure and build with CMake.
3. Copy generated UF2 to Pico W mass-storage device in BOOTSEL mode.

## Wi-Fi Configuration (Without Exposing Credentials)

If your firmware uses Wi-Fi, avoid hardcoding SSID/password in tracked files.

Recommended pattern:

- Keep a local untracked file (example: `wifi_secrets.py` for MicroPython).
- Import credentials from that file in `main.py`.
- Commit only a template like `wifi_secrets.example.py`.
- Add real secrets file to `.gitignore`.

Example template:

```python
# wifi_secrets.example.py
WIFI_SSID = "YOUR_SSID"
WIFI_PASSWORD = "YOUR_PASSWORD"
```

## Component List and Pin Mapping

See `docs/wiring.md` for:

- Components inventory (from `diagram.json` once provided)
- Pico W GPIO mapping table
- Net-by-net connection notes

## Architecture Notes

See `docs/architecture.md` for:

- Module boundaries
- Suggested file responsibilities
- Behavior-preserving organization strategy

## Assumptions

Because firmware and `diagram.json` were not included in this checkout, documentation currently includes clearly marked placeholders and a conservative default mapping table. Replace placeholders with exact values from your source files.
