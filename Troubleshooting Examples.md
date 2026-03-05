These real-world examples demonstrate my hardware and network diagnostic skills, often resolving issues that stumped others. They tie into my homelab setups and resume bullets on packet loss, Ethernet fixes, and PC builds.

## Intermittent Packet Loss (Kinked Ethernet Cable)
- **Challenge**: Random packet loss flagged as upstream in pfSense logs; multiple Spectrum tech visits couldn't identify the issue.
- **Diagnosis**: Used PingPlotter and WinMTR for long-term trace routes to isolate hops and confirm it wasn't ISP-side.
- **Solution**: With the ISP's regional supervisor, traced to an Ethernet cable bent too sharply between rooms. Connected a laptop directly to the modem—packet loss vanished. Re-routed and re-terminated the cable.
- **Outcome**: Full gigabit restored. Supervisor gave me his personal email for future issues, noting I "know more than his techs."

## 100 Mbps Link Negotiation Issue (Worn RJ45 Latch)
- **Challenge**: Network stuck at 100Mbps despite gigabit hardware.
- **Diagnosis**: Ruled out duplex settings, drivers, and switch configs.
- **Solution**: Inspected the LAN Ethernet cable. RJ45 latch had worn out and wasn't seating properly. Cut off the bad end and crimped a new connector. (Type-B wired of course)
- **Outcome**: Gigabit speeds restored; highlighted the importance of physical layer checks in troubleshooting.

## Remote PC Builds for Friend (Aero)
- **Challenge**: Guided two remote PC builds over the phone, including compatibility issues on older hardware.
- **First Build (Ryzen 2000 on B350 Motherboard)**: Needed BIOS update for CPU support without a compatible chip; used USB flashback, but system was unplugged mid-process. (I was mortified)
- **Solution**: Proceeded cautiously; system booted successfully into Windows install despite the interruption.
- **Second Build (Ryzen 9000 Series)**: Long initial boot time scared the builder; diagnosed as normal DDR5 memory training on AMD platform.
- **Outcome**: Both systems stable on first boot; demonstrated remote troubleshooting and hardware knowledge.