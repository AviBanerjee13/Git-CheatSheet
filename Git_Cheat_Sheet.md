# **GIT Cheat Sheet**
---
### *Reference*
### https://www.atlassian.com/git/tutorials/
## Getting Started

| git init                              | Creates a git repository                           |
|---------------------------------------|--------------------------------------------------------------------------|
| git init \<directory>                  | Creates a git repo in specified directory                                |
| git init --bare my-project.git        | Creates a git repo without a working directory                           |
| git init --template=\<template dir>    | Creates a git repo with the specified template                           |
| git init --seperate-git-dir=\<git dir> | Creates a git repo when the dot files are located in specified directory |

### *Notes*
* You can safely run git init again on the same project directory. It will not override an existing .git configuration.
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
| -HTTP             | http[s]://host.xz[:port]/path/to/repo.git/                                                    |
***
| git config                                 | Set config values on a --local or --global or --system scope.       |
|--------------------------------------------|---------------------------------------------------------------------|
| --local                                    | Local repository level. Stored at .git/config                       |
| --global                                   | User specific. Stored at C:\Users\<username>\.gitconfig for Windows |
| --system                                   | At machine level. Stored at C:\ProgramData\Git\config               |
| git config --\<scope> user.name \<name>      | Sets username in the given scope                                    |
| git config --\<scope> user.email \<email>    | Sets user email in the given scope                                  |
| git config --\<scope> core.editor "code --wait" | Sets the editor in the given scope                                  |
| git config --global -e                     | Opens the global config file in the specified editor                |
| git config --local -e                      | Opens the local config file in specified editor                     |

***
| diff-so-fancy                                                         | Package that beautifies git diff |
|-----------------------------------------------------------------------|----------------------------------|
| npm install -g diff-so-fancy                                          | npm to install package           |
| git diff --color | diff-so-fancy                                      | usage                            |
| git config --global core.pager "diff-so-fancy | less --tabs=4 -RFX"   | diff-so-fancy configuration      |
| git config --global pager.show "diff-so-fancy | less --tabs=1,5 -RFX" | diff-so-fancy configuration      |
| git config --global color.ui true                                     | diff-so-fancy configuration      |
| git config --\<scope> core.editor "code -w"                            | diff-so-fancy configuration      |
| git config --global color.diff-highlight.oldNormal "red bold"         | diff-so-fancy configuration      |
| git config --global color.diff-highlight.oldHighlight "red bold 52"   | diff-so-fancy configuration      |
| git config --global color.diff-highlight.newNormal "green bold"       | diff-so-fancy configuration      |
| git config --global color.diff-highlight.newHighlight "green bold 22" |
***
### *Notes*
To use Visual Studio for diff and merge in GIT - 
* git config --global -e
* Change the config file as follows

[difftool "visualstudio"]  
>prompt = true  
cmd = 'C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/Common7/IDE/CommonExtensions/Microsoft/TeamFoundation/Team Explorer/vsdiffmerge.exe' "$LOCAL" "$REMOTE" Source Target //t

[mergetool "visualstudio"]  
>prompt = true  
cmd = 'C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/Common7/IDE/CommonExtensions/Microsoft/TeamFoundation/Team Explorer/vsdiffmerge.exe' "$LOCAL" "$REMOTE" "$BASE" "$MERGED" //m  
trustExitCode = true  

[diff]  
>tool = visualstudio

[merge]
>tool = visualstudio

