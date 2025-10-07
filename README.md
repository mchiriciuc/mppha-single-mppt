# MPPHA - Single MPPT Voltronic Inverter Interface

ESPHome-based WiFi interface for Voltronic-style solar inverters, MPP Solar PIP inverters, etc. with one MPPT , providing seamless integration with Home Assistant.

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
  - Device mode monitoring (Battery/Grid/Standby/Fault)
  - Status LED integration
  - 802.11k/v WiFi roaming support

## Hardware Requirements

- **MCU**: ESP32-S3-DevKitC-1
- **Interface Board**: MPPHA (custom PCB)
- **Inverter**: Voltronic-style solar inverters (PIP series, etc.)
- **Connection**: UART (GPIO6/GPIO7) at 2400 baud

## Installation

1. Connect the MPPHA device to the serial port of the inverter with the supplied RJ45 cable
2. The inverter should power the board trough the RJ45 cable and a orange led should light up on the board
3. The second led should pulse slowly (aprox. once per second)

## Initial Setup

1. **Power up the device** - The ESP32 will create a WiFi access point named `mppha_single-XXXXXX - Setup` (password: `setup1234`) - Default IP 192.168.4.1
2. **Connect via Bluetooth** using ESP Improv in the Home Assistant ESPHome dashboard
3. **Configure WiFi credentials** through the provisioning interface
4. **Device auto-discovers** in Home Assistant

## Configuration

All configuration is done through Home Assistant after initial setup:

- **Battery Settings**: Configure voltage thresholds and charging parameters
- **Priority Settings**: Set charging and output source priorities
- **Current Limits**: Adjust maximum charging currents
- **Log Level**: Change logging verbosity for debugging

## Troubleshooting

### Device not connecting to WiFi
- Try the fallback AP mode (`mppha_single-XXXXXX - Setup`)
- Check WiFi credentials
- Ensure 2.4GHz WiFi is available (5GHz not supported)

### Entities not appearing in Home Assistant
- Wait 30 seconds for auto-discovery
- Restart Home Assistant
- Check ESPHome logs for connection errors

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
