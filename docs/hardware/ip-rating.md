# IP Rating Guide for HaloSense

## Overview

This document explains the IP (Ingress Protection) rating system and its application to HaloSense enclosure design. Understanding IP ratings is critical for designing a sensor that can reliably operate in challenging environments like kitchens and bathrooms.

**Target IP Rating for HaloSense:** IP54 or higher
**Rationale:** Protection against dust accumulation and water splashes in humid/wet environments

## IP Rating System (IEC 60529)

The IP rating (Ingress Protection rating or International Protection rating) is an international standard defined by IEC 60529 that classifies the degree of protection provided by mechanical casings and electrical enclosures against:
- **Solid particles** (dust, dirt, debris)
- **Liquid ingress** (water, moisture)

### IP Code Format

```
IP [First Digit] [Second Digit] [Optional Letters]
   └─ Solids    └─ Liquids     └─ Additional info
```

**Example:** IP54
- **IP** = Ingress Protection
- **5** = Protected against dust (limited ingress)
- **4** = Protected against water splashes from any direction

### First Digit: Solid Particle Protection

| Digit | Protection Level | Description | Test Method |
|-------|------------------|-------------|-------------|
| **0** | No protection | No special protection | — |
| **1** | >50mm objects | Protected against large objects (back of hand) | 50mm diameter probe |
| **2** | >12.5mm objects | Protected against fingers or similar objects | 12.5mm diameter probe |
| **3** | >2.5mm objects | Protected against tools, thick wires, etc. | 2.5mm diameter probe |
| **4** | >1mm objects | Protected against most wires, screws, large ants | 1mm diameter probe |
| **5** | **Dust protected** | **Limited dust ingress (no harmful deposit)** | **Dust chamber test** |
| **6** | Dust tight | Total protection against dust ingress | Vacuum chamber test |

**Notes:**
- **Level 5 (Dust Protected):** Some dust may enter, but not enough to interfere with operation
- **Level 6 (Dust Tight):** No dust ingress whatsoever (requires sealed enclosure with gaskets)

### Second Digit: Liquid Ingress Protection

| Digit | Protection Level | Description | Test Method |
|-------|------------------|-------------|-------------|
| **0** | No protection | No special protection | — |
| **1** | Dripping water (vertical) | Protection against vertically falling drops | 1mm/min for 10 min |
| **2** | Dripping water (15° tilt) | Protection against dripping water when tilted 15° | 3mm/min for 10 min |
| **3** | Spraying water | Protection against water spray up to 60° from vertical | Spray nozzle, 10 L/min |
| **4** | **Splashing water** | **Protection against water splashes from any direction** | **Spray nozzle, any angle** |
| **5** | Water jets | Protection against low-pressure water jets | 12.5 L/min @ 30 kPa |
| **6** | Powerful water jets | Protection against powerful water jets | 100 L/min @ 100 kPa |
| **7** | Immersion up to 1m | Protection against temporary immersion (30 min) | 1m depth for 30 min |
| **8** | Immersion beyond 1m | Protection against continuous immersion | Manufacturer specified |
| **9K** | High-pressure/high-temp jets | Protection against high-pressure, high-temperature water jets | 80°C, 8-10 MPa |

**Notes:**
- **Level 4 (Splash Water):** Water splashing from any direction shall not harm the device
- **Level 5+ (Jets/Immersion):** Not required for HaloSense (indoor sensor, not outdoor/industrial)

### Common IP Ratings Explained

| IP Rating | Solid Protection | Liquid Protection | Typical Applications |
|-----------|------------------|-------------------|----------------------|
| **IP20** | Finger-safe | No liquid protection | Indoor electronics (PC cases, power supplies) |
| **IP40** | Wire/tool protection | No liquid protection | Indoor appliances |
| **IP44** | Wire/tool protection | Splash water | Outdoor lights, bathroom fixtures |
| **IP54** | **Dust protected** | **Splash water** | **Kitchen/bathroom sensors, outdoor enclosures** |
| **IP65** | Dust tight | Water jets | Outdoor sensors, industrial equipment |
| **IP67** | Dust tight | Temporary immersion | Smartphones, outdoor cameras |
| **IP68** | Dust tight | Continuous immersion | Underwater devices, submersible sensors |

## HaloSense IP54 Target Rating

### Why IP54?

**IP54** provides the optimal balance of protection and manufacturability for HaloSense:

#### First Digit: IP**5**4 (Dust Protected)

