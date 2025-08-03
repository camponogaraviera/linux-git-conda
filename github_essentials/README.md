<!-- Header: -->
<div align="center"> 
  <a href="https://docs.github.com/en">
    <img align="center" src="https://avatars.githubusercontent.com/u/3571983?s=200&v=4" alt="github" height="200" width="200" />
  </a>
  <h1> GitHub Essentials </h1>
</div>

# Table of Contents

- [Preliminaries](#preliminaries)
- [Installing a Git GUI](#installing-a-git-gui)
- [Installing Git from CLI](#installing-git-from-cli)
- [Fork](#fork)
- [Git Clone](#git-clone)
- [View Markdown file](#view-markdown-file)
- [Working with Branches](#working-with-branches)
  - [Accessing Specific Commits](#accessing-specific-commits)
  - [Git Cherry-Pick](#git-cherry-pick)
- [Staging Files](#staging-files)
- [Committing Files](#committing-files)
- [Stashing](#stashing)
- [Untracking and Unstaging Files](#untracking-and-unstaging-files)
- [Restoring Files](#restoring-files)
- [Reverting to a Previous Version](#reverting-to-a-previous-version)
- [Pushing Commits to your Remote Repository](#pushing-commits-to-your-remote-repository)
- [Git Merge vs Git Rebase Workflow](#git-merge-vs-git-rebase-workflow)
- [Pulling Updates From an Upstream Remote Repository](#pulling-updates-from-an-upstream-remote-repository)
- [Issue Tracker](#issue-tracker)
- [Pull Request](#pull-request)
- [Clean Up Commit History](#clean-up-commit-history)
- [GitHub Versioning](#github-versioning)
- [The .gitignore File](#the-gitignore-file)
- [Atom IDE](#atom-ide)

# Preliminaries

> **Note:** text enclosed in `< >` (angle brackets) represents placeholders that should be replaced with actual values.

- GitHub: a cloud-based hosting platform running on a server that uses git as its command-line tool.
- Git: an open-source version control that runs on a CLI completely independent of GitHub.

<!--- ############################################################################################################################################### -->

# Installing a Git GUI

One can choose to install a Git GUI on a local machine rather than using Git via Terminal. To this end, simply:

1. Download the [source tree](https://www.sourcetreeapp.com/) application.

# [Installing Git](https://github.com/git-guides/install-git) from CLI

For more information, see the [Git from source](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) guide.

## On Windows

1. Download the latest version from [gitforwindows.org](https://gitforwindows.org/);

2. Follow the instructions as provided in the Git Setup wizard as they appear.

## On Linux

For debian-based distros (Ubuntu/Ubuntu-derivatives):

```sh
sudo apt update && apt install git-all
```

And for your sanity, install pip (a Python package manager):

```bash
sudo apt update && apt install python3-pip && pip -V
```
Note: the `pip -V` flag is shorthand for `pip --version`.

## With Anaconda

1. Download [Anaconda](https://www.anaconda.com/products/individual) latest version;
  - On Windows: follow the installation wizard.
  - On Linux: follow [these steps](../conda_essentials/README.md/#Installing-Anaconda).
    
2. With an open Anaconda command-line prompt, [simply](https://anaconda.org/anaconda/git):
```sh
conda install -c anaconda git && git --version
```
Note: the `-c` flag (abbreviated from --channel) points to the channel (e.g., anaconda) from which git will be installed.

<!--- ############################################################################################################################################### -->

# [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

One can choose to make a copy of a public/private GitHub repository from their own [Organization](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/about-organizations) or someone else's GitHub account by clicking on the [Fork](https://github.com/octocat/Spoon-Knife) button.

<!--- ############################################################################################################################################### -->

# [Git Clone](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) 

You can set up a Git linkage by cloning your private/public repository to a custom folder/directory of your Local Machine using the Command-line interface ([Unix-like](../linux_essentials/README.md) terminal or [Anaconda environment](../conda_essentials/README.md) prompt with [Git](https://anaconda.org/anaconda/git) installed).

## Git clone with different protocols

- There are four possible [protocol choices](https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols): Local, HTTP, Secure Shell (SSH), and Git.
  - Cloning over HTTPS: the protocol uses private key authentication to clone a private repository using a git username and an access token. It is also the git recommended way for cloning public repositories.
  - Cloning over SSH: the protocol uses SSH keys for authentication.

### Cloning over HTTPS

- To clone a public repository over HTTPS:
```bash
git clone https://github.com/<github-username>/<public-repo-name>.git
```

- To clone a private repository over HTTPS:
```bash
git clone https://github.com/<github-username>/<private-repo-name>.git
<username>
<token>
```

### Cloning over SSH

- To clone a repository over SSH:
```bash
git clone ssh://<user>@<server>/<project_name>.git
```
or
```bash
git clone <user>@<server>:<git_username>/<repo_name>.git
```

## Shallow clone

To clone a repository fetching only the latest commit ignoring previous commit history:

```bash
git clone --depth=1 https://github.com/user/repo.git
```

<!--- ############################################################################################################################################### -->

# View Markdown File

- After `git clone`, to visualize a README.md (markdown) file on the web browser, one can use grip via the CLI:
```sh
pip install grip && grip -b README.md
```

<!--- ############################################################################################################################################### -->

# Working with Branches

- [git branch](https://git-scm.com/docs/git-branch) - Show available branches and highlight the current branch.
- [git branch \<new-branch-name>](https://git-scm.com/docs/git-branch) - Create a new branch named `<new-branch-name>`.
- [git checkout \<new-branch-name>](https://git-scm.com/docs/git-checkout) - Switch to the newly created branch.
  
- The command `git checkout -b <new-branch-name>` is shorthand for:
```sh
git branch <new-branch-name>
git checkout <new-branch-name>
```

## Accessing Specific Commits

- Fetch the branch you are interested in:
```bash
git fetch origin <branch-name>
```
- Once the branch is fetched, switch to the specific commit by its hash ID (Use `git log` to find the hash ID):
```bash 
git checkout <commit-hash>
```

## [Git Cherry-Pick](https://git-scm.com/docs/git-cherry-pick)

- To bring only specific commits from a `feature branch` into a `target branch` (main, dev, etc.), run:
```bash
git checkout <feature-branch>                                  # Step 1: Switch to the feature branch you want to bring commits from.
git log                                                        # Step 2: Show the log to find the IDs of the commits you want to bring.
git checkout <target-branch>                                   # Step 3: Switch to the branch you want to move the commits into.
git cherry-pick <commit-id1> <commit-id2> ... <commit-idN>     # Step 4: Bring one or several commits to the current branch.
```

<!--- ############################################################################################################################################### -->

# Staging Files 

- To add/stage all file changes (new/untracked and modified files) to the Git staging area for commit:
```bash
git add --all
```
or
```bash
git add -A
```

<!--- ############################################################################################################################################### -->

# Committing Files

- To commit all staged files with a commit message:
  
```bash
git commit -am "commit message"
```

- To overwrite the last commit message:
  
```bash
git commit --amend
```

<!--- ############################################################################################################################################### -->

# Stashing

Git stash is useful to temporarily save uncommitted changes in the working directory. This allows one to switch branches or perform other tasks without losing the current work. Stashed changes are not automatically applied to a new branch, however, one can apply them manually afterwards.

```bash
git stash push -m "descriptive message" # Stash changes with a message.
git stash list                          # List all stashes.
git checkout -b <feature-branch>        # Create and switch to a new feature branch.
git stash pop                           # Apply the latest stash and remove it from the stash list.
```

- The command `git stash pop` is shorthand for:
```sh
git stash apply # Applies the latest stash.
git stash drop  # Removes the latest stash.
```

<!--- ############################################################################################################################################### -->

# [Untracking and Unstaging Files](https://git-scm.com/docs/git-rm)

- To delete unchanged files from the local working directory:
```bash
git rm <filename1> <filename2> 
```

- To delete changed files from the local working directory:
```bash
git rm -f <filename1> <filename2>
``` 

- To unstage and untrack uncommitted files from git index (staging area), keeping it in the local working directory:
```bash
git rm --cached <filename>
```
Untracking means the file will be deleted from the remote repository on the next commit, but will remain locally.

Commit all changes to take effect:
```bash
git add -A
git commit -m "message"
```

Note: Git **safety check** ensure that the files on your current branch match those in the staging index.

<!--- ############################################################################################################################################### -->

# Restoring Files

- [git restore .](https://git-scm.com/docs/git-restore) - To discard all unstaged (**before `git add`**) and uncommitted (**before `git commit`**) file changes and restore the originals from Head.

- [git restore \<filename1> \<filename2> ...](https://git-scm.com/docs/git-restore) - To discard specific file changes in the local working directory.

- [git restore --staged \<filename>](https://git-scm.com/docs/git-restore) - To unstage (**after `git add`**) an uncommitted (**before `git commit`**) file keeping the file changes in the local working directory.
  
- [git checkout \<hash-id>](https://git-scm.com/docs/git-checkout) or [git reflog \<hash-id>](https://git-scm.com/docs/git-reflog) - [Recovers/restores](https://git-scm.com/book/en/v2/Git-Internals-Maintenance-and-Data-Recovery) a file after committing (**after `git commit`**). Use `git log` or `git reflog` to find the commit hash ID.

- [git fsck](https://git-scm.com/docs/git-fsck) (file system check) - To scan the repository for integrity issues such as dangling objects (e.g., blobs, commits, and tags) that are not reachable.
  
<!--- ############################################################################################################################################### -->

# [Reverting to a Previous Version](https://git-scm.com/docs/git-reset)

- To revert the current branch to the latest commit discarding all uncommitted file changes:
```bash
git reset --hard HEAD
```

- To revert the repository, i.e., to move Head to a specific commit version:
```bash
git reset --hard <version_id> 
```
or
```bash
git reset --soft <version_id> 
```

- Notes:
  - The `--hard` flag discards all uncommitted file changes (staged and unstaged).
  - The `--soft` flag keeps all file changes (staged and unstaged), but stages commit differences.

<!--- ############################################################################################################################################### -->
  
# [Pushing Commits](https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository) to your Remote Repository

- Keywords:
  - Remote repository: a repository on a GitHub server.
  - Local repository: a cloned repository on your computer.

- To push changes from your local cloned repository to a remote repository, run:
```sh
git clone <remote-repo-url>.git                     # (Optional) If you haven't cloned the remote repository yet.
git status                                          # (Optional) Show the status of the local repository.
git diff                                            # (Optional) Show changes made to the local repository.
git remote add <remote-alias> <remote-repo-url>     # (Optional) Adds a remote repository with the alias <remote-alias>.
git remote -v                                       # (Optional) List the configured remotes.

# When a repository is cloned, Git automatically sets up a remote named `origin` for both `fetch` and `push`.
# However, when a repository is initialized with `git init`, no remote is configured by default.

git add -A                               # Stage all file changes for commit.
git commit -am "commit message"          # Commit all staged files with a <commit_message>.
git push -u <remote-alias> <branch-name> # To push all local changes to the <branch-name> branch of the remote repository.
```
- Note: get your password (access token) at: `Settings` >> `Developer settings` >> `Personal access tokens` >> `Generate new token` >> `Select scopes (repo)`.

- Pushing commits from the current branch to a target branch:
```sh
git branch # Show available branches and highlight the name of the current branch.
git push -u <remote-alias> <current-branch-name>:<target-branch-name>
```

<!--- ############################################################################################################################################### -->

# [Git Merge](https://git-scm.com/docs/git-merge) vs [Git Rebase](https://git-scm.com/docs/git-rebase) Workflow

When working collaboratively on a project, one has the choice to join/combine two or more development histories by taking commits from a feature branch and placing them on top of the header of a target branch (e.g., main, dev, etc.).

## Git Merge

The git merge command joins/combines commits from a source branch (feature branch) into a target branch. It creates a new commit, known as a merge commit, on top of the target branch's header, preserving the commit history of both feature and target branches.

- To merge/join previous commits from a `<feature-branch>` into a brand new single merge commit placed on top of the `<target-branch>`, run:
```bash
git checkout <target-branch> # Switch to the branch named "<target-branch>".
git merge <feature-branch>   # Merge the "<feature-branch>" into the "<target-branch>".
```

- Git merge commit history visualization:
```bash
   Before merge:      After merge:
                           (*) 
                            |   \
         (F2)               |  (F2) 
          |                 |    |
    (M5)  |                (M5)  |
     |  (F1)                |  (F1)
    (M4) /                 (M4) /
     |                      |
    (M3)                   (M3)
```

- Legend:
  - M: main branch (target branch).
  - F: source branch (feature branch).

### [Git squash merge](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---squash)

Git squash merge condenses all changes from the source branch into a single new commit on top of the target branch. This new commit does not preserve the commit history from the source branch.

- To squash all commits from a `<feature-branch>` into a single merge commit on top of the `<target-branch>`, run:
```bash
git checkout <target-branch>        # Switch to the branch named "<target-branch>".
git merge --squash <feature-branch> # Squash merge the "<feature-branch>" into the "<target-branch>".
```

The above command should be followed by `git merge --abort` whenever a merge results in a conflict, and will fail if there were uncommitted changes before `git merge`. Therefore, make sure to commit all changes before running a merge. If you get hit by the message "stopped before committing as requested", simply run: `git commit -am "commit message"`.
  
## Git Rebase 

Git rebase is used to integrate changes from one branch into another by rewinding the changes of the source branch (`<feature-branch>`) and replaying them on top of the target branch (`<target-branch>`). This operation rewrites the commit history of the source branch.

- To rebase/move previous commits from a branch named `<feature-branch>` onto the top of a branch named `<target-branch>`, run:
```bash
git checkout <feature-branch> # Switch to the branch named "<feature-branch>".
git rebase -i <target-branch> # Rebase "<feature-branch>" onto the "<target-branch>".
```

**Rebasing upon the last `n` commits from a branch named `<feature-branch>`:**
```bash
git checkout <feature-branch>
git rebase -i  HEAD~<n> # Operate upon the last n commits within the interactive mode. 
```

*Note:* the `-i` flag enables interactive mode, where the default terminal text editor will pop up to enable the user to edit how a list of commits should be rebased.

- Git rebase commit history visualization:
```bash
Before rebase      After rebase
                       (F2)                                                   
     (F2)               |   
      |                (F1)  
     (F1)               |  
 (M5) /                (M5) 
  |                     |
 (M4)                  (M4)
  |                     |
 (M3)                  (M3)
```

- Legend:
  - M: main branch (target branch).
  - F: source branch (feature branch).

**Example rebasing against a target branch named `"main"`.**

```bash
git clone <remote-repo-url>.git           # Clone the remote repository.
git checkout -b <feature-branch>          # Create and switch to a new branch "<feature-branch>".
git add -A                                # Stage all file changes for commit.
git commit -am "commit message"           # Commit all staged files before merge.
git checkout main                         # Switch to the "main" branch.
git pull                                  # Sync your local "main" branch with the remote repository.
git checkout <feature-branch>             # Switch back to the feature branch.
git rebase -i main                        # Rebase your feature branch against the latest "main" branch.
git push origin <feature-branch> --force  # Push the rebased feature branch to the remote repository.
```

Optional step:
```bash
git checkout main                # Switch to the "main" branch.
git merge <feature-branch>       # Merge the feature branch into the "main" branch.
git push origin main             # Push the updated "main" branch to the remote repository.
```

<!--- ############################################################################################################################################### -->

# [Pulling Updates](https://docs.github.com/en/get-started/using-git/getting-changes-from-a-remote-repository) from an Upstream Remote Repository

- Keywords:
  - Upstream repository: the original repository from which a fork was created.

If you forked a remote repository owned by another GitHub user, there are two ways you can pull updates from said repository (a.k.a upstream repository) to sync both your local (cloned) copy and your remote forked repository.

- From the web UI:

  - **Before pull (fetch and merge):** `This branch is <N> commit(s) behind <repo-name>:<branch-name>.`

  1. Click on **Fetch upstream:** `Fetch and merge <N> upstream commit(s) from <repo-name>:<branch-name>.`

  2. Click on **Fetch and merge**. The output message should be `This branch is up to date with <repo-name>:<branch-name>.`

- From the command line:

  - To [sync](https://docs.github.com/github/collaborating-with-issues-and-pull-requests/syncing-a-fork) both the cloned repository and the remote forked repository:
```sh
# Step 1:
git clone <forked-repo-url>.git         # Clone the remote repository.
cd <repo-name>                          # Access the cloned repository.

# Step 2:
git remote add upstream <orig-repo-url> # Add the original repository as "upstream".
git remote -v                           # List the configured remotes.

# Step 3 (Optional):
git checkout <branch-name>              # Switch to the desired branch if not using the default one.

# Step 4 (Optional, if local changes were made):
git add -A
git commit -am "commit message"

# Step 5:
git fetch upstream                      # To retrieve all the new remote-tracking branches and tag updates from the upstream remote repository.

# Step 6:
git merge upstream/<branch-name>        # Merge changes from the upstream remote repository into the local branch named <branch-name>.

# Step 7:
git push -u origin <branch-name>        # Push changes to the forked remote repository.
```

- Alternatively, one can use `git pull` (shortcut for `git fetch` + `git merge` or `git rebase`):
```sh
cd <repo-name>
git remote add upstream <orig-repo-url>  
git checkout <branch-name>

# (Optional, if local changes were made):
git add -A
git commit -am "commit message"

git pull --rebase upstream <branch-name>
git push -u origin <branch-name> 
```
**Note:** commit all new changes made in your local cloned repository before running the `git pull` command to avoid a [merge conflict](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line).
  
- For example, suppose you are cloning your repository (not a fork) and `<branch-name>` is `dev`:
```bash
# (Optional, if local changes were made):
git add -A
git commit -am "commit message"

git pull --rebase origin dev
git push -u origin dev
```
If conflicts still exist, `resolve conflicts`, then:
```bash
git add -A
git rebase --continue
git push -u origin dev
```

<!--- ############################################################################################################################################### -->

# [Issue Tracker](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue)

There are two common ways to report a bug:

1. [Create an issue](hhttps://github.com/QuCAI-Lab/educational-resources/issues/new) through the [Issue Tracker](https://github.com/camponogaraviera/linux-git-conda/issues) from the web UI.

2. Create an `issue` from your computer's command line using [GitHub CLI](https://docs.github.com/en/github-cli/github-cli/about-github-cli).

<!--- ############################################################################################################################################### -->

# [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)

You can push changes from your forked repository to a specified branch of a remote repository owned by another GitHub user, as follows:

1. Fork the desired repository to your GitHub account.

2. Clone your forked repository:

```bash
git clone https://github.com/<yourgithubusername>/<repo-name>.git 
```

3. Create a new branch for the pull request and check out:

```sh
cd <repo-name>
git checkout -b <newbranch>
```

4. Check your changes before committing:

```sh
git status
git diff
```

5. Assigning "upstream" as the original remote repository that will be synced with the fork:

```sh
git remote -v
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
```

6. Set your Local Git Identity:

```sh
git config user.name "<yourgithubusername>"
git config user.email "youremail@mail.com"
git config --list
```

7. Push changes using your local shell/Anaconda Prompt, as follows:

```sh
git add -A
git commit -am "topic of the pull request"
git push -u upstream <newbranch>
```

8. On the web UI, click the `Compare & pull request` button.

9. Finally, click on `Create pull request`.

The admin or CI/CD tool of the upstream (original) repository will review the pull request and merge (or ignore) your proposed changes.

<!--- ############################################################################################################################################### -->

# Clean Up Commit History

```bash
git checkout --orphan temp     # Create a new orphan branch named `temp` with no history.
git add -A                     # Stage all files for commit.
git commit -am "init"          # Commit all staged files with the message "init".
git branch -D dev              # Delete the old branch named `dev`.
git branch -m dev              # Rename the current branch (temp) to `dev`.
git push -u origin dev --force # Force push the new `dev` branch to the remote repository, replacing the old one.
```

<!--- ############################################################################################################################################### -->

# GitHub Versioning

The development workflow includes:

- `dev` (development) branch: to work on bugs and features.
- `staging` branch: quality assurance and testing.
- `stable/0.0.x` branch: work is ready for deployment.

The pre-release related to a development branch reads `<package-name> 0.0.1-early-access`. After completing the User Acceptance Testing (UAT) process, one creates a `stable/0.0.2` branch with the following release: `<package-name> 0.0.2`.

<!--- ############################################################################################################################################### -->

# The [.gitignore](https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files) File

The `.gitignore` file instructs Git to ignore/untrack specific files or folders from a project.

- Common special characters:
  - `*` denotes a wildcard match (placeholder).
  - `/` is used to ignore pathnames relative to the .gitignore file.
  - `#` the hash symbol denotes the comment syntax.
  
- Gitignore Cheat Sheet:
  - To ignore all files (located anywhere) with extension ".ext": *.ext
  - To ignore all files with extension ".ext" except the "filename.ext" file: !filename.ext
  - To ignore all directories named ".dir" and all its contents: .dir/ 
  - To ignore a "filename.ext" file located in the root directory: /filename.ext
  - To ignore any file (located anywhere) named "filename.ext": filename.ext
  - To ignore any file or directory named ".filename": .filename
  - To ignore all files and directories starting with "filename": filename*

- Receipt for pushing after updating the .gitignore file:
  - git rm -r --cached . # To remove already tracked files from Git cache. 
  - git add --all :/

## Adding the .gitignore file

To add a `.gitignore` file to your cloned repository using the command-line interpreter, follow these steps.

1. Navigate to the relative/absolute path of the directory containing the cloned Git repository in your local machine:
```sh
cd ~/<repo_pathname> 
```
2. Create a .gitignore file:
```sh
touch .gitignore
```
or
```sh
cat > .gitignore
```
or simply (to open gedit text editor)
```sh
gedit .gitignore
```
Note: after saving, the file will be hidden by default, to view hidden files type `ll` in the command-line interpreter.

3. Add the file to the staging area:
```
git add .gitignore
```
4. Commit changes:

```
git commit -am "<message>" .gitignore
```

- To add a `.gitignore_global` file to all Git repositories cloned in your local machine:

```sh
git config --global core.excludesfile ~/.gitignore_global
```

## Minimal template

```gitignore

# Ignoring files whose filename ends with the suffix ~
*~

# Ignoring text files
*.txt

# Ignoring virtualenv files
.venv
venv/
ENV/

# Ignoring Jupyter Notebook files with extension .ipynb_checkpoints
.ipynb_checkpoints
```

For more .gitignore templates, see the [github/gitignore](https://github.com/github/gitignore) public repository.

<!--- ############################################################################################################################################### -->

# Atom IDE

Just in case you want to skip the above command-line steps. A suggested IDE to manage your GitHub repositories on a local server is [Atom](https://atom-editor.cc/). To install Atom on Linux, see [this manual](https://flight-manual.atom.io/getting-started/sections/installing-atom/). Once installed, you can clone, push changes, fetch/merge (pull) updates, and open pull requests using the Atom GUI. 

With open Atom IDE:
- To clone: click on the `GitHub` tab >> click on the `Clone an existing GitHub repository...` tab.
- To push: click on `Git` >> click on `Stage All` >> click on `Commit to main` >> click on `Push`.
- To pull: click on `Fetch` >> click on `Pull`.
