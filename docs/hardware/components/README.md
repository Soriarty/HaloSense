# HaloSense Hardware Component Documentation

This directory contains detailed technical documentation for all hardware components used in the HaloSense custom PCB design.

## Directory Structure

Each component has its own subdirectory containing:
- **README.md** - Main technical documentation
- **datasheets/** - Official PDF datasheets and manufacturer documentation
  - **README.md** - Index of available datasheets

```
docs/hardware/components/
├── README.md (this file)
├── espressif-esp32-wroom-32e/    # ESP32 MCU module (recommended)
│   ├── README.md
│   └── datasheets/
│       ├── README.md
│       └── *.pdf (official datasheets)
├── espressif-esp32-wrover-e/     # ESP32 MCU module with PSRAM
│   ├── README.md
│   └── datasheets/
│       ├── README.md
│       └── *.pdf (official datasheets)
└── hirose-dm3at/                 # Micro SD card socket
    ├── README.md
    └── datasheets/
        ├── README.md
        └── *.pdf (official datasheets)
```

## Component Inventory

### ESP32 Microcontroller Module
**Espressif ESP32-WROOM-32E** - Wi-Fi + Bluetooth MCU Module (Recommended)
- **Status:** Documented, **recommended for HaloSense**
- **Documentation:** [espressif-esp32-wroom-32e/README.md](./espressif-esp32-wroom-32e/README.md)
- **Datasheets:** [espressif-esp32-wroom-32e/datasheets/README.md](./espressif-esp32-wroom-32e/datasheets/README.md)
- **Key Features:**
  - Dual-core Xtensa LX6 @ 240 MHz
  - 520 KB SRAM, 4/8/16 MB Flash
  - Wi-Fi 802.11 b/g/n + Bluetooth 4.2 BR/EDR/BLE
  - **All GPIOs available** including GPIO16/GPIO17
  - Compatible with Ethernet RMII (LAN8720A PHY)
  - 38 GPIO pins + peripherals (UART, I2C, SPI, ADC, DAC)
  - Operating: -40°C to +85°C
- **Source:** OLIMEX ESP32-POE reference design
- **HaloSense Use:** Primary MCU for sensor fusion, network connectivity, automation logic

### ESP32 Microcontroller Module (with PSRAM)
**Espressif ESP32-WROVER-E** - Wi-Fi + Bluetooth MCU Module with 8MB PSRAM
- **Status:** Documented, **NOT recommended for HaloSense** (GPIO limitations)
- **Documentation:** [espressif-esp32-wrover-e/README.md](./espressif-esp32-wrover-e/README.md)
- **Datasheets:** [espressif-esp32-wrover-e/datasheets/README.md](./espressif-esp32-wrover-e/datasheets/README.md)
- **Key Features:**
  - Same as WROOM-32E + **8MB PSRAM**
  - **⚠️ GPIO16 and GPIO17 NOT available** (used internally for PSRAM)
  - **⚠️ NOT compatible with OLIMEX Ethernet design** (requires GPIO17 for clock)
  - Higher power consumption (+20mA when using PSRAM)
  - Slightly larger: 18 × 31.4 mm (vs 18 × 25.5 mm)
- **Source:** OLIMEX ESP32-POE reference design (alternative variant)
- **HaloSense Impact:** **Use WROOM-32E instead** - Ethernet support requires GPIO17

### Micro SD Card Socket
**Hirose Electric DM3 Series** - DM3AT-SF-PEJM5 (TFC-9P-1.7H)
- **Status:** Documented (implementation decision pending Phase 2)
- **Documentation:** [hirose-dm3at/README.md](./hirose-dm3at/README.md)
- **Datasheets:** [hirose-dm3at/datasheets/README.md](./hirose-dm3at/datasheets/README.md)
- **Key Features:**
  - Push-Push mechanism with ejection
  - Height: 1.7mm (low profile)
  - ESP32 SDMMC HS2 interface (GPIO15/14/2 for CMD/CLK/DATA0)
  - 10,000 insertion cycles rated
  - Optional local data logging capability
  - **Critical:** Boot strapping pin conflicts (GPIO2, GPIO12, GPIO15)
- **Source:** OLIMEX ESP32-POE reference design

## Documentation Structure

Each component documentation includes:
- **Technical specifications** - Complete electrical and performance characteristics
- **Pin configuration** - Pinout diagrams and ESP32 connections
- **PCB design guidelines** - Mounting patterns, keepout zones, critical warnings
- **Assembly notes** - Reflow profiles, soldering guidelines, precautions
- **Integration notes** - HaloSense-specific considerations

## Design Considerations

### GPIO Planning

Components documented here may have specific GPIO requirements or conflicts that must be resolved during Phase 2 hardware design:

| Component | Interface | GPIO Pins | Notes |
|-----------|-----------|-----------|-------|
| ESP32-WROOM-32E | MCU | All 38 GPIOs available | **Recommended:** All GPIOs functional |
| ESP32-WROVER-E | MCU | GPIO16/17 **NOT available** | **⚠️ PSRAM uses GPIO16/17 internally** |
| Micro SD Socket | SDMMC HS2 | GPIO15 (CMD), GPIO14 (CLK), GPIO2 (DATA0) | **Boot strapping conflicts:** GPIO2, GPIO12, GPIO15 |

**Critical GPIO Conflicts:**
- **GPIO15 (HS2_CMD):** Must be HIGH at boot (boot strapping pin)
- **GPIO2 (HS2_DATA0):** Must be LOW/floating at boot (boot strapping pin)
- **GPIO12 (HS2_DATA2):** Flash voltage select (boot strapping pin)

See complete GPIO allocation table: [../../sensors/README.md](../../sensors/README.md)

### Power Budget Impact

Component power consumption contributes to the overall PoE power budget:

| Component | Voltage | Current (typical) | Power | Status |
|-----------|---------|-------------------|-------|--------|
| ESP32-WROOM-32E (Ethernet mode) | 3.3V | ~100 mA | ~330 mW | **Primary MCU** |
| ESP32-WROOM-32E (Wi-Fi TX) | 3.3V | ~160 mA | ~528 mW | Fallback mode |
| ESP32-WROVER-E (Ethernet + PSRAM) | 3.3V | ~120 mA | ~396 mW | If PSRAM used |
| Micro SD Socket (idle) | 3.3V | <1μA | <3.3μW | Negligible |
| Micro SD Socket (active read) | 3.3V | ~50mA | ~165mW | Temporary peaks only |
| Micro SD Socket (active write) | 3.3V | ~80mA | ~264mW | Temporary peaks only |

See complete power budget analysis: [../power-budget.md](../power-budget.md)

## Integration Checklist

When adding a new hardware component:
- [ ] Create component subdirectory (e.g., `component-name/`)
- [ ] Create `README.md` with detailed technical documentation
- [ ] Create `datasheets/` subdirectory for PDF files
- [ ] Create `datasheets/README.md` to catalog PDFs
- [ ] Download and organize official datasheets
- [ ] Verify voltage level compatibility (3.3V/5V)
- [ ] Document GPIO requirements and conflicts
- [ ] Check for boot strapping pin conflicts
- [ ] Measure/estimate power consumption
- [ ] Update GPIO allocation table in this README
- [ ] Update power budget calculations in this README
- [ ] Add PCB design guidelines and critical warnings
- [ ] Document assembly requirements (reflow profiles, etc.)

## OLIMEX ESP32-POE Reference Components

Components documented here are derived from the OLIMEX ESP32-POE reference design:
- **Repository:** `hardware/reference/esp32-poe/` (git submodule)
- **Source:** https://github.com/OLIMEX/ESP32-POE
- **Revision:** M1 (KiCad 7+ format)

HaloSense uses these as proven reference designs but adapts them for:
- Custom circular form factor
- Optimized component selection
- HaloSense-specific requirements

## References

- [HaloSense Project README](../../../README.md)
- [Hardware Design Documentation](../README.md)
- [Sensor Documentation](../../sensors/README.md)
- [OLIMEX ESP32-POE Reference](../../hardware/reference/esp32-poe/)

---

## Navigation

← **[Hardware](../README.md)** | **[Sensors](../../sensors/README.md)** | **[Main Documentation](../../../README.md)**

---

**Last Updated:** 2025-12-01
