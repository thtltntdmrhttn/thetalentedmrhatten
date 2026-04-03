# Changelog

All notable changes to this project will be documented in this file.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [2026-04-03]

### Added
- Home Assistant Connect ZBT-2 installed and Zigbee network migrated from SkyConnect
- ZBT-2 also added as second Thread border router
- Apple HomePod gen 2 integrated (`media_player.stairs_2`) at 192.168.1.12
- Apple TV 4K (gen 2) paired with AirPlay, Companion, and RAOP protocols
- Yamaha RX-A6A MusicCast integrated (`media_player.living_room_2` + 3 zones) at 192.168.1.21
- LG OLED48C1PUB TV integrated (`media_player.lg_webos_tv_oled48c1pub`) at 192.168.1.13
- HomeKit Bridge paired (code 128-81-894)
- Music Assistant add-on (v2.8.1) with BBC Sounds and AirPlay providers
- Hallway temperature indicator automations (red >22.5C, blue <18C, white normal, 9am-1am)
- DHCP reservations on Nighthawk: HomePod .12, Yamaha .21, NUC .26
- Repository restructured as scalable home automation control center
- `docs/ARCHITECTURE.md` — system architecture overview
- `docs/HARDWARE.md` — hardware inventory and specifications
- `docs/NETWORK.md` — network device inventory and DHCP reservations
- `docs/BACKLOG.md` — task backlog, automation ideas, and hardware wishlist
- `CHANGELOG.md` — this file
- Dashboard updated with HomePod, Yamaha, LG TV media controls

### Changed
- Evening Protocol scene: Cosmic Light set to OFF
- Repository now serves dual purpose: Cloudflare Pages portal and home automation documentation

### Removed
- Globe temperature indicator automations (replaced by Hallway temperature indicators)

## [2026-03-29]

### Added
- HMAC-signed TOTP tokens replacing plaintext sessionStorage auth
- JWT-based admin verification for all admin actions
- SRI (Subresource Integrity) pinning for CDN-loaded scripts
- Butler skill for personal life management

### Fixed
- `isApprovedUser(null)` returning `true` (critical auth bypass)
- Approved users localStorage poisoning vector
- Multiple XSS vectors in email rendering and news links
- Navigation bypass via console `showPage()` calls

## [2026-03-28]

### Added
- Cloudflare Access protection across all 3 domains
- Portal pages: Access Control, Remote Terminal, Wine Cellar, Finance, Reminders
- Art Nouveau theme with Bodoni Moda typography
- Speaker dropdown with volume control and multi-room media playback
- Git-backed config system with git-crypt encryption and 1Password CLI
- Repo-backed wine cellar data (`data/wines.json`)

### Changed
- Portal-level approval gate for unapproved visitors
- CF Access session duration set to 15 minutes with binding cookies

### Security
- 11 vulnerabilities fixed (2 critical, 3 XSS, API key exposure, CSS injection, session bypass)
- Content-Security-Policy meta tag and `_headers` file for CF Pages
- All hardcoded tokens scrubbed; secrets loaded from encrypted files

## [2026-03-25]

### Added
- Onju Voice 2 ESPHome integration (wake word, STT, TTS working)
- Ollama local LLM (qwen2.5:3b) on NUC for voice assistant Q&A
- BBC World Service toggle automation with input_boolean
- Wallmote Duo button automations (all lights on/off)

### Fixed
- Wake word model name mismatch (`ok_nabu_v0.1` vs `okay_nabu`)
- openWakeWord threshold tuning (settled at 0.3)

## [2026-03-24]

### Added
- Initial portal deployment to Cloudflare Pages
- Home Assistant integration with Claude Code
- Command Center dashboard with room-based sections
- 3 scene protocols: Daylight (6500K), Evening (2700K), Nighttime (candlelight)
- Globe temperature indicator automations
- Entity management tools (`ha-entity-manager.py`, `ha-dashboard-push.py`)

### Removed
- 806 stale entities (iBeacon trackers, dead devices, orphan sensors)
