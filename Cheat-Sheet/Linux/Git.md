
## Introduction

**Git** is a free, open-source **distributed version control system** created by **Linus Torvalds** in **2005** for managing the Linux kernel source code. Git tracks changes to files over time — letting you save snapshots of your project, go back to any previous state, collaborate with others, and manage multiple versions of your work simultaneously. Unlike older systems, every developer has a **full copy of the entire history** on their machine. Git is the most widely used version control system in the world and is the backbone of platforms like **GitHub**, **GitLab**, and **Bitbucket**.


## Core Concepts

**Definition:** Understanding these concepts is essential before using Git — they explain how Git thinks.

### The Three Areas
**Definition:** Every file in a Git project lives in one of three areas at any given time.
```
Working Directory  →  Staging Area (Index)  →  Repository (.git)
    (Your files)         (git add)               (git commit)
```

| Area | Description |
|------|-------------|
| **Working Directory** | Your actual files — where you edit code |
| **Staging Area** | Files you've marked to include in the next commit |
| **Repository** | The `.git` folder — stores all commits and history |

### Four Object Types
**Definition:** Git stores everything internally as four types of objects.

| Object | Description |
|--------|-------------|
| **Blob** | File content (no filename, no metadata) |
| **Tree** | Directory listing — maps filenames to blobs |
| **Commit** | Snapshot — points to a tree + parent commit + metadata |
| **Tag** | Named pointer to a commit |

### HEAD
**Definition:** `HEAD` is a pointer that tells Git which commit you are currently on — usually points to a branch.
```bash
HEAD → main → commit abc123    # Normal state — on a branch
HEAD → commit abc123           # Detached HEAD — directly on a commit
```

### Commits
**Definition:** A commit is a permanent snapshot of all staged files — never changes once created.
```
Each commit stores:
  - A pointer to the file tree (what files looked like)
  - Parent commit hash (where it came from)
  - Author name, email, and timestamp
  - Your commit message
  - A unique SHA-1 hash (e.g. a3c4d9f...)
```

---

## Installation & Setup

**Definition:** Install Git and set up your identity — required before making any commits.

### Install Git
**Definition:** Download and install Git for your operating system.
```bash
# Ubuntu / Debian
sudo apt install git

# macOS (via Homebrew)
brew install git

# Windows
# Download from https://git-scm.com/download/win

# Check version
git --version
```

### Configure Identity
**Definition:** Set your name and email — these appear in every commit you make.
```bash
# Set globally (applies to all repos on this machine)
git config --global user.name  "Dark Kumar"
git config --global user.email "dark@example.com"

# Set for one specific repository only
git config user.name  "Dark Kumar"
git config user.email "dark@example.com"
```

### Configure Editor & Settings
**Definition:** Set your preferred text editor and other helpful defaults.
```bash
git config --global core.editor "code --wait"    # VS Code
git config --global core.editor "vim"            # Vim
git config --global core.editor "nano"           # Nano

git config --global init.defaultBranch main      # Default branch name
git config --global core.autocrlf input          # Line endings (Linux/macOS)
git config --global core.autocrlf true           # Line endings (Windows)
git config --global pull.rebase false            # Merge on pull (default)
git config --global color.ui auto               # Colored output
```

### View Configuration
**Definition:** See your current Git configuration at different levels.
```bash
git config --list                    # All settings
git config --global --list          # Global settings only
git config user.name                 # One specific value
git config --show-origin user.name  # Show which file sets this value
```

### Configuration Levels
**Definition:** Git settings can be set at three levels — each overrides the one above.

| Level | Flag | File Location | Scope |
|-------|------|---------------|-------|
| System | `--system` | `/etc/gitconfig` | All users on machine |
| Global | `--global` | `~/.gitconfig` | Current user, all repos |
| Local | (none) | `.git/config` | Current repo only |

---

## Initialize a Repository

**Definition:** Start tracking a project with Git — creates the hidden `.git` folder.

### New Repository
**Definition:** Turn any folder into a Git repository with `git init`.
```bash
# Initialize in current directory
git init

# Initialize and name the default branch
git init -b main

# Initialize a new folder
git init my-project
cd my-project
```

### Bare Repository
**Definition:** A repository without a working directory — used as a shared remote on servers.
```bash
git init --bare project.git    # No working files — just the .git data
```

---

## Staging & Committing

**Definition:** The two-step process of creating a commit — first stage files, then commit them.

### Stage Files
**Definition:** Add files to the staging area — tells Git what to include in the next commit.
```bash
git add file.txt               # Stage one specific file
git add file1.txt file2.txt    # Stage multiple files
git add .                      # Stage ALL changes in current directory
git add -A                     # Stage all changes (tracked + untracked)
git add *.js                   # Stage all .js files
git add src/                   # Stage everything inside a folder
git add -p                     # Interactive — choose specific hunks to stage
```

