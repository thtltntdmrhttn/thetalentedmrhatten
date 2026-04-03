# Network Device Inventory

Last scanned: 2026-04-03

## Network Topology

- **Router**: Netgear RAX80 (Nighthawk AX8) at 192.168.1.1
- **Subnet**: 192.168.1.0/24
- **DNS/DHCP**: Router-managed

## DHCP Reservations

| IP | Device | MAC |
|----|--------|-----|
| 192.168.1.12 | Apple HomePod gen 2 (Stairs) | AC:BC:B5:F2:A5:92 |
| 192.168.1.21 | Yamaha RX-A6A MusicCast | 70:97:41:8e:95:54 |
| 192.168.1.26 | Intel NUC (Home Assistant) | 94:C6:91:A3:B0:2D |

## Full Device Inventory

| IP | MAC | Device | Category | Notes |
|----|-----|--------|----------|-------|
| 192.168.1.1 | 14:59:C0:93:2F:45 | Netgear RAX80 Router | Network | Gateway, DHCP, WiFi 6 |
| 192.168.1.7 | - | Onju Voice 2 (ESPHome) | Smart Home | Voice satellite, ESP32-S3, WiFi |
| 192.168.1.12 | AC:BC:B5:F2:A5:92 | Apple HomePod gen 2 | Media | AirPlay, Thread, reserved IP |
| 192.168.1.13 | 64:CB:E9:9D:EE:82 | LG OLED48C1PUB TV | Media | webOS, Magic Remote |
| 192.168.1.14 | 54:E6:1B:F0:6F:6D | Apple TV 4K (gen 2) | Media | AirPlay, Companion, RAOP paired |
| 192.168.1.16 | - | Windows PC (Terence) | Compute | Primary workstation |
| 192.168.1.18 | E6:FC:22:5D:ED:59 | Unknown | - | Needs identification |
| 192.168.1.19 | 00:F6:20:6E:93:B0 | Unknown | - | Needs identification |
| 192.168.1.20 | 44:07:0B:39:78:13 | Unknown (Yamaha old IP?) | - | Possible stale lease |
| 192.168.1.21 | 70:97:41:8E:95:54 | Yamaha RX-A6A MusicCast | Media | AV receiver, reserved IP |
| 192.168.1.26 | 94:C6:91:A3:B0:2D | Intel NUC (Home Assistant) | Compute | HA server, reserved IP |
| 192.168.1.27 | D8:9C:67:9B:54:D9 | Unknown | - | Needs identification |
| 192.168.1.32 | 9C:9E:6E:91:B8:B4 | Unknown | - | Needs identification |

## Known Issues

- **Netgear RAX80 integration**: pynetgear library has an UnboundLocalError bug; HA integration non-functional even on HA 2026.3.4. Upstream fix pending.
- **4 unknown devices**: IPs .18, .19, .27, .32 need identification (consider MAC vendor lookup or physical audit).
- **.20 ambiguity**: MAC 44:07:0B matches Yamaha OUI; likely a stale lease from before DHCP reservation was set on .21.

## Network Upgrade Path

Current RAX80 is consumer-grade. See `BACKLOG.md` for UniFi upgrade plan.
