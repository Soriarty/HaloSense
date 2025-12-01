# ESP32-WROOM-32E / ESP32-WROOM-32UE Module

## Component Overview

**Manufacturer:** Espressif Systems
**Series:** ESP32-WROOM-32E (PCB antenna) / ESP32-WROOM-32UE (U.FL connector)
**Type:** Wi-Fi + Bluetooth + Bluetooth LE MCU Module
**Flash Memory:** 4MB (N4) / 8MB (N8) / 16MB (N16) variants
**Antenna:** PCB antenna (32E) / U.FL connector (32UE)

## Purpose in HaloSense

The ESP32-WROOM-32E module serves as the main microcontroller for the HaloSense presence sensor:
- **Primary MCU:** All sensor data processing and automation logic
- **Wi-Fi connectivity:** 802.11 b/g/n (2.4GHz) as fallback network option
- **Bluetooth:** Optional proximity detection and configuration
- **GPIO expansion:** Sensor interfacing (UART, I2C, digital I/O)
- **Ethernet PHY interface:** LAN8720A connection via RMII

## Technical Specifications

### Processor

| Parameter | Specification |
|-----------|--------------|
| **CPU** | Dual-core Xtensa® LX6 @ 240 MHz |
| **ROM** | 448 KB |
| **SRAM** | 520 KB |
| **Flash** | 4MB / 8MB / 16MB (external SPI flash) |
| **RTC SRAM** | 16 KB (slow), 8 KB (fast) |

### Wireless Connectivity

| Parameter | Specification |
|-----------|--------------|
| **Wi-Fi** | IEEE 802.11 b/g/n, 2.4 GHz |
| **Wi-Fi Mode** | Station / SoftAP / SoftAP+Station |
| **Bluetooth** | Bluetooth v4.2 BR/EDR and BLE |
| **Antenna** | PCB antenna (32E) / U.FL connector (32UE) |
| **Antenna Gain** | 2 dBi (PCB antenna) |

### Electrical Characteristics

| Parameter | Specification |
|-----------|--------------|
| **Supply Voltage** | 3.0V - 3.6V (3.3V typical) |
| **Operating Current** | Active (Wi-Fi): ~160 mA @ 240 MHz |
| | Active (BT/BLE): ~100 mA |
| | Modem-sleep: ~20 mA |
| | Light-sleep: ~0.8 mA |
| | Deep-sleep: ~10 μA |
| **Operating Temperature** | -40°C to +85°C |
| **Storage Temperature** | -40°C to +150°C |

### Physical Specifications

| Parameter | Specification |
|-----------|--------------|
| **Dimensions** | 18.0 × 25.5 × 3.1 mm |
| **Pin Count** | 38 pins + 1 thermal pad |
| **Mounting Type** | SMD (Surface Mount) |
| **Pin Pitch** | 1.27 mm |

## Pin Configuration

### Complete GPIO Pinout (from OLIMEX Schematic)

