---
title: Setup Git
parent: Local Development
nav_order: 1
---
# Git
Make sure your Git Push user is already set up, as shown in the [access documentation](/access).

Now you can [add your SSH Key](/wpengine/add-git-key) to the project you are working on. Once you have added your key, it can take several minutes for access to be granted.

## Multiple Environments
Your site may have multiple environments on WPEngine.
See the [WPE Environemts](/wpengine/#environments) documentation if you're not sure what that means.
If there are multiple, add all of them as remotes to the same local git repository, and name them accordingly so you can easily keep track of them.

## Clone the First Repository
Start by cloning a single environment.

To get the repository URL, go to [my.wpengine.com](https://my.wpengine.com/) and select the environment you want to clone. Click "Git Push" in the left menu. In the bottom right, you fill find the Git URL for that install.

**Important note**: There are two Git URLs listed for each environment. _Always_ use the top
`git@git.wpengine.com:production/installname.git`
URL, and _never_ the
`git@git.wpengine.com:staging/installname.git`
URL, even if you are working on a staging environment. The second URL is for the [legacy staging system](/wpengine).

![Screenshot showing where to find Git URL](git-url.png)

## Rename the Remote
When you have cloned the remote environment, it will be connected to your local repository as a remote named `origin`.
Rename this remote according to the environment, e.g. `prod`, `stage` or `dev`.

Your Git GUI should allow you to rename remotes. You can also use the git command:

```sh
git remote rename origin envname
```

## Add the Other Repositories
Once you have a local git repository, add the other environments as additional remotes. Name those remotes accordingly.

Your Git GUI should allow you to do this. You can also use the git command:
```sh
git remote add remotename remoteurl
```

Now `git fetch --all` to see the latest branches on all remotes.

Your Git GUI should now show all remotes and remote branches, something like this:

![Git GUI showing prod and stage remotes](git-remotes.png)

Next step: [Add SFTP Config](/local-development/sftp-config)
