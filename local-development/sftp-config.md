---
parent: Local Development
title: SFTP Config
nav_order: 2
---
# Create SFTP Config
Create a text file at `docker-compose/sftp-config` (no file extension) with the SFTP credentials.
If you have started the Util container before creating this file, there will be a folder in its place.
Exit the Util container and replace the folder with the text file.

The credentials should be in the shared LastPass folder. If not, you may need to [create a new SFTP user](/wpengine/add-sftp-user).

The sftp-config file should be in this format:
```sh
ENV=DEV

if [ $ENV = PROD ]; then
  HOSTNAME=
  USERNAME=
  PASSWORD=''
elif [ $ENV = STAGE ]; then
  HOSTNAME=
  USERNAME=
  PASSWORD=''
elif [ $ENV = DEV ]; then
  HOSTNAME=
  USERNAME=
  PASSWORD=''
fi
PORT=2222
```

When using this file, make sure you set the `ENV` variable to the corresponding environment.
Do not include spaces around the `=`.

The password is in `'single quotes'` to avoid issues with special characters.

Next step: [Start Local WordPress](/local-development/start-wordpress)