***
| alias                                 | alias for git commands        |
|---------------------------------------|-------------------------------|
| git config --global alias.co checkout | example of checkout alias     |
| git config --global alias.br branch   | example of branch alias       |
| git config --global alias.st status   | example of status alias       |
| git config --local alias.cm commit    | example of commit alias       |
***
| git diff                     | Diffing changes                                                                             |
|------------------------------|---------------------------------------------------------------------------------------------|
| git diff HEAD \<filename>     | Diffing between local and committed (HEAD is default, can be omitted. filename is optional) |
| git diff --cached \<filename> | Diffing local and staged changes (filename is optional)                                     |
***
| Saving changes           | Saving changes from working directory to Staging and Repository                                                     |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| git add \<filename>       | adds file to staging area                                                                                           |
| git add \<directory>      | adds directory to staging                                                                                           |
| git add -p               | begins an interactive session, will present a chunk of changes and prompt for a command - y to stage or n to ignore |
| git add .                | adds all files to stage                                                                                             |
| git status               | examine the current status of repository                                                                            |
| git reset                | reset add                                                                                                           |
| git commit               | commit a snapshot to repository                                                                                     |
| git stash                | takes uncommited changes(both staged and unstaged) and saves them away for later use                                |
| git stash pop            | pops the changes from stash and reapplies them                                                                      |
| git stash list           | lists the stashes                                                                                                   |
| git stash save "comment" | stashes with a comment                                                                                              |
| git stash -u             | stashes untracked files                                                                                             |
| git stash -a             | stashes all files including ignored files                                                                           |
***
| .gitignore           | Matching patterns                                                          | uses globbing patterns to match files against names and ignore them                                                                                                          |
|----------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/logs              | logs/debug.log logs/monday/foo.bar build/logs/debug.log                    | You can prepend a pattern with a double asterisk to match directories anywhere in the repository.                                                                            |
| **/logs/debug.log    | logs/debug.log build/logs/debug.log but not logs/build/debug.log           | You can also use a double asterisk to match files based on their name and the name of their parent directory.                                                                |
| *.log                | debug.log foo.log .log logs/debug.log                                      | An asterisk is a wildcard that matches zero or more characters.                                                                                                              |
| *.log !important.log | debug.log trace.log but not important.log logs/important.log               | Prepending an exclamation mark to a pattern negates it. If a file matches a pattern, but  also matches a negating pattern defined later in the file, it will not be ignored. |
| logs/**/debug.log    | logs/debug.log logs/monday/debug.log logs/monday/pm/debug.log              | A double asterisk matches zero or more directories.                                                                                                                          |
| logs/*day/debug.log  | logs/monday/debug.log logs/tuesday/debug.log but not logs/latest/debug.log | Wildcards can be used in directory names as well.                                                                                                                            |
| logs/debug.log       | logs/debug.log but not debug.log build/logs/debug.log                      | Patterns specifying a file in a particular directory are relative to the repository root. (You can prepend a slash if you like, but it doesn't do anything special.)         |
***

| git log                                                                       | Shows commit history                                                             |
|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| git log -n \<limit> / git log -\<limit>                                         | Shows only \<limit> commits                                                           |
| git log --oneline                                                             | Condenses commit to a single line                                                    |
| git log --stat                                                                | which files were altered and the relative number of lines that were added or deleted |
| git log -p                                                                    | Displays the path representing the commits, most detailed view.                      |
| git log \<filename>                                                            | Displays log for a file                                                              |
| git log --author="\<pattern>"                                                  | Searches commits with a author name that matches the pattern                         |
| git log --grep="\<pattern>"                                                    | Searches commits with a commit message that matches the pattern                      |
| git log -S"Hello, World!"                                                     | Searches commits with content matching the patter("Hello, World!")                   |
| git log \<since>..\<until>                                                      | Show only commits that occur between \<since> and \<until>                             |
| git log --after="\<date>"  git log --after="yesterday" git log --before=\<date> | Shows commits after or before a certain date                                         |
| git log --graph --decorate --oneline                                          | Show a text based graph of the commits on the left hand side of the commit messages  |
| git log master..feature-branch                                                | Useful for comparing branches                                                        |
| git log --merges / git log --no-merges                                        | Displays commits with merges or no merges                                            |
***
| git tagging                      | A tag is like a branch that doesn’t change. Unlike branches, tags, after being created, have no further history of commits. |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| git tag \<tagname> / git tag v1.1 | Lightweight tag. Less meta data. Usually used for private releases                                                          |
| git tag -a \<tagname>             | Annotated tag. More metadata. Public releases. Editor opens for entering more information                                   |
***
