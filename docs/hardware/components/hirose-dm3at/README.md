# Micro SD Card Socket - HRS DM3 Series

## Component Overview

**Manufacturer:** Hirose Electric (HRS)
**Series:** DM3 microSD™ Card Connectors
**Part Number:** TFC-9P-1.7H (ATFFS150A01BR016) or compatible DM3AT-SF-PEJM5
**Type:** Push-Push with ejection mechanism, Top board mounting (Standard)
**Height:** 1.7mm (low profile)

## Purpose in HaloSense

Optional micro SD card slot for local data logging and configuration storage:
- Sensor data logging (presence events, motion detection, light levels)
- Configuration backup/restore
- Firmware update storage
- Diagnostic log storage
- Offline operation capability

## Technical Specifications

### Electrical Characteristics

| Parameter | Specification |
|-----------|--------------|
| **Voltage Rating** | 125V AC |
| **Current Rating** | 0.5A per contact |
| **Contact Resistance** | 100mΩ max (initial) |
| **Insulation Resistance** | 1000 MΩ min @ 500V DC |
| **Withstanding Voltage** | 500V AC / 1 minute |
| **Operating Voltage** | 3.3V typical (ESP32 logic level) |

### Environmental Ratings

| Parameter | Specification |
|-----------|--------------|
| **Operating Temperature** | -25°C to +85°C (Note 1) |
| **Storage Temperature** | -40°C to +85°C (Note 2) |
| **Operating Humidity** | RH 95% max (no condensation) |

**Note 1:** Includes temperature rise caused by current flow
**Note 2:** Applies to products stored for long periods prior to mounting

### Mechanical Specifications

| Parameter | Specification |
|-----------|--------------|
| **Durability** | 10,000 cycles @ 400-600 cycles/hour |
| **Insertion/Ejection** | Push-Push mechanism with 4.0mm eject distance |
| **Card Detection** | Normally Open switch (2 contacts: A and B) |
| **PCB Height** | ~2.9mm above PCB surface |
| **Footprint** | 15.1mm × 14.5mm (see PCB pattern) |

### Materials and Finishes

| Part | Material | Finish |
|------|----------|--------|
| **Insulator** | LCP (Liquid Crystal Polymer) | Black, UL94V-0 |
| **Contacts** | Copper alloy | Gold plated (contact area & leads) |
| **Shield/Cover** | Stainless steel | Gold plated (leads) |
| **Other components** | Stainless steel, Piano wire | Nickel plated |

## Pin Configuration

### microSD Card Pinout

| Pin | Name | Function | ESP32 Connection |
|-----|------|----------|------------------|
| 1 | DAT2/RES | Data Line 2 | GPIO12 (HS2_DATA2) |
| 2 | CD/DAT3/CS | Card Detect / Data 3 / Chip Select | GPIO13 (HS2_DATA3) |
| 3 | CMD/DI | Command / Data In | **GPIO15 (HS2_CMD)** |
| 4 | VDD | Power Supply | 3.3V (regulated) |
| 5 | CLK/SCLK | Clock | **GPIO14 (HS2_CLK)** |
| 6 | GND | Ground | GND |
| 7 | DAT0/DO | Data Line 0 / Data Out | **GPIO2 (HS2_DATA0)** |
| 8 | DAT1/RES | Data Line 1 | GPIO4 (HS2_DATA1) |

### Card Detection Switch

| Switch Contact | State without Card | State with Card Inserted |
|----------------|-------------------|-------------------------|
| Switch A | Open | Closed |
| Switch B | Open | Closed |

**Connection:** Typically connected to a GPIO with internal pull-up for card presence detection.

## ESP32 Interface - SDMMC Host Controller

### HS2 Mode (High Speed SD/SDIO/MMC Host 2)

The ESP32 has two SDMMC host controllers. HS2 is typically used for SD card interfacing:

**Required Connections (1-bit SD mode):**
- **GPIO15** → HS2_CMD (Command line)
- **GPIO14** → HS2_CLK (Clock line)
- **GPIO2** → HS2_DATA0 (Data line 0)

**Optional Connections (4-bit SD mode):**
- **GPIO4** → HS2_DATA1 (Data line 1)
- **GPIO12** → HS2_DATA2 (Data line 2)
- **GPIO13** → HS2_DATA3 (Data line 3)

**Supporting Circuitry:**
- **Pull-up resistors:** 10kΩ on CMD, DAT0-3 lines (can use internal ESP32 pull-ups)
- **Decoupling capacitor:** 10μF + 100nF near VDD pin
- **Card detect:** GPIO input with internal pull-up (connect to switch contact)

### SDMMC vs SPI Mode

