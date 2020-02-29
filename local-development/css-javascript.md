---
title: CSS and JavaScript
parent: Local Development
nav_order: 5
---
# Editing CSS and Javascript

The JavaScript and SASS files are compiled using Node Webpack.

Use the `node` container to compile these files:

```sh
docker-compose run --service-ports node # start the node container
npm install # installs node modules
npm run help # lists available commands
exit # ( exit container )
```
