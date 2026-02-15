# 🚀 Unity Shop - Team Development Guide

**Repository:** https://github.com/siddiquesakib/Unity-Shop  
**Team:** Unity-Stack  
**Team Leader:** Mohammad Siddique Sakib

---

## 📋 Table of Contents

1. [Initial Setup](#initial-setup)
2. [Daily Workflow](#daily-workflow)
3. [Branch Management](#branch-management)
4. [Commit Conventions](#commit-conventions)
5. [Code Review Process](#code-review-process)
6. [Do's and Don'ts](#dos-and-donts)
7. [Common Commands](#common-commands)
8. [Troubleshooting](#troubleshooting)
9. [Emergency Procedures](#emergency-procedures)

---

## 🎯 Initial Setup (First Time Only)

### Step 1: Install Prerequisites

```bash
# Check Node.js version (should be 18+)
node --version

# Check npm version
npm --version

# Check Git version
git --version
```

### Step 2: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/siddiquesakib/Unity-Shop.git

# Navigate to project directory
cd Unity-Shop

# Verify remote
git remote -v
```

### Step 3: Install Dependencies

```bash
# Install all project dependencies
npm install

# Or if using yarn
yarn install
```

### Step 4: Set Up Environment Variables

```bash
# Copy the example environment file
cp .env.example .env.local

# Open and configure your local environment
# Use your preferred editor (VS Code, Nano, Vim, etc.)
code .env.local
```

**Required Environment Variables:**
```env
DATABASE_URL="your_database_connection_string"
NEXTAUTH_SECRET="your_secret_key_here"
NEXTAUTH_URL="http://localhost:3000"
NEXT_PUBLIC_API_URL="http://localhost:3000/api"

# Add other project-specific variables
```

### Step 5: Database Setup

```bash
# Run database migrations
npx prisma migrate dev

# Generate Prisma Client
npx prisma generate

# (Optional) Seed database with sample data
npm run seed
```

### Step 6: Verify Installation

```bash
# Start development server
npm run dev

# Open browser and check
# http://localhost:3000
```

---

## 📅 Daily Workflow

### Starting Your Work Day

```bash
# 1. Navigate to project directory
cd Unity-Shop

# 2. Make sure you're on the main branch
git checkout main

# 3. Pull the latest changes
git pull origin main

# 4. Check current status
git status

# 5. Create a new branch for your work
git checkout -b feature/your-feature-name
```

### During Development

```bash
# Check what files you've modified
git status

# See detailed changes
git diff

# Stage specific files
git add path/to/file.js

# Or stage all changes (use carefully!)
git add .

# Commit your changes
git commit -m "feat: add user authentication module"

# Push your branch to remote
git push origin feature/your-feature-name
```

### Before Ending Your Day

```bash
# 1. Make sure all changes are committed
git status

# 2. Push your latest work
git push origin feature/your-feature-name

# 3. Update your local main branch
git checkout main
git pull origin main

# 4. Go back to your feature branch
git checkout feature/your-feature-name
```

---

## 🌿 Branch Management

### Branch Naming Convention

```bash
# Feature branches
git checkout -b feature/shopping-cart
git checkout -b feature/user-authentication

# Bug fix branches
git checkout -b fix/cart-calculation-error
git checkout -b fix/login-validation

# Hotfix branches (urgent production fixes)
git checkout -b hotfix/payment-gateway-crash

# Improvement branches
git checkout -b improve/dashboard-performance
git checkout -b improve/loading-speed

# Documentation branches
git checkout -b docs/update-readme
git checkout -b docs/api-documentation
```

### Branch Structure

```
main (production-ready code)
├── develop (integration branch)
│   ├── feature/shopping-cart
│   ├── feature/seller-dashboard
│   └── feature/analytics
└── hotfix/critical-bug
```

### Creating a New Branch

```bash
# Always create from the latest main
git checkout main
git pull origin main
git checkout -b feature/your-feature-name
```

### Merging Branches

```bash
# Update your feature branch with latest main
git checkout feature/your-feature-name
git pull origin main

# If there are conflicts, resolve them, then:
git add .
git commit -m "fix: resolve merge conflicts"

# Push updated branch
git push origin feature/your-feature-name
```

### Deleting Branches

```bash
# Delete local branch (after merge)
git branch -d feature/your-feature-name

# Force delete (if not merged)
git branch -D feature/your-feature-name

# Delete remote branch
git push origin --delete feature/your-feature-name
```

---

## 📝 Commit Conventions

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Commit Types

| Type | Description | Example |
|------|-------------|---------|
| `feat` | New feature | `feat: add product filter functionality` |
| `fix` | Bug fix | `fix: resolve cart total calculation error` |
| `docs` | Documentation | `docs: update API documentation` |
| `style` | Code style (formatting) | `style: format code with prettier` |
| `refactor` | Code refactoring | `refactor: optimize database queries` |
| `test` | Adding tests | `test: add unit tests for cart module` |
| `chore` | Maintenance tasks | `chore: update dependencies` |
| `perf` | Performance improvement | `perf: optimize image loading` |

### Good Commit Examples

```bash
# ✅ Good commits
git commit -m "feat: add seller registration form"
git commit -m "fix: resolve checkout payment validation bug"
git commit -m "docs: update installation instructions"
git commit -m "refactor: improve product search algorithm"
git commit -m "perf: optimize database queries for dashboard"

# ❌ Bad commits
git commit -m "update"
git commit -m "fix bug"
git commit -m "changes"
git commit -m "asdfasdf"
git commit -m "final version"
```

### Detailed Commit Example

```bash
git commit -m "feat(auth): implement JWT authentication system

- Add JWT token generation and validation
- Create secure authentication middleware
- Implement refresh token mechanism
- Add password hashing with bcrypt

Closes #123"
```

---

## 👀 Code Review Process

### Creating a Pull Request

```bash
# 1. Push your branch
git push origin feature/your-feature-name

# 2. Go to GitHub repository
# 3. Click "Compare & pull request"
# 4. Fill in the PR template
```

### Pull Request Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Manual testing completed
- [ ] No console errors

## Screenshots (if applicable)
Add screenshots here

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
```

### Reviewing Pull Requests

```bash
# 1. Fetch the PR branch
git fetch origin pull/ID/head:BRANCH_NAME

# 2. Checkout the branch
git checkout BRANCH_NAME

# 3. Test the changes
npm run dev

# 4. Leave review on GitHub
```

---

## ✅ Do's and Don'ts

### ✅ DO's

#### Git Best Practices

```bash
# ✅ Pull before starting work
git pull origin main

# ✅ Commit frequently with clear messages
git commit -m "feat: add product search feature"

# ✅ Push your work daily
git push origin feature/your-feature-name

# ✅ Create feature branches for each task
git checkout -b feature/task-name

# ✅ Keep commits small and focused
git add specific-file.js
git commit -m "fix: resolve validation error in login form"

# ✅ Update your branch regularly
git pull origin main

# ✅ Review your changes before committing
git diff
```

#### Code Best Practices

```bash
# ✅ Run tests before committing
npm run test

# ✅ Lint your code
npm run lint

# ✅ Format code
npm run format

# ✅ Check for TypeScript errors
npm run type-check

# ✅ Test locally before pushing
npm run dev
```

### ❌ DON'Ts

#### Critical Mistakes to Avoid

```bash
# ❌ NEVER commit to main directly
# BAD:
git checkout main
git commit -m "changes"
git push origin main

# ❌ NEVER force push to main
# BAD:
git push -f origin main

# ❌ NEVER commit sensitive data
# BAD:
git add .env
git add .env.local
git add config/secrets.js

# ❌ NEVER commit node_modules
# BAD:
git add node_modules/

# ❌ NEVER use generic commit messages
# BAD:
git commit -m "update"
git commit -m "fix"
git commit -m "changes"

# ❌ NEVER delete other people's work
# BAD:
git push -f origin feature/someone-else-branch

# ❌ NEVER work without pulling first
# BAD:
# Start work without: git pull origin main
```

#### Files to NEVER Commit

```bash
# These should be in .gitignore
.env
.env.local
.env.production
node_modules/
.next/
dist/
build/
*.log
.DS_Store
.vscode/
.idea/
```

---

## 🛠️ Common Commands Reference

### Essential Daily Commands

```bash
# Check status
git status

# View commit history
git log --oneline

# View recent commits (last 5)
git log -5

# See changes
git diff

# See staged changes
git diff --staged

# Discard local changes (be careful!)
git checkout -- filename.js

# Unstage file
git reset HEAD filename.js
```

### Branch Commands

```bash
# List all branches
git branch -a

# Switch branch
git checkout branch-name

# Create and switch to new branch
git checkout -b new-branch-name

# Delete local branch
git branch -d branch-name

# Rename current branch
git branch -m new-branch-name
```

### Remote Commands

```bash
# View remotes
git remote -v

# Fetch all remote branches
git fetch origin

# Pull latest changes
git pull origin main

# Push branch
git push origin branch-name

# Push and set upstream
git push -u origin branch-name
```

### Stashing Commands

```bash
# Save work temporarily
git stash

# Save with message
git stash save "work in progress on feature X"

# List stashes
git stash list

# Apply latest stash
git stash apply

# Apply specific stash
git stash apply stash@{0}

# Apply and remove stash
git stash pop

# Delete stash
git stash drop stash@{0}
```

### Undoing Changes

```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Undo specific commit
git revert commit-hash

# Amend last commit message
git commit --amend -m "new message"

# Add forgotten file to last commit
git add forgotten-file.js
git commit --amend --no-edit
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

# Run tests in watch mode
npm test -- --watch

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

# Open Prisma Studio
npx prisma studio

# Reset database (CAUTION!)
npx prisma migrate reset

# Seed database
npm run seed
```

---

## 🚨 Troubleshooting

### Problem: Merge Conflicts

```bash
# 1. Identify conflicting files
git status

# 2. Open files and resolve conflicts manually
# Look for markers: <<<<<<<, =======, >>>>>>>

# 3. After resolving, stage files
git add resolved-file.js

# 4. Complete the merge
git commit -m "fix: resolve merge conflicts"

# 5. Push changes
git push origin your-branch-name
```

### Problem: Accidentally Committed to Wrong Branch

```bash
# 1. Save commit hash
git log -1

# 2. Undo commit (keep changes)
git reset --soft HEAD~1

# 3. Stash changes
git stash

# 4. Switch to correct branch
git checkout correct-branch

# 5. Apply changes
git stash pop

# 6. Commit to correct branch
git add .
git commit -m "your message"
```

### Problem: Need to Discard All Local Changes

```bash
# WARNING: This will delete all uncommitted changes!

# Discard all changes
git reset --hard HEAD

# Remove untracked files
git clean -fd

# Pull latest
git pull origin main
```

### Problem: Accidentally Deleted Files

```bash
# Restore specific file
git checkout HEAD -- path/to/file.js

# Restore all deleted files
git checkout HEAD -- .
```

### Problem: Wrong Commit Message

```bash
# Change last commit message
git commit --amend -m "corrected message"

# If already pushed (use carefully!)
git push --force-with-lease origin your-branch-name
```

### Problem: node_modules Issues

```bash
# 1. Delete node_modules
rm -rf node_modules

# 2. Delete package-lock.json
rm package-lock.json

# 3. Clear npm cache
npm cache clean --force

# 4. Reinstall
npm install
```

### Problem: Port Already in Use

```bash
# Find process using port 3000
lsof -i :3000

# Kill the process
kill -9 PID

# Or use different port
PORT=3001 npm run dev
```

---

## 🆘 Emergency Procedures

### Emergency: Pushed Sensitive Data

```bash
# 1. Remove from latest commit
git rm --cached .env
git commit -m "chore: remove sensitive file"
git push origin branch-name

# 2. Rotate all exposed credentials IMMEDIATELY
# - Change database passwords
# - Regenerate API keys
# - Update JWT secrets
# - Contact team leader

# 3. For older commits, contact team leader
# May need to use git filter-branch or BFG Repo-Cleaner
```

### Emergency: Broke the Main Branch

```bash
# Contact team leader immediately!
# Don't try to fix it yourself

# Meanwhile, continue work on feature branch
git checkout -b emergency-fix/your-fix
```

### Emergency: Lost Work

```bash
# Check reflog
git reflog

# Find your lost commit
# Look for: HEAD@{X}: commit: your message

# Restore it
git checkout HEAD@{X}

# Create recovery branch
git checkout -b recovery-branch
```

---

## 📞 Getting Help

### Before Asking for Help

1. ✅ Read error messages carefully
2. ✅ Check this guide
3. ✅ Search on Google/Stack Overflow
4. ✅ Try `git status` to understand current state

### When Asking for Help

Provide:
- Exact error message
- Commands you ran
- Current branch: `git branch`
- Current status: `git status`
- Recent commits: `git log -3`

### Contact

**Team Leader:** Mohammad Siddique Sakib  
**Communication:** [Your team communication channel]

---

## 📚 Additional Resources

### Documentation Links

- [Git Documentation](https://git-scm.com/doc)
- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev/)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

### Useful Git Commands Cheatsheet

```bash
# Quick reference for most common commands

# Start work
git pull origin main
git checkout -b feature/my-feature

# Save work
git add .
git commit -m "feat: description"
git push origin feature/my-feature

# Update branch
git pull origin main

# Create PR on GitHub
# Review, test, merge

# Clean up
git checkout main
git pull origin main
git branch -d feature/my-feature
```

---

## ✨ Team Workflow Summary

### Perfect Day Workflow

```bash
# Morning
cd Unity-Shop
git checkout main
git pull origin main
git checkout -b feature/todays-task

# Development
# ... write code ...
npm run dev  # test locally
npm run lint  # check code quality

# Commit work
git add .
git commit -m "feat: implement feature X"
git push origin feature/todays-task

# Create PR on GitHub
# Get review
# Merge after approval

# Evening cleanup
git checkout main
git pull origin main
git branch -d feature/todays-task
```

---

## 🎯 Key Principles

1. **Never commit directly to main**
2. **Always pull before starting work**
3. **Write clear commit messages**
4. **Test before committing**
5. **Push work daily**
6. **Ask for help when stuck**
7. **Review your own code before PR**
8. **Respect team members' work**
9. **Keep branches small and focused**
10. **Communicate with the team**

---

<div align="center">

## 🚀 Happy Coding!

**Remember:** When in doubt, ask the team leader!

**Built with ❤️ by Unity-Stack Team**

</div>
