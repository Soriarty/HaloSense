# HaloSense Power Budget Analysis

## Overview

This document provides a comprehensive power consumption analysis for the HaloSense presence sensor. The device is designed to operate on IEEE 802.3af PoE (Power over Ethernet), with USB-C as an alternative power source.

**Target Power Consumption:** ≤5W typical operation
**Available PoE Power:** 15.4W (IEEE 802.3af Class 0)
**Design Margin:** 3× safety factor (15.4W available ÷ 5W target)

## PoE Power Delivery Standards

HaloSense is designed for IEEE 802.3af PoE compatibility:

| Standard | Power at PSE | Power at PD | Voltage | Class | Notes |
|----------|--------------|-------------|---------|-------|-------|
| **802.3af (PoE)** | **15.4W** | **12.95W** | 44-57V | 0-3 | **HaloSense target** |
| 802.3at (PoE+) | 30W | 25.5W | 50-57V | 4 | Future expansion headroom |
| 802.3bt Type 3 | 60W | 51W | 50-57V | 5-6 | Not required |
| 802.3bt Type 4 | 100W | 71W | 50-57V | 7-8 | Not required |

**Key Points:**
- **PSE (Power Sourcing Equipment):** PoE switch/injector output power
- **PD (Powered Device):** Power available at HaloSense after cable losses
- **Cable Loss:** Up to 2.45W over 100m Cat5e/Cat6 cable
- **HaloSense assumes:** ~13-14W usable power at device (conservative estimate accounting for real-world cable losses)

## Component Power Consumption Breakdown

### 1. ESP32 Microcontroller

**Model:** ESP32-WROOM-32E (based on OLIMEX ESP32-POE design)

| Operating Mode | Current @ 3.3V | Power | Notes |
|----------------|----------------|-------|-------|
| Active (WiFi TX) | 160-200mA | 528-660mW | Peak WiFi transmission |
| Active (WiFi RX) | 95-100mA | 313-330mW | WiFi receiving |
| **Typical (Ethernet)** | **50-100mA** | **165-330mW** | **Normal operation without WiFi** |
| Modem-sleep | 20-40mA | 66-132mW | Periodic wakeup |
| Light-sleep | 0.8-1.0mA | 2.6-3.3mW | Deep sleep with peripheral power |
| Deep-sleep | 10-150μA | 0.033-0.495mW | Ultra-low power standby |

**HaloSense Operating Mode:**
- **Primary:** Ethernet connectivity (WiFi disabled)
- **Typical consumption:** 100mA @ 3.3V = **330mW**
- **Worst case:** 200mA @ 3.3V = **660mW** (WiFi fallback mode active)

**Source:** ESP32 Datasheet (Espressif Systems)

### 2. Ethernet PHY (LAN8720A)

**Model:** LAN8720A/LAN8720Ai (Microchip/SMSC)

| Operating Mode | Current @ 3.3V | Power | Notes |
|----------------|----------------|-------|-------|
| Active (100Mbps) | 60-80mA | 198-264mW | Full-duplex operation |
| Active (10Mbps) | 45-60mA | 148-198mW | Reduced speed |
| **Typical** | **60mA** | **198mW** | **Normal operation** |
| Power-down | <1μA | <0.003mW | Disabled state |

**HaloSense Operating Mode:**
- **Primary:** 100Mbps full-duplex for Home Assistant communication
- **Typical consumption:** 60mA @ 3.3V = **198mW**
- **Worst case:** 80mA @ 3.3V = **264mW**

**Source:** LAN8720A Datasheet (Microchip Technology)

### 3. mmWave Radar Sensor (DFRobot C4001)

**Model:** DFRobot SEN0609 (24GHz FMCW radar)

| Operating Mode | Current @ 3.3V | Power | Notes |
|----------------|----------------|-------|-------|
| **Active (estimated)** | **50-100mA** | **165-330mW** | **Continuous presence detection** |
| Standby | Unknown | TBD | Not documented |

**Estimation Methodology:**
- DFRobot does not publish official power consumption specifications
- Estimated based on similar 24GHz mmWave sensors:
  - HLK-LD2410: 79mA @ 5V (typical)
  - HLK-LD2450: 120mA @ 5V (typical)
  - HLK-LD2410B: 50mA @ 5V (typical)
- Conservative estimate: 50-100mA @ 3.3V for 24GHz FMCW operation

**HaloSense Operating Mode:**
- **Primary:** Continuous presence detection (always active)
- **Typical consumption:** 75mA @ 3.3V = **248mW** (midpoint estimate)
- **Worst case:** 100mA @ 3.3V = **330mW**

