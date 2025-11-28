# HaloSense Installation Guide

Complete guide for installing and configuring your HaloSense presence sensor.

## 🚧 Work in Progress

Installation guide will be completed after hardware and firmware are finalized.

## Overview

This guide covers the installation process from initial setup to Home Assistant integration.

**Estimated Installation Time:** 30-60 minutes (after assembly)

---

## Prerequisites

### Before Installation

- [ ] HaloSense device fully assembled ([see Assembly Guide](assembly.md))
- [ ] Firmware uploaded and tested
- [ ] Network infrastructure ready (PoE switch or router + power)
- [ ] Home Assistant instance running (optional but recommended)
- [ ] Mounting location selected

### Required Equipment

**Essential:**
- Computer or smartphone (for initial configuration)
- Network access (same network as Home Assistant)
- Web browser

**For Wired Installation:**
- Ethernet cable (Cat5e or better)
- PoE switch/injector OR separate USB-C power adapter

**For WiFi Installation:**
- USB-C power adapter (5V/2A minimum)
- WiFi network credentials (2.4GHz)

**Mounting Hardware:**
- Drill and appropriate drill bits (for permanent mounting)
- Screwdriver (if using screws)
- Level (for alignment)
- Pencil (for marking holes)
- Optional: Adhesive mounting tape (for temporary/non-invasive mounting)

---

## Installation Methods

### Method 1: PoE (Recommended)

**Advantages:**
- Single cable for power and data
- Most reliable connectivity
- Professional installation appearance
- No additional power adapter needed

**Steps:**
1. Connect Ethernet cable to HaloSense
2. Connect other end to PoE-enabled switch/injector
3. Device powers on automatically
4. Verify status LED indicates successful boot

**Requirements:**
- IEEE 802.3af PoE switch or injector
- Cat5e or better Ethernet cable

### Method 2: Ethernet + USB-C Power

**Advantages:**
- Wired data connection reliability
- Flexible power placement
- Works with any standard network switch

**Steps:**
1. Connect Ethernet cable to HaloSense
2. Connect Ethernet cable to network switch/router
3. Connect USB-C power adapter to HaloSense
4. Plug power adapter into outlet
5. Verify status LED indicates successful boot

**Requirements:**
- Standard network switch/router
- USB-C power adapter (5V/2A minimum)
- Ethernet cable

### Method 3: WiFi + USB-C Power

**Advantages:**
- No cable routing required
- Easier temporary installations
- Good for testing locations

**Steps:**
1. Connect USB-C power adapter to HaloSense
2. Plug power adapter into outlet
3. Device boots and attempts WiFi connection
4. Configure WiFi if needed (see WiFi Setup below)

**Requirements:**
- USB-C power adapter (5V/2A minimum)
- 2.4GHz WiFi network

**Note:** WiFi mode may have slightly higher latency than wired connections.

---

## Initial Setup

### 1. Power On and Boot

1. Connect power (via PoE or USB-C)
2. Observe status LED:
   - **Solid/Slow blink:** Normal operation
   - **Fast blink:** Connecting to network
   - **No light:** Check power connection

3. Wait 30-60 seconds for boot completion

### 2. Network Connection

#### For Wired Connections (PoE or Ethernet)
- Device automatically obtains IP via DHCP
- No additional configuration needed
- Check router/switch for assigned IP address

#### For WiFi Connections
If WiFi credentials are pre-configured:
- Device connects automatically
- Check router for assigned IP address

If WiFi needs configuration:
1. Connect to fallback AP: "HaloSense Fallback"
2. Open browser to `http://192.168.4.1`
3. Enter WiFi credentials
4. Device restarts and connects to WiFi

### 3. Verify Connectivity

**Option A: Find IP via Router**
1. Access your router's admin interface
2. Look for "HaloSense" in connected devices
3. Note the assigned IP address

**Option B: Use ESPHome Discovery**
If using ESPHome dashboard:
1. Open ESPHome dashboard
2. Device should appear automatically
3. Click to view logs/details

**Option C: Check mDNS**
Try accessing:
- `http://halosense.local/` (may not work on all networks)

### 4. Access Web Interface

1. Open browser
2. Navigate to device IP address (e.g., `http://192.168.1.100`)
3. You should see ESPHome web interface
4. Verify sensor readings appear

---

## Home Assistant Integration

### Auto-Discovery (Easiest)

1. Ensure HaloSense and Home Assistant are on same network
2. Go to **Settings** → **Devices & Services**
3. Look for "Discovered" notification
4. Click **Configure** on HaloSense entry
5. Enter API encryption key (if prompted)
6. Device is added automatically

### Manual Integration

If auto-discovery doesn't work:

1. Go to **Settings** → **Devices & Services**
2. Click **+ Add Integration**
3. Search for and select **ESPHome**
4. Enter HaloSense IP address
5. Enter API encryption key
6. Click **Submit**

**Encryption Key Location:**
- Found in `firmware/secrets.yaml` on build machine
- Or check ESPHome logs during first boot

### Verify Integration

