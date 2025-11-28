# DFRobot C4001 mmWave Presence Sensor (SEN0609)

## Overview

The DFRobot C4001 is a 24GHz FMCW (Frequency Modulated Continuous Wave) millimeter-wave radar sensor designed for presence and motion detection. This sensor is superior to traditional PIR sensors as it can detect both static and moving objects, making it ideal for detecting people who are sitting, sleeping, or in motion.

**Product Information:**
- **SKU:** SEN0609
- **Manufacturer:** DFRobot
- **Technology:** 24GHz mmWave FMCW Radar
- **Dimensions:** 26mm × 30mm

## Key Features

- Detects both **static presence** and **motion**
- Long detection range (up to 25 meters for motion)
- Precise distance and velocity measurement capabilities
- Wide beam angle (100° × 40°)
- Resistant to environmental interference (temperature, light, dust, noise)
- Dual voltage support (3.3V and 5V)
- UART communication interface
- Industrial temperature range (-40°C to 85°C)

## Technical Specifications

### Detection Capabilities

| Parameter | Specification |
|-----------|--------------|
| Presence Detection Range | Up to 16 meters |
| Motion Detection Range | Up to 25 meters |
| Distance Measurement Range | 1.2 to 25 meters |
| Velocity Detection Range | 0.1 to 10 m/s |
| Beam Angle (Horizontal) | 100° |
| Beam Angle (Vertical) | 40° |

### Electrical Characteristics

| Parameter | Specification |
|-----------|--------------|
| Operating Voltage | 3.3V or 5V |
| Operating Temperature | -40°C to 85°C |
| Radar Frequency | 24 GHz |
| Modulation Type | FMCW |

### Communication Interface

| Parameter | Specification |
|-----------|--------------|
| Interface Type | UART (Serial) |
| Default Baud Rate | 115200 bps (configurable 4800-115200) |
| Data Bits | 8 |
| Stop Bits | 1 |
| Parity | None |
| Logic Level | 3.3V/5V compatible |

## Pin Configuration

| Pin | Function | Description |
|-----|----------|-------------|
| VIN | Power Supply | Connect to 3.3V or 5V |
| GND | Ground | Common ground |
| RX | Serial Receive | UART receive pin (connects to TX of controller) |
| TX | Serial Transmit | UART transmit pin (connects to RX of controller) |
| OUT | Voltage Output | Trigger output signal |

## Operating Modes

### 1. Exist Mode (Presence Detection)

Detects the presence of objects/people within the configured range and triggers an output signal. This mode is useful for:
- Occupancy detection
- Automatic lighting control
- Security applications

**Key Parameters:**
- **Trigger Sensitivity:** 0-9 (configurable)
- **Maintain Sensitivity:** 0-9 (configurable)
- **Detection Range:** 30-2500 cm (configurable)
- **Trigger Delay:** Configurable time before activation
- **Maintain Delay:** Configurable time before deactivation

### 2. Speed Mode (Motion Analysis)

Provides detailed information about detected targets including:
- **Distance** to target
- **Velocity** of target
- **Energy Level** of detection signal

This mode is useful for:
- Traffic monitoring
- Intrusion detection
- Activity analysis

## Installation Orientations

The sensor supports three mounting orientations:

1. **Top Installation:** Sensor facing downward (ceiling mount)
2. **Bottom Installation:** Sensor facing upward (floor mount)
3. **Horizontal Installation:** Sensor facing horizontally (wall mount)

Configure the orientation in software to ensure proper detection algorithms.

## Wiring Examples

### Arduino UNO Connection

```
DFRobot C4001    Arduino UNO
-----------      -----------
VIN       <----> 5V
GND       <----> GND
RX        <----> Pin 5 (Software Serial TX)
TX        <----> Pin 4 (Software Serial RX)
OUT       <----> (Optional digital input)
```

### ESP32 Connection (for HaloSense)

```
DFRobot C4001    ESP32
-----------      -----
VIN       <----> 3.3V or 5V
GND       <----> GND
RX        <----> GPIO TX (Hardware Serial)
TX        <----> GPIO RX (Hardware Serial)
OUT       <----> (Optional GPIO input)
```

**Note:** Plan GPIO allocation - the C4001 requires one UART port. ESP32 has multiple hardware UART ports (UART0, UART1, UART2).

## Library Support

### DFRobot Official Library

The sensor is supported by DFRobot's official Arduino library with both I2C and UART communication modes.

**Key Library Methods:**
- Motion detection and presence detection
- Sensitivity adjustment (0-9 range)
- Detection range configuration (30-2500 cm)
- Delay settings for triggering behavior
- Distance and velocity readout (Speed Mode)

### ESPHome Integration

The C4001 is compatible with ESPHome for Home Assistant integration.

