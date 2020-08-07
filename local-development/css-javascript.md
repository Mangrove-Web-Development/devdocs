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

By default, there is a `global.js` file that is enqueued for the entire site front-end. Any JavaScript for specific areas of the site should be added to new `.js` files in the `js` directory. These will automatically be detected by the compile commands (after you restart the command).

[WIP] How to add more primary JS files.

SCSS source files are found in the `theme/sass` directory.

[WIP] How to add more primary SCSS Files.
## Output Files
Compiled CSS and JS files are output to the `theme/dist` directory. These _are_ tracked in Git, so they will appear as changed whenever they are recompiled. Commit these changes.

## Node Container
The node container opens a command line starting in your theme directory. This path is controlled by the `docker-compose.yml` file under `volumes:` ending with `:/theme`.

To start the node container:
```sh
docker-compose run --service-ports node
```

### yarn vs npm
Node packages and scripts are managed using either the [yarn](https://yarnpkg.com)
or [npm](https://www.npmjs.com) command line tools.

npm was used for older projects, but we have migrated to using yarn due to compatibility issues
with npm and Windows.

To see if a project is using yarn or npm, check for the package lock file.

- yarn: `yarn.lock`
- npm:  `package-lock.json`

If a project is still using npm,
you may continue using npm on that project,
or update the project to use yarn:

- Delete `package-lock.json`
- Update `package.json` with yarn commands
- Delete `node_modules`
- `yarn install` and continue development with yarn.

### Node Scripts
Node scripts are defined in `package.json`.
Run these scripts with:
```sh
yarn run scriptname
```
or
```sh
npm run scriptname
```

For convenience, some scripts have aliases that can be used interchangeably.
E.g. `yarn run dev` and `yarn run develop` do the same thing.


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
