---
title: Syncing Installs
nav_order: 5
parent: Workflow
---

# Syncing WordPress Installs

We have access to multiple tools for synchronizing files and data
between separate WordPress installs, each with advantages and disadvantages.

## Migrate DB Pro + Media Addon
See [plugin documentation](/wordpress-plugins/migrate-db-pro) for usage.
### Pros
- This WordPress plugin can be used on virtually any WordPress install.
- Can clone the whole database.
- Can clone select database tables.
- Can copy media files between installs.

### Cons
- It takes significant server resources from both the source and
    destination WordPress installs.
- It is relatively slow, and can take a very long time.
- Excessive resource use and long run times can cause the process to fail.

## WPEngine Copy Environment
### Pros
- Copies the entire database.
- Can copy the complete WordPress install files,
    including plugins, theme, media and core files.

### Cons
- Only works between environments within a single WPE site.
- Cannot select specific tables to copy; completely overwrites destination database.
- Cannot copy only media files; the entire destination install files are replaced.
- Does not coordinate with environment Git repository,
    which can cause issues.
    You may need to [delete the dist folder](/wpengine/troubleshooting).

## WP-Util Container Scripts
### Pros
- Can clone database.
- Can clone media files.
- Can clone plugin files.
- Can directly connect to WPEngine install via SFTP.
- Can import from database (SQL) file.

### Cons
- Only works for syncing the local development environment.

## WordPress Import/Export Tools
### Pros
- Native WordPress functionality available on all installs.
- Can select specific posts/other data to export.

### Cons
- Importing media usually does not work.
- Changes post IDs, which can cause issues.
- Need to manage post authors.

## phpMyAdmin
### Pros
- Generally available with most WordPress hosting.
- Full access to database.

### Cons
- Requires good understanding to use.
- Not specific to WordPress, so lacks WP specific tools.
- Requires manual search-replace.
