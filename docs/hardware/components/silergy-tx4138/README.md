# Silergy TX4138 Buck Converter

## Component Overview

**Manufacturer:** Silergy Corp.
**Part Number:** TX4138
**Type:** Wide Input Range Step-Down (Buck) Converter
**Package:** ESOIC-8

## Purpose in HaloSense

5V power supply from PoE input:
- Converts 48V PoE to 5V system rail
- Wide input range (4.5V to 60V)
- Up to 4A continuous output current
- Drives USB, battery charger, and 3.3V regulators

## Key Specifications

| Parameter | Specification |
|-----------|--------------|
| **Input Voltage** | 4.5V to 60V |
| **Output Voltage** | 0.8V to 40V (adjustable) |
| **Output Current** | Up to 4A continuous |
| **Switching Freq** | Variable (typically ~400kHz) |
| **Efficiency** | ~90% @ 5V output from 48V input |
| **Standby Current** | 400μA |
| **Package** | ESOIC-8 |

## HaloSense Configuration

- **Vin:** 48V from TPS2378 PoE controller
- **Vout:** 5V (system rail)
- **L:** 33μH inductor
- **Feedback:** Resistor divider for 5V output

## Related Documentation

- **Datasheet:** [datasheets/README.md](datasheets/README.md)

---

**Status:** 📋 Placeholder - Documentation TBD

**Last Updated:** 2025-12-01
