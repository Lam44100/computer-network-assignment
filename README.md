# NET2201 Computer Networks Group Assignment Pack

This repository contains the design, Cisco IOS configuration scripts, verification scripts, and report/presentation guides for the NET2201 Computer Networks group assignment.

Current working branch: `dev`

## Shared Document

- [Group report working document](https://imailsunwayedu-my.sharepoint.com/:w:/g/personal/23058944_imail_sunway_edu_my/IQCnC4ep8WQYTp_J6Ywx0a8BAfOt6x0IqGCOE_keaJm1Hxg?e=GesoP3)

## File Structure

```text
computer-network-assignment/
|-- README.md
|-- configs/
|   |-- R1-INTERNAL.ios
|   |-- R2-ISP.ios
|   |-- SW1-DIST.ios
|   `-- SW2-ACCESS.ios
|-- diagrams/
|   `-- topology.mmd
|-- docs/
|   |-- network-design.md
|   |-- packet-tracer-and-lab-build-guide.md
|   |-- report-template.md
|   |-- video-and-presentation-guide.md
|   `-- workplan-checklist.md
`-- tests/
    |-- PC-tests.md
    |-- R1-INTERNAL-tests.ios
    |-- R2-ISP-tests.ios
    |-- README.md
    |-- SW1-DIST-tests.ios
    `-- SW2-ACCESS-tests.ios
```

## What Each Folder Is For

- `configs/` - paste-ready IOS configuration files for each router and switch.
- `diagrams/` - Mermaid topology diagram source for documentation.
- `docs/` - assignment planning, network design, report, lab, video, and presentation documents.
- `tests/` - copy-paste verification commands for routers, switches, and Packet Tracer PCs.

## Recommended Workflow

1. Review [docs/network-design.md](docs/network-design.md) to understand the topology, VLANs, IP addressing, routing, security, and testing plan.
2. Build the topology in Cisco Packet Tracer using [docs/packet-tracer-and-lab-build-guide.md](docs/packet-tracer-and-lab-build-guide.md).
3. Paste the matching config from `configs/` into each Cisco device:
   - `R1-INTERNAL.ios` for the internal router
   - `R2-ISP.ios` for the ISP/external router
   - `SW1-DIST.ios` for the distribution/main switch
   - `SW2-ACCESS.ios` for the access switch
4. Configure the internal PCs to use DHCP and configure the external host manually as `198.51.100.10/24` with gateway `198.51.100.1`.
5. Run the verification scripts in `tests/`:
   - Use the `.ios` test files on routers and switches.
   - Use `tests/PC-tests.md` from Packet Tracer PC command prompts.
6. Capture screenshots or copied outputs for the report.
7. Use [docs/report-template.md](docs/report-template.md) to assemble the final PDF report.
8. Use [docs/video-and-presentation-guide.md](docs/video-and-presentation-guide.md) for the demo video and presentation.

## Current Verification Status

- `tests/PC-tests.md`: Conducted and successful.
- Router and switch verification scripts are available for evidence capture.

## Configuration Notes

- All IOS configuration scripts set the device clock to `12:00:00 2 July 2026` and configure timezone `MYT UTC+8`.
- Access ports use PortFast, BPDU Guard, port security, and DTP-disabled access mode where supported.
- EtherChannel trunk member ports explicitly disable PortFast and BPDU Guard so the trunk bundle can operate correctly.
- Native VLAN is changed to VLAN `999`; trunks allow VLANs `10,20,30,99,999`.
- Adjust interface names if your Packet Tracer or lab equipment uses different ports.
