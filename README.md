# Cloudflare backup via GitHub Actions
Cloudflare scheduled backup of all zones and records via Github Actions

[![Zones](https://github.com/fabriziosalmi/cloudflare/actions/workflows/zones.yml/badge.svg)](https://github.com/fabriziosalmi/cloudflare/actions/workflows/zones.yml) [![Records](https://github.com/fabriziosalmi/cloudflare/actions/workflows/records.yml/badge.svg)](https://github.com/fabriziosalmi/cloudflare/actions/workflows/records.yml) 

## Features
- Scheduled backup to json files
- Backup all account zones
- Backup all zones records

## How to use it

1. Clone the repository
2. ⚠️ Set repository to **private** 
3. Enable GitHub Actions if disabled
4. Create a token on [Cloudflare dashboard](https://dash.cloudflare.com/profile/api-tokens) with read all resources permissions (quick way) or specific zones permissions
5. Setup `CLOUDFLARE_API_TOKEN` as action repository secret (url format: https://github.com/user/repo/settings/secrets/actions)
6. Setup scheduled cronjob on the zones.yml action like this bu uncommenting it:

```
on:
  schedule:
    - cron: '0 2 * * *'
  workflow_dispatch:
```

6. Records backup will be executed only after a successful zones backup
7. Enjoy automated backups via GitHub Actions ^_^
