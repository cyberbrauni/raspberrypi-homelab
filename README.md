# Raspberry Pi Home Lab

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Platform](https://img.shields.io/badge/Platform-Raspberry%20Pi-red)
![Docker](https://img.shields.io/badge/Docker-Docker%20Compose-blue)
![Service](https://img.shields.io/badge/Service-Pi--hole-green)
![Network](https://img.shields.io/badge/Network-DNS%20Filtering-purple)
![Last Commit](https://img.shields.io/github/last-commit/cyberbrauni/raspberrypi-homelab)

## Description
A self-hosted homelab built on a Raspberry Pi 4 using Docker Compose. The project combines network-wide DNS filtering (Pi-Hole), centralized file storage (Samba), and secure remote access to the home network (WireGuard VPN).

## Features
- Pi-hole: Network-wide DNS filtering and domain blocking.
- Samba NAS: Shared file storage accessible from devices on the local network.
- WireGuard VPN: Encrypted remote access to the home network.
- Docker Compose: Containerized services with persistent configuration.
- Remote DNS filtering: Configured VPN clients use Pi-hole for DNS queries.
- Split-tunnel VPN: Only home-network traffic is routed through the VPN; other internet traffic uses the client's regular connection.

## 1. Pi-hole — DNS Filtering

Pi-hole provides DNS-based domain blocking for supported devices on the home network.

Implemented:

- Deployed Pi-hole using Docker Compose.
- Configured persistent storage for Pi-hole settings and DNS configuration.
- Configured the Raspberry Pi as the network's DNS server.
- Added blocklists for domain-based filtering.
- Tested DNS resolution and confirmed that blocked test domains resolve to 0.0.0.0.
- Configured WireGuard clients to use Pi-hole for DNS queries.

Limitations:

- DNS-based filtering does not block every advertisement, including many ads delivered from the same domains as regular content.
- Devices configured to use alternative DNS servers or certain encrypted DNS services may bypass network DNS filtering.

## 2. Samba — Network-Attached Storage

Samba provides shared file storage accessible to authorized devices on the home network.

Implemented:

- Deployed Samba in a Docker container.
- Configured a host directory for persistent shared files.
- Published the SMB service on the local network.
- Verified access to the share from an Android device over WireGuard.

The Samba service remains accessible through the home network and VPN. SMB ports are not intentionally forwarded from the public internet.

## 3. WireGuard — Secure Remote Access

WireGuard provides encrypted remote access to the home network.

Implemented:

- Deployed WireGuard using Docker Compose.
- Configured the server to listen on UDP port 51820.
- Created separate client profiles for an Android phone and a laptop.
- Configured split-tunnel routing for the home LAN and VPN subnet.
- Configured Pi-hole as the DNS server for VPN clients.
- Configured router port forwarding to the Raspberry Pi.
- Connected an Android phone over mobile data and verified a successful WireGuard handshake.
- Confirmed remote access to the Pi-hole web interface and Samba share.

## Security Considerations

Security was considered when configuring remote access.

- Only the WireGuard UDP port is forwarded from the router to the Raspberry Pi.
- Samba ports 139 and 445 are not intentionally exposed to the public internet.
- VPN clients use individual peer configurations.
- VPN configuration files and private keys must remain private.
- Service configuration and persistent data are stored separately from container images.
- Firewall rules and remote access should be reviewed when services or network requirements change.

## Lessons Learned

This project provided practical experience with:

- Linux system administration and command-line troubleshooting.
- Docker containers, Compose files, persistent volumes, and container networking.
- DNS resolution, blocklists, and network-wide filtering.
- SMB file sharing and remote file access.
- VPN configuration, routing, and NAT port forwarding.
- Testing network services and verifying connectivity through logs and command-line tools.
- Applying basic security practices to self-hosted services.

## Status
The project is completed.
