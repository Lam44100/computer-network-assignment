# Video and Presentation Guide

## 3-4 Minute Video Demonstration Script

Target length: 3-4 minutes.

### 0:00-0:25 - Introduction

Speaker 1:

"This is our NET2201 small-to-medium enterprise network implementation. The network uses four VLANs: Staff/Admin, Student/User, Guest/Public, and Management. It includes two switches, one internal router for inter-VLAN routing and DHCP, and one ISP router for external connectivity."

Show:

- Physical lab setup
- Device labels
- Cable connections

### 0:25-1:00 - Topology and VLANs

Speaker 2:

"SW1 and SW2 are connected using EtherChannel. R1 connects to SW1 using an 802.1Q trunk for router-on-a-stick. Each VLAN has one end device for testing."

Show commands:

```text
show vlan brief
show interfaces trunk
show etherchannel summary
```

### 1:00-1:45 - Inter-VLAN Routing and DHCP

Speaker 3:

"R1 has subinterfaces for VLANs 10, 20, 30, and 99. It also provides DHCP pools for each VLAN, so hosts receive IP addresses automatically."

Show commands:

```text
show ip interface brief
show ip dhcp binding
show ip dhcp pool
```

Show one PC DHCP address.

### 1:45-2:30 - Connectivity Testing

Speaker 4:

"We tested connectivity from each VLAN to its gateway, between VLANs, and from the internal network to the external ISP network."

Show:

```text
ping 192.168.20.x
ping 198.51.100.10
traceroute 198.51.100.10
show ip route
```

### 2:30-3:15 - Security and Reliability

Speaker 5:

"The network includes secure management using SSH, port security, BPDU Guard, shutdown unused ports, VLAN 999 for unused and native VLAN use, and restricted trunk allowed VLANs. SW1 is configured as the STP root bridge."

Show commands:

```text
show spanning-tree
show port-security interface f0/2
show running-config
```

### 3:15-3:45 - Closing

Speaker 1:

"The implementation meets the assignment requirements by demonstrating VLANs, trunking, router-on-a-stick, DHCP, static/default routing, STP, EtherChannel, switch security, secure management, and successful end-to-end testing."

## 15-Minute Presentation Structure

| Time | Section | Presenter |
|---:|---|---|
| 1 min | Introduction and scenario | Member 1 |
| 2 min | Topology and device roles | Member 1 |
| 2 min | VLAN and IP addressing plan | Member 2 |
| 2 min | Inter-VLAN routing, DHCP, and routing plan | Member 3 |
| 2 min | Switch security, STP, and EtherChannel | Member 4 |
| 3-4 min | Video demonstration | All |
| 1-2 min | Testing, troubleshooting, and conclusion | Member 5 |

## Q&A Preparation Questions

Every member should be ready to answer:

- Why did we use VLANs?
- Why is router-on-a-stick needed?
- What is the purpose of trunking?
- Why do trunks need allowed VLANs?
- Why did we change the native VLAN from VLAN 1?
- How does DHCP know which VLAN pool to use?
- Why does the ISP router need return routes?
- What problem does STP prevent?
- What is EtherChannel used for?
- What does port security protect against?
- How did we troubleshoot DHCP or ping failures?
