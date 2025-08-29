# SwitchBot API v1.1 Template for Zabbix 7.0 — GPT-5 generated PoC

This repository contains a **Zabbix 7.0 template** for monitoring **SwitchBot devices** via the official **SwitchBot Cloud API v1.1**.  
It was vibe-coded with GPT-5 and is provided **for personal use / PoC purposes**.

## Features

- **Auto-discovery (LLD)** of multiple device types:
  - Bots *(disabled by default — see Notes)*  
  - Color Bulbs  
  - Contact Sensors (with motion, brightness, open state)  
  - Curtains  
  - Meters (Temperature / Humidity)  
  - Meters (CO₂)  
  - Motion Sensors  
  - Plugs 
- **Metrics collected** (depending on device type):
  - Battery level  
  - Power state  
  - Brightness  
  - Motion detection  
  - Open/close state  
  - Raw JSON for troubleshooting  
- **Script-based items only** (no external scripts needed, all inline JavaScript).  
- Includes **signed request handling** (HMAC-SHA256) for SwitchBot API v1.1.  

## Notes

- The **Bot discovery rule is disabled** because current Bot models always return `battery = 100` from the Cloud API, making battery monitoring unreliable.  
- This template is experimental; it works, but was primarily built as a PoC.  
- Requires Zabbix 7.0+ with support for JavaScript item types.  

## Installation

1. Import the template YAML (`zbx_export_templates.yaml`) into your Zabbix frontend.  
2. Set the following **user macros** at the host or template level:

   - `{$SWITCHBOT.API}` – API endpoint (default: `https://api.switch-bot.com`)  
   - `{$SWITCHBOT.BATTERY.MIN}` – Minimum battery threshold (default: `20`)  
   - `{$SWITCHBOT.CO2.MAX}` – Maximum CO₂ level threshold (default: `1000`)  
   - `{$SWITCHBOT.HUM.MAX}` – Maximum humidity threshold (default: `70`)  
   - `{$SWITCHBOT.HUM.MIN}` – Minimum humidity threshold (default: `30`)  
   - `{$SWITCHBOT.INTERVAL}` – Interval for API polling (default: `10m`)  
   - `{$SWITCHBOT.SECRET}` – SwitchBot API secret (HMAC sign)  
   - `{$SWITCHBOT.TOKEN}` – SwitchBot API token (Authorization header)  

3. Link the template to a dummy host (no agent required).  

## License

This template is distributed under the **GNU AGPLv3**, the same license as Zabbix.  
