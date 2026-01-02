# Pi-hole Setup

## Deployment
- Deployed using Docker Compose
- Exposed ports:
  - 53 (DNS)
  - 80 (Web UI)

## Setting the Admin Password
- After first container start, default password is auto-generated and cannot be retrieved
- Set a new password interactively inside the container:
### Bash:
- docker exec -it pihole /bin/bash
- pihole -a -p
- exit

## Optionally, to disable password:
### Bash:
- docker exec -it pihole /bin/bash
- pihole -a -p ""
- exit

## Verification
Web interface is accessible via http://<raspberrypi_IP>/admin
- can log in using newly set password

## Pi-Hole Dashboard

![Pi-hole Dashboard](../images/pihole-dashboard.PNG)
