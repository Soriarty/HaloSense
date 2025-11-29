# Panasonic EKMC1604111 PIR Motion Sensor (Wall Installation Type)

## Overview

The Panasonic EKMC1604111 is a compact PaPIRs (Panasonic Passive Infrared) motion sensor designed specifically for wall-mounted installations. This sensor features a three-step lens design optimized for detecting human motion across different distance zones with asymmetric vertical coverage ideal for wall placement at human mid-height (~1.2-1.5m).

**Product Information:**
- **Model:** EKMC1604111
- **Series:** EKMC (VZ) - PaPIRs Motion Sensor
- **Type:** Wall Installation Type
- **Manufacturer:** Panasonic
- **Lens Color:** White (also available: EKMC1604112 Black, EKMC1604113 Pearl White)
- **Current Consumption:** 170μA (standby mode)
- **Output Type:** Digital

## Key Features

- **Three-step lens design** for multi-zone detection (12m / 6m / 3m)
- **Wide horizontal coverage** (105°, up to 112° max) - excellent room coverage
- **Asymmetric vertical coverage** (40°, optimized +6.6° / -49° for wall mounting)
- **Ultra-low power consumption** (170μA) - ideal for PoE applications
- **Digital output** - simple GPIO integration
- **Wide voltage range** (3.0V - 6.0V) - **HaloSense: 3.3V operation**
- **Compact through-hole design** - easy mainboard integration
- **Industrial temperature range** (-20°C to +60°C)
- **Instant motion detection** - significantly faster response than mmWave

## Technical Specifications

### Detection Capabilities

| Parameter | Specification |
|-----------|--------------|
| Detection Distance (1st step lens) | 12 meters |
| Detection Distance (2nd step lens) | 6 meters |
| Detection Distance (3rd step lens) | 3 meters |
| Horizontal Detection Angle | 40° typical (55.6° max) |
| Vertical Detection Angle | 105° typical (112° max) |
| Detection Zones | 68 beams |
| Response Time | <0.1s (instant motion trigger) |

**Detection Orientation:**
- **Horizontal (TOP VIEW):** 105° (112° max) - wide room coverage
- **Vertical (SIDE VIEW):** 40° (55.6° max) - asymmetric: +6.6° (above) / -49° (below)
- **Optimized mounting height:** Human mid-height (~1.2-1.5m) on wall

### Electrical Characteristics

| Parameter | Symbol | Min | Typical | Max | Conditions |
|-----------|--------|-----|---------|-----|------------|
| Operating Voltage | Vdd | 3.0V | **3.3V** | 6.0V | **HaloSense: 3.3V** |
| Current Consumption (standby) | Iw | - | 170μA | - | Vdd=3.3V, 25°C, Iout=0 |
| Output Current (during detection) | Iout | - | ~85μA | 100μA | Vdd=3.3V, 25°C, R=33kΩ |
| Output Voltage (during detection) | Vout | Vdd·0.5V | **2.8V** | Vdd-0.5V | Vdd=3.3V, 25°C |
| Circuit Stability Time | Twu | - | - | 30 sec | Power-on warmup |

**Operating Conditions:**
- **Operating Temperature:** -20°C to +60°C (no frost, no condensation)
- **Storage Temperature:** -20°C to +70°C
- **Power Supply Voltage Range:** 3.0V to 6.0V (datasheet), **HaloSense: 3.3V**

### Power Supply Selection

**HaloSense Design Decision: 3.3V Power Supply** ✅

Although the EKMC1604111 supports 3.0V to 6.0V operation, **3.3V is the only recommended voltage** for HaloSense integration.

#### Why 3.3V?

**1. ESP32 GPIO Compatibility** (Critical)
```
PIR @ 3.3V → Output HIGH = 2.8V → ESP32 GPIO (Safe ✅)
PIR @ 5.0V → Output HIGH = 4.5V → ESP32 GPIO (DAMAGE! ❌)
```

