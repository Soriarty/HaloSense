# Hardware Design Documentation

This directory contains hardware design specifications and analysis for the HaloSense presence sensor.

## 📄 Documents

### Hardware Components

**[Components Overview & GPIO Planning](components/README.md)** - Complete component documentation

**MCU & Wireless:**
- **[ESP32-WROOM-32E](components/espressif-esp32-wroom-32e/README.md)** - Main MCU (recommended)
  - All 38 GPIOs available, Wi-Fi + Bluetooth, Ethernet RMII compatible
- **[ESP32-WROVER-E](components/espressif-esp32-wrover-e/README.md)** - MCU with PSRAM (not recommended)
  - GPIO16/17 unavailable (PSRAM internal use), Ethernet clock conflict

**Networking:**
- **[Microchip LAN8720A](components/microchip-lan8720a/README.md)** - Ethernet PHY
  - 10/100 Mbps RMII interface, ~60 mA @ 3.3V
- **[TI TPS2378](components/ti-tps2378/README.md)** - PoE Controller
  - IEEE 802.3af/at, Class 0/4 selectable, up to 25.5W
- **[WCH CH340X](components/wch-ch340x/README.md)** - USB-to-UART Bridge
  - ESP32 programming interface, auto-reset support

**Power Management:**
- **[Silergy TX4138](components/silergy-tx4138/README.md)** - 5V Buck Converter
  - 48V PoE → 5V, 4.5-60V input, up to 4A output
- **[TI TPS62A02A](components/ti-tps62a02a/README.md)** - 3.3V Buck Converter
  - 5V → 3.3V for LAN PHY, 2.4MHz switching, 2A output
- **[TP4054](components/tp-tp4054/README.md)** - Li-Po Battery Charger
  - Single cell Li-Po/Li-Ion, 4.2V float, optional backup

**Connectors:**
- **[Hirose DM3AT](components/hirose-dm3at/README.md)** - Micro SD Socket (omitted)
  - Boot strapping conflicts, not included in HaloSense design

### Power and Electrical

- **[power-budget.md](power-budget.md)** - Complete power consumption analysis
  - Component-by-component breakdown
  - PoE budget verification (1.3W typical / 15.4W available)
  - USB-C power scenarios
  - MSL rating vs power trade-off analysis
  - Optimization opportunities

### Environmental Protection

- **[ip-rating.md](ip-rating.md)** - IP54 enclosure design guide
  - IP rating system explained (IEC 60529)
  - IP54 target specification (dust protected + splash water)
  - Enclosure design requirements and checklist
  - MSL rating correlation for component selection
  - DIY testing procedures

## 🔗 Related Documentation

- **[Sensor Documentation](../sensors/README.md)** - All sensors technical specs
- **[Development Workflows](../development/README.md)** - Developer guides and workflows
- **[Project Documentation](../../README.md)** - Main project README

## 📋 Planned Documents

- **hardware-design.md** - PCB schematic and layout design (KiCad)
- **bom.md** - Bill of Materials with JLCPCB part numbers
- **assembly.md** - PCB assembly guide and soldering notes

---

**Last Updated:** 2025-12-01
