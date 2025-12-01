# HaloSense Hardware Design

This directory contains the KiCad PCB design files for the HaloSense presence sensor.

## 🚧 Work in Progress

Hardware design is currently in development. Check back for updates!

## Planned Components

### Custom PCB Design

The HaloSense mainboard is a custom circular PCB design using the OLIMEX ESP32-POE board KiCad files as a reference/base design.

**Key Features:**
- Circular form factor
- ESP32 microcontroller with PoE support
- Integrated sensor connectors
- USB-C + Ethernet rear panel
- Power management (PoE/USB-C detection)

## Directory Structure

```
hardware/
├── schematics/     # KiCad schematic files (.kicad_sch)
├── pcb/            # KiCad PCB layout files (.kicad_pcb)
├── gerbers/        # Manufacturing files (Gerber + drill)
├── reference/      # Reference designs (git submodules)
│   └── esp32-poe/  # OLIMEX ESP32-POE reference design
└── HARDWARE_DESIGN.md  # This file
```

## Reference Design

The HaloSense design uses the **OLIMEX ESP32-POE** board as a reference design, available as a git submodule:

**Location:** `hardware/reference/esp32-poe/`

**Repository:** https://github.com/OLIMEX/ESP32-POE.git

**Latest Revision:** M1 (KiCad 6+ format)
- Schematic: `HARDWARE/ESP32-PoE-hardware-revision-M1/ESP32-PoE_Rev_M1.kicad_sch`
- PCB Layout: `HARDWARE/ESP32-PoE-hardware-revision-M1/ESP32-PoE_Rev_M1.kicad_pcb`
- Gerbers: `HARDWARE/ESP32-PoE-hardware-revision-M1/Gerbers/`

**Usage:**
- Reference for ESP32 + Ethernet + PoE circuitry
- Component selection guidance
- PCB layout best practices
- NOT used as a component - we create a custom variant

## Design Requirements

### Power System
- **PoE (IEEE 802.3af):** 15.4W available, ~5W typical consumption
- **USB-C:** 5V/2A minimum
- **Hybrid Mode:** Ethernet data + USB-C power

### Interfaces
- **Ethernet:** 10/100 Mbps (LAN8720A or similar PHY)
- **WiFi:** 802.11 b/g/n (2.4GHz, ESP32 built-in)
- **UART:** For mmWave sensor (DFRobot C4001)
- **I2C:** For PIR and light sensors (shared bus)
- **GPIO:** Additional pins for future expansion

### Physical Specifications
- **Form Factor:** Circular PCB
- **Target Diameter:** TBD (optimize for component placement)
- **Mounting:** Standard hole pattern for enclosure attachment
- **Connectors:** Rear panel with RJ45 + USB-C

## Reference Design

The design is based on the OLIMEX ESP32-POE board:
- **Repository:** https://github.com/OLIMEX/ESP32-POE
- **License:** CERN Open Hardware License

We use this as a proven reference architecture for ESP32 + Ethernet + PoE functionality, adapted to our circular form factor and custom requirements.

## Development Tools

### Required Software
- [KiCad 8.0+](https://www.kicad.org/) - PCB design software
- Git for version control

### KiCad Libraries
- Standard KiCad libraries
- OLIMEX ESP32-POE symbols/footprints (as reference)
- Custom component libraries (TBD)

## Design Guidelines

When contributing to hardware design:

1. **Follow KiCad best practices**
   - Use consistent grid settings (5mil for PCB routing)
   - Meaningful net names
   - Proper reference designators

2. **Power integrity**
   - Adequate decoupling capacitors
   - Proper ground planes
   - Separate analog/digital grounds where appropriate

3. **Signal integrity**
   - Impedance-controlled traces for high-speed signals
   - Minimize trace lengths for sensitive signals
   - Proper termination where required

4. **Manufacturability**
   - Standard PCB stackup (2-layer or 4-layer)
   - Minimum trace/space per manufacturer capabilities
   - Proper clearances for high voltage (PoE)

5. **Testing**
   - Test points for critical signals
   - Debug header for ESP32 programming
   - LED indicators for power and status

## Current Status

- [ ] Schematic design
  - [ ] Power supply (PoE + USB-C)
  - [ ] ESP32 core circuit
  - [ ] Ethernet PHY
  - [ ] Sensor interfaces
  - [ ] USB-C power delivery
- [ ] PCB layout
  - [ ] Component placement
  - [ ] Power routing
  - [ ] Signal routing
  - [ ] Ground planes
- [ ] Design verification
  - [ ] Design Rule Check (DRC)
  - [ ] Electrical Rule Check (ERC)
  - [ ] Simulation (if applicable)
- [ ] Manufacturing files
  - [ ] Gerber generation
  - [ ] Bill of Materials (BOM)
  - [ ] Assembly drawings

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines on contributing to hardware design.

**Key points:**
- Include updated schematics and PCB files
- Document design decisions
- Verify DRC/ERC passes
- Prototype and test if possible

## License

Hardware design files are licensed under CC BY-NC-SA 4.0. See [LICENSE.md](../LICENSE.md) for details.

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense
