---
layout: default
title: Open Source Projects
nav_enabled: true
nav_order: 0
color_scheme: dark
---
# Open Source Projects

[GR_Core](https://github.com/GoobyFRS/GR_Desk) - [Gooby_RCON](https://github.com/GoobyFRS/Gooby_RCON) - [GoobyDesk](https://github.com/GoobyFRS/GoobyDesk)

[Goobs WiFi Scanner](https://github.com/GoobyFRS/Goobs-WiFi-Scanner) - [blocklist](https://github.com/GoobyFRS/blocklist) - [GoobyDDNS_Windows](https://github.com/GoobyFRS/GoobyDDNS_Windows) - [GoobyDDNS_Linux](https://github.com/GoobyFRS/GoobyDDNS_Linux)

### New Server Stand-Up Check List

1. Update & Upgrade
1. Set Timezone
1. Set Hostname
1. Remove snapd
    1. ```sudo apt remove snapd -y```
1. Install packages
    1. ```sudo apt install git curl wget whois python3-full pydf speedtest-cli fail2ban```
1. Setup New Users
1. Enable Auto-Updates
    1. ```sudo dpkg-reconfigure unattended-upgrades```

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw logging on
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow 80/udp
sudo ufw allow https
sudo ufw allow 443/udp
sudo ufw enable
```
