# Node-RED Dokku

This repository can be deployed to a Dokku instance.

## Quick Start

[Install Dokku](https://dokku.com/docs/getting-started/installation/) on the intended host.

Install the [dokku-letsencrypt](https://github.com/dokku/dokku-letsencrypt) plugin.

Create the app and attach a data directory.

```bash
dokku apps:create node-red
dokku storage:ensure-directory node-red-data --chown heroku
dokku storage:mount node-red /var/lib/dokku/data/storage/node-red-data:/data
```

Deploy NODE-Red

```bash
git push production main
```
