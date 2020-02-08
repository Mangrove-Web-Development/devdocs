# Using Git

## Making it Easier
Git is very confusing, so feel free to ask other devs about it when something
doesn't make sense. Also, GUI software can make things easier:

* [Fork](https://git-fork.com/) (Mac/Windows)
* [SourceTree](https://www.sourcetreeapp.com/) (Mac/Windows)
* [GitUp](https://gitup.co/) (Mac)
* [Tower](https://www.git-tower.com/mac) (Mac)

## Merging Code
Code should be merged using the `git merge` feature. Merging can often be a
confusing procedure, so using the merge open in Git GUI software can be helpful.

Do not copy changes from one branch and commit them on another separately. This
makes it look like the codebases are different when they are not, which makes
it hard to understand the status of a project.

## Git Ignore
Instead of ignoring files and folders specifically, newer projects ignore everything, and then you must unignore your project folders.  This helps avoid accidentally adding non-project files to the repository.

To unignore a directory, you prepend the line in .gitingore with a !.  However, if the parent directory is ignored, this will not work, so you must unignore all ancestor directories as well, and ignore all the other directories in the ancestors.

```
/*                              # ignore all files and folders in the repo directory

!/wp-content                    # unignore /wp-content directory
/wp-content/*                   # ignore all files/folders in /wp-content
!/wp-content/themes             # unignore themes directory
/wp-content/themes/*            # ignore all themes
!/wp-content/themes/your-theme  # unignore your theme
```
