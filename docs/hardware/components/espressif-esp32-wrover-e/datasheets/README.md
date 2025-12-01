# ESP32-WROVER-E / WROVER-IE Official Datasheets

This directory contains the official PDF datasheets and technical documentation from Espressif Systems.

## Files

**TODO:** Add the following datasheets to this directory:

- **esp32-wrover-e_esp32-wrover-ie_datasheet_en.pdf** - ESP32-WROVER-E/IE Module Datasheet
  - Source: https://www.espressif.com/sites/default/files/documentation/esp32-wrover-e_esp32-wrover-ie_datasheet_en.pdf
  - Contains: Complete module specifications with PSRAM, pin configuration, electrical characteristics, mechanical drawings
  - **Key sections:** GPIO16/GPIO17 limitations, PSRAM specifications

- **esp32_datasheet_en.pdf** - ESP32 SoC Datasheet (same as WROOM-32E)
  - Source: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf
  - Contains: ESP32 chip specifications, peripheral descriptions, memory architecture

- **esp32_hardware_design_guidelines_en.pdf** - Hardware Design Guidelines (same as WROOM-32E)
  - Source: https://www.espressif.com/sites/default/files/documentation/esp32_hardware_design_guidelines_en.pdf
  - Contains: PCB layout recommendations, RF design, power supply design, strapping pins

- **esp32_psram_info.pdf** - PSRAM Application Note (WROVER-specific)
  - Source: Available in Espressif documentation repository
  - Contains: PSRAM usage guidelines, memory management, performance optimization

- **esp32_technical_reference_manual_en.pdf** - Technical Reference Manual (same as WROOM-32E)
  - Source: https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf
  - Contains: Complete peripheral register descriptions, PSRAM interface details

## Online Resources

- **Product Page:** https://www.espressif.com/en/products/modules/esp32
- **ESP32 Documentation:** https://docs.espressif.com/projects/esp-idf/en/latest/esp32/
- **PSRAM Guide:** https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/external-ram.html
- **ESP-IDF Programming Guide:** https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/index.html
- **Espressif GitHub:** https://github.com/espressif/esp-idf

## Usage

These PDF files are reference materials for:
- **WROVER Module Datasheet:** Pin assignments (NC on GPIO16/GPIO17!), PSRAM specs, electrical characteristics
- **SoC Datasheet:** Chip capabilities, peripheral features, memory maps
- **Hardware Guidelines:** PCB layout, RF design, PSRAM power considerations
- **PSRAM Application Note:** External RAM usage, cache configuration, performance tuning
- **Technical Manual:** Register-level programming, PSRAM controller configuration

For quick reference and HaloSense-specific notes (including GPIO16/GPIO17 limitations), see the main component documentation: [../README.md](../README.md)

---

**Important:** ESP32-WROVER-E has GPIO16 and GPIO17 internally connected to PSRAM and NOT available for external use. See main documentation for details.

**Note:** PDF files should be downloaded manually from Espressif's official website. They are tracked in the repository for offline reference.