**Action Required:** Measure actual consumption during prototyping phase

**Source:** Estimated from comparable mmWave sensors (LD2410, LD2450, LD2410B datasheets)

### 4. PIR Motion Sensor (Panasonic EKMC1604111)

**Model:** Panasonic EKMC1604111 (PaPIRs wall installation type)

| Operating Mode | Current @ 3.3V | Power | Notes |
|----------------|----------------|-------|-------|
| **Standby** | **0.17mA** | **0.56mW** | **Continuous monitoring** |
| Detection active | 0.17mA | 0.56mW | Same as standby (passive sensor) |

**HaloSense Operating Mode:**
- **Primary:** Continuous passive infrared monitoring
- **Consumption:** 0.17mA @ 3.3V = **0.56mW**
- **Notes:** Passive sensor with minimal power requirements

**Source:** EKMC Series Datasheet (Panasonic Industrial Devices)
**Reference:** `/docs/sensors/panasonic-ekmc1604111/EKMC1604111_TECHNICAL_GUIDE.md`

### 5. Ambient Light Sensor (ROHM BH1750FVI)

**Model:** ROHM BH1750FVI (Digital 16-bit I2C light sensor)

| Operating Mode | Current @ 3.3V | Power | Notes |
|----------------|----------------|-------|-------|
| **Active (Continuous H-Resolution)** | **120μA** | **0.40mW** | **Normal measurement mode** |
| Active @ 100lx typical | 120μA | 0.40mW | Datasheet typical condition |
| Active (One-Time) | 120μA (burst) | 0.40mW | Single measurement then power-down |
| Power-down | 0.01μA | 0.000033mW | I2C Power_Down command |

**HaloSense Operating Mode:**
- **Primary:** Continuous H-Resolution Mode (1 lx resolution)
- **Measurement interval:** 60 seconds (configurable in ESPHome)
- **Consumption:** 120μA @ 3.3V = **0.40mW**
- **Notes:** Can be power-cycled between measurements for even lower power

**Trade-off vs VEML6030:**
- BH1750: 120μA, MSL 3 rating (better moisture handling)
- VEML6030: 13μA, MSL 4 rating (worse moisture handling)
- **Decision:** Chose BH1750 for uniform MSL 3 components across board
- **Impact:** +107μA (~0.35mW additional power) - negligible

**Source:** BH1750FVI Datasheet (ROHM Semiconductor)
**Reference:** `/docs/sensors/rohm-bh1750/BH1750_TECHNICAL_GUIDE.md`

### 6. Supporting Components

**Additional power consumers:**

| Component | Current @ Voltage | Power | Notes |
|-----------|-------------------|-------|-------|
| Status LED | 2-5mA @ 3.3V | 6.6-16.5mW | GPIO-controlled, can be disabled |
| Pull-up/down resistors | <0.1mA total | <0.33mW | I2C, GPIO, configuration pins |
| Voltage regulators (quiescent) | 5-10mA @ various | 16-50mW | LDO efficiency losses |
| PoE module (isolation transformer) | — | ~500mW | IEEE 802.3af module efficiency loss |

**Typical total:** ~50-100mW
**Notes:** Most supporting components have negligible power impact

## Total Power Budget Summary

### Typical Operating Scenario

**Configuration:** Ethernet connectivity, continuous presence detection, 60s light sensor updates

| Component | Current @ 3.3V | Power (mW) | Percentage |
|-----------|----------------|------------|------------|
| ESP32 (Ethernet active) | 100mA | 330 | 43.7% |
| LAN8720A PHY | 60mA | 198 | 26.2% |
| DFRobot C4001 mmWave | 75mA | 248 | 32.8% |
| Panasonic EKMC1604111 PIR | 0.17mA | 0.56 | 0.07% |
| ROHM BH1750FVI Light | 0.12mA | 0.40 | 0.05% |
| Supporting components | — | 50 | 6.6% |
| **Total (3.3V rail)** | **~235mA** | **~777mW** | — |
| **PoE module losses** | — | **~500mW** | — |
| **Total System Power** | — | **~1,280mW** | — |

**Rounded total:** **~1.3W typical**
**Available PoE power:** 15.4W (PSE) → ~13W (PD, after cable losses)
**Design margin:** **10× safety factor**

### Worst-Case Operating Scenario

**Configuration:** WiFi fallback active, continuous detection, all components at maximum ratings

