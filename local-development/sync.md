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

These commands work for both single and Multisite installs.
```sh
download-plugins
download-uploads
download-db
exit
```

`exit` will exit the container and bring you back to your normal terminal.

The `download` commands require the [SFTP config file](sftp-config).

## Single Site WordPress
```sh
import-db
```

## Multisite
```sh
multisite-import-db
```

## Alternatives
[WIP] Site files can also be downloaded and imported manually with any SFTP client. Migrate DB Pro can also be used.
