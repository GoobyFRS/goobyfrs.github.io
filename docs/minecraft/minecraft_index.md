---
layout: default
title: Minecraft
nav_enabled: true
nav_order: 0
color_scheme: dark
---
# Minecraft at Home

[Minecraft Wiki](https://minecraft.wiki/) - Official Wiki

[MultiMC](https://multimc.org/) - Multi-Platform launcher

[Corretto](https://aws.amazon.com/corretto/) - Preferred Linux JRE - [Ninite](https://ninite.com/) - Easy Windows Java Source

[Seed Map](https://www.chunkbase.com/apps/seed-map) - [Custom World Preset Generator](https://minecraft.tools/en/custom.php)

[Startup Script Generator](https://docs.papermc.io/misc/tools/start-script-gen/) - [Aikars Flags](https://docs.papermc.io/paper/aikars-flags/) - Start Up Flags Comments

## Technical Notes

- Minecraft ≥ 26.1 and above requires Java 25.
- Minecraft ≥ 1.20.5 and 1.21.11 requires Java 21.
- Minecraft ≥ 1.18 requires Java 17.
- Minecraft ≥ 1.12 requires Java 8.

Older versions of Minecraft can run on newer Java, for example, Minecraft 1.16 can run on Java 17, Minecraft 1.18 can run on Java 20, etc.

[**Oracle OS Firewall Fix**](https://discourse.cubecoders.com/t/using-amp-on-oracle-cloud/2307): Execute as ```root```.

```bash
apt purge ufw
iptables -L INPUT --line-numbers
...
6 REJECT  All  -- anywhere   anywhere   reject-with icmp-host-prohibited
```

Remove the REJECT and save the rules. You can now re-install ufw.

```bash
iptables -P INPUT DROP
iptables -D INPUT 6
iptables-save > /etc/iptables/rules.v4
```

## Discord

[Invite Link](ge6necsyxR)

- ```welcome```: Welcome Info and Rules
- ```announcements```: Community Announcements
- ```community```: Group Chat
- ```birdhousemc```: Minecraft Server Cross Chat
- ```bot-spam```: Tatsu Bot Channel
- ```memes-n-nsfw```: NSFW content MUST go here.
- ```tech-alerts```: Private Channel
