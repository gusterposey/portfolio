

## Overview
This project involved migrating my home network firewall from a pfSense setup on an older desktop PC to a dedicated low-power OPNSense appliance. The goal was to improve efficiency, reduce power consumption, and ensure seamless transfer of configurations like FQ-CoDel AQM, DNS servers, and static IP assignments. This upgrade optimized my symmetrical gigabit connection for low-latency activities, such as gaming.

- **Key Outcomes**: Reduced continuous power load by ~40W (from ~50-60W on the old PC to ~10-20W on the appliance). Achieved maximum speeds of 888 Mbps down / 890 Mbps up with AQM overhead, with better overall performance and stability.
- **Tech Stack**: pfSense (legacy), OPNSense, Intel-based mini-PC (Celeron J4125 with 4x Intel i-226-V 2.5GB ports), eMMC SSD, RAM upgrade.
- **Duration**: 1-2 weeks, including planning, migration, and testing.
- **Relevance**: Demonstrates network migration, configuration management, and optimization skills—applicable to IT support, systems administration, or infrastructure roles.

## Motivation
My original pfSense ran on an eBay-sourced office PC (Intel i5-2500 CPU, 4GB DDR3 RAM, HP NC364T 4-port NIC). It worked reliably but had issues like worn RJ45 ports, tightly bent Ethernet cables causing packet loss, and coil whine from the NIC. Power draw was higher than it should have been, and I wanted a purpose-built appliance for better efficiency and performance on my gigabit connection.

## Steps Taken
1. **Hardware Preparation**:
   - Purchased a barebone router-style mini-PC with Celeron J4125 CPU and 4x 2.5GB Intel ports.
   - Added RAM and an eMMC SSD for OPNSense installation.
   - Installed OPNSense via USB bootable image and booted the appliance.

2. **Backup and Export**:
   - Backed up the full pfSense configuration as an XML file (including NAT rules, static IPs, DNS servers, port forwards, and FQ-CoDel AQM settings).

3. **Migration**:
   - Imported the pfSense XML config into OPNSense.
   - Verified all settings transferred correctly: FQ-CoDel AQM enabled, preferred DNS servers set, static IP assignments intact.
   - Adjusted any minor incompatibilities (e.g., OPNSense-specific tweaks for AQM parameters).

4. **Testing and Optimization**:
   - Monitored network performance using tools like speed tests and bufferbloat checks (via waveform.com tools).
   - Confirmed symmetrical gigabit speeds: Max stable at 888 Mbps down / 890 Mbps up for AQM overhead.
   - Ensured no interruptions to hosted services or internal network.

5. **Power and Performance Validation**:
   - Measured power draw with a watt meter: Dropped ~40W continuously compared to the old PC.
   - Noted improved stability and lower heat/noise from the dedicated appliance.

## Challenges and Solutions
- **Challenge**: Potential config incompatibilities during XML import (e.g., AQM or DNS nuances between pfSense and OPNSense).
  - **Solution**: Manually verified and reconfigured key settings post-import—took ~1 hour of testing to ensure FQ-CoDel was active and effective.
- **Challenge**: Ensuring no downtime during switchover.
  - **Solution**: Tested the new appliance in parallel before swapping it into production; monitored for packet loss or latency spikes.
- **Challenge**: Hardware-specific issues from the old setup (e.g., NIC coil whine, worn connectors).
  - **Solution**: The new appliance eliminated these inherently; no migration needed.

## Network Topology

- 

## Lessons Learned
This migration highlighted the benefits of dedicated appliances for efficiency and reliability. It also reinforced troubleshooting fundamentals, like verifying configs layer by layer. Power savings alone made it worthwhile, and the process prepped me for similar enterprise migrations.