| Pin | Name | Function | Alternative Functions |
|-----|------|----------|----------------------|
| 1 | GND | Ground | Power ground |
| 2 | VDD33 | Power Supply | 3.3V input (300mA max) |
| 3 | EN | Enable | Active HIGH, 10kΩ pull-up required |
| 4 | GPI36 | Input Only | SENSOR_VP, ADC1_CH0, RTC_GPIO0 |
| 5 | GPI39 | Input Only | SENSOR_VN, ADC1_CH3, RTC_GPIO3 |
| 6 | GPI34 | Input Only | ADC1_CH6, RTC_GPIO4 |
| 7 | GPI35 | Input Only | ADC1_CH7, RTC_GPIO5 |
| 8 | GPIO32 | Bidirectional | XTAL_32K_P, ADC1_CH4, TOUCH9, RTC_GPIO9 |
| 9 | GPIO33 | Bidirectional | XTAL_32K_N, ADC1_CH5, TOUCH8, RTC_GPIO8 |
| 10 | GPIO25 | Bidirectional | DAC_1, ADC2_CH8, RTC_GPIO6, EMAC_RXD0 |
| 11 | GPIO26 | Bidirectional | DAC_2, ADC2_CH9, RTC_GPIO7, EMAC_RXD1 |
| 12 | GPIO27 | Bidirectional | ADC2_CH7, TOUCH7, RTC_GPIO17, EMAC_RX_DV |
| 13 | GPIO14 | Bidirectional | ADC2_CH6, TOUCH6, RTC_GPIO16, MTMS, HSPICLK, **HS2_CLK**, SD_CLK, EMAC_TXD2 |
| 14 | GPIO12 | Bidirectional | ADC2_CH5, TOUCH5, RTC_GPIO15, MTDI, HSPIQ, **HS2_DATA2**, SD_DATA2, EMAC_TXD3 |
| 15 | GND | Ground | Power ground |
| 16 | GPIO13 | Bidirectional | ADC2_CH4, TOUCH4, RTC_GPIO14, MTCK, HSPID, **HS2_DATA3**, SD_DATA3, EMAC_RX_ER |
| 17 | NC | Not Connected | Reserved (WROVER: SPI Flash) |
| 18 | NC | Not Connected | Reserved (WROVER: SPI Flash) |
| 19 | NC | Not Connected | Reserved (WROVER: SPI Flash) |
| 20 | NC | Not Connected | Reserved (WROVER: SPI Flash) |
| 21 | NC | Not Connected | Reserved (WROVER: SPI Flash) |
| 22 | NC | Not Connected | Reserved (WROVER: SPI Flash) |
| 23 | GPIO15 | Bidirectional | ADC2_CH3, TOUCH3, MTDO, HSPICS0, RTC_GPIO13, **HS2_CMD**, SD_CMD, EMAC_RXD3 |
| 24 | GPIO2 | Bidirectional | ADC2_CH2, TOUCH2, RTC_GPIO12, HSPIWP, **HS2_DATA0**, SD_DATA0 |
| 25 | GPIO0 | Bidirectional | ADC2_CH1, TOUCH1, RTC_GPIO11, CLK_OUT1, EMAC_TX_CLK |
| 26 | GPIO4 | Bidirectional | ADC2_CH0, TOUCH0, RTC_GPIO10, HSPIHD, **HS2_DATA1**, SD_DATA1, EMAC_TX_ER |
| 27 | GPIO16 | Bidirectional | HS1_DATA4, U2RXD, EMAC_CLK_OUT |
| 28 | GPIO17 | Bidirectional | HS1_DATA5, U2TXD, EMAC_CLK_OUT_180 |
| 29 | GPIO5 | Bidirectional | VSPICS0, HS1_DATA6, EMAC_RX_CLK |
| 30 | GPIO18 | Bidirectional | VSPICLK, HS1_DATA7 |
| 31 | GPIO19 | Bidirectional | VSPIQ, U0CTS, EMAC_TXD0 |
| 32 | NC | Not Connected | Reserved |
| 33 | GPIO21 | Bidirectional | VSPIHD, EMAC_TX_EN |
| 34 | GPIO3 | Bidirectional | U0RXD, CLK_OUT2 |
| 35 | GPIO1 | Bidirectional | U0TXD, CLK_OUT3, EMAC_RXD2 |
| 36 | GPIO22 | Bidirectional | VSPIWP, U0RTS, EMAC_TXD1 |
| 37 | GPIO23 | Bidirectional | VSPID, HS1_STROBE |
| 38 | GND | Ground | Power ground |
| 39 | THERMAL_PAD | Thermal Pad | Connect to GND plane |

### GPIO Functional Grouping

#### Input-Only GPIOs
- **GPI36** (SENSOR_VP) - ADC1_CH0
- **GPI39** (SENSOR_VN) - ADC1_CH3
- **GPI34** - ADC1_CH6
- **GPI35** - ADC1_CH7

**Note:** These pins do NOT have internal pull-up/pull-down resistors. Use external resistors if needed.

#### Strapping Pins (Boot Mode Configuration)
- **GPIO0** - Must be HIGH for normal boot, LOW for download mode
- **GPIO2** - Must be LOW or floating for normal boot
- **GPIO5** - Timing of SDIO Slave
- **GPIO12** - Flash voltage (VDD_SDIO) selection: LOW=3.3V, HIGH=1.8V
- **GPIO15** - Must be HIGH for normal boot (MTDO)

**Critical:** Ensure strapping pins have correct states during boot!

#### SD Card Interface (SDMMC HS2)
**HS2 Mode GPIOs** (for micro SD card - see [hirose-dm3at](../hirose-dm3at/README.md)):
- **GPIO15** - HS2_CMD (Command)
- **GPIO14** - HS2_CLK (Clock)
- **GPIO2** - HS2_DATA0 (Data 0) - **⚠️ Boot strapping pin!**
- **GPIO4** - HS2_DATA1 (Data 1)
- **GPIO12** - HS2_DATA2 (Data 2) - **⚠️ Boot strapping pin!**
- **GPIO13** - HS2_DATA3 (Data 3)

**Warning:** GPIO2, GPIO12, GPIO15 are boot strapping pins. Careful PCB design required!

