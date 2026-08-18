# Git & GitHub Commands — Complete Obsidian Notes

> **Important:** `Git` and `GitHub` are not the same thing.
>
> * **Git** → Version control system running on your computer.
> * **GitHub** → Remote hosting/service for Git repositories.
>
> Most commands below are **Git commands**. Commands such as `gh` belong to the **GitHub CLI**.

---

# 1. Git Configuration

## git config

Used to configure Git settings.

### Check Git configuration

```bash
git config --list
```

### Set username

```bash
git config --global user.name "Your Name"
```

### Set email

```bash
git config --global user.email "you@example.com"
```

### Check a specific setting

```bash
git config --global user.name
git config --global user.email
```

### Set default branch

```bash
git config --global init.defaultBranch main
```

### Set default editor

```bash
git config --global core.editor "code --wait"
```

### Why `--global`?

`--global` applies the setting to all repositories for the current user.

Without `--global`, the configuration applies only to the current repository.

```bash
git config user.name "Project User"
```

---

# 2. Creating a Repository

## git init

Creates a new Git repository in the current directory.

```bash
git init
```

This creates a hidden `.git` directory containing Git's repository information.

---

## git init <directory>

Creates a repository inside a new directory.

```bash
git init my-project
```

---

## git clone

Downloads an existing remote repository to your computer.

```bash
git clone https://github.com/user/project.git
```

Clone with a custom directory name:

```bash
git clone https://github.com/user/project.git my-project
```

---

## git clone --branch

Clone a specific branch.

```bash
git clone --branch development https://github.com/user/project.git
```

Short form:

```bash
git clone -b development https://github.com/user/project.git
```

---

# 3. Checking Repository Status

## git status

Shows the current state of the working directory and staging area.

```bash
git status
```

It tells you about:

* Modified files
* New files
* Deleted files
* Staged files
* Untracked files
* Current branch

---

## git status --short

Provides compact output.

```bash
git status --short
```

Example:

```text
 M Main.java
?? Test.java
A  README.md
```

---

# 4. Git Workflow

The basic Git workflow is:

```text
Working Directory
        ↓
     git add
        ↓
Staging Area
        ↓
    git commit
        ↓
Local Repository
        ↓
     git push
        ↓
Remote Repository
```

The most important commands are:

```bash
git status
git add
git commit
git push
git pull
```

---

# 5. Staging Files

## git add

Moves changes from the working directory to the staging area.

Add one file:

```bash
git add file.txt
```

Add multiple files:

```bash
git add file1.txt file2.txt
```

Add all changes:

```bash
git add .
```

Another common form:

```bash
git add -A
```

---

## git add -u

Stages modifications and deletions of already tracked files.

```bash
git add -u
```

It does not stage new untracked files.

---

## git add -p

Interactively select parts of a file to stage.

```bash
git add -p
```

Very useful when one file contains multiple unrelated changes.

---

# 6. Unstaging Files

## git restore --staged

Removes a file from the staging area without deleting its changes.

```bash
git restore --staged file.txt
```

All staged files:

```bash
git restore --staged .
```

Older equivalent:

```bash
git reset HEAD file.txt
```

`git restore --staged` is generally clearer for this purpose.

---

# 7. Discarding Changes

## git restore

Restores a file to its last committed version.

```bash
git restore file.txt
```

This permanently discards the unstaged changes in that file.

---

## Restore multiple files

```bash
git restore .
```

**Be careful:** this can discard uncommitted changes.

---

# 8. Committing Changes

## git commit

Creates a commit from staged changes.

```bash
git commit -m "Add login functionality"
```

A commit is a snapshot of your project at a particular point in time.

---

## git commit -a

Automatically stages modifications and deletions of tracked files and commits them.

```bash
git commit -a -m "Fix login bug"
```

It does **not** include new untracked files.

---

## git commit --amend

Modifies the most recent commit.

```bash
git commit --amend
```

Change the commit message:

```bash
git commit --amend -m "Updated login functionality"
```

Add forgotten changes to the previous commit:

```bash
git add forgotten-file.java
git commit --amend --no-edit
```

Avoid amending commits that have already been shared with others unless you understand the consequences.