### Unstage Files
**Definition:** Remove files from staging without changing the actual file content.
```bash
git restore --staged file.txt  # Unstage one file (modern command)
git reset HEAD file.txt        # Unstage one file (older syntax)
git reset HEAD                 # Unstage everything
```

### Commit
**Definition:** Save a permanent snapshot of all staged files to the repository.
```bash
git commit -m "Add login feature"               # Commit with inline message
git commit                                       # Opens editor for message
git commit -am "Fix typo in README"             # Stage all tracked + commit
git commit --amend -m "Better message"          # Fix last commit message
git commit --amend --no-edit                    # Add to last commit, keep message
git commit --allow-empty -m "Empty commit"      # Commit with no changes
```

### Write Good Commit Messages
**Definition:** A good commit message explains WHY the change was made, not just WHAT.
```
Format:
  <type>: <short summary> (50 chars max)

  <optional longer body — explain WHY, not just WHAT>
  (72 chars per line)

  <optional footer — breaking changes, issue references>

Examples:
  feat: add user authentication
  fix: resolve null pointer in login service
  docs: update API documentation
  refactor: simplify database connection logic
  test: add unit tests for cart module
  chore: update dependencies

Types:
  feat     — new feature
  fix      — bug fix
  docs     — documentation only
  style    — formatting (no logic change)
  refactor — code change (no feature or fix)
  test     — adding/updating tests
  chore    — maintenance, tooling, dependencies
```

---

## Viewing Status & History

**Definition:** Commands to see what's changed, what's staged, and the full history of commits.

### Check Status
**Definition:** See which files are modified, staged, or untracked.
```bash
git status          # Full status — all details
git status -s       # Short format — compact one-line-per-file
git status -sb      # Short format + current branch name
```

**Status symbols (short format):**

| Symbol | Meaning |
|--------|---------|
| `??` | Untracked — Git doesn't know about this file |
| `A ` | Newly added to staging |
| `M ` | Modified and staged |
| ` M` | Modified but NOT staged |
| `MM` | Modified, partially staged |
| `D ` | Deleted and staged |
| `R ` | Renamed |

### View Commit History
**Definition:** See the list of all past commits on the current branch.
```bash
git log                          # Full log — hash, author, date, message
git log --oneline                # Compact — one line per commit
git log --oneline --graph        # ASCII branch graph
git log --oneline --graph --all  # Graph of ALL branches
git log -5                       # Last 5 commits only
git log --author="Dark"          # Commits by a specific author
git log --since="2025-01-01"     # Commits after a date
git log --until="2025-06-01"     # Commits before a date
git log --grep="login"           # Commits with "login" in the message
git log -- file.txt              # Commits that changed a specific file
git log -p                       # Full diff of each commit
git log --stat                   # Files changed + line counts per commit
git log --follow file.txt        # Follow file through renames
```

### View a Specific Commit
**Definition:** Inspect the full details and changes of one commit.
```bash
git show abc1234                 # Show commit details + diff
git show HEAD                    # Show latest commit
git show HEAD~1                  # Show commit before HEAD
git show HEAD:file.txt           # Show file content at HEAD
git show abc1234:src/app.js      # File content at specific commit
```

---

## Undoing Changes

**Definition:** Git has several ways to undo changes — choose based on whether commits are public or local.

### Discard Working Directory Changes
**Definition:** Throw away unsaved changes in your working directory — this CANNOT be undone.
```bash
git restore file.txt             # Discard changes to one file (modern)
git restore .                    # Discard ALL working directory changes
git checkout -- file.txt         # Same as restore (older syntax)
git clean -fd                    # Delete untracked files and directories
git clean -n                     # Dry run — show what would be deleted
```

### Undo Last Commit (Local — Not Pushed)
**Definition:** Move HEAD back one commit — three modes depending on what to do with changes.
```bash
git reset --soft HEAD~1    # Undo commit — keep changes STAGED
git reset --mixed HEAD~1   # Undo commit — keep changes in working dir (default)
git reset --hard HEAD~1    # Undo commit — DISCARD all changes (cannot undo!)
```

### Undo Any Commit (Safe — Public)
**Definition:** Create a NEW commit that reverses a previous one — safe for shared branches.
```bash
git revert abc1234         # Create new commit that undoes abc1234
git revert HEAD            # Revert the latest commit
git revert HEAD~3..HEAD    # Revert last 3 commits
git revert --no-commit abc1234   # Stage the revert without committing yet
```

### Reset vs Revert

| | `git reset` | `git revert` |
|--|-------------|--------------|
| History | Rewrites it | Preserves it |
| Safe to use on shared branches | ❌ No | ✅ Yes |
| Creates new commit | No | Yes |
| Use when | Local changes not pushed | Already pushed commits |

