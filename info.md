## Marstek Integration

Integrate Marstek energy devices with Home Assistant for local monitoring and control.

### Features

- Real-time monitoring of Marstek batteries and inverters (Venus A, Venus D, Venus E 3.0+)
- Local polling via UDP broadcast on port 30000
- Automatic device discovery via mDNS/DHCP
- Sensor entities for battery state of charge, power flow, voltage, current, and more
- Device actions for controlling device settings

### Requirements

- Home Assistant Core ^2025.10.0 or HAOS ^15.0
- Marstek devices and Home Assistant must be on the same local network
- OPEN API must be enabled on your Marstek devices (via the Marstek app)
- **Not compatible with Venus E2.0 devices**

### Installation

1. In Home Assistant, go to **Settings → Devices & Services → HACS**
2. Navigate to **Integrations** and click the **"+ Explore & Download Repositories"** button
3. Search for **"Marstek"** and click to download
4. Restart Home Assistant
5. Go to **Settings → Devices & Services** and click **"Add Integration"**
6. Search for **"Marstek"** and follow the configuration flow

### Configuration

The integration supports automatic discovery. Once installed, it will automatically scan your local network for Marstek devices that have OPEN API enabled.

No manual configuration YAML is required — everything is set up through the config flow in the Home Assistant UI.
