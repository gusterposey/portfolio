# Proxmox Homelab Setup: Virtualization, Media Server, and AI Integration

## Overview
This project documents my Proxmox-based homelab, starting as a simple virtualization host for storage and evolving into a full media management and AI system. It includes HBA passthrough for TrueNAS storage, a Windows VM for media servers (Plex and Jellyfin) with GPU transcoding, Docker containers for AI tools, and an arr suite integrated with qBittorrent for automated downloads. Services are securely exposed via a Caddy LXC container.

- **Key Outcomes**: Reliable RAIDZ1 storage for SMB shares, dual media servers with GPU-accelerated transcoding, local LLM capabilities, and automated media organization with VPN-protected downloads. Handles family TV compatibility and low-latency access.
- **Tech Stack**: Proxmox (host), TrueNAS (storage VM), Windows 10 (media VM), NVIDIA RTX 4060 Ti (GPU passthrough), Docker Desktop (for Ollama/OpenWebUI, arr apps, qBittorrent), Jellyfin/Plex, Sonarr/Radarr/Prowlarr, qBittorrent (with NordVPN integration), Caddy (reverse proxy with Let's Encrypt/Cloudflare tunnel).
- **Host Hardware**: Ryzen 7 1700 CPU (8 cores/16 threads), ASUS Prime B350 Motherboard, 64 GB DDR4 RAM. Overcame IOMMU group limitations with ACS override for HBA/GPU passthrough.
- **Duration**: Ongoing evolution over several months, with key upgrades like GPU integration taking 1-2 weeks.
- **Relevance**: Showcases virtualization, hardware passthrough, containerization, and service deployment—skills applicable to IT infrastructure support, systems administration, or media/networking roles.

## Motivation
Initially, I set up Proxmox solely for a TrueNAS VM using a single 4TB WD drive as a virtual disk for basic SMB shares. As needs grew (e.g., media streaming for family Samsung Tizen TVs), I expanded to proper HBA-passthrough storage, added a Windows VM for reliable media servers (after Plex plugin errors on TrueNAS), integrated GPU transcoding, and layered on AI/media tools via Docker. The goal was a self-contained system for storage, streaming, and local LLM experimentation without cloud reliance.

## Steps Taken
1. **Initial Proxmox Setup**:
   - Installed Proxmox on the Ryzen 7 1700 host with ASUS B350 motherboard and 64 GB RAM.
   - Created a TrueNAS VM with a single 4TB WD drive passed as a virtual disk for basic SMB shares.

2. **Storage Upgrade with HBA Passthrough**:
   - Updated BIOS on the B350 Motherboard for better IOMMU grouping and ACS override potential.
   - Enabled ACS override in Proxmox to enable better IOMMU grouping for proper PCIe device isolation.
   - Passed through an HBA controller to the TrueNAS VM.
   - Added 3x 6TB WD Red HDDs, configured as RAIDZ1 array in TrueNAS for resilient SMB shares.

3. **Media Server VM**:
   - Plex plugin on TrueNAS errored repeatedly, so created a Windows 10 VM (allocated 4 cores/8 threads and 32 GB RAM—half the host resources).
   - Installed Plex on the VM; later added Jellyfin, but kept Plex running in parallel for better compatibility with Samsung Tizen TVs (shares the same media library).
   - Added Zotac NVIDIA RTX 4060 Ti 16GB GPU; remade VM from i440fx to Q35 machine type to enable PCIe passthrough (i440fx limited to PCI, causing issues).
   - Configured NVENC for hardware-accelerated encoding and transcoding in Plex/Jellyfin.

4. **Docker and Additional Services**:
   - Installed Docker Desktop on the Windows VM.
   - Set up Ollama and OpenWebUI containers for local LLM (leveraging the 4060 Ti's 16 GB VRAM for fast inference—resolved GPU integration pains through trial/error).
   - Added Sonarr, Radarr, and Prowlarr for automated media organization and indexing.
   - Integrated qBittorrent with the arr suite for auto-downloads (e.g., searching a show in Sonarr triggers qBittorrent). Configured qBittorrent's built-in VPN dependency to ensure it only runs while connected to NordVPN, preventing leaks. Exposed qBittorrent internally for network access..

5. **Service Exposure**:
   - Created an LXC container for Caddy reverse proxy.
   - Configured Caddy with Let's Encrypt for TLS and a Cloudflare tunnel for secure external access to Jellyfin (pointed to a personal URL).
   - Ensured no exposure risks by verifying firewall rules in OPNSense.

## Challenges and Solutions
- **Challenge**: IOMMU group limitations on B350 chipset blocked clean HBA/GPU passthrough.
  - **Solution**: Updated BIOS for motherboard. Enabled IOMMU optimizations and ACS override. Enabled ACS override in Proxmox kernel parameters; tested isolation with `lspci -vv` commands.
- **Challenge**: Plex plugin errors on TrueNAS; inefficient Windows VM for media.
  - **Solution**: Switched to Windows VM for stability; allocated half host resources to balance performance (not ideal efficiency, but functional).
- **Challenge**: GPU integration with OpenWebUI in Docker Desktop.
  - **Solution**: Trial-and-error configs (e.g., NVIDIA drivers in VM, Docker GPU flags); remade VM to Q35 for proper PCIe support.
- **Challenge**: Secure external exposure for Jellyfin without vulnerabilities.
  - **Solution**: Used Caddy LXC with Cloudflare tunnel and Let's Encrypt—zero direct ports open.
- **Challenge**: Ensuring qBittorrent only runs with VPN active.
  - **Solution**: Leveraged qBittorrent's built-in VPN dependency settings; integrated seamlessly with arr suite for automated, protected downloads.

## Lessons Learned
This setup taught me the value of passthrough for performance (e.g., native RAIDZ1 vs. virtual disks) and the trade-offs of Windows VMs for compatibility. GPU acceleration transformed media/AI tasks, and tools like the arr suite + qBittorrent streamlined organization with built-in safety. Overall, it honed my virtualization and container skills for scalable homelabs.

## Visuals
![Proxmox Dashboard](https://github.com/gusterposey/portfolio/blob/main/proxmox.png?raw=true "Proxmox Dashboard")
![TrueNAS Hardware](https://github.com/gusterposey/portfolio/blob/main/truenas.png?raw=true "TrueNAS Hardware")
![Windows 10 VM Hardware](https://github.com/gusterposey/portfolio/blob/main/windowsvm.png?raw=true "Windows 10 VM Hardware")