---

# 9. Viewing Commit History

## git log

Shows commit history.

```bash
git log
```

---

## git log --oneline

Compact history.

```bash
git log --oneline
```

Example:

```text
a82f123 Add login
b72d432 Fix validation
c91d221 Initial commit
```

---

## git log --oneline --graph

Displays branches visually.

```bash
git log --oneline --graph
```

---

## git log --all

Shows commits from all branches.

```bash
git log --all
```

---

## git log --stat

Shows files changed in each commit.

```bash
git log --stat
```

---

## git log -p

Shows the actual changes introduced by commits.

```bash
git log -p
```

---

## git log --author

Find commits by a specific author.

```bash
git log --author="Abhi"
```

---

## git log --since

Show commits after a specific date.

```bash
git log --since="2 weeks ago"
```

---

# 10. Viewing Changes

## git diff

Shows unstaged changes.

```bash
git diff
```

---

## git diff --staged

Shows staged changes.

```bash
git diff --staged
```

---

## git diff HEAD

Shows all changes since the latest commit.

```bash
git diff HEAD
```

---

## Compare two commits

```bash
git diff commit1 commit2
```

---

## Compare branches

```bash
git diff main development
```

---

# 11. Branches

Branches allow you to work on different versions/features of a project independently.

Example:

```text
main
 │
 ├── feature/login
 │
 ├── feature/payment
 │
 └── bugfix/navbar
```

---

## git branch

Lists local branches.

```bash
git branch
```

---

## git branch -a

Lists local and remote branches.

```bash
git branch -a
```

---

## git branch -r

Lists remote branches.

```bash
git branch -r
```

---

## Create a branch

```bash
git branch feature-login
```

This creates the branch but does not switch to it.

---

## Delete a branch

```bash
git branch -d feature-login
```

Force delete:

```bash
git branch -D feature-login
```

`-D` can delete a branch even when Git thinks it contains unmerged commits.

---

## Rename current branch

```bash
git branch -m new-name
```

Rename another branch:

```bash
git branch -m old-name new-name
```

---

# 12. Switching Branches

## git switch

Switch to an existing branch.

```bash
git switch development
```

---

## Create and switch

```bash
git switch -c feature-login
```

This is one of the most commonly used commands.

---

## Older command: git checkout

```bash
git checkout development
```

Create and switch:

```bash
git checkout -b feature-login
```

`git switch` is generally preferred for branch switching because its purpose is clearer.

---

# 13. Merging

## git merge

Combines changes from another branch into the current branch.

Example:

```bash
git switch main
git merge feature-login
```

This merges `feature-login` into `main`.

---

## Fast-forward merge

If no conflicting commits exist on the target branch, Git may simply move the branch pointer forward.

```text
main
  ↓
A---B---C
        ↑
     feature
```

---

## No-fast-forward merge

```bash
git merge --no-ff feature-login
```

Creates an explicit merge commit.

Useful when you want the feature branch history to remain visible.

---

# 14. Merge Conflicts

A merge conflict occurs when Git cannot automatically determine which changes to keep.

Example:

```text
<<<<<<< HEAD
Your code
=======
Other branch code
>>>>>>> feature
```

You manually edit the file and choose the correct version.

Then:

```bash
git add file.java
git commit
```

---

## Abort Merge

If you want to cancel the merge:

```bash
git merge --abort
```

---

# 15. Remote Repositories

A remote is a reference to another Git repository, usually on GitHub.

---

## git remote

Lists remotes.

```bash
git remote
```

---

## git remote -v

Shows remote URLs.

```bash
git remote -v
```

Typical output:

