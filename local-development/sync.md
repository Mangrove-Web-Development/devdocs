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

You may get this error in WP-Admin:
```
wp_check_site_meta_support_prefilter was called incorrectly.
```
In that case, within the Util container:

```sh
wp --allow-root network meta set 1 site_meta_supported 1
```

## Alternatives
[WIP] Site files can also be downloaded and imported manually with any SFTP client. Migrate DB Pro can also be used.
