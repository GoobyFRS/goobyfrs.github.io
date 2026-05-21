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

## Monitoring

None at this time.

### Setup

Create a ```start.sh``` with the following content...

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