| Feature | SDMMC Mode (HS2) | SPI Mode |
|---------|------------------|----------|
| **Speed** | Up to 40 MHz (High Speed) | Up to 20 MHz typically |
| **Data Lines** | 1-bit or 4-bit parallel | Single MOSI/MISO |
| **Performance** | ~20 MB/s (4-bit HS) | ~2.5 MB/s |
| **GPIO Usage** | Dedicated HS2 pins | Any SPI-capable GPIO |
| **Complexity** | Hardware SDMMC controller | Software bitbang or SPI peripheral |
| **Recommended** | ✅ For HaloSense | ❌ Not recommended (slower) |

## PCB Design Guidelines

### Mounting Pattern

**Critical Dimensions:**
- Footprint: 15.1mm (length) × 14.5mm (width)
- Pin pitch: 1.1mm
- Shield connection: 4 points for EMI protection
- **Keepout zones:** See Note 3 below

### PCB Layout Notes

**Note 1:** ⚠️ **CL (Center Line) Indication**
The ℄ symbol indicates the center line of the microSD card slot. Align this with mechanical drawings.

**Note 2:** 📌 **Card Detection Switch Zones**
Two card detection switch contacts (A and B) change state when card is inserted.

**Note 3:** 🚫 **No Conductive Traces**
**CRITICAL:** Hatched areas on PCB pattern indicate **NO CONDUCTIVE TRACES ALLOWED**. These zones prevent short circuits with the metal card body and shield. Violation will cause:
- Short circuits between card and PCB traces
- Potential data corruption
- Card detection malfunction

**Note 4:** 🔌 **Shield/Ground Connections**
Four shield connection points must be soldered to PCB ground plane for:
- Mechanical strength
- EMI shielding
- ESD protection
- Reliable ground reference

### Signal Integrity Considerations

1. **Trace impedance:** 50Ω controlled impedance for CLK and CMD lines (optional for <20MHz)
2. **Trace length matching:** Match DATA0-3 lengths within 5mm for 4-bit mode
3. **Ground plane:** Continuous ground plane under signal traces
4. **Decoupling:** Place 100nF capacitor <5mm from VDD pin
5. **Pull-ups:** 10kΩ resistors on CMD and all DATx lines (or use ESP32 internal pull-ups)

## Assembly and Soldering

### Reflow Soldering Profile

**Recommended Profile (Lead-Free SAC305):**
- **Preheat:** 150°C for 90-120 seconds
- **Soak:** 200°C for 50 seconds
- **Peak:** 230-250°C max (250°C absolute maximum)
- **Time above 230°C:** <50 seconds
- **Cooling:** Natural cool-down

**Important:** Maximum 2 reflow cycles

### Hand Soldering

- **Temperature:** 350°C
- **Duration:** 3 seconds max per joint
- **Tip:** Use fine chisel tip for SMD leads

## Precautions and Warnings

### ⚠️ CRITICAL PRECAUTIONS

1. **DO NOT clean with solvents**
   Never immerse or clean the entire connector with cleaning solutions. This may affect the ejection mechanism and electrical performance.

2. **DO NOT apply excessive force**
   Handle carefully during assembly and after PCB mounting to avoid damaging the delicate mechanism.

3. **Correct card insertion**
   The connector includes reverse insertion protection, but always insert cards correctly:
   - Contacts facing DOWN (toward PCB)
   - Notched corner toward the card slot opening
   - Push until click is felt

4. **Mount before inserting card**
   The connector MUST be correctly mounted on the PCB before inserting any card. Do not insert cards in unmounted connectors.

5. **FPC mounting reinforcement**
   When mounting on Flexible Printed Circuit (FPC), use a flat reinforcement plate **minimum 0.3mm thick** under the FPC.

6. **Card detection switch handling**
   The Normally Open card detection switch is delicate. Do not manually actuate or apply force to switch contacts.

### Manufacturing Marks

Small visible residual manufacturing fluids or tooling marks do not affect connector performance. This is normal.

### Card Wear

Repeated insertions and removals (up to 10,000 cycles rated) may leave minor marks on the card itself. This does not affect connector or card performance.

## ESPHome Configuration

### Basic SD Card Configuration (1-bit mode)

```yaml
# SD Card Configuration
# Uses ESP32 SDMMC Host 2 (HS2) in 1-bit mode

esp32:
  framework:
    type: esp-idf
    sdkconfig_options:
      CONFIG_SDMMC_ENABLED: "y"

# SD Card Logger
logger:
  level: INFO
  logs:
    sdmmc_periph: DEBUG
    sdmmc_common: DEBUG
    sdmmc_req: DEBUG
    sdspi_host: DEBUG
    vfs_fat_sdmmc: DEBUG
    vfs_fat_sdspi: DEBUG

# Custom component for SD card management
esphome:
  on_boot:
    priority: -100
    then:
      - logger.log: "Checking for SD card..."
      # Add custom SD card initialization here

# Card detection GPIO (example)
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO_CD  # TBD - connect to card detect switch
      mode: INPUT_PULLUP
    name: "SD Card Detected"
    device_class: connectivity
```

### Advanced Configuration (4-bit mode)

