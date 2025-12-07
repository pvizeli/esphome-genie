---
title: Perfume Genie ESPHome Firmware
---

## About

Perfume Genie is an ESPHome-based smart fragrance diffuser controller. This project provides firmware for two versions:

- **Genie 2** - ESP8266-based controller with WiFi captive portal
- **Genie 3** - ESP32-C6-based controller with Bluetooth Improv and Bluetooth Proxy

Both versions feature:
- PWM-controlled fan speed
- RGB status LED (WS2812 on Genie 2, Common-Anode RGB on Genie 3)
- Physical button control
- Home Assistant integration
- OTA updates

## Installation

**First time flashing your Genie?** Check out our [Hardware Flashing Guide](flashing.html) for detailed instructions on connecting to your device.

You can use the button below to install the pre-built firmware directly to your device via USB from the browser.

<esp-web-install-button manifest="./firmware/esphome-genie.manifest.json"></esp-web-install-button>

<script type="module" src="https://unpkg.com/esp-web-tools@10/dist/web/install-button.js?module"></script>

## Configuration

After flashing:

**Genie 2 (ESP8266):**
- Connect to the "perfume-genie2 Fallback" WiFi network (password: `config123`)
- Follow the captive portal to configure your WiFi credentials

**Genie 3 (ESP32-C6):**
- Use the [Improv WiFi](https://www.improv-wifi.com/) app on your phone
- Press the physical button to authorize provisioning
- Configure WiFi via Bluetooth

## Source Code

View the source code and configuration files on [GitHub](https://github.com/pvizeli/esphome-genie).

## Support

For issues or questions, please [open an issue](https://github.com/pvizeli/esphome-genie/issues) on GitHub.
