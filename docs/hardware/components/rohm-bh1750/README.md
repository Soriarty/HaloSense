# ROHM BH1750FVI Ambient Light Sensor

## Overview

The ROHM BH1750FVI is a digital 16-bit ambient light sensor IC with I2C bus interface. This sensor provides accurate lux measurements with spectral response approximating the human eye, making it ideal for automatic backlight adjustment and ambient light detection in smart home applications.

**Product Information:**
- **Manufacturer:** ROHM Semiconductor
- **Part Number:** BH1750FVI / BH1750FVI-TR (tape and reel)
- **Package:** WSOF-6 (SMD)
- **Interface:** I2C bus (f/s Mode Support)
- **Current Consumption:** 120μA typical (@ 100 lx)

## Key Features

- **Wide detection range:** 1 - 65,535 lx (extendable to 0.11 - 100,000 lx with measurement time adjustment)
- **High resolution:** 16-bit digital output
- **Spectral response:** Approximates human eye sensitivity
- **Low power consumption:** 120μA typical active, 0.01μA power-down
- **I2C interface:** Standard/Fast mode, 2 selectable slave addresses
- **No external components required**
- **Light noise rejection:** 50Hz / 60Hz rejection function
- **Light source independent:** Works with incandescent, fluorescent, halogen, LED, and sunlight
- **MSL 3:** Moisture Sensitivity Level 3 (168 hours @ 30°C/60% RH)
- **Small package:** WSOF-6 SMD (2.6mm × 1.6mm)

## Technical Specifications

### Detection Capabilities

| Parameter | Specification |
|-----------|--------------|
| Measurement Range (default) | 1 - 65,535 lx |
| Measurement Range (extended) | 0.11 - 100,000 lx (with MTreg adjustment) |
| Resolution (H-Resolution Mode) | 1 lx |
| Resolution (L-Resolution Mode) | 4 lx |
| Resolution (H-Resolution Mode2) | 0.5 lx |
| Measurement Accuracy | ±20% (0.96 - 1.44 times actual) |
| Dark Output (0 lx) | 0 - 16 counts |
| Peak Wavelength | 560 nm (human eye response) |

### Electrical Characteristics

| Parameter | Symbol | Min | Typical | Max | Unit | Conditions |
|-----------|--------|-----|---------|-----|------|------------|
| Supply Voltage | Vcc | 2.4V | 3.0V | 3.6V | V | **HaloSense: 3.3V** |
| I2C Reference Voltage | VDVI | 1.65V | - | VCC | V | |
| Supply Current (active) | Icc1 | - | 120μA | 190μA | μA | Ev = 100 lx |
| Power-Down Current | Icc2 | 0.01μA | - | 1.0μA | μA | No light input |
| Operating Temperature | Topr | -40°C | 25°C | 85°C | °C | |
| Storage Temperature | Tstg | -40°C | - | 100°C | °C | |

**Power Consumption @ 3.3V (HaloSense):**
- **Active Mode:** 120μA × 3.3V = **0.40mW** (typical)
- **Power-Down Mode:** 0.01μA × 3.3V = **0.033μW** (standby)

### Communication Interface

| Parameter | Specification |
|-----------|--------------|
| Interface Type | I2C bus (Standard/Fast mode) |
| I2C Clock Frequency | Up to 400 kHz |
| Data Format | 16-bit digital output |
| Default I2C Address (ADDR='L') | 0x23 (0100011 binary) |
| Alternative I2C Address (ADDR='H') | 0x5C (1011100 binary) |
| Logic Level (DVI ≥ 1.8V) | VIH: 0.7×DVI, VIL: 0.3×DVI |

## Pin Configuration

| Pin | Function | Description |
|-----|----------|-------------|
| VCC | Power Supply | Connect to **3.3V** (ESP32 power rail) |
| ADDR | I2C Address Select | 'L' (≤0.3VCC) = 0x23, 'H' (≥0.7VCC) = 0x5C |
| GND | Ground | Common ground |
| SDA | I2C Data | I2C data line (requires pull-up resistor) |
| DVI | I2C Reference & Reset | I2C reference voltage + async reset terminal |
| SCL | I2C Clock | I2C clock line (requires pull-up resistor) |

**Pin Layout (WSOF-6 package):**
```
    1: VCC
   /      \
  2: ADDR  6: SCL
  3: GND   5: DVI
   \      /
    4: SDA
```

### DVI Terminal (Critical)

