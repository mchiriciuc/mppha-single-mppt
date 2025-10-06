# MPPHA - Single MPPT Voltronic Inverter Interface

ESPHome-based WiFi interface for Voltronic-style solar inverters, providing seamless integration with Home Assistant.

[![Made for ESPHome](https://img.shields.io/badge/Made%20for-ESPHome-black?logo=esphome)](https://esphome.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Features

- **Comprehensive Monitoring**
  - Grid voltage, frequency, and power metrics
  - Solar (PV) voltage, current, and charging power
  - Battery voltage, charging/discharging current, and state
  - Inverter heat sink temperature and bus voltage
  - Output power, voltage, and load percentage
  - Complete fault and warning indicators

- **Remote Configuration**
  - Battery charging parameters (bulk, float, recharge voltages)
  - Charging source priority (Utility/Solar/Both)
  - Output source priority
  - Maximum charging currents (AC and DC)
  - Dynamic log level control

- **Easy Setup**
  - ESP32 Improv WiFi provisioning via Bluetooth
  - Dashboard import for quick adoption
  - No hardcoded credentials required
  - Automatic AP fallback mode

- **Smart Features**
  - Battery type auto-detection with human-readable names
  - Device mode monitoring (Battery/Grid/Standby/Fault)
  - Status LED integration
  - 802.11k/v WiFi roaming support

## Hardware Requirements

- **MCU**: ESP32-S3-DevKitC-1
- **Interface Board**: MPPHA (custom PCB)
- **Inverter**: Voltronic-style solar inverters (PIP series, etc.)
- **Connection**: UART (GPIO6/GPIO7) at 2400 baud

## Installation

### Option 1: ESPHome Dashboard (Recommended)

1. Open your ESPHome dashboard
2. Click "New Device" → "Continue" → "Open ESPHome Web"
3. Connect your ESP32-S3 via USB
4. The device will appear as "MPPHA Single"
5. Configure WiFi using ESP Improv (Bluetooth)

### Option 2: Manual Installation

```bash
# Clone the repository
git clone https://github.com/mchiriciuc/mppha-single-mppt.git
cd mppha-single-mppt

# Install ESPHome (if not already installed)
pip install esphome

# Compile and upload
esphome run firmware.yaml
```

## Initial Setup

1. **Power up the device** - The ESP32 will create a WiFi access point named `mppha_single-XXXXXX - Setup` (password: `setup1234`)
2. **Connect via Bluetooth** using ESP Improv in the Home Assistant ESPHome dashboard
3. **Configure WiFi credentials** through the provisioning interface
4. **Device auto-discovers** in Home Assistant

## Configuration

All configuration is done through Home Assistant after initial setup:

- **Battery Settings**: Configure voltage thresholds and charging parameters
- **Priority Settings**: Set charging and output source priorities
- **Current Limits**: Adjust maximum charging currents
- **Log Level**: Change logging verbosity for debugging

## Supported Battery Types

- AGM
- User-Defined
- Pylontech
- WECO
- Soltaro
- Lib-protocol

## External Component

This project uses the `pipsolar` custom component for Voltronic protocol communication. Ensure you have the component in your `components/` directory.

## Wiring

| ESP32-S3 Pin | Function | Inverter Connection |
|--------------|----------|---------------------|
| GPIO6        | TX       | RX (Inverter)       |
| GPIO7        | RX       | TX (Inverter)       |
| GPIO45       | Status LED | Built-in LED      |
| GND          | Ground   | GND (Inverter)      |

⚠️ **Important**: Ensure proper voltage levels (3.3V logic) and use appropriate level shifters if required.

## Troubleshooting

### Device not connecting to WiFi
- Try the fallback AP mode (`mppha_single-XXXXXX - Setup`)
- Check WiFi credentials
- Ensure 2.4GHz WiFi is available (5GHz not supported)

### No data from inverter
- Verify UART connections (TX ↔ RX)
- Check baud rate (should be 2400)
- Ensure inverter is powered on
- Review logs via ESPHome dashboard

### Entities not appearing in Home Assistant
- Wait 30 seconds for auto-discovery
- Restart Home Assistant
- Check ESPHome logs for connection errors

## Development

```bash
# Validate configuration
esphome config firmware.yaml

# Compile without upload
esphome compile firmware.yaml

# Monitor logs
esphome logs firmware.yaml
```

## Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Test your changes thoroughly
4. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Credits

- ESPHome Community for the excellent framework
- Pipsolar component developers
- Home Assistant community

## Support

- 🐛 [Report Issues](https://github.com/mchiriciuc/mppha-single-mppt/issues)
- 💬 [Discussions](https://github.com/mchiriciuc/mppha-single-mppt/discussions)
- 📖 [ESPHome Documentation](https://esphome.io)

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history and updates.

---

**Made with ❤️ for the ESPHome community**
