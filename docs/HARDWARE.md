# Hardware Inventory

Last updated: 2026-04-03

## Compute

### Intel NUC (Home Assistant Server)
- **IP**: 192.168.1.26 (DHCP reserved)
- **CPU**: Intel Core i7-8559U @ 2.70GHz
- **RAM**: 16GB
- **Disk**: 228GB total, ~185GB free
- **OS**: Home Assistant OS
- **HA Version**: 2026.3.4
- **Ollama**: qwen2.5:3b model (~2GB RAM when loaded)

### Windows PC (Terence)
- **IP**: 192.168.1.16
- **OS**: Windows 11 Home (10.0.26200)
- **Role**: Primary workstation, Claude Code host

## Wireless Radios and Coordinators

### Home Assistant Connect ZBT-2 (Zigbee)
- **Protocol**: Zigbee 3.0
- **Serial**: E072A1D78450
- **Integration**: ZHA
- **Role**: Primary Zigbee coordinator (migrated from SkyConnect)
- **Connected devices**: 19 lights, buttons, sensors

### Home Assistant Connect ZBT-1 (Thread/OTBR)
- **Protocol**: Thread (OpenThread Border Router)
- **Role**: Thread border router for Matter-over-Thread devices

### Z-Wave JS USB Stick
- **Integration**: Z-Wave JS (add-on v0.21.0, update available: v1.1.0)
- **Connected devices**: Wallmote Duo, Doorbell

### Original SkyConnect (Legacy)
- **Status**: Replaced by ZBT-2 for Zigbee duties
- **Note**: Kept as spare

## Media Devices

### Apple HomePod gen 2 (Stairs)
- **IP**: 192.168.1.12 (DHCP reserved)
- **MAC**: AC:BC:B5:F2:A5:92
- **HA Entity**: `media_player.stairs_2` (native), `media_player.stairs_3` (Music Assistant/AirPlay)
- **Protocols**: AirPlay, Thread
- **Notes**: Streaming via Music Assistant solves pyatv AAC limitation

### Yamaha RX-A6A MusicCast
- **IP**: 192.168.1.21 (DHCP reserved)
- **MAC**: 70:97:41:8E:95:54
- **HA Entity**: `media_player.living_room_2` (+ zone2/3/4)
- **Integration**: Yamaha MusicCast

### Apple TV 4K (gen 2)
- **IP**: 192.168.1.14
- **MAC**: 54:E6:1B:F0:6F:6D
- **HA Entity**: `media_player.living_room_3_2`
- **Protocols**: AirPlay, Companion, RAOP (all paired)
- **Integration**: Apple TV

### LG OLED48C1PUB TV
- **IP**: 192.168.1.13
- **MAC**: 64:CB:E9:9D:EE:82
- **HA Entity**: `media_player.lg_webos_tv_oled48c1pub`
- **Integration**: LG webOS TV

## Voice and Sensors

### Onju Voice 2 (ESPHome)
- **IP**: 192.168.1.7
- **Platform**: ESP32-S3, ESPHome 2026.3.1
- **Components**: I2S microphone (GPIO017), I2S DAC media_player (GPIO012)
- **Wake word**: "OK Nabu" (server-side openWakeWord, threshold 0.3)
- **Pipeline**: openWakeWord > Whisper STT > Ollama qwen2.5:3b > Piper TTS
- **Limitations**: Cannot play live HTTP streams (I2S limitation); use Music Assistant for streaming

### Aranet4 CO2/Temperature/Humidity Sensor
- **Protocol**: Bluetooth
- **Measures**: CO2 (ppm), temperature, humidity, atmospheric pressure
- **Use case**: Indoor air quality monitoring, ventilation automation trigger

### Aeotec Wallmote Duo (Z-Wave)
- **Protocol**: Z-Wave (Node 10, ZW129)
- **Battery**: 100%
- **Automations**: Button 1 = all lights ON, Button 2 = all lights OFF

### Doorbell (Z-Wave)
- **Protocol**: Z-Wave
- **Tones**: 4 (Ding Dong, Chimes, Ship Bell, Christmas Tree)
- **Volume**: 0.3

### Samjin Button (Zigbee/ZHA)
- **Battery**: 100%
- **Status**: Available, no automation assigned

### Bike Button (Zigbee/ZHA)
- **Battery**: 100%
- **Status**: Available, no automation assigned

## Lighting

### Zigbee Lights (19 total)
- **Tuya lights**: Full RGB (hs) + color_temp (2000K-6500K range)
- **OSRAM lights**: Color_temp only (2702K-6500K range)
- **Rooms**: Kitchen, Lounge, Office, Bedroom, Bathroom, Hallway, Attic, Stairs
- **Note**: 3 OSRAM lights previously dead (Lamp One revived in Session 11; Office Lamp, Bedroom Nook removed)

### Smart Switches (7 total)
- Various Z-Wave and Zigbee in-wall switches

## Network

### Netgear RAX80 (Nighthawk AX8)
- **IP**: 192.168.1.1
- **MAC**: 14:59:C0:93:2F:45
- **WiFi**: WiFi 6 (802.11ax)
- **HA Integration**: Non-functional (pynetgear UnboundLocalError bug)
- **Upgrade path**: See BACKLOG.md for UniFi recommendation
