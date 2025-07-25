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

---

#### 📁 Repository

```
git init                     # Create new local repo
git clone <url>             # Clone existing repo
```

---

#### 📄 Stage & Commit

```
git status                  # View changes
git add <file>              # Stage file
git add .                   # Stage all files
git commit -m "Message"     # Commit changes
```

---

#### 🌿 Branching

```
git branch                  # List branches
git branch <name>           # Create new branch
git checkout <name>         # Switch branch
git checkout -b <name>      # Create and switch
git merge <name>            # Merge into current
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

#### 📦 History & Logs

```
git log                      # Show commit log
git log --oneline --graph    # Compact log
```

---

#### ❌ Undo

```
git restore <file>           # Unstage/undo changes
git reset --soft HEAD~1      # Undo last commit (keep files)
git reset --hard HEAD~1      # Undo commit + changes
```

---

#### 🙈 .gitignore Example

```
*.log
*.class
/build/
/.idea/
/node_modules/
```

---