- ESP32 GPIO pins are **3.3V logic level**
- **Maximum safe input voltage:** 3.6V (per ESP32 datasheet)
- PIR output @ 3.3V: **2.8V** (Vdd - 0.5V) → **Safe for direct connection**
- PIR output @ 5.0V: **4.5V** (Vdd - 0.5V) → **Exceeds ESP32 maximum, requires level shifter**

**2. Design Simplicity**
- **3.3V:** Direct GPIO connection, one pull-down resistor (33kΩ)
- **5.0V:** Requires level shifter (e.g., BSS138 MOSFET or resistor divider) + pull-down resistor (47kΩ)

**3. BOM Cost & Reliability**
| Aspect | 3.3V | 5.0V |
|--------|------|------|
| **Components** | PIR + 33kΩ resistor | PIR + 47kΩ resistor + level shifter |
| **BOM lines** | 2 | 3-4 |
| **PCB area** | Minimal | Additional space for level shifter |
| **Failure points** | 2 components | 3-4 components |
| **Cost** | Lower | Higher |

**4. Noise Margin Trade-off**
- **5.0V advantage:** Higher signal voltage (4.5V vs 2.8V) = better noise immunity
- **3.3V sufficient:** Digital output, low current (85μA), short PCB traces
- ESP32 GPIO HIGH threshold: ~2.0V → **2.8V provides 0.8V margin** (adequate)
- Proper PCB layout (ground plane, guard traces) ensures reliable operation

**5. Power Consumption**
- **3.3V:** 170μA × 3.3V = **0.56mW**
- **5.0V:** 170μA × 5.0V = **0.85mW**
- Savings: 0.29mW (negligible, but contributes to overall PoE power budget)

#### Design Recommendation

**Use 3.3V power rail for PIR sensor:**
- Available from ESP32 3.3V regulator output
- Direct GPIO connection (no level shifter)
- Single 33kΩ pull-down resistor
- Simpler, cheaper, more reliable

**If 5.0V operation is required** (not recommended):
- Must add level shifter circuit (voltage divider or MOSFET-based)
- Change pull-down resistor to 47kΩ
- Additional PCB complexity and BOM cost
- **Not supported in this documentation** (3.3V only)

### Physical Dimensions

| Parameter | Specification |
|-----------|--------------|
| Lens Diameter | ø20.7mm |
| PCB Mounting Diameter | ø11mm |
| Overall Height | 20.2mm (above PCB) |
| Pin Diameter | ø0.45mm ±0.05mm |
| Pin Spacing (P.C.D.) | ø5.08mm ±0.2mm |
| Pin Configuration | 3 pins (GND, VDD, OUT) |
| Mounting Angle | 45° ±4° (two pins), 45° ±4° (one pin) |
| Mounting Type | Through-hole (THT) |

## Pin Configuration

| Pin | Function | Description |
|-----|----------|-------------|
| VDD | Power Supply | **Connect to 3.3V** (ESP32 power rail) |
| GND | Ground | Common ground |
| OUT | Digital Output | High (2.8V) when motion detected, Open circuit when no motion |

**Pin Layout (bottom view):**
```
    VDD
   /   \
 GND   OUT
```

Pin circle diameter (P.C.D.): 5.08mm ±0.2mm
Pin spacing: 120° between VDD-GND, VDD-OUT

## Detection Characteristics

### Detection Condition Requirements

For reliable detection, the following conditions must be met:
- **Temperature difference:** >4°C between target and surroundings
- **Movement speed:** 1.0 m/s (typical human walking speed)
- **Target concept:** Human body ~700mm × 250mm
- **Target movement:** Crossing detection beam (perpendicular motion preferred)

### Three-Step Lens System

The EKMC1604111 features a unique three-step lens design providing multiple detection zones:

| Lens Step | Detection Range | Use Case |
|-----------|----------------|----------|
| 1st step | 12 meters | Large rooms, hallways |
| 2nd step | 6 meters | Medium rooms |
| 3rd step | 3 meters | Small rooms, close proximity |