**Expected Configuration (ESPHome YAML):**
```yaml
uart:
  id: uart_radar
  tx_pin: GPIO_TX
  rx_pin: GPIO_RX
  baud_rate: 115200  # Default: 115200, configurable down to 4800

sensor:
  - platform: dfrobot_c4001
    uart_id: uart_radar
    presence:
      name: "Presence Detected"
    distance:
      name: "Target Distance"
    velocity:
      name: "Target Velocity"
```

**Note:** If you change the sensor's baud rate via UART commands, update the `baud_rate` parameter accordingly.

## UART Communication Protocol

### Serial Port Parameters

| Parameter | Value |
|-----------|-------|
| Default Baud Rate | 115200 bps (configurable down to 4800) |
| Data Bits | 8 |
| Stop Bits | 1 |
| Parity | None |
| Flow Control | None |

### Command Format

Commands use **ASCII code strings** for easy debugging:
- **Configuration commands:** End with carriage return (`\r`) and line feed (`\n`)
- **Parameters:** Separated by one or more spaces
- **Active data reporting:** Starts with `$`, ends with `*`, parameters separated by `,`

### Important Configuration Rules

1. **Before configuration:** Send `sensorStop` to stop the module
2. **After configuration:** Send `saveConfig` to save parameters to Flash
3. **Activate settings:** Send `sensorStart` to start with new parameters (or `resetSystem 0` for baud rate changes)

### Key Configuration Commands

#### 1. Detection Distance Configuration

**Set Range:** `setRange <min> <max>`
- `min`: Minimum detection distance (0.6-25m, default 0.6m)
- `max`: Maximum detection distance (must be > min and ≤ 25m, default 6m)

**Example:**
```
DFRobot:/> setRange 0.6 12
Done
```

**Note:** There is a ~1m transition zone. If max is set to 3m, targets at 3-4m may still be detected with significant movement.

#### 2. Trigger Distance Configuration

**Set Trigger Range:** `setTrigRange <distance>`
- Defines the distance threshold for initial detection
- Range: 0-25m, default 6m
- Must be ≤ (max detection distance - min detection distance)

**Example:**
```
DFRobot:/> setTrigRange 10
Done
```

**Use case:** Prevents false triggers from edge movements. Smaller trigger distance requires closer proximity to sensor axis.

#### 3. Sensitivity Configuration

**Set Sensitivity:** `setSensitivity <hold> <trigger>`
- `hold`: Hold sensitivity (0-9, default 7) - sensitivity after target detected
- `trigger`: Trigger sensitivity (0-9, default 5) - ease of initial detection
- Higher number = higher sensitivity

**Examples:**
```
DFRobot:/> setSensitivity 6 5
Done

DFRobot:/> setSensitivity 255 3    # Keep hold unchanged, set trigger to 3
Done
```

**Recommendation:** Use trigger sensitivity 2-6 for most applications. Values 8-9 may cause false positives.

#### 4. Latency/Delay Configuration

**Set Latency:** `setLatency <confirm> <disappear>`
- `confirm`: Confirmation delay (0-100s, default 0.050s) - how long target must be present to trigger
- `disappear`: Disappearance delay (0.5-1500s, default 15s) - how long target must be absent to deactivate

**Example:**
```
DFRobot:/> setLatency 0.5 15
Done
```

**Recommendations:**
- **Confirm delay ≥ 0.5s:** Greatly reduces false positives for non-critical timing
- **Disappear delay ≥ 15s:** Reduces missed detections (can use 30s, 60s, 90s for better reliability)

#### 5. Inhibit Time Configuration

**Set Inhibit:** `setInhibit <time>`
- Blocking time after OUT pin signal change (0.1-255s, default 1s)
- Prevents interference from relays, motors, fans during power switching

**Example:**
```
DFRobot:/> setInhibit 0.5
Done
```

#### 6. UART Baud Rate Configuration

**Set UART Baud:** `setUart <baudrate>`
- Range: 4800-115200 bps, default 9600
- **Important:** Requires `resetSystem 0` (not `sensorStart`) to activate

**Example:**
```
DFRobot:/> setUart 57600
Done
DFRobot:/> saveConfig
Done
DFRobot:/> resetSystem 0
```

#### 7. Micro Motion Detection (Speed Mode Only)

**Set Micro Motion:** `setMicroMotion <0|1>`
- 0: Disable (default)
- 1: Enable micro motion detection

#### 8. Threshold Factor (Speed Mode Only)

**Set Threshold Factor:** `setThrFactor <factor>`
- Larger factor = bigger action/object required for detection
- Default: 5

### Control Commands

| Command | Description |
|---------|-------------|
| `sensorStop` | Stop module (required before configuration) |
| `sensorStart` | Start module with current settings |
| `sensorStart 1` | Start module with same state as before stopping |
| `saveConfig` | Save parameters to Flash (required!) |
| `resetCfg` | Restore factory defaults |
| `resetSystem` | Software reset and restart |
| `resetSystem 0` | Normal restart |
| `resetSystem 1` | Restart and enter bootloader |
| `setRunApp 0` | Switch to presence detection mode |
| `setRunApp 1` | Switch to speed/distance measurement mode |

