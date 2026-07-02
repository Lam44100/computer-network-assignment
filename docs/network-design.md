# NET2201 Proposed Network Design

## 1. Design Summary

This design represents a small organization migrating from a flat network to a segmented enterprise network. It uses VLANs, trunking, router-on-a-stick, DHCP, static/default routing, EtherChannel, STP, switch security, and SSH-based management.

The design is suitable for Cisco Packet Tracer and can be reproduced using common Cisco lab equipment such as 2960 switches and ISR routers. Interface names may need adjustment depending on the exact lab hardware.

## 2. Topology

Devices:

| Device | Role |
|---|---|
| R1-INTERNAL | Router-on-a-stick, DHCP server, default route to ISP |
| R2-ISP | External/ISP router and simulated remote network |
| SW1-DIST | Main switch connected to R1 and SW2 |
| SW2-ACCESS | Access switch connected to SW1 |
| PC-STAFF | VLAN 10 test host |
| PC-STUDENT | VLAN 20 test host |
| PC-GUEST | VLAN 30 test host |
| PC-MGMT | VLAN 99 test host |
| EXT-SERVER or EXT-PC | External network test host |

Recommended physical links:

| Link | Port A | Port B | Purpose |
|---|---|---|---|
| R1 to SW1 | R1 G0/0 | SW1 G0/1 | 802.1Q trunk for router-on-a-stick |
| SW1 to SW2 | SW1 F0/23 | SW2 F0/23 | EtherChannel trunk member |
| SW1 to SW2 | SW1 F0/24 | SW2 F0/24 | EtherChannel trunk member |
| R1 to R2 | R1 G0/1 | R2 G0/0 | WAN/ISP link |
| R2 to external host | R2 G0/1 | EXT-SERVER NIC | External test network |

## 3. VLAN Plan

| VLAN | Name | Purpose | Subnet | Default Gateway |
|---:|---|---|---|---|
| 10 | STAFF_ADMIN | Staff/Admin users | 192.168.10.0/24 | 192.168.10.1 |
| 20 | STUDENT_USER | Student/User department | 192.168.20.0/24 | 192.168.20.1 |
| 30 | GUEST_PUBLIC | Guest/Public users | 192.168.30.0/24 | 192.168.30.1 |
| 99 | MANAGEMENT | Device management | 192.168.99.0/24 | 192.168.99.1 |
| 999 | UNUSED_NATIVE | Unused ports and native VLAN | No user subnet | Not assigned |

## 4. IP Addressing Plan

| Device/Interface | IP Address | Mask | Notes |
|---|---:|---:|---|
| R1 G0/0.10 | 192.168.10.1 | 255.255.255.0 | VLAN 10 gateway |
| R1 G0/0.20 | 192.168.20.1 | 255.255.255.0 | VLAN 20 gateway |
| R1 G0/0.30 | 192.168.30.1 | 255.255.255.0 | VLAN 30 gateway |
| R1 G0/0.99 | 192.168.99.1 | 255.255.255.0 | VLAN 99 gateway |
| R1 G0/1 | 203.0.113.1 | 255.255.255.252 | Link to ISP |
| R2 G0/0 | 203.0.113.2 | 255.255.255.252 | Link to R1 |
| R2 G0/1 | 198.51.100.1 | 255.255.255.0 | External network gateway |
| SW1 VLAN 99 | 192.168.99.11 | 255.255.255.0 | Switch management |
| SW2 VLAN 99 | 192.168.99.12 | 255.255.255.0 | Switch management |
| EXT-SERVER/EXT-PC | 198.51.100.10 | 255.255.255.0 | Static external test host |

## 5. DHCP Plan

DHCP is configured on R1.

| Pool | Network | Default Router | Excluded Range |
|---|---|---|---|
| VLAN10_STAFF | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.1-192.168.10.20 |
| VLAN20_STUDENT | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.1-192.168.20.20 |
| VLAN30_GUEST | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.1-192.168.30.20 |
| VLAN99_MGMT | 192.168.99.0/24 | 192.168.99.1 | 192.168.99.1-192.168.99.30 |

## 6. Switch Port Assignment

