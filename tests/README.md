# NET2201 Verification Test Scripts

These scripts match the testing plan in `docs/network-design.md`.

Use them after all devices are configured and all links show green/up in Packet Tracer.

## How to Use

1. Open each network device CLI.
2. Copy the matching script into that device:
   - `R1-INTERNAL-tests.ios`
   - `R2-ISP-tests.ios`
   - `SW1-DIST-tests.ios`
   - `SW2-ACCESS-tests.ios`
3. Open each PC command prompt.
4. Run the commands in `PC-tests.md`.
5. Save screenshots or copied outputs for the report.

## Important Notes

- PC DHCP addresses can vary. If a PC receives a different address from the expected `.21` or `.31` values, use the actual DHCP address shown by `ipconfig`.
- Packet Tracer PCs usually use `tracert`, while Cisco IOS devices use `traceroute`.
- A successful requirement needs both configuration evidence and testing evidence.

## Required Evidence Checklist

- [ ] Each VLAN PC receives a DHCP address.
- [ ] Each PC can ping its default gateway.
- [ ] PC-STAFF can ping PC-STUDENT.
- [ ] PC-GUEST can ping PC-MGMT.
- [ ] An internal PC can ping `198.51.100.10`.
- [ ] An internal PC can trace the path to `198.51.100.10`.
- [ ] Trunks are active and allow VLANs `10,20,30,99,999`.
- [ ] EtherChannel is up.
- [ ] STP is running and SW1 is root bridge for VLANs `10,20,30,99`.
- [ ] Port security is enabled on access ports.
