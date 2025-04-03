# git-notes
# Git Commands Cheat Sheet

## 1. Initialize a New Git Repository & Push to GitHub
```bash
# Create a new local repository
git init  

# Add a new file
echo "# My First Repo" > README.md  

# Stage the file
git add README.md  

# Commit the changes
git commit -m "Initial commit"  

# Connect to a GitHub repository
git remote add origin https://github.com/your-username/your-repo.git  

# Push changes to GitHub
git push -u origin main  
```

## 2. Clone an Existing Repository
```bash
# Clone a GitHub repository to your local machine
git clone https://github.com/your-username/your-repo.git  
```

## 3. Create a New Branch & Switch to It
```bash
# Create a new branch
git branch feature-branch  

# Switch to the new branch
git checkout feature-branch  

# OR (shortcut)
git checkout -b feature-branch  
```

## 4. Make Changes & Push to GitHub
```bash
# Add a new file
echo "print('Hello, Git!')" > hello.py  

# Stage the file
git add hello.py  

# Commit the changes
git commit -m "Added hello.py"  

# Push the branch to GitHub
git push origin feature-branch  
```

## 5. Merge Branches (Feature Branch → Main Branch)
```bash
# Switch to the main branch
git checkout main  

# Merge the feature branch
git merge feature-branch  

# Push the changes to GitHub
git push origin main  
```

## 6. Undo Last Commit (Before Pushing to GitHub)
```bash
# Undo the last commit (keep changes staged)
git reset --soft HEAD~1  

# Undo the last commit (remove changes)
git reset --hard HEAD~1  
```

## 7. Revert a Pushed Commit (Without Deleting History)
```bash
# Revert a specific commit
git revert <commit-hash>  

# Push the reverted commit
git push origin main  
```

## 8. Delete a Branch
```bash
# Delete a local branch
git branch -d feature-branch  

# Delete a remote branch
git push origin --delete feature-branch  
```

## 9. Stash Uncommitted Changes (Temporary Save)
```bash
# Save current changes without committing
git stash  

# List all stashed changes
git stash list  

# Apply the last stashed changes
git stash pop  
```

## 10. Check Git Logs & History
```bash
# View commit history
git log --oneline --graph --all  

# View the last 5 commits
git log -5  
```

## 11. Set Up a Git Ignore File (.gitignore)
```bash
# Create a .gitignore file
echo "node_modules/" > .gitignore  

# Add it to Git
git add .gitignore  

# Commit the changes
git commit -m "Added .gitignore"  
```

## 12. Fork a Repository & Sync with Upstream
```bash
# Add upstream (original repo)
git remote add upstream https://github.com/original-owner/original-repo.git  

# Fetch the latest changes from upstream
git fetch upstream  

# Merge changes into your local main branch
git merge upstream/main  

# Push changes to your GitHub fork
git push origin main  
```