### Recover Deleted Commits
**Definition:** Use `reflog` to find and restore commits that seem lost.
```bash
git reflog                      # Show history of HEAD movements
git checkout abc1234            # Go to the lost commit
git branch recover-branch       # Create branch from it
git reset --hard abc1234        # Or reset to it directly
```

---

## Branches

**Definition:** A branch is a lightweight pointer to a commit — allows parallel development without affecting main code.

### Create Branches
**Definition:** Make a new branch — it starts at the current commit.
```bash
git branch feature-login         # Create branch (don't switch)
git checkout -b feature-login    # Create AND switch (older syntax)
git switch -c feature-login      # Create AND switch (modern syntax)
git branch feature-x abc1234     # Create branch from specific commit
git branch feature-x origin/main # Create branch from remote branch
```

### Switch Branches
**Definition:** Move to a different branch — working directory updates to match.
```bash
git switch main                  # Switch to main (modern)
git checkout main                # Switch to main (older)
git switch -                     # Switch to previous branch
git checkout -                   # Same (older syntax)
```

### List Branches
**Definition:** View all branches — local, remote, or both.
```bash
git branch                       # Local branches only
git branch -v                    # Local + last commit on each
git branch -r                    # Remote branches only
git branch -a                    # All branches (local + remote)
git branch --merged              # Branches already merged into current
git branch --no-merged           # Branches not yet merged
```

### Rename & Delete Branches
**Definition:** Rename a branch or delete it once it is no longer needed.
```bash
git branch -m old-name new-name  # Rename current branch
git branch -m new-name           # Rename branch you're currently on

git branch -d feature-login      # Delete (only if merged)
git branch -D feature-login      # Force delete (even if not merged)

# Delete remote branch
git push origin --delete feature-login
git push origin :feature-login   # Older syntax
```

---

## Merging

**Definition:** Combine changes from one branch into another — the most common way to integrate work.

### Basic Merge
**Definition:** Merge another branch into the current branch — Git creates a merge commit if needed.
```bash
git switch main
git merge feature-login          # Merge feature-login into main
git merge --no-ff feature-login  # Always create merge commit (no fast-forward)
git merge --squash feature-login # Squash all commits into one (then commit manually)
git merge --abort                # Cancel an in-progress merge
```

### Fast-Forward vs 3-Way Merge
**Definition:** Git uses fast-forward when no new commits exist on the base — otherwise a merge commit is created.
```
Fast-Forward (no divergence):
  main:    A → B
  feature: A → B → C → D
  result:  main moves to D (no merge commit)

3-Way Merge (diverged):
  main:    A → B → C
  feature: A → B → D → E
  result:  A → B → C → D → E → M (M = merge commit)
```

### Resolve Merge Conflicts
**Definition:** When the same lines are changed differently — Git pauses and asks you to resolve.
```bash
# Step 1: Attempt merge — conflicts reported
git merge feature-login

# Step 2: Open conflicted file — it looks like:
<<<<<<< HEAD
  const name = "main version";      # Your current branch version
=======
  const name = "feature version";   # Incoming branch version
>>>>>>> feature-login

# Step 3: Edit the file — remove conflict markers, keep what you want

# Step 4: Stage the resolved file
git add conflicted-file.js

# Step 5: Complete the merge
git commit
```

---

## Rebasing

**Definition:** Reapply commits on top of another branch — creates a cleaner, linear history.

### Basic Rebase
**Definition:** Move your branch's commits so they start from the tip of another branch.
```bash
git switch feature-login
git rebase main              # Reapply feature commits on top of latest main

# If conflicts occur during rebase:
git rebase --continue        # After resolving conflicts — continue
git rebase --skip            # Skip the current conflicting commit
git rebase --abort           # Cancel and go back to before rebase
```

### Interactive Rebase
**Definition:** Rewrite, reorder, squash, or edit commits before sharing — powerful history cleanup tool.
```bash
git rebase -i HEAD~3         # Interactively edit last 3 commits
git rebase -i abc1234        # Edit all commits after abc1234
```

**Interactive rebase commands (shown in editor):**
```
pick   abc1234 Add login feature      # Keep commit as-is
reword abc1234 Add login feature      # Keep commit, edit message
edit   abc1234 Add login feature      # Stop here — amend the commit
squash abc1234 Add login feature      # Combine into previous commit (keep message)
fixup  abc1234 Add login feature      # Combine into previous commit (discard message)
drop   abc1234 Add login feature      # Delete this commit entirely
```

### Rebase vs Merge

| | `git merge` | `git rebase` |
|--|-------------|--------------|
| History | Preserves all history | Creates clean linear history |
| Merge commit | Yes (usually) | No |
| Safe on shared branches | ✅ Yes | ❌ No — rewrites history |
| Use when | Merging feature to main | Cleaning up local commits |

> **Golden Rule:** Never rebase commits that have been pushed to a shared branch.

---

## Remote Repositories

**Definition:** A remote is a version of your repo hosted on a server — allows collaboration with others.

