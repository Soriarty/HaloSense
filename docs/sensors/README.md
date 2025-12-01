# HaloSense Sensor Documentation

This directory contains detailed technical documentation for all sensors used in the HaloSense presence detection system.

## Directory Structure

Each sensor has its own subdirectory containing:
- **<SENSOR>_TECHNICAL_GUIDE.md** - Main technical documentation
- **datasheets/** - Official PDF datasheets and manufacturer documentation
  - **DATASHEETS_INDEX.md** - Index of available datasheets

```
docs/sensors/
├── README.md (this file)
├── dfrobot-c4001/          # mmWave radar sensor
│   ├── README.md
│   └── datasheets/
│       ├── DATASHEETS_INDEX.md
│       └── *.pdf (official datasheets)
├── panasonic-ekmc1604111/  # PIR motion sensor
│   ├── EKMC1604111_TECHNICAL_GUIDE.md
│   └── datasheets/
│       ├── DATASHEETS_INDEX.md
│       └── *.pdf (official datasheets)
└── rohm-bh1750/            # Ambient light sensor
    ├── BH1750_TECHNICAL_GUIDE.md
    └── datasheets/
        ├── DATASHEETS_INDEX.md
        └── *.pdf (official datasheets)
```

## Sensor Inventory

### mmWave Radar Sensor
**DFRobot C4001 (SEN0609)** - 24GHz FMCW Radar
- **Status:** Selected
- **Documentation:** [README.md](./dfrobot-c4001/README.md)
- **Datasheets:** [README.md](./dfrobot-c4001/datasheets/README.md)
- **Key Features:**
  - Presence detection: up to 16m
  - Motion detection: up to 25m
  - Distance and velocity measurement
  - 100° × 40° beam angle
  - UART interface (115200 baud default, configurable 4800-115200)
  - 3.3V/5V operation
  - ESPHome compatible

### PIR Motion Sensor
**Panasonic EKMC1604111** - Wall Installation Type PaPIRs Sensor
- **Status:** Selected
- **Documentation:** [README.md](./panasonic-ekmc1604111/README.md)
- **Datasheets:** [README.md](./panasonic-ekmc1604111/datasheets/README.md)
- **Key Features:**
  - Three-step lens: 12m / 6m / 3m detection zones
  - Wide horizontal coverage: 105° (112° max)
  - Wall-optimized vertical coverage: 40° (asymmetric +6.6° / -49°)
  - Response time: <0.1s (instant motion trigger)
  - Digital output interface (simple GPIO)
  - Ultra-low power: 170μA standby
  - 3.0V-6.0V operation (3.3V/5V compatible)
  - 68 detection zones
  - Mainboard-integrated (through-hole mounting)

### Ambient Light Sensor
**ROHM BH1750FVI** - Digital 16-bit I2C Ambient Light Sensor
- **Status:** Selected
- **Documentation:** [README.md](./rohm-bh1750/README.md)
- **Datasheets:** [README.md](./rohm-bh1750/datasheets/README.md)
- **Key Features:**
  - Measurement range: 1-65,535 lx
  - Resolution: 1 lx (H-Resolution mode)
  - I2C interface (0x23 or 0x5C address)
  - Supply voltage: 2.4-3.6V (3.3V operation)
  - Current consumption: 120μA @ 100lx (0.4mW typical)
  - Power-down mode: 0.01μA
  - Spectral response close to human eye
  - MSL 3 rating (better moisture handling)
  - ESPHome native support
  - JLCPCB available (C78960, Extended Parts)

## Documentation Structure

Each sensor documentation includes:
- **Technical specifications** - Complete electrical and performance characteristics
- **Pin configuration** - Pinout diagrams and connections
- **Wiring examples** - Sample connections for ESP32 and other platforms
- **Operating modes** - Different modes of operation and use cases
- **Command structure** - Serial/I2C command protocols
- **Library support** - ESPHome integration and Arduino libraries
- **Integration notes** - HaloSense-specific considerations

## GPIO Allocation Planning

| Sensor | Interface | GPIO Pins | Notes |
|--------|-----------|-----------|-------|
| DFRobot C4001 | UART | TX, RX (+ optional OUT) | Requires 1 hardware UART port (UART1 or UART2) |
| Panasonic EKMC1604111 | Digital GPIO | 1 GPIO input | **External pull-down required:** 33kΩ (±5%, 0805 SMD) to GND |
| ROHM BH1750FVI | I2C | SDA, SCL | Address: 0x23 (ADDR='L') or 0x5C (ADDR='H'), shared I2C bus |

**ESP32 Available Interfaces:**
- **UART0:** Used for programming/debug console (reserved)
- **UART1:** Available (recommended for C4001 mmWave)
- **UART2:** Available (backup)
- **GPIO:** Multiple available for digital inputs (PIR uses 1 GPIO)
- **I2C:** Multiple devices can share SDA/SCL pins (recommended for light sensor)

## Power Budget Considerations

Target total power consumption: ~5W (PoE budget available: 15.4W)

| Component | Voltage | Current (typical) | Power | Status |
|-----------|---------|-------------------|-------|--------|
| ESP32-WROOM-32E | 3.3V | 100mA | 330mW | Base platform (Ethernet mode) |
| LAN8720A PHY | 3.3V | 60mA | 198mW | Ethernet interface |
| DFRobot C4001 | 3.3V | 75mA (est.) | 248mW | Measure during prototyping |
| Panasonic EKMC1604111 | 3.3V | 0.17mA | 0.56mW | ✓ Selected, negligible power |
| ROHM BH1750FVI | 3.3V | 0.12mA | 0.40mW | ✓ Selected, negligible power |
| Supporting components | 3.3V | — | ~50mW | Status LED, resistors, regulators |
| **Total (3.3V rail)** | **3.3V** | **~235mA** | **~827mW** | PoE module regulation |
| **Total System (incl. PoE losses)** | - | - | **~1.3W** | **Excellent margin (10× headroom)** |

**Design Margin:** 1.3W typical / 15.4W available = **8.5% PoE capacity utilized**
**Worst-case scenario:** 1.8W (WiFi fallback active, all components at max current)

**See detailed power budget analysis:** [`power-budget.md`](../hardware/power-budget.md)

## Integration Checklist

When adding a new sensor:
- [ ] Create sensor subdirectory (e.g., `sensor-name/`)
- [ ] Create `README.md` with detailed technical documentation
- [ ] Create `datasheets/` subdirectory for PDF files
- [ ] Create `datasheets/README.md` to catalog PDFs
- [ ] Download and organize official datasheets
- [ ] Verify voltage level compatibility (3.3V/5V)
- [ ] Confirm interface type and GPIO requirements
- [ ] Check ESPHome library availability
- [ ] Measure power consumption
- [ ] Update GPIO allocation table in sensors/README.md
- [ ] Update power budget calculations in sensors/README.md
- [ ] Add wiring examples for ESP32
- [ ] Test basic functionality before integration

## References

- [HaloSense Project README](../../README.md)
- [CLAUDE.md - Project Instructions](../../.claude/CLAUDE.md)
- Official manufacturer datasheets (linked in individual sensor docs)

---

## Navigation

← **[Main Documentation](../../README.md)** | **[Hardware](../hardware/README.md)** | **[Development](../development/README.md)**

---

**Last Updated:** 2025-11-29
