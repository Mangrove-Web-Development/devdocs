---
parent: Local Development
title: SFTP Config
---
# Create SFTP Config
Create a text file at `docker-compose/sftp-config` (no file extension) with the SFTP credentials. The credentials should be in the shared LastPass folder. If not, you may need to [create a new SFTP user](/wpengine/add-sftp-user).


```sh
ENV=STAGE
if [ $ENV = PROD ]; then
  HOSTNAME=
  USERNAME=
  PASSWORD=''
elif [ $ENV = STAGE ]; then
  HOSTNAME=
  USERNAME=
  PASSWORD=''
fi
PORT=2222
```

This text file is a shell script. You can switch between different credentials in the file by changing the `ENV` variable accordingly.

The password is in `'single quotes'` to avoid issues with special characters.