### Manage Remotes
**Definition:** Add, view, rename, and remove connections to remote repositories.
```bash
git remote                          # List remote names
git remote -v                       # List remotes with their URLs
git remote add origin https://github.com/user/repo.git   # Add remote
git remote add upstream https://github.com/original/repo.git  # Second remote
git remote rename origin new-name   # Rename remote
git remote remove origin            # Delete remote connection
git remote set-url origin https://github.com/user/new-repo.git  # Change URL
git remote show origin              # Detailed info about a remote
```

### Remote URL Formats
**Definition:** Two protocols for connecting to remote repos — HTTPS is simpler, SSH is more secure.
```bash
# HTTPS — uses username/password or token
https://github.com/username/repo.git

# SSH — uses SSH key pair (more secure, no password needed)
git@github.com:username/repo.git

# Switch existing remote from HTTPS to SSH
git remote set-url origin git@github.com:username/repo.git
```

---

## Fetch, Pull & Push

**Definition:** Commands to synchronize your local repository with a remote.

### Fetch
**Definition:** Download remote changes WITHOUT merging — safe to run anytime to see what's new.
```bash
git fetch origin                    # Fetch all changes from origin
git fetch origin main               # Fetch only the main branch
git fetch --all                     # Fetch from all remotes
git fetch --prune                   # Fetch + remove deleted remote branches
```

### Pull
**Definition:** Fetch AND integrate remote changes — combines `fetch` + `merge` (or `rebase`).
```bash
git pull                            # Pull from tracked remote branch
git pull origin main                # Pull specific branch from origin
git pull --rebase                   # Pull with rebase instead of merge
git pull --no-rebase                # Pull with merge (explicit)
git pull --ff-only                  # Only if fast-forward is possible
```

### Push
**Definition:** Upload your local commits to the remote repository.
```bash
git push origin main                # Push main branch to origin
git push                            # Push current branch (if tracking set)
git push -u origin main             # Push + set as tracking branch
git push --all origin               # Push ALL branches
git push origin --tags              # Push all tags
git push origin feature-login       # Push specific branch

# Force push (use carefully — rewrites remote history)
git push --force origin main        # Force push (dangerous)
git push --force-with-lease origin main  # Safer force push — fails if remote has new commits
```

### Set Tracking Branch
**Definition:** Link your local branch to a remote branch — enables plain `git push`/`git pull`.
```bash
git branch --set-upstream-to=origin/main main
git push -u origin main             # Push and set tracking at the same time
```

---

## Cloning

**Definition:** Download a complete copy of a remote repository — full history included.

### Basic Clone
**Definition:** Clone an entire repository to your local machine.
```bash
git clone https://github.com/user/repo.git          # Clone to folder named 'repo'
git clone https://github.com/user/repo.git my-app   # Clone to custom folder name
git clone git@github.com:user/repo.git              # Clone via SSH
```

### Partial Clones
**Definition:** Clone only part of the history or a single branch — faster for large repos.
```bash
git clone --depth 1 https://github.com/user/repo.git       # Shallow — latest commit only
git clone --depth 10 https://github.com/user/repo.git      # Last 10 commits only
git clone --branch feature-x https://github.com/user/repo.git  # One specific branch
git clone --single-branch --branch main https://...         # Only main branch history
```

---

## Tags

**Definition:** A named reference to a specific commit — used to mark release versions like `v1.0.0`.

### Create Tags
**Definition:** Two types of tags — lightweight (just a pointer) or annotated (stores extra data).
```bash
# Lightweight tag — just a pointer to a commit
git tag v1.0                        # Tag current commit
git tag v1.0 abc1234                # Tag a specific commit

# Annotated tag — stores tagger name, date, message (recommended for releases)
git tag -a v1.0 -m "Version 1.0 release"
git tag -a v1.0 abc1234 -m "Version 1.0"
```

### List & View Tags
**Definition:** See all tags or inspect a specific one.
```bash
git tag                             # List all tags
git tag -l "v1.*"                   # List tags matching pattern
git show v1.0                       # Show tag details and commit
```

### Share & Delete Tags
**Definition:** Tags are not pushed automatically — you must push them explicitly.
```bash
git push origin v1.0                # Push one specific tag
git push origin --tags              # Push all tags

git tag -d v1.0                     # Delete local tag
git push origin --delete v1.0      # Delete remote tag
git push origin :refs/tags/v1.0    # Older syntax for delete
```

---

## Stashing

**Definition:** Temporarily save uncommitted changes so you can switch context without committing.

### Save & Restore Stash
**Definition:** Push changes onto a stash stack and pop them back when needed.
```bash
git stash                           # Stash tracked changes
git stash push -m "WIP: login form" # Stash with a description
git stash -u                        # Stash including untracked files
git stash -a                        # Stash everything (including ignored files)

git stash pop                       # Apply most recent stash + remove it
git stash apply                     # Apply most recent stash + KEEP it
git stash apply stash@{2}           # Apply specific stash
```

