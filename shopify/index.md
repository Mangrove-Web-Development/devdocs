---
nav_order: 50
title: Shopify
---

# Shopify Development

## Install Theme Kit
Install [Theme Kit](https://shopify.github.io/themekit/)

## Working on an Existing Project
1. Pull Git repo from BitBucket.
1. Create `config.yml` at the root of your project directory.
    - Copy contents from LastPass (search for **_Store Name_ _Theme Name_ Theme Kit Config**).
1. `theme get --list` to confirm setup is correct.  
    Output should be something like:
    ```sh
    theme get --list
    Available theme versions:
    [163311819][live] debut
    [78911832134] debut 2020 v1
    ```
    Compare the theme ID in `config.yml` to make sure it is not the current `[live]` theme.
1. `theme open` to open the theme preview on Shopify in your web browser.
1. `theme watch` to watch changes to the local theme files and
    automatically upload changes to Shopify.
1. `theme deploy` to make sure Shopify is updated with the exact files in your local directory,
    deleting any extra files from Shopify.
1. Commit and push to Bitbucket!

## Setup New Theme
1. In Shopify, duplicate current live theme (unless starting from scratch/other theme).
    * Rename to __*Theme Name* *Year* v*Version*__. E.g. *Cooltheme 2020 v1*.
1. Create a new private repository on Bitbucket in the Mangrove Client Projects project.
    * Name this repo **_Client Name_ _Theme Name_**.
1. Clone the empty repo to your local development machine.
1. Add a `.gitignore` file with content:
    ```
    config.yml
    ```
1. In your local repo directory:
    1. View a list of all themes in the store with their theme IDs.  
        `theme get --list -p apipassword -s storename.myshopify.com`
    1. Setup the `config.yml` file and download theme files to your local repository.  
        `theme get -p apipassword -s storename.myshopify.com -t themeid`
    1. Commit downloaded theme files and push to Bitbucket.
        * Make sure **not** to commit `config.yml`!
    1. Save the contents of `config.yml` in a LastPass note.
        * Name: *Store Name* *Theme Name* Theme Kit Config.
        * Folder: Shared-Mangrove Client Logins
        * Type: Generic
    1. Edit theme info in `config/settings_schema.json`:
        * theme_name (max. 25 characters)
        * theme_author (max. 25 characters)
        * theme_version
        * theme_documentation_url
        * theme_support_url

## [WIP]
Below are some notes for future documentation. You can safely ignore them.

Get API Key by creating a Private App

Apps > Manage Private Apps > Create New

Name: Mangrove Theme Developer
email: support@mangrove-web.com

Admin API: `Read and write` on `Theme templates and theme assets`.  
    `No access` for all other permissions.

Webhook API Version: latest

No access to storefront data.

Save. 

---
Project Setup

One API Key per account.

Separate Config for each theme.

Save Config to LastPass

Setup Git Repo.

---
Existing Theme Setup

Copy Theme - Rename to _Theme Name Year v1_. E.g. Black Friday Popup -> Black Friday Popup 2020 v1.
