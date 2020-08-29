---
title: Utilities
parent: Local Development
nav_order: 10
---
# Utilities
Command-line scripts for managing the local WordPress install are provided by the `util` service.
To start a `util` container and access this command line*, run:

```sh
docker-compose run util
```

*_Note for Windows users_: Do **not** use the Cygwin command line.
This can cause errors. Instead, use the standard Windows _cmd_ command line.

## WP-CLI
The complete WP-CLI command line interface for WordPress is available within this container.
See the [public documentation][wpcli] for the complete list of available commands.

[wpcli]: https://developer.wordpress.org/cli/commands/

### Search-Replace
You will most likely need to use the search-replace command:

```sh
wp search-replace oldstring newstring
```
[Full documentation](https://developer.wordpress.org/cli/commands/search-replace/)

## Custom Scripts
Several custom scripts are available for the Mangrove workflow.

### Download Scripts
These scripts require the `sftp-config` file to be setup before the container is started.
See the [sftp-config documentation](local-development/sftp-config) to set that up.
You will most likely use these scripts as part of [syncing your local install](sync).

These commands were written assuming that the remote server is a WPEngine server,
however, they will work with any SFTP server with the same file structure as WPEngine.

```sh
download-plugins
download-uploads
download-db
```

The command line should display information about the transfer soon after the command is run.
If that is not the case, there is an error, and you can kill the process with `ctrl`+`c`.

`download-db` downloads the latest database backup file,
and places it at `/wordpress.sql`, ready for the `import-db` command.

Also available is:
```sh
download-directory /path/on/server/ /var/www/html/path/on/local/
```
to download an arbitrary remote folder.
However, it is unlikely you will need to use this.

### Import Database Scripts
- These scripts import the `wordpress.sql` file at the root of the local project directory.
- Make sure to use the appropriate command for a single vs multisite install.
- If your database file is gzipped (`wordpress.sql.gz`),
    you need to first unzip the file for this to work.

```sh
import-db
multisite-import-db
```

### Init WordPress Scripts
You probably don't need to use these, as you will most likely skip straight to the above import
commands.
However, if you do need to initialize you local WordPress install without importing data,
you can use these scripts to set default values and skip the in-browser install screens.

```sh
wp-init
multisite-init
```
