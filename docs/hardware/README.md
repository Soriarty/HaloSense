# Hardware Design Documentation

This directory contains hardware design specifications and analysis for the HaloSense presence sensor.

## 📄 Documents

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

**Last Updated:** 2025-11-29
