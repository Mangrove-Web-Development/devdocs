---
title: Start WordPress
parent: Local Development
nav_order: 3
---
# Start WordPress

Open your terminal in the root of your git repository.

`docker-compose up -d` starts server containers in _detached_ mode so your command line stays on your host machine.

It can take some time to start up, especially on the first run.

# Initialize WordPress
You can use the Util container to Initialize either a single-site or Multisite WordPress install.
Alternatively, you can also just use the WordPress installer at [localhost](http://localhost).

## Single Site
To initialize a single site at [http://localhost](http://localhost):

```sh
docker-compose run util # start the Util container.
wp-init # Initialize single-site WordPress.
exit # Exits the Util container.
```
See [WP Util Image Readme] for more details.

## Multisite
To initialize Multisite at [http://multisite.local](http://multisite.local):

```sh
docker-compose run util
multisite-init
exit
```

### Hosts File
For Multisite, you need to edit your hosts file. See the [WP Util Image Readme] for more details.

## Next
Now that WordPress is installed, you can [download the plugins and site data](sync).

[WP Util Image Readme]: https://hub.docker.com/r/rubidot/wputil
