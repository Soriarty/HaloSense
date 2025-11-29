# ROHM BH1750FVI Official Datasheets

This directory contains the official PDF datasheets and technical documentation from ROHM Semiconductor for the BH1750FVI digital ambient light sensor.

## Files

- **rohm-bh1750fvi-datasheet.pdf** - BH1750FVI Complete Datasheet (18 pages)
  - Source: Downloaded from Mouser Electronics (original filename: bh1750fvi-e-186247.pdf)
  - Contains: Complete specifications for BH1750FVI digital 16-bit serial output ambient light sensor
  - Includes: Electrical characteristics, I2C protocol specifications, operating modes, dimensional drawings, register maps, command set
  - **Primary reference** for BH1750 specifications

## Online Resources

- **ROHM Product Page:** https://www.rohm.com/products/sensors-mems/ambient-light-sensors/bh1750fvi-product
- **Mouser Electronics:** https://www.mouser.com/ProductDetail/ROHM-Semiconductor/BH1750FVI-TR
- **JLCPCB Parts Library:** https://jlcpcb.com/partdetail/Rohm-BH1750FVI_TR/C78960

## BH1750 Series Overview

The BH1750 series includes multiple package variants:
- **BH1750FVI:** WSOF006-2020 package (2.0mm × 2.0mm × 0.8mm) ← **HaloSense selection**
- **BH1750:** Legacy package (no longer recommended for new designs)

Both variants share identical electrical specifications:
- Supply voltage: 2.4-3.6V (HaloSense uses 3.3V)
- Current consumption: 120μA typ @ 100lx, 0.01μA power-down
- I2C interface: Standard/Fast mode (100kHz/400kHz)
- Measurement range: 1-65,535 lx

## Usage

This PDF file is the reference material for:
- **Complete Datasheet:** Electrical specifications, I2C command set, operating modes, timing diagrams, register maps
- **Integration:** Schematic design, PCB layout, I2C address selection (ADDR pin)
- **Firmware Development:** Command protocol implementation, measurement mode selection

For quick reference and ESPHome integration details, see the main sensor documentation: [../README.md](../README.md)

## Key Specifications Summary

**Selected Model:** BH1750FVI-TR (JLCPCB C78960)
- **Package:** WSOF006-2020 (SMD, 2.0mm × 2.0mm)
- **Sensitivity:** 1 lx resolution
- **Range:** 1-65,535 lx
- **Accuracy:** ±20% typical
- **I2C Address:** 0x23 (ADDR='L') or 0x5C (ADDR='H')
- **MSL Rating:** MSL 3 (168 hours @ 30°C/60%RH after bag opening)
- **Operating Temperature:** -40°C to +85°C

**Advantages for HaloSense:**
- MSL 3 rating (better than VEML6030/7700 MSL 4) for kitchen/bathroom installations
- Proven technology with excellent ESPHome support
- Simple single-command measurement operation
- JLCPCB Extended Parts (C78960) - $3 setup fee per unique part

**Trade-offs:**
- Higher current consumption (120μA vs VEML6030 13μA)
- Larger package (2.0mm × 2.0mm vs VEML 2.0mm × 1.25mm)
- Still well within power budget (1.85W typical << 15.4W PoE limit)

---

**Note:** PDF files are tracked in the repository for offline reference. They are available from official sources if needed.
