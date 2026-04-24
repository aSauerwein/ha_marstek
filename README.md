# Marstek Home Assistant Integration

<div align="center">

[![HACS Default][hacs-badge]][hacs-url]
![GitHub Release][release-badge]
[![License][license-badge]][license-url]
[![Quality Scale][quality-badge]][quality-url]

**Monitor and control Marstek energy storage devices directly from Home Assistant — fully local, no cloud required.**

</div>

---

## Overview

The Marstek integration provides seamless integration with Marstek battery and inverter systems (Venus A, Venus D, Venus E 3.0+) for real-time monitoring and control within Home Assistant.

It communicates **locally** over your network using UDP broadcast, so your data stays on your premises. No cloud services, no external APIs.

## Features

- **Real-time monitoring** — battery state of charge, power flow, voltage, current, temperature
- **Local-only communication** — no cloud dependency, data stays on your network
- **Automatic discovery** — devices found via UDP broadcast and mDNS
- **Device actions** — control device settings directly from Home Assistant
- **Config flow** — easy setup through the Home Assistant UI, no YAML required

## System Requirements

| Requirement | Minimum |
|---|---|
| Home Assistant Core | ^2025.10.0 |
| Home Assistant OS | ^15.0 |
| Network | HA and devices on the same local network |
| Device API | OPEN API must be enabled on Marstek devices |

> [!WARNING]
> This integration is **not compatible** with Venus E2.0 devices. Using it with Venus E2.0 may cause disconnection between the device and the CT003 controller.

## Installation

### Option 1: Install via HACS (Recommended)

[![Install with HACS](https://my.home-assistant.io/badges/hacs_repository.svg)][hacs-install-url]

1. Open **HACS** in Home Assistant
2. Go to **Integrations** → click the **"+"** button
3. Search for **"Marstek"**
4. Click **Download**
5. Restart Home Assistant
6. Go to **Settings → Devices & Services** → **Add Integration**
7. Search for **"Marstek"** and follow the setup wizard

### Option 2: Manual Installation

1. Clone this repository and switch to the `marstek-dev` branch:
   ```bash
   git clone https://github.com/MarstekEnergy/ha_marstek.git
   cd ha_marstek
   git checkout marstek-dev
   ```

2. Copy the `custom_components/marstek` folder to your Home Assistant config directory:
   ```bash
   cp -r ./custom_components/marstek /path/to/homeassistant/config/custom_components/
   ```

3. Restart Home Assistant

4. Go to **Settings → Devices & Services** → **Add Integration**

5. Search for **"Marstek"** and follow the configuration flow

## Configuration

No manual `configuration.yaml` entry is needed. The integration uses a web-based config flow accessible through the Home Assistant UI.

Upon first setup, the integration will automatically:
1. Broadcast a UDP discovery packet on port `30000`
2. Listen for responses from nearby Marstek devices
3. Present discovered devices for configuration

> [!TIP]
> If your device isn't discovered, verify that OPEN API is enabled in the Marstek app and that port 30000 is open on your network.

## Supported Devices

| Device | Supported |
|---|---|
| Venus A | ✅ |
| Venus D | ✅ |
| Venus E 3.0 | ✅ (with updated firmware) |
| Venus E2.0 | ❌ Not compatible |
| Other Marstek devices with OPEN API | ✅ |

## Updating the Integration

### Via HACS

HACS will automatically notify you when a new version is available. Click **Update** in the HACS UI, then restart Home Assistant.

### Manual Update

```bash
cd /path/to/ha_marstek
git pull origin marstek-dev
cp -r ./custom_components/marstek /path/to/homeassistant/config/custom_components/
```

## Directory Structure

After installation, your Home Assistant directory will contain:

```
config/custom_components/marstek/
├── __init__.py         # Integration entry point
├── config_flow.py      # UI configuration flow
├── const.py            # Constants and defaults
├── coordinator.py       # Data update coordinator
├── device_action.py    # Device actions
├── manifest.json        # Integration metadata
├── quality_scale.yaml   # HACS quality scale (Bronze)
├── scanner.py           # UDP device scanner
├── sensor.py            # Sensor entity definitions
├── strings.json         # Config flow strings
└── translations/
    └── en.json          # English translations
```

## Frequently Asked Questions

### What is OPEN API?

OPEN API is a local communication interface built into Marstek device firmware. It allows querying device status and sending control commands over the local network without requiring an internet connection.

Enable it in the Marstek mobile app under device settings.

### Why can't I find my device?

- OPEN API is not enabled on the device
- Home Assistant and the device are on different network segments
- Port 30000 is blocked by a firewall
- The device is in a sleep state — try pinging the network or checking again

### What sensors are available?

Typical sensors include:
- Battery state of charge (%)
- Battery voltage and current
- Power flow (charge/discharge/standby)
- Device temperature
- Grid power, load power
- System status

### Can I use this with the Marstek app at the same time?

Yes, both can coexist on the same network. However, avoid making conflicting commands from both interfaces simultaneously.

## Development

### Running Tests

```bash
pip install -r requirements.txt -r requirements_test.txt
pytest tests/
```

### Code Structure

- `scanner.py` — UDP broadcast discovery
- `coordinator.py` — DataUpdateCoordinator for entity state management
- `sensor.py` — Entity definitions for all sensor types
- `config_flow.py` — Home Assistant config flow implementation

## License

Copyright (C) 2025 Hamedata Technology Co., Limited.

This software is provided under a proprietary license. See the [LICENSE](LICENSE) file for full terms. Redistribution and use in source and binary forms must retain the copyright notice and license terms.

---

<div align="center">

Built with ❤️ for the Home Assistant community

[hacs-badge]: https://img.shields.io/badge/HACS-Default-41BDF5.svg?style=for-the-badge&logo=home-assistant
[hacs-url]: https://hacs.xyz/docs/features/integrations
[hacs-install-url]: https://my.home-assistant.io/redirect/hacs_repository/?owner=MarstekEnergy&repository=ha_marstek&category=integration
[release-badge]: https://img.shields.io/github/v/release/MarstekEnergy/ha_marstek?style=for-the-badge
[license-badge]: https://img.shields.io/badge/License-Proprietary-888?style=for-the-badge
[license-url]: LICENSE
[quality-badge]: https://img.shields.io/badge/Quality_Scale-Bronze-F5B700?style=for-the-badge
[quality-url]: https://www.home-assistant.io/integrations/marstek

</div>
