
# 🚀 Introduction to Git Commands

Git is a **distributed version control system** used to track changes in code, collaborate with teams, and manage project history efficiently. Whether you're building a small project or working in a large-scale production environment, Git is a **must-have skill**.

In real-world development:
- Developers use Git to track code changes
- DevOps engineers use it in CI/CD pipelines
- Teams collaborate using platforms like GitHub and GitLab

👉 If you're a **student, beginner, developer, or DevOps engineer**, learning Git commands will make your workflow faster, safer, and more professional.


## Installation & Setup

### git --version
Check installed Git version
```bash
git --version
````

### git config

Set user configuration (name & email)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

# Repository Management

## Initialize & Clone

### git init

Initialize a new Git repository

```bash
git init
```

### git clone

Clone a remote repository

```bash
git clone https://github.com/user/repo.git
```

---

# 📄 Basic Workflow Commands

## File Tracking

### git status

Check current state of working directory

```bash
git status
```

### git add

Add files to staging area

```bash
git add file.txt
git add .
```

### git commit

Save changes with a message

```bash
git commit -m "Initial commit"
```

---

# 🔍 Viewing Changes & History

## Logs & Differences

### git log

View commit history

```bash
git log
```

### git diff

Show changes between commits or files

```bash
git diff
```

---

# 🌿 Branching & Merging

## Branch Management

### git branch

List or create branches

```bash
git branch
git branch feature-branch
```

### git checkout

Switch branches

```bash
git checkout feature-branch
```

### git switch

Modern way to switch branches

```bash
git switch feature-branch
```

### git merge

Merge branches

```bash
git merge feature-branch
```

---

# 🔄 Remote Repositories

## Working with Remote

### git remote

Manage remote repositories

```bash
git remote -v
```

### git push

Push changes to remote repo

```bash
git push origin main
```

### git pull

Fetch and merge remote changes

```bash
git pull origin main
```

### git fetch

Download changes without merging

```bash
git fetch
```

---

# ⚡ Undoing Changes

## Fix Mistakes

### git restore

Discard changes in working directory

```bash
git restore file.txt
```

### git reset

Unstage or reset commits

```bash
git reset file.txt
git reset --hard HEAD~1
```

### git revert

Create a new commit to undo changes

```bash
git revert <commit_id>
```

---

# 🧠 Stashing Changes

## Temporary Save

### git stash

Save changes temporarily

```bash
git stash
```

### git stash pop

Apply stashed changes

```bash
git stash pop
```

---

# 🧹 Cleaning & Maintenance

## Remove Unwanted Files

### git clean

Delete untracked files

```bash
git clean -f
```

---

# 🔐 Tags & Releases

## Version Tagging

### git tag

Create a tag

```bash
git tag v1.0
```

### git push --tags

Push tags to remote

```bash
git push --tags
```

---

# ⚙️ Advanced Commands

## Rewriting History

### git rebase

Reapply commits on top of another base

```bash
git rebase main
```

---

# 📊 Common Git Workflow (Real-World)

```bash
git clone repo_url
git checkout -b feature
git add .
git commit -m "Add feature"
git push origin feature
```

---

# 💡 Pro Tips

* Always write meaningful commit messages
* Use branches for every feature or fix
* Pull latest changes before pushing
* Avoid `git reset --hard` unless you’re sure

---

# 📌 Conclusion

Git commands are the backbone of modern software development. Mastering them will help you:

* Work efficiently in teams
* Track and manage code changes
* Avoid costly mistakes

👉 Start practicing daily, and Git will quickly become second nature.

---

**🔥 Keep this cheat sheet bookmarked on bluemd.in for quick reference!**

```
```
