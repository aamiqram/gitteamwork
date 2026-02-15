# 🚀 Unity Shop - Team Development Guide (v2.0)

**Repository:** https://github.com/siddiquesakib/Unity-Shop  
**Team:** Unity-Stack  
**Team Leader:** Mohammad Siddique Sakib  
**Team Size:** 6 Members

---

## 📋 Table of Contents

1. [Branching Strategy](#branching-strategy)
2. [Initial Setup](#initial-setup)
3. [Daily Workflow](#daily-workflow)
4. [Working on Your Branch](#working-on-your-branch)
5. [Merging to Develop](#merging-to-develop)
6. [Release Process](#release-process)
7. [Commit Conventions](#commit-conventions)
8. [Do's and Don'ts](#dos-and-donts)
9. [Common Commands](#common-commands)
10. [Troubleshooting](#troubleshooting)

---

## 🌿 Branching Strategy

### Our Branch Structure

```
main (production-ready code - PROTECTED, NO DIRECT PUSH)
  ↑
develop (integration & testing - merge here before main)
  ↑
  ├── member-1 (Team Member 1's work)
  ├── member-2 (Team Member 2's work)
  ├── member-3 (Team Member 3's work)
  ├── member-4 (Team Member 4's work)
  ├── member-5 (Team Member 5's work)
  └── member-6 (Team Member 6's work)
```

### Branch Rules

| Branch | Purpose | Who Can Push | Merge From | Merge To |
|--------|---------|--------------|------------|----------|
| **main** | Production code | ❌ NOBODY (Team Leader only via PR) | develop | - |
| **develop** | Integration & testing | ✅ All members via PR | member-* branches | main |
| **member-1 to member-6** | Individual work | ✅ Assigned member only | develop | develop |

### Key Principles

1. **NEVER push directly to main** - Team leader merges via PR only
2. **Work on your assigned member branch** - Don't work on other members' branches
3. **Sync with develop regularly** - Pull develop changes to stay updated
4. **Merge to develop when feature is ready** - Create PR for code review
5. **Test before merging** - Make sure your code works

---

## 🎯 Initial Setup (First Time Only)

### Step 1: Identify Your Member Branch

**Ask your team leader which branch is assigned to you:**
- member-1
- member-2
- member-3
- member-4
- member-5
- member-6

Let's assume you're assigned **member-3** for this guide.

### Step 2: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/siddiquesakib/Unity-Shop.git

# Navigate to project directory
cd Unity-Shop

# Verify remote
git remote -v
```

### Step 3: Fetch All Branches

```bash
# Fetch all branches from remote
git fetch origin

# View all available branches
git branch -a

# You should see:
# * main
#   remotes/origin/main
#   remotes/origin/develop
#   remotes/origin/member-1
#   remotes/origin/member-2
#   remotes/origin/member-3
#   remotes/origin/member-4
#   remotes/origin/member-5
#   remotes/origin/member-6
```

### Step 4: Checkout Your Assigned Branch

```bash
# Checkout your assigned member branch (example: member-3)
git checkout member-3

# Verify you're on the correct branch
git branch
# Output: * member-3

# Pull latest changes
git pull origin member-3
```

### Step 5: Install Dependencies

```bash
# Install all project dependencies
npm install
```

### Step 6: Set Up Environment Variables

```bash
# Copy the example environment file
cp .env.example .env.local

# Open and configure your environment
code .env.local
```

**Required Environment Variables:**
```env
DATABASE_URL="your_database_connection_string"
NEXTAUTH_SECRET="your_secret_key_here"
NEXTAUTH_URL="http://localhost:3000"
NEXT_PUBLIC_API_URL="http://localhost:3000/api"
```

### Step 7: Database Setup

```bash
# Run database migrations
npx prisma migrate dev

# Generate Prisma Client
npx prisma generate

# (Optional) Seed database
npm run seed
```

### Step 8: Verify Installation

```bash
# Start development server
npm run dev

# Open browser at http://localhost:3000
```

---

## 📅 Daily Workflow

### 🌅 Starting Your Work Day

```bash
# 1. Navigate to project directory
cd Unity-Shop

# 2. Make sure you're on YOUR member branch
git checkout member-3
# Replace member-3 with your assigned branch

# 3. Pull latest changes from YOUR branch
git pull origin member-3

# 4. Sync with develop to get team updates
git pull origin develop

# 5. Check status
git status

# Now you're ready to start coding! 🎉
```

### 💻 During Development

```bash
# Check what files you've modified
git status

# See detailed changes
git diff

# Stage specific files
git add path/to/file.js

# Or stage all changes
git add .

# Commit your changes
git commit -m "feat: add user authentication"

# Push to YOUR member branch
git push origin member-3
```

### 🌙 Before Ending Your Day

```bash
# 1. Make sure all changes are committed
git status

# 2. Push your work to YOUR branch
git push origin member-3

# 3. (Optional) Pull latest develop changes
git pull origin develop

# Good night! 😊
```

---

## 🔨 Working on Your Branch

### Your Member Branch Workflow

```bash
# ALWAYS work on your assigned branch
git checkout member-3

# Pull latest from YOUR branch
git pull origin member-3

# Write code, make changes...

# Stage changes
git add .

# Commit with clear message
git commit -m "feat: implement shopping cart functionality"

# Push to YOUR branch
git push origin member-3
```

### Syncing with Team Changes (from develop)

```bash
# Make sure you're on your branch
git checkout member-3

# Pull latest team changes from develop
git pull origin develop

# If there are conflicts, resolve them
# Then commit the merge
git add .
git commit -m "merge: sync with develop branch"

# Push updated branch
git push origin member-3
```

### Creating Feature Sub-branches (Optional)

If you want to organize your work into smaller features:

```bash
# Create feature branch from your member branch
git checkout member-3
git checkout -b member-3/shopping-cart

# Work on feature
# ... code ...

# Commit changes
git add .
git commit -m "feat: add shopping cart UI"

# When done, merge back to your member branch
git checkout member-3
git merge member-3/shopping-cart

# Push to your member branch
git push origin member-3

# Delete feature sub-branch
git branch -d member-3/shopping-cart
```

---

## 🔄 Merging to Develop

### When to Merge to Develop

✅ Merge when:
- You completed a feature
- Your code is tested and working
- No console errors or warnings
- Ready for team integration

### Step-by-Step Merge Process

#### Option 1: Using Pull Request (RECOMMENDED)

```bash
# 1. Make sure your work is committed and pushed
git checkout member-3
git add .
git commit -m "feat: complete user profile feature"
git push origin member-3

# 2. Go to GitHub: https://github.com/siddiquesakib/Unity-Shop
# 3. Click "Pull requests" tab
# 4. Click "New pull request"
# 5. Set:
#    - base: develop
#    - compare: member-3 (your branch)
# 6. Fill in PR details:
#    Title: "feat: Add user profile feature"
#    Description: What you built, how to test it
# 7. Create pull request
# 8. Request review from team leader
# 9. Wait for approval and merge
```

#### Option 2: Direct Merge (Only if team agrees)

```bash
# 1. Sync your branch with develop first
git checkout member-3
git pull origin develop

# 2. Resolve any conflicts if they exist
# 3. Push resolved version
git push origin member-3

# 4. Switch to develop branch
git checkout develop

# 5. Pull latest develop
git pull origin develop

# 6. Merge your branch into develop
git merge member-3

# 7. Test that everything works
npm run dev

# 8. Push to develop
git push origin develop

# 9. Switch back to your branch
git checkout member-3
```

---

## 🚀 Release Process (Team Leader Only)

### Merging Develop to Main

```bash
# Team leader only!

# 1. Ensure all member branches are merged to develop
# 2. Test develop thoroughly
# 3. Create PR from develop to main
# 4. Review and approve
# 5. Merge to main
# 6. Tag release

git checkout main
git pull origin main
git merge develop
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main --tags
```

---

## 📝 Commit Conventions

### Commit Message Format

```
<type>(<scope>): <subject>
```

### Commit Types

| Type | Usage | Example |
|------|-------|---------|
| `feat` | New feature | `feat: add product search` |
| `fix` | Bug fix | `fix: resolve cart calculation error` |
| `style` | Formatting | `style: format code with prettier` |
| `refactor` | Code improvement | `refactor: optimize query performance` |
| `test` | Adding tests | `test: add cart unit tests` |
| `docs` | Documentation | `docs: update README` |
| `chore` | Maintenance | `chore: update dependencies` |

### Good Commit Examples

```bash
# ✅ GOOD
git commit -m "feat: implement user authentication system"
git commit -m "fix: resolve checkout payment bug"
git commit -m "refactor: improve product search algorithm"
git commit -m "docs: add API documentation"

# ❌ BAD
git commit -m "update"
git commit -m "fix"
git commit -m "changes"
git commit -m "done"
```

---

## ✅ Do's and Don'ts

### ✅ MUST DO

```bash
# ✅ Always work on YOUR assigned branch
git checkout member-3

# ✅ Pull before starting work
git pull origin member-3
git pull origin develop

# ✅ Commit frequently with clear messages
git commit -m "feat: add login form validation"

# ✅ Push your work daily
git push origin member-3

# ✅ Sync with develop regularly
git pull origin develop

# ✅ Test before pushing
npm run dev
npm run lint

# ✅ Ask before merging to develop
# Create PR or inform team leader
```

### ❌ NEVER DO

```bash
# ❌ NEVER push to main
git push origin main  # ⛔ FORBIDDEN

# ❌ NEVER work on other members' branches
git checkout member-5  # ⛔ Only if you're member-5

# ❌ NEVER force push to develop
git push -f origin develop  # ⛔ FORBIDDEN

# ❌ NEVER delete others' work
git push -f origin member-2  # ⛔ FORBIDDEN

# ❌ NEVER commit sensitive data
git add .env
git add .env.local  # ⛔ FORBIDDEN

# ❌ NEVER commit node_modules
git add node_modules/  # ⛔ FORBIDDEN

# ❌ NEVER use generic commit messages
git commit -m "update"  # ⛔ BAD
git commit -m "fix"     # ⛔ BAD
```

---

## 🛠️ Common Commands Reference

### Daily Use Commands

```bash
# Check which branch you're on
git branch

# Check current status
git status

# View recent commits
git log --oneline -5

# See what changed
git diff

# Discard changes in specific file
git checkout -- filename.js

# Unstage file
git reset HEAD filename.js
```

### Branch Management

```bash
# Switch to your branch
git checkout member-3

# Switch to develop
git checkout develop

# View all branches
git branch -a

# Pull latest from your branch
git pull origin member-3

# Pull latest from develop
git pull origin develop

# Push to your branch
git push origin member-3
```

### Syncing Commands

```bash
# Complete sync workflow
git checkout member-3
git pull origin member-3
git pull origin develop
git add .
git commit -m "merge: sync with develop"
git push origin member-3
```

### Stashing (Save Work Temporarily)

```bash
# Save current work
git stash

# Save with message
git stash save "work in progress on cart"

# View stashed work
git stash list

# Restore latest stash
git stash pop

# Restore specific stash
git stash apply stash@{0}
```

---

## 🔧 Development Commands

### Running the Project

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run linter
npm run lint

# Fix linting issues
npm run lint:fix

# Format code
npm run format

# Run tests
npm test

# Type checking
npm run type-check
```

### Database Commands

```bash
# Create migration
npx prisma migrate dev --name migration-name

# Apply migrations
npx prisma migrate deploy

# Generate Prisma Client
npx prisma generate

# Open Prisma Studio (Database GUI)
npx prisma studio

# Reset database (CAUTION!)
npx prisma migrate reset
```

---

## 🚨 Troubleshooting

### Problem: Merge Conflicts

```bash
# When you see merge conflict

# 1. Check which files have conflicts
git status

# 2. Open conflicting files in editor
# Look for markers: <<<<<<<, =======, >>>>>>>

# 3. Choose which code to keep or combine them

# 4. Remove conflict markers

# 5. Stage resolved files
git add resolved-file.js

# 6. Complete the merge
git commit -m "fix: resolve merge conflicts with develop"

# 7. Push
git push origin member-3
```

### Problem: I'm on the Wrong Branch

```bash
# Save your current work
git stash

# Switch to correct branch
git checkout member-3

# Apply your work
git stash pop
```

### Problem: I Need to Undo Last Commit

```bash
# Undo commit but keep changes
git reset --soft HEAD~1

# Make corrections

# Commit again
git add .
git commit -m "feat: corrected feature implementation"
```

### Problem: I Accidentally Committed to Wrong Branch

```bash
# 1. Note the commit hash
git log -1

# 2. Undo the commit (keep changes)
git reset --soft HEAD~1

# 3. Stash changes
git stash

# 4. Switch to correct branch
git checkout member-3

# 5. Apply changes
git stash pop

# 6. Commit to correct branch
git add .
git commit -m "feat: your feature"
git push origin member-3
```

### Problem: My Branch is Behind Develop

```bash
# Sync with develop
git checkout member-3
git pull origin develop

# Resolve any conflicts if needed

# Push updated branch
git push origin member-3
```

### Problem: I Need Team Member's Code

```bash
# Option 1: Wait for them to merge to develop
git pull origin develop

# Option 2: Communicate with team member
# They should merge their code to develop first
```

### Problem: Port Already in Use

```bash
# Find and kill process on port 3000
lsof -i :3000
kill -9 PID

# Or use different port
PORT=3001 npm run dev
```

### Problem: node_modules Issues

```bash
# Clean reinstall
rm -rf node_modules
rm package-lock.json
npm cache clean --force
npm install
```

---

## 📊 Team Workflow Summary

### Perfect Day Workflow

```bash
# ☀️ Morning (Before starting work)
cd Unity-Shop
git checkout member-3
git pull origin member-3
git pull origin develop

# 💻 During Work
# ... write code ...
git add .
git commit -m "feat: implement feature"
git push origin member-3

# 🌙 Evening (Before leaving)
git add .
git commit -m "wip: work in progress"
git push origin member-3

# 📦 When Feature Complete
# Create Pull Request to develop
# Request review from team leader
```

### Weekly Workflow

```
Monday:
- Sync with develop
- Start new feature

Tuesday-Thursday:
- Work on feature
- Push daily
- Sync with develop

Friday:
- Complete feature
- Test thoroughly
- Create PR to develop
- Code review

Weekend:
- Team leader merges PRs
- Reviews develop branch
```

---

## 🎯 Branch Assignment Reference

Keep track of team member branches:

| Team Member | Branch | Responsibilities |
|-------------|--------|------------------|
| Member 1 | member-1 | [Your area] |
| Member 2 | member-2 | [Your area] |
| Member 3 | member-3 | [Your area] |
| Member 4 | member-4 | [Your area] |
| Member 5 | member-5 | [Your area] |
| Member 6 | member-6 | [Your area] |

---

## 🔒 Protected Branches Policy

### main Branch
- 🔒 **Protected**
- ❌ **No direct pushes**
- ✅ **Only team leader merges via PR**
- 📋 **Requires code review**
- ✅ **Must pass all tests**

### develop Branch
- ⚠️ **Semi-protected**
- ✅ **Members can merge via PR**
- 📋 **Recommended: code review**
- ✅ **Should be tested before merge**

### member-* Branches
- 🔓 **Not protected**
- ✅ **Each member has full access to their own**
- ❌ **Don't push to others' branches**

---

## 📞 Getting Help

### Before Asking for Help

1. ✅ Read error messages carefully
2. ✅ Check this guide
3. ✅ Check which branch you're on: `git branch`
4. ✅ Check current status: `git status`

### When Asking for Help

**Provide this information:**
```bash
# Current branch
git branch

# Current status
git status

# Recent commits
git log -3 --oneline

# Copy the error message
```

### Contact

**Team Leader:** Mohammad Siddique Sakib  
**Communication Channel:** [Your team communication]

---

## 🎓 Quick Reference Card

```bash
# 🌅 Start Day
git checkout member-3
git pull origin member-3
git pull origin develop

# 💻 Work
git add .
git commit -m "feat: description"
git push origin member-3

# 🔄 Sync with Team
git pull origin develop

# 📦 Finish Feature
# Go to GitHub
# Create PR: member-3 → develop
# Request review

# ❌ NEVER DO
git push origin main  # ⛔
git push -f origin develop  # ⛔
git checkout member-X  # ⛔ (if X is not yours)
```

---

## 🎯 Key Principles

1. **Work on YOUR branch only** (member-X)
2. **NEVER push to main**
3. **Sync with develop regularly**
4. **Push your work daily**
5. **Use Pull Requests to merge to develop**
6. **Write clear commit messages**
7. **Test before merging**
8. **Communicate with team**
9. **Ask when in doubt**
10. **Respect team members' branches**

---

<div align="center">

## 🚀 Happy Coding!

**Remember: Your branch = Your responsibility**

**Built with ❤️ by Unity-Stack Team**

---

### Quick Help

**Wrong branch?** → `git checkout member-3`  
**Need updates?** → `git pull origin develop`  
**Ready to merge?** → Create PR to develop  
**Confused?** → Ask team leader  

</div>

# 🚀 Unity Shop - Quick Reference Cheat Sheet

**Repository:** https://github.com/siddiquesakib/Unity-Shop

---

## 📌 Your Daily Commands

### 🌅 Start Your Day
```bash
cd Unity-Shop
git checkout member-X    # Replace X with your number
git pull origin member-X
git pull origin develop
```

### 💻 While Working
```bash
git status              # Check what changed
git add .              # Stage all changes
git commit -m "feat: description of what you did"
git push origin member-X
```

### 🌙 End Your Day
```bash
git add .
git commit -m "wip: work in progress"
git push origin member-X
```

---

## 🌿 Branch Structure

```
main (🔒 PROTECTED - Never push here!)
  ↑
develop (⚠️ Merge via PR)
  ↑
  ├── member-1
  ├── member-2
  ├── member-3
  ├── member-4
  ├── member-5
  └── member-6
```

**Your branch:** member-X (Replace X with your assigned number)

---

## ✅ DO's

```bash
✅ git checkout member-X          # Work on YOUR branch
✅ git pull origin develop         # Sync with team regularly
✅ git commit -m "feat: feature"   # Clear commit messages
✅ git push origin member-X        # Push daily
✅ Create PR to merge to develop   # Use Pull Requests
```

---

## ❌ DON'Ts

```bash
❌ git push origin main           # NEVER push to main
❌ git push -f origin develop     # NEVER force push
❌ git checkout member-5          # NEVER work on others' branches
❌ git add .env                   # NEVER commit secrets
❌ git commit -m "update"         # NEVER use vague messages
```

---

## 🔄 Sync with Team (Do this daily!)

```bash
git checkout member-X
git pull origin develop
# If conflicts, resolve them
git add .
git commit -m "merge: sync with develop"
git push origin member-X
```

---

## 📦 Merge to Develop (When feature is ready)

```bash
# 1. Push your latest work
git push origin member-X

# 2. Go to GitHub
https://github.com/siddiquesakib/Unity-Shop

# 3. Create Pull Request:
   base: develop
   compare: member-X

# 4. Request review from team leader

# 5. Wait for approval and merge
```

---

## 🆘 Quick Fixes

### Wrong Branch?
```bash
git stash
git checkout member-X
git stash pop
```

### Undo Last Commit?
```bash
git reset --soft HEAD~1
```

### Merge Conflict?
```bash
# 1. Open conflicting file
# 2. Look for: <<<<<<< ======= >>>>>>>
# 3. Fix the code
# 4. git add filename
# 5. git commit -m "fix: resolve conflict"
```

### Port in Use?
```bash
lsof -i :3000
kill -9 PID
```

---

## 📝 Commit Message Format

| Type | When to Use | Example |
|------|-------------|---------|
| `feat` | New feature | `feat: add login page` |
| `fix` | Bug fix | `fix: resolve cart bug` |
| `refactor` | Code improvement | `refactor: optimize queries` |
| `docs` | Documentation | `docs: update README` |
| `style` | Formatting | `style: format code` |

---

## 🎯 Remember

1. **YOUR BRANCH = member-X** (Know your number!)
2. **NEVER touch main branch**
3. **Sync with develop daily**
4. **Push your work every day**
5. **Use PR to merge to develop**

---

## 📞 Need Help?

**Check your status:**
```bash
git branch        # Which branch am I on?
git status        # What files changed?
```

**Contact:** Mohammad Siddique Sakib (Team Leader)

---

<div align="center">

### Print this and keep it handy! 📄

**Built with ❤️ by Unity-Stack**

</div>

# 🔄 Unity Shop - Git Workflow Diagram

**Team:** Unity-Stack  
**Repository:** https://github.com/siddiquesakib/Unity-Shop

---

## 📊 Branch Structure Diagram

```
┌──────────────────────────────────────────────────────────────┐
│                      🔒 main (Production)                     │
│                   ⛔ NO DIRECT PUSH                           │
│              Only Team Leader via PR                          │
└────────────────────────▲─────────────────────────────────────┘
                         │
                         │ PR (Code Review Required)
                         │
┌────────────────────────┴─────────────────────────────────────┐
│                    ⚠️ develop (Integration)                   │
│                  All team changes merge here                  │
│              Merge via Pull Request (Recommended)             │
└─┬──────┬──────┬──────┬──────┬──────┬─────────────────────────┘
  │      │      │      │      │      │
  │      │      │      │      │      │
  ▼      ▼      ▼      ▼      ▼      ▼
┌─────┐┌─────┐┌─────┐┌─────┐┌─────┐┌─────┐
│mem-1││mem-2││mem-3││mem-4││mem-5││mem-6│  ← 👥 Individual Work
└─────┘└─────┘└─────┘└─────┘└─────┘└─────┘
Each member works on their own branch
```

---

## 🔄 Daily Workflow

### Individual Member Workflow

```
      ┌──────────────────┐
      │  Start Your Day  │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │  git checkout    │
      │    member-X      │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │  git pull origin │
      │    member-X      │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │  git pull origin │
      │     develop      │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │   Write Code 💻  │
      │   Test Locally   │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │   git add .      │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │   git commit -m  │
      │  "feat: ..."     │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │  git push origin │
      │    member-X      │
      └────────┬─────────┘
               │
               ▼
      ┌──────────────────┐
      │   End Your Day   │
      └──────────────────┘
```

---

## 🔀 Merge to Develop Process

### When Feature is Complete

```
┌─────────────────────────────────────────────┐
│  Your Branch (member-X)                     │
│  Feature Complete ✅                        │
└───────────────────┬─────────────────────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Push Latest Changes │
         │  git push origin     │
         │     member-X         │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │   Go to GitHub       │
         │   Create Pull Request│
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │   PR Configuration   │
         │   base: develop      │
         │   compare: member-X  │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Request Review      │
         │  from Team Leader    │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │   Team Leader        │
         │   Reviews Code       │
         └──────────┬───────────┘
                    │
         ┌──────────┴──────────┐
         │                     │
         ▼                     ▼
   ┌─────────┐          ┌─────────┐
   │Request  │          │Approved │
   │Changes  │          │   ✅    │
   └────┬────┘          └────┬────┘
        │                    │
        │                    ▼
        │          ┌──────────────────┐
        │          │  Merge to develop│
        │          └──────────┬───────┘
        │                     │
        │                     ▼
        │          ┌──────────────────┐
        │          │   develop updated│
        │          │   with your work │
        │          └──────────────────┘
        │
        └──────► Fix issues, push again
```

---

## 🔄 Syncing with Team Changes

### Keeping Your Branch Updated

```
  Your Branch (member-X)
         │
         │  Daily Sync
         │
         ▼
  ┌──────────────────┐
  │  git pull origin │
  │     develop      │
  └────────┬─────────┘
           │
     ┌─────┴──────┐
     │            │
     ▼            ▼
  No Conflict   Conflict!
     │            │
     │            ▼
     │     ┌──────────────┐
     │     │  Resolve     │
     │     │  Conflicts   │
     │     └──────┬───────┘
     │            │
     │            ▼
     │     ┌──────────────┐
     │     │  git add .   │
     │     │  git commit  │
     │     └──────┬───────┘
     │            │
     └────────────┴────────┐
                           │
                           ▼
                  ┌──────────────┐
                  │  git push    │
                  │  origin      │
                  │  member-X    │
                  └──────────────┘
```

---

## 🚀 Release Process (Team Leader Only)

### Develop → Main Deployment

```
┌──────────────────────────────────────────┐
│  All Features Merged to develop          │
└───────────────────┬──────────────────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Test develop branch │
         │  Thoroughly          │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Create PR           │
         │  develop → main      │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Code Review         │
         │  Final Testing       │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Merge to main       │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Create Release Tag  │
         │  v1.0.0              │
         └──────────┬───────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Deploy to Production│
         └──────────────────────┘
```

---

## 📅 Weekly Timeline Example

```
Monday          Tuesday-Thursday         Friday
  │                    │                   │
  ▼                    ▼                   ▼
┌──────┐         ┌──────────┐       ┌──────────┐
│Sync  │         │  Develop │       │ Create   │
│with  │──────►  │  Feature │──────►│ PR to    │
│Team  │         │  & Push  │       │ develop  │
└──────┘         └──────────┘       └────┬─────┘
                                          │
                                          ▼
                                    ┌──────────┐
                                    │Code      │
                                    │Review    │
                                    └────┬─────┘
                                         │
  Weekend                                │
     │                                   │
     ▼                                   │
┌──────────┐                            │
│Team Lead │◄───────────────────────────┘
│Merges to │
│ develop  │
└──────────┘
```

---

## 🎯 Key Rules Visualized

### ✅ CORRECT Workflow

```
member-X ──PR──► develop ──PR──► main
   │                │
   │                │
  You           Team Work    Production
  Work          Integration
```

### ❌ WRONG Workflows

```
❌ DON'T DO THIS:

member-X ──DIRECT PUSH──► main
(NEVER PUSH DIRECTLY TO MAIN!)

member-X ──DIRECT PUSH──► member-Y
(DON'T WORK ON OTHER'S BRANCHES!)

member-X ──FORCE PUSH──► develop
(NO FORCE PUSHING!)
```

---

## 🔄 Conflict Resolution Flow

```
         Pull from develop
                │
                ▼
         ┌─────────────┐
         │  Conflict?  │
         └──────┬──────┘
                │
        ┌───────┴───────┐
        │               │
        ▼               ▼
     ┌────┐         ┌─────┐
     │ NO │         │ YES │
     └─┬──┘         └──┬──┘
       │               │
       │               ▼
       │        ┌────────────────┐
       │        │  Open file     │
       │        │  Find markers: │
       │        │  <<<<<<<       │
       │        │  =======       │
       │        │  >>>>>>>       │
       │        └───────┬────────┘
       │                │
       │                ▼
       │        ┌────────────────┐
       │        │  Choose code   │
       │        │  to keep or    │
       │        │  combine both  │
       │        └───────┬────────┘
       │                │
       │                ▼
       │        ┌────────────────┐
       │        │  Remove markers│
       │        └───────┬────────┘
       │                │
       │                ▼
       │        ┌────────────────┐
       │        │  git add file  │
       │        └───────┬────────┘
       │                │
       │                ▼
       │        ┌────────────────┐
       │        │  git commit    │
       │        │  "fix: resolve │
       │        │   conflict"    │
       │        └───────┬────────┘
       │                │
       └────────────────┴─────────┐
                                  │
                                  ▼
                           ┌─────────────┐
                           │  git push   │
                           │  origin     │
                           │  member-X   │
                           └─────────────┘
```

---

## 💡 Pro Tips

### When to Sync with Develop

```
📅 Frequency: DAILY

Best Times:
┌──────────────────────────────────────┐
│  ☀️ Morning (Start of day)           │
│  🍽️ After lunch                      │
│  🌙 Before ending work               │
└──────────────────────────────────────┘

Why?
- Get latest team changes
- Avoid big conflicts later
- Stay in sync with team
```

### When to Create PR

```
✅ Create PR when:
├─ Feature is complete
├─ Code is tested
├─ No console errors
└─ Ready for review

❌ Don't create PR when:
├─ Work in progress
├─ Code not tested
├─ Known bugs exist
└─ Not ready for review
```

---

## 🆘 Emergency Scenarios

### Scenario 1: Accidentally on Wrong Branch

```
❌ You're on member-5 but you're member-3

1. git stash              (Save work)
2. git checkout member-3  (Correct branch)
3. git stash pop         (Restore work)
4. Continue working ✅
```

### Scenario 2: Committed to Wrong Branch

```
❌ Committed to develop instead of member-3

1. git log -1            (Note commit hash)
2. git reset --soft HEAD~1  (Undo commit)
3. git stash             (Save changes)
4. git checkout member-3  (Correct branch)
5. git stash pop         (Restore changes)
6. git add .
7. git commit -m "..."
8. git push origin member-3 ✅
```

### Scenario 3: Deleted Important Code

```
❌ Accidentally deleted code

If not committed yet:
1. git checkout -- filename  (Restore file)

If committed:
1. git log --oneline        (Find commit)
2. git checkout HASH filename  (Restore)

If pushed:
Contact team leader immediately! 🆘
```

---

## 🎯 Summary: Your Responsibilities

```
┌────────────────────────────────────────┐
│  YOUR Branch (member-X)                │
├────────────────────────────────────────┤
│  ✅ Work here daily                    │
│  ✅ Push changes regularly             │
│  ✅ Sync with develop                  │
│  ✅ Test your code                     │
│  ✅ Write clear commits                │
│  ✅ Create PRs when ready              │
└────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  DON'T Touch                           │
├────────────────────────────────────────┤
│  ❌ main branch                        │
│  ❌ Other members' branches            │
│  ❌ Force push anywhere                │
└────────────────────────────────────────┘
```

---

<div align="center">

## 📚 Keep This Diagram Handy!

**For questions, contact Team Leader**

**Built with ❤️ by Unity-Stack Team**

</div>