### Manage Stashes
**Definition:** View, inspect, and clean up the stash list.
```bash
git stash list                      # Show all stashes
git stash show                      # Summary of most recent stash
git stash show -p                   # Full diff of most recent stash
git stash show stash@{1}            # Show specific stash

git stash drop                      # Delete most recent stash
git stash drop stash@{2}            # Delete specific stash
git stash clear                     # Delete ALL stashes
```

### Create Branch from Stash
**Definition:** Apply a stash to a new branch — useful if applying causes conflicts.
```bash
git stash branch new-branch         # Create branch + apply stash + drop stash
```

---

## Cherry Pick

**Definition:** Apply a specific commit from one branch onto the current branch — copy just that one commit.

### Basic Cherry Pick
**Definition:** Pick one or more specific commits and apply them to the current branch.
```bash
git cherry-pick abc1234             # Apply one commit
git cherry-pick abc1234 def5678     # Apply multiple commits
git cherry-pick abc1234..def5678    # Apply a range of commits
git cherry-pick main~1              # Apply second-to-last commit on main
```

### Cherry Pick Options
**Definition:** Control whether to commit immediately or stage for review first.
```bash
git cherry-pick --no-commit abc1234  # Stage changes but don't commit yet
git cherry-pick -e abc1234           # Cherry-pick and edit the commit message
git cherry-pick --abort              # Cancel cherry-pick in progress
git cherry-pick --continue           # Continue after resolving conflicts
```

---

## Git Diff

**Definition:** Show the exact line-by-line differences between versions of files.

### Compare Working Directory
**Definition:** See what has changed but not yet been staged.
```bash
git diff                            # Working dir vs staging area
git diff file.txt                   # Changes in one specific file
```

### Compare Staging Area
**Definition:** See what is staged and ready to be committed.
```bash
git diff --staged                   # Staging area vs last commit
git diff --cached                   # Same as --staged
git diff --staged file.txt          # Staged changes in one file
```

### Compare Commits & Branches
**Definition:** Compare any two commits, branches, or tags.
```bash
git diff main feature-x             # Difference between two branches
git diff abc1234 def5678            # Difference between two commits
git diff HEAD~1 HEAD                # Last commit vs the one before
git diff v1.0 v2.0                  # Difference between two tags
git diff main..feature-x            # Same as main vs feature-x
```

### Useful Diff Options
**Definition:** Flags to customize diff output format.
```bash
git diff --stat                     # Summary — only filenames and line counts
git diff --name-only                # Only filenames — no content
git diff --word-diff                # Highlight changed words inline
git diff -w                         # Ignore all whitespace changes
```

---

## Git Log

**Definition:** Advanced log commands to search, filter, and visualize the commit history.

### Filtering Log
**Definition:** Narrow down history to find specific commits.
```bash
git log --oneline -10               # Last 10 commits, one line each
git log --author="Dark"             # Commits by author name or email
git log --since="2 weeks ago"       # Commits within time period
git log --since="2025-01-01" --until="2025-06-01"
git log --grep="fix"                # Commits where message contains "fix"
git log -S "functionName"           # Commits that added/removed this string
git log -G "regex"                  # Commits where diff matches regex
git log -- path/to/file.txt         # Commits that touched a specific file
git log --diff-filter=D             # Only commits that deleted files
```

### Visualizing History
**Definition:** Display branches and merges as an ASCII graph.
```bash
git log --oneline --graph --all --decorate
# Shows: all branches + graph + tag names

# Pretty custom format
git log --pretty=format:"%h %ad | %s%d [%an]" --date=short
```

### Pretty Format Codes
**Definition:** Placeholders for building custom log output formats.

| Code | Meaning |
|------|---------|
| `%h` | Abbreviated commit hash |
| `%H` | Full commit hash |
| `%s` | Subject (first line of message) |
| `%b` | Body of message |
| `%an` | Author name |
| `%ae` | Author email |
| `%ad` | Author date |
| `%cd` | Committer date |
| `%d` | Ref names (branch, tag) |
| `%n` | Newline |

---

## Git Blame

**Definition:** Show which commit and author last modified each line of a file.

### Basic Blame
**Definition:** Annotate every line of a file with commit hash, author, and date.
```bash
git blame file.txt                  # Annotate entire file
git blame -L 10,20 file.txt         # Annotate only lines 10–20
git blame -w file.txt               # Ignore whitespace changes
git blame --since="1 month ago" file.txt  # Blame since a date
```

### Reading Blame Output
**Definition:** Each line shows who last changed it and in which commit.
```
abc1234a (Dark Kumar   2025-01-15 10:30:00) const name = "Dark";
def5678b (Alice Smith  2025-01-12 14:20:00) const age  = 25;
```

---

## Searching

**Definition:** Find specific content across commits, files, and history.