```text
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

---

## git remote add

Adds a remote.

```bash
git remote add origin https://github.com/user/project.git
```

`origin` is simply the conventional name for the primary remote.

---

## git remote remove

Removes a remote.

```bash
git remote remove origin
```

---

## git remote rename

```bash
git remote rename origin upstream
```

---

## git remote set-url

Changes the URL of an existing remote.

```bash
git remote set-url origin https://github.com/user/new-project.git
```

---

# 16. Fetching Changes

## git fetch

Downloads changes from a remote repository without modifying your current working branch.

```bash
git fetch
```

Fetch from a specific remote:

```bash
git fetch origin
```

Fetch all remotes:

```bash
git fetch --all
```

---

## Important Difference

```text
git fetch
```

Downloads changes.

```text
git pull
```

Downloads + integrates changes.

---

# 17. Pulling Changes

## git pull

Downloads changes and integrates them into your current branch.

```bash
git pull
```

Equivalent conceptually to:

```bash
git fetch
git merge
```

---

## git pull --rebase

Fetches changes and rebases your local commits on top of them.

```bash
git pull --rebase
```

Often used to maintain a cleaner history.

---

# 18. Pushing Changes

## git push

Uploads local commits to the remote repository.

```bash
git push
```

---

## Push specific branch

```bash
git push origin main
```

---

## Push new branch

```bash
git push -u origin feature-login
```

`-u` establishes the upstream tracking relationship.

After this, you can usually use:

```bash
git push
```

---

## Delete remote branch

```bash
git push origin --delete feature-login
```

---

# 19. Tracking Branches

## git branch -vv

Shows tracking information.

```bash
git branch -vv
```

Example:

```text
* main abc123 [origin/main] Latest commit
```

---

## git push -u

```bash
git push -u origin main
```

Sets:

```text
local main
      ↓
origin/main
```

---

# 20. Rebase

## git rebase

Moves or reapplies commits onto another base.

Example:

```bash
git switch feature
git rebase main
```

Conceptually:

```text
Before:

A---B---C main
     \
      D---E feature
```

After:

```text
A---B---C---D'---E' feature
```

Rebase creates new commit IDs for the rebased commits.

---

## Interactive Rebase

```bash
git rebase -i HEAD~3
```

Useful for:

* Squashing commits
* Reordering commits
* Editing commit messages
* Removing commits

Example:

```text
pick abc First commit
squash def Second commit
pick xyz Third commit
```

---

## Abort Rebase

```bash
git rebase --abort
```

---

## Continue Rebase

After resolving a conflict:

```bash
git add file.java
git rebase --continue
```

---

# 21. Reset

`git reset` moves the current branch pointer and can modify the staging area and working tree depending on the mode.

---

## git reset --soft

```bash
git reset --soft HEAD~1
```

Removes the latest commit but keeps its changes staged.

```text
Commit ❌
Changes ✅ staged
```

---

## git reset --mixed

```bash
git reset --mixed HEAD~1
```

Removes the commit and unstages the changes.

```text
Commit ❌
Changes ✅ unstaged
```

This is the default mode.

---

## git reset --hard

```bash
git reset --hard HEAD~1
```

Removes the commit and discards the associated working-tree changes.

```text
Commit ❌
Changes ❌
```

**Dangerous command.**

---

# 22. Revert

## git revert

Creates a new commit that reverses the changes introduced by an earlier commit.

```bash
git revert abc123
```

Unlike `reset`, `revert` preserves the existing history.

Prefer `revert` when undoing commits that have already been pushed/shared.

---

# 23. HEAD

`HEAD` represents the commit currently checked out.

Usually:

```text
HEAD
 ↓
main
 ↓
Latest Commit
```

---

## HEAD~1

Previous commit.

```bash
git show HEAD~1
```

---

## HEAD~2

Two commits before HEAD.

```bash
git show HEAD~2
```

---

# 24. Git Tags

Tags are used to mark important points in history, commonly releases.

Example:

```text
v1.0.0
v1.1.0
v2.0.0
```

---

## Create tag

```bash
git tag v1.0.0
```

---

## Annotated tag

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
```

Annotated tags contain additional metadata.

---

## List tags

```bash
git tag
```

---

## Show tag

```bash
git show v1.0.0
```

---

## Push tag

```bash
git push origin v1.0.0
```

---

## Push all tags

```bash
git push origin --tags
```

---

## Delete local tag

```bash
git tag -d v1.0.0
```

---

## Delete remote tag

```bash
git push origin --delete v1.0.0
```

---

# 25. Stashing

Stash temporarily stores uncommitted changes.

Useful when:

```text
You are working on Feature A
        ↓
Urgent bug arrives
        ↓
Need to switch branches
        ↓
Don't want to commit unfinished work
        ↓
git stash
```

---

## git stash

```bash
git stash
```

---

## git stash push

```bash
git stash push -m "Login work in progress"
```

---

## List stashes

```bash
git stash list
```

---

## Apply stash

```bash
git stash apply
```

Applies the latest stash but keeps it in the stash list.

---

## Apply specific stash

```bash
git stash apply stash@{1}
```

---

## Pop stash

```bash
git stash pop
```

Applies the stash and removes it from the stash list.

---

## Delete stash

```bash
git stash drop stash@{0}
```

---

## Delete all stashes

```bash
git stash clear
```

---

# 26. Cherry-Pick

## git cherry-pick

Applies a specific commit from another branch to the current branch.

```bash
git cherry-pick abc123
```

Example:

```text
main:

A---B---C

feature:

A---B---D---E
```

Cherry-pick `E` into main:

```text
A---B---C---E'
```

Useful when you need one particular fix without merging the entire branch.

---

## Abort Cherry-Pick

```bash
git cherry-pick --abort
```

---

# 27. Git Blame

## git blame

Shows who last modified each line of a file.

```bash
git blame Main.java
```

Useful for understanding the history of a particular line.

---

# 28. Git Show

## git show

Displays information about a commit.

```bash
git show abc123
```

Latest commit:

```bash
git show HEAD
```

Show a specific file from a commit:

```bash
git show abc123:file.txt
```

---

# 29. Git Reflog

## git reflog

Shows where HEAD and branch references have previously pointed.

```bash
git reflog
```

Extremely useful for recovering commits after:

* `reset`
* `rebase`
* accidental branch deletion
* other history changes

Example:

```text
abc123 HEAD@{0}: reset
def456 HEAD@{1}: commit
```

You can often recover the previous state using the reflog.

---

# 30. Git Clean

## git clean

Removes untracked files.

Preview first:

```bash
git clean -n
```

Actually remove untracked files:

```bash
git clean -f
```

Remove untracked directories:

```bash
git clean -fd
```

**Be careful:** deleted untracked files are not normally recoverable through Git.

---

# 31. Git Restore

Restore files from a specific source.

```bash
git restore --source=HEAD file.txt
```

Restore from another branch:

```bash
git restore --source=main file.txt
```

---

# 32. Git Checkout

`git checkout` is an older multi-purpose command.

Switch branch:

```bash
git checkout main
```

Create branch:

```bash
git checkout -b feature
```

Restore file:

```bash
git checkout -- file.txt
```

Modern Git generally prefers:

```bash
git switch
git restore
```

for these separate operations.

---

# 33. Git Submodules

Submodules allow one Git repository to contain another Git repository.

Add submodule:

```bash
git submodule add https://github.com/user/library.git
```

Initialize submodules:

```bash
git submodule init
```

Download submodules:

```bash
git submodule update
```

Clone repository with submodules:

```bash
git clone --recurse-submodules https://github.com/user/project.git
```

---

# 34. Git Worktree

Allows multiple working directories connected to the same repository.

Create worktree:

```bash
git worktree add ../feature feature
```

List worktrees:

```bash
git worktree list
```

Remove worktree:

```bash
git worktree remove ../feature
```

Useful when you need to work on multiple branches simultaneously without repeatedly switching branches.

---

# 35. Git Bisect

Used to find which commit introduced a bug.

Start:

```bash
git bisect start
```

Mark current version as bad:

```bash
git bisect bad
```

Mark a known good version:

```bash
git bisect good abc123
```

Git checks out a commit in between.

Test it and mark:

```bash
git bisect good
```

or

```bash
git bisect bad
```

Repeat until Git identifies the problematic commit.

Finish:

```bash
git bisect reset
```

---

# 36. Git Archive

Creates an archive of a repository.

```bash
git archive HEAD
```

Create ZIP:

```bash
git archive --format=zip HEAD > project.zip
```

---

# 37. Git Grep

Searches tracked files.

```bash
git grep "TODO"
```

Search specific branch:

```bash
git grep "TODO" main
```

Useful for quickly searching a codebase.

---