| Switch | Ports | Mode | VLAN/Purpose |
|---|---|---|---|
| SW1 | G0/1 | Trunk | To R1, allowed VLANs 10,20,30,99,999 |
| SW1 | F0/2 | Access | VLAN 10, PC-STAFF |
| SW1 | F0/3 | Access | VLAN 20, PC-STUDENT |
| SW1 | F0/23-24 | EtherChannel trunk | To SW2 |
| SW1 | Other unused ports | Access/shutdown | VLAN 999 |
| SW2 | F0/2 | Access | VLAN 30, PC-GUEST |
| SW2 | F0/3 | Access | VLAN 99, PC-MGMT |
| SW2 | F0/23-24 | EtherChannel trunk | To SW1 |
| SW2 | Other unused ports | Access/shutdown | VLAN 999 |

## 7. Routing Plan

R1:

- Directly connected to all internal VLANs through subinterfaces.
- Has a default route to R2 at 203.0.113.2.

R2:

- Directly connected to WAN link and external network.
- Has return routes for all internal VLANs via R1 at 203.0.113.1.

## 8. Security Plan

The design applies these security controls:

| Feature | Where Applied | Purpose |
|---|---|---|
| SSH management | Routers and switches | Avoid insecure Telnet |
| Local username and enable secret | Routers and switches | Protect privileged access |
| Management VLAN 99 | Switch SVIs | Separate device management traffic |
| Port security | Access ports | Limit MAC addresses on endpoint ports |
| PortFast and BPDU Guard | Access ports only | Protect STP edge ports connected to end devices |
| DTP disabled | Access ports | Prevent unwanted trunk negotiation |
| Native VLAN changed to 999 | Trunks | Avoid VLAN 1 native trunking |
| Unused ports shutdown | Switches | Reduce attack surface |
| Unused ports assigned to VLAN 999 | Switches | Isolate inactive ports |

Note: EtherChannel trunk member ports explicitly disable PortFast and BPDU Guard. This prevents edge-port features from being applied to switch-to-switch trunk links while keeping those protections on access ports.

All routers and switches set the local device clock to `12:00:00 2 July 2026` and timezone `MYT UTC+8` at the beginning of their IOS configuration scripts. This supports consistent timestamps for screenshots, command outputs, and troubleshooting evidence.

## 9. Testing Plan

Minimum tests:

| Test | Expected Result |
|---|---|
| `show clock` on routers and switches | Clock shows 2 July 2026 with MYT timezone |
| PC-STAFF gets DHCP IP | 192.168.10.21 or above |
| PC-STUDENT gets DHCP IP | 192.168.20.21 or above |
| PC-GUEST gets DHCP IP | 192.168.30.21 or above |
| PC-MGMT gets DHCP IP | 192.168.99.31 or above |
| Each PC pings gateway | Successful |
| PC-STAFF pings PC-STUDENT | Successful |
| PC-GUEST pings PC-MGMT | Successful |
| Internal PC pings 198.51.100.10 | Successful |
| Internal PC traceroutes to 198.51.100.10 | Path shows R1 then R2 |
| `show interfaces trunk` | Trunks active with VLANs 10,20,30,99,999 allowed |
| `show etherchannel summary` | Port-channel up |
| `show spanning-tree` | SW1 root bridge for VLANs 10,20,30,99 |
| `show port-security interface f0/2` | Port security enabled on access port |

Use the copy-paste verification scripts in `tests/` to run these checks consistently. `tests/PC-tests.md` has been conducted successfully for the Packet Tracer PC connectivity checks.

## 10. Troubleshooting Notes

Common issues and fixes:

| Symptom | Likely Cause | Fix |
|---|---|---|
| PC cannot get DHCP address | VLAN, trunk, or DHCP pool issue | Check access VLAN, trunk allowed VLANs, and R1 DHCP pool |
| Inter-VLAN ping fails | Router subinterface missing/wrong encapsulation | Check `encapsulation dot1Q` and gateway IPs |
| External ping fails | Missing default route or return route | Check R1 default route and R2 static routes |
| EtherChannel down | Mismatched mode or trunk settings | Check both sides use same channel-group and trunk config |
| Switch SSH fails | Missing management IP/default gateway/domain/RSA keys | Check VLAN 99 SVI, `ip default-gateway`, username, and crypto key |