### Search File Content
**Definition:** Search for a string across all tracked files.
```bash
git grep "TODO"                     # Find "TODO" in all tracked files
git grep -n "functionName"          # With line numbers
git grep -i "todo"                  # Case-insensitive
git grep -l "TODO"                  # Only filenames, not content
git grep "TODO" -- "*.js"           # Only in .js files
git grep "text" abc1234             # Search in specific commit
```

### Search Commit History
**Definition:** Find commits that introduced or removed specific content.
```bash
git log -S "secretKey"              # Commits that added/removed "secretKey"
git log -G "password.*="            # Commits matching a regex pattern
git log --all --grep="hotfix"       # All branches, message contains "hotfix"
```

---

## Submodules

**Definition:** Include one Git repository inside another — useful for managing external dependencies.

### Add & Use Submodules
**Definition:** Add an external repository as a subdirectory of your project.
```bash
git submodule add https://github.com/user/lib.git libs/lib   # Add submodule
git submodule init                  # Initialize submodule config
git submodule update                # Clone/update all submodules
git submodule update --init --recursive    # Init + update (including nested)
```

### Clone with Submodules
**Definition:** When cloning a project that has submodules — they are not cloned automatically.
```bash
git clone --recurse-submodules https://github.com/user/repo.git
# Or after cloning:
git submodule update --init --recursive
```

### Update Submodules
**Definition:** Pull the latest changes in submodule repositories.
```bash
git submodule update --remote       # Pull latest from each submodule's remote
git submodule foreach git pull origin main  # Run command in each submodule
```

---

## Git Hooks

**Definition:** Scripts that Git runs automatically before or after events — automate quality checks.

### Hook Location
**Definition:** Hooks live in `.git/hooks/` — create executable scripts with the hook name.
```bash
ls .git/hooks/      # See available hook samples
```

### Common Hooks
**Definition:** The most useful hooks for automating workflow tasks.

| Hook | When it runs | Common use |
|------|-------------|------------|
| `pre-commit` | Before commit is created | Run linter, tests |
| `commit-msg` | After commit message is entered | Validate message format |
| `pre-push` | Before `git push` runs | Run test suite |
| `post-commit` | After commit is created | Notifications |
| `post-merge` | After `git merge` completes | Install dependencies |
| `pre-rebase` | Before rebase starts | Safety checks |

### Example pre-commit Hook
**Definition:** A hook that runs tests before allowing a commit — reject if tests fail.
```bash
#!/bin/sh
# .git/hooks/pre-commit
npm test
if [ $? -ne 0 ]; then
  echo "Tests failed — commit rejected"
  exit 1
fi
echo "All tests passed — committing"
exit 0
```

```bash
chmod +x .git/hooks/pre-commit     # Make the hook executable
```

---

## Git Aliases

**Definition:** Custom shortcuts for long or frequently typed Git commands.

### Set Aliases
**Definition:** Create short names for commands you type all the time.
```bash
# Set globally
git config --global alias.st    status
git config --global alias.co    checkout
git config --global alias.br    branch
git config --global alias.ci    commit
git config --global alias.lg    "log --oneline --graph --all"
git config --global alias.last  "log -1 HEAD"
git config --global alias.undo  "reset --soft HEAD~1"
git config --global alias.unstage "restore --staged"
```

### Use Aliases
**Definition:** Call your alias like any other Git command.
```bash
git st        # Same as: git status
git co main   # Same as: git checkout main
git lg        # Same as: git log --oneline --graph --all
git undo      # Same as: git reset --soft HEAD~1
```

### Shell Aliases (Optional)
**Definition:** Even shorter shortcuts set in your shell config (`.bashrc` / `.zshrc`).
```bash
alias g="git"
alias gs="git status"
alias ga="git add ."
alias gc="git commit -m"
alias gp="git push"
alias gpl="git pull"
alias gl="git log --oneline --graph --all"
```

---

## gitignore

**Definition:** A `.gitignore` file tells Git which files and folders to ignore — never track them.

### Create .gitignore
**Definition:** Place a `.gitignore` file in the root of your repository.
```bash
touch .gitignore       # Create the file
```

### Gitignore Patterns
**Definition:** Rules and patterns for specifying what to ignore.
```gitignore
# Comments start with #

# Ignore a specific file
secret.env
config.local.js

# Ignore all files with an extension
*.log
*.tmp
*.pyc
*.class

# Ignore a specific folder and everything inside it
node_modules/
dist/
build/
.cache/
__pycache__/

# Ignore any file named .env in any subfolder
**/.env

# Ignore all .txt files EXCEPT README.txt
*.txt
!README.txt

# Ignore files in root directory only (not subdirectories)
/config.json

# Ignore everything inside a folder but keep the folder itself
logs/*
!logs/.gitkeep

# Pattern matching
debug[0-9].log        # debug0.log to debug9.log
*.{jpg,png,gif}       # Any image file
```

