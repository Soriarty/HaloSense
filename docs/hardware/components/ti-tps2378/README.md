# Texas Instruments TPS2378 PoE Controller

## Component Overview

**Manufacturer:** Texas Instruments
**Part Number:** TPS2378DDAR
**Type:** IEEE 802.3af/at PoE-PD Interface and PWM Controller
**Package:** HSOIC-8 (PowerPAD)

## Purpose in HaloSense

PoE power extraction and management:
- IEEE 802.3af (PoE) / 802.3at (PoE+) compliant
- Provides regulated DC output from Ethernet cable
- Class 0 (default 0.44-12.95W) or Class 4 (12.95-25.5W) selectable
- Drives external MOSFET for power switching

## Key Specifications

| Parameter | Specification |
|-----------|--------------|
| **Input Voltage** | 36V to 57V (from PoE PSE) |
| **Output Power** | Up to 25.5W (Class 4, 802.3at) |
| **Efficiency** | ~90% typical |
| **Package** | HSOIC-8 (PowerPAD) |
| **Temperature** | -40°C to +85°C |

## HaloSense Configuration

- **Class Selection:** Jumper selectable (Class 0 default / Class 4)
- **Output:** ~48V DC (feeds TX4138 buck converter)
- **Control:** GPIO12 (PHY_PWR) for enable/disable

## Related Documentation

- **Datasheet:** [datasheets/README.md](datasheets/README.md)
- **OLIMEX Reference:** `hardware/reference/esp32-poe/`

---

**Status:** 📋 Placeholder - Documentation TBD

**Last Updated:** 2025-12-01