# 38. Git Maintenance

## git gc

Performs garbage collection and repository optimization.

```bash
git gc
```

Usually Git handles maintenance automatically.

---

# 39. Git fsck

Checks repository integrity.

```bash
git fsck
```

Can help identify dangling or unreachable Git objects.

---

# 40. Git Help

Get help for a command.

```bash
git help commit
```

Short help:

```bash
git commit -h
```

General help:

```bash
git help
```

---

# 41. Git Version

```bash
git --version
```

Example:

```text
git version 2.x.x
```

---

# 42. GitHub CLI (`gh`)

The `gh` command is GitHub's official command-line interface.

Check installation:

```bash
gh --version
```

---

# 43. GitHub Login

## gh auth login

Authenticate with GitHub.

```bash
gh auth login
```

Check authentication:

```bash
gh auth status
```

Logout:

```bash
gh auth logout
```

---

# 44. GitHub Repositories

## gh repo create

Create a GitHub repository.

```bash
gh repo create
```

Create with a name:

```bash
gh repo create my-project
```

Create a public repository:

```bash
gh repo create my-project --public
```

Create a private repository:

```bash
gh repo create my-project --private
```

---

## gh repo clone

Clone a GitHub repository.

```bash
gh repo clone username/project
```

---

## gh repo view

View repository information.

```bash
gh repo view
```

---

## gh repo list

List repositories.

```bash
gh repo list
```

---

# 45. GitHub Pull Requests

## gh pr create

Create a pull request.

```bash
gh pr create
```

Specify title:

```bash
gh pr create --title "Add login feature"
```

Specify body:

```bash
gh pr create --title "Add login feature" --body "Implemented login functionality"
```

---

## gh pr list

List pull requests.

```bash
gh pr list
```

---

## gh pr view

View a pull request.

```bash
gh pr view 123
```

---

## gh pr checkout

Checkout a pull request locally.

```bash
gh pr checkout 123
```

---

## gh pr merge

Merge a pull request.

```bash
gh pr merge 123
```

---

## gh pr close

Close a pull request.

```bash
gh pr close 123
```

---

# 46. GitHub Issues

## gh issue create

Create an issue.

```bash
gh issue create
```

---

## gh issue list

List issues.

```bash
gh issue list
```

---

## gh issue view

View an issue.

```bash
gh issue view 123
```

---

## gh issue close

Close an issue.

```bash
gh issue close 123
```

---

# 47. GitHub Releases

## gh release create

Create a GitHub release.

```bash
gh release create v1.0.0
```

With title:

```bash
gh release create v1.0.0 --title "Version 1.0.0"
```

With notes:

```bash
gh release create v1.0.0 --notes "Initial release"
```

---

## gh release list

```bash
gh release list
```

---

## gh release view

```bash
gh release view v1.0.0
```

---

# 48. GitHub Actions

GitHub Actions workflows are generally managed through `.github/workflows/*.yml` files.

Git itself does not provide commands such as `git action`.

Using GitHub CLI:

```bash
gh workflow list
```

List workflow runs:

```bash
gh run list
```

View a run:

```bash
gh run view
```

Watch a running workflow:

```bash
gh run watch
```

Re-run a workflow:

```bash
gh run rerun <run-id>
```

---

# 49. GitHub API

GitHub CLI can also interact with the GitHub API.

```bash
gh api repos/OWNER/REPOSITORY
```

Example:

```bash
gh api repos/octocat/Hello-World
```

This is useful for automation and scripting.

---

# 50. Typical Git Development Workflow

## Starting a New Project

```bash
mkdir my-project

cd my-project

git init

git add .

git commit -m "Initial commit"

git branch -M main

git remote add origin https://github.com/user/my-project.git

git push -u origin main
```

---

# 51. Typical Feature Development Workflow

Create feature branch:

```bash
git switch -c feature/login
```

Check status:

```bash
git status
```

Make changes.

Stage:

```bash
git add .
```

Commit:

```bash
git commit -m "Add login functionality"
```

Push:

```bash
git push -u origin feature/login
```

Create Pull Request.

After PR is merged:

```bash
git switch main

git pull

git branch -d feature/login
```

