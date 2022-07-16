# Node-RED Dokku

A dead simple Node-RED deployment for your friendly local Dokku PaaS.

## Quick Start

### Prerequisites

1. [Install Dokku](https://dokku.com/docs/getting-started/installation/) on the intended host

   ```bash
   wget https://raw.githubusercontent.com/dokku/dokku/v0.27.7/bootstrap.sh;
   sudo DOKKU_TAG=v0.27.7 bash bootstrap.sh
   ```

2. Install the [dokku-letsencrypt](https://github.com/dokku/dokku-letsencrypt) plugin

   ```bash
   sudo dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git
   dokku letsencrypt:cron-job --add
   ```

### Deployment

1. Create the app and attach a data directory

   ```bash
   dokku apps:create node-red
   dokku storage:ensure-directory node-red-data --chown heroku
   dokku storage:mount node-red /var/lib/dokku/data/storage/node-red-data:/data
   ```

2. Configure port mapping, set a domain, and enable SSL.

   ```bash
   dokku proxy:ports-add node-red http:80:1880
   dokku domains:set node-red nodered.your.domain.tld
   ```

3. Deploy repository to Dokku

   ```bash
   git remote add production dokku@host.your.domain.tld:node-red
   git push production main
   ```

4. Configure Node-RED (e.g. set an admin password)

   ```
   nano /var/lib/dokku/data/storage/node-red-data/settings.js
   ```
