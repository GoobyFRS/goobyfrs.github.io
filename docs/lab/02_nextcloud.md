---
layout: default
title: Matts Home Cloud
nav_enabled: true
parent: Home Lab
nav_order: 2
---
# Matts Home Cloud (NextCloud)

[GitHub Repo](https://github.com/nextcloud/all-in-one)

- IPv4, IPv6, SDWAN enabled.
- 1 vCPU Cores
- 2 GB Memory
- 50 GB SSD
- S3-compatible Bucket Storage
- Ubuntu Pro Enabled

NextCloud is essentially a Self-Hosted Google Photos platform. Allowing me to backup anything (but primarily photo galleries on my phone). I trust my NextCloud instance with my own data. The Application runs in a container inside a IaC deployed Virtual Machine. The Production Data is stored across 2 S3-compatible buckets.

## Monitoring

- HTTPS Checks from UptimeDawg
- Linode Cloud Manager Alerts Enabled
- NewRelic Agent Installed

### Limitations

- Slow image load times when browsing large folders in the app or on the web.
- 10 GB Maximum Upload File Size

If you need to upload a singular file larger than 10 GB, we can do it.

Submit a ticket at ```https://support.mattfaulkner.net```

## First Time Setup

Not yet defined.
