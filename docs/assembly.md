# HaloSense Assembly Guide

Step-by-step instructions for building your HaloSense presence sensor.

## 🚧 Work in Progress

Assembly guide will be completed after hardware and enclosure designs are finalized.

## Overview

This guide covers the complete assembly process from bare components to finished device.

**Estimated Assembly Time:** 2-4 hours (first build)

**Skill Level Required:**
- Basic soldering (if assembling from components)
- Familiarity with electronics
- 3D printer operation (or access to printing service)

---

## Prerequisites

### Tools Required

**Essential:**
- Soldering iron (temperature controlled, 60W+ recommended)
- Solder (lead-free or leaded, 0.8mm diameter)
- Flush cutters
- Small Phillips screwdriver
- Multimeter
- USB-C cable for programming
- Computer with ESPHome installed

**Recommended:**
- Soldering flux
- Desoldering wick/pump
- Tweezers (fine tip)
- Magnifying glass/helping hands
- ESD mat and wrist strap
- Wire strippers (if making custom cables)
- Heat gun (for heat shrink)

**Nice to Have:**
- Solder fume extractor
- PCB holder/vice
- Hot air station (for SMD rework)
- Digital caliper

### Components Needed

Refer to [BOM (Bill of Materials)](bom.md) for complete list.

**Quick Checklist:**
- [ ] HaloSense PCB (fabricated)
- [ ] All components (see BOM)
- [ ] 3D printed enclosure parts
- [ ] Mounting hardware (screws, spacers)
- [ ] Cables (Ethernet and/or USB-C)

---

## Assembly Steps

### Phase 1: PCB Assembly

*Detailed instructions pending hardware design completion*

#### Step 1.1: Inspect PCB
- Check for manufacturing defects
- Verify all traces and pads are intact
- Confirm board dimensions match design

#### Step 1.2: Solder Surface Mount Components (SMD)
**Order:** Smallest to largest components

1. **Resistors and capacitors (0603)**
   - Apply flux to pads
   - Use tweezers to place component
   - Solder one pad, then the other
   - Inspect for bridges

2. **Integrated circuits (if SMD)**
   - Check orientation carefully (pin 1 marking)
   - Tack opposite corners first
   - Solder all pins
   - Check for shorts with multimeter

3. **Inductors and larger passives**
   - Follow manufacturer polarity if applicable
   - Ensure good thermal connection

#### Step 1.3: Solder Through-Hole Components
**Order:** Low profile to tall components

1. **ESP32 module**
   - Align carefully (check pin 1)
   - Solder corner pins first
   - Solder remaining pins
   - Inspect for cold joints

2. **Connectors**
   - RJ45 Ethernet jack
   - USB-C connector
   - Sensor headers/connectors

3. **Power components**
   - PoE module (if through-hole)
   - Voltage regulators
   - Terminal blocks (if used)

#### Step 1.4: Component Testing
- Visual inspection for solder bridges
- Continuity test for shorts
- Resistance check on power rails
- Test voltages before connecting sensors

### Phase 2: Sensor Integration

#### Step 2.1: DFRobot C4001 mmWave Radar
1. Connect to UART pins (TX, RX, VCC, GND)
2. Verify baud rate configuration (115200)
3. Test with serial monitor before enclosing
4. Document which GPIO pins are used

#### Step 2.2: PIR Motion Sensor
*Instructions TBD after component selection*

#### Step 2.3: Ambient Light Sensor
*Instructions TBD after component selection*

### Phase 3: Initial Testing

#### Step 3.1: Power-On Test
1. Connect USB-C power (5V/2A adapter)
2. Check for:
   - Status LED illumination
   - No smoke or burning smell
   - No excessive heat
3. Measure voltages:
   - 5V rail
   - 3.3V rail
   - Sensor power

#### Step 3.2: Firmware Upload
1. Connect to computer via USB-C
2. Flash ESPHome firmware ([see firmware guide](../firmware/FIRMWARE_GUIDE.md))
3. Monitor serial output for errors
4. Verify WiFi/Ethernet connectivity

#### Step 3.3: Sensor Verification
1. Check sensor detection in ESPHome logs
2. Test mmWave presence detection
3. Verify PIR motion detection
4. Test light sensor readings
5. Confirm data updates in Home Assistant

### Phase 4: Enclosure Assembly

*Detailed instructions pending enclosure design completion*

#### Step 4.1: Prepare Enclosure
1. Clean 3D printed parts
2. Remove support material if any
3. Test fit all components
4. Drill or enlarge holes if needed

#### Step 4.2: PCB Installation
1. Install M3 spacers in enclosure
2. Place PCB on spacers
3. Secure with M3 screws
4. Ensure no shorts to enclosure