| Component | Current @ 3.3V | Power (mW) | Percentage |
|-----------|----------------|------------|------------|
| ESP32 (WiFi TX peak) | 200mA | 660 | 50.5% |
| LAN8720A PHY | 80mA | 264 | 20.2% |
| DFRobot C4001 mmWave | 100mA | 330 | 25.2% |
| Panasonic EKMC1604111 PIR | 0.17mA | 0.56 | 0.04% |
| ROHM BH1750FVI Light | 0.12mA | 0.40 | 0.03% |
| Supporting components | — | 100 | 7.6% |
| **Total (3.3V rail)** | **~380mA** | **~1,255mW** | — |
| **PoE module losses** | — | **~500mW** | — |
| **Total System Power** | — | **~1,755mW** | — |

**Rounded total:** **~1.8W worst case**
**Available PoE power:** ~13W (PD)
**Design margin:** **7.2× safety factor**

### USB-C Power Scenario

**Configuration:** USB-C 5V/2A power supply (10W available)

| Component | Voltage | Current | Power | Notes |
|-----------|---------|---------|-------|-------|
| 3.3V rail (from 5V regulator) | 3.3V | 235-380mA | 777-1,255mW | See typical/worst case above |
| Regulator efficiency loss (~85%) | — | — | 137-221mW | LDO or buck converter losses |
| **Total USB-C draw** | **5V** | **~183-295mA** | **~915-1,476mW** | — |

**Rounded total:** **~0.9-1.5W from USB-C**
**Available USB-C power:** 10W (5V/2A supply)
**Design margin:** **6.7-11× safety factor**

## Power Mode Comparison

| Power Source | Typical Power | Worst-Case Power | Available Power | Margin |
|--------------|---------------|------------------|-----------------|--------|
| **PoE (802.3af)** | **1.3W** | **1.8W** | **13W** | **7-10×** |
| **USB-C (5V/2A)** | **0.9W** | **1.5W** | **10W** | **6.7-11×** |
| **USB-C (5V/1A)** | 0.9W | 1.5W | 5W | 3.3-5.5× |

**Recommendation:** Both PoE and USB-C (5V/2A) provide excellent power margin. Minimum USB-C specification: 5V/1A (5W).

## Component Selection Rationale

### MSL Rating vs Power Trade-off (Light Sensor)

**Options considered:**

| Sensor | Power | MSL Rating | JLCPCB | Decision |
|--------|-------|------------|--------|----------|
| **BH1750FVI** | **0.40mW** | **MSL 3** | **C78960** | **Selected** |
| VEML6030 | 0.04mW | MSL 4 | C132182 | Rejected |
| VEML7700 | 0.16mW | MSL 4 | C1850416 | Rejected |
| TSL2591 | 1.00mW | Unknown | C176812 | Rejected |

**Decision Driver:**
- Uniform MSL 3 components across entire board (C4001 mmWave: MSL 3, EKMC1604111 PIR: MSL 3)
- Better moisture handling for kitchen/bathroom installations (IP54 enclosure + MSL 3 components)
- Power penalty: +0.36mW (BH1750 0.40mW - VEML6030 0.04mW) = **negligible** in ~1.3W system
- Proven ESPHome support, simple operation, excellent availability

**MSL Rating Impact:**
- MSL 3: 168 hours @ 30°C/60%RH after bag opening (JEDEC J-STD-020)
- MSL 4: 72 hours @ 30°C/60%RH after bag opening
- HaloSense target: Kitchen/bathroom with IP54+ enclosure → MSL 3 preferred

## Power Efficiency Opportunities

### Current Configuration (Baseline)

- ESP32 running full-speed with Ethernet
- mmWave radar in continuous detection mode
- PIR sensor always monitoring (passive, minimal power)
- Light sensor: continuous 60s interval measurements
- Status LED enabled

### Optimization Options (Future Considerations)

#### 1. ESP32 Power Optimization
- **Modem-sleep mode:** Reduce WiFi power when Ethernet is active → Save ~50-150mW
- **CPU frequency scaling:** 80MHz instead of 240MHz when idle → Save ~50-100mW
- **Disable WiFi radio completely:** When Ethernet is stable → Save ~100-200mW
- **Implementation:** ESPHome `wifi.enable_on_boot: false`

#### 2. Light Sensor Power Cycling
- **Current:** Continuous H-Resolution Mode (120μA)
- **Alternative:** One-Time Measurement + Power-Down between readings
- **Savings:** ~0.3mW (negligible, not worth implementation complexity)