#### Ethernet RMII Interface (for LAN8720A PHY)
- **GPIO0** - EMAC_TX_CLK (Clock output from PHY to ESP32)
- **GPIO19** - EMAC_TXD0 (Transmit Data 0)
- **GPIO21** - EMAC_TX_EN (Transmit Enable)
- **GPIO22** - EMAC_TXD1 (Transmit Data 1)
- **GPIO25** - EMAC_RXD0 (Receive Data 0)
- **GPIO26** - EMAC_RXD1 (Receive Data 1)
- **GPIO27** - EMAC_RX_DV (Receive Data Valid)

**RMII Clock Options:**
- **GPIO16** - EMAC_CLK_OUT (50MHz clock output to PHY)
- **GPIO17** - EMAC_CLK_OUT_180 (50MHz clock output, 180° phase shift)

#### I2C Interface (for sensors)
**HaloSense I2C Configuration (BH1750 Light Sensor):**
- **GPIO32** - SDA (Serial Data)
- **GPIO33** - SCL (Serial Clock)

**Note:** Default I2C pins GPIO21/GPIO22 conflict with Ethernet RMII (EMAC_TX_EN/EMAC_TXD1), so GPIO32/GPIO33 are used instead. These pins are available on both WROOM-32E and WROVER-E modules.

#### UART Interfaces
**UART0** (Programming/Console):
- **GPIO1** - U0TXD (Transmit)
- **GPIO3** - U0RXD (Receive)

**UART1** (Flexible, internal only - not routed to pins by default)

**UART2** (Available for sensors):
- **GPIO16** - U2RXD (Receive)
- **GPIO17** - U2TXD (Transmit)

#### SPI Interfaces
**HSPI (available for external devices):**
- **GPIO12** - HSPIQ (MISO)
- **GPIO13** - HSPID (MOSI)
- **GPIO14** - HSPICLK (CLK)
- **GPIO15** - HSPICS0 (CS)

**VSPI (available for external devices):**
- **GPIO18** - VSPICLK (CLK)
- **GPIO19** - VSPIQ (MISO)
- **GPIO23** - VSPID (MOSI)
- **GPIO5** - VSPICS0 (CS)

### Reserved / Internal Use Pins

⚠️ **DO NOT USE** - Connected to internal SPI flash:
- **GPIO6** - Flash CLK (not exposed on module)
- **GPIO7** - Flash DATA0 (not exposed on module)
- **GPIO8** - Flash DATA1 (not exposed on module)
- **GPIO9** - Flash DATA2 (not exposed on module)
- **GPIO10** - Flash DATA3 (not exposed on module)
- **GPIO11** - Flash CMD (not exposed on module)

**Note from OLIMEX Schematic:**
> "GPIO6 to GPIO11 are connected to the SPI flash integrated on the module and are not led out!"

## GPIO Allocation for HaloSense

### Assigned GPIOs (from OLIMEX ESP32-POE Design)

#### Ethernet (LAN8720A RMII) - **Primary Connectivity**
- GPIO0 - EMAC_TX_CLK
- GPIO19 - EMAC_TXD0
- GPIO21 - EMAC_TX_EN
- GPIO22 - EMAC_TXD1
- GPIO25 - EMAC_RXD0
- GPIO26 - EMAC_RXD1
- GPIO27 - EMAC_RX_DV
- GPIO17 - EMAC_CLK_OUT_180 (50MHz clock to PHY)

#### I2C (Sensors) - **GPIO32/GPIO33**
OLIMEX uses GPIO16 (I2C-SCL) in their extension headers, but GPIO21/GPIO22 (default I2C) conflict with Ethernet RMII.

**HaloSense Solution:**
- **GPIO32** - I2C SDA (BH1750 Light Sensor)
- **GPIO33** - I2C SCL (BH1750 Light Sensor)
- No conflicts with Ethernet, boot strapping pins, or other peripherals

#### Available for Sensors (HaloSense Custom Allocation)

**For mmWave Sensor (UART):**
- **GPIO16** (RX), **GPIO9** (TX) - Software UART (hardware UART2 conflicts with Ethernet clock)

**For PIR Sensor (Digital Input):**
- **GPI35** - Input-only GPIO with external 33kΩ pull-down resistor

**For Light Sensor (I2C):**
- **GPIO32** (SDA), **GPIO33** (SCL) - Hardware I2C for BH1750FVI

### HaloSense GPIO Conflict Resolution

**Resolved Conflicts:**
1. **I2C vs Ethernet:** Default I2C pins (GPIO21/GPIO22) conflict with Ethernet RMII
   - **✅ Resolution:** Use GPIO32 (SDA) and GPIO33 (SCL) for I2C sensors

