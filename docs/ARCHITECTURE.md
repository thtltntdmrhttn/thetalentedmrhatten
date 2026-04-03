# Home Automation Architecture

Last updated: 2026-04-03

## System Overview

```
                        INTERNET
                           |
                    [Netgear RAX80]
                     192.168.1.1
                    WiFi 6 / LAN
                           |
          +----------------+----------------+
          |                |                |
    [Intel NUC]     [Windows PC]     [IoT Devices]
   192.168.1.26     192.168.1.16     .7,.12,.13,.21
   Home Assistant   Claude Code      Onju, HomePod,
   Ollama LLM       Workstation      LG TV, Yamaha
```

## Core Platform

### Home Assistant (NUC - 192.168.1.26)
- **Version**: 2026.3.4
- **OS**: Home Assistant OS
- **Role**: Central automation hub, device management, voice assistant backend
- **Entity count**: ~490 (19 lights, 10 automations, 3 scenes, 7 switches, 8 media players)
- **Add-ons**: Z-Wave JS, Advanced SSH, VS Code Server, Matter Server, Music Assistant, Ollama, openWakeWord, Whisper, Piper

### Claude Code (Windows PC - 192.168.1.16)
- **Role**: Configuration management, automation authoring, system administration
- **Connection**: REST API + WebSocket to HA
- **Tools**: ha-api.sh, ha-entity-manager.py, ha-dashboard-push.py
- **Config sync**: git-crypt encrypted repo, 1Password CLI for secrets

## Communication Protocols

### Zigbee (ZHA via ZBT-2)
- **Coordinator**: Home Assistant Connect ZBT-2
- **Devices**: 19 lights (Tuya, OSRAM), buttons (Samjin, Bike), sensors
- **Network**: Mesh topology, devices act as routers

### Z-Wave (Z-Wave JS)
- **Controller**: USB Z-Wave stick
- **Devices**: Wallmote Duo, Doorbell, smart switches
- **Add-on**: Z-Wave JS v0.21.0

### Thread / Matter (ZBT-1)
- **Border router**: Home Assistant Connect ZBT-1 (OTBR)
- **Status**: Active, ready for Matter-over-Thread devices

### WiFi
- **Devices**: Onju Voice 2, HomePod, LG TV, Yamaha RX-A6A
- **Network**: Netgear RAX80 (WiFi 6)

### Bluetooth
- **Devices**: Aranet4 CO2 sensor
- **Range**: Limited to NUC proximity

## Integration Map

```
+------------------+     +------------------+     +------------------+
|    ZHA (ZBT-2)   |     |   Z-Wave JS      |     |   Thread/OTBR    |
|  19 Zigbee lights|     |  Wallmote Duo     |     |    (ZBT-1)       |
|  Buttons/Sensors |     |  Doorbell         |     |  Matter devices  |
+--------+---------+     +--------+---------+     +--------+---------+
         |                        |                        |
         +------------------------+------------------------+
                                  |
                        +---------+---------+
                        |  HOME ASSISTANT   |
                        |   192.168.1.26    |
                        +---------+---------+
                                  |
         +------------------------+------------------------+
         |              |                |                  |
+--------+------+ +-----+------+ +------+-------+ +-------+--------+
|    Tuya       | |  ESPHome   | | Music Assist | |   Ollama       |
| Cloud devices | | Onju Voice | | BBC Sounds   | | qwen2.5:3b     |
|               | | .7         | | AirPlay      | | Voice Q&A      |
+---------------+ +------------+ +--------------+ +----------------+
         |              |                |
+--------+------+ +-----+------+ +------+-------+
|  LG webOS TV  | |  Cast      | | HomeKit      |
|  .13          | | Chromecast | | Bridge       |
+---------------+ +------------+ +--------------+
         |
+--------+------+
| Yamaha         |
| MusicCast .21  |
+----------------+
```

## Voice Pipeline

```
Wake word       STT              LLM               TTS
"OK Nabu"  -->  Whisper   -->  Ollama qwen2.5  -->  Piper
(openWakeWord)  (local)        (local, NUC)        (local)
threshold: 0.3                 prefer_local_intents: true
                               Device cmds -> HA native
                               General Q&A -> Ollama
```

- All processing is local (no cloud dependency for voice)
- Onju Voice 2 handles audio I/O; NUC handles all compute
- Cold start: ~3.4s (Ollama model loading); warm: ~1.4s

## Web Portal

### Cloudflare Pages (thetalentedmrhatten.com)
- **Source**: This repo, `public/` directory, auto-deploys from master
- **Auth**: Cloudflare Access (email OTP) + portal-level approval gate
- **Domains**: thetalentedmrhatten.com, terencelinushatten.com, oliviafrancesmcdowell.com
- **Pages**: Dashboard, Command Center, Voice, Devices, Security, Architecture, Roadmap, Glossary, Website Build, Access Control, Remote Terminal, Wine Cellar, Reminders, Finance
- **Admin**: TOTP via Google Authenticator, HMAC-signed session tokens

## Data Flow

```
[Sensors/Devices] --> [HA Automations] --> [Device Actions]
                          |
                    [HA REST API]
                          |
                  [Claude Code CLI]
                          |
              [Git repo + Cloudflare Pages]
```

## Security Layers

1. **Network**: RAX80 NAT/firewall, no port forwarding
2. **Cloudflare Access**: Email OTP on all portal domains
3. **Portal auth**: Approved user list, HMAC-signed TOTP tokens
4. **Admin auth**: JWT verification from CF cookie
5. **Secrets**: git-crypt encrypted, 1Password CLI managed
6. **HA access**: Long-lived token loaded from encrypted secrets file

## Directory Structure (this repo)

```
thetalentedmrhatten/
+-- public/              Cloudflare Pages site (DO NOT MODIFY from docs)
|   +-- index.html       Portal SPA
|   +-- _headers         CF Pages security headers
+-- data/                Application data
|   +-- wines.json       Wine collection
|   +-- approved-users.json
|   +-- audit-log.json
|   +-- butler-notes.json
+-- docs/                Home automation documentation
|   +-- ARCHITECTURE.md  This file
|   +-- HARDWARE.md      Hardware inventory
|   +-- NETWORK.md       Network device inventory
|   +-- BACKLOG.md       Task backlog and ideas
+-- CHANGELOG.md         Project changelog
```
