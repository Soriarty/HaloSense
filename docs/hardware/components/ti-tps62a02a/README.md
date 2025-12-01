# Texas Instruments TPS62A02A Buck Converter

## Component Overview

**Manufacturer:** Texas Instruments
**Part Number:** TPS62A02ADRLR
**Type:** 2A Step-Down (Buck) Converter
**Package:** SOT-563-6

## Purpose in HaloSense

3.3V power supply for LAN8720A Ethernet PHY:
- Converts 5V to 3.3V (LAN power rail)
- 2.4MHz switching frequency (low ripple)
- Up to 2A output current
- Ultra-low quiescent current (23μA)

## Key Specifications

| Parameter | Specification |
|-----------|--------------|
| **Input Voltage** | 2.5V to 5.5V |
| **Output Voltage** | 0.6V to 5.5V (configured via resistors) |
| **Output Current** | Up to 2.0A |
| **Switching Freq** | 2.4MHz |
| **Efficiency** | ~90% @ 3.3V output |
| **Quiescent Current** | 23μA (light load) |
| **Package** | SOT-563-6 |

## HaloSense Configuration

- **Vin:** +5VP (from PoE or USB)
- **Vout:** 3.3V (LAN8720A supply)
- **L:** 1.0μH inductor
- **Cout:** 22μF capacitor

## Related Documentation

- **Datasheet:** [datasheets/README.md](datasheets/README.md)

---

**Status:** 📋 Placeholder - Documentation TBD

**Last Updated:** 2025-12-01