2. **UART2 vs Ethernet Clock:** Hardware UART2 (GPIO16/GPIO17) conflicts with EMAC_CLK_OUT_180
   - **✅ Resolution:** Use software UART on GPIO16 (RX) and GPIO9 (TX) for mmWave sensor

**Avoided Conflicts:**
- **SD Card:** Omitted to avoid boot strapping pin conflicts (GPIO2, GPIO12, GPIO15)

**Recommended GPIO Allocation for HaloSense:**

| Sensor/Function | GPIOs | Interface | Notes |
|-----------------|-------|-----------|-------|
| **Ethernet (LAN8720A)** | GPIO0, 17, 18, 19, 21, 22, 23, 25, 26, 27 | RMII | **Primary connectivity** |
| **mmWave (DFRobot C4001)** | GPIO16 (RX), GPIO9 (TX) | Software UART | Avoids GPIO17 Ethernet clock |
| **PIR (EKMC1604111)** | GPI35 | Digital Input | Input-only GPIO, 33kΩ pull-down |
| **Light (BH1750FVI)** | GPIO32 (SDA), GPIO33 (SCL) | Hardware I2C | No conflicts with Ethernet |
| **SD Card** | Omitted | — | Avoids boot strapping conflicts |

**Note:** GPIO allocation finalized based on OLIMEX ESP32-POE schematic analysis.

## Power Budget Impact

### Power Consumption (ESP32-WROOM-32E)

| Mode | Current @ 3.3V | Power | Use Case |
|------|----------------|-------|----------|
| **Active (Wi-Fi TX)** | ~160 mA | ~528 mW | Wi-Fi data transmission |
| **Active (Wi-Fi RX)** | ~95 mA | ~314 mW | Wi-Fi data reception |
| **Modem Sleep** | ~20 mA | ~66 mW | Wi-Fi connected, CPU active |
| **Light Sleep** | ~0.8 mA | ~2.6 mW | Periodic wake for sensor polling |
| **Deep Sleep** | ~10 μA | ~0.033 mW | Long-term standby |
| **Ethernet (RMII)** | ~100 mA | ~330 mW | Wired network (preferred mode) |

**HaloSense Typical Operation:**
- **Primary mode:** Ethernet active, Wi-Fi disabled: **~330 mW**
- **Fallback mode:** Wi-Fi active (modem sleep): **~66 mW**
- **Total ESP32 + Ethernet:** ~330 mW + 198 mW (LAN8720A) = **~528 mW**

See complete power budget: [../../power-budget.md](../../power-budget.md)

## PCB Design Guidelines

### Decoupling and Power Supply

1. **Decoupling Capacitors (close to VDD33 pins):**
   - 100nF ceramic (×4) - within 5mm of each VDD pin
   - 10μF tantalum or ceramic (×1) - bulk capacitance

2. **EN Pin:**
   - 10kΩ pull-up resistor to VDD33
   - 0.1μF capacitor to GND (optional, for noise immunity)
   - Connect to supervisor IC or RC reset circuit

3. **Strapping Resistors:**
   - GPIO0: 10kΩ pull-up (normal boot)
   - GPIO2: 10kΩ pull-down or leave floating
   - GPIO5: 10kΩ pull-up
   - GPIO12: 10kΩ pull-down (3.3V flash voltage)
   - GPIO15: 10kΩ pull-up

4. **Power Supply:**
   - Stable 3.3V rail with ≥500mA capacity
   - Low-noise LDO recommended (for ADC accuracy)
   - Separate analog supply filtering if using ADC

### RF Design Considerations

**PCB Antenna Variant (ESP32-WROOM-32E):**
- Keepout zone: 15mm × 5mm at antenna end
- No copper pour under antenna area
- Ground plane on all other layers for shielding

**U.FL Connector Variant (ESP32-WROOM-32UE):**
- 50Ω controlled impedance trace from module to antenna connector
- Keep trace as short as possible (<30mm)
- Solid ground plane under RF trace

### Thermal Management

- Connect thermal pad (pin 39) to ground plane
- Via stitching around thermal pad (multiple 0.3mm vias)
- Ensure adequate copper area for heat dissipation
- Consider heatsink or thermal vias for continuous Wi-Fi TX operation

## Assembly and Soldering

### Reflow Soldering Profile

**Recommended Profile (Lead-Free SAC305):**
- **Preheat:** 150-180°C for 60-120 seconds
- **Soak:** 180-200°C for 60-120 seconds
- **Reflow:** Peak 250°C max (240-250°C range)
- **Time above 217°C:** 60-90 seconds
- **Cooling:** Natural cool-down, <6°C/s

