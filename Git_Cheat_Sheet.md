# **GIT Cheat Sheet**
---
## Getting Started

| git init                              | Creates a git repository                           |
|---------------------------------------|--------------------------------------------------------------------------|
| git init \<directory>                  | Creates a git repo in specified directory                                |
| git init --bare my-project.git        | Creates a git repo without a working directory                           |
| git init --template=\<template dir>    | Creates a git repo with the specified template                           |
| git init --seperate-git-dir=\<git dir> | Creates a git repo when the dot files are located in specified directory |

### *Notes*
* If you've already run git init on a project directory and it contains a .git subdirectory, you can safely run git init again on the same project directory. It will not override an existing .git configuration.
* By default, git init will initialize the Git configuration to the .git subdirectory path. The subdirectory path can be modified. Set the $GIT_DIR environment variable to a custom path and git init will initialize the Git configuration files there. Or pass the --separate-git-dir argument for the same result. 
* A common use case for a separate .git subdirectory is to keep your system configuration "dotfiles" (.bashrc, .vimrc, etc.) in the home directory while keeping the .git folder elsewhere.
* You would create a bare repository to git push and git pull from, but never directly commit to it. Central repositories should always be created as bare repositories and developer local repos are non bare. *eg: **sssh \<user>@\<host> cd path/above/repo git init --bare my-project.git***

| git clone \<repo>                           | Clones a local or remote repo                                                                       |
|--------------------------------------------|-----------------------------------------------------------------------------------------------------|
| git clone \<repo> \<directory>               | Clone the repo located at \<repo> into the folder \<directory> locally                                |
| git clone -branch \<tag> \<repo>             | Clone the repo at repo and only clone the ref for the tag                                           |
| git clone -depth=1 \<repo>                  | Shallow Clone: Only clone the history of commits specified by the option depth=1                    |
| git clone -branch \<branch name> \<repo>     | Clones the specified branch instead of where remote HEAD is pointing to (usually the remote master) |
| git clone --template=\<template dir> \<repo> | Clones \<repo> using template in template directory                                                  |
| git clone --\<bare/mirror> \<repo>           | Similar to init bare. Clone but does not create a working directory                                 |
### *Notes*
* git clone uses a git init to create the repo locally

| GIT URL Protocols | Git has its own URL syntax which is used to pass remote repository locations to Git commands   |
|-------------------|------------------------------------------------------------------------------------------------|
| -SSH              | Authenticated network protocol - ssh://[user@]host.xz[:port]/path/to/repo.git/                 |
| -GIT              | Unique to git, runs on port (9418), non authenticated - git://host.xz[:port]/path/to/repo.git/ |
| -HTTP             | http[s]://host.xz[:port]/path/to/repo.git/                                                     |


***
### diff-so-fancy => Package that beautifies git diff 
* npm install -g diff-so-fancy => npm to install package
* git diff --color | diff-so-fancy => usage
##### *doff-so-fancy configuration*
* git config --global core.pager "diff-so-fancy | less --tabs=4 -RFX"
* git config --global pager.show "diff-so-fancy | less --tabs=1,5 -RFX"
* git config --global color.ui true
* git config --global color.diff-highlight.oldNormal "red bold"
* git config --global color.diff-highlight.oldHighlight "red bold 52"
* git config --global color.diff-highlight.newNormal "green bold"
* git config --global color.diff-highlight.newHighlight "green bold 22"
***
* Git Log 
* git log --graph --oneline --decorate
* git log --pretty=format:"%cn commited %h on %cd"
* git log -3 => Limit the number of commits to last 3
* git log --after="2018-12-1"
* git log --after="yesterday"
* git log --after="2018-12-1" --before="2018-12-26"
* git log --author="John"
* git log --author="John\|Mary"
* git log --grep="comment in the commit"
* git log --foo.py bar.py #By File
* git log -S"Hello, World!" #By Content
* git log \<since>..\<until>
* git log master..feature
* git log --no-merges
* git log --merges