#### Step 4.3: Cable Routing
1. Route Ethernet cable through opening
2. Organize cables with clips/ties
3. Ensure no strain on connectors
4. Leave service loop for maintenance

#### Step 4.4: Final Assembly
1. Align top cover with base
2. Check sensor window alignment
3. Secure with screws or clips
4. Verify LED visibility

### Phase 5: Final Testing

#### Step 5.1: Functional Test
- [ ] Powers on via PoE
- [ ] Powers on via USB-C
- [ ] Connects to network (Ethernet)
- [ ] Connects to WiFi (if applicable)
- [ ] Reports to Home Assistant
- [ ] mmWave sensor detects presence
- [ ] PIR sensor detects motion
- [ ] Light sensor reads correctly
- [ ] Web interface accessible
- [ ] OTA updates work

#### Step 5.2: Performance Test
- [ ] Verify detection range (16m presence)
- [ ] Check update frequency
- [ ] Monitor for false positives/negatives
- [ ] Temperature check (should be <60°C)
- [ ] Power consumption measurement

#### Step 5.3: Reliability Test
- [ ] Run for 24 hours minimum
- [ ] Check for crashes/reboots
- [ ] Verify consistent network connectivity
- [ ] Monitor sensor stability

---

## Troubleshooting

### PCB Issues

**Problem:** No power
- Check solder joints on power connector
- Verify voltage regulator orientation
- Test with multimeter for shorts

**Problem:** ESP32 not programmable
- Check USB-C data lines
- Verify CP2102/CH340 driver installed
- Try different USB cable/port

**Problem:** Ethernet not working
- Verify LAN8720 connections
- Check RJ45 pinout
- Test with known-good cable

### Sensor Issues

**Problem:** mmWave not detecting
- Verify UART pins are correct
- Check baud rate (115200)
- Ensure 5V power to sensor
- Test with serial monitor first

**Problem:** PIR false triggers
- Adjust sensitivity
- Check for air currents
- Verify proper mounting

**Problem:** Light sensor erratic
- Check I2C connections (SDA/SCL)
- Verify pull-up resistors
- Test with i2c_scan

### Firmware Issues

**Problem:** Won't connect to WiFi
- Double-check SSID and password
- Verify WiFi signal strength
- Check 2.4GHz vs 5GHz
- Try fallback AP mode

**Problem:** Home Assistant not discovering
- Verify mDNS is enabled
- Check firewall settings
- Try manual integration with IP
- Restart Home Assistant

---

## Safety Notes

⚠️ **Important Safety Information:**

1. **PoE Safety**
   - PoE carries up to 57V (before regulation)
   - Ensure proper isolation between PoE and user-accessible parts
   - Never touch PCB while PoE is connected

2. **ESD Protection**
   - Use ESD mat and wrist strap when handling PCB
   - ESP32 is sensitive to static electricity
   - Store components in ESD bags

3. **Soldering Safety**
   - Work in well-ventilated area
   - Use fume extractor if available
   - Never leave soldering iron unattended
   - Wear safety glasses

4. **Power Safety**
   - Verify polarity before connecting power
   - Don't exceed voltage ratings
   - Use fused power supply
   - Disconnect power before making changes

---

## Quality Checklist

Before considering assembly complete:

**Visual Inspection:**
- [ ] All solder joints shiny and smooth
- [ ] No solder bridges between pins
- [ ] Components properly oriented
- [ ] No damaged components
- [ ] Enclosure properly closed

**Electrical Testing:**
- [ ] Voltage rails correct
- [ ] No shorts to ground
- [ ] Current draw reasonable
- [ ] Temperature within spec

**Functional Testing:**
- [ ] All sensors responding
- [ ] Network connectivity stable
- [ ] Home Assistant integration working
- [ ] OTA updates successful

**Mechanical:**
- [ ] Enclosure fits snugly
- [ ] No rattling components
- [ ] Mounting secure
- [ ] Cable strain relief adequate

---

## Post-Assembly

### Break-In Period
- Run for 48-72 hours before permanent installation
- Monitor for any issues
- Fine-tune sensor settings
- Document any quirks or adjustments

### Documentation
- Take photos of assembly
- Note any modifications or substitutions
- Document sensor calibration values
- Keep for future reference

### Backup
- Export ESPHome configuration
- Save Home Assistant automations
- Document network settings

---

## Next Steps

Once assembly is complete:
1. Proceed to [Installation Guide](installation.md)
2. Configure Home Assistant automations
3. Fine-tune sensor settings for your environment
4. Share your build in [Discussions](https://github.com/Soriarty/HaloSense/discussions)!

---

## Contributing

Found errors in this guide or have improvements? See [CONTRIBUTING.md](../CONTRIBUTING.md) for how to submit updates.

Photos of your build process are especially valuable for helping others!

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense

**Last Updated:** 2025-11-28 (Placeholder version)
