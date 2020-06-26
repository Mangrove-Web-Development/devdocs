---
nav_order: 10
title: Troubleshooting
has_children: false
has_toc: false
parent: WPEngine
---
# WPE Troubleshooting

## No or Broken Changes After Git Deploy
From the [WPEngine documentation][WPEDoc]:
> The deployment end of the Git push process will only remove files from your application that
> you have also removed from your repository.
> [...]
> If a file never existed in your repository at all,
> it won’t be removed from either your live or staging application.

This means that if a file is added to the server by something other than Git,
for example via SFTP,
it will most likely remain on the server unless manually removed.
The most common and confusing occurrence of this is with with WPE's environment cloning feature.

### WPE Clone and Git
WPE cloning works completely independently of WPE's Git integration.
When an environment is cloned, the Git repositories for both environments are unaffected,
and the repositories are unaware of the file changes.
Because of this, the Git repository for the destination environment will almost certainly be
out of sync with the files in the environment after a clone operation.

The Git repo of the destination environment will not be aware of any files from the source
environment that do not happen to have a tracked file in the latest commit at the exact same
location.
Therefore, these files will not be removed on the next git push.
While not ideal, these leftover files usually do not cause a problem,
except within the theme `dist` directory.

Extra files in the `dist` directory may be loaded instead of the intended file,
causing CSS or JS updates not to appear even after they have been pushed and deployed.

#### To fix this:
1. Log into the environment via SFTP and delete the `dist` directory.
1. Git push to WPE to deploy the latest files.

### Pushing Without More Changes
If you have already pushed a commit,
you cannot push that same commit on the same branch to re-deploy.
You can either make another change and push a new commit,
or you can create a new branch at the same commit and push the new branch.
Once the new branch has deployed to WPE, you may delete that branch.

[WPEDoc]: https://wpengine.com/support/git/#Removing_Files_with_Git_push
