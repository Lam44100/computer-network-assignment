# Packet Tracer and Lab Build Guide

## 1. Build the Topology

Place these devices:

- 1 router named `R1-INTERNAL`
- 1 router named `R2-ISP`
- 2 switches named `SW1-DIST` and `SW2-ACCESS`
- 4 internal PCs named `PC-STAFF`, `PC-STUDENT`, `PC-GUEST`, and `PC-MGMT`
- 1 external host named `EXT-SERVER` or `EXT-PC`

Recommended Packet Tracer models:

- Routers: 2911 or any router with at least two Gigabit Ethernet interfaces
- Switches: 2960
- End devices: Generic PCs or server

## 2. Cable the Devices

| Connection | Cable | Purpose |
|---|---|---|
| R1 G0/0 to SW1 G0/1 | Copper straight-through | Router-on-a-stick trunk |
| SW1 F0/23 to SW2 F0/23 | Copper crossover or auto | EtherChannel member |
| SW1 F0/24 to SW2 F0/24 | Copper crossover or auto | EtherChannel member |
| R1 G0/1 to R2 G0/0 | Copper crossover or auto | WAN/ISP link |
| R2 G0/1 to EXT-SERVER | Copper straight-through | External test network |
| PC-STAFF to SW1 F0/2 | Copper straight-through | VLAN 10 |
| PC-STUDENT to SW1 F0/3 | Copper straight-through | VLAN 20 |
| PC-GUEST to SW2 F0/2 | Copper straight-through | VLAN 30 |
| PC-MGMT to SW2 F0/3 | Copper straight-through | VLAN 99 |

## 3. Apply Configurations

Configure devices in this order:

1. SW1-DIST
2. SW2-ACCESS
3. R1-INTERNAL
4. R2-ISP
5. End devices

Paste the matching file from the `configs` folder into each device CLI.

Important notes:

- Each IOS config sets the clock first with `clock set 12:00:00 2 July 2026`, then enters configuration mode and sets timezone `MYT UTC+8`.
- If your router uses `fastEthernet` instead of `gigabitEthernet`, adjust the interface names before pasting.
- If your switch does not support LACP with `channel-group 1 mode active`, use `channel-group 1 mode desirable` or `channel-group 1 mode on` on both switches, depending on instructor/lab support.
- If Packet Tracer rejects `switchport nonegotiate` on an access port, continue with `switchport mode access`; the access mode still prevents the port from becoming a trunk.
- PortFast and BPDU Guard are applied on access ports. EtherChannel trunk member ports explicitly disable PortFast and BPDU Guard so the switch-to-switch trunk bundle forms correctly.

## 4. Configure End Devices

Internal PCs:

| PC | Network Setting | Expected IP Range |
|---|---|---|
| PC-STAFF | DHCP | 192.168.10.21-192.168.10.254 |
| PC-STUDENT | DHCP | 192.168.20.21-192.168.20.254 |
| PC-GUEST | DHCP | 192.168.30.21-192.168.30.254 |
| PC-MGMT | DHCP | 192.168.99.31-192.168.99.254 |

External host:

| Setting | Value |
|---|---|
| IP address | 198.51.100.10 |
| Subnet mask | 255.255.255.0 |
| Default gateway | 198.51.100.1 |

## 5. Verification Order

Run tests in this order so problems are easier to isolate:

1. On routers and switches: `show clock`
2. On switches: `show vlan brief`
3. On switches: `show interfaces trunk`
4. On switches: `show etherchannel summary`
5. On R1 and R2: `show ip interface brief`
6. On R1: `show ip dhcp binding`
7. On each PC: confirm DHCP address
8. From each PC: ping its gateway
9. From PC-STAFF: ping PC-STUDENT
10. From PC-GUEST: ping PC-MGMT
11. From an internal PC: ping `198.51.100.10`
12. From an internal PC: traceroute `198.51.100.10`
13. On switches: `show spanning-tree`
14. On switches: `show port-security interface f0/2`

The same checks are available as copy-paste scripts in the `tests` folder. Use `tests/PC-tests.md` for Packet Tracer PCs and the `.ios` files for routers and switches.

## 6. Evidence Naming Convention

Use clear filenames so the report is easy to assemble:

- `01-topology-packet-tracer.png`
- `02-physical-lab-photo.jpg`
- `03-show-vlan-brief-sw1.png`
- `04-show-interfaces-trunk-sw1.png`
- `05-show-etherchannel-summary.png`
- `06-show-ip-dhcp-binding-r1.png`
- `07-ping-inter-vlan.png`
- `08-ping-external-network.png`
- `09-show-spanning-tree.png`
- `10-show-port-security.png`

## 7. Lab Day Fallbacks

If a command is not accepted:

- Check the exact device model and IOS feature support.
- Use `?` in CLI to find the supported command form.
- Keep the design requirement the same, but adapt syntax to the device.
- Record the issue and fix in the troubleshooting section of the report.

If EtherChannel is unavailable:

- Demonstrate STP using two switch links.
- Document that hardware or IOS limitations prevented EtherChannel.
- Still show STP preventing Layer 2 loops.

If SSH key generation fails:

- Confirm hostname and domain name are configured.
- Retry `crypto key generate rsa modulus 1024`.
- If unsupported, document secure password protection and explain the limitation.
