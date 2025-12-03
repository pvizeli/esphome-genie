# Release Setup Guide

This guide explains how to set up automated releases for the Perfume Genie ESPHome firmware.

## GitHub Pages Setup

To enable the web-based firmware installer, you need to configure GitHub Pages:

1. Go to your repository on GitHub
2. Navigate to **Settings** > **Pages**
3. Under **Source**, select **GitHub Actions**
4. Save the settings

The workflow will automatically deploy the firmware installer to `https://<username>.github.io/<repository>/`

## Creating Releases

### Automatic Builds

Every push to the `main` branch will:
- Build firmware for both Genie 2 and Genie 3
- Deploy the latest firmware to GitHub Pages
- Update the web installer with the new binaries

### Creating a Release

To create a versioned release:

1. Go to your repository on GitHub
2. Click on **Releases** > **Create a new release**
3. Click **Choose a tag** and create a new tag (e.g., `v1.0.0`)
4. Fill in the release title and description
5. Click **Publish release**

The workflow will automatically:
- Build firmware for both devices
- Upload the `.factory.bin` and `.ota.bin` files to the release
- Upload `manifest.json` files for each device
- Deploy the firmware to GitHub Pages

### Release Assets

Each release will include:
- `genie-2.bin` - Firmware for ESP8266 version (Genie 2)
- `genie-2.ota.bin` - OTA update for ESP8266 version
- `genie-3.bin` - Firmware for ESP32-C6 version (Genie 3)
- `genie-3.ota.bin` - OTA update for ESP32-C6 version
- `esphome-genie.manifest.json` - Combined web installer manifest for both devices

## Web Installer

After GitHub Pages is enabled, users can visit your site to install firmware directly from their browser using ESP Web Tools:

- No need to install ESPHome or any development tools
- Works directly in Chrome, Edge, or Opera browsers
- Supports both USB flashing and OTA updates

## Manual Workflow Trigger

You can also manually trigger the build workflow:

1. Go to **Actions** tab
2. Select **Build and Publish ESPHome Firmware**
3. Click **Run workflow**
4. Select the branch and click **Run workflow**

## Workflow Overview

The project uses three separate workflows:

1. **ci.yml** - Continuous Integration
   - Tests both Genie 2 and Genie 3 configurations
   - Validates against stable, beta, and dev ESPHome versions
   - Runs on pull requests, pushes to main, and daily schedules

2. **publish-firmware.yml** - Firmware Publishing (triggers on releases)
   - Uses ESPHome's official reusable workflows
   - Builds firmware for both devices
   - Creates combined manifest (esphome-genie.manifest.json)
   - Uploads binaries to GitHub release

3. **publish-pages.yml** - GitHub Pages Deployment
   - Triggers on static file changes or after firmware publishes
   - Downloads latest firmware from releases
   - Deploys web installer to GitHub Pages

## Customization

### Updating the Website

Edit [`static/index.md`](static/index.md) to customize:
- Project description
- Installation instructions
- Additional documentation

### Jekyll Theme

Edit [`static/_config.yml`](static/_config.yml) to:
- Change the site title and description
- Select a different Jekyll theme
- Configure repository links

## Troubleshooting

### Pages not deploying

If GitHub Pages isn't deploying:
- Check that **GitHub Actions** is selected as the source in repository settings
- Ensure the workflow has **contents: write** and **pages: write** permissions
- Check the Actions tab for any workflow errors

### Build failures

If builds are failing:
- Verify that the YAML configurations are valid ESPHome configs
- Check that all required packages are referenced correctly
- Review the workflow logs in the Actions tab

## Further Reading

- [ESPHome Build Action](https://github.com/esphome/build-action)
- [ESP Web Tools](https://esphome.github.io/esp-web-tools/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
