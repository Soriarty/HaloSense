# HaloSense Sensor Documentation

This directory contains detailed technical documentation for all sensors used in the HaloSense presence detection system.

## Directory Structure

Each sensor has its own subdirectory containing:
- **<SENSOR>_TECHNICAL_GUIDE.md** - Main technical documentation
- **datasheets/** - Official PDF datasheets and manufacturer documentation
  - **DATASHEETS_INDEX.md** - Index of available datasheets

```
docs/sensors/
├── SENSORS_INDEX.md (this file)
├── dfrobot-c4001/          # mmWave radar sensor
│   ├── C4001_TECHNICAL_GUIDE.md
│   └── datasheets/
│       ├── DATASHEETS_INDEX.md
│       └── *.pdf (official datasheets)
├── pir-sensor/             # PIR motion sensor (future)
│   ├── PIR_TECHNICAL_GUIDE.md
│   └── datasheets/
└── light-sensor/           # Ambient light sensor (future)
    ├── LIGHT_TECHNICAL_GUIDE.md
    └── datasheets/
```

## Sensor Inventory

### mmWave Radar Sensor
**DFRobot C4001 (SEN0609)** - 24GHz FMCW Radar
- **Status:** Selected
- **Documentation:** [C4001_TECHNICAL_GUIDE.md](./dfrobot-c4001/C4001_TECHNICAL_GUIDE.md)
- **Datasheets:** [DATASHEETS_INDEX.md](./dfrobot-c4001/datasheets/DATASHEETS_INDEX.md)
- **Key Features:**
  - Presence detection: up to 16m
  - Motion detection: up to 25m
  - Distance and velocity measurement
  - 100° × 40° beam angle
  - UART interface (9600 baud)
  - 3.3V/5V operation
  - ESPHome compatible

### PIR Motion Sensor
**Status:** To Be Determined
- **Requirements:**
  - I2C or UART interface preferred
  - 3.3V logic level
  - Low power consumption
  - ESPHome library support

### Ambient Light Sensor
**Status:** To Be Determined
- **Requirements:**
  - I2C interface preferred
  - Lux measurement capability
  - 3.3V logic level
  - Low power consumption
  - ESPHome library support

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
| DFRobot C4001 | UART | TX, RX (+ optional OUT) | Requires 1 hardware UART port |
| PIR Sensor | TBD | TBD | Plan after component selection |
| Light Sensor | TBD | TBD | Preferably I2C (shared bus) |

**ESP32 Available Interfaces:**
- UART0: Used for programming/debug console
- UART1: Available (consider for C4001)
- UART2: Available
- I2C: Multiple devices can share SDA/SCL pins

## Power Budget Considerations

Target total power consumption: ~5W (PoE budget)

| Component | Voltage | Current (typical) | Status |
|-----------|---------|-------------------|--------|
| ESP32-POE | 3.3V | ~200-500mA | Base platform |
| DFRobot C4001 | 3.3V/5V | TBD | Measure during prototyping |
| PIR Sensor | TBD | TBD | Pending selection |
| Light Sensor | TBD | TBD | Pending selection |

## Integration Checklist

When adding a new sensor:
- [ ] Create sensor subdirectory (e.g., `sensor-name/`)
- [ ] Create `SENSOR_NAME_TECHNICAL_GUIDE.md` with detailed technical documentation
- [ ] Create `datasheets/` subdirectory for PDF files
- [ ] Create `datasheets/DATASHEETS_INDEX.md` to catalog PDFs
- [ ] Download and organize official datasheets
- [ ] Verify voltage level compatibility (3.3V/5V)
- [ ] Confirm interface type and GPIO requirements
- [ ] Check ESPHome library availability
- [ ] Measure power consumption
- [ ] Update GPIO allocation table in SENSORS_INDEX.md
- [ ] Update power budget calculations in SENSORS_INDEX.md
- [ ] Add wiring examples for ESP32
- [ ] Test basic functionality before integration

## References

- [HaloSense Project README](../../README.md)
- [CLAUDE.md - Project Instructions](../../.claude/CLAUDE.md)
- Official manufacturer datasheets (linked in individual sensor docs)

---

**Last Updated:** 2025-11-28