#### 3. Status LED Management
- **Current:** Always on or blinking
- **Alternative:** Disable after initialization, enable only on errors
- **Savings:** 6-16mW (~0.5-1% of total)

#### 4. Dynamic Sensor Management
- **Scenario:** Disable mmWave during known occupancy (very advanced)
- **Savings:** ~250-330mW (20-25% of total)
- **Complexity:** High, may reduce reliability

**Recommendation:** Current power consumption (1.3W typical) is excellent. Optimizations are **not necessary** for PoE operation. Focus on reliability over micro-optimization.

## PoE Module Design Considerations

### Recommended PoE Controller

**Suggested IC:** Texas Instruments TPS23753A or TPS23754
**Alternative:** Microchip LTC4267, Silvertel Ag9900M (integrated module)

**Key Features Required:**
- IEEE 802.3af Class 0 compliance (15.4W PSE)
- Integrated DC/DC converter or external FET driver
- Under-voltage lockout (UVLO)
- Over-current protection (OCP)
- Thermal shutdown
- 3.3V regulated output @ 500mA minimum

### Power Supply Rail Design

| Rail | Voltage | Max Current | Regulation | Use Case |
|------|---------|-------------|------------|----------|
| **3.3V Main** | 3.3V ±5% | 500mA | Buck converter from PoE | ESP32, PHY, sensors |
| **5V Sensor** | 5V ±5% | 200mA | Buck converter from PoE | Optional 5V sensors (future) |

**Current Design:** Single 3.3V rail powers all components (BH1750, EKMC1604111, C4001 all support 3.3V operation)

### Inrush Current Limiting

- PoE standard requires controlled startup (IEEE 802.3af classification signature)
- TPS23753A/TPS23754 handles classification automatically
- No additional inrush limiting components required

## Measurement and Validation Plan

### Prototyping Phase Measurements

**Required measurements:**

1. **C4001 mmWave Power Consumption**
   - Measure actual current draw in presence detection mode
   - Verify against 50-100mA estimate
   - Test at various detection ranges and sensitivities

2. **ESP32 Baseline Current**
   - Measure with Ethernet active, WiFi disabled
   - Measure with WiFi fallback active
   - Verify against 50-200mA range

3. **Total System Power**
   - Measure at PoE input (before transformer)
   - Measure at 3.3V rail (after regulation)
   - Calculate PoE module efficiency

4. **Thermal Performance**
   - Measure component temperatures at maximum power
   - Verify thermal margin for 40°C ambient (worst-case installation)

### Testing Equipment

- **Current measurement:** Multimeter (±0.1mA accuracy) or INA219 current sensor
- **Power measurement:** USB power meter (for USB-C testing) or PoE power meter
- **Thermal measurement:** IR thermometer or thermal camera
- **Duration:** 24-hour burn-in test at maximum power

### Acceptance Criteria

- ✓ Total system power ≤ 2W typical operation
- ✓ Total system power ≤ 3W worst-case operation
- ✓ No component exceeds 70°C @ 25°C ambient
- ✓ No component exceeds 85°C @ 40°C ambient (outdoor installation)
- ✓ PoE negotiation successful (IEEE 802.3af signature detection)
- ✓ 24-hour continuous operation without thermal issues

## Conclusion

**HaloSense power budget is excellent:**

- **Typical operation:** 1.3W (8.5% of PoE capacity)
- **Worst-case operation:** 1.8W (11.7% of PoE capacity)
- **Design margin:** 7-10× safety factor
- **Component selection:** Optimized for reliability (MSL 3 uniform rating) over micro-watt savings

**Key advantages:**

1. **Massive headroom:** 13W available vs 1.3W used = room for future expansion
2. **Reliable power delivery:** PoE provides stable, isolated power without USB cables
3. **Flexible deployment:** Both PoE and USB-C support with excellent margins
4. **Thermal safety:** Low power dissipation ensures cool operation even in enclosed spaces
5. **MSL 3 uniform components:** Better moisture handling for kitchen/bathroom installations

**No power optimization required.** Current design is robust and production-ready from a power perspective.

---

## Navigation

← **[Hardware Documentation](README.md)** | **[Sensors](../sensors/README.md)** | **[Development](../development/README.md)** | **[Main README](../../README.md)**

---

**Document Version:** 1.0
**Last Updated:** 2025-11-29
**Author:** HaloSense Development Team

**Revision History:**
- **v1.0 (2025-11-29):** Initial power budget analysis with BH1750 light sensor selection