### Common .gitignore Templates
**Definition:** Standard ignore patterns for popular languages and tools.
```gitignore
# Node.js
node_modules/
npm-debug.log
.env
.env.local
dist/

# Python
__pycache__/
*.py[cod]
*.egg-info/
.venv/
venv/
dist/
.env

# macOS
.DS_Store
.AppleDouble
.LSOverride

# Windows
Thumbs.db
ehthumbs.db
Desktop.ini

# IDEs
.vscode/
.idea/
*.sublime-project
*.sublime-workspace

# Git global ignore (set once for all repos)
git config --global core.excludesFile ~/.gitignore_global
```

### Fix Accidentally Tracked Files
**Definition:** If you committed something that should be ignored — remove it from tracking.
```bash
git rm --cached file.txt           # Untrack one file (keep local copy)
git rm --cached -r node_modules/   # Untrack entire folder
git rm --cached .                  # Untrack everything (re-apply .gitignore)
git commit -m "Remove tracked files that should be ignored"
```

---

## gitattributes

**Definition:** A `.gitattributes` file controls how Git handles specific file types — line endings, diffs, merges.

### Common Uses
**Definition:** Define per-file settings for line endings, binary files, and diff behavior.
```gitattributes
# Force Unix line endings for all text files
* text=auto eol=lf

# Windows line endings for batch files
*.bat text eol=crlf
*.cmd text eol=crlf

# Mark binary files — prevents line ending conversion and diffing
*.png  binary
*.jpg  binary
*.gif  binary
*.pdf  binary
*.zip  binary
*.exe  binary

# Use custom diff driver for a file type
*.md diff=markdown

# Merge strategy for generated files
package-lock.json merge=ours
```

---

## Git Workflows

**Definition:** Team conventions for how branches are used and code is merged — choose one and stick to it.

### Centralized Workflow
**Definition:** Everyone works on `main` — simplest setup, no feature branches.
```
All developers → push/pull from main
Good for: small teams, simple projects
```

### Feature Branch Workflow
**Definition:** Every feature or fix gets its own branch — merged to main when done.
```
main
  ├── feature/login        ← new feature
  ├── feature/dashboard    ← another feature
  └── fix/typo-navbar      ← bug fix

Steps:
1. git switch -c feature/login
2. Work and commit
3. git push -u origin feature/login
4. Open Pull Request → review → merge to main
5. git branch -d feature/login
```

### Gitflow Workflow
**Definition:** Strict branching for versioned releases — uses `main`, `develop`, `feature`, `release`, and `hotfix` branches.
```
main        — production-ready code only
develop     — integration branch for features
feature/*   — new features (branch from develop)
release/*   — release preparation (branch from develop)
hotfix/*    — urgent fixes for production (branch from main)

Flow:
feature → develop → release → main
hotfix  → main + develop
```

### Trunk-Based Development
**Definition:** Everyone commits to `main` (trunk) frequently — short-lived feature branches of max 1-2 days.
```
main ← all developers commit here often
short-lived branches → merge within 24-48 hours
Requires: feature flags, good test coverage
Good for: CI/CD, fast-moving teams
```

---

## GitHub Flow

**Definition:** A simplified workflow used by GitHub and many modern teams — six clear steps.

### The Six Steps
**Definition:** A lightweight, branch-based workflow that works well with Pull Requests.
```bash
# Step 1: Create a branch
git switch -c feature/user-auth

# Step 2: Make changes and commit
git add .
git commit -m "feat: add JWT authentication"

# Step 3: Push to remote
git push -u origin feature/user-auth

# Step 4: Open a Pull Request on GitHub
# → Code review happens here

# Step 5: Merge after approval
# → Done via GitHub UI or:
git switch main
git merge feature/user-auth

# Step 6: Delete the branch
git branch -d feature/user-auth
git push origin --delete feature/user-auth
```

---

## Debugging with Git

**Definition:** Git has powerful tools to track down exactly when and where a bug was introduced.

### Git Bisect
**Definition:** Binary search through commit history to find the commit that introduced a bug.
```bash
# Step 1: Start bisect session
git bisect start

# Step 2: Mark current state (has the bug)
git bisect bad

# Step 3: Mark a known good commit (no bug)
git bisect good v1.0
git bisect good abc1234

# Step 4: Git checks out a commit halfway between
# You test it, then mark it:
git bisect good     # This commit is fine
git bisect bad      # This commit has the bug

# Git keeps narrowing until it finds the first bad commit
# Step 5: When done — reset to original state
git bisect reset
```

### Git Bisect with Script
**Definition:** Automate bisect by providing a test script — Git runs it for each commit.
```bash
git bisect start
git bisect bad HEAD
git bisect good v1.0
git bisect run npm test         # Runs test for each commit
git bisect reset
```

