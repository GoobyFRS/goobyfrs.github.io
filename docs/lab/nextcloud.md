---
layout: default
title: Matts Home Cloud
nav_enabled: true
parent: Home Lab
nav_order: 2
---
# Matts Home Cloud

NextCloud is essentially a Self-Hosted Google Photos platform. Allowing me to backup anything (but primarily photo galleries on my phone). I trust my NextCloud instance with my own data. The Application runs in a container inside a IaC deployed Virtual Machine. The Production Data is stored across 2 S3-compatible buckets.

### Limitations

- Slow image load times when browsing large folders in the app or on the web.
- 10 GB Maximum Upload File Size

If you need to upload a singular file larger than 10 GB, we can do it.

Submit a ticket at ```https://support.mattfaulkner.net```

## First Time Setup