---
title: CSS and JavaScript
parent: Local Development
nav_order: 5
---
# Editing CSS and Javascript

Theme JavaScript and SASS source files are compiled using Node Webpack.

Use the `node` container to compile these files.

## Source Files 
JavaScript source files are found in the `theme/js` directory.

[WIP] How to add more primary JS files.

SCSS source files are found in the `theme/sass` directory.

[WIP] How to add more primary SCSS Files.
## Output Files
Compiled CSS and JS files are output to the `theme/dist` directory. These _are_ tracked in Git, so they will appear as changed whenever they are recompiled. Commit these changes.

## Node Container
The node container opens a command line starting in your theme directory. This path is controlled by the `docker-compose.yml` file under `volumes:` ending with `:/theme`.

By default, there is a `global.js` file that is enqueued for the entire site front-end. Any JavaScript for specific areas of the site should be added to new `.js` files in the `js` directory. These will automatically be detected by the compile commands (after you restart the command).

```sh
docker-compose run --service-ports node # start the node container
npm install # installs node modules
npm run help # lists available commands
exit # ( exit container )
```


## Node Container Commands
Commands in the node container are node scripts which can be found in `package.json`. To run these commands, use the format:

```sh
npm run commandname
```

### Commands
For convenience, some commands have aliases that can be used interchangeably. E.g. `npm run dev` and `npm run develop` do the same thing.


- `build`
- `production`
    - Compiles SASS and JavaScript for production use. Run this command and commit output files before any production deploys.
- `watch`
    - Use this instead of `develop` if you are on Windows. Windows does not report file change like Mac and other Unix-like systems do, so polling is used instead for compatibility.
- `dev`
- `develop`
    - Watches source SCSS and JavaScript files for changes and compiles for development.  
    When changes are detected, files are recompiled and the browser is automatically refreshed.

## Next
That should be about all you need to get started on your project!

You might want to read about the [additional features](/local-development/features)
available in the local development setup,
or get a better understanding of [Docker and how it works](/docker/).