After integration:
1. Go to **Settings** → **Devices & Services** → **ESPHome**
2. Click on HaloSense device
3. Verify entities are visible:
   - Presence sensor (binary)
   - Distance sensor
   - Velocity sensor
   - Light level sensor (when implemented)
   - Diagnostic sensors (WiFi, uptime, etc.)

---

## Physical Installation

### Location Selection

**Optimal Placement:**
- **Height:** 2.0-2.5m (6.5-8 feet) above floor
- **Coverage:** Central location for room coverage
- **Obstacles:** Clear line of sight to monitored area
- **Interference:** Away from fans, HVAC vents, direct sunlight

**Avoid:**
- Behind furniture or obstructions
- Near heat sources (radiators, vents)
- Direct sunlight on sensors
- High vibration areas

### Mounting Options

#### Wall Mount

1. Hold device at desired location
2. Use level to ensure straight alignment
3. Mark screw hole locations with pencil
4. Drill pilot holes (size depends on wall type)
5. Insert wall anchors if needed
6. Attach mounting bracket with screws
7. Secure HaloSense to bracket
8. Route cables neatly

**Cable Routing:**
- Use cable clips along wall/ceiling
- Maintain neat appearance
- Avoid sharp bends in Ethernet cable
- Leave service loop for maintenance

#### Ceiling Mount

Similar to wall mount but:
- Ensure adequate sensor angle coverage
- Consider sensor beam direction (downward)
- Cable routing through ceiling or conduit
- May require flush mount or pendant style bracket

#### Desk/Shelf Mount

1. Place weighted base on surface
2. Ensure stable placement
3. Route cables behind/under furniture
4. Avoid blocking sensor windows

### Sensor Alignment

After mounting:
1. Power on device
2. Access web interface or Home Assistant
3. Observe presence detection
4. Walk through coverage area
5. Adjust angle/position if needed
6. Ensure LED is visible but not distracting

---

## Configuration

### Sensor Calibration

#### mmWave Radar (DFRobot C4001)

**Detection Range:**
1. Access device via ESPHome web interface
2. Monitor detection distance
3. Adjust sensitivity if needed
4. Test with person at various distances

**Sensitivity Tuning:**
- High sensitivity: Detects small movements, more false positives
- Low sensitivity: Requires larger movements, fewer false positives
- Start with medium sensitivity and adjust

#### PIR Motion Sensor

*Configuration TBD after component selection*

#### Ambient Light Sensor

*Configuration TBD after component selection*

### Automation Setup

Example automations in Home Assistant:

**Turn on lights when presence detected:**
```yaml
automation:
  - alias: "Living Room Lights On"
    trigger:
      - platform: state
        entity_id: binary_sensor.halosense_presence
        to: "on"
    action:
      - service: light.turn_on
        target:
          entity_id: light.living_room
```

**Turn off lights after 5 minutes of no presence:**
```yaml
automation:
  - alias: "Living Room Lights Off"
    trigger:
      - platform: state
        entity_id: binary_sensor.halosense_presence
        to: "off"
        for:
          minutes: 5
    action:
      - service: light.turn_off
        target:
          entity_id: light.living_room
```

---

## Testing

### Functional Test Checklist

- [ ] Device powers on and boots
- [ ] Status LED functioning
- [ ] Network connection established
- [ ] Web interface accessible
- [ ] Home Assistant integration working
- [ ] Presence detection responding
- [ ] Distance measurement accurate
- [ ] Velocity measurement working (if applicable)
- [ ] Light sensor reading correctly (when implemented)
- [ ] LED indicator visible
- [ ] OTA updates functional

### Coverage Test

1. Walk through entire monitored area
2. Verify detection at various distances
3. Test detection angles (center vs edges)
4. Check for blind spots
5. Document coverage map if needed

### Performance Test

- [ ] Detection latency acceptable (<1 second)
- [ ] No false positives (adjust sensitivity)
- [ ] No false negatives (adjust sensitivity/placement)
- [ ] Stable operation over 24 hours
- [ ] Temperature within acceptable range (<60°C)

---

## Troubleshooting

### Device Not Powering On

**Check:**
- PoE switch/injector functioning
- USB-C cable and adapter working
- Status LED for any indication
- Power connections secure

**Try:**
- Different power source
- Different Ethernet cable
- Direct connection to power adapter
- Check fuse in PoE injector (if applicable)

### Cannot Connect to Network

**Wired (Ethernet):**
- Verify cable continuity
- Check switch port status LED
- Try different Ethernet port
- Verify DHCP is enabled on network
- Check router for device in client list

