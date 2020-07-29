---
title: phpMyAdmin
parent: More Features
grand_parent: Local Development
nav_order: 2
---
# phpMyAdmin
phpMyAdmin is available at [localhost:8080](http://localhost:8080).

You can login with the `root` or `wordpress` user,
with password `wordpress`,
as set in the `docker-compose.yml` file.

The upload limit for files uploaded to phpMyAdmin is set in bytes by the
`UPLOAD_LIMIT` environment variable on the `phpmyadmin` service
specified in the `docker-compose.yml` file.
