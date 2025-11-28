# HaloSense Bill of Materials (BOM)

Complete list of components needed to build a HaloSense presence sensor.

## 🚧 Work in Progress

BOM is currently under development. Component list will be finalized after hardware design completion.

## Overview

This document lists all components, quantities, and recommended suppliers for building HaloSense.

## Component Categories

### Electronics
- Custom PCB
- Microcontroller and supporting components
- Sensors
- Connectors
- Passive components

### Mechanical
- Enclosure components
- Mounting hardware
- Cable management

### Accessories
- Cables
- Power supplies (if not using PoE)

---

## Main Components

### Microcontroller & Connectivity

| Component | Description | Quantity | Approximate Cost | Supplier Links |
|-----------|-------------|----------|------------------|----------------|
| ESP32-WROOM-32 | ESP32 module with WiFi | 1 | $3-5 | [Mouser](https://mouser.com), [DigiKey](https://digikey.com) |
| LAN8720A | Ethernet PHY | 1 | $1-2 | [LCSC](https://lcsc.com), DigiKey |
| RJ45 Connector | Ethernet port with magnetics | 1 | $1-2 | AliExpress, Mouser |
| USB-C Connector | Power + optional data | 1 | $0.50-1 | LCSC, AliExpress |

### Sensors

| Component | Description | Quantity | Approximate Cost | Supplier Links |
|-----------|-------------|----------|------------------|----------------|
| DFRobot C4001 (SEN0609) | 24GHz mmWave presence sensor | 1 | $15-20 | [DFRobot](https://www.dfrobot.com/product-2639.html), [Amazon](https://amazon.com) |
| PIR Sensor | Motion detection (TBD model) | 1 | $1-3 | TBD |
| Light Sensor | Ambient light/lux (TBD model) | 1 | $1-2 | TBD |

### Power Management

| Component | Description | Quantity | Approximate Cost | Supplier Links |
|-----------|-------------|----------|------------------|----------------|
| PoE Module | IEEE 802.3af PoE to 5V | 1 | $3-5 | AliExpress, eBay |
| Buck Converter | 5V to 3.3V (if needed) | 1 | $0.50-1 | LCSC, DigiKey |
| Power Protection | TVS diodes, fuses | Multiple | $1-2 | Mouser, DigiKey |

### Passive Components

*Detailed list pending schematic completion*

| Type | Values | Quantity Range | Approximate Cost |
|------|--------|----------------|------------------|
| Resistors | Various (0603) | 20-30 | $1-2 (kit) |
| Capacitors | Various (0603, 0805) | 15-25 | $2-3 (kit) |
| LEDs | Status indicators | 2-3 | $0.50 |
| Crystal | 25MHz (Ethernet) | 1 | $0.50 |

---

## Enclosure & Mechanical

### 3D Printed Parts

| Component | Description | Material | Print Time | Cost |
|-----------|-------------|----------|------------|------|
| Main Housing | Top cover | PETG | ~4-6 hours | $2-3 |
| Base | Bottom base | PETG | ~3-4 hours | $1-2 |
| Mounting Bracket | Wall/ceiling mount | PETG | ~1-2 hours | $0.50-1 |

**Total Filament:** ~100-150g PETG

### Hardware

| Component | Description | Quantity | Cost |
|-----------|-------------|----------|------|
| M3 Screws | Various lengths (8mm, 12mm, 16mm) | 8-12 | $1-2 |
| M3 Nuts | Standard | 4-8 | $0.50 |
| M3 Spacers | PCB standoffs (6mm, 10mm) | 4-6 | $1-2 |
| Adhesive Pads | 3M VHB or similar (optional) | 1 pack | $2-3 |

---

## Cables & Accessories

| Component | Description | Quantity | Cost |
|-----------|-------------|----------|------|
| Ethernet Cable | Cat5e or better, various lengths | 1 | $2-10 |
| USB-C Cable | For power (if not using PoE) | 1 | $3-5 |
| USB-A to USB-C | For initial programming | 1 | $2-3 |
| USB-C Power Adapter | 5V/2A minimum (if needed) | 1 | $5-10 |

---

## Optional Components

| Component | Description | Use Case | Cost |
|-----------|-------------|----------|------|
| PoE Injector | Add PoE to non-PoE switch | No PoE switch | $15-30 |
| External Antenna | Improve WiFi range | WiFi mode in difficult locations | $5-10 |
| Heat Sink | Additional cooling | High ambient temperature | $1-2 |

---

## Total Cost Estimate

### Basic Build (Single Unit)

| Category | Estimated Cost |
|----------|----------------|
| Electronics (PCB + components) | $30-40 |
| Sensors | $17-25 |
| Enclosure (3D printed) | $3-5 |
| Hardware & cables | $5-10 |
| **Total per unit** | **$55-80** |

### Bulk Build (10 Units)

Significant savings on:
- PCB fabrication (amortized setup costs)
- Component bulk pricing
- Shipping consolidation

**Estimated cost per unit (10+ quantity):** $40-60

*Note: Costs exclude tools, power supplies, and one-time setup costs*

---

## Recommended Suppliers

### Electronics Components
- **Mouser Electronics** - Wide selection, good for US/EU
- **DigiKey** - Excellent search, fast shipping
- **LCSC** - Low-cost components, good for Asia/bulk
- **AliExpress** - Modules and breakout boards
- **Arrow Electronics** - Sometimes has better pricing

### PCB Fabrication
- **JLCPCB** - Low cost, fast turnaround
- **PCBWay** - Good quality, assembly service
- **OSH Park** - US-based, high quality
- **AISLER** - EU-based, good for small batches

### 3D Printing Filament
- **Prusament** - High quality PETG
- **eSUN** - Good value
- **Polymaker** - Reliable results
- **Atomic Filament** - Premium option

### Tools (if needed)
- **Soldering iron** - Any temperature-controlled iron
- **Multimeter** - Basic model sufficient
- **Crimping tool** - For cable connections
- **3D printer** - If not available locally, use print service

---

## Purchasing Tips

### For Individual Builders
1. Start with sensor modules to test before ordering PCBs
2. Order PCBs in minimum quantities (usually 5-10)
3. Buy passive component kits rather than individual pieces
4. Consider local electronics shops for urgent items

### For Bulk/Group Buys
1. Coordinate with other builders to reach MOQ discounts
2. PCB fabrication costs drop significantly at 25-50 units
3. Consider PCB assembly service for larger quantities
4. Negotiate shipping for consolidated orders

### Cost Optimization
- Use LCSC for passives (very low cost)
- Order PCBs during promotions
- 3D print locally to avoid shipping
- Reuse cables and power supplies when possible

---

## Substitutions & Alternatives

### Acceptable Substitutions
- ESP32 modules: Any ESP32-WROOM-32 compatible
- Ethernet PHY: Other LAN8720-compatible chips
- Connectors: Any spec-compatible alternatives

### Not Recommended to Substitute
- DFRobot C4001: Specific firmware integration
- PoE module: Must meet IEEE 802.3af standard

---

## Verification Checklist

Before ordering:
- [ ] Verify component footprints match PCB design
- [ ] Confirm voltage ratings for power components
- [ ] Check sensor compatibility with firmware
- [ ] Verify connector pinouts
- [ ] Ensure sufficient power budget
- [ ] Double-check quantities

---

## Updates & Revisions

This BOM will be updated as:
- Hardware design finalizes
- Component availability changes
- Pricing updates
- Better alternatives are found

**Last Updated:** 2025-11-28 (Placeholder version)

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense
