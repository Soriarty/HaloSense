# WCH CH340X USB-to-UART Bridge

## Component Overview

**Manufacturer:** WCH (Nanjing Qinheng Microelectronics)
**Part Number:** CH340X
**Type:** USB to UART Bridge IC
**Package:** MSOP-10

## Purpose in HaloSense

USB programming and debug interface for ESP32:
- USB-to-UART conversion for ESP32 programming
- DTR/RTS flow control for automatic bootloader entry
- No external crystal required (internal oscillator)
- Compatible with common USB-UART drivers

## Key Specifications

| Parameter | Specification |
|-----------|--------------|
| **Interface** | USB 2.0 Full Speed (12 Mbps) |
| **UART Baud Rate** | Up to 2 Mbps |
| **Supply Voltage** | 3.3V or 5V I/O compatible |
| **Package** | MSOP-10 |
| **Driver** | Built-in to most OS (Linux, Windows, macOS) |

## ESP32 Connection

- **TXD** → GPIO3 (U0RXD)
- **RXD** → GPIO1 (U0TXD)
- **DTR/RTS** → Auto-reset circuit (GPIO0, EN)

## Related Documentation

- **Datasheet:** [datasheets/README.md](datasheets/README.md)

---

**Status:** 📋 Placeholder - Documentation TBD

**Last Updated:** 2025-12-01
