# Firmware Architecture (Behavior-Preserving)

## Objective

Document code organization for Raspberry Pi Pico W without changing core logic.

## High-Level Structure

## MicroPython variant

```text
src/
  main.py          # Entry point
lib/
  *.py             # Reusable drivers/helpers
docs/
  wiring.md
  architecture.md
```

### Suggested module responsibilities

- `src/main.py`
  - Bootstraps board init and runtime loop.
  - Orchestrates peripherals and network flow.
  - Contains the original logic unchanged.
- `lib/<driver>.py`
  - Device-specific protocol handling (I2C/SPI/UART/GPIO abstraction).
- `lib/<service>.py`
  - Network/service wrappers (MQTT/HTTP/etc.) if used.

## C/C++ Pico SDK variant

```text
include/
  *.h              # Public interfaces
src/
  main.cpp         # Entry point and loop
  *.cpp            # Implementations
CMakeLists.txt
docs/
  wiring.md
  architecture.md
```

### Suggested module responsibilities

- `src/main.cpp`: initialization + scheduler/loop.
- `src/*.cpp`: per-peripheral/business-logic implementation.
- `include/*.h`: stable interfaces and shared constants.

## Runtime Flow Template

1. Board and clock initialization.
2. Peripheral pin configuration.
3. Optional Wi-Fi stack bring-up.
4. Main control loop:
   - read inputs
   - update state
   - drive outputs
   - publish/log data

## Wi-Fi Credential Strategy

- Keep credentials in an untracked local file.
- Load at runtime.
- Fail safely with clear serial diagnostics if missing.

## Integration Checklist

- [ ] Entry file copied without logic edits.
- [ ] Peripheral modules moved without behavior changes.
- [ ] Pin constants verified against `docs/wiring.md`.
- [ ] Wokwi simulation matches real wiring assumptions.
