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
├── dfrobot-c4001/                # mmWave radar sensor
├── panasonic-ekmc1604111/        # PIR motion sensor
├── rohm-bh1750/                  # Ambient light sensor
├── espressif-esp32-wroom-32e/    # ESP32 MCU (recommended)
├── espressif-esp32-wrover-e/     # ESP32 MCU with PSRAM
├── microchip-lan8720a/           # Ethernet PHY
├── ti-tps2378/                   # PoE controller
├── ti-tps62a02a/                 # 3.3V buck converter
├── silergy-tx4138/               # 5V buck converter
├── tp-tp4054/                    # Li-Po battery charger
├── wch-ch340x/                   # USB-to-UART bridge
└── hirose-dm3at/                 # Micro SD socket (omitted)
```

## Component Inventory

### Sensors

**DFRobot C4001 (SEN0609)** - 24GHz mmWave Radar Sensor
- **Status:** Documented
- **Documentation:** [dfrobot-c4001/README.md](./dfrobot-c4001/README.md)
- **Datasheets:** [dfrobot-c4001/datasheets/README.md](./dfrobot-c4001/datasheets/README.md)
- **GPIO:** GPIO16 (RX), GPIO9 (TX) - Software UART, 115200 baud
- **Key Features:**
  - Presence detection: up to 16m, Motion: up to 25m
  - 100° × 40° beam angle, Distance & velocity measurement
  - UART interface (configurable 4800-115200 baud)
  - 3.3V/5V operation, ESPHome compatible
- **HaloSense Use:** Accurate presence detection (even stationary people)

**Panasonic EKMC1604111** - PIR Motion Sensor (Wall Type)
- **Status:** Documented
- **Documentation:** [panasonic-ekmc1604111/README.md](./panasonic-ekmc1604111/README.md)
- **Datasheets:** [panasonic-ekmc1604111/datasheets/README.md](./panasonic-ekmc1604111/datasheets/README.md)
- **GPIO:** GPI35 (input-only) with 33kΩ pull-down resistor
- **Key Features:**
  - Three-step lens: 12m/6m/3m detection zones
  - Coverage: 105° × 40° (asymmetric vertical), 68 beams
  - Response time: <0.1s (instant motion trigger)
  - Ultra-low power: 170μA standby (0.56mW @ 3.3V)
  - Digital output, through-hole mounting
- **HaloSense Use:** Fast motion detection for instant room entry trigger

**ROHM BH1750FVI** - Digital Ambient Light Sensor
- **Status:** Documented
- **Documentation:** [rohm-bh1750/README.md](./rohm-bh1750/README.md)
- **Datasheets:** [rohm-bh1750/datasheets/README.md](./rohm-bh1750/datasheets/README.md)
- **GPIO:** GPIO32 (SDA), GPIO33 (SCL) - Hardware I2C
- **Key Features:**
  - Range: 1-65,535 lx (extendable to 0.11-100,000 lx)
  - Resolution: 0.5-4 lx (configurable modes)
  - I2C interface (address 0x23 or 0x5C)
  - Power: 120μA active, 0.01μA standby (0.4mW typical)
  - ESPHome native support, JLCPCB available (C78960)
- **HaloSense Use:** Ambient light measurement for smart lighting automation

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

### Ethernet PHY
**Microchip LAN8720A** - 10/100 Mbps Ethernet PHY with RMII Interface
- **Status:** Placeholder - Documentation TBD
- **Documentation:** [microchip-lan8720a/README.md](./microchip-lan8720a/README.md)
- **Key Features:**
  - 10/100 BASE-TX Ethernet PHY, RMII interface
  - ~60 mA @ 3.3V, QFN-24 package
- **Source:** OLIMEX ESP32-POE reference design

### PoE Controller
**Texas Instruments TPS2378** - IEEE 802.3af/at PoE-PD Controller
- **Status:** Placeholder - Documentation TBD
- **Documentation:** [ti-tps2378/README.md](./ti-tps2378/README.md)
- **Key Features:**
  - IEEE 802.3af/at compliant, up to 25.5W (Class 4)
  - HSOIC-8 PowerPAD package
- **Source:** OLIMEX ESP32-POE reference design

### Power Management ICs
**TI TPS62A02A** - 3.3V Buck Converter for LAN PHY
- **Status:** Placeholder - Documentation TBD
- **Documentation:** [ti-tps62a02a/README.md](./ti-tps62a02a/README.md)

**Silergy TX4138** - 5V Buck Converter from PoE
- **Status:** Placeholder - Documentation TBD
- **Documentation:** [silergy-tx4138/README.md](./silergy-tx4138/README.md)

**TP4054** - Li-Po Battery Charger IC
- **Status:** Placeholder - Documentation TBD
- **Documentation:** [tp-tp4054/README.md](./tp-tp4054/README.md)

### USB-to-UART Bridge
**WCH CH340X** - USB Programming Interface
- **Status:** Placeholder - Documentation TBD
- **Documentation:** [wch-ch340x/README.md](./wch-ch340x/README.md)

### Micro SD Card Socket
**Hirose Electric DM3AT** - Micro SD Socket (OMITTED)
- **Status:** Documented (omitted from HaloSense design)
- **Documentation:** [hirose-dm3at/README.md](./hirose-dm3at/README.md)
- **Reason:** Boot strapping pin conflicts
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

**HaloSense GPIO Allocation (ESP32-WROOM-32E):**

| Component | Interface | GPIO Pins | Notes |
|-----------|-----------|-----------|-------|
| **Ethernet (LAN8720A)** | RMII | GPIO0, 17, 18, 19, 21, 22, 23, 25, 26, 27 | Primary connectivity |
| **mmWave (DFRobot C4001)** | Software UART | GPIO16 (RX), GPIO9 (TX) | 115200 baud |
| **PIR (Panasonic EKMC1604111)** | Digital Input | GPI35 | Input-only, 33kΩ pull-down |
| **Light (ROHM BH1750FVI)** | Hardware I2C | GPIO32 (SDA), GPIO33 (SCL) | No conflicts |
| **Micro SD Socket** | — | Omitted | Avoided boot strapping conflicts |

**Module Comparison:**

| Module | GPIO Availability | HaloSense Compatibility |
|--------|-------------------|------------------------|
| ESP32-WROOM-32E | All 38 GPIOs available | ✅ **Recommended** - All sensors compatible |
| ESP32-WROVER-E | GPIO16/17 **NOT available** | ⚠️ Not recommended - Ethernet clock conflict |

**Resolved Conflicts:**
- ✅ **I2C vs Ethernet:** Using GPIO32/GPIO33 instead of default GPIO21/GPIO22
- ✅ **UART vs Ethernet Clock:** Using software UART on GPIO16/GPIO9 instead of GPIO16/GPIO17
- ✅ **SD Card Boot Strapping:** Omitted to avoid GPIO2, GPIO12, GPIO15 conflicts

See sensor-specific documentation: [../../sensors/README.md](../../sensors/README.md)

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