### Reflog
**Definition:** A safety net — tracks every movement of HEAD, even across resets and rebases.
```bash
git reflog                      # Show history of HEAD movements
git reflog show feature-branch  # Reflog for a specific branch

# Recover from bad reset
git reflog                      # Find the commit before the reset
git reset --hard HEAD@{3}       # Jump back to that point
```

---

## Tips & Tricks

**Definition:** Useful Git shortcuts and patterns that save time in daily development.

### Quick Fixes
**Definition:** Common small fixes for everyday situations.
```bash
# Fix last commit message
git commit --amend -m "Corrected message"

# Add forgotten file to last commit
git add forgotten-file.js
git commit --amend --no-edit

# Undo last commit but keep changes
git reset --soft HEAD~1

# Discard all local changes and sync with remote
git fetch origin
git reset --hard origin/main

# See which branch a commit is on
git branch --contains abc1234

# Find all branches that contain a commit
git branch -a --contains abc1234
```

### Working with Commits
**Definition:** Useful ways to inspect and reference commits.
```bash
# Reference commits relatively
HEAD         # Current commit
HEAD~1       # One commit before HEAD
HEAD~3       # Three commits before HEAD
HEAD^        # First parent (same as HEAD~1 for linear)
HEAD^2       # Second parent (for merge commits)
abc1234^1    # First parent of commit abc1234

# Copy file from another branch
git checkout feature-x -- src/utils.js

# See what changed between two dates
git diff HEAD@{7.days.ago} HEAD

# Count commits on current branch
git rev-list --count HEAD

# Find first commit in repo
git rev-list --max-parents=0 HEAD
```

### Helpful Shortcuts
**Definition:** Time-saving command patterns for common scenarios.
```bash
# Stage only already-tracked files (no new files)
git add -u

# Stage and commit in one command
git commit -am "Quick fix"

# See remote URL
git remote get-url origin

# Show all aliases
git config --get-regexp alias

# Clean build artifacts and ignored files
git clean -fdx

# Check if you're inside a git repo
git rev-parse --is-inside-work-tree

# Show size of repo
git count-objects -vH
```

---

## Best Practices

**Definition:** Guidelines for using Git effectively in teams and solo projects.

### Commit Practices
**Definition:** Small, focused commits make history readable and bugs easy to track down.
```bash
# Bad — one giant commit
git commit -m "lots of changes"

# Good — small, specific commits
git commit -m "feat: add email validation to signup form"
git commit -m "fix: handle null user in dashboard"
git commit -m "docs: add API usage examples to README"
```

### Branch Naming
**Definition:** Use a consistent naming convention — makes branches easy to understand at a glance.
```
feature/user-authentication     ← new feature
fix/login-null-pointer           ← bug fix
hotfix/critical-security-patch  ← urgent production fix
release/v2.1.0                   ← release preparation
docs/update-api-reference        ← documentation only
refactor/database-layer          ← internal restructure
chore/upgrade-dependencies       ← maintenance
```

### Protecting Main Branch
**Definition:** Use these strategies to keep your main branch stable and deployable.
```
✅ Require Pull Requests before merging
✅ Require code review approvals
✅ Require status checks (tests must pass)
✅ Prevent force pushes to main
✅ Require branches to be up to date before merge
✅ Delete branches after merge (keep it clean)
```

### Daily Workflow
**Definition:** A healthy Git routine that keeps your work organized.
```bash
# Start of day — sync with remote
git switch main
git pull origin main

# Start new work
git switch -c feature/my-feature

# Commit often — small, focused changes
git add -p                     # Stage specific hunks
git commit -m "feat: add X"

# Keep branch up to date with main
git fetch origin
git rebase origin/main

# Before PR — clean up commit history
git rebase -i HEAD~3           # Squash WIP commits into meaningful ones

# Push and open PR
git push -u origin feature/my-feature
```

### Things to Avoid
**Definition:** Common Git mistakes that cause pain for you and your team.
```bash
# ❌ Force pushing to shared branches
git push --force origin main      # Rewrites history others have

# ❌ Committing sensitive data
git add .env                      # Never commit API keys, passwords

# ❌ Giant commits
git commit -am "work"             # Hard to review and revert

# ❌ Committing directly to main
git switch main
git commit -m "quick fix"         # Skips review process

# ❌ Leaving TODO/debug code in commits
# Remove console.log, debug flags before committing

# ❌ Ignoring .gitignore
# Always set up .gitignore before first commit
```

### Summary of Rules

* Commit **early and often** — small focused commits
* Write **meaningful commit messages** — what AND why
* Use **branches** for every feature and fix
* **Never force-push** to shared/main branches
* **Never commit secrets** — API keys, passwords, tokens
* **Pull before push** — stay in sync with remote
* **Review your diff** before committing — `git diff --staged`
* Use `.gitignore** from the very start of a project
* **Delete merged branches** — keep the repo clean
* Use **Pull Requests** for code review before merging to main
