---
parent: Access
title: Generate an SSH Key
nav_order: 1
---
# Generate an SSH Key

See the GitHub documentation on [Checking for existing SSH keys](https://help.github.com/en/github/authenticating-to-github/checking-for-existing-ssh-keys) and [Generating a new SSH key](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

## Submit Your Public Key

You should now have public and private key files.

The _private key_ is found in the `id_rsa` file. **Anyone who has a copy of this file has access to everything you have access to** via the SSH key system, so this should only exist on your computer and **not be shared, copied, or stored elsewhere**.

The _public key_ is found in the `id_rsa.pub` file. This is needed to give you access to things and can be freely shared. Copy the contents of `id_rsa.pub` to the [SSH Keys document](https://docs.google.com/document/d/18f2wRxvz3h4fRB6XDwiAOWtG9yAR9olstZruN3ppMRY) and let your Mangrove contact know it's ready.