The **DVI terminal** serves dual purposes:
1. **I2C Reference Voltage:** Sets logic levels for I2C bus
2. **Asynchronous Reset:** Must be held LOW (≤0.4V) for at least 1μs after VCC power-up

**HaloSense Design:** Connect DVI to 3.3V through a simple RC filter (1kΩ + 1μF) to ensure proper reset timing.

## Operating Modes

The BH1750FVI supports three measurement modes with different resolution and speed trade-offs:

### 1. H-Resolution Mode (High Resolution)

**Specifications:**
- **Resolution:** 1 lx per count
- **Measurement Time:** 120ms typical (max 180ms)
- **Range:** 1 - 65,535 lx
- **Use Case:** Standard ambient light measurement

**Opcode:**
- Continuously: `0x10` (0001_0000)
- One Time: `0x20` (0010_0000)

### 2. L-Resolution Mode (Low Resolution, Fast)

**Specifications:**
- **Resolution:** 4 lx per count
- **Measurement Time:** 16ms typical (max 24ms)
- **Range:** 4 - 65,535 lx
- **Use Case:** Fast updates, less critical accuracy

**Opcode:**
- Continuously: `0x13` (0001_0011)
- One Time: `0x23` (0010_0011)

### 3. H-Resolution Mode2 (Very High Resolution)

**Specifications:**
- **Resolution:** 0.5 lx per count
- **Measurement Time:** 120ms typical (max 180ms)
- **Range:** 0.5 - 65,535 lx
- **Use Case:** Low-light detection (<10 lx)

**Opcode:**
- Continuously: `0x11` (0001_0001)
- One Time: `0x21` (0010_0001)

### Continuous vs One-Time Measurement

| Mode | Behavior |
|------|----------|
| **Continuously** | Sensor remains active, updates every 120ms (H-Res) or 16ms (L-Res) |
| **One Time** | Single measurement, then automatically enters Power Down mode |

**HaloSense Recommendation:** Use **Continuously H-Resolution Mode** with 60-second update interval in ESPHome for optimal power/accuracy balance.

## I2C Protocol

### Slave Addresses

- **ADDR Pin = 'L' (GND):** 0x23 (default for HaloSense)
- **ADDR Pin = 'H' (VCC):** 0x5C

### Command Set

| Command | Opcode | Description |
|---------|--------|-------------|
| Power Down | `0x00` | Enter standby mode (0.01μA) |
| Power On | `0x01` | Wake from standby |
| Reset | `0x07` | Reset data register (not accepted in Power Down) |
| Continuously H-Res | `0x10` | Start continuous 1 lx resolution measurement |
| Continuously H-Res2 | `0x11` | Start continuous 0.5 lx resolution measurement |
| Continuously L-Res | `0x13` | Start continuous 4 lx resolution measurement |
| One Time H-Res | `0x20` | Single 1 lx measurement + auto power-down |
| One Time H-Res2 | `0x21` | Single 0.5 lx measurement + auto power-down |
| One Time L-Res | `0x23` | Single 4 lx measurement + auto power-down |
| Change MTreg (High) | `01000_MT[7:5]` | Adjust measurement time (high bits) |
| Change MTreg (Low) | `011_MT[4:0]` | Adjust measurement time (low bits) |

### Measurement Sequence

**Write Command (example: Continuously H-Resolution, ADDR=0x23):**
```
START → 0x23 (W) → ACK → 0x10 → ACK → STOP
```

**Read Result (after 120ms):**
```
START → 0x23 (R) → ACK → High_Byte → ACK → Low_Byte → NACK → STOP
```

**Lux Calculation:**
```
Lux = ((High_Byte << 8) | Low_Byte) / 1.2
```

**Example:**
- High Byte = `0x83` (10000011 = 131 decimal upper part = 2^15 + 2^9 + 2^8 + 2^7)
- Low Byte = `0x90` (10010000 = 144 decimal → combined value consideration)
- Wait, let me recalculate: High×256 + Low = 131×256 + 144 = 33536 + 144 = 33680
- Lux = 33680 / 1.2 ≈ 28067 lx

### Measurement Time Adjustment (MTreg)

The BH1750FVI allows sensitivity adjustment by changing the measurement time register (MTreg):

| MTreg Value | Sensitivity | Min Detection | Resolution (H-Res) |
|-------------|-------------|---------------|-------------------|
| 31 (0x1F) | 0.45× default | 0.23 lx | 1.85 lx/count |
| 69 (0x45) | **1.0× default** | **1 lx** | **1 lx/count** |
| 254 (0xFE) | 3.68× default | 0.11 lx (H-Res2) | 0.23 lx/count |