**Note:** 4-bit mode provides ~8× faster performance but uses 6 GPIO pins total.

```yaml
# For 4-bit SDMMC mode, all DATA lines must be connected:
# GPIO15 = CMD
# GPIO14 = CLK
# GPIO2 = DATA0
# GPIO4 = DATA1
# GPIO12 = DATA2
# GPIO13 = DATA3
```

## Power Budget Impact

### Power Consumption

| State | Current @ 3.3V | Power |
|-------|----------------|-------|
| **Idle (no card)** | <1μA | <3.3μW |
| **Card present (idle)** | ~100μA | ~330μW |
| **Active read** | ~50mA | ~165mW |
| **Active write** | ~80mA | ~264mW |

**Impact on HaloSense power budget:**
- Idle: Negligible (<0.001% of 1.3W budget)
- Active: ~0.17W read / ~0.26W write (temporary peaks)

**Note:** SD card current is drawn from 3.3V rail during active operations only. Idle consumption is negligible.

## Design Decision for HaloSense

### ⚠️ GPIO Conflict Warning

**CRITICAL ISSUE:** The standard ESP32 SDMMC HS2 pins conflict with other functions:

| GPIO | HS2 Function | **Potential Conflict** |
|------|-------------|----------------------|
| GPIO15 | HS2_CMD | **Boot strapping pin** (must be HIGH at boot) |
| GPIO14 | HS2_CLK | May conflict with Ethernet or other peripherals |
| GPIO2 | HS2_DATA0 | **Boot strapping pin** (must be LOW/floating at boot) |
| GPIO12 | HS2_DATA2 | **Boot strapping pin** (MTDI, flash voltage select) |
| GPIO13 | HS2_DATA3 | Available |
| GPIO4 | HS2_DATA1 | May conflict with UART or other peripherals |

### Implementation Options

**Option 1: Include SD slot (OLIMEX approach)**
- Provides local logging and offline operation
- Requires careful GPIO management (boot strapping conflicts)
- May need pull-up/pull-down resistors to ensure proper boot behavior
- SPI mode alternative if GPIO conflicts cannot be resolved

**Option 2: Omit SD slot (simplified design)**
- Reduces GPIO conflicts
- Relies on network connectivity for all logging
- Simpler design, lower BOM cost
- Can add in future hardware revision if needed

### Recommendation for Phase 2

**Decision deferred to Phase 2 (Hardware Design):**
- Analyze complete GPIO allocation table
- Determine if boot strapping conflicts can be resolved
- Evaluate if SPI mode is acceptable (slower but more flexible GPIO)
- Consider if local storage is essential for use case

**Footprint placeholder:** Consider adding PCB footprint as unpopulated component for future hardware revision flexibility.

## Related Documentation

- **Datasheet:** [datasheets/hrs-dm3-series-datasheet.pdf](datasheets/hrs-dm3-series-datasheet.pdf) (HRS DM3 Series microSD Connectors)
- **Datasheets Index:** [datasheets/README.md](datasheets/README.md) (Complete datasheet catalog)
- **OLIMEX Reference:** `hardware/reference/esp32-poe/HARDWARE/ESP32-PoE-hardware-revision-M1/`
- **SD Card Standard:** SD Association Physical Layer Specification
- **ESP32 Datasheet:** Espressif ESP32 Technical Reference Manual (SDMMC Host Controller chapter)

## References

### Datasheets and Sources

- **HRS DM3 Series Datasheet:** [Mouser - e60900232-38395.pdf](https://www.mouser.com/datasheet/2/185/e60900232-38395.pdf)
- **Component on EasyEDA:** [OLIMEX_Connectors_MICRO_SD](https://easyeda.com/components/OLIMEX-Connectors-MICRO-SD-TFC-9P-1-xH-ATFFS150A01BR016_09ea8cc170d44fe6927f1eb3e307935a)
- **Distributor (JASSTA):** [Micros.com.pl](https://www.micros.com.pl/en/product/z-9tf-09h1-5,125742.html)
- **microSD Card Pinout Guide:** [Components101](https://components101.com/misc/microsd-card-pinout-datasheet)
- **SD Pinout Reference:** [PinoutGuide.com](https://pinoutguide.com/Memory/sdcard_pinout.shtml)

### Operation Manuals

- **DM3AT Series:** ETAD-F0345
- **DM3BT Series:** ETAD-F0324
- **DM3CS Series:** ETAD-F0335
- **DM3D Series:** ETAD-F0353

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-01 | Initial documentation for HaloSense Phase 2 planning |

---

**Status:** 📋 Component documented, implementation decision pending Phase 2 GPIO allocation analysis

**Next Steps:**
1. Complete GPIO allocation table in Phase 2
2. Resolve boot strapping pin conflicts (GPIO2, GPIO12, GPIO15)
3. Decide: SDMMC mode vs SPI mode vs omit SD slot
4. Update PCB design with chosen implementation
