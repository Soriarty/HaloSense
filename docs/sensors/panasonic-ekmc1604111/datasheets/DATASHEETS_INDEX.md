# Panasonic EKMC1604111 Official Datasheets

This directory contains the official PDF datasheets and technical documentation from Panasonic for the EKMC (VZ) series PaPIRs motion sensors.

## Files

- **panasonic-ekmc-series-datasheet.pdf** - EKMC Series Complete Datasheet
  - Source: Downloaded from Mouser Electronics (original filename: adatlap-1541159...)
  - Contains: Complete specifications for EKMC1601/1603/1604 series
  - Includes: Electrical characteristics, detection zones, dimensional drawings, timing diagrams
  - **Primary reference** for EKMC1604111 specifications

- **panasonic-ekmb-ekmc-reference.pdf** - EKMB/EKMC Technical Reference
  - Source: Panasonic technical documentation
  - Contains: Additional technical details for both EKMB and EKMC series
  - Includes: Application notes, design considerations, extended specifications

## Online Resources

- **Panasonic PaPIRs Website:** https://industrial.panasonic.com/ww/products/sensors/built-in-sensors/infrared-sensors/papirs
- **Product Search:** Search "EKMC1604111" on Panasonic Industrial website
- **Mouser Electronics:** https://www.mouser.com/ (search "EKMC1604111")
- **CAD Data:** Available from Panasonic PaPIRs website (3D models, PCB footprints)

## EKMC Series Overview

The EKMC (VZ) series includes three detection types:
- **EKMC1601xxx:** Standard detection type (5m range, 94° × 82° coverage)
- **EKMC1603xxx:** Long distance detection type (12m range, 102° × 92° coverage)
- **EKMC1604xxx:** **Wall installation type** (12m/6m/3m zones, 40° × 105° coverage) ← **HaloSense selection**

Each type is available in three lens colors:
- **xx1:** White
- **xx2:** Black
- **xx3:** Pearl White

## Usage

These PDF files are reference materials for:
- **EKMC Series Datasheet:** Complete electrical specifications, detection characteristics, pinout, dimensions
- **EKMB/EKMC Reference:** Design guidelines, application examples, performance optimization

For quick reference and integration details, see the main sensor documentation: [../EKMC1604111_TECHNICAL_GUIDE.md](../EKMC1604111_TECHNICAL_GUIDE.md)

## Model Selection Notes

**Selected Model:** EKMC1604111
- **1604:** Wall installation type with three-step lens
- **1:** White lens color
- **Detection:** 12m (1st step), 6m (2nd step), 3m (3rd step)
- **Coverage:** 40° horizontal (55.6° max) × 105° vertical (112° max)
- **Optimal for:** Wall-mounted presence detection paired with mmWave radar

**Alternative Models (same EKMC1604 type):**
- **EKMC1604112:** Black lens (same specifications)
- **EKMC1604113:** Pearl white lens (same specifications)

**Alternative Types (different detection patterns):**
- **EKMC1603111:** Long distance type (12m, 102° × 92°) - wider horizontal, narrower vertical
- **EKMC1601111:** Standard type (5m, 94° × 82°) - shorter range, balanced coverage

---

**Note:** PDF files are tracked in the repository for offline reference. They are available from official sources if needed.
