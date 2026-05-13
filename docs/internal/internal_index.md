---
layout: default
title: SMB Projects
nav_enabled: true
nav_order: 0
---
# Internal Documents

## BlueBotPC

Enabling Growth thru Strategic IT Infrastructure Engineering. Founded 2017.

## GR Host

Hosting and Managed Cloud Services. Founded 2023.

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
