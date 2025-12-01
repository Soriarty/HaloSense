# ESP32-WROVER-E / ESP32-WROVER-IE Module

## Component Overview

**Manufacturer:** Espressif Systems
**Series:** ESP32-WROVER-E (commercial) / ESP32-WROVER-IE (industrial)
**Type:** Wi-Fi + Bluetooth + Bluetooth LE MCU Module **with PSRAM**
**Flash Memory:** 4MB (N4) / 8MB (N8) / 16MB (N16) variants
**PSRAM:** 2MB (R2) / 8MB (R8) integrated PSRAM (SPI interface)
**Antenna:** PCB antenna

## Purpose in HaloSense

The ESP32-WROVER-E module is an **alternative** to ESP32-WROOM-32E with additional PSRAM for memory-intensive applications:
- **PSRAM advantage:** 8MB external RAM for large buffers, image processing, complex algorithms
- **Use case:** If HaloSense requires extensive data buffering or future feature expansion
- **Trade-off:** **GPIO16 and GPIO17 are NOT available** (used internally for PSRAM)

⚠️ **GPIO Limitation:** If Ethernet RMII clock (GPIO17) or UART2 (GPIO16/17) are required, **ESP32-WROOM-32E must be used instead**.

## Technical Specifications

### Processor (Same as WROOM-32E)

| Parameter | Specification |
|-----------|--------------|
| **CPU** | Dual-core Xtensa® LX6 @ 240 MHz |
| **ROM** | 448 KB |
| **SRAM** | 520 KB (internal) |
| **PSRAM** | **2MB or 8MB (external, SPI interface)** ← **Key difference** |
| **Flash** | 4MB / 8MB / 16MB (external SPI flash) |
| **RTC SRAM** | 16 KB (slow), 8 KB (fast) |

### Wireless Connectivity (Same as WROOM-32E)

| Parameter | Specification |
|-----------|--------------|
| **Wi-Fi** | IEEE 802.11 b/g/n, 2.4 GHz |
| **Wi-Fi Mode** | Station / SoftAP / SoftAP+Station |
| **Bluetooth** | Bluetooth v4.2 BR/EDR and BLE |
| **Antenna** | PCB antenna |
| **Antenna Gain** | 2 dBi |

### Electrical Characteristics

| Parameter | Specification |
|-----------|--------------|
| **Supply Voltage** | 3.0V - 3.6V (3.3V typical) |
| **Operating Current** | Active (Wi-Fi): ~160 mA @ 240 MHz |
| | Active (BT/BLE): ~100 mA |
| | **PSRAM Active:** +20 mA (when accessing PSRAM) |
| | Modem-sleep: ~20 mA |
| | Light-sleep: ~0.9 mA |
| | Deep-sleep: ~10 μA |
| **Operating Temperature** | -40°C to +85°C (WROVER-E) |
| | -40°C to +105°C (WROVER-IE industrial) |
| **Storage Temperature** | -40°C to +150°C |

### Physical Specifications

| Parameter | Specification |
|-----------|--------------|
| **Dimensions** | 18.0 × 31.4 × 3.3 mm (larger than WROOM due to PSRAM) |
| **Pin Count** | 38 pins + 1 thermal pad |
| **Mounting Type** | SMD (Surface Mount) |
| **Pin Pitch** | 1.27 mm |

## Pin Configuration

### ⚠️ CRITICAL DIFFERENCE: GPIO16 and GPIO17 NOT CONNECTED

**From OLIMEX Schematic Note 1:**
> "When ESP32-WROVER, take in mind that **GPIO16<27> and GPIO17<28> are not connected!**"

| Pin | WROOM-32E | WROVER-E | Impact |
|-----|-----------|----------|--------|
| 27 | GPIO16 (U2RXD, EMAC_CLK_OUT) | **NC (Not Connected)** | ⚠️ **PSRAM uses GPIO16 internally** |
| 28 | GPIO17 (U2TXD, EMAC_CLK_OUT_180) | **NC (Not Connected)** | ⚠️ **PSRAM uses GPIO17 internally** |

### GPIO16 and GPIO17 Internal Use (WROVER Only)

**PSRAM SPI Interface** (internal connections, not exposed):
- **GPIO16** - PSRAM CS (Chip Select)
- **GPIO17** - PSRAM CLK (Clock)

**PSRAM shares SPI bus with Flash:**
- GPIO6 - SPI_CLK (Flash + PSRAM clock)
- GPIO7 - SPI_Q / SPI_HD (Flash + PSRAM data)
- GPIO8 - SPI_D / SPI_WP (Flash + PSRAM data)
- GPIO9-11 - Additional flash pins