This multi-zone design allows adaptation to different room sizes and provides reliable detection across varying distances.

### Detection Zone Coverage

**Horizontal Coverage (TOP VIEW):**
- Typical: 105° (wide room coverage)
- Maximum: 112°
- Effective for wall-mounted sensors covering wide areas

**Vertical Coverage (SIDE VIEW):**
- Typical: 40° (asymmetric distribution)
- Maximum: 55.6°
- Optimized distribution: +6.6° (upward) / -49° (downward)
- **Wall mounting optimization:** Sensor aimed slightly downward, ideal for human mid-height placement

**Detection Zones:**
- 68 individual detection beams
- Multi-beam pattern reduces blind spots
- Overlapping coverage ensures reliable detection

### Timing Characteristics

**Circuit Stability Time (Twu):**
- Maximum: 30 seconds after power-on
- During warmup: Output status undefined (ON/OFF)
- Detection not guaranteed until warmup complete
- **Important:** Factor warmup time into system initialization

## Output Signal Characteristics

### Digital Output Behavior

| State | Output Voltage | Description |
|-------|----------------|-------------|
| Motion Detected | Vdd - 0.5V (HIGH) | Target present within detection zone |
| No Motion | Open Circuit (LOW) | No target detected or target stationary |

**Output Timing:**
```
Power Supply    ___________________
               |
               |____Twu (≤30s)____|_____

Detecting      ____Present__Absent__Present__Absent____
Target

Output         ____  ____    ____  ____
Voltage           |__|    |__|    |__|
               LOW  HIGH LOW  HIGH LOW
```

### Pull-Down Resistor Requirement

**Critical:** The output requires an external pull-down resistor to prevent false alarms.

#### Why Pull-Down Resistor is Required

From the datasheet (page 7, Output current specification):
- **Maximum output current:** 100μA (Note 2)
- **Warning:** "If the output current is more than 100μA, this may cause false alarms."

The PIR sensor output is an **open-drain** type:
- **Motion detected:** Output pulls HIGH (Vdd - 0.5V)
- **No motion:** Output is **open circuit** (floating)

Without a pull-down resistor, the floating output can pick up noise and cause false triggers in the ESP32 GPIO.

#### Resistor Value Calculation

**Design constraint:** Output current must not exceed 100μA (datasheet specification)

Using Ohm's Law: **R = V / I**

**For HaloSense (3.3V ESP32 system):**
```
Given:
  Vdd = 3.3V (ESP32 power rail)
  Vout (HIGH) = Vdd - 0.5V = 3.3V - 0.5V = 2.8V
  Iout (max) = 100μA (datasheet limit to prevent false alarms)

Calculate minimum resistance:
  R_min = Vout / Iout = 2.8V / 100μA = 28,000Ω = 28kΩ

Choose standard value with safety margin:
  → 33kΩ (E12/E24 series, next higher standard value)

Verify actual current with 33kΩ:
  I_actual = Vout / R = 2.8V / 33kΩ = 84.85μA ✅
  (Well within 100μA limit, 15% safety margin)
```

#### Verification: Power Dissipation

Check that power dissipation is within resistor limits:

**For 33kΩ @ 3.3V:**
```
P = V² / R = (2.8V)² / 33,000Ω = 7.84V² / 33,000Ω = 0.237mW

Result: 0.24mW << 100mW (typical 0805 SMD resistor rating)
```

Power dissipation is **negligible** - even a 1/20W (50mW) resistor would be adequate, but 1/10W (100mW) is standard for 0805 SMD.

#### Resistor Specification for BOM

**For HaloSense (3.3V ESP32 system):**

