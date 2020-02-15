---
title: Add a WPE Git Push Key
nav_order: 1
parent: WPEngine
---

# SSH Keys for Git Push
In order to access and push to the git repository for a site, the developer's SSH key must be added to Git Push developers for that site. See [SSH Keys](https://docs.google.com/document/d/18f2wRxvz3h4fRB6XDwiAOWtG9yAR9olstZruN3ppMRY) for Mangrove team SSH keys.

## Adding a New Developer
Always add a new SSH key to the [mangrove install](https://my.wpengine.com/installs/mangrove/git_push) before adding it to any other installs. This will ensure that the developer will be listed as `mangrove-username` instead of `randominstall-username`.


## Adding the Developer to a Site
Once the key is added to the `mangrove` install, it can be added to any installs the developer should have access to.

Go to [my.wpengine.com](https://my.wpengine.com/) > select the install > "Git push".
