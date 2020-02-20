---
parent: Local Development
title: SFTP Config
---
# Create SFTP Config
Create a text file at `docker-compose/sftp-config` (no file extension) with the SFTP credentials. The credentials should be in the shared LastPass folder. If not, you may need to [create a new SFTP user](/wpengine/add-sftp-user).


```sh
HOSTNAME=
USERNAME=
PASSWORD=''
PORT=2222
```

Note: place password in `'single quotes'` to avoid issues with special characters