**Formula:**
```
Lux = ((High_Byte << 8) | Low_Byte) × (69 / MTreg) / 1.2
```

## ESPHome Configuration

### Basic Configuration

```yaml
# I2C Bus Setup
i2c:
  sda: GPIO21  # ESP32-POE
  scl: GPIO22  # ESP32-POE
  scan: true
  frequency: 100kHz  # Standard I2C

# BH1750 Ambient Light Sensor
sensor:
  - platform: bh1750
    name: "${friendly_name} Ambient Light"
    address: 0x23  # ADDR pin to GND
    resolution: H_RESOLUTION  # H_RESOLUTION, H_RESOLUTION2, L_RESOLUTION
    measurement_duration: 69  # Default MTreg value
    update_interval: 60s
    unit_of_measurement: "lx"
    accuracy_decimals: 0
    filters:
      - sliding_window_moving_average:
          window_size: 3
          send_every: 1
```

### Advanced Configuration (Low Light Optimization)

```yaml
sensor:
  - platform: bh1750
    name: "${friendly_name} Ambient Light"
    address: 0x23
    resolution: H_RESOLUTION2  # 0.5 lx resolution for low light
    measurement_duration: 254  # Max sensitivity (3.68× default)
    update_interval: 60s
    filters:
      - clamp:
          min_value: 0
          max_value: 65535
      - or:
        - throttle: 10s
        - delta: 5.0  # Only report if change >5 lx
```

### I2C Address Selection

**Hardware (ADDR pin wiring):**
- **GND (default):** I2C address = 0x23
- **VCC:** I2C address = 0x5C

**ESPHome:**
```yaml
sensor:
  - platform: bh1750
    address: 0x5C  # If ADDR pin connected to VCC
```

## Performance Comparison

### BH1750 vs VEML6030/7700

| Feature | BH1750FVI | VEML6030 | VEML7700 |
|---------|-----------|----------|----------|
| **Range (default)** | 1 - 65,535 lx | 0 - 120,000 lx | 0 - 120,000 lx |
| **Range (extended)** | 0.11 - 100,000 lx | 0 - 120,000 lx | 0 - 120,000 lx |
| **Resolution** | 0.5 - 4 lx | 16-bit configurable | 16-bit configurable |
| **Power (active)** | **120μA** | 2-13μA | 2-20μA |
| **Power (standby)** | 0.01μA | 0.5μA | 0.5μA |
| **Interface** | I2C (0x23/0x5C) | I2C (0x10/0x48) | I2C (0x10 fixed) |
| **Interrupt Pin** | ✗ No | ✓ Yes | ✗ No |
| **MSL Rating** | **MSL 3** | MSL 4 | MSL 4 |
| **Package** | WSOF-6 | SMD-6P (2×2mm) | SMD-4P |
| **Price (IC, LCSC)** | ~$0.48 | ~$0.31 | ~$0.50 |
| **JLCPCB Part#** | C78960 | C132182 | C1850416 |

**BH1750 Advantages:**
- ✅ **Lower MSL rating (MSL 3)** - Better for humid environments (kitchen/bathroom)
- ✅ **Proven, mature technology** - Widely used, extensive community support
- ✅ **Simple operation** - No complex gain/integration time tuning needed
- ✅ **Slightly cheaper breakout boards** (~$4.50 vs $6-8)

**BH1750 Disadvantages:**
- ❌ **10× higher active current** (120μA vs 13μA)
- ❌ **No interrupt pin** - Polling-based only
- ❌ **Limited ultra-low light** - Min 0.11 lx vs VEML's true 0 lx capability

## HaloSense Integration Notes

### Power Supply Design

**Voltage:** 3.3V from ESP32 power rail

**Reasoning:**
1. **ESP32 Compatibility:** I2C logic levels match ESP32 3.3V I/O
2. **Simplicity:** No level shifters required
3. **Power Budget:** 120μA @ 3.3V = 0.40mW (negligible impact on PoE budget)

### I2C Bus Configuration

**Bus Setup:**
- **I2C Shared Bus:** BH1750 (0x23) shares bus with future sensors
- **Pull-up Resistors:** 4.7kΩ to 3.3V (on SDA and SCL)
- **DVI Terminal:** Connect to 3.3V via RC filter (1kΩ + 1μF)

