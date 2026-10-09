# Switching Problems and Solutions

An animated group presentation that explains and solves three Layer 2 switching problems: **VLANs and trunking**, **Spanning Tree Protocol (STP)**, and **EtherChannel with port security**.

Each problem includes a scenario, a step-by-step animation of how it works, the Cisco IOS configuration, and verification commands. It is built to help students understand the topics and explain them to a teacher.

## Problems Covered

### 1. VLANs and Trunking
Sales (VLAN 10) and HR (VLAN 20) users are spread across two switches. VLANs separate the broadcast domains, and an 802.1Q trunk (native VLAN 99) carries them between the switches.

- Same-VLAN hosts communicate across the trunk.
- Different-VLAN hosts stay isolated because no Layer 3 device connects them.

### 2. Spanning Tree Protocol (STP)
Three switches are connected in a triangle (FastEthernet, cost 19). The project shows:

- Root bridge election by the lowest Bridge ID (priority, then MAC)
- Root port, designated port and blocked port selection
- How to make a chosen switch the root with `spanning-tree vlan 1 priority 4096`

### 3. EtherChannel (LACP) and Port Security
- **EtherChannel:** Fa0/23 and Fa0/24 are bundled into Port-channel 1 using LACP, so STP no longer blocks a link and traffic keeps flowing if one cable fails.
- **Port security:** Fa0/1 allows a maximum of 2 sticky MAC addresses. A third device triggers a violation and the port goes **err-disabled**.

## Features

- Cover page with university, team and course details
- Animated walkthrough for every problem (frames travelling across trunks, STP election, link failure, port violation)
- For each problem: **What is the problem?**, **How it works**, **How to solve it (steps)**
- Key Cisco IOS commands and verification commands on each slide
- Animated "Thank You" ending slide
- Keyboard navigation (left and right arrow keys) and Prev / Replay / Next buttons
- Light and dark mode support, responsive on phones and desktops

## Project Structure

```
.
├── switching_animated.html   # Animated slide deck (open in any browser)
├── Switching_Project.pptx    # Static PowerPoint version of the project
└── README.md
```

## How to Run

No installation or build step is needed.

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```
2. Open `switching_animated.html` in a web browser (double-click it, or run `open switching_animated.html` on macOS / `start switching_animated.html` on Windows).
3. Use the **Next / Prev / Replay** buttons or the arrow keys to move through the slides.

To hold the presentation on GitHub Pages, enable **Settings > Pages**, choose the main branch, and rename `switching_animated.html` to `index.html`.

## Key Commands Used

```text
! VLANs and trunking
vlan 10 / name Sales
interface fa0/1
 switchport mode access
 switchport access vlan 10
interface gi0/1
 switchport mode trunk
 switchport trunk native vlan 99

! STP
spanning-tree vlan 1 priority 4096
show spanning-tree vlan 1

! EtherChannel
interface range fa0/23 - 24
 channel-group 1 mode active
interface port-channel 1
 switchport mode trunk
show etherchannel summary

! Port security
interface fa0/1
 switchport port-security
 switchport port-security maximum 2
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
show port-security interface fa0/1
```

## Tools and Technologies

- HTML, CSS and JavaScript (single file, no external libraries)
- SVG for the network animations
- Cisco IOS CLI / Cisco Packet Tracer for the configurations

## Testing the Configurations

The configurations can be built and tested in **Cisco Packet Tracer** using the topologies described in the slides. Use the verification commands (`show vlan brief`, `show interfaces trunk`, `show spanning-tree`, `show etherchannel summary`, `show port-security`) to confirm the expected results.

## License

This project was created for academic purposes at Uttara University. Add a license of your choice (for example MIT) if you wish to share it publicly.
