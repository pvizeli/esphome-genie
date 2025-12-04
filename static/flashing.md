---
title: Hardware Flashing Guide
---

# Hardware Flashing Guide

This guide explains how to flash ESPHome firmware to your Rituals Perfume Genie device for the **first time**. After the initial flash, all future updates can be done wirelessly via Home Assistant (OTA updates).

**Note:** If your device is already running ESPHome, use the [web installer](index.html) instead.

## Prerequisites

Before you begin, you'll need:

- **USB-to-UART adapter** (3.3V compatible)
- **Jumper wires** or test clips
- **Computer** with Chrome, Edge, or Opera browser
- **Basic electronics knowledge**
- The device you want to flash (Genie 2 or Genie 3)

**⚠️ Safety Warning:** You'll be working with electronics. Ensure proper handling and avoid short circuits.

## Genie 2 (ESP8266) Flashing

### Hardware Overview

The Genie 2 uses an **ESP-WROOM-02** (ESP8266) module.

### Required Connections

You need to connect the following pins between your USB-to-UART adapter and the Genie device:

| Adapter Pin | Genie Pin | Purpose |
|-------------|-----------|---------|
| 3.3V | VCC | Power |
| GND | GND | Ground |
| TX | RX | Data transmit |
| RX | TX | Data receive |
| - | GPIO0 → GND | Boot mode (hold during power-up) |

**Important:** The GPIO0 to GND connection is only needed during the initial power-up to enter flash mode.

### Step-by-Step Flashing Process

1. **Prepare Your Setup**
   - Open the Genie device carefully to access the circuit board
   - Identify the pins on the ESP-WROOM-02 module
   - You can use test clips or temporarily hold wires against the pins (no soldering required for testing)

2. **Enter Flash Mode**
   - Connect GPIO0 to GND (hold with a jumper wire or test clip)
   - Connect all other pins as shown in the table above
   - While holding GPIO0 to GND, power up the device (either via USB or the adapter's 3.3V)
   - You should now be in flash mode

3. **Flash the Firmware**
   - Go to [https://pvizeli.github.io/esphome-genie](https://pvizeli.github.io/esphome-genie)
   - Click the "Install" button
   - Select your USB-to-UART adapter from the browser popup
   - Follow the on-screen instructions
   - Wait for the flashing process to complete

4. **Disconnect GPIO0**
   - After flashing is complete, disconnect GPIO0 from GND
   - Power cycle the device (disconnect and reconnect power)
   - The device should boot into ESPHome

### Troubleshooting

**Problem:** Device not detected
- Ensure your USB-to-UART adapter is properly connected
- Try a different USB port
- Check that you're using a browser that supports Web Serial (Chrome, Edge, Opera)

**Problem:** Flashing fails or times out
- Make sure GPIO0 is connected to GND before powering up
- Try providing external power via the device's micro-USB port during flashing
- Verify all pin connections are solid

**Problem:** Device boots into original firmware
- GPIO0 may not have been grounded during power-up
- Try the flashing process again, ensuring GPIO0 is held low when powering on

## Genie 3 (ESP32-C6) Flashing

### Hardware Overview

The Genie 3 uses an **ESP32-C6** module.

### Required Connections

The Genie 3 uses almost identical connections to Genie 2, with **one important difference**:

| Adapter Pin | Genie Pin | Purpose |
|-------------|-----------|---------|
| 3.3V | VCC | Power |
| GND | GND | Ground |
| TX | RX | Data transmit |
| RX | TX | Data receive |
| - | **GPIO9 → GND** | Boot mode (hold during power-up) |

**⚠️ Critical Difference:** Use **GPIO9** instead of GPIO0 for the Genie 3!

### Step-by-Step Flashing Process

The flashing process for Genie 3 is identical to Genie 2, except:

1. **Use GPIO9 instead of GPIO0**
   - Connect GPIO9 to GND (not GPIO0)
   - Hold this connection during power-up to enter flash mode

2. **Follow the same steps as Genie 2**
   - Enter flash mode by holding GPIO9 to GND during power-up
   - Use the web installer at [https://pvizeli.github.io/esphome-genie](https://pvizeli.github.io/esphome-genie)
   - Flash the firmware
   - Disconnect GPIO9 from GND after flashing
   - Power cycle the device

### Troubleshooting

The troubleshooting steps are the same as Genie 2, but remember to use **GPIO9** instead of GPIO0.

## After Flashing

### First Boot

After successfully flashing, the device will boot into ESPHome. Here's what to expect:

1. **LED Behavior**
   - On boot: White LED (initialization)
   - After boot: Blue LED (WiFi disconnected) or Green LED (WiFi connected)

2. **WiFi Configuration**

   **For Genie 2 (ESP8266):**
   - Look for a WiFi network named "perfume-genie2 Fallback"
   - Connect to it (password: `config123`)
   - Follow the captive portal to configure your WiFi credentials

   **For Genie 3 (ESP32-C6):**
   - Download the [Improv WiFi](https://www.improv-wifi.com/) app on your phone
   - Use Bluetooth to provision WiFi credentials
   - Press the physical button on the device to authorize provisioning

3. **Home Assistant Integration**
   - Once connected to WiFi, the device will be automatically discovered by Home Assistant
   - Go to **Settings → Devices & Services** in Home Assistant
   - Click "Configure" on the discovered ESPHome device
   - Enter the encryption key when prompted

### Future Updates

**Good news!** After this initial flash, you never need to connect wires again. All future firmware updates can be done wirelessly:

- Updates via Home Assistant dashboard
- OTA updates from this website (when new versions are released)
- ESPHome dashboard (if you run your own ESPHome instance)

## Additional Resources

- [Home Assistant Community Discussion](https://community.home-assistant.io/t/replace-the-software-of-the-rituals-genie-esp-with-esphome/762356)
- [ESP Genie GitHub Repository](https://github.com/KarolKozlowski/esp-geine)
- [ESPHome Documentation](https://esphome.io/)

## Need Help?

If you encounter issues not covered in this guide:

1. Check the troubleshooting sections above
2. Review the community discussions linked above
3. [Open an issue](https://github.com/pvizeli/esphome-genie/issues) on GitHub

---

[← Back to Main Page](index.html)
