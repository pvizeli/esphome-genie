# ESPHome Genie

ESPHome firmware for Rituals Perfume Genie devices, supporting both Genie 2 (ESP8266) and Genie 3 (ESP32-C6) versions.

## Features

- 🌊 PWM-controlled fan speed with auto-off timer
- 💡 WS2812 RGB status LED
- 🔘 Physical button control
- 🏠 Native Home Assistant integration
- 📡 OTA updates (wireless firmware updates)
- 🔄 Automatic firmware updates from GitHub releases
- 📶 WiFi provisioning via captive portal (Genie 2) or Bluetooth (Genie 3)

## Quick Start

### Installation

Visit **[https://pvizeli.github.io/esphome-genie/](https://pvizeli.github.io/esphome-genie/)** for:

- 🌐 **Web-based firmware installer** - Flash your device directly from the browser
- 📖 **Hardware flashing guide** - First-time setup instructions
- ⚙️ **Configuration guide** - WiFi setup and Home Assistant integration

### Supported Devices

| Device | Chip | Features |
|--------|------|----------|
| **Genie 2** | ESP8266 (ESP-WROOM-02) | WiFi, Captive Portal |
| **Genie 3** | ESP32-C6 | WiFi, Bluetooth Improv, BLE Proxy |

## Configuration Files

- `genie-2.yml` - ESP8266 (Genie 2) configuration
- `genie-3.yml` - ESP32-C6 (Genie 3) configuration
- `common.yml` - Shared configuration for both devices

## Development

### Building Locally

```bash
# Validate configuration
esphome config genie-2.yml
esphome config genie-3.yml

# Compile firmware
esphome compile genie-2.yml
esphome compile genie-3.yml
```

### Creating a Release

1. Create a new release on GitHub with a version tag (e.g., `v1.0.0`)
2. GitHub Actions will automatically:
   - Build firmware for both devices
   - Create a combined manifest file
   - Upload binaries to the release
   - Deploy to GitHub Pages

## Project Structure

```
.
├── genie-2.yml              # ESP8266 device config
├── genie-3.yml              # ESP32-C6 device config
├── common.yml               # Shared configuration
├── static/
│   ├── index.md            # Main documentation page
│   ├── flashing.md         # Hardware flashing guide
│   └── _config.yml         # Jekyll configuration
└── .github/workflows/
    ├── ci.yml              # CI testing (stable/beta/dev)
    ├── publish-firmware.yml # Release builds
    └── publish-pages.yml   # GitHub Pages deployment
```

## GPIO Pin Mappings

### Common Pins (Both Devices)
- GPIO3: Power button
- GPIO4: Fan PWM control
- GPIO15: WS2812 LED

### Device-Specific
- **Genie 2**: GPIO0 for flash mode
- **Genie 3**: GPIO9 for flash mode, GPIO16 for connect button

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Resources

- [Official Documentation](https://pvizeli.github.io/esphome-genie/)
- [ESPHome Documentation](https://esphome.io/)
- [Home Assistant Community Discussion](https://community.home-assistant.io/t/replace-the-software-of-the-rituals-genie-esp-with-esphome/762356)

## License

See [LICENSE](LICENSE) file for details.

## Credits

Based on community efforts to reverse-engineer and provide open-source firmware for Rituals Perfume Genie devices.

Special thanks to:
- [KarolKozlowski/esp-geine](https://github.com/KarolKozlowski/esp-geine) for hardware documentation
- Home Assistant community for testing and feedback
