# Backlog

Task tracking, ideas, and hardware planning for the home automation system.

Last updated: 2026-04-03

---

## Automation Ideas

### 1. Circadian Lighting
- **Priority**: High
- **Method**: Adaptive Lighting integration via HACS
- **Description**: Auto-adjust color temperature throughout the day. Cool white (6500K) in morning, warm (2700K) in evening, candlelight (2000K) at night.
- **Prerequisites**: Install HACS, install Adaptive Lighting custom integration
- **Devices**: All 19 Zigbee lights (Tuya support 2000-6500K range, OSRAM 2702-6500K)

### 2. Presence-Based Automation
- **Priority**: High
- **Method**: Phone/device tracker entities, HA zones
- **Description**: Auto-control lights when arriving home or leaving. Turn on entry lights on arrival, turn off everything on departure.
- **Prerequisites**: Reliable device tracker (phone WiFi, BLE, or companion app)
- **Enhancement**: Pair with Aqara FP2 mmWave sensor for room-level occupancy

### 3. CO2-Based Ventilation
- **Priority**: Medium
- **Method**: Aranet4 sensor threshold trigger
- **Description**: Turn on attic fan or send notification when CO2 exceeds 1000ppm. Aranet4 sensor already reporting to HA.
- **Prerequisites**: Smart switch on attic fan (or notification-only as first step)
- **Devices**: Aranet4 (sensor), attic fan (needs smart switch)

### 4. Morning Routine
- **Priority**: Medium
- **Method**: Time-triggered automation with gradual transitions
- **Description**: Gradual light brightening over 15-30 minutes before wake time. Start BBC World Service on HomePod at target wake time.
- **Prerequisites**: Music Assistant (installed), HomePod AirPlay (working)
- **Devices**: Bedroom lights, HomePod gen 2

### 5. Movie Mode
- **Priority**: Medium
- **Method**: Scene + automation or script
- **Description**: Single button to: dim all lights to 5%, turn on LG TV, switch Yamaha to correct HDMI input, set volume to comfortable level.
- **Prerequisites**: LG webOS integration (active), Yamaha MusicCast integration (needs loading)
- **Devices**: 19 lights, LG OLED48C1PUB, Yamaha RX-A6A

---

## Hardware Wishlist

### Networking
| Item | Purpose | Est. Cost | Priority |
|------|---------|-----------|----------|
| Ubiquiti UniFi Dream Machine or Cloud Gateway | Replace RAX80, proper network management, VLAN support for IoT isolation | $200-380 | High |

### Sensors
| Item | Purpose | Est. Cost | Priority |
|------|---------|-----------|----------|
| Aqara FP2 Presence Sensor (mmWave) | Room-level occupancy detection, no false negatives unlike PIR | $60 | High |
| Aqara P2 or Hue Motion Sensors (x3-4) | Hallway/bathroom/kitchen motion-triggered lighting | $25-40 each | Medium |
| Door/window contact sensors (x4-6) | Security alerts, HVAC efficiency (don't heat with windows open) | $15-20 each | Medium |

### Climate
| Item | Purpose | Est. Cost | Priority |
|------|---------|-----------|----------|
| Ecobee or Nest Thermostat | Smart HVAC scheduling, occupancy-aware, HA integration | $180-250 | Medium |
| Smart blinds (Ikea FYRTUR or Lutron Serena) | Circadian/privacy automation, heat management | $100-300/window | Low |

### Compute / AI
| Item | Purpose | Est. Cost | Priority |
|------|---------|-----------|----------|
| USB Coral TPU | Hardware ML acceleration for Frigate NVR (if cameras added) | $35-60 | Low |

---

## Integration TODO

| Integration | Status | Action Needed |
|-------------|--------|---------------|
| HACS | Not installed | Install via SSH docker exec, add as HA integration |
| Mushroom Cards | Blocked by HACS | Install after HACS |
| Adaptive Lighting | Blocked by HACS | Install after HACS, configure circadian schedule |
| Yamaha MusicCast | **Active** | Loaded at 192.168.1.21, main + 4 zones |
| Netgear RAX80 | Broken (pynetgear bug) | Monitor upstream library for fix |
| HomePod (Apple TV) | **Active** | Paired at 192.168.1.12, AirPlay working |
| Apple TV 4K | **Active** | Paired at 192.168.1.14, AirPlay + Companion + RAOP |
| LG webOS TV | **Active** | Auto-detected at 192.168.1.13 |
| Midea AC | Not started | Research LAN integration via HACS |
| GE Profile AC (SmartHQ) | Not started | Research integration options |
| Samjin Button | Available, unassigned | Create automation (e.g., toggle scene) |
| Bike Button | Available, unassigned | Create automation |
| Matter Server | v8.1.0 | Update to v8.3.0 |
| Z-Wave JS | v0.21.0 | Update to v1.1.0 |
| Invintory wines | Research complete | Build browser bookmarklet for collection export |

---

## Bug Fixes

| Issue | Severity | Notes |
|-------|----------|-------|
| Netgear RAX80 pynetgear UnboundLocalError | Low | Upstream bug, no HA-side fix. Monitor pynetgear releases. |
| Google Home duplicate Evening Protocol | Low | User needs to delete the Google Home routine manually |
| Unknown network devices (.18, .19, .27, .32) | Info | Need MAC vendor lookup or physical audit to identify |
| .20 stale DHCP lease (possible old Yamaha) | Info | Likely resolved once lease expires or router is replaced |

---

## Completed

- [x] Voice assistant pipeline (OK Nabu > Whisper > Ollama > Piper)
- [x] Music Assistant + BBC World Service on HomePod
- [x] Git-crypt config sync with 1Password
- [x] Cloudflare Access + portal security hardening
- [x] Scene protocols (Daylight, Evening, Nighttime)
- [x] Wallmote Duo automations
- [x] Entity cleanup (806 stale entities removed)
- [x] HA 2025.8 > 2026.3.4 migration (color_temp > color_temp_kelvin)