| Parameter | Specification | Notes |
|-----------|---------------|-------|
| **Resistance** | **33kΩ** | Standard E12/E24 value |
| **Tolerance** | ±5% or ±1% | 5% sufficient (±1% for tighter control) |
| **Power Rating** | 1/10W (100mW) or higher | 1/8W, 1/4W also acceptable |
| **Package (SMD)** | 0603, 0805, or 1206 | Choose based on assembly capability |
| **Package (THT)** | 1/4W axial (optional) | If through-hole assembly preferred |
| **Technology** | Thick film or thin film | Standard carbon film acceptable |
| **Temperature Coefficient** | ±100ppm/°C or better | Not critical for this application |
| **Operating Temp** | -40°C to +125°C | Match or exceed PIR sensor range (-20 to +60°C) |

**Standard values compatible with JLCPCB Basic Components:**
- **Primary choice:** 33kΩ, ±5%, 0805 SMD, 1/10W thick film
- **Alternative:** 33kΩ, ±1%, 0603 SMD, 1/10W thick film (tighter tolerance)
- **Through-hole:** 33kΩ, ±5%, 1/4W axial, carbon film (if THT assembly preferred)

#### Design Notes

1. **Resistor placement:**
   - Place resistor as close as possible to PIR sensor OUT pin
   - Minimize trace length to reduce noise pickup

2. **PCB layout:**
   - Connect resistor between OUT pin and local GND plane
   - Keep ground connection short and direct

3. **Alternative: ESP32 internal pull-down:**
   - ESP32 has internal pull-down resistors (~45kΩ typical)
   - **Not recommended** because:
     - Internal resistance varies (20kΩ-50kΩ range)
     - May be too weak for 3.3V (could allow >100μA current)
     - External resistor provides reliable, predictable value
   - If you must use internal pull-down, test thoroughly and monitor for false triggers

**Recommended for HaloSense:** **33kΩ, ±5%, 0805 SMD, 1/10W** (3.3V operation only)

## Wiring Examples

### ESP32 Connection (for HaloSense)

```
Panasonic EKMC1604111    ESP32 (3.3V)
---------------------    ------------
VDD               <----> 3.3V
GND               <----> GND
OUT               <----> GPIO Input
                         |
                         R = 33kΩ (±5%, 0805 SMD)
                         |
                        GND
```

**Circuit Details:**
- **Pull-down resistor:** 33kΩ between OUT and GND (external, on PCB)
- **Resistor specs:** 33kΩ, ±5%, 0805 SMD, 1/10W (see "Resistor Specification for BOM" above)
- **Current draw:** ~85μA when motion detected (within 100μA limit)
- **Power dissipation:** 0.24mW (negligible)

**GPIO Planning:**
- Requires 1 digital GPIO input pin
- External 33kΩ pull-down resistor required (do not rely on ESP32 internal pull-down)
- No UART/I2C required - simple digital interface
- Interrupt-driven monitoring recommended for instant response

### Recommended GPIO Configuration (ESP32)

**ESPHome YAML Example (Recommended - External 33kΩ):**
```yaml
binary_sensor:
  - platform: gpio
    pin: GPIO_PIR  # Hardware: External 33kΩ pull-down to GND on PCB
    name: "PIR Motion Detected"
    device_class: motion
    filters:
      - delayed_off: 2s  # Optional: debounce to ignore brief drops
    on_press:
      then:
        - logger.log: "Motion detected by PIR (instant trigger)"
    on_release:
      then:
        - logger.log: "Motion ended"
```

**Key points:**
- **External 33kΩ resistor on PCB** (not internal pull-down)
- Pin configured as simple input (no pull-down specified in YAML)
- `delayed_off` filter optional but recommended to prevent flicker
- Response time: <0.1s (instant trigger when entering room)

**Alternative: ESP32 Internal Pull-Down (NOT RECOMMENDED):**
```yaml
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO_PIR
      mode:
        input: true
        pulldown: true  # ESP32 internal ~45kΩ pull-down
    name: "PIR Motion Detected"
    device_class: motion
```

**Why external resistor is preferred:**
- ESP32 internal pull-down varies (20kΩ-50kΩ range)
- May allow >100μA current at 3.3V, causing false alarms
- External 33kΩ provides predictable, reliable operation
- Minimal cost (~$0.001 per resistor in volume)

## Performance Comparison: PIR vs mmWave