**Protection:**
- Limited dust ingress (small amounts may enter but not enough to harm operation)
- Suitable for kitchens (cooking fumes, flour dust, steam particulates)
- Suitable for bathrooms (lint, dust, moisture-borne particles)

**Design Requirements:**
- Enclosure seams should minimize gaps (not hermetically sealed)
- Sensor windows must allow function while blocking dust accumulation
- Internal PCB coating recommended (conformal coating for moisture/dust resistance)

**Trade-off vs IP6X:**
- IP6X (dust tight) requires complete sealing with gaskets → more expensive, harder to service
- IP5X (dust protected) allows slight air exchange → better for sensors requiring airflow/ventilation
- HaloSense sensors (mmWave, PIR, light) don't require hermetic sealing

#### Second Digit: IP5**4** (Splash Water Protected)

**Protection:**
- Water splashing from any direction cannot harm the device
- Suitable for kitchens (sink splashes, boiling water condensation, spills)
- Suitable for bathrooms (shower overspray, sink splashes, high humidity)

**Design Requirements:**
- Water cannot pool on top of enclosure (sloped/curved top surface)
- Drainage paths for any water that enters (weep holes at bottom)
- Sealed cable entry points (Ethernet/USB-C connectors)
- Sensor windows designed to shed water (hydrophobic coating optional)

**Trade-off vs IP5X (higher second digits):**
- IPX5 (water jets) requires protection against 12.5 L/min streams → overkill for indoor sensor
- IPX4 (splash water) is sufficient for indoor wet environments
- No submersion expected (IPX7/IPX8 not needed)

### IP54 vs Higher Ratings

| Consideration | IP54 | IP65 | IP67 | Recommendation |
|---------------|------|------|------|----------------|
| Dust protection | Limited ingress | Dust tight | Dust tight | IP54 sufficient |
| Water protection | Splash resistant | Jet resistant | Immersion resistant | IP54 sufficient |
| Enclosure complexity | Simple seams | Gaskets required | Full sealing | IP54 easier to manufacture |
| Serviceability | Easy to open | Harder to service | Difficult to service | IP54 better for DIY |
| Cost | Low | Medium | High | IP54 cost-effective |
| Kitchen/bathroom use | ✓ Excellent | ✓ Overkill | ✓ Overkill | IP54 optimal |
| Outdoor use | ✗ Limited | ✓ Good | ✓ Excellent | IP54 indoor only |

**Conclusion:** IP54 is the **optimal rating** for HaloSense. Higher ratings (IP65+) provide no additional benefit for indoor sensors and increase manufacturing complexity.

## Component MSL Rating Correlation

### MSL (Moisture Sensitivity Level) Overview

**MSL Rating (JEDEC J-STD-020)** defines how long a component can be exposed to ambient conditions (30°C/60% RH) after opening the moisture barrier bag, before reflow soldering:

| MSL Level | Floor Life | Conditions | Typical Components |
|-----------|------------|------------|-------------------|
| MSL 1 | Unlimited | 30°C/85% RH | Ceramic resistors, capacitors |
| MSL 2 | 1 year | 30°C/60% RH | Most SMD components |
| **MSL 3** | **168 hours (7 days)** | **30°C/60% RH** | **BH1750, C4001, EKMC1604111** |
| MSL 4 | 72 hours (3 days) | 30°C/60% RH | VEML6030, VEML7700 (rejected) |
| MSL 5 | 48 hours (2 days) | 30°C/60% RH | BGAs, fine-pitch ICs |
| MSL 6 | 6 hours | 30°C/60% RH | Highly moisture-sensitive ICs |

### HaloSense Component Selection for MSL 3 Uniformity

**All HaloSense sensors are MSL 3:**

| Component | Model | MSL Rating | Rationale |
|-----------|-------|------------|-----------|
| mmWave Radar | DFRobot C4001 | MSL 3 | 24GHz RF module, moisture-sensitive antenna |
| PIR Sensor | Panasonic EKMC1604111 | MSL 3 | Optical lens and pyroelectric element |
| **Light Sensor** | **ROHM BH1750FVI** | **MSL 3** | **Selected for MSL uniformity** |
| ~~Alternative~~ | ~~VEML6030~~ | ~~MSL 4~~ | ~~Rejected for inconsistent MSL rating~~ |

**Design Decision:**
- Uniform MSL 3 components → better long-term moisture resistance in kitchen/bathroom installations
- BH1750 (MSL 3, 120μA) chosen over VEML6030 (MSL 4, 13μA) despite 10× higher power
- Power penalty negligible (0.4mW vs 0.04mW in a ~1300mW system)

