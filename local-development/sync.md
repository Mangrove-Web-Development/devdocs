---
title: Sync Site Data
parent: Local Development
nav_order: 4
---

# Sync Site Files and Database
This must be done _after_ you [Install WordPress](start-wordpress).

## The Util Container
The simplest way to sync down a site is with the command line tools in the Util container.

To enter the Util container:
```bash
docker-compose run util
```

Available commands within Util:

```bash
download-plugins
download-uploads
download-db
import-db
exit
```

`exit` will exit the container and bring you back to your normal terminal.

The `download` commands require the [SFTP config file](sftp-config).

## Alternatives
[WIP] Site files can also be downloaded and imported manually with any SFTP client. Migrate DB Pro can also be used.