### EKMC1604111 (PIR) vs DFRobot C4001 (mmWave)

| Feature | EKMC1604111 PIR | C4001 mmWave |
|---------|-----------------|--------------|
| **Response Time** | <0.1s (instant) | ~1-2s (processing delay) |
| **Static Detection** | ✗ No | ✓ Yes |
| **Moving Detection** | ✓ Yes | ✓ Yes |
| **Horizontal Coverage** | 105° | 100° |
| **Vertical Coverage** | 40° (asymmetric) | 40° |
| **Detection Range** | 12m (motion) | 16m (presence), 25m (motion) |
| **Distance Measurement** | ✗ No | ✓ Yes |
| **Current Consumption** | 170μA | TBD (higher) |
| **Interface** | Digital (1 GPIO) | UART (2 GPIO + processing) |
| **Temperature Sensitivity** | ✓ Requires >4°C difference | ✓ Immune |
| **Best Use Case** | Instant motion trigger | Continuous presence monitoring |

### Complementary Operation Strategy

The EKMC1604111 PIR and C4001 mmWave sensors complement each other perfectly:

**PIR Advantages:**
- **Instant response** (<0.1s) when entering room
- **Simple interface** (1 GPIO, minimal processing)
- **Ultra-low power** (170μA)
- **Fast trigger** for immediate automation

**mmWave Advantages:**
- **Static presence detection** (person sitting/sleeping)
- **Distance measurement** (debugging, zoning)
- **Environmental immunity** (temperature, light, dust)
- **Reliable presence** (no false negatives)

**Combined Strategy:**
1. **PIR triggers instant response** - lights on immediately when entering room
2. **mmWave maintains presence** - keeps lights on while person present (even stationary)
3. **PIR detects exit motion** - faster exit detection than mmWave
4. **mmWave confirms absence** - prevents premature shutoff if person still present

## Integration Notes for HaloSense

### Mainboard Integration

**Design Approach:**
- **Integrated on mainboard** (not separate module like mmWave)
- **Top-side placement** alongside ESP32 and sensor connectors
- **Through-hole mounting** (THT assembly required)
- **Lens clearance:** Ensure 20.7mm diameter lens has unobstructed view
- **Mounting height consideration:** PCB should position sensor ~1.2-1.5m above floor for optimal wall-mount performance

### Power Considerations

- **Current consumption:** 170μA typical (standby)
- **Current during detection:** ~85μA (output through 33kΩ pull-down)
- **Total power:** 170μA × 3.3V = **0.56mW** - negligible impact on PoE power budget
- **Power rail:** ESP32 3.3V regulator output

### GPIO Planning

- **GPIO requirement:** 1 digital input pin
- **No UART conflict:** PIR uses GPIO, mmWave uses UART - fully compatible
- **Pull-down resistor:** External **33kΩ** (0805 SMD, ±5%, 1/10W) - do not use ESP32 internal pull-down
- **Interrupt-driven:** Configure GPIO interrupt for instant response

### PCB Layout Recommendations

1. **Component Placement:**
   - Position sensor where lens has clear view (no obstructions)
   - Consider sensor orientation relative to expected motion direction
   - Vertical coverage is asymmetric: aim slightly downward

2. **Electrical:**
   - **Pull-down resistor (33kΩ):**
     - Place as close as possible to PIR sensor OUT pin
     - Recommended: 0805 SMD footprint adjacent to sensor
     - Connect directly between OUT pin and local GND plane
     - Keep trace length <5mm to minimize noise pickup
   - **Power supply:**
     - Keep VDD traces clean (low noise, avoid switching noise sources)
     - Bypass capacitor (0.1μF ceramic) mandatory near VDD pin
     - Additional 10μF capacitor recommended for stability
   - **Ground connection:**
     - Connect PIR GND pin to solid ground plane
     - Use via stitching around sensor for good ground reference
   - **Signal routing:**
     - Route OUT trace to ESP32 GPIO with ground guard traces if possible
     - Keep away from high-frequency signals (UART, I2C, SPI)