**MSL Rating ≠ IP Rating:**
- **MSL:** Component moisture sensitivity during **assembly/storage** (before potting/enclosure)
- **IP Rating:** Device ingress protection during **operation** (after assembly in enclosure)
- Both must be considered for reliable kitchen/bathroom deployment

## HaloSense Enclosure Design Requirements

### IP54 Design Checklist

#### Enclosure Geometry

- [ ] **Top surface sloped or curved** (no horizontal surfaces where water can pool)
- [ ] **Smooth exterior** (no crevices where dust/water can accumulate)
- [ ] **Cable entry from bottom or side** (not from top where water can run in)
- [ ] **Weep holes at lowest point** (allow condensation drainage, 1-2mm diameter)

#### Sealing Strategy

- [ ] **Close-fitting seams** (0.5mm max gap, no gaskets required for IP54)
- [ ] **Snap-fit or screw assembly** with overlapping edges (labyrinth seal design)
- [ ] **Sensor windows recessed** (protects PIR/light sensors from direct splashes)
- [ ] **mmWave sensor window flush** (allows radar signal passage, water-shedding surface)

#### Material Selection

- [ ] **Enclosure:** ABS, PETG, or ASA plastic (3D printable, moisture-resistant)
- [ ] **Sensor windows:** Polycarbonate or acrylic (clear for light sensor, opaque/printed for PIR)
- [ ] **Gaskets (if used):** Silicone or EPDM rubber (kitchen/bathroom safe)
- [ ] **Fasteners:** Stainless steel (corrosion-resistant in humid environments)

#### PCB Protection

- [ ] **Conformal coating:** Acrylic or silicone coating on PCB (prevents moisture/dust damage)
- [ ] **Elevated mounting:** PCB standoffs (keeps board away from any water ingress at bottom)
- [ ] **Component orientation:** Connectors facing down or sideways (not upward where water can enter)

#### Connector Sealing

- [ ] **Ethernet (RJ45):** Vertical connector with dust cover or recessed housing
- [ ] **USB-C:** Vertical connector with dust cover or recessed housing
- [ ] **Cable strain relief:** Prevents water wicking along cable into enclosure

### IP54 Testing Procedure (DIY/Prototyping)

#### Dust Protection Test (First Digit: 5)

**Equipment:**
- Talcum powder or flour (simulates fine dust)
- Vacuum cleaner (simulates airflow carrying dust)

**Procedure:**
1. Assemble HaloSense in enclosure (fully sealed)
2. Place in cardboard box with 100g talcum powder
3. Shake box vigorously for 5 minutes
4. Use vacuum cleaner to create airflow over enclosure for 5 minutes
5. Open enclosure and inspect interior
6. **Pass criteria:** Minimal dust on PCB, no dust in sensor cavities, device operates normally

**Note:** This is a simplified test. Official IP5X testing requires a dust chamber with 2kg/m³ talc circulation for 8 hours.

#### Water Splash Test (Second Digit: 4)

**Equipment:**
- Spray bottle (mist setting)
- 500mL water
- Towel (to dry enclosure exterior)

**Procedure:**
1. Assemble HaloSense in enclosure (fully sealed, device powered on)
2. Spray water from all directions (top, sides, bottom, angled)
   - Distance: 30-50cm from enclosure
   - Duration: 10 minutes total (2 minutes per direction)
   - Volume: 500mL water total
3. Wipe exterior dry with towel
4. Open enclosure and inspect interior
5. **Pass criteria:** No water on PCB, no water in sensor cavities, device still operates, no electrical short

**Note:** This is a simplified test. Official IPX4 testing uses a spray nozzle with 10 L/min for 5 minutes from every direction.

### Maintenance and Long-Term Protection

#### Cleaning Recommendations

**Exterior:**
- Wipe with damp cloth (mild soap solution if needed)
- Avoid abrasive cleaners (can scratch sensor windows)
- Dry thoroughly after cleaning

**Interior (annual maintenance):**
- Open enclosure and inspect for dust accumulation
- Gently blow out dust with compressed air (low pressure)
- Inspect PCB for signs of corrosion or moisture damage
- Re-apply conformal coating if damaged (rare)

#### Installation Best Practices

**Kitchen Installation:**
- Mount away from direct steam sources (stovetop, kettle)
- Avoid mounting above sink where splashes are most frequent
- Ceiling mount preferred over wall mount (reduces splash exposure)

