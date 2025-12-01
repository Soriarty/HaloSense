# Microchip LAN8720A Ethernet PHY

## Component Overview

**Manufacturer:** Microchip Technology Inc.
**Part Number:** LAN8720A-CP (LAN8720Ai-CP for industrial)
**Type:** 10/100 Mbps Ethernet PHY (RMII Interface)
**Package:** QFN-24 (4mm × 4mm)

## Purpose in HaloSense

Primary Ethernet connectivity via RMII interface to ESP32:
- 10/100 BASE-TX Ethernet PHY
- RMII interface (reduced pin count vs MII)
- Integrated MAC layer interfacing
- Supports PoE power delivery via magnetics

## Key Specifications

| Parameter | Specification |
|-----------|--------------|
| **Interface** | RMII (Reduced MII) |
| **Speed** | 10/100 Mbps auto-negotiation |
| **Supply Voltage** | 3.3V (I/O), 1.2V (core, internal LDO) |
| **Current** | ~60 mA @ 3.3V (typical) |
| **Package** | QFN-24 (4mm × 4mm) |
| **Temperature** | -40°C to +85°C (CP), -40°C to +105°C (industrial) |

## RMII Pin Connection to ESP32

- **GPIO0** - EMAC_TX_CLK (50MHz ref clock from PHY)
- **GPIO17** - EMAC_CLK_OUT_180 (50MHz output to PHY)
- **GPIO18** - MDIO (management data I/O)
- **GPIO19** - EMAC_TXD0
- **GPIO21** - EMAC_TX_EN
- **GPIO22** - EMAC_TXD1
- **GPIO23** - MDC (management clock)
- **GPIO25** - EMAC_RXD0
- **GPIO26** - EMAC_RXD1
- **GPIO27** - EMAC_RX_CRS_DV

## Related Documentation

- **Datasheet:** [datasheets/README.md](datasheets/README.md)
- **OLIMEX Reference:** `hardware/reference/esp32-poe/`

---

**Status:** 📋 Placeholder - Documentation TBD

**Last Updated:** 2025-12-01
