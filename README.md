# Dual-Site Corporate Network with IPsec VPN

A fully configured dual-site corporate network built in Cisco Packet Tracer, simulating two geographically separated offices (Sofia and Plovdiv) connected via a site-to-site IPsec VPN tunnel.

## Network Topology



## Overview

| | Sofia Site | Plovdiv Site |
|---|---|---|
| Edge Router | Router0 (1841) | Router2 (1841) |
| Internal Router | R-S-Office (2911) | R-P-Office (2911) |
| Switches | S-Sw-1, S-Sw-2, S-Sw-3 | R-Sw-1, R-Sw-2, R-Sw-3 |
| DHCP Server | 192.168.50.10 | 192.168.51.10 |

## VLAN Segmentation

| VLAN | Name | Sofia Subnet | Plovdiv Subnet |
|------|------|-------------|----------------|
| 10 | Managers | 192.168.10.0/24 | 192.168.11.0/24 |
| 20 | Q/A | 192.168.20.0/24 | 192.168.21.0/24 |
| 30 | Programmers | 192.168.30.0/24 | 192.168.31.0/24 |
| 40 | WiFi | 192.168.40.0/24 | 192.168.41.0/24 |
| 50 | Servers | 192.168.50.0/24 | 192.168.51.0/24 |

## IP Addressing

| Device | Interface | IP Address |
|--------|-----------|------------|
| Router0 | Fa0/0 (LAN) | 192.168.1.1/24 |
| Router0 | Se0/0/0 (WAN) | 10.1.1.1/30 |
| Router1 | Se0/0/0 | 10.1.1.2/30 |
| Router1 | Se0/0/1 | 10.2.2.1/30 |
| Router2 | Se0/0/1 (WAN) | 10.2.2.2/30 |
| Router2 | Fa0/0 (LAN) | 192.168.2.1/24 |
| R-S-Office | Gi0/0 | 192.168.1.2/24 |
| R-P-Office | Gi0/0 | 192.168.2.2/24 |

## Technologies Used

- **VLANs & Trunking** — 802.1Q trunking across all switches
- **Router-on-a-Stick** — subinterfaces on R-S-Office and R-P-Office
- **DHCP with Relay** — centralized DHCP server per site with ip helper-address
- **EIGRP** — dynamic routing within each site
- **WiFi** — WPA2 access points on both sites
- **IPsec VPN** — site-to-site encrypted tunnel between Router0 and Router2

## IPsec VPN Configuration

### IKE Phase 1
```
crypto isakmp policy 10
 encryption aes
 hash md5
 authentication pre-share
 group 2
```

### IKE Phase 2
```
crypto ipsec transform-set VPN-SET esp-aes esp-md5-hmac
```

### Verification
```
show crypto isakmp sa    → QM_IDLE confirms tunnel is up
show crypto ipsec sa     → shows encrypted/decrypted packet counters
```

## Files

| File | Description |
|------|-------------|
| `network.pkt` | Cisco Packet Tracer project file |

## Author

**Aleksandar Gotev**  
Cybersecurity Student — Technical University of Sofia  
[LinkedIn](https://www.linkedin.com/in/aleksandar-gotev)
