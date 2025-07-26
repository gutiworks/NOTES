### 🧾 **GIT TERMINAL CHEAT SHEET**

#### 🔧 Setup

```
git config --global --list
git config --local --list // on the repo path C://Documents/Repo

git config --global user.name "Your Name"
git config --global user.email "your@email.com"

git config --local user.name "Your Name"
git config --local user.email "your@email.com"
```
```
//Show hidden files to find .git
ls -a 
dir /a
rm -rf // Force remove of .git if want to delete a repo
```

---

#### 📁 Repository

```
git init                     # Create new local repo
git clone <url>              # Clone existing repo
```

---

#### 🌿 Branching

```
git branch                  # List branches
git branch <name>           # Create new branch
git checkout <name>         # Switch branch
git merge <name>            # Merge into current
git branch -d <name>        # Delete branch
```

---

#### 📄 Stage & Commit

```
git status                  # View changes
git add <file>              # Stage file
git add .                   # Stage all files
git diff                    # See unstaged changes
git log                     # Show commit log
git commit -m "Message"     # Commit changes
```

---

#### 🗃️ Stash (temp storage)

```
git stash                 # Save uncommitted changes
git stash -m              # Save uncommitted changes with message
git stash pop             # Apply and remove last stash
git stash list            # List stashed changes
git stash clear           # Clear list
```

---

#### 🌐 Remote

```
git remote add origin <url>   # Link remote
git remote -v                 # View remotes
git push -u origin main       # Push first time
git push                      # Push changes
git pull                      # Fetch & merge
```

---

#### ❌ Undo

```
git restore <file>           # Delete non staged files
git restore --staged <file>  # Unstage files
git clean -f                 # Delete non staged changes
```

---
