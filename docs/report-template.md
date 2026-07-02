# NET2201 Computer Networks Group Assignment Report

Course code and title: NET2201 Computer Networks  
Assignment title: Design and Implementation of a Small-to-Medium Enterprise Network  
Practical group: [Insert practical group]  
Submission date: [Insert date]

## Cover Page

| Student Name | Student ID | Contribution |
|---|---|---:|
| [Name 1] | [ID] | [%] |
| [Name 2] | [ID] | [%] |
| [Name 3] | [ID] | [%] |
| [Name 4] | [ID] | [%] |
| [Name 5] | [ID] | [%] |

## 1. Introduction

This project designs and implements a segmented small-to-medium enterprise network. The organization is upgraded from a flat network to a VLAN-based network with inter-VLAN routing, centralized DHCP, secure device management, Layer 2 security, redundancy, and external network connectivity.

Objectives:

- Design a structured VLAN-based network.
- Configure trunking and router-on-a-stick inter-VLAN routing.
- Provide automatic IP addressing using DHCP.
- Configure static/default routing to an external network.
- Apply basic switch security and secure device management.
- Verify the design in Cisco Packet Tracer and real Cisco lab equipment.

## 2. Network Requirements

The network includes:

- At least four VLANs.
- At least four end devices.
- At least two switches.
- At least two routers.
- Trunking between switches and router.
- Router-on-a-stick inter-VLAN routing.
- DHCP pools for each VLAN.
- Static/default routing to an external/ISP network.
- STP and EtherChannel demonstration.
- At least four switch security features.
- SSH-based secure device management.

Selected SRWE concepts:

- VLAN segmentation
- 802.1Q trunking
- Inter-VLAN routing
- DHCP
- Static and default routing
- STP
- EtherChannel
- Port security
- Secure management using SSH

## 3. Network Topology

Insert Packet Tracer topology screenshot here.

Insert physical lab topology photo here.

Device roles:

| Device | Role |
|---|---|
| R1-INTERNAL | Inter-VLAN routing, DHCP, default route |
| R2-ISP | ISP/external router and return routing |
| SW1-DIST | Main switch, trunks, EtherChannel, STP root |
| SW2-ACCESS | Access switch for users and management host |

## 4. VLAN and IP Addressing Plan

Use the tables from `docs/network-design.md`.

### VLAN Table

| VLAN | Name | Purpose | Subnet | Gateway |
|---:|---|---|---|---|
| 10 | STAFF_ADMIN | Staff/Admin | 192.168.10.0/24 | 192.168.10.1 |
| 20 | STUDENT_USER | Student/User | 192.168.20.0/24 | 192.168.20.1 |
| 30 | GUEST_PUBLIC | Guest/Public | 192.168.30.0/24 | 192.168.30.1 |
| 99 | MANAGEMENT | Management | 192.168.99.0/24 | 192.168.99.1 |
| 999 | UNUSED_NATIVE | Unused/native VLAN | N/A | N/A |

### DHCP Pool Table

| Pool | Network | Default Gateway | Excluded Range |
|---|---|---|---|
| VLAN10_STAFF | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.1-192.168.10.20 |
| VLAN20_STUDENT | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.1-192.168.20.20 |
| VLAN30_GUEST | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.1-192.168.30.20 |
| VLAN99_MGMT | 192.168.99.0/24 | 192.168.99.1 | 192.168.99.1-192.168.99.30 |

## 5. Configuration Details

Summarize important configuration here and place full configs in the appendix.

### Router Configuration

Key items:

- R1 router-on-a-stick subinterfaces for VLANs 10, 20, 30, and 99.
- DHCP pools on R1.
- R1 default route to R2.
- R2 return routes to internal VLANs.

### Switch Configuration

Key items:

- VLAN creation.
- Access port assignment.
- Trunk port configuration.
- EtherChannel between SW1 and SW2.
- STP root bridge selection.
- Switch management IP addresses.

### Security Configuration

Implemented security features:

- SSH instead of Telnet.
- Enable secret and local username.
- Port security.
- BPDU Guard.
- Disabled unused ports.
- Unused ports assigned to VLAN 999.
- DTP disabled on access ports.
- Native VLAN changed to VLAN 999.

## 6. Testing and Verification

Insert evidence for:

- Ping tests
- DHCP verification
- VLAN verification
- Trunk verification
- Routing table verification
- STP/EtherChannel verification
- Port security verification

Recommended evidence table:

| Test | Command/Evidence | Expected Result | Actual Result |
|---|---|---|---|
| VLAN verification | `show vlan brief` | VLANs 10,20,30,99,999 exist | [Insert] |
| Trunk verification | `show interfaces trunk` | Correct trunks and allowed VLANs | [Insert] |
| DHCP bindings | `show ip dhcp binding` | PCs receive correct IPs | [Insert] |
| Routing | `show ip route` | Connected/static/default routes visible | [Insert] |
| Inter-VLAN ping | PC ping test | Successful | [Insert] |
| External ping | Ping 198.51.100.10 | Successful | [Insert] |
| PC verification script | `tests/PC-tests.md` | DHCP, gateway, inter-VLAN, external ping, and traceroute successful | Conducted successfully |
| EtherChannel | `show etherchannel summary` | Port-channel up | [Insert] |
| STP | `show spanning-tree` | SW1 root bridge | [Insert] |
| Security | `show port-security interface` | Port security enabled | [Insert] |

## 7. Troubleshooting

Record real issues encountered and how they were solved.

| Problem | How Identified | Solution |
|---|---|---|
| [Example: PC did not receive DHCP] | Checked PC IP and `show interfaces trunk` | Added missing VLAN to trunk allowed list |
| [Insert] | [Insert] | [Insert] |

Packet Tracer PC verification was conducted using `tests/PC-tests.md` and completed successfully. Router and switch command outputs should be added from the `.ios` scripts in the `tests` folder.

## 8. Video Demonstration Link or Evidence

Video link: [Insert link]

The video demonstrates:

- Physical lab setup
- Main network devices
- VLAN, trunk, and inter-VLAN routing verification
- DHCP operation
- Successful ping tests
- Security feature verification
- Group member explanation

## 9. Conclusion

The project successfully designed, simulated, implemented, and verified a segmented enterprise network using SRWE concepts. The network supports VLAN-based segmentation, DHCP, inter-VLAN routing, external routing, redundancy, and secure management. Through Packet Tracer and lab implementation, the group gained practical experience in configuration, testing, and troubleshooting Cisco networks.

## 10. References

- Cisco Networking Academy, Switching, Routing, and Wireless Essentials materials.
- Cisco Systems, Cisco IOS Command Reference.
- Cisco Systems, VLAN, trunking, DHCP, STP, EtherChannel, and port security documentation.

## 11. Appendix

Attach:

- Full R1 configuration
- Full R2 configuration
- Full SW1 configuration
- Full SW2 configuration
- Additional screenshots
- Additional testing outputs
- Physical lab photos