**Bathroom Installation:**
- Mount outside shower spray zone (1.5m+ from showerhead)
- Ceiling mount preferred over wall mount
- Ensure adequate ventilation (reduces long-term condensation buildup)

## Regulatory and Standards Compliance

### Relevant Standards

| Standard | Title | Relevance to HaloSense |
|----------|-------|------------------------|
| **IEC 60529** | Degrees of Protection (IP Code) | **Primary standard for IP rating** |
| IEC 60950-1 | IT Equipment Safety | General electrical safety (replaced by IEC 62368-1) |
| IEC 62368-1 | Audio/Video/ICT Equipment Safety | Modern safety standard for HaloSense class devices |
| EN 55032 | Electromagnetic Compatibility (Emissions) | EMC compliance for CE marking |
| EN 55035 | Electromagnetic Compatibility (Immunity) | EMC compliance for CE marking |

### Certification Considerations

**For DIY/Open Source Project:**
- IP rating testing can be performed in-house (see testing procedures above)
- No formal certification required for personal use
- Document test results for community validation

**For Commercial/Production:**
- Official IP54 certification requires third-party testing lab
- Test reports required for CE marking documentation
- Estimated cost: $500-2000 per enclosure variant (IP testing + report)

## Comparison: HaloSense IP54 vs Common Devices

| Device | IP Rating | Environment | Notes |
|--------|-----------|-------------|-------|
| **HaloSense (target)** | **IP54** | **Kitchen/bathroom** | **Dust + splash water** |
| iPhone 15 Pro | IP68 | Outdoor, submersible | Overkill for indoor sensor |
| Nest Thermostat | IP20 | Indoor dry | Insufficient for kitchen/bathroom |
| Philips Hue Motion Sensor | IP42 | Indoor, light splash | Marginal for bathroom |
| Aqara Motion Sensor P1 | IP44 | Indoor, splash resistant | Similar to HaloSense target |
| Fibaro Motion Sensor | IP44 | Indoor, splash resistant | Similar to HaloSense target |
| Outdoor security camera | IP65-IP67 | Outdoor, weatherproof | Overdesigned for HaloSense use case |

**Conclusion:** IP54 positions HaloSense between standard indoor sensors (IP20-IP42) and outdoor/industrial sensors (IP65+), making it **ideal for kitchen/bathroom deployment**.

## Summary and Recommendations

### Key Takeaways

1. **IP54 is optimal for HaloSense:**
   - First digit 5 (dust protected) prevents dust accumulation in kitchens/bathrooms
   - Second digit 4 (splash water) protects against sink/shower splashes
   - Balanced protection without overengineering

2. **Component selection supports IP54 enclosure:**
   - All sensors are MSL 3 (better moisture handling than MSL 4)
   - Conformal coating on PCB adds additional moisture protection
   - No hermetically sealed components required

3. **Enclosure design priorities:**
   - Water-shedding geometry (sloped/curved surfaces)
   - Labyrinth seals (overlapping edges, no gaskets required)
   - Recessed sensor windows (protect optics from splashes)
   - Bottom drainage (weep holes for any condensation)

4. **Testing can be DIY:**
   - Simplified dust test (talcum powder + vacuum)
   - Simplified water test (spray bottle from all directions)
   - No expensive equipment required for prototyping validation

5. **IP54 does not mean waterproof:**
   - Not suitable for direct water jets (IPX5+)
   - Not suitable for submersion (IPX7+)
   - Not suitable for outdoor rain exposure (IP65+ recommended)
   - **Perfect for:** Indoor kitchens and bathrooms with normal use

### Design Action Items

- [ ] Design enclosure with IP54 compliance in mind (see checklist above)
- [ ] Create 3D printable prototype and perform DIY IP testing
- [ ] Document test results (photos, videos, measurements)
- [ ] Apply conformal coating to prototype PCBs
- [ ] Iterate enclosure design based on test failures
- [ ] Consider future: Official IP54 certification if commercializing

---

**Document Version:** 1.0
**Last Updated:** 2025-11-29
**Author:** HaloSense Development Team

**References:**
- IEC 60529:2013 (Degrees of protection provided by enclosures - IP Code)
- JEDEC J-STD-020 (Moisture/Reflow Sensitivity Classification for Nonhermetic Solid State Surface Mount Devices)
- HaloSense Power Budget Analysis (`power-budget.md`)

**Revision History:**
- **v1.0 (2025-11-29):** Initial IP rating documentation with IP54 target specification
