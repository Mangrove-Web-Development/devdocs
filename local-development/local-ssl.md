---
title: Local SSL
parent: Local Development
nav_order: 6
---

# Local SSL
[WIP] This document is a fragment. Need to write complete doc.


## Generate Certificates
*!!!MAC ONLY!!!*
Have not yet tested for Windows.

Use mkcert to generate locally-trusted development certificates.

To create certificates:
```
mkdir ~/cert # make sure cert folder exists
mkcert -cert-file ~/cert/localssl.pem -key-file ~/cert/localssl-key.pem localhost multisite.local myriad2020.wpengine.com
```
