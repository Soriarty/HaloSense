# HaloSense Firmware

ESPHome-based firmware configuration for the HaloSense presence sensor.

## 🚧 Work in Progress

Firmware is currently under development. Basic structure is in place, sensor integration pending hardware completion.

## Overview

HaloSense uses [ESPHome](https://esphome.io/) for firmware, providing:
- Easy configuration via YAML
- Seamless Home Assistant integration
- OTA (Over-The-Air) updates
- Web interface for diagnostics
- MQTT support (optional)

## File Structure

```
firmware/
├── halosense.yaml          # Main ESPHome configuration
├── secrets.yaml            # Sensitive data (not in git)
└── README.md               # This file
```

## Quick Start

### Prerequisites

1. **Install ESPHome:**
   ```bash
   pip install esphome
   ```

2. **Create secrets.yaml:**
   ```bash
   cp secrets.yaml.example secrets.yaml
   # Edit secrets.yaml with your credentials
   ```

### Configuration

Edit `halosense.yaml` to match your setup:
- WiFi credentials (in `secrets.yaml`)
- GPIO pin assignments (after hardware is finalized)
- Sensor configurations
- Home Assistant API settings

### Validate Configuration

```bash
esphome config halosense.yaml
```

### Compile Firmware

```bash
esphome compile halosense.yaml
```

### Upload to Device

**Initial flash (via USB):**
```bash
esphome upload halosense.yaml --device /dev/ttyUSB0
```

**OTA updates (after initial flash):**
```bash
esphome upload halosense.yaml
# Or use Home Assistant ESPHome dashboard
```

### View Logs

```bash
esphome logs halosense.yaml
```

## Secrets Configuration

Create a `secrets.yaml` file (not tracked in git):

```yaml
# WiFi
wifi_ssid: "YourSSID"
wifi_password: "YourPassword"

# Fallback AP
ap_password: "FallbackPassword"

# API
api_encryption_key: "your-32-char-encryption-key"

# OTA
ota_password: "YourOTAPassword"

# MQTT (optional)
mqtt_broker: "homeassistant.local"
mqtt_username: "mqtt_user"
mqtt_password: "mqtt_pass"
```

## Sensor Configuration

### DFRobot C4001 mmWave Radar

**Documentation:** [docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md](../docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md)

**Configuration:**
```yaml
uart:
  id: uart_radar
  tx_pin: GPIO_TX  # Update with actual GPIO
  rx_pin: GPIO_RX  # Update with actual GPIO
  baud_rate: 115200

sensor:
  - platform: dfrobot_c4001
    uart_id: uart_radar
    presence:
      name: "Living Room Presence"
    distance:
      name: "Target Distance"
    velocity:
      name: "Target Velocity"
```

### PIR Motion Sensor (TBD)

Configuration pending component selection.

### Ambient Light Sensor (TBD)

Configuration pending component selection.

## Network Configuration

### Ethernet (Preferred)

HaloSense prioritizes wired Ethernet for reliability:
```yaml
ethernet:
  type: LAN8720
  mdc_pin: GPIO23
  mdio_pin: GPIO18
  clk_mode: GPIO17_OUT
  phy_addr: 0
  power_pin: GPIO12
```

### WiFi (Fallback)

WiFi is configured as a fallback if Ethernet is unavailable:
```yaml
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Fallback hotspot
  ap:
    ssid: "HaloSense Fallback"
    password: !secret ap_password
```

## Power Management

The firmware will detect and optimize for available power mode:

- **PoE Mode:** Full features, maximum update rates
- **USB-C Mode:** Optimized for lower power consumption
- **Hybrid Mode:** Ethernet data with USB-C power

## Home Assistant Integration

### Auto-Discovery

ESPHome devices are automatically discovered by Home Assistant when connected to the same network.

### Manual Configuration

If auto-discovery doesn't work:

1. Go to **Settings** → **Devices & Services**
2. Click **+ Add Integration**
3. Search for "ESPHome"
4. Enter HaloSense IP address

### Entities

Once integrated, HaloSense exposes:
- **Presence sensor** - Binary (occupied/clear)
- **Distance sensor** - Numeric (meters)
- **Velocity sensor** - Numeric (m/s)
- **Light level** - Numeric (lux)
- **Diagnostic sensors** - WiFi signal, uptime, etc.

## Advanced Configuration

### Custom Automation Triggers

```yaml
# Example: Presence timeout
binary_sensor:
  - platform: template
    name: "Room Occupied"
    lambda: |-
      if (id(presence_sensor).state) {
        return true;
      }
      return false;
    filters:
      - delayed_off: 5min  # Stay "occupied" for 5 min after last detection
```

### MQTT Integration (Optional)

```yaml
mqtt:
  broker: !secret mqtt_broker
  username: !secret mqtt_username
  password: !secret mqtt_password
  discovery: true
  discovery_prefix: homeassistant
```

### Multi-Zone Detection

Future feature: Configure multiple detection zones with different sensitivity settings.

## Troubleshooting

### Device Not Found

1. Check Ethernet/WiFi connection
2. Verify device is powered on (check status LED)
3. Check router for device IP address
4. Try fallback AP mode

### Sensors Not Working

1. Verify GPIO pin assignments match hardware
2. Check sensor wiring and power
3. Review ESPHome logs for errors
4. Verify sensor libraries are up to date

### OTA Upload Fails

1. Ensure device is reachable on network
2. Verify OTA password is correct
3. Try uploading via USB
4. Check available flash space

## Development Commands

```bash
# Validate configuration
esphome config halosense.yaml

# Compile without uploading
esphome compile halosense.yaml

# Upload via OTA
esphome upload halosense.yaml

# Upload via USB
esphome upload halosense.yaml --device /dev/ttyUSB0

# View real-time logs
esphome logs halosense.yaml

# View logs via network
esphome logs halosense.yaml --device 192.168.1.100

# Clean build files
esphome clean halosense.yaml

# Generate secrets template
esphome secrets halosense.yaml
```

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines on contributing to firmware development.

**Key points:**
- Test on actual hardware
- Document configuration changes
- Follow ESPHome best practices
- Include comments in YAML

## Resources

- **ESPHome Documentation:** https://esphome.io/
- **Home Assistant:** https://www.home-assistant.io/
- **ESP32 Datasheet:** https://www.espressif.com/en/products/socs/esp32
- **DFRobot C4001 Guide:** [docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md](../docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md)

## License

Firmware configuration is licensed under CC BY-NC-SA 4.0. See [LICENSE.md](../LICENSE.md) for details.

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense
