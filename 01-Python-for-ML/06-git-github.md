# Git & GitHub Basics

- Git is a Version Control System (VCS) Version Control System keeps track of every change you make to your files.
- Git works on your computer and GitHub stores your Git repositories online.
# Commands & Examples


## 1️⃣ Initialize a Git Repository

- Command

```bash
git init
```

- What does it do?

1. Converts a normal folder into a Git repository.

2. Git creates a hidden folder named `.git` which stores all version history.

## Example

### Before

```
MyProject/
```

Run

```bash
git init
```

### After

```
MyProject/
│
├── .git/
```


💡 **Remember**

You only run `git init` **once** per project.


## 2️⃣ Check Repository Status

- Command

```bash
git status
```
- What does it do?

Shows:

- Modified files
- New files
- Deleted files
- Files waiting to be committed

## Example

```
modified: app.py

untracked: README.md
```

💡 **Why use it?**

Always check the status before committing.



## 3️⃣ Add Files to Staging Area

Git saves changes in **two steps**:

```
Working Directory
       ↓
Staging Area
       ↓
Commit
```


- Add One File

```bash
git add app.py
```


- Add Multiple Files

```bash
git add file1.py file2.py
```

- Add Everything

```bash
git add .
```

- What does it do?

Moves selected files into the **Staging Area**.

Think of it like:

> "These files are ready to be saved."

## 4️⃣ Save Changes (Commit)

- Command

```bash
git commit -m "Added login page"
```


- What does it do?

Creates a permanent snapshot of your project.

- Example Timeline

```
Version 1
Initial Project

↓

Version 2
Added Login

↓

Version 3
Fixed Bug

↓

Version 4
Added Dashboard
```

Each version is a **Commit**.


💡 Write meaningful commit messages.

✅ Good

```bash
git commit -m "Fixed login validation bug"
```

❌ Bad

```bash
git commit -m "update"
```

| Situation | Prefix |
| --- | --- |
| Added something new | `feat:` |
| Fixed a bug | `fix:` |
| Improved code structure only | `refactor:` |
| Updated README/docs | `docs:` |
| Added tests | `test:` |
| Dependency/config changes | `chore:` |
## 5️⃣ View Commit History

- Command

```bash
git log --oneline
```


## Example Output

```
a1b2c3 Added login

d4e5f6 Initial project
```
- What does it do?

Shows every commit you've made.

## 6️⃣ Connect Local Repository to GitHub

- Command

```bash
git remote add origin https://github.com/username/repository.git
```


- What does it do?



Connects your local Git repository to a GitHub repository.


💡 Run only once.


## 7️⃣ Upload Code to GitHub

- First Push

```bash
git push -u origin main
```



- Future Pushes

```bash
git push
```


- What does it do?

Uploads your commits to GitHub.


## 8️⃣ Download Latest Changes

- Command

```bash
git pull
```


- What does it do?

Downloads the newest commits from GitHub.


💡 Always pull before starting work.


## 9️⃣ Clone a Repository

- Command

```bash
git clone https://github.com/user/project.git
```

- What does it do?

Downloads an existing GitHub repository.

Example

```
GitHub
      ↓
Your Computer
```

## 🔟 Create a Branch
- Command

```bash
git branch feature-login
```

- What does it do?

Creates a new branch.

Example

```
main

feature-login
```


- Why Companies Use Branches

```
main
Production Code

feature-login
Your Work

feature-payment
Another Feature
```

## 1️⃣1️⃣ Switch Branch

- Old Command

```bash
git checkout feature-login
```

- Modern Command

```bash
git switch feature-login
```


- What does it do?

Switches to another branch.



## 1️⃣2️⃣ Create and Switch Branch

- Command

```bash
git checkout -b feature-payment
```


Equivalent to:

```bash
git branch feature-payment

git switch feature-payment
```


This command does both at once.


## 1️⃣3️⃣ Merge Branches

- Command

```bash
git merge feature-payment
```


- What does it do?

Combines another branch into the current branch.

Example

```
feature-payment

↓

Merge

↓

main
```

## 1️⃣4️⃣ List All Branches

- Command

```bash
git branch
```

Example

```
* main

feature-login

feature-payment
```

The `*` shows your current branch.

## 1️⃣5️⃣ Delete a Branch

- Command

```bash
git branch -d feature-payment
```

- What does it do?

Deletes a branch after it has been merged.



## 1️⃣6️⃣ Restore Changes

- Command

```bash
git restore app.py
```


- What does it do?

Removes all uncommitted changes from a file.

⚠️ This cannot be undone.


## 1️⃣7️⃣ Remove Files from Staging

- Command

```bash
git restore --staged app.py
```


- What does it do?

Removes a file from the staging area.

Your changes remain in the file.


## 1️⃣8️⃣ View Changes
- Command

```bash
git diff
```


- What does it do?

Shows exactly what has changed.

Example

```diff
-print("Hello")

+print("Hello World")
```

---

# ⭐ Top 10 Commands You Must Master

| Priority | Command | Purpose |
|----------|----------|----------|
| ⭐⭐⭐⭐⭐ | `git init` | Initialize repository |
| ⭐⭐⭐⭐⭐ | `git status` | Check repository status |
| ⭐⭐⭐⭐⭐ | `git add .` | Stage files |
| ⭐⭐⭐⭐⭐ | `git commit -m "message"` | Save snapshot |
| ⭐⭐⭐⭐ | `git log --oneline` | View history |
| ⭐⭐⭐⭐ | `git clone` | Download repository |
| ⭐⭐⭐⭐⭐ | `git pull` | Get latest changes |
| ⭐⭐⭐⭐⭐ | `git push` | Upload changes |
| ⭐⭐⭐⭐⭐ | `git checkout -b branch-name` | Create & switch branch |
| ⭐⭐⭐⭐⭐ | `git merge branch-name` | Merge branches |

---

# 🏢 Real Industry Workflow

```
Developer

↓

git pull

↓

git checkout -b feature-auth

↓

Write Code

↓

git status

↓

git add .

↓

git commit -m "Added JWT authentication"

↓

git push -u origin feature-auth

↓

Create Pull Request (GitHub)

↓

Code Review

↓

Approval

↓

Merge into main

↓

Deployment
```

---

# 🎯 Git Workflow Summary

```
Create Project
      │
      ▼
git init
      │
      ▼
Write Code
      │
      ▼
git status
      │
      ▼
git add .
      │
      ▼
git commit -m "message"
      │
      ▼
git push
      │
      ▼
GitHub
```

---

# 💡 Pro Tips

- ✅ Commit frequently.
- ✅ Write meaningful commit messages.
- ✅ Pull before starting work.
- ✅ Never work directly on `main` in team projects.
- ✅ Use feature branches for every new task.
- ✅ Push your work regularly.
- ✅ Always review `git status` before committing.

---

# 📌 Conclusion

If you master these 10 commands and understand the workflow, you'll know around **80% of the Git commands used in real software development**. The remaining 20% consists of advanced topics like:

- `git rebase`
- `git stash`
- `git cherry-pick`
- `git revert`
- `git reset`
- Merge conflicts
- Pull Requests
- GitHub Actions
- CI/CD
- Advanced branching strategies

These can be learned after you're comfortable with the fundamentals.

