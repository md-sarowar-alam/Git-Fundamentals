# Git Fundamentals Guide for DevOps Engineers

> A comprehensive guide covering Git basics to advanced concepts for fresh DevOps engineers.

**Repository**: [md-sarowar-alam/Git-Fundamentals](https://github.com/md-sarowar-alam/Git-Fundamentals)  
**Clone URL (HTTPS)**: `https://github.com/md-sarowar-alam/Git-Fundamentals.git`  
**Clone URL (SSH)**: `git@github.com:md-sarowar-alam/Git-Fundamentals.git`

## Table of Contents
- [Introduction to Git](#introduction-to-git)
- [Installing Git](#installing-git)
- [Installing GitHub CLI (gh)](#installing-github-cli-gh)
- [Creating a Git Repository](#creating-a-git-repository)
  - [Creating from GUI](#creating-from-gui)
  - [Creating from Command Line](#creating-from-command-line)
- [Cloning Repositories](#cloning-repositories)
- [Git Authentication](#git-authentication)
  - [HTTPS Authentication](#https-authentication)
  - [SSH Authentication](#ssh-authentication)
- [Basic Git Operations](#basic-git-operations)
  - [Git Commit Workflow](#git-commit-workflow)
  - [Viewing History](#viewing-history)
- [Rolling Back Commits](#rolling-back-commits)
  - [Reset vs Revert](#reset-vs-revert)
  - [Rollback Scenarios](#rollback-scenarios)
  - [Recovery from Mistakes](#recovery-from-mistakes)
- [Git Branching](#git-branching)
  - [Creating Branches](#creating-branches)
  - [Switching Branches](#switching-branches)
  - [Merging Branches](#merging-branches)
  - [Branching Strategies](#branching-strategies)
- [Forking Workflow](#forking-workflow)
  - [What is Forking](#what-is-forking)
  - [Fork and Clone](#fork-and-clone)
  - [Contributing to Open Source](#contributing-to-open-source)
- [Remote Upstream Setup](#remote-upstream-setup)
  - [Understanding Remotes](#understanding-remotes)
  - [Syncing with Upstream](#syncing-with-upstream)
- [Pull Requests](#pull-requests)
  - [Creating Pull Requests](#creating-pull-requests)
  - [Review Process](#review-process)
  - [PR Best Practices](#pr-best-practices)
- [Deploying to Heroku](#deploying-to-heroku)
  - [Heroku Setup](#heroku-setup)
  - [Deployment Workflow](#deployment-workflow)
  - [CI/CD Integration](#cicd-integration)
- [Advanced Topics](#advanced-topics)
  - [Repository Roles](#repository-roles)
  - [Branch Protection Rules](#branch-protection-rules)
  - [Restricting Branch Deletion](#restricting-branch-deletion)
  - [Protecting History](#protecting-history)

---

## Getting Started with This Guide

This comprehensive guide is available on GitHub. You can clone it to your local machine and use it offline:

```bash
# Clone via HTTPS
git clone https://github.com/md-sarowar-alam/Git-Fundamentals.git

# Or clone via SSH
git clone git@github.com:md-sarowar-alam/Git-Fundamentals.git

# Navigate into the directory
cd Git-Fundamentals

# Open README.md in your favorite editor
code README.md  # VS Code
# or
cat README.md   # View in terminal
```

**Star this repository** ⭐ on [GitHub](https://github.com/md-sarowar-alam/Git-Fundamentals) if you find it helpful!

---

## Introduction to Git

**Git** is a distributed version control system that tracks changes in your code. It allows multiple developers to work on the same project simultaneously without conflicts.

### Key Concepts:
- **Repository (Repo)**: A directory that contains your project files and Git history
- **Commit**: A snapshot of your project at a specific point in time
- **Branch**: A parallel version of your repository
- **Remote**: A version of your repository hosted on a server (GitHub, GitLab, etc.)

---

## Installing Git

### Windows:
```bash
# Download from: https://git-scm.com/download/win
# Or use Chocolatey
choco install git

# Verify installation
git --version
```

### Linux (Ubuntu/Debian):
```bash
sudo apt update
sudo apt install git

# Verify installation
git --version
```

### macOS:
```bash
# Using Homebrew
brew install git

# Verify installation
git --version
```

### Initial Configuration:
```bash
# Set your name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Check your configuration
git config --list

# Set default branch name
git config --global init.defaultBranch main
```

---

## Installing GitHub CLI (gh)

GitHub CLI (`gh`) is a powerful command-line tool that brings GitHub functionality to your terminal. It's required for commands like `gh auth login`, `gh repo fork`, `gh pr create`, and more.

### Windows:

**Option 1: Using WinGet (Windows Package Manager)**
```bash
# Install GitHub CLI
winget install --id GitHub.cli

# Verify installation
gh --version
```

**Option 2: Using Chocolatey**
```bash
# Install GitHub CLI
choco install gh

# Verify installation
gh --version
```

**Option 3: Using Scoop**
```bash
# Install GitHub CLI
scoop install gh

# Verify installation
gh --version
```

**Option 4: Manual Installation**
- Download the `.msi` installer from: https://cli.github.com/
- Run the installer
- Restart your terminal
- Verify: `gh --version`

### Linux (Ubuntu/Debian):

```bash
# Add GitHub CLI repository
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
&& sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

# Install GitHub CLI
sudo apt update
sudo apt install gh -y

# Verify installation
gh --version
```

### Linux (Fedora/RHEL/CentOS):

```bash
# Add GitHub CLI repository
sudo dnf install 'dnf-command(config-manager)'
sudo dnf config-manager --add-repo https://cli.github.com/packages/rpm/gh-cli.repo

# Install GitHub CLI
sudo dnf install gh

# Verify installation
gh --version
```

### macOS:

**Option 1: Using Homebrew (Recommended)**
```bash
# Install GitHub CLI
brew install gh

# Verify installation
gh --version
```

**Option 2: Using MacPorts**
```bash
# Install GitHub CLI
sudo port install gh

# Verify installation
gh --version
```

### Authenticating with GitHub CLI:

After installation, authenticate with your GitHub account:

```bash
# Start authentication process
gh auth login

# Follow the prompts:
# 1. Select "GitHub.com" (or GitHub Enterprise Server)
# 2. Select "HTTPS" or "SSH" protocol
# 3. Authenticate with web browser (recommended) or paste authentication token
# 4. Choose your preferred Git protocol

# Verify authentication
gh auth status

# View authenticated user
gh api user | grep login
```

### Common GitHub CLI Commands:

```bash
# Repository operations
gh repo create my-new-repo --public
gh repo view owner/repo
gh repo fork owner/repo --clone

# Pull Request operations
gh pr create --title "My PR" --body "Description"
gh pr list
gh pr view 123
gh pr checkout 123

# Issue operations
gh issue create --title "Bug report"
gh issue list
gh issue view 456

# Gist operations
gh gist create file.txt
gh gist list

# Check CLI version and updates
gh version
gh upgrade
```

### GitHub CLI Configuration:

```bash
# Set default editor
gh config set editor "code --wait"  # VS Code
gh config set editor "vim"          # Vim

# Set default Git protocol
gh config set git_protocol ssh
gh config set git_protocol https

# View all config
gh config list

# Set preferred browser
gh config set browser firefox
```

### Why Use GitHub CLI?

1. **Faster Workflows**: Perform GitHub actions without leaving the terminal
2. **Automation**: Script GitHub operations for CI/CD pipelines
3. **Reduced Context Switching**: Stay focused in your development environment
4. **Access to GitHub API**: Easily interact with GitHub's REST and GraphQL APIs
5. **Interactive Prompts**: Guided commands for complex operations

**Official Documentation**: https://cli.github.com/manual/

---

## Creating a Git Repository

### Creating from GUI

#### GitHub:
1. **Log in to GitHub** (https://github.com)
2. **Click the "+" icon** in the top-right corner
3. **Select "New repository"**
4. **Fill in the details:**
   - Repository name
   - Description (optional)
   - Public or Private
   - Initialize with README (optional)
   - Add .gitignore (optional)
   - Choose a license (optional)
5. **Click "Create repository"**

#### GitLab:
1. **Log in to GitLab** (https://gitlab.com)
2. **Click "New project"**
3. **Choose "Create blank project"**
4. **Fill in the details:**
   - Project name
   - Project URL
   - Visibility level (Private, Internal, Public)
   - Initialize with README (optional)
5. **Click "Create project"**

#### Bitbucket:
1. **Log in to Bitbucket** (https://bitbucket.org)
2. **Click "Create" > "Repository"**
3. **Fill in the details:**
   - Repository name
   - Access level (Private or Public)
   - Include README (optional)
4. **Click "Create repository"**

### Creating from Command Line

#### Initialize a New Repository:
```bash
# Create a new directory
mkdir my-project
cd my-project

# Initialize Git repository
git init

# Verify initialization
ls -la  # You should see a .git directory
```

#### Create Your First Commit:
```bash
# Create a README file
echo "# My Project" > README.md

# Check status
git status

# Add file to staging area
git add README.md

# Commit the file
git commit -m "Initial commit: Add README"

# View commit history
git log
```

#### Connect to Remote Repository:
```bash
# Add remote origin (replace with your repository URL)
git remote add origin https://github.com/username/repository.git

# Verify remote
git remote -v

# Push to remote
git push -u origin main
```

---

## Cloning Repositories

Cloning creates a local copy of a remote repository on your machine.

### Public Repository:

```bash
# Clone via HTTPS
git clone https://github.com/username/public-repo.git

# Clone via SSH
git clone git@github.com:username/public-repo.git

# Example: Clone this Git Fundamentals guide
git clone https://github.com/md-sarowar-alam/Git-Fundamentals.git
# Or with SSH
git clone git@github.com:md-sarowar-alam/Git-Fundamentals.git

# Clone to a specific directory
git clone https://github.com/username/public-repo.git my-folder

# Clone a specific branch
git clone -b branch-name https://github.com/username/public-repo.git

# Shallow clone (only recent history)
git clone --depth 1 https://github.com/username/public-repo.git
```

### Private Repository:

```bash
# Clone via HTTPS (will prompt for credentials)
git clone https://github.com/username/private-repo.git

# Clone via SSH (requires SSH key setup)
git clone git@github.com:username/private-repo.git

# Clone with Personal Access Token (GitHub)
git clone https://username:TOKEN@github.com/username/private-repo.git
```

### After Cloning:
```bash
# Navigate into the cloned repository
cd repository-name

# Check remote configuration
git remote -v

# View branches
git branch -a
```

---

## Git Authentication

### HTTPS Authentication

#### Using Personal Access Token (PAT):

**GitHub:**
1. Go to Settings > Developer settings > Personal access tokens > Tokens (classic)
2. Click "Generate new token"
3. Select scopes (repo, workflow, etc.)
4. Generate and save the token

**Clone with PAT:**
```bash
git clone https://USERNAME:TOKEN@github.com/username/repo.git

# Or configure credential helper
git config --global credential.helper store
# Then enter credentials once, they'll be saved
```

**Cache Credentials:**
```bash
# Cache for 1 hour (3600 seconds)
git config --global credential.helper cache

# Cache for 8 hours
git config --global credential.helper 'cache --timeout=28800'

# Store permanently (Windows)
git config --global credential.helper wincred

# Store permanently (Linux/Mac)
git config --global credential.helper store
```

### SSH Authentication

SSH (Secure Shell) provides a more secure way to authenticate without entering passwords repeatedly.

#### Step 1: Check for Existing SSH Keys
```bash
# List existing SSH keys
ls -la ~/.ssh

# Look for files like:
# id_rsa.pub
# id_ecdsa.pub
# id_ed25519.pub
```

#### Step 2: Generate New SSH Key
```bash
# Generate ED25519 key (recommended)
ssh-keygen -t ed25519 -C "your.email@example.com"

# Or RSA key (if ED25519 not supported)
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"

# Press Enter to accept default location
# Enter a passphrase (optional but recommended)
```

#### Step 3: Add SSH Key to SSH Agent
```bash
# Start SSH agent
eval "$(ssh-agent -s)"

# Add your SSH private key
ssh-add ~/.ssh/id_ed25519

# Or for RSA
ssh-add ~/.ssh/id_rsa
```

#### Step 4: Add SSH Key to GitHub/GitLab

**Copy your public key:**
```bash
# Linux/Mac
cat ~/.ssh/id_ed25519.pub

# Windows (PowerShell)
Get-Content ~/.ssh/id_ed25519.pub | clip

# Windows (Git Bash)
cat ~/.ssh/id_ed25519.pub | clip
```

**GitHub:**
1. Go to Settings > SSH and GPG keys
2. Click "New SSH key"
3. Paste your public key
4. Click "Add SSH key"

**GitLab:**
1. Go to Preferences > SSH Keys
2. Paste your public key
3. Click "Add key"

#### Step 5: Test SSH Connection
```bash
# Test GitHub connection
ssh -T git@github.com

# Test GitLab connection
ssh -T git@gitlab.com

# Expected output:
# Hi username! You've successfully authenticated...
```

#### Step 6: Use SSH URLs
```bash
# Clone with SSH
git clone git@github.com:username/repository.git

# Change existing repository from HTTPS to SSH
git remote set-url origin git@github.com:username/repository.git

# Verify
git remote -v
```

---

## Basic Git Operations

### Git Commit Workflow

Understanding the three states of Git:
1. **Working Directory**: Modified files
2. **Staging Area (Index)**: Files ready to be committed
3. **Repository**: Committed snapshots

```bash
# Check status of your repository
git status

# Create or modify files
echo "Hello World" > file.txt

# Add specific file to staging
git add file.txt

# Add all changes
git add .

# Add all files with specific extension
git add *.js

# Interactive staging
git add -p

# Remove file from staging (keep changes)
git restore --staged file.txt

# Commit staged changes
git commit -m "Add file.txt with hello world message"

# Commit with detailed message
git commit -m "Subject line" -m "Description line 1" -m "Description line 2"

# Add and commit in one step (tracked files only)
git commit -am "Update existing files"

# Amend last commit (change message or add forgotten files)
git add forgotten-file.txt
git commit --amend -m "New commit message"

# Show changes not staged
git diff

# Show changes staged for commit
git diff --staged

# Show changes in a specific file
git diff file.txt
```

### Commit Message Best Practices:
```bash
# Good commit message format:
# <type>(<scope>): <subject>
#
# <body>
#
# <footer>

# Examples:
git commit -m "feat: Add user authentication"
git commit -m "fix: Resolve login button crash"
git commit -m "docs: Update README with installation steps"
git commit -m "refactor: Simplify database query logic"
git commit -m "test: Add unit tests for user service"
```

### Viewing History

```bash
# View commit history
git log

# Compact one-line format
git log --oneline

# Show last N commits
git log -n 5

# Show commits with file changes
git log --stat

# Show commits with full diff
git log -p

# Graph view of branches
git log --graph --oneline --all

# Filter by author
git log --author="John Doe"

# Filter by date
git log --since="2 weeks ago"
git log --after="2025-01-01"
git log --before="2025-12-31"

# Filter by commit message
git log --grep="bug fix"

# Show commits for specific file
git log -- file.txt

# Show who changed what in a file
git blame file.txt

# Show specific commit details
git show commit-hash
```

### Undoing Changes

```bash
# Discard changes in working directory
git restore file.txt

# Unstage file (keep changes)
git restore --staged file.txt

# Discard all local changes
git restore .

# Revert a commit (creates new commit)
git revert commit-hash

# Reset to previous commit (be careful!)
# Soft: keep changes staged
git reset --soft HEAD~1

# Mixed: keep changes unstaged (default)
git reset HEAD~1

# Hard: discard all changes (dangerous!)
git reset --hard HEAD~1

# Reset to specific commit
git reset --hard commit-hash
```

---

## Rolling Back Commits

Rolling back commits is a critical skill for DevOps engineers. Understanding different rollback methods and their impacts helps you recover from mistakes safely.

### Understanding the Scenario

Let's say you have this commit history:
```bash
git log --oneline
# d4f6e2a (HEAD -> main) Commit 4: Latest changes
# c3e5d1b Commit 3: Add feature X
# b2d4c0a Commit 2: Update configuration
# a1c3b9f Commit 1: Initial setup
```

### Method 1: Reset (Rewriting History)

#### Reset to Immediate Previous Commit

```bash
# Soft Reset: Go back 1 commit, keep changes staged
git reset --soft HEAD~1
# Impact: Commit 4 removed, files still staged
# Use when: You want to re-commit with different message/files

# Mixed Reset (default): Go back 1 commit, keep changes unstaged
git reset HEAD~1
# or
git reset --mixed HEAD~1
# Impact: Commit 4 removed, files in working directory
# Use when: You want to modify files before recommitting

# Hard Reset: Go back 1 commit, discard all changes
git reset --hard HEAD~1
# Impact: Commit 4 completely removed, ALL CHANGES LOST
# Use when: You want to completely discard the commit
```

#### Reset to Specific Commit

```bash
# View commit history
git log --oneline

# Reset to Commit 2 (b2d4c0a)
git reset --soft b2d4c0a    # Keep changes from commits 3 & 4 staged
git reset --mixed b2d4c0a   # Keep changes from commits 3 & 4 unstaged
git reset --hard b2d4c0a    # Discard commits 3 & 4 completely

# Go back 2 commits
git reset --soft HEAD~2     # Back to Commit 2
git reset --hard HEAD~2     # Back to Commit 2, discard all

# Go back 3 commits
git reset --hard HEAD~3     # Back to Commit 1
```

#### Impact of Reset

```bash
# Local Repository Only:
- ✅ Changes local commit history
- ✅ Safe if not pushed to remote
- ❌ Dangerous if already pushed and others pulled

# After Reset, Force Push Required (DANGER!):
git push --force origin main
# ⚠️ WARNING: Rewrites remote history
# ⚠️ Others will have conflicts when they pull
# ⚠️ NEVER do this on shared branches
```

### Method 2: Revert (Safe History Preservation)

```bash
# Revert the last commit (creates new commit)
git revert HEAD
# Creates "Revert 'Commit 4: Latest changes'"
# Impact: History preserved, safe for shared branches

# Revert specific commit
git revert c3e5d1b
# Undoes changes from Commit 3 only
# Impact: New commit created, history intact

# Revert multiple commits
git revert HEAD~2..HEAD
# Reverts last 2 commits (creates 2 new commits)

# Revert without committing (review first)
git revert -n HEAD
git status  # Review changes
git commit -m "Revert: Rollback changes"
```

#### Impact of Revert

```bash
# Safe for All Scenarios:
- ✅ Preserves complete history
- ✅ Safe for shared branches
- ✅ Can be pushed without force
- ✅ Transparent to team members
- ✅ Can be reverted again if needed

# After Revert:
git push origin main  # Normal push, no force needed
```

### Method 3: Checkout (Temporary View)

```bash
# Temporarily view a specific commit
git checkout b2d4c0a
# Impact: HEAD detached, read-only view
# Use when: Inspecting old code without changing history

# View and create branch from old commit
git checkout -b recovery-branch b2d4c0a
# Impact: New branch from Commit 2
# Use when: Want to start fresh from old commit

# Return to main branch
git checkout main
```

### Method 4: Cherry-Pick (Selective Rollback)

```bash
# If you want to keep some commits but not others:

# Current: 1 -> 2 -> 3 -> 4
# Want: 1 -> 2 -> 4 (skip 3)

git reset --hard HEAD~2    # Go back to commit 2
git cherry-pick d4f6e2a    # Apply commit 4 only
# Result: 1 -> 2 -> 4 (commit 3 excluded)
```

### Complete Rollback Scenarios

#### Scenario 1: Rollback Last Commit (Not Pushed)

```bash
# You made a bad commit, want to fix it
git log --oneline
# d4f6e2a (HEAD -> main) Bad commit

# Option A: Keep changes, recommit
git reset --soft HEAD~1
# Edit files
git add .
git commit -m "Fixed commit"

# Option B: Discard completely
git reset --hard HEAD~1
```

#### Scenario 2: Rollback Last Commit (Already Pushed)

```bash
# Bad commit is on remote, others may have pulled

# SAFE METHOD: Use revert
git revert HEAD
git push origin main

# DANGEROUS METHOD: Force push (coordinate with team!)
git reset --hard HEAD~1
git push --force origin main
# ⚠️ Notify team immediately!
```

#### Scenario 3: Rollback Multiple Commits

```bash
# Want to go back from Commit 4 to Commit 1
git log --oneline
# d4f6e2a Commit 4
# c3e5d1b Commit 3
# b2d4c0a Commit 2
# a1c3b9f Commit 1

# Method 1: Reset (local only)
git reset --hard a1c3b9f

# Method 2: Revert (safe for remote)
git revert --no-commit HEAD~3..HEAD
git commit -m "Revert commits 2, 3, and 4"

# Method 3: New branch from old commit
git checkout -b recovery a1c3b9f
git branch -D main
git branch -m recovery main
git push --force origin main
```

#### Scenario 4: Rollback Specific File Only

```bash
# Only rollback changes to one file

# From immediate previous commit
git checkout HEAD~1 -- config.js
git commit -m "Rollback config.js to previous version"

# From specific commit
git checkout b2d4c0a -- config.js
git commit -m "Rollback config.js to Commit 2"
```

### Recovering from Mistakes

#### If You Reset Too Far Back

```bash
# View reflog (Git's safety net)
git reflog
# Shows:
# d4f6e2a HEAD@{0}: reset: moving to HEAD~1
# e5g7f3c HEAD@{1}: commit: Commit 4
# c3e5d1b HEAD@{2}: commit: Commit 3

# Recover the "lost" commit
git reset --hard HEAD@{1}
# or
git reset --hard e5g7f3c
```

#### If You Force Pushed and Broke Remote

```bash
# Team members should:
git fetch origin
git reset --hard origin/main

# Or to save their work:
git fetch origin
git rebase origin/main
```

### Best Practices for Rollback

```bash
# 1. Always check what you're rolling back
git log --oneline -5
git diff HEAD~1

# 2. Create backup branch before risky operations
git branch backup-before-reset

# 3. Use revert for shared branches
git revert HEAD  # Safe for team

# 4. Use reset only for local commits
git reset --hard HEAD~1  # Only if not pushed

# 5. Communicate with team before force push
# Send message: "Force pushing to main, please don't pull for 5 min"

# 6. Verify after rollback
git log --oneline
git status

# 7. Test after rollback
npm test  # or your test command
```

### Quick Reference: When to Use What

| Situation | Command | Impact | Safe for Remote? |
|-----------|---------|--------|------------------|
| Undo last commit, keep changes | `git reset --soft HEAD~1` | Changes staged | ❌ No |
| Undo last commit, discard changes | `git reset --hard HEAD~1` | Changes lost | ❌ No |
| Undo last commit safely | `git revert HEAD` | New commit | ✅ Yes |
| View old commit temporarily | `git checkout <commit>` | Detached HEAD | ✅ Yes |
| Undo specific commit | `git revert <commit>` | New commit | ✅ Yes |
| Recover lost commit | `git reflog` + `git reset` | Restore commit | Depends |

### Common Rollback Commands Summary

```bash
# Rollback last commit (local only)
git reset --hard HEAD~1

# Rollback last commit (safe for remote)
git revert HEAD

# Rollback to specific commit (local)
git reset --hard <commit-hash>

# Rollback to specific commit (safe for remote)
git revert <commit-hash>

# Rollback last 3 commits (local)
git reset --hard HEAD~3

# Rollback last 3 commits (safe for remote)
git revert --no-commit HEAD~3..HEAD
git commit -m "Revert multiple commits"

# Rollback one file only
git checkout <commit-hash> -- filename.txt

# View rollback history
git reflog

# Recover after mistake
git reset --hard <commit-from-reflog>
```

---

## Git Branching

Branches allow you to work on different features or fixes independently without affecting the main codebase.

### Creating Branches

```bash
# List all branches
git branch

# List all branches including remote
git branch -a

# Create a new branch
git branch feature-login

# Create and switch to new branch
git checkout -b feature-login

# Or using newer syntax
git switch -c feature-login

# Create branch from specific commit
git branch branch-name commit-hash

# Create branch from another branch
git branch new-branch existing-branch
```

### Switching Branches

```bash
# Switch to existing branch (old method)
git checkout main

# Switch to existing branch (new method)
git switch main

# Switch to previous branch
git switch -

# Create and switch to new branch
git switch -c feature-name
```

### Merging Branches

```bash
# Switch to target branch (usually main)
git switch main

# Merge feature branch into current branch
git merge feature-login

# Merge with commit message
git merge feature-login -m "Merge feature-login into main"

# Abort merge if conflicts
git merge --abort

# Continue merge after resolving conflicts
git add resolved-file.txt
git commit
```

### Merge Types:

#### Fast-Forward Merge:
```bash
# When target branch hasn't diverged
git merge feature-branch
# No merge commit created, just moves pointer forward
```

#### Three-Way Merge:
```bash
# When both branches have new commits
git merge feature-branch
# Creates a merge commit
```

#### Squash Merge:
```bash
# Combine all commits into one
git merge --squash feature-branch
git commit -m "Add complete feature"
```

### Handling Merge Conflicts

```bash
# When merge conflict occurs
git merge feature-branch
# CONFLICT (content): Merge conflict in file.txt

# Check conflicted files
git status

# Edit conflicted files
# Look for conflict markers:
# <<<<<<< HEAD
# Your changes
# =======
# Their changes
# >>>>>>> feature-branch

# After resolving conflicts
git add file.txt
git commit -m "Resolve merge conflicts"

# Or abort the merge
git merge --abort
```

### Deleting Branches

```bash
# Delete local branch (safe - only if merged)
git branch -d feature-login

# Force delete local branch (even if not merged)
git branch -D feature-login

# Delete remote branch
git push origin --delete feature-login

# Or shorter syntax
git push origin :feature-login

# Prune deleted remote branches
git fetch --prune
```

### Branch Management

```bash
# Rename current branch
git branch -m new-branch-name

# Rename another branch
git branch -m old-name new-name

# Copy a branch
git branch -c new-branch-copy

# Show branches with last commit
git branch -v

# Show merged branches
git branch --merged

# Show unmerged branches
git branch --no-merged

# Track remote branch
git branch --set-upstream-to=origin/main main
```

### Branching Strategies

#### 1. **Git Flow**
```bash
# Main branches
main        # Production-ready code
develop     # Integration branch

# Supporting branches
feature/*   # New features
release/*   # Release preparation
hotfix/*    # Emergency fixes

# Example workflow
git checkout develop
git checkout -b feature/user-auth
# ... work on feature ...
git checkout develop
git merge feature/user-auth
```

#### 2. **GitHub Flow** (Simpler)
```bash
# Single main branch
main        # Always deployable

# Feature branches
feature/*   # All changes

# Example workflow
git checkout main
git pull origin main
git checkout -b feature/add-search
# ... work on feature ...
git push origin feature/add-search
# Create Pull Request on GitHub
# After review and approval, merge to main
```

#### 3. **GitLab Flow**
```bash
# Environment branches
main           # Development
staging        # Staging environment
production     # Production environment

# Feature branches work similarly
git checkout main
git checkout -b feature/new-api
# ... work ...
git push origin feature/new-api
# Merge to main -> staging -> production
```

### Rebasing

```bash
# Rebase current branch onto main
git checkout feature-branch
git rebase main

# Interactive rebase (edit, squash, reorder commits)
git rebase -i HEAD~3

# Continue after resolving conflicts
git rebase --continue

# Abort rebase
git rebase --abort

# Rebase vs Merge:
# Rebase: Linear history, cleaner but rewrites history
# Merge: Preserves history, shows actual timeline
```

### Cherry-Picking

```bash
# Apply specific commit from another branch
git cherry-pick commit-hash

# Cherry-pick multiple commits
git cherry-pick commit1 commit2 commit3

# Cherry-pick without committing
git cherry-pick -n commit-hash
```

---

## Forking Workflow

Forking is a powerful Git workflow commonly used in open-source development and collaborative projects.

### What is Forking

**Fork**: A complete copy of a repository under your GitHub/GitLab account. Unlike cloning, forking creates a server-side copy that you own and can modify independently.

**Key Differences:**
```bash
# Clone: Local copy only
git clone https://github.com/owner/repo.git

# Fork: Creates your own copy on GitHub/GitLab
# Done via GUI, then clone your fork
git clone https://github.com/YOUR_USERNAME/repo.git
```

**When to Use Forking:**
- Contributing to open-source projects
- Experimenting with someone else's project
- Creating your own version of a project
- When you don't have write access to original repo

### Fork and Clone

#### Step 1: Fork Repository (GitHub)

**Via GUI:**
1. Navigate to the repository you want to fork
2. Click the **"Fork"** button in the top-right corner
3. Select your account as the destination
4. Wait for GitHub to create the fork
5. You now have a copy at `https://github.com/YOUR_USERNAME/repo`

**Via GitHub CLI:**
```bash
# Fork a repository
gh repo fork owner/repository

# Fork and clone in one command
gh repo fork owner/repository --clone

# Fork without cloning
gh repo fork owner/repository --clone=false
```

#### Step 2: Clone Your Fork

```bash
# Clone your forked repository
git clone https://github.com/YOUR_USERNAME/repository.git

# Or with SSH
git clone git@github.com:YOUR_USERNAME/repository.git

# Navigate into the directory
cd repository

# Verify remote
git remote -v
# Output:
# origin  https://github.com/YOUR_USERNAME/repository.git (fetch)
# origin  https://github.com/YOUR_USERNAME/repository.git (push)
```

#### Step 3: Add Upstream Remote

```bash
# Add original repository as upstream
git remote add upstream https://github.com/ORIGINAL_OWNER/repository.git

# Or with SSH
git remote add upstream git@github.com:ORIGINAL_OWNER/repository.git

# Verify remotes
git remote -v
# Output:
# origin    https://github.com/YOUR_USERNAME/repository.git (fetch)
# origin    https://github.com/YOUR_USERNAME/repository.git (push)
# upstream  https://github.com/ORIGINAL_OWNER/repository.git (fetch)
# upstream  https://github.com/ORIGINAL_OWNER/repository.git (push)

# Disable push to upstream (safety measure)
git remote set-url --push upstream no_push
```

### Contributing to Open Source

#### Complete Workflow:

```bash
# 1. Fork the repository (via GitHub GUI)

# 2. Clone your fork
git clone https://github.com/YOUR_USERNAME/project.git
cd project

# 3. Add upstream remote
git remote add upstream https://github.com/ORIGINAL_OWNER/project.git

# 4. Create a feature branch
git checkout -b fix-typo-in-readme

# 5. Make your changes
echo "Fixed typo" >> README.md

# 6. Commit your changes
git add README.md
git commit -m "docs: Fix typo in README installation section"

# 7. Push to your fork
git push origin fix-typo-in-readme

# 8. Create Pull Request (via GitHub GUI)
# Go to your fork on GitHub
# Click "Compare & pull request"
# Fill in PR details and submit
```

#### Keeping Your Fork Updated:

```bash
# Fetch latest changes from upstream
git fetch upstream

# Switch to main branch
git checkout main

# Merge upstream changes
git merge upstream/main

# Or rebase (for cleaner history)
git rebase upstream/main

# Push updates to your fork
git push origin main

# Update feature branch with latest main
git checkout fix-typo-in-readme
git rebase main
# Or merge
git merge main
```

#### Fork Syncing (GitHub Feature):

```bash
# Via GitHub GUI:
# Go to your fork
# Click "Sync fork" button
# Click "Update branch"

# Via GitHub CLI:
gh repo sync YOUR_USERNAME/repository

# Sync and pull to local
gh repo sync YOUR_USERNAME/repository --branch main
git pull origin main
```

### Forking Best Practices

```bash
# 1. Always sync before starting new work
git fetch upstream
git checkout main
git merge upstream/main

# 2. Create branches for each feature/fix
git checkout -b descriptive-branch-name

# 3. Keep commits atomic and well-described
git commit -m "type: Clear description of change"

# 4. Regularly update your feature branch
git fetch upstream
git rebase upstream/main

# 5. Test before pushing
# Run tests, build the project

# 6. Push to your fork, not upstream
git push origin branch-name
```

### Deleting Forks

```bash
# Delete via GitHub GUI:
# Repository > Settings > Danger Zone > Delete this repository

# Delete via GitHub CLI:
gh repo delete YOUR_USERNAME/repository

# Clean up local repository
cd ..
rm -rf repository
```

### Accepting Contributions from Forks

When someone forks your repository and wants to contribute changes back, here's how you (as the original repository owner) handle it:

#### Scenario: Someone Forked Your Repo and Made Changes

```bash
# The contributor's workflow (they do this):
# 1. Fork your repository: YOUR_USERNAME/your-repo
# 2. Clone their fork: git clone https://github.com/CONTRIBUTOR/your-repo.git
# 3. Create branch: git checkout -b fix-bug
# 4. Make changes and commit
# 5. Push to their fork: git push origin fix-bug
# 6. Create Pull Request to your repository
```

#### Method 1: Accept via Pull Request (Recommended)

**Step 1: Contributor Creates PR**
- They go to their fork on GitHub
- Click "Contribute" > "Open pull request"
- Select base repository: `YOUR_USERNAME/your-repo` (base: main)
- Select head repository: `CONTRIBUTOR/your-repo` (compare: fix-bug)
- Create pull request

**Step 2: You Review the PR**

```bash
# View PR list
gh pr list

# View specific PR details
gh pr view 42

# Check PR diff
gh pr diff 42

# Read comments and changes via GitHub GUI
# Go to Pull Requests tab
# Click on the PR
# Review Files changed tab
```

**Step 3: Test Changes Locally (Optional)**

```bash
# Checkout the PR locally for testing
gh pr checkout 42

# Or manually fetch the PR
git fetch origin pull/42/head:pr-42
git checkout pr-42

# Test the changes
npm test
npm run build
# Run your application and verify

# If changes look good, switch back
git checkout main
```

**Step 4: Request Changes or Approve**

```bash
# Request changes via GitHub GUI or CLI
gh pr review 42 --request-changes -b "Please fix the styling issues"

# Approve the PR
gh pr review 42 --approve -b "Looks good! Thanks for the contribution"

# Add comments
gh pr review 42 --comment -b "Great work overall"
```

**Step 5: Merge the PR**

```bash
# Merge via GitHub GUI:
# Click "Merge pull request"
# Choose merge strategy:
#   - Merge commit (preserves all commits)
#   - Squash and merge (combines into one commit)
#   - Rebase and merge (linear history)
# Click "Confirm merge"
# Optionally delete their branch

# Merge via CLI:
gh pr merge 42

# Squash merge (cleaner history)
gh pr merge 42 --squash --body "Thanks @contributor for fixing the bug"

# Rebase merge
gh pr merge 42 --rebase

# Merge commit
gh pr merge 42 --merge
```

**Step 6: Update Your Local Repository**

```bash
# Pull the merged changes
git checkout main
git pull origin main

# Verify the changes are included
git log --oneline -5
```

#### Method 2: Manual Merge (Without PR)

If contributor sent you changes via email or you want to merge manually:

```bash
# Add contributor's fork as a remote
git remote add contributor https://github.com/CONTRIBUTOR/your-repo.git

# Fetch their changes
git fetch contributor

# View their branches
git branch -r | grep contributor

# Checkout their branch
git checkout -b review-contributor-changes contributor/fix-bug

# Review and test the changes
git log
git diff main

# If satisfied, merge into your main branch
git checkout main
git merge review-contributor-changes

# Push to your repository
git push origin main

# Clean up
git branch -d review-contributor-changes
git remote remove contributor
```

#### Method 3: Cherry-Pick Specific Commits

If you only want specific commits from their fork:

```bash
# Add their fork as remote
git remote add contributor https://github.com/CONTRIBUTOR/your-repo.git

# Fetch their changes
git fetch contributor

# View their commits
git log contributor/fix-bug

# Cherry-pick specific commits
git checkout main
git cherry-pick abc123def456

# Or multiple commits
git cherry-pick abc123 def456 ghi789

# Push to your repository
git push origin main

# Remove remote
git remote remove contributor
```

#### Method 4: Using Git Request-Pull

For email-based contributions:

```bash
# Contributor generates pull request summary
git request-pull main https://github.com/CONTRIBUTOR/your-repo.git fix-bug

# They send you the output via email

# You fetch and merge as in Method 2
git remote add contributor https://github.com/CONTRIBUTOR/your-repo.git
git fetch contributor
git merge contributor/fix-bug
```

#### Best Practices for Accepting Contributions:

```bash
# 1. Always review code before merging
# - Check for security issues
# - Verify code quality
# - Test functionality

# 2. Require CI/CD checks to pass
# - Set up GitHub Actions
# - Require all tests to pass
# - Check code coverage

# 3. Use branch protection
# Settings > Branches > Branch protection rules
# - Require pull request reviews
# - Require status checks to pass
# - Require conversation resolution

# 4. Communicate clearly
# - Thank contributors
# - Provide constructive feedback
# - Be respectful and encouraging

# 5. Document contribution process
# Create CONTRIBUTING.md in your repo
```

#### Example CONTRIBUTING.md:

```markdown
# Contributing to [Project Name]

## How to Contribute

1. **Fork the repository**
   - Click the "Fork" button at the top right

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/repo-name.git
   cd repo-name
   ```

3. **Create a branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

4. **Make your changes**
   - Write clear, documented code
   - Follow our coding standards
   - Add tests for new features

5. **Commit your changes**
   ```bash
   git commit -m "feat: Add new feature"
   ```

6. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

7. **Create a Pull Request**
   - Go to the original repository
   - Click "New Pull Request"
   - Select your fork and branch
   - Describe your changes
   - Submit the PR

## Code Review Process

- Maintainers will review your PR
- Address any requested changes
- Once approved, your PR will be merged

## Code of Conduct

Please be respectful and constructive in all interactions.

## Questions?

Open an issue or contact the maintainers.
```

#### Handling Multiple Contributors:

```bash
# List all PRs from forks
gh pr list --state open

# Check who forked your repo
gh api repos/YOUR_USERNAME/your-repo/forks | jq '.[].owner.login'

# View network graph
# Go to Insights > Network on GitHub
# See all forks and their changes visually

# Batch review multiple PRs
for pr in 42 43 44; do
  gh pr checkout $pr
  npm test
  git checkout main
done

# Merge multiple approved PRs
gh pr merge 42 --squash
gh pr merge 43 --squash
gh pr merge 44 --squash
```

#### Sync Fork Feature (GitHub):

```bash
# If contributor's fork is behind, they can sync via:
# GitHub GUI: Click "Sync fork" > "Update branch"

# Or via CLI in their fork:
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

# Then they can rebase their feature branch:
git checkout fix-bug
git rebase main
git push origin fix-bug --force-with-lease
```

#### Protecting Your Repository:

```bash
# Set up branch protection to require reviews:
# Settings > Branches > Add rule
# - Branch name pattern: main
# - ✓ Require pull request reviews before merging
# - ✓ Require status checks to pass before merging
# - ✓ Require conversation resolution before merging
# - ✓ Include administrators

# This ensures:
# - No direct pushes to main
# - All changes come through reviewed PRs
# - Automated tests must pass
# - Discussions must be resolved
```

---

## Remote Upstream Setup

Managing multiple remotes is essential for collaborative development and fork workflows.

### Understanding Remotes

**Remote**: A reference to a repository hosted on a server (GitHub, GitLab, etc.)

```bash
# List all remotes
git remote

# List with URLs
git remote -v

# Show detailed info about a remote
git remote show origin

# Show all remote branches
git branch -r
```

### Common Remote Configurations

#### Configuration 1: Origin Only (Simple)
```bash
# When you clone your own repository
git clone https://github.com/YOUR_USERNAME/project.git

# Remotes:
origin -> your repository
```

#### Configuration 2: Origin + Upstream (Fork)
```bash
# When working with forks
origin   -> your fork
upstream -> original repository
```

#### Configuration 3: Multiple Remotes (Team)
```bash
origin   -> your fork
upstream -> main project repo
team     -> team repository
staging  -> staging environment
production -> production environment
```

### Adding Remotes

```bash
# Add upstream remote
git remote add upstream https://github.com/original-owner/repo.git

# Add team remote
git remote add team https://github.com/team/repo.git

# Add with SSH
git remote add upstream git@github.com:original-owner/repo.git

# Verify
git remote -v
```

### Modifying Remotes

```bash
# Change remote URL
git remote set-url origin https://github.com/new-url/repo.git

# Change from HTTPS to SSH
git remote set-url origin git@github.com:username/repo.git

# Rename remote
git remote rename origin old-origin

# Remove remote
git remote remove upstream
```

### Syncing with Upstream

#### Fetching from Upstream:

```bash
# Fetch all branches from upstream
git fetch upstream

# Fetch specific branch
git fetch upstream main

# Fetch from all remotes
git fetch --all

# View fetched branches
git branch -a
```

#### Merging Upstream Changes:

```bash
# Method 1: Merge (preserves history)
git checkout main
git fetch upstream
git merge upstream/main
git push origin main

# Method 2: Rebase (linear history)
git checkout main
git fetch upstream
git rebase upstream/main
git push origin main --force-with-lease

# Method 3: Pull (fetch + merge)
git checkout main
git pull upstream main
git push origin main
```

#### Syncing Feature Branch:

```bash
# Keep feature branch updated with upstream
git checkout feature-branch

# Fetch latest upstream
git fetch upstream

# Option 1: Rebase on upstream/main
git rebase upstream/main

# Option 2: Merge upstream/main
git merge upstream/main

# Resolve conflicts if any, then push
git push origin feature-branch --force-with-lease
```

### Working with Multiple Remotes

```bash
# Push to specific remote
git push origin main
git push upstream main

# Pull from specific remote
git pull origin main
git pull upstream main

# Set default upstream for branch
git branch --set-upstream-to=origin/main main

# Or during push
git push -u origin main

# Track remote branch
git checkout -b feature-branch origin/feature-branch

# Or shorter
git checkout --track origin/feature-branch
```

### Troubleshooting Remotes

```bash
# Remote connection issues
git remote -v  # Check URLs are correct

# Test connection
ping github.com
ssh -T git@github.com

# Update remote after repository rename
git remote set-url origin NEW_URL

# Fix diverged branches
git fetch origin
git reset --hard origin/main  # Caution: loses local changes

# Or merge
git fetch origin
git merge origin/main

# Check remote branch status
git remote show origin

# Prune deleted remote branches
git fetch --prune
git remote prune origin
```

### Advanced Remote Patterns

```bash
# Mirror push to multiple remotes
git remote set-url --add --push origin https://github.com/user/repo.git
git remote set-url --add --push origin https://gitlab.com/user/repo.git
# Now git push origin pushes to both

# Pull from upstream, push to fork
git pull upstream main
git push origin main

# Create branch from upstream
git checkout -b feature upstream/main

# Compare local with remote
git diff main origin/main

# Show commits not in remote
git log origin/main..main

# Show commits in remote not local
git log main..origin/main
```

---

## Pull Requests

Pull Requests (PRs) or Merge Requests (MRs in GitLab) are a way to propose changes to a repository.

### Creating Pull Requests

#### Preparation:

```bash
# 1. Ensure your branch is up to date
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/add-user-profile

# 3. Make changes and commit
git add .
git commit -m "feat: Add user profile page with avatar support"

# 4. Push to remote
git push origin feature/add-user-profile

# Or set upstream and push
git push -u origin feature/add-user-profile
```

#### Creating PR via GitHub GUI:

1. **Navigate to Repository** on GitHub
2. **Click "Pull requests"** tab
3. **Click "New pull request"**
4. **Select branches:**
   - Base: `main` (target branch)
   - Compare: `feature/add-user-profile` (your branch)
5. **Review changes** in the diff
6. **Click "Create pull request"**
7. **Fill in PR template:**
   ```markdown
   ## Description
   Added user profile page with avatar upload functionality
   
   ## Changes
   - Created profile component
   - Added avatar upload API
   - Implemented image compression
   
   ## Testing
   - Tested on Chrome, Firefox, Safari
   - Unit tests added and passing
   
   ## Screenshots
   [Attach screenshots]
   
   ## Related Issues
   Closes #123
   ```
8. **Assign reviewers**
9. **Add labels** (bug, enhancement, etc.)
10. **Click "Create pull request"**

#### Creating PR via GitHub CLI:

```bash
# Create PR from current branch
gh pr create

# Create with title and body
gh pr create --title "Add user profile" --body "Implements user profile page"

# Create as draft
gh pr create --draft

# Create and assign reviewers
gh pr create --reviewer @user1,@user2

# Create with label
gh pr create --label enhancement,frontend

# Create to specific branch
gh pr create --base develop

# View PR in browser
gh pr view --web
```

#### Creating MR via GitLab CLI:

```bash
# Push and create MR
git push -o merge_request.create origin feature-branch

# With title and description
git push -o merge_request.create \
       -o merge_request.title="Add feature" \
       -o merge_request.description="Detailed description" \
       origin feature-branch

# Set target branch
git push -o merge_request.create \
       -o merge_request.target=develop \
       origin feature-branch

# Remove source branch after merge
git push -o merge_request.create \
       -o merge_request.remove_source_branch \
       origin feature-branch
```

### Review Process

#### As PR Author:

```bash
# Check PR status
gh pr status

# View PR details
gh pr view 123

# View PR diff
gh pr diff 123

# View PR checks
gh pr checks 123

# Address review comments - make changes
git add .
git commit -m "fix: Address review comments"
git push origin feature-branch
# PR automatically updates

# Respond to comments on GitHub GUI
# Add inline comments, explanations

# Request re-review
gh pr review 123 --request @reviewer
```

#### As Reviewer:

```bash
# Checkout PR locally for testing
gh pr checkout 123

# Or manually
git fetch origin pull/123/head:pr-123
git checkout pr-123

# Test the changes
npm test
npm run build

# Leave review comments via GUI or CLI
gh pr review 123 --approve
gh pr review 123 --request-changes --body "Please fix the styling"
gh pr review 123 --comment --body "Looks good overall"

# Add inline comments on specific lines via GUI
```

#### Reviewer Checklist:

```markdown
### Code Review Checklist

#### Functionality
- [ ] Code does what it's supposed to do
- [ ] Edge cases handled
- [ ] No obvious bugs

#### Code Quality
- [ ] Code is readable and maintainable
- [ ] Follows project coding standards
- [ ] No code duplication
- [ ] Functions are small and focused
- [ ] Proper error handling

#### Testing
- [ ] Tests are included
- [ ] Tests are meaningful
- [ ] All tests pass
- [ ] Coverage is adequate

#### Documentation
- [ ] Code is properly commented
- [ ] README updated if needed
- [ ] API docs updated

#### Security
- [ ] No sensitive data exposed
- [ ] Input validation present
- [ ] No SQL injection risks
- [ ] Dependencies are secure

#### Performance
- [ ] No obvious performance issues
- [ ] Database queries optimized
- [ ] No memory leaks
```

### PR Best Practices

#### Writing Good PRs:

```bash
# 1. Keep PRs small and focused
# Bad: 50 files changed, multiple features
# Good: 5 files changed, one feature

# 2. Write descriptive titles
# Bad: "Fixed stuff"
# Good: "feat: Add user authentication with JWT"

# 3. Provide context in description
# Include:
# - What changed
# - Why it changed
# - How to test
# - Screenshots if UI changed

# 4. Link related issues
Closes #123
Resolves #456
Related to #789

# 5. Request specific reviewers
# Tag relevant team members

# 6. Respond to feedback promptly
# Don't let PRs go stale
```

#### PR Workflow Commands:

```bash
# Update PR with latest main
git checkout feature-branch
git fetch origin
git rebase origin/main
# Resolve conflicts if any
git push origin feature-branch --force-with-lease

# Squash commits before merging
git rebase -i HEAD~3
# Mark commits as 'squash' or 'fixup'
git push origin feature-branch --force-with-lease

# Add more commits to PR
git checkout feature-branch
git add .
git commit -m "Address review feedback"
git push origin feature-branch

# Sync with upstream (for forks)
git fetch upstream
git rebase upstream/main
git push origin feature-branch --force-with-lease
```

#### Merging Pull Requests:

```bash
# Merge via GitHub GUI:
# 1. Click "Merge pull request"
# 2. Choose merge strategy:
#    - Create merge commit (preserves history)
#    - Squash and merge (cleaner history)
#    - Rebase and merge (linear history)
# 3. Confirm merge
# 4. Delete branch (optional)

# Merge via CLI:
gh pr merge 123

# Squash merge
gh pr merge 123 --squash

# Rebase merge
gh pr merge 123 --rebase

# Auto-delete branch after merge
gh pr merge 123 --delete-branch

# Merge manually (if needed)
git checkout main
git merge --no-ff feature-branch
git push origin main
git branch -d feature-branch
git push origin --delete feature-branch
```

### Advanced PR Techniques

```bash
# Draft PRs (GitHub)
gh pr create --draft
# Convert to ready
gh pr ready 123

# Co-authored commits
git commit -m "feat: Add feature


Co-authored-by: Name <email@example.com>
Co-authored-by: Name2 <email2@example.com>"

# Link PRs to projects
# Done via GitHub GUI Projects tab

# Auto-close issues with PR
# In PR description:
# Closes #123
# Fixes #456
# Resolves #789

# Request review from teams
gh pr create --reviewer @org/team-name

# Add PR to merge queue (GitHub)
# Settings > Branches > Enable merge queue

# Approve own PR (if allowed)
gh pr review 123 --approve
```

---

## Deploying to Heroku

Heroku is a cloud platform that enables developers to deploy, manage, and scale applications easily using Git.

**Practice Repository**: [my-heroku-app](https://github.com/md-sarowar-alam/my-heroku-app.git) - A sample application for Heroku deployment practice (private repo).

> **Note**: The practice repository is private. You'll need to fork it or create your own application following the examples below.

**Repository Structure:**
```
my-heroku-app/
├── .gitignore          # Ignore node_modules, .env
├── Procfile            # Heroku process file: web: node server.js
├── server.js           # Main Express server with static file serving
├── package.json        # Dependencies (Express ^5.1.0) and scripts
├── package-lock.json   # Dependency lock file
└── my_photo.jpg        # Static asset (image displayed on page)
```

**Key Features of the Sample App:**
- ✅ Express.js server with static file serving
- ✅ Displays HTML page with embedded image
- ✅ Uses `process.env.PORT` for Heroku compatibility
- ✅ Properly configured Procfile for web dyno
- ✅ Complete `.gitignore` for Node.js projects

**Repository Structure:**
```
my-heroku-app/
├── .gitignore          # Ignore node_modules, .env
├── Procfile            # Heroku process file
├── server.js           # Main Express server
├── package.json        # Dependencies and scripts
├── package-lock.json   # Dependency lock file
└── my_photo.jpg        # Static asset (image)
```

### Heroku Setup

#### Prerequisites:

```bash
# Install Heroku CLI

# Windows (using installer)
# Download from: https://devcenter.heroku.com/articles/heroku-cli

# Windows (using Chocolatey)
choco install heroku-cli

# macOS
brew tap heroku/brew && brew install heroku

# Linux (Ubuntu/Debian)
curl https://cli-assets.heroku.com/install-ubuntu.sh | sh

# Verify installation
heroku --version
```

#### Login to Heroku:

```bash
# Login via browser
heroku login

# Login via CLI (for CI/CD)
heroku login -i
# Enter email and password

# Verify login
heroku auth:whoami

# Login with API key
export HEROKU_API_KEY=your-api-key
heroku auth:token
```

#### Create Heroku App:

```bash
# Create new app (auto-generated name)
heroku create

# Create with specific name
heroku create my-awesome-app

# Create in specific region
heroku create my-app --region eu

# List your apps
heroku apps

# View app info
heroku apps:info my-app

# Verify remote was added
git remote -v
# Should show:
# origin  https://github.com/md-sarowar-alam/my-heroku-app.git (fetch)
# origin  https://github.com/md-sarowar-alam/my-heroku-app.git (push)
# heroku  https://git.heroku.com/my-awesome-app.git (fetch)
# heroku  https://git.heroku.com/my-awesome-app.git (push)

# Note: You'll have both 'origin' (GitHub) and 'heroku' remotes
# - origin: Your source code repository on GitHub
# - heroku: Your Heroku deployment target
```

### Deployment Workflow

#### Basic Deployment:

```bash
# Make sure your code is committed
git status
git add .
git commit -m "Prepare for deployment"

# Deploy to Heroku
git push heroku main

# If your branch is not main
git push heroku branch-name:main

# View deployed app
heroku open

# View logs
heroku logs --tail
```

**Example: Deploy a Sample Application**

```bash
# Clone a sample Heroku app (private repo - requires authentication)
git clone https://github.com/md-sarowar-alam/my-heroku-app.git
cd my-heroku-app

# Login to Heroku
heroku login

# Create Heroku app
heroku create my-awesome-app

# Deploy to Heroku
git push heroku main

# Open the deployed app
heroku open
```

#### Project Configuration Files:

**For Node.js:**
```json
// package.json (from my-heroku-app repository)
{
  "name": "my-heroku-app",
  "version": "1.0.0",
  "description": "Simple Node.js app for Heroku",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "engines": {
    "node": "18.x"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^5.1.0"
  }
}
```

```javascript
// server.js (from my-heroku-app repository)
const express = require('express');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;

// Serve static files (including your photo)
app.use(express.static(__dirname));

app.get('/', (req, res) => {
  res.send(`
    <!DOCTYPE html>
    <html>
    <head>
        <title>Module - 02 | Batch 08</title>
    </head>
    <body>
        <h1>Hello! Your Node app is running on Heroku</h1>
        <img src="my_photo.jpg" alt="My Photo" style="max-width: 100%; height: auto;" />
    </body>
    </html>
  `);
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

**Procfile:**
```bash
# Procfile (no extension)
web: node server.js

# For Python
web: gunicorn app:app

# For Ruby
web: bundle exec rails server -p $PORT

# For PHP
web: vendor/bin/heroku-php-apache2 public/
```

**For Python:**
```txt
# requirements.txt
Flask==2.3.0
gunicorn==21.2.0
```

```python
# app.py
from flask import Flask
import os

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello from Heroku!'

if __name__ == '__main__':
    port = int(os.environ.get('PORT', 5000))
    app.run(host='0.0.0.0', port=port)
```

```
# runtime.txt
python-3.11.0
```

#### Environment Variables:

```bash
# Set environment variables
heroku config:set API_KEY=secret-key
heroku config:set DATABASE_URL=postgres://...

# View all config vars
heroku config

# Get specific config
heroku config:get API_KEY

# Unset config
heroku config:unset API_KEY

# Edit multiple configs
heroku config:edit

# Load from .env file (using plugin)
heroku plugins:install heroku-config
heroku config:push
```

#### Database Setup:

```bash
# Add PostgreSQL
heroku addons:create heroku-postgresql:mini

# View database info
heroku pg:info

# Access database URL
heroku config:get DATABASE_URL

# Run database migrations
heroku run python manage.py migrate

# Or for Node.js
heroku run npm run migrate

# Access database via CLI
heroku pg:psql

# Create database backup
heroku pg:backups:capture

# Download backup
heroku pg:backups:download
```

#### Scaling:

```bash
# Scale web dynos
heroku ps:scale web=2

# Scale worker dynos
heroku ps:scale worker=1

# View dyno information
heroku ps

# Restart all dynos
heroku restart

# Restart specific dyno
heroku restart web.1
```

### Advanced Heroku Deployment

#### Review Apps (for PRs):

```yaml
# app.json
{
  "name": "my-app",
  "description": "My awesome application",
  "repository": "https://github.com/user/repo",
  "env": {
    "API_KEY": {
      "description": "API key for external service",
      "required": true
    },
    "NODE_ENV": {
      "description": "Node environment",
      "value": "production"
    }
  },
  "formation": {
    "web": {
      "quantity": 1,
      "size": "basic"
    }
  },
  "addons": [
    "heroku-postgresql:mini",
    "heroku-redis:mini"
  ],
  "buildpacks": [
    {
      "url": "heroku/nodejs"
    }
  ]
}
```

**Enable Review Apps:**
1. Go to Pipeline in Heroku Dashboard
2. Enable Review Apps
3. Configure settings
4. Review apps auto-deploy for each PR

#### Pipeline Setup:

```bash
# Create pipeline
heroku pipelines:create my-pipeline

# Add app to pipeline
heroku pipelines:add my-pipeline --app my-staging-app --stage staging
heroku pipelines:add my-pipeline --app my-prod-app --stage production

# Promote from staging to production
heroku pipelines:promote --app my-staging-app

# View pipeline info
heroku pipelines:info my-pipeline
```

### Complete Walkthrough: Deploying my-heroku-app

Here's a step-by-step guide using the actual `my-heroku-app` repository:

```bash
# Step 1: Clone the repository
git clone https://github.com/md-sarowar-alam/my-heroku-app.git
cd my-heroku-app

# Step 2: Review the project structure
ls
# You should see:
# - server.js (main Express application)
# - package.json (dependencies: Express ^5.1.0)
# - Procfile (contains: web: node server.js)
# - my_photo.jpg (static asset image)
# - .gitignore (ignores node_modules and .env)

# Step 3: Inspect the key files
cat package.json        # Check dependencies and start script
cat Procfile           # Verify Heroku process configuration
cat server.js          # Review Express server code
cat .gitignore         # Check ignored files

# Step 4: Install dependencies locally (optional, for testing)
npm install

# Step 5: Test locally before deploying
npm start
# Visit http://localhost:3000 in your browser
# You should see: "Hello! Your Node app is running" with your photo
# Press Ctrl+C to stop

# Step 6: Login to Heroku
heroku login
# Browser will open for authentication

# Step 7: Create Heroku app with unique name
heroku create devops-batch09-myapp
# Or let Heroku generate a name:
# heroku create

# Step 8: Verify remotes were added
git remote -v
# Should show:
# origin  https://github.com/md-sarowar-alam/my-heroku-app.git
# heroku  https://git.heroku.com/devops-batch09-myapp.git

# Step 9: Deploy to Heroku
git push heroku main
# Watch the build process

# Step 10: Ensure web dyno is running
heroku ps:scale web=1

# Step 11: Check dyno status
heroku ps
# Should show: web.1: up

# Step 12: View real-time logs
heroku logs --tail
# Look for: "Server is running on port XXXXX"
# Press Ctrl+C to exit

# Step 13: Open deployed app in browser
heroku open
# Your app should display the HTML page with photo

# Step 14: Check app configuration
heroku config
# View all environment variables

# Step 15: Set custom environment variables (optional)
heroku config:set NODE_ENV=production
heroku config:set APP_TITLE="My Awesome App"

# Step 16: View app info
heroku apps:info
# Shows: region, web URL, Git URL, etc.

# Step 17: Make a change and redeploy
# Edit server.js or add new file
echo "\n<!-- Updated $(date) -->" >> server.js
git add .
git commit -m "Update: Add timestamp comment"
git push heroku main

# Step 18: View release history
heroku releases
# Shows all deployments

# Step 19: Rollback if needed (optional)
heroku rollback
# Or to specific version:
# heroku rollback v3

# Step 20: Run commands in Heroku environment
heroku run bash
# Inside Heroku dyno:
ls -la
node --version
npm list
exit

# Step 21: Monitor app health
heroku ps:metrics
heroku logs --source app --tail

# Step 22: Restart app
heroku restart

# Step 23: Clean up (delete app when done)
heroku apps:destroy --app devops-batch09-myapp --confirm devops-batch09-myapp
```

**What Makes This App Heroku-Ready:**

1. **Procfile** - Tells Heroku how to start the app:
   ```
   web: node server.js
   ```

2. **Dynamic PORT** - Uses Heroku's assigned port:
   ```javascript
   const PORT = process.env.PORT || 3000;
   ```

3. **package.json start script** - Defines how to start:
   ```json
   "scripts": {
     "start": "node server.js"
   }
   ```

4. **Static file serving** - Serves images and other assets:
   ```javascript
   app.use(express.static(__dirname));
   ```

5. **.gitignore** - Prevents committing node_modules:
   ```
   node_modules/
   .env
   ```

**Common Issues and Solutions:**

```bash
# Issue: Application Error / H10 error
# Solution: Check logs
heroku logs --tail
# Ensure Procfile exists and is correct

# Issue: Port binding error
# Solution: Verify you're using process.env.PORT
grep "process.env.PORT" server.js

# Issue: Module not found
# Solution: Ensure dependencies are in package.json
npm install --save missing-package
git add package.json package-lock.json
git commit -m "Add missing dependency"
git push heroku main

# Issue: Build failure
# Solution: Specify Node.js version in package.json
# Add to package.json:
# "engines": { "node": "18.x" }

# Issue: Cannot access app URL
# Solution: Scale web dyno
heroku ps:scale web=1
heroku ps
```

#### Custom Buildpacks:

```bash
# Set buildpack
heroku buildpacks:set heroku/nodejs

# Add additional buildpack
heroku buildpacks:add --index 1 heroku/python

# View buildpacks
heroku buildpacks

# Remove buildpack
heroku buildpacks:remove heroku/python

# Use custom buildpack
heroku buildpacks:set https://github.com/user/custom-buildpack
```

#### Deployment Hooks:

```bash
# Heroku automatically runs these if present (package.json scripts):
"scripts": {
  "heroku-prebuild": "echo Pre-build",
  "heroku-postbuild": "npm run build"
}

# Optional custom script (not an automatic Heroku lifecycle hook)
# This must be run manually, e.g. via `npm run heroku-cleanup` or from CI/CD:
"scripts": {
  "heroku-cleanup": "npm prune --production"
}

# Run commands after deployment
# Using release phase in Procfile:
release: python manage.py migrate
web: gunicorn app:app
```

### CI/CD Integration

#### GitHub Actions Deployment:

```yaml
# .github/workflows/deploy.yml
name: Deploy to Heroku

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Deploy to Heroku
        uses: akhileshns/heroku-deploy@v3.12.14
        with:
          heroku_api_key: ${{secrets.HEROKU_API_KEY}}
          heroku_app_name: "my-app"
          heroku_email: "your-email@example.com"

      - name: Run migrations
        run: |
          heroku run python manage.py migrate --app my-app
        env:
          HEROKU_API_KEY: ${{secrets.HEROKU_API_KEY}}
```

#### GitLab CI Deployment:

```yaml
# .gitlab-ci.yml
stages:
  - deploy

deploy_staging:
  stage: deploy
  image: ruby:3.0
  before_script:
    - gem install dpl
  script:
    - dpl --provider=heroku --app=my-staging-app --api-key=$HEROKU_API_KEY
  only:
    - develop

deploy_production:
  stage: deploy
  image: ruby:3.0
  before_script:
    - gem install dpl
  script:
    - dpl --provider=heroku --app=my-prod-app --api-key=$HEROKU_API_KEY
  only:
    - main
  when: manual
```

#### Direct Git Deployment:

```bash
# Add Heroku remote
heroku git:remote -a my-app

# Deploy specific branch
git push heroku develop:main

# Force push (use carefully)
git push heroku main --force

# Deploy from subdirectory
git subtree push --prefix backend heroku main

# Or using heroku-repo plugin
heroku plugins:install heroku-repo
heroku repo:purge_cache -a my-app
```

**Example: Deploy from existing repository**

```bash
# Clone your application
git clone https://github.com/md-sarowar-alam/my-heroku-app.git
cd my-heroku-app

# Add Heroku remote (if not already added)
heroku git:remote -a your-heroku-app-name

# Or create new Heroku app
heroku create

# Deploy
git push heroku main

# View deployment
heroku open
heroku logs --tail
```

#### Container Deployment:

```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

CMD ["node", "server.js"]
```

```bash
# Set stack to container
heroku stack:set container

# Deploy container
git push heroku main

# Or use Heroku Container Registry
heroku container:login
heroku container:push web
heroku container:release web
```

### Monitoring and Logs:

```bash
# View real-time logs
heroku logs --tail

# View specific dyno logs
heroku logs --dyno web.1

# View logs with source
heroku logs --source app

# Filter logs
heroku logs --tail | grep ERROR

# View metrics
heroku ps:metrics

# Add logging addon
heroku addons:create papertrail

# View app status
heroku apps:info
```

### Heroku Troubleshooting:

```bash
# Check build logs
heroku logs --tail

# Run bash in dyno
heroku run bash

# Check environment
heroku run env

# Test Procfile locally
heroku local web

# Check release history
heroku releases

# Rollback to previous release
heroku rollback v123

# Restart app
heroku restart

# Clear build cache
heroku plugins:install heroku-repo
heroku repo:purge_cache -a my-app
```

---

## Advanced Topics

### Repository Roles

Different platforms have different permission levels for collaborators:

#### GitHub Repository Roles:

| Role | Description | Permissions |
|------|-------------|-------------|
| **Read** | Can view and clone | Clone, pull, view issues/PRs |
| **Triage** | Can manage issues | Read + manage issues and PRs |
| **Write** | Can push to repo | Triage + push, create branches |
| **Maintain** | Can manage repo | Write + manage settings (no delete) |
| **Admin** | Full access | All permissions including delete |

**Setting Roles in GitHub:**
```bash
# Via GUI:
# Repository > Settings > Collaborators > Add people
# Select permission level

# Via GitHub CLI
gh api repos/owner/repo/collaborators/username -X PUT -f permission=write
```

#### GitLab Repository Roles:

| Role | Description | Permissions |
|------|-------------|-------------|
| **Guest** | Minimal access | View issues, leave comments |
| **Reporter** | Read-only | Clone, pull, download code |
| **Developer** | Push access | Reporter + push, create branches, merge |
| **Maintainer** | Manage repo | Developer + manage settings, protect branches |
| **Owner** | Full control | All permissions |

**Setting Roles in GitLab:**
```bash
# Via GUI:
# Project > Members > Invite member
# Select role level

# Via GitLab API
curl --request POST --header "PRIVATE-TOKEN: <token>" \
  "https://gitlab.com/api/v4/projects/PROJECT_ID/members" \
  --data "user_id=USER_ID&access_level=30"
```

#### Azure DevOps Roles:

| Role | Permissions |
|------|-------------|
| **Reader** | View repo, clone |
| **Contributor** | Reader + push changes |
| **Build Admin** | Contributor + manage build pipelines |
| **Project Admin** | Full administrative access |

### Branch Protection Rules

Branch protection prevents unauthorized changes to important branches.

#### GitHub Branch Protection:

**Configure via GUI:**
1. Repository > Settings > Branches
2. Add rule or edit existing
3. Configure protection rules

**Common Protection Rules:**
```yaml
# Require pull request reviews
- Require approvals: 1-6 reviewers
- Dismiss stale reviews when new commits are pushed
- Require review from Code Owners

# Require status checks
- Require branches to be up to date
- Require specific checks to pass (CI/CD)

# Require signed commits
- Require commit signature verification

# Additional rules
- Include administrators
- Restrict who can push
- Allow force pushes: No
- Allow deletions: No
```

**Example GitHub API:**
```bash
# Protect main branch
curl -X PUT \
  -H "Authorization: token YOUR_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/OWNER/REPO/branches/main/protection \
  -d '{
    "required_status_checks": {
      "strict": true,
      "contexts": ["continuous-integration/jenkins"]
    },
    "enforce_admins": true,
    "required_pull_request_reviews": {
      "required_approving_review_count": 2
    },
    "restrictions": null
  }'
```

#### GitLab Protected Branches:

**Configure via GUI:**
1. Project > Settings > Repository > Protected Branches
2. Select branch and protection levels

**Protection Levels:**
```bash
# Allowed to merge:
- No one
- Developers + Maintainers
- Maintainers

# Allowed to push:
- No one
- Developers + Maintainers
- Maintainers

# Allowed to force push: Yes/No
# Code owner approval required: Yes/No
```

**Example GitLab API:**
```bash
# Protect main branch
curl --request POST --header "PRIVATE-TOKEN: <token>" \
  "https://gitlab.com/api/v4/projects/PROJECT_ID/protected_branches" \
  --data "name=main&push_access_level=40&merge_access_level=30"

# Access levels:
# 0 = No access
# 30 = Developer
# 40 = Maintainer
# 60 = Admin
```

### Restricting Branch Deletion

#### GitHub:

**Method 1: Branch Protection Rules**
```bash
# In branch protection settings:
# ✓ Do not allow deletion
```

**Method 2: Required Reviews**
```bash
# Require pull request reviews before merging
# This prevents direct pushes and deletions
```

**Method 3: Repository Permissions**
```bash
# Limit write access to specific users/teams
# Repository > Settings > Manage access
# Only users with "Admin" role can delete protected branches
```

#### GitLab:

**Protected Branches:**
```bash
# Project > Settings > Repository > Protected Branches
# Set "Allowed to push" and "Allowed to merge" to "Maintainers"
# Developers cannot delete protected branches

# Via API
curl --request POST --header "PRIVATE-TOKEN: <token>" \
  "https://gitlab.com/api/v4/projects/PROJECT_ID/protected_branches" \
  --data "name=main&allow_force_push=false"
```

#### Local Git Configuration:

```bash
# Prevent accidental local branch deletion
# Create git alias
git config --global alias.delete-branch '!f() { \
  echo "Are you sure you want to delete branch $1? (yes/no)"; \
  read answer; \
  if [ "$answer" = "yes" ]; then \
    git branch -D $1; \
  else \
    echo "Deletion cancelled"; \
  fi; \
}; f'

# Usage
git delete-branch feature-branch
```

### Protecting History

#### Preventing Force Pushes:

```bash
# GitHub: Branch Protection Rules
# ✓ Do not allow force pushes

# GitLab: Protected Branches
# Allowed to force push: Toggle OFF

# Azure DevOps: Branch Policies
# Enable "Limit merge types" - uncheck "Rebase and fast-forward"
```

#### Preventing History Rewriting:

**Server-side Hooks (GitHub/GitLab):**
```bash
# Configure in Settings > Webhooks > Pre-receive hooks
# Reject force pushes and history rewrites
```

**Git Configuration:**
```bash
# Deny all force pushes to main
git config branch.main.pushRemote noforcepush

# For team repos, use server-side hooks
# Example pre-receive hook (saves in bare repo):
#!/bin/bash
while read oldrev newrev refname; do
  if [[ "$refname" == "refs/heads/main" ]]; then
    if [ "$oldrev" != "0000000000000000000000000000000000000000" ]; then
      # Check if it's a force push
      if ! git merge-base --is-ancestor $oldrev $newrev; then
        echo "ERROR: Force push to main is not allowed"
        exit 1
      fi
    fi
  fi
done
```

#### Signed Commits (Verification):

**Setup GPG Signing:**
```bash
# Generate GPG key
gpg --full-generate-key

# List keys
gpg --list-secret-keys --keyid-format LONG

# Export public key
gpg --armor --export KEY_ID

# Add to GitHub: Settings > SSH and GPG keys > New GPG key

# Configure Git to sign commits
git config --global user.signingkey KEY_ID
git config --global commit.gpgsign true

# Sign individual commit
git commit -S -m "Signed commit"

# Verify signatures
git log --show-signature
```

#### Audit Logging:

```bash
# GitHub: Enterprise only
# Settings > Audit log

# GitLab: Premium/Ultimate
# Admin Area > Monitoring > Audit Events

# Git built-in logging
git log --all --full-history --reflog
git reflog show --all

# Track who did what
git log --pretty=format:"%h - %an, %ar : %s"

# Find when file was deleted
git log --all --full-history -- path/to/file
```

#### Backup and Recovery:

```bash
# Create backup
git bundle create repo-backup.bundle --all

# Restore from backup
git clone repo-backup.bundle restored-repo

# Mirror repository
git clone --mirror https://github.com/user/repo.git
cd repo.git
git push --mirror https://github.com/user/backup-repo.git

# Recover deleted branch
git reflog
git checkout -b recovered-branch commit-hash

# Recover deleted commits
git fsck --lost-found
```

### Repository Templates and Standards

**Create `.gitignore`:**
```bash
# Example .gitignore (from my-heroku-app repository)
node_modules/
.env

# For Node.js projects
node_modules/
dist/
.env
*.log
npm-debug.log*

# For Python
__pycache__/
*.py[cod]
venv/
.env

# For Java
*.class
target/
*.jar

# For .NET
bin/
obj/
*.dll
```

**Create `CODEOWNERS`:**
```bash
# .github/CODEOWNERS or .gitlab/CODEOWNERS
# Global owners
* @team-lead

# Directory owners
/docs/ @documentation-team
/src/backend/ @backend-team
/src/frontend/ @frontend-team

# File type owners
*.js @javascript-team
*.py @python-team
*.md @technical-writers
```

**Create Pull Request Template:**
```markdown
# .github/pull_request_template.md

## Description
<!-- Describe your changes -->

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added to complex code
- [ ] Documentation updated
- [ ] No new warnings
- [ ] Tests added/updated
- [ ] All tests pass
```

---

## Quick Reference Commands

### Essential Daily Commands:
```bash
# Check status
git status

# Pull latest changes
git pull

# Create and switch to branch
git switch -c feature-name

# Stage and commit
git add .
git commit -m "Your message"

# Push changes
git push origin branch-name

# Switch to main and update
git switch main
git pull

# Merge feature branch
git merge feature-name

# Delete merged branch
git branch -d feature-name

# Sync with upstream (for forks)
git fetch upstream
git merge upstream/main

# Create pull request (GitHub CLI)
gh pr create

# Deploy to Heroku
git push heroku main
```

### Configuration:
```bash
# View config
git config --list

# Set user info
git config --global user.name "Name"
git config --global user.email "email@example.com"

# Set default editor
git config --global core.editor "code --wait"

# Aliases
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
git config --global alias.cm commit
```

### Troubleshooting:
```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Discard all local changes
git restore .

# Update remote URL
git remote set-url origin new-url

# Fetch all branches
git fetch --all

# Clean untracked files
git clean -fd

# Show what will be cleaned
git clean -nd
```

---

## Best Practices for DevOps Engineers

1. **Commit Often, Push Regularly**: Small, frequent commits are better than large ones
2. **Write Meaningful Commit Messages**: Follow conventional commits format
3. **Use Branches**: Never commit directly to main/master
4. **Pull Before Push**: Always sync with remote before pushing
5. **Review Before Committing**: Use `git diff` to review your changes
6. **Protect Main Branch**: Require reviews and passing tests
7. **Use SSH for Authentication**: More secure than HTTPS
8. **Sign Your Commits**: Adds verification and trust
9. **Keep History Clean**: Use rebase for feature branches, merge for releases
10. **Automate with CI/CD**: Integrate Git with Jenkins, GitHub Actions, GitLab CI
11. **Keep Forks Synced**: Regularly update your fork with upstream changes
12. **Write Descriptive PRs**: Include context, testing steps, and screenshots
13. **Keep PRs Small**: Easier to review and less likely to have conflicts
14. **Test Before Deploying**: Always test locally and in staging before production
15. **Use Environment Variables**: Never commit secrets or credentials

---

## Additional Resources

### This Guide
- **GitHub Repository**: https://github.com/md-sarowar-alam/Git-Fundamentals
- **Issues & Discussions**: https://github.com/md-sarowar-alam/Git-Fundamentals/issues
- **Fork This Repo**: https://github.com/md-sarowar-alam/Git-Fundamentals/fork
- **Sample Heroku App**: https://github.com/md-sarowar-alam/my-heroku-app (Private - for deployment practice)

### Official Documentation
- **Official Git Documentation**: https://git-scm.com/doc
- **GitHub Docs**: https://docs.github.com
- **GitLab Docs**: https://docs.gitlab.com
- **Atlassian Git Tutorials**: https://www.atlassian.com/git/tutorials
- **Pro Git Book** (Free): https://git-scm.com/book/en/v2
- **Git Cheat Sheet**: https://education.github.com/git-cheat-sheet-education.pdf

---

## Practice Exercises

### Exercise 1: Basic Workflow
```bash
# 1. Clone this repository
git clone https://github.com/md-sarowar-alam/Git-Fundamentals.git
cd Git-Fundamentals

# 2. Create a test file
echo "# My Practice" > practice.md

# 3. Make 3 commits with different changes
git add practice.md
git commit -m "feat: Add practice file"

echo "Adding more content" >> practice.md
git add practice.md
git commit -m "docs: Update practice file"

echo "Final changes" >> practice.md
git add practice.md
git commit -m "docs: Complete practice exercise"

# 4. View your commit history
git log --oneline
```

### Exercise 2: Branching and Merging
```bash
# 1. Create a feature branch
# 2. Make changes and commit
# 3. Switch back to main
# 4. Make different changes and commit
# 5. Merge feature branch
# 6. Resolve any conflicts
```

### Exercise 3: SSH Setup
```bash
# 1. Generate SSH key
# 2. Add to GitHub/GitLab
# 3. Test connection
# 4. Clone a repository using SSH
```

### Exercise 4: Branch Protection
```bash
# 1. Create a repository on GitHub
# 2. Set up branch protection for main
# 3. Try to push directly to main (should fail)
# 4. Create PR and merge properly
```

### Exercise 5: Forking Workflow
```bash
# 1. Fork this repository on GitHub
# Go to: https://github.com/md-sarowar-alam/Git-Fundamentals
# Click "Fork" button

# 2. Clone your fork locally
git clone https://github.com/YOUR_USERNAME/Git-Fundamentals.git
cd Git-Fundamentals

# 3. Add upstream remote
git remote add upstream https://github.com/md-sarowar-alam/Git-Fundamentals.git
git remote -v

# 4. Create a feature branch
git checkout -b docs/improve-readme

# 5. Make changes and push to your fork
echo "\n## My Contribution" >> README.md
git add README.md
git commit -m "docs: Add contribution section"
git push origin docs/improve-readme

# 6. Create a pull request to original repo
# Go to your fork on GitHub and click "Compare & pull request"
```

### Exercise 6: Pull Request Practice
```bash
# 1. Create a new branch in your repository
# 2. Make multiple commits
# 3. Push and create a PR
# 4. Request review from a colleague
# 5. Address feedback and update PR
# 6. Merge using squash strategy
```

### Exercise 7: Heroku Deployment
```bash
# Complete Heroku Deployment Exercise

# 1. Clone the sample Heroku app
git clone https://github.com/md-sarowar-alam/my-heroku-app.git
cd my-heroku-app

# 2. Inspect the files
cat package.json     # Check dependencies (express ^5.1.0)
cat Procfile         # Should contain: web: node server.js
cat server.js        # Review the Express application
cat .gitignore       # Check ignored files (node_modules, .env)

# 3. Test locally first
npm install          # Install dependencies
npm start            # Run locally on port 3000
# Open browser: http://localhost:3000
# Verify the page loads with photo

# 4. Login to Heroku
heroku login

# 5. Create Heroku app with unique name
heroku create devops-batch09-$(whoami)
# Or let Heroku generate a name:
heroku create

# 6. Check remotes (should have 'origin' and 'heroku')
git remote -v

# 7. Deploy to Heroku
git push heroku main

# 8. Scale the web dyno
heroku ps:scale web=1

# 9. Set environment variables (optional)
heroku config:set NODE_ENV=production
heroku config:set APP_NAME="My Heroku App"

# 10. View all config
heroku config

# 11. Check dyno status
heroku ps

# 12. View real-time logs
heroku logs --tail
# Press Ctrl+C to exit

# 13. Open deployed app
heroku open

# 14. Make a change and redeploy
echo "\n// Updated on $(date)" >> server.js
git add server.js
git commit -m "Update server with timestamp"
git push heroku main

# 15. View release history
heroku releases

# 16. Rollback if needed (optional)
heroku rollback v2

# 17. View app info
heroku apps:info

# 18. Restart app
heroku restart

# 19. Run bash in Heroku dyno
heroku run bash
# Inside dyno:
ls -la
node --version
exit

# 20. Clean up (delete app when done)
heroku apps:destroy --app your-app-name --confirm your-app-name
```

**What You'll Learn:**
- ✅ Cloning and inspecting a Heroku-ready app
- ✅ Testing locally before deployment
- ✅ Creating and configuring Heroku apps
- ✅ Deploying using Git push
- ✅ Managing environment variables
- ✅ Monitoring logs and app health
- ✅ Rolling back deployments
- ✅ Running commands in Heroku environment

---

**Last Updated**: January 2026  
**Repository**: [md-sarowar-alam/Git-Fundamentals](https://github.com/md-sarowar-alam/Git-Fundamentals)  
**Maintainer**: [MD Sarowar Alam](https://github.com/md-sarowar-alam)  
**Audience**: Fresh DevOps Engineers  

---

### Support This Project

- ⭐ **Star** this repository: https://github.com/md-sarowar-alam/Git-Fundamentals
- 🍴 **Fork** it for your own use
- 🐛 **Report issues** or **suggest improvements**
- 📖 **Share** with your fellow DevOps engineers
- 💬 **Discuss** on GitHub Discussions

---

5. **Make your changes and commit**:
   ```bash
   git add .
   git commit -m "docs: Your improvement description"
   ```
6. **Push to your fork**:
   ```bash
   git push origin docs/your-improvement
   ```
7. **Create a Pull Request** on GitHub

**Issues**: Report bugs or suggest improvements at [GitHub Issues](https://github.com/md-sarowar-alam/Git-Fundamentals/issues)

---

## 🧑‍💻 Author

**Md. Sarowar Alam**  
Lead DevOps Engineer, Hogarth Worldwide  
📧 Email: sarowar@hotmail.com  
🔗 LinkedIn: [linkedin.com/in/sarowar](https://www.linkedin.com/in/sarowar/)  
🐙 GitHub: [@md-sarowar-alam](https://github.com/md-sarowar-alam)

---

### License

This guide is provided as educational material for DevOps engineers.

---

**© 2026 Md. Sarowar Alam. All rights reserved.**

