# TP4054 Li-Po Battery Charger IC

## Component Overview

**Manufacturer:** TECH PUBLIC (or compatible: BL4054B-42)
**Part Number:** TP4054-42-SOT25-R
**Type:** Single Cell Li-Ion/Li-Po Battery Charger
**Package:** SOT-23-5

## Purpose in HaloSense

Optional battery backup charging (if battery connected):
- Charges single Li-Po/Li-Ion cell to 4.2V
- Constant current / constant voltage (CC/CV) charging
- Programmable charge current up to 800mA
- Charge status indication (CHRG pin)

## Key Specifications

| Parameter | Specification |
|-----------|--------------|
| **Input Voltage** | 4.5V to 6.5V (VCC) |
| **Battery Voltage** | 4.2V final float voltage |
| **Charge Current** | Up to 800mA (programmable via R_PROG) |
| **Package** | SOT-23-5 |
| **Efficiency** | ~85% typical |

## HaloSense Configuration

- **R_PROG:** 2kΩ to 10kΩ (sets charge current)
- **Input:** +5V_USB or external 5V supply
- **Battery:** Optional Li-Po cell (not included by default)

## Related Documentation

- **Datasheet:** [datasheets/README.md](datasheets/README.md)
- **Compatible:** BL4054B-42TPRN

---

**Status:** 📋 Placeholder - Documentation TBD

**Last Updated:** 2025-12-01