3. **Mechanical:**
   - Through-hole mounting: standard PCB drill (ø0.45mm pins)
   - Pin spacing: 5.08mm P.C.D. (120° separation)
   - Allow 20.2mm height clearance above PCB
   - Lens diameter: ø20.7mm - ensure enclosure cutout

4. **Thermal:**
   - Keep away from heat-generating components (ESP32, PoE circuit)
   - Temperature stability improves detection reliability
   - >4°C difference required between target and surroundings

### Mounting and Orientation

**Wall Mounting (Optimal):**
- Height: 1.2-1.5m above floor (human mid-height)
- Orientation: Sensor lens parallel to wall, aimed slightly downward
- Horizontal coverage: 105° provides wide room coverage
- Vertical coverage: Asymmetric (-49° / +6.6°) optimized for this height

**Field of View Planning:**
- Pair with mmWave for overlapping coverage
- Both sensors have ~100-105° horizontal coverage
- Both sensors have 40° vertical coverage
- Ensures PIR instant trigger followed by mmWave presence confirmation

### ESPHome Configuration Priority

**Primary Use: Instant Motion Trigger**
- Binary sensor platform (GPIO input)
- Device class: motion
- Fast response for immediate automation

**Combined Logic Example:**
```yaml
binary_sensor:
  - platform: gpio
    pin: GPIO_PIR
    name: "PIR Motion"
    id: pir_motion
    device_class: motion

  - platform: dfrobot_c4001  # mmWave presence
    name: "mmWave Presence"
    id: mmwave_presence

  - platform: template
    name: "Room Occupancy"
    id: room_occupancy
    lambda: |-
      // Instant ON with PIR, maintain with mmWave
      if (id(pir_motion).state) return true;
      if (id(mmwave_presence).state) return true;
      return false;
```

### Testing and Calibration

1. **Warmup Period:**
   - Allow 30 seconds after power-on before testing
   - Output is undefined during warmup

2. **Detection Testing:**
   - Walk across sensor field of view (perpendicular motion)
   - Test at different distances (3m, 6m, 12m zones)
   - Verify >4°C temperature difference (room vs body temp)

3. **Response Time:**
   - Compare PIR trigger time vs mmWave trigger time
   - PIR should respond <0.1s (almost instant)
   - mmWave typically 1-2s (noticeable delay)

4. **False Positive Check:**
   - Ensure pull-down resistor properly sized
   - Monitor for spurious triggers without motion
   - Adjust resistor value if needed

## References

### Datasheets

All datasheets are available in the `datasheets/` subdirectory:
- **EKMC Series Datasheet:** Complete specifications for EKMC1601/1603/1604 models
- **EKMB/EKMC Technical Reference:** Additional technical details
- See [DATASHEETS_INDEX.md](datasheets/DATASHEETS_INDEX.md) for full listing

### Official Resources

- **Panasonic PaPIRs Website:** https://industrial.panasonic.com/ww/products/sensors/built-in-sensors/infrared-sensors/papirs
- **EKMC Series Page:** Search "EKMC1604111" on Panasonic Industrial website
- **CAD Data:** Available from Panasonic PaPIRs website (3D models, footprints)

### Related HaloSense Documentation

- **Sensor Index:** [docs/sensors/README.md](../README.md) - All sensors overview
- **mmWave Sensor:** [docs/sensors/dfrobot-c4001/README.md](../dfrobot-c4001/README.md) - Complementary sensor
- **Hardware Design:** `docs/hardware/HARDWARE_DESIGN.md` (planned) - PCB integration

## License

This documentation is part of the HaloSense project and follows the same license terms (CC BY-NC-SA 4.0).

---

**Last Updated:** 2025-11-28
**Document Version:** 1.0
**Sensor Model:** Panasonic EKMC1604111 (White, Wall Installation Type)

**Version History:**
- **v1.0 (2025-11-28):** Initial documentation created from official Panasonic EKMC series datasheet