---

# 52. Typical Bug Fix Workflow

```bash
git switch main

git pull

git switch -c bugfix/login-error
```

Fix the bug.

```bash
git add .

git commit -m "Fix login error"

git push -u origin bugfix/login-error
```

Create a Pull Request.

---

# 53. Daily Git Commands

These are the commands you will use most frequently.

```bash
git status

git add .

git commit -m "message"

git pull

git push

git switch branch-name

git switch -c new-branch

git branch

git merge branch-name

git log --oneline

git diff

git stash

git stash pop
```

---

# 54. Most Important Commands to Memorize

## Beginner Level

```bash
git init
git clone
git status
git add
git commit
git push
git pull
git branch
git switch
git merge
```

## Intermediate Level

```bash
git fetch
git diff
git stash
git restore
git reset
git revert
git rebase
git cherry-pick
git tag
git reflog
```

## Advanced Level

```bash
git rebase -i
git bisect
git worktree
git submodule
git reflog
git fsck
git filter-repo
```

## GitHub CLI

```bash
gh auth login
gh repo create
gh repo clone
gh repo view
gh repo list
gh pr create
gh pr list
gh pr view
gh pr checkout
gh pr merge
gh issue create
gh issue list
gh issue view
gh issue close
gh release create
gh workflow list
gh run list
gh run view
gh api
```

---

# 55. Git Command Cheat Sheet

| Command           | Purpose                              |
| ----------------- | ------------------------------------ |
| `git init`        | Create repository                    |
| `git clone`       | Clone repository                     |
| `git status`      | Check repository status              |
| `git add`         | Stage changes                        |
| `git commit`      | Save staged changes                  |
| `git log`         | View history                         |
| `git diff`        | View changes                         |
| `git branch`      | Manage branches                      |
| `git switch`      | Switch branches                      |
| `git merge`       | Merge branches                       |
| `git fetch`       | Download remote changes              |
| `git pull`        | Fetch + integrate                    |
| `git push`        | Upload commits                       |
| `git remote`      | Manage remotes                       |
| `git stash`       | Temporarily save changes             |
| `git restore`     | Restore files                        |
| `git reset`       | Move/reset HEAD and staging          |
| `git revert`      | Create commit undoing another commit |
| `git rebase`      | Reapply commits onto another base    |
| `git cherry-pick` | Apply a specific commit              |
| `git tag`         | Mark releases                        |
| `git reflog`      | Recover previous HEAD states         |
| `git blame`       | Find line authors                    |
| `git show`        | Show commit details                  |
| `git clean`       | Remove untracked files               |
| `git bisect`      | Find bug-introducing commit          |
| `git worktree`    | Manage multiple working trees        |
| `git submodule`   | Manage nested repositories           |
| `git grep`        | Search tracked files                 |
| `git archive`     | Create repository archive            |
| `git gc`          | Optimize repository                  |
| `git fsck`        | Check repository integrity           |
| `git help`        | Git documentation                    |
| `gh auth`         | GitHub authentication                |
| `gh repo`         | GitHub repositories                  |
| `gh pr`           | GitHub pull requests                 |
| `gh issue`        | GitHub issues                        |
| `gh release`      | GitHub releases                      |
| `gh workflow`     | GitHub Actions workflows             |
| `gh run`          | GitHub Actions runs                  |
| `gh api`          | GitHub API                           |

---

# 56. Git Mental Model

The most important thing to understand is the relationship between these four areas:

```text
                git add
Working ──────────────────→ Staging
                                │
                                │ git commit
                                ↓
                          Local Repository
                                │
                                │ git push
                                ↓
                         Remote Repository
                                │
                                │ git fetch / pull
                                ↓
                          Local Repository
```

Remember:

```text
git add       → Prepare changes

git commit    → Save changes locally

git push      → Upload commits

git fetch     → Download remote information

git pull      → Download + integrate

git merge     → Combine branches

git rebase    → Reapply commits on a new base

git stash     → Temporarily hide uncommitted work

git revert    → Undo using a new commit

git reset     → Move history/HEAD

git reflog    → Find previous HEAD states
```

This mental model is more important than memorizing every Git command.