**WiFi:**
- Verify 2.4GHz WiFi is available (ESP32 doesn't support 5GHz)
- Check WiFi credentials in secrets.yaml
- Look for fallback AP "HaloSense Fallback"
- Verify WiFi signal strength at installation location

### Home Assistant Not Discovering Device

1. Verify both on same network (no VLAN isolation)
2. Check mDNS/Bonjour service running
3. Try manual integration with IP address
4. Check firewall settings (ports 6053, 6052)
5. Restart Home Assistant

### Sensor Not Detecting

**mmWave Radar:**
- Verify sensor has clear line of sight
- Check sensitivity settings
- Ensure no radio interference
- Verify UART connection in logs
- Test with known movement at various distances

**PIR Sensor:**
*Troubleshooting TBD after component selection*

### False Positives/Negatives

**False Positives (detects when room is empty):**
- Lower sensitivity setting
- Check for moving objects (curtains, pets, fans)
- Verify stable mounting (no vibration)
- Review detection range settings

**False Negatives (doesn't detect presence):**
- Increase sensitivity setting
- Verify sensor alignment/angle
- Check for obstructions
- Test detection range
- Verify person is within detection area

### Poor Performance

- Check device temperature (should be <60°C)
- Verify adequate ventilation
- Check power supply quality
- Review WiFi signal strength (if applicable)
- Check network latency

---

## Maintenance

### Routine Checks

**Monthly:**
- Verify detection accuracy
- Check for firmware updates
- Clean sensor windows (gentle, dry cloth)
- Verify mounting security

**Quarterly:**
- Review automation effectiveness
- Check connection quality (WiFi signal, Ethernet)
- Verify power consumption normal
- Backup configuration

**Annually:**
- Deep clean enclosure
- Inspect cable condition
- Verify all mounting hardware tight
- Consider recalibration

### Firmware Updates

Via Home Assistant:
1. Go to **Settings** → **Devices & Services** → **ESPHome**
2. Click on HaloSense device
3. Click **Update** if available
4. Wait for OTA update to complete

Via ESPHome CLI:
```bash
esphome upload firmware/halosense.yaml
```

**Note:** Device will reboot after update. Automations may trigger during reboot.

### Backup Configuration

**ESPHome Configuration:**
- Keep `halosense.yaml` and `secrets.yaml` backed up
- Version control recommended (git)

**Home Assistant:**
- Regular Home Assistant backups include ESPHome device configs
- Export automations related to HaloSense

---

## Uninstallation

### Removing from Home Assistant

1. Go to **Settings** → **Devices & Services** → **ESPHome**
2. Click on HaloSense device
3. Click **Delete** (three-dot menu)
4. Confirm deletion

### Physical Removal

1. Power off device (disconnect power)
2. Disconnect cables
3. Remove mounting hardware
4. Patch/fill mounting holes if needed
5. Store device safely if reusing

### Factory Reset

To reset device to factory defaults:
1. Connect via USB
2. Reflash firmware with ESPHome
3. Reconfigure from scratch

---

## Advanced Configuration

### Static IP Assignment

Edit `halosense.yaml`:
```yaml
wifi:
  manual_ip:
    static_ip: 192.168.1.100
    gateway: 192.168.1.1
    subnet: 255.255.255.0
```

Or configure DHCP reservation on router (recommended).

### Multiple Sensors

To install multiple HaloSense devices:
1. Give each unique device name in `halosense.yaml`
2. Flash with unique configuration
3. Each appears as separate device in Home Assistant
4. Create room-specific automations

### MQTT Integration

If using MQTT instead of Home Assistant API:
```yaml
mqtt:
  broker: !secret mqtt_broker
  username: !secret mqtt_username
  password: !secret mqtt_password
  discovery: true
```

### Custom Detection Zones

*Advanced feature - TBD in future firmware updates*

---

## Safety Notes

⚠️ **Installation Safety:**

1. **Electrical Safety**
   - Turn off power before working with PoE
   - Use proper voltage-rated tools
   - PoE carries up to 57V (before regulation)
   - Avoid touching exposed connections when powered

2. **Ladder Safety**
   - Use stable ladder for ceiling/high wall mounts
   - Have someone assist with installation
   - Never overreach on ladder

3. **Drilling Safety**
   - Check for electrical wiring behind walls
   - Use stud finder to locate safe drilling locations
   - Wear safety glasses when drilling
   - Know your wall type (drywall, plaster, concrete)

4. **Cable Routing**
   - Avoid pinching cables
   - No sharp bends in Ethernet cables
   - Secure cables to prevent tripping hazard
   - Keep cables away from heat sources

---

## Support and Resources

### Getting Help

- **Documentation:** https://github.com/Soriarty/HaloSense/tree/main/docs
- **Issues:** https://github.com/Soriarty/HaloSense/issues
- **Discussions:** https://github.com/Soriarty/HaloSense/discussions

### Useful Links

- **ESPHome Documentation:** https://esphome.io/
- **Home Assistant:** https://www.home-assistant.io/
- **DFRobot C4001 Guide:** [C4001_TECHNICAL_GUIDE.md](sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md)

---

## Post-Installation

### Next Steps

1. Fine-tune sensor settings for your environment
2. Create Home Assistant automations
3. Monitor performance over first week
4. Share your installation in [Discussions](https://github.com/Soriarty/HaloSense/discussions)
5. Consider installing additional sensors for complete home coverage

### Share Your Setup

Help others by sharing:
- Installation photos
- Coverage maps
- Automation examples
- Tips and tricks learned
- Problem solutions

---

## Contributing

Found issues with this guide? See [CONTRIBUTING.md](../CONTRIBUTING.md) for how to suggest improvements.

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense

**Last Updated:** 2025-11-28 (Placeholder version)