### Complete GPIO Pinout (WROVER Specific)

**Identical to WROOM-32E except:**

| Pin | Name | Function | Notes |
|-----|------|----------|-------|
| 27 | **NC** | **Not Connected** | ⚠️ **GPIO16 used internally for PSRAM CS** |
| 28 | **NC** | **Not Connected** | ⚠️ **GPIO17 used internally for PSRAM CLK** |

**All other pins (1-26, 29-39) are identical to ESP32-WROOM-32E.**
See [ESP32-WROOM-32E GPIO pinout](../espressif-esp32-wroom-32e/README.md#complete-gpio-pinout-from-olimex-schematic) for complete pin details.

### Reserved / Internal Use Pins (WROVER-E)

⚠️ **DO NOT USE** - Connected to internal SPI flash and PSRAM:
- **GPIO6** - Flash/PSRAM CLK (not exposed)
- **GPIO7** - Flash/PSRAM DATA0 (not exposed)
- **GPIO8** - Flash/PSRAM DATA1 (not exposed)
- **GPIO9** - Flash/PSRAM DATA2 (not exposed)
- **GPIO10** - Flash/PSRAM DATA3 (not exposed)
- **GPIO11** - Flash CMD (not exposed)
- **GPIO16** - **PSRAM CS (not exposed, WROVER only)**
- **GPIO17** - **PSRAM CLK (not exposed, WROVER only)**

**Note from OLIMEX Schematic Note 2:**
> "GPIO6 to GPIO11 are connected to the SPI flash integrated on the module and are not led out!"

**Additional WROVER Note:**
> GPIO16 and GPIO17 are used internally by PSRAM and are not available on module pins.

## Impact on HaloSense Design

### Loss of GPIO16/GPIO17 Functionality

**Affected functions when using ESP32-WROVER-E:**

| Function | GPIO Required | WROVER Impact | Workaround |
|----------|---------------|---------------|------------|
| **Ethernet Clock (RMII)** | GPIO17 (EMAC_CLK_OUT_180) | ❌ **NOT AVAILABLE** | Use GPIO16 variant or GPIO0 input |
| **UART2** | GPIO16 (U2RXD), GPIO17 (U2TXD) | ❌ **NOT AVAILABLE** | Use different GPIO for UART |
| **I2C (OLIMEX design)** | GPIO16 (SCL) | ❌ **NOT AVAILABLE** | Use alternative GPIO (GPIO4/GPIO5) |

### Critical Design Decision

**ESP32-WROVER-E is NOT COMPATIBLE with OLIMEX ESP32-POE Ethernet design** because:
- OLIMEX uses **GPIO17** for EMAC_CLK_OUT_180 (50MHz Ethernet clock to LAN8720A PHY)
- WROVER-E does not expose GPIO17 (used internally for PSRAM)

**Options for HaloSense:**

1. **Use ESP32-WROOM-32E** (Recommended)
   - ✅ All GPIOs available including GPIO16/GPIO17
   - ✅ Compatible with Ethernet RMII (GPIO17 clock output)
   - ✅ Compatible with UART2 on GPIO16/GPIO17
   - ❌ No PSRAM (520KB SRAM only)

2. **Use ESP32-WROVER-E with Ethernet Clock Workaround**
   - ✅ 8MB PSRAM available
   - ⚠️ Use GPIO16 for EMAC_CLK_OUT or external clock source
   - ⚠️ Reassign UART2 and I2C to different GPIOs
   - Requires custom PCB design different from OLIMEX

3. **Use ESP32-WROVER-E without Ethernet**
   - ✅ 8MB PSRAM available
   - ❌ WiFi-only connectivity (no PoE, no Ethernet)
   - Not recommended for HaloSense (Ethernet is primary connectivity)

**Recommendation for HaloSense:** **Use ESP32-WROOM-32E** unless PSRAM is absolutely required.

## GPIO Allocation for HaloSense (WROVER-E)

⚠️ **Only use WROVER-E if you can live without GPIO16/GPIO17**

### Modified GPIO Allocation (vs WROOM-32E)

**Differences from WROOM-32E:**

| Function | WROOM-32E | WROVER-E Alternative |
|----------|-----------|---------------------|
| Ethernet Clock | GPIO17 (EMAC_CLK_OUT_180) | ⚠️ Use GPIO16 (if available) or external oscillator |
| UART2 (mmWave) | GPIO16 (RX), GPIO17 (TX) | Use GPIO32 (RX), GPIO33 (TX) |
| I2C (sensors) | GPIO16 (SCL), GPIO17 (SDA) | Use GPIO4 (SDA), GPIO5 (SCL) |

**Recommended HaloSense GPIO Allocation (WROVER-E):**

| Sensor/Function | GPIOs | Interface | Notes |
|-----------------|-------|-----------|-------|
| **Ethernet (LAN8720A)** | Modified RMII | RMII | **⚠️ Requires GPIO17 workaround!** |
| **mmWave (DFRobot C4001)** | GPIO32 (RX), GPIO33 (TX) | UART | Reassigned from GPIO16/17 |
| **PIR (EKMC1604111)** | GPIO35 | Digital Input | With external 33kΩ pull-down |
| **Light (BH1750)** | GPIO4 (SDA), GPIO5 (SCL) | I2C | Same as WROOM-32E |
| **SD Card** | Omit | — | Boot strapping conflicts |

**⚠️ Warning:** This allocation is **NOT directly compatible** with OLIMEX ESP32-POE design. Custom PCB required.

## PSRAM Usage in ESPHome/ESP-IDF

### Enabling PSRAM

```yaml
esp32:
  board: esp32dev
  framework:
    type: esp-idf
  platformio_options:
    board_build.arduino.memory_type: qio_qspi  # Enable PSRAM

# PSRAM Configuration
esphome:
  platformio_options:
    build_flags:
      - -DBOARD_HAS_PSRAM
      - -mfix-esp32-psram-cache-issue
```

### PSRAM Benefits for HaloSense

| Feature | Without PSRAM (WROOM) | With PSRAM (WROVER) |
|---------|----------------------|---------------------|
| **Available RAM** | ~200 KB (after framework) | ~200 KB + **2/8 MB PSRAM** |
| **Sensor Buffers** | Limited buffering | Large data logging buffers |
| **Image Processing** | Not feasible | Possible (future camera integration) |
| **Complex Algorithms** | Memory constrained | Ample headroom |

**HaloSense Current Requirements:** Basic sensor fusion does NOT require PSRAM.
**Future-proofing:** PSRAM useful if adding camera, audio, or ML processing.

## Power Budget Impact

### Power Consumption (ESP32-WROVER-E)

| Mode | Current @ 3.3V | Power | Difference vs WROOM |
|------|----------------|-------|---------------------|
| **Active (Wi-Fi TX)** | ~160 mA | ~528 mW | Same |
| **Active (PSRAM access)** | ~180 mA | ~594 mW | +20 mA when using PSRAM |
| **Modem Sleep** | ~20 mA | ~66 mW | Same |
| **Light Sleep** | ~0.9 mA | ~3.0 mW | Slightly higher (+0.1 mA) |
| **Deep Sleep** | ~10 μA | ~0.033 mW | Same |

**Impact:** PSRAM adds ~20 mA when actively accessed. Negligible for HaloSense if PSRAM not heavily used.

See complete power budget: [../../power-budget.md](../../power-budget.md)

## PCB Design Guidelines

### Same as WROOM-32E with Additional Notes

**PSRAM-Specific:**
- **No external components required** - PSRAM is fully integrated
- **GPIO16/GPIO17 pads:** Leave unconnected (NC) on PCB
- **Power supply:** Ensure stable 3.3V under PSRAM access load (+20mA bursts)

**All other guidelines identical to ESP32-WROOM-32E:**
See [ESP32-WROOM-32E PCB Design](../espressif-esp32-wroom-32e/README.md#pcb-design-guidelines)

## Assembly and Soldering

### Same Profile as WROOM-32E

See [ESP32-WROOM-32E Assembly](../espressif-esp32-wroom-32e/README.md#assembly-and-soldering) for complete reflow profile and hand soldering notes.

**Maximum 3 reflow cycles**

## Precautions and Warnings

### ⚠️ CRITICAL PRECAUTIONS (Same as WROOM-32E)

1. **ESD Protection** - ESP32 is ESD sensitive
2. **Voltage Levels** - 3.0V - 3.6V only, NO 5V
3. **Boot Strapping Pins** - GPIO0, GPIO2, GPIO5, GPIO12, GPIO15
4. **Reserved Pins** - GPIO6-GPIO11 (Flash), **GPIO16-GPIO17 (PSRAM)** ← **WROVER specific**
5. **RF Exposure** - Maintain antenna keepout zones

### Additional WROVER-E Specific Warnings

⚠️ **GPIO16/GPIO17 are INTERNALLY CONNECTED to PSRAM**
- Do NOT attempt to use GPIO16/GPIO17 on WROVER modules
- Pin 27 and Pin 28 are NC (Not Connected) on the module
- Connecting external circuits to these pins may damage the module or PSRAM

⚠️ **Module Selection**
- Verify your design does NOT require GPIO16 or GPIO17 before choosing WROVER
- If Ethernet clock (GPIO17) is needed, use WROOM-32E instead

## ESPHome Configuration

### WROVER-E Configuration with PSRAM

```yaml
esp32:
  board: esp-wrover-kit  # Use WROVER board definition
  framework:
    type: esp-idf
    sdkconfig_options:
      CONFIG_ESP32_SPIRAM_SUPPORT: y

# ⚠️ Ethernet NOT possible with WROVER unless GPIO17 clock workaround implemented
# Use WiFi instead:
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

# Sensor Interfaces (adjusted for missing GPIO16/17)
uart:
  - id: uart_mmwave
    tx_pin: GPIO33      # Changed from GPIO17 (not available on WROVER)
    rx_pin: GPIO32      # Changed from GPIO16 (not available on WROVER)
    baud_rate: 115200

i2c:
  sda: GPIO4            # Same as WROOM-32E
  scl: GPIO5            # Same as WROOM-32E
  scan: true

binary_sensor:
  - platform: gpio
    pin:
      number: GPIO35    # PIR sensor (changed from GPIO32)
      mode: INPUT
    name: "PIR Motion"
    device_class: motion
```

## Comparison: WROOM-32E vs WROVER-E

| Feature | ESP32-WROOM-32E | ESP32-WROVER-E | HaloSense Impact |
|---------|----------------|----------------|------------------|
| **Flash** | 4/8/16 MB | 4/8/16 MB | Same |
| **SRAM** | 520 KB | 520 KB | Same |
| **PSRAM** | ❌ None | ✅ 2/8 MB | WROVER advantage |
| **GPIO16** | ✅ Available | ❌ NC (PSRAM CS) | **WROVER limitation** |
| **GPIO17** | ✅ Available | ❌ NC (PSRAM CLK) | **WROVER limitation** |
| **Ethernet (OLIMEX)** | ✅ Compatible | ❌ Requires workaround | **WROOM recommended** |
| **UART2 (GPIO16/17)** | ✅ Available | ❌ Use alternatives | WROVER limitation |
| **Power (active)** | 160 mA | 180 mA (with PSRAM) | +20 mA |
| **Dimensions** | 18 × 25.5 mm | 18 × 31.4 mm | WROVER slightly larger |
| **Price** | Lower | Higher | WROOM cheaper |

**HaloSense Recommendation:** **ESP32-WROOM-32E**
- Ethernet support is critical (PoE primary connectivity)
- PSRAM not required for basic sensor fusion
- GPIO16/GPIO17 needed for Ethernet clock and/or UART2

## Related Documentation

- **Datasheet:** See [datasheets/README.md](datasheets/README.md) for PDF documentation
- **WROOM-32E Documentation:** [ESP32-WROOM-32E](../espressif-esp32-wroom-32e/README.md)
- **OLIMEX Reference:** `hardware/reference/esp32-poe/HARDWARE/ESP32-PoE-hardware-revision-M1/`
- **Espressif PSRAM Guide:** https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/external-ram.html

## References

### Official Sources

- **Product Page:** https://www.espressif.com/en/products/modules/esp32
- **Datasheet (ESP32-WROVER-E):** See datasheets/ folder
- **Datasheet (ESP32-WROVER-IE):** See datasheets/ folder (industrial variant)
- **PSRAM Application Note:** See datasheets/ folder

### Related HaloSense Components

- **ESP32-WROOM-32E:** [Documentation](../espressif-esp32-wroom-32e/README.md) - **Recommended for HaloSense**
- **Ethernet PHY:** LAN8720A (TBD documentation)
- **Sensors:** [mmWave](../../sensors/dfrobot-c4001/README.md), [PIR](../../sensors/panasonic-ekmc1604111/README.md), [Light](../../sensors/rohm-bh1750/README.md)

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-01 | Initial documentation based on OLIMEX ESP32-POE schematic analysis with WROVER-specific GPIO16/17 limitations |

---

**Status:** 📋 Component documented from OLIMEX reference design

**OLIMEX Schematic Notes:**
- Symbol: `ESP32-WROVER(WROOM)-UNIVERSAL`
- **Note 1:** "When ESP32-WROVER, take in mind that GPIO16<27> and GPIO17<28> are not connected!"
- **Note 2:** "GPIO6 to GPIO11 are connected to the SPI flash integrated on the module and are not led out!"
- Variants supported: ESP32-WROVER-E-N4R8, ESP32-WROVER-IE

**Design Decision:** **Use ESP32-WROOM-32E for HaloSense** unless PSRAM is absolutely required and Ethernet clock workaround is implemented.

