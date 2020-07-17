---
title: Sync Site Data
parent: Local Development
nav_order: 4
---

# Sync Site Files and Database

## The Util Container
The simplest way to sync down a site is with the command line tools in the Util container.

To enter the Util container:
```bash
docker-compose run util
```
You command line is now within the Util container.
To exit the container and return to your normal terminal,
use the `exit` command.

### Downloading Resources
The following `download` commands require the [SFTP config file](sftp-config).
These commands work for both single and Multisite installs.

```sh
download-plugins
download-uploads
download-db
```
### Importing the Database
To work with the database,
your local development services need to be running.

At the root of your project directory:
```sh
docker-compose up -d
```

#### Single Site WordPress
```sh
import-db
```

#### Multisite
```sh
multisite-import-db
```

You may get this error in WP-Admin:
```
wp_check_site_meta_support_prefilter was called incorrectly.
```
In that case, within the Util container:

```sh
wp network meta set 1 site_meta_supported 1
```

## Alternatives
[WIP] Site files can also be downloaded and imported manually with any SFTP client. Migrate DB Pro can also be used.

## Next
[Compile SASS and JavaScript.](/local-development/css-javascript)