**Important:** Maximum 3 reflow cycles

### Hand Soldering

**NOT RECOMMENDED** due to fine-pitch SMD pads and thermal pad.
If absolutely necessary:
- **Temperature:** 350°C max
- **Duration:** <3 seconds per pin
- **Tip:** Fine chisel or conical tip
- **Flux:** Use quality no-clean flux

## Precautions and Warnings

### ⚠️ CRITICAL PRECAUTIONS

1. **ESD Protection**
   - ESP32 is ESD sensitive. Use proper ESD precautions during handling and assembly.
   - ESD protection recommended on exposed I/O pins.

2. **Voltage Levels**
   - VDD33: 3.0V - 3.6V only. **DO NOT apply 5V!**
   - GPIO: 3.3V logic levels only. Use level shifters for 5V devices.

3. **Boot Strapping Pins**
   - Ensure GPIO0, GPIO2, GPIO5, GPIO12, GPIO15 have correct states during power-on and reset.
   - Incorrect strapping may prevent boot or enter download mode unintentionally.

4. **Reserved Pins**
   - **NEVER connect to GPIO6-GPIO11** - internal SPI flash use only.
   - Connecting these pins will damage the module.

5. **RF Exposure**
   - Maintain antenna keepout zones.
   - For commercial products, perform RF compliance testing (FCC, CE, etc.).

6. **Current Capacity**
   - Each GPIO pin: 12mA source/sink max, 28mA absolute maximum.
   - Total current for all GPIOs: 200mA max (40mA recommended).

## ESPHome Configuration

### Basic ESP32 Configuration

```yaml
esp32:
  board: esp32dev
  framework:
    type: esp-idf  # Required for Ethernet support

# Ethernet Configuration (OLIMEX ESP32-POE compatible)
ethernet:
  type: LAN8720
  mdc_pin: GPIO23
  mdio_pin: GPIO18
  clk_mode: GPIO17_OUT
  phy_addr: 0
  power_pin: GPIO12  # Optional, enables PHY power control

# WiFi as Fallback
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  # Use Ethernet as primary, WiFi as fallback
  enable_on_boot: false

# Sensor Interfaces
uart:
  - id: uart_mmwave
    tx_pin: GPIO9       # DFRobot C4001 mmWave sensor
    rx_pin: GPIO16
    baud_rate: 115200

i2c:
  sda: GPIO32           # BH1750FVI light sensor
  scl: GPIO33
  scan: true

binary_sensor:
  - platform: gpio
    pin:
      number: GPIO35    # Panasonic EKMC1604111 PIR sensor
      mode: INPUT
    name: "PIR Motion"
    device_class: motion
```

## Related Documentation

- **Datasheet:** See [datasheets/README.md](datasheets/README.md) for PDF documentation
- **OLIMEX Reference:** `hardware/reference/esp32-poe/HARDWARE/ESP32-PoE-hardware-revision-M1/`
- **Espressif Documentation:** https://docs.espressif.com/projects/esp-idf/en/latest/esp32/
- **ESP32 Technical Reference:** https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf

## References

### Official Sources

- **Product Page:** https://www.espressif.com/en/products/modules/esp32
- **Datasheet (ESP32-WROOM-32E):** See datasheets/ folder
- **Datasheet (ESP32-WROOM-32UE):** See datasheets/ folder
- **ESP32 Hardware Design Guidelines:** https://www.espressif.com/sites/default/files/documentation/esp32_hardware_design_guidelines_en.pdf

### Related HaloSense Components

- **Ethernet PHY:** LAN8720A (TBD documentation)
- **Micro SD Socket:** [Hirose DM3AT](../hirose-dm3at/README.md)
- **Sensors:** [mmWave](../../sensors/dfrobot-c4001/README.md), [PIR](../../sensors/panasonic-ekmc1604111/README.md), [Light](../../sensors/rohm-bh1750/README.md)

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-01 | Initial documentation based on OLIMEX ESP32-POE schematic analysis |

---

**Status:** 📋 Component documented from OLIMEX reference design

**OLIMEX Schematic Notes:**
- Symbol: `ESP32-WROVER(WROOM)-UNIVERSAL`
- Footprint: `ESP32-WROVER_MODULE`
- Variants supported: ESP32-WROOM-32E-N4, ESP32-WROOM-32E-N16, ESP32-WROOM-32UE

**Next Steps:**
1. Resolve I2C vs Ethernet GPIO conflicts (GPIO21/22)
2. Finalize sensor GPIO allocation
3. Determine SD card implementation (or omit)
4. Add official Espressif datasheets to datasheets/ folder
5. Update PCB design with chosen variant

