---
nav_order: 7
title: LargeFS
has_toc: false
parent: WPEngine
---
# WPE LargeFS
This documentation is focused on clarifying technical details about how LargeFS works and the required setup. For references regarding client policies and communication, see
[WPEngine Storage](https://docs.google.com/document/d/1sC4xnyUOczMkwwgOxYrgLZS-dA0wmN86aWlg8pmUXes).

## What it’s for
LargeFS is a system to move the `uploads` folder content to AWS S3 storage,
freeing up server disk space.

## How it works for PROD
- Media uploads are uploaded to the WPEngine server as usual.
- Periodically, an automatic system will copy uploads from the WPE server to the S3 bucket,
    and delete them from the WPE server.
- All future requests for the file will be served from the S3 bucket.
    This happens through the WPE NGINX layer, so file URLs remain unchanged.

## How it ___should*___ work for other environments
Note: using ENV here in place of actual environment labels, e.g. STAGE or DEV
- Any files still on the WPEngine server will be copied to ENV as usual.
- ENV should also be setup with the NGINX layer that refers to the S3 bucket for files
    not in the WPE uploads folder.
- ENV should not have the service that copies files to the S3 bucket.
    Any files uploaded to ENV should stay on the ENV install and not be available to
    PROD or other environments.

## Setup
- Review the AWS SOPs document for current details on how to setup AWS access.
- The S3 bucket should generally be configured on a client-owned AWS account.
- Chat with WPE support* about setting up LargeFS.  
    __*Not all technicians have a deep understanding of how LargeFS works__.  
    Make sure they set up PROD with the copy-to-S3 system, and other environments without that.
- If LargeFS is setup on PROD, and PROD is copied to a new environment,
    I don’t know if the LargeFS will be properly configured on the new environment.
    This should be tested, and this document updated.

## Sites Using LargeFS
- Mangrove-web.com
    - Account: wpengine
    - Bucket: heritagelargefs
    - Folder: mangrove
- Other LargeFS setups should be confirmed and documented here.

## Migrating Servers
Migrating an install from one server to another will break the LargeFS setup.
Chat with WPE support to make sure they set it up again properly after moving an install.

## Backups
Files offloaded from the WPE server to AWS using LargeFS do not get included
in the WPE automated backups.
Make sure clients are aware that their media files are not automatically backed up when
using LargeFS.
We manually backup all S3 buckets on the billing@mangrove-web.com Backblaze account.