### Active Data Reporting

#### Presence Detection Output: `$DFHPD`

Format: `$DFHPD,<result>, , , *`

Parameters:
- `result`: 0 = No person, 1 = Person detected

**Examples:**
```
$DFHPD,1, , , *    # Person detected
$DFHPD,0, , , *    # No person
```

#### Distance & Speed Output: `$DFDMD`

Format: `$DFDMD,<num>,<target>,<dist>,<speed>,<energy>, , *`

Parameters:
- `num`: Number of targets (0 or 1)
- `target`: Target number (1 when detected)
- `dist`: Distance in meters (0-25m)
- `speed`: Speed in m/s (0-10 m/s)
- `energy`: Signal energy level

**Example:**
```
$DFDMD,1,1,1.817,0.129,15304, , *    # Person at 1.817m, moving 0.129m/s
```

### Query Commands

| Command | Response | Description |
|---------|----------|-------------|
| `getRange` | `Response <min> <max>` | Get detection range |
| `getTrigRange` | `Response <dist>` | Get trigger distance |
| `getSensitivity` | `Response <hold> <trigger>` | Get sensitivity settings |
| `getLatency` | `Response <confirm> <disappear>` | Get delay settings |
| `getInhibit` | `Response <time>` | Get inhibit time |
| `getUart` | `Response <baudrate>` | Get UART baud rate |
| `getMicroMotion` | `Response <0\|1>` | Get micro motion state |
| `getThrFactor` | `Response <factor>` | Get threshold factor |
| `getHWV` | Hardware version string | Get hardware version |
| `getSWV` | Software version string | Get software version |

### Complete Configuration Example

```
# Configure for 3m range, moderate sensitivity, 2s confirm / 15s disappear delays

DFRobot:/> sensorStop
DFRobot:/> setRange 0.6 3
Done
DFRobot:/> setSensitivity 6 5
Done
DFRobot:/> setLatency 2 15
Done
DFRobot:/> saveConfig
save cfg complete
Done
DFRobot:/> sensorStart
Done
```

## Performance Characteristics

### Advantages Over PIR Sensors

| Feature | C4001 mmWave | Traditional PIR |
|---------|--------------|-----------------|
| Static Detection | ✓ Yes | ✗ No |
| Moving Detection | ✓ Yes | ✓ Yes |
| Distance Measurement | ✓ Yes | ✗ No |
| Velocity Measurement | ✓ Yes | ✗ No |
| Temperature Interference | ✓ Resistant | ✗ Sensitive |
| Light Interference | ✓ Immune | ✗ Can affect |
| Dust/Particles | ✓ Resistant | ✗ Can trigger |

### Environmental Resistance

The sensor provides robust performance in challenging conditions:
- **Temperature changes:** No false triggers
- **Ambient light:** Completely unaffected
- **Dust and particles:** Does not cause false detections
- **Environmental noise:** Advanced filtering

## Integration Notes for HaloSense

### Power Considerations
- Typical current draw: TBD (measure during prototyping)
- Compatible with both 3.3V and 5V ESP32 power rails
- Include in total PoE power budget calculation (~5W target)

### GPIO Planning
- Requires 1 hardware UART port (TX/RX pins)
- Optional OUT pin for simple trigger detection
- Consider using UART1 or UART2 (UART0 typically used for programming/debug)

### Mounting Location
- Central ceiling mount recommended for best coverage
- 100° × 40° beam pattern - plan sensor orientation
- Avoid direct mounting near metal objects (can affect radar)

### ESPHome Configuration Priority
- Primary use: Presence detection (Exist Mode)
- Secondary use: Distance measurement for debugging
- Configure appropriate sensitivity levels during testing
- Set reasonable trigger/maintain delays to avoid flicker

## References

- **Official Product Page:** https://wiki.dfrobot.com/SKU_SEN0609_C4001_mmWave_Presence_Sensor_25m
- **Datasheet 1:** https://img.dfrobot.com.cn/wiki/5ea64bf6cf1d8c7738ad2881/35d327648fb4b29373af27a13d9d7405.pdf
- **Datasheet 2:** https://dfimg.dfrobot.com/5ea64bf6cf1d8c7738ad2881/wiki/3b88a4ecd7d7f18918a0fa8ba1f970c6.pdf

## License

This documentation is part of the HaloSense project and follows the same license terms (CC BY-NC-SA 4.0).

---

**Last Updated:** 2025-11-28
**Document Version:** 2.0
**Sensor Hardware Revision:** Refer to DFRobot official documentation

**Version History:**
- **v2.0 (2025-11-28):** Added comprehensive UART protocol documentation from official communication protocol PDF
- **v1.0 (2025-11-28):** Initial documentation created from wiki and partial datasheet information
