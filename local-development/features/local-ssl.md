---
title: Local SSL
parent: More Features
grand_parent: Local Development
nav_order: 1
---

# Local SSL
For some projects, using HTTPS locally is helpful.
The current docker-compose.yml file in MGTemplate serves at https://localhost
and https://multisite.local in addition to the http URLs by default.
However, it uses a self-signed certificate, which is not allowed by Chrome.

To get https fully working,
you need to mount a locally trusted SSL certificate to the proxy container.

## Generate Certificate with mkcert
mkcert is a command line tool that generates SSL certificates and
installs them so your browsers trust them.
**These certificates are for local development on your machine only!**


**!!!MAC ONLY!!!**  
Contact Jonathan about this for Windows.

Install [mkcert](https://mkcert.dev/).

To create the certificate:
```
mkdir ~/cert # make sure cert folder exists
mkcert -cert-file ~/cert/localssl.pem -key-file ~/cert/localssl-key.pem localhost multisite.local
```
If you have additional domains you want to use for local development,
just append them, space separated, to the above command.

If the command gives you warnings and tells you to "Run "mkcert -install"",
run `mkcert -install`.

## Mount the Certificate
If you're using the latest `docker-compose.yml` file,
there is a `proxy` container with the `cert` volume commented out.
```
volumes:
  # - ~/cert:/cert
```
To mount your certificate, just uncomment that line by removing the leading `#`.

Restart your containers to start using your locally-trusted certificate!
