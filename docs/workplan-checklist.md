# NET2201 Assignment Workplan Checklist

Due date: 2 August 2026, 11:59 PM  
Presentation week: week commencing 3 August 2026  
Implementation weeks: week commencing 20 July and 27 July 2026

## 1. Group Setup

- [ ] Confirm 5 members from the same practical group.
- [ ] Record each student name, ID, and contribution percentage.
- [ ] Assign roles:
  - [ ] Network design and topology lead
  - [ ] VLAN/IP addressing and DHCP lead
  - [ ] Routing and router configuration lead
  - [ ] Switch security, STP, and EtherChannel lead
  - [ ] Documentation, screenshots, video, and presentation lead
- [ ] Schedule internal checkpoints before lab weeks.
- [ ] Create a shared folder for Packet Tracer files, configs, screenshots, photos, and video.

## 2. Design Completion

- [ ] Confirm topology has at least 4 PCs, 2 switches, and 2 routers.
- [ ] Confirm VLANs:
  - [ ] VLAN 10 STAFF_ADMIN
  - [ ] VLAN 20 STUDENT_USER
  - [ ] VLAN 30 GUEST_PUBLIC
  - [ ] VLAN 99 MANAGEMENT
  - [ ] VLAN 999 UNUSED_NATIVE
- [ ] Confirm addressing plan:
  - [ ] VLAN 10: 192.168.10.0/24
  - [ ] VLAN 20: 192.168.20.0/24
  - [ ] VLAN 30: 192.168.30.0/24
  - [ ] VLAN 99: 192.168.99.0/24
  - [ ] R1-to-ISP: 203.0.113.0/30
  - [ ] External network: 198.51.100.0/24
- [ ] Confirm port map matches `docs/network-design.md`.
- [ ] Confirm routing plan:
  - [ ] R1 has default route to ISP router.
  - [ ] ISP router has return routes to internal VLAN networks.
- [ ] Confirm selected security features:
  - [ ] Port security
  - [ ] Shutdown unused ports
  - [ ] Unused ports assigned to VLAN 999
  - [ ] DTP disabled on access ports
  - [ ] Secure trunking with allowed VLANs
  - [ ] Native VLAN changed from VLAN 1
  - [ ] BPDU Guard on access ports
  - [ ] SSH management

## 3. Packet Tracer Implementation

- [ ] Build Packet Tracer topology.
- [ ] Configure R1 using `configs/R1-INTERNAL.ios`.
- [ ] Configure R2 using `configs/R2-ISP.ios`.
- [ ] Configure SW1 using `configs/SW1-DIST.ios`.
- [ ] Configure SW2 using `configs/SW2-ACCESS.ios`.
- [ ] Configure all PCs to use DHCP, except any external test server/PC if using static addressing.
- [ ] Save Packet Tracer file with date/version in filename.

## 4. Verification Evidence

Capture screenshots or copied command outputs for:

- [ ] `show vlan brief`
- [ ] `show interfaces trunk`
- [ ] `show ip interface brief`
- [ ] `show ip route`
- [ ] `show running-config`
- [ ] `show interfaces status`
- [ ] `show spanning-tree`
- [ ] `show etherchannel summary`
- [ ] `show ip dhcp binding`
- [ ] `show ip dhcp pool`
- [ ] `show port-security interface`
- [ ] PC DHCP address details
- [ ] Ping from each PC to its default gateway
- [ ] Ping between VLANs
- [ ] Ping from internal VLAN PC to external network
- [ ] Traceroute from internal VLAN PC to external network

## 5. Real Lab Implementation

Before lab:

- [ ] Print or save configs for offline access.
- [ ] Bring topology diagram and port map.
- [ ] Confirm cable types and device interfaces.
- [ ] Assign one member to photograph setup and collect evidence.

During lab:

- [ ] Cable devices according to port map.
- [ ] Configure devices.
- [ ] Save configs with `copy running-config startup-config`.
- [ ] Capture verification commands.
- [ ] Record issues and fixes in troubleshooting log.
- [ ] Take physical topology photos.
- [ ] Record short video clips for final demo.

## 6. Report Completion

- [ ] Use `docs/report-template.md`.
- [ ] Keep final PDF under 25 A4 pages with font size 11.
- [ ] Include topology screenshots/photos.
- [ ] Include VLAN/IP/DHCP tables.
- [ ] Include important configuration snippets.
- [ ] Include testing results.
- [ ] Include troubleshooting narrative.
- [ ] Include video link/evidence.
- [ ] Include references.
- [ ] Place full device configs in appendix.

## 7. Video and Presentation

- [ ] Record 3-4 minute demo using `docs/video-and-presentation-guide.md`.
- [ ] Show physical setup.
- [ ] Show VLAN/trunk/inter-VLAN routing verification.
- [ ] Show DHCP operation.
- [ ] Show successful ping tests.
- [ ] Show at least one security verification.
- [ ] Ensure all members speak or are ready to answer questions.
- [ ] Prepare 15-minute presentation plus 5-minute Q&A.

## 8. Final Submission

- [ ] Final PDF report reviewed by all members.
- [ ] Packet Tracer file backed up.
- [ ] Config files backed up.
- [ ] Screenshots and video backed up.
- [ ] Email report to the relevant lab instructor before 2 August 2026, 11:59 PM.
