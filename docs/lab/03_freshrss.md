---
layout: default
title: FreshRSS
nav_enabled: true
parent: Home Lab
nav_order: 3
---
# FreshRSS

[GitHub Repo](https://github.com/FreshRSS/FreshRSS)

**GoobyRSS is offline at this time.**

- IPv4, IPv6, SDWAN enabled.
- 1 vCPU Cores
- 1 GB Memory
- 8 GB SSD

## Monitoring

None

start.sh

```bash
docker run -d --restart unless-stopped --log-opt max-size=10m \
  -p 8081:80 \
  -e TZ=America/Denver \
  -e 'CRON_MIN=1,31' \
  -v freshrss_data:/var/www/FreshRSS/data \
  -v freshrss_extensions:/var/www/FreshRSS/extensions \
  --name freshrss \
  freshrss/freshrss
```
