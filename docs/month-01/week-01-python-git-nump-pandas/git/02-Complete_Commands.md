# 🎓 The Complete Git Command Handbook
**Topic:** Definitive Command Reference  
**Version:** 1.0 (Academy Standard)

---
> **💡 Note on Modern Git:**  
> Newer versions of Git have split some `checkout` functions into `switch` (for branches) and `restore` (for files) to reduce confusion. We will show **both** so you can work on any team.

---

## 🟢 Level 1: Setup & Initialization
*Goal: Get Git ready on your machine.*

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `git config` | `git config --global user.name "Name"` | Sets your identity for all repos. |
| | `git config --global user.email "email"` | Sets your email for all repos. |
| | `git config --list` | Shows all current settings. |
| `git init` | `git init` | Turns current folder into a Git repo. |
| `git clone` | `git clone <url>` | Downloads a repo from GitHub to your computer. |

---

## 🟡 Level 2: Daily Workflow (The Core)
*Goal: Save and share your work.*

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `git status` | `git status` | **Use this constantly.** Shows changed files, staged files, and current branch. |
| `git add` | `git add filename.py` | Stages a specific file for commit. |
| | `git add .` | Stages **all** changed files (be careful!). |
| `git commit` | `git commit -m "message"` | Saves a snapshot with a message. |
| | `git commit -am "message"` | Skips `add` for tracked files (advanced shortcut). |
| `git push` | `git push` | Uploads commits to GitHub. |
| | `git push -u origin main` | Links local `main` to remote `main` (first time only). |
| `git pull` | `git pull` | Downloads changes from GitHub + merges them. |
| `git fetch` | `git fetch` | Downloads changes but **doesn't merge** (safe inspection). |

---

## 🟠 Level 3: Branching & Navigation
*Goal: Work on multiple features safely.*

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `git branch` | `git branch` | Lists all local branches. |
| | `git branch <name>` | Creates a new branch (doesn't switch). |
| | `git branch -d <name>` | Deletes a branch (safe check). |
| | `git branch -D <name>` | Forces delete (even if not merged). |
| `git checkout` | `git checkout <branch>` | **Classic:** Switches to a branch. |
| *(Classic)* | `git checkout -b <new>` | **Classic:** Creates + switches to new branch. |
| `git switch` | `git switch <branch>` | **Modern:** Switches to a branch (safer). |
| *(Modern)* | `git switch -c <new>` | **Modern:** Creates + switches to new branch. |
| `git merge` | `git merge <branch>` | Combines specified branch into current branch. |

> **⚠️ Checkout vs. Switch:**  
> Use `git switch` for branches. It prevents accidental file overwrites.  
> Use `git checkout` only if you are on an older Git version or following older tutorials.

---

## 🟣 Level 4: History & Inspection
*Goal: See what happened and who did it.*

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `git log` | `git log` | Shows full commit history (press `q` to quit). |
| | `git log --oneline` | **Essential:** Compact one-line per commit. |
| | `git log --graph --all` | Shows branch structure visually. |
| | `git log -n 5` | Shows only the last 5 commits. |
| `git diff` | `git diff` | Shows changes not yet staged. |
| | `git diff --staged` | Shows changes ready to be committed. |
| | `git diff main..feature` | Compares two branches. |
| `git show` | `git show <commit>` | Shows details of a specific commit. |
| `git blame` | `git blame <file>` | Shows who edited each line of a file. |

---

## 🔴 Level 5: Undoing & Fixing Mistakes
*Goal: Rescue yourself when things go wrong.*

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `git restore` | `git restore <file>` | **Modern:** Discards changes in working directory. |
| *(Modern)* | `git restore --staged <file>` | Unstages a file (keeps changes). |
| `git checkout` | `git checkout -- <file>` | **Classic:** Discards changes in working directory. |
| *(Classic)* | | (Use `git restore` instead if possible). |
| `git reset` | `git reset HEAD <file>` | Unstages a file (keeps changes). |
| | `git reset --hard <commit>` | **DANGER:** Deletes all changes after commit. |
| `git revert` | `git revert <commit>` | Creates a **new** commit that undoes a past commit (safe for shared branches). |
| `git clean` | `git clean -fd` | Deletes untracked files and folders. |
| `git stash` | `git stash` | Saves changes temporarily (like a pocket). |
| | `git stash pop` | Retrieves changes from stash. |
| | `git stash list` | Shows all saved stashes. |

---

## ⚫ Level 6: Advanced & Maintenance
*Goal: Professional history management.*

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `git rebase` | `git rebase main` | Replays current branch on top of `main` (linear history). |
| | `git rebase -i HEAD~3` | **Interactive:** Edit/squash last 3 commits. |
| `git reflog` | `git reflog` | **Safety Net:** History of ALL movements (even deleted commits). |
| `git cherry-pick`| `git cherry-pick <id>` | Applies a specific commit from another branch. |
| `git tag` | `git tag v1.0` | Marks a commit as a release version. |
| | `git push --tags` | Pushes versions to GitHub. |
| `git bisect` | `git bisect start` | Binary search to find which commit broke code. |

---

## 🌐 Level 7: Remote Management
*Goal: Manage connections to GitHub.*

| Command | Usage | Explanation |
| :--- | :--- | :--- |
| `git remote` | `git remote -v` | Shows connected GitHub URLs. |
| `git remote add`| `git remote add origin <url>` | Links local repo to GitHub. |
| `git remote remove`| `git remote remove origin` | Disconnects from GitHub. |

---

## 🛠️ Pro Setup: Aliases (Save Time)
*Type less, do more.*  
Run these commands once to create shortcuts.

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.last "log -1 HEAD"
git config --global alias.unstage "reset HEAD --"
```
**Now you can type:**  
`git st` instead of `git status`  
`git co main` instead of `git checkout main`

---

## 🏆 Academy Command Challenge
*Test your knowledge.*

1.  **Inspect:** Run `git log --oneline --graph --all`. Take a screenshot of your history.
2.  **Navigate:** Create a branch `test`, switch to it, then switch back to `main` using `git switch`.
3.  **Undo:** Make a change to a file, then use `git restore` to undo it.
4.  **Save:** Use `git stash` to save changes, then `git stash pop` to bring them back.
5.  **Identify:** Use `git blame` on your README file to see who wrote the first line.

---

## 💡 Final Cheat Sheet (Print This)

| I want to... | Command |
| :--- | :--- |
| **Start** | `git init` or `git clone <url>` |
| **See Changes** | `git status` & `git diff` |
| **Save Changes** | `git add .` & `git commit -m "msg"` |
| **Upload** | `git push` |
| **Download** | `git pull` |
| **New Feature** | `git switch -c feature-name` |
| **Finish Feature** | `git switch main` & `git merge feature-name` |
| **Undo File** | `git restore <file>` |
| **Undo Commit** | `git revert <commit>` |
| **See History** | `git log --oneline` |
| **Emergency** | `git reflog` |

---

> **"Mastering Git is not about memorizing every command. It's about knowing which command solves your current problem."**  
> Keep this handbook handy. You are now equipped for any scenario. 🚀