**GPIO Allocation:**
- **SDA:** GPIO21 (ESP32-POE standard I2C)
- **SCL:** GPIO22 (ESP32-POE standard I2C)

**I2C Address Conflicts:**
- ✅ BH1750: 0x23 (ADDR=GND, default)
- ✅ No conflicts with mmWave (UART), PIR (digital GPIO)
- ✅ Future expansion: Can use 0x5C if needed

### PCB Design Considerations

**Component Placement:**
- **Location:** Top-side of circular PCB, near light sensor window
- **Orientation:** Photodiode (PD) area facing enclosure light window
- **Clearance:** 0.4mm minimum around PD area (0.25mm × 0.3mm active area)

**Optical Design:**
- **Light Window:** Clear polycarbonate window in enclosure
- **Window Transmission:** Calibrate with MTreg if transmission <100%
- **Dust Protection:** Window prevents dust on sensor surface

**PCB Layout:**
- **Ground Plane:** Continuous ground plane under sensor
- **Decoupling:** 0.1μF ceramic capacitor close to VCC pin
- **Trace Width:** Standard I2C traces (0.2mm minimum)

### Moisture Sensitivity (MSL 3)

**MSL 3 Rating:** 168 hours @ 30°C / 60% RH floor life

**Advantages for HaloSense:**
- ✅ **Better than VEML (MSL 4):** Easier moisture handling
- ✅ **Humid Environments:** Suitable for kitchen/bathroom with proper enclosure
- ✅ **Assembly:** Less stringent baking requirements vs MSL 4

**Protection Measures:**
- **Enclosure:** IP54+ rating (dust + splash water protection)
- **Conformal Coating:** Acrylic or silicone coating on PCB
- **Ventilation:** Breathing slots with labyrinth path (water cannot enter)

### Calibration and Measurement Accuracy

**Typical Accuracy:** ±20% (0.96 - 1.44× actual lux)

**Calibration Method:**
1. **Reference Measurement:** Use calibrated lux meter in target environment
2. **MTreg Adjustment:** Adjust MTreg to compensate for optical window transmission
3. **ESPHome Calibration:** Use `calibrate_linear` filter for fine-tuning

**Example Calibration:**
```yaml
sensor:
  - platform: bh1750
    name: "Ambient Light"
    address: 0x23
    filters:
      - calibrate_linear:
          - 0.0 -> 0.0
          - 100.0 -> 96.0   # Correct -4% error at 100 lx
          - 1000.0 -> 1044.0  # Correct +4.4% error at 1000 lx
```

### Light Source Independence

BH1750FVI is designed to provide consistent readings across different light sources:

| Light Source | Relative Reading |
|--------------|------------------|
| Fluorescent Light | 1.00 (reference) |
| Incandescent Light | 0.95 - 1.05 |
| Halogen Lamp | 0.95 - 1.05 |
| White LED | 0.90 - 1.10 |
| Sunlight | 0.95 - 1.05 |

**HaloSense Benefit:** Accurate readings regardless of home lighting type.

## Datasheets and References

**Official Documentation:**
- `docs/sensors/rohm-bh1750/datasheets/rohm-bh1750fvi-datasheet.pdf` - Complete datasheet (18 pages)
- Manufacturer: ROHM Semiconductor
- Datasheet Revision: D (2011.11)

**External Resources:**
- ESPHome BH1750 Component: https://esphome.io/components/sensor/bh1750.html
- I2C Specification: NXP I2C-bus specification (UM10204)
- ROHM Website: https://www.rohm.com

**JLCPCB Assembly:**
- Part Number: C78960
- Package: WSOF-6
- Assembly Type: SMT (Extended Parts, $3 setup fee)
- MSL Rating: MSL 3
- Stock: Excellent availability

## Recommended Operating Conditions

**For HaloSense (Indoor Smart Home Use):**
- **Supply Voltage:** 3.3V ±5% (3.135V - 3.465V)
- **Ambient Temperature:** 0°C to 50°C (typical home range)
- **Update Interval:** 60 seconds (balance power/responsiveness)
- **Measurement Mode:** Continuously H-Resolution (1 lx resolution)
- **Light Range:** 1 - 10,000 lx (covers darkness to bright daylight indoors)

**Power Budget Contribution:**
- **Active (60s interval):** ~120μA continuous = 0.40mW
- **Total HaloSense Impact:** <0.02% of 5W target budget

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-11-29 | Initial technical guide for HaloSense integration |
