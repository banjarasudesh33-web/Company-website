# Git Workflow Guide - Advanced Git Commands

This guide demonstrates how to use advanced Git commands in your development workflow for the Lalasa Private Ltd website project.

## 📚 Table of Contents
1. [git stash](#git-stash) - Temporary work suspension
2. [git cherry-pick](#git-cherry-pick) - Apply specific commits
3. [git revert](#git-revert) - Safe undo operations
4. [git reset](#git-reset) - Destructive operations (local only)
5. [Practical Workflows](#practical-workflows)

---

## 🚛 git stash

**Purpose:** Temporarily save uncommitted changes without committing them.

### When to Use
- Switching branches without committing incomplete work
- Pulling updates from remote without conflicts
- Experimenting with different approaches
- Saving work before urgent bug fixes

### Basic Commands

```bash
# Stash current changes
git stash

# Stash with a descriptive message
git stash save "WIP: implementing contact form validation"

# List all stashes
git stash list

# Show what's in a stash
git stash show stash@{0}

# Show detailed diff of stash
git stash show -p stash@{0}

# Apply the most recent stash (keeps it)
git stash apply

# Apply specific stash (keeps it)
git stash apply stash@{2}

# Pop stash (apply and remove)
git stash pop

# Delete a stash
git stash drop stash@{1}

# Delete all stashes
git stash clear

# Stash only unstaged changes
git stash --keep-index

# Stash untracked files too
git stash -u

# Stash with partial content
git stash --patch
```

### Real-World Example

```bash
# You're working on feature branch and need to check something on main
git status
# On branch feature/contact-form
# Modified: index.html
# Modified: src/css/styles.css

# Save your work
git stash save "WIP: contact form styling"

# Switch to main
git checkout main

# Pull latest changes
git pull origin main

# Switch back to your feature
git checkout feature/contact-form

# Get your work back
git stash pop

# Continue working
```

### Stash Best Practices

```bash
# Always use descriptive messages
git stash save "WIP: responsive navbar adjustments"

# Don't stash for days - commit instead
git stash save "temporary..." # ❌ Unclear

# Clean up old stashes regularly
git stash list
git stash drop stash@{5}

# Use stash names for reference
git stash save "bugfix/email-validation: client-side checks"
```

---

## 🎯 git cherry-pick

**Purpose:** Apply specific commits from one branch to another.

### When to Use
- Backporting bugfixes to older versions
- Selectively applying commits from feature branches
- Moving specific changes between branches
- Applying commits from pull requests

### Basic Commands

```bash
# Cherry-pick a single commit
git cherry-pick abc1234

# Cherry-pick with specific commit message
git cherry-pick --edit abc1234

# Cherry-pick multiple commits
git cherry-pick abc1234 def5678 ghi9012

# Cherry-pick range (inclusive)
git cherry-pick abc1234^..def5678

# Cherry-pick without committing (stage only)
git cherry-pick --no-commit abc1234

# Continue after resolving conflicts
git cherry-pick --continue

# Skip problematic commit during cherry-pick
git cherry-pick --skip

# Abort entire cherry-pick
git cherry-pick --abort
```

### Real-World Example

**Scenario: Critical bugfix in develop needs to be in main immediately**

```bash
# Developer finds bug and commits fix on develop
# Commit hash: abc1234 - "fix: resolve form submission bug"

# Switch to main (production branch)
git checkout main

# Pull latest main code
git pull origin main

# Cherry-pick the bugfix
git cherry-pick abc1234

# If conflicts occur, resolve them:
# 1. Edit the conflicted files
# 2. Stage the resolved files
git add index.html

# Continue cherry-pick
git cherry-pick --continue

# If conflicts are too complex
git cherry-pick --abort

# Push the fix to production
git push origin main

# Deployment automatically happens via CI/CD
```

### Cherry-Pick with Conflicts

```bash
# Start cherry-pick
git cherry-pick abc1234

# Git shows conflicts:
# CONFLICT (content): Merge conflict in index.html

# Edit the conflicted file and resolve
# Look for conflict markers:
<<<<<<< HEAD
  <!-- Your current main branch code -->
=======
  <!-- Code being cherry-picked -->
>>>>>>> abc1234

# After resolving conflicts
git add index.html
git cherry-pick --continue

# Or abort if needed
git cherry-pick --abort
```

### Cherry-Pick Best Practices

```bash
# Use full commit hashes for clarity
git cherry-pick abc123456789  # ✓ Full hash
git cherry-pick abc1234       # ? Short, may be ambiguous

# Cherry-pick without automatic commit first
git cherry-pick --no-commit abc1234
git add .
git commit -m "feat: applied critical fix from develop"

# Verify before cherry-picking
git log --oneline develop | head -10

# After cherry-picking, verify changes
git show HEAD
```

---

## ⏮️ git revert

**Purpose:** Create new commits that undo previous changes (safe for shared branches).

### When to Use
- Undoing mistakes on public/shared branches
- Safe history preservation for collaboration
- Audit trail of changes and reversals
- When team can't force-push

### Basic Commands

```bash
# Revert a single commit
git revert abc1234

# Revert without editing message
git revert --no-edit abc1234

# Revert last commit
git revert HEAD

# Revert multiple commits (creates multiple revert commits)
git revert abc1234 def5678

# Revert range of commits
git revert abc1234^..def5678

# Revert and edit commit message
git revert abc1234 --edit

# Revert without committing (stage changes first)
git revert -n abc1234

# Continue after resolving revert conflicts
git revert --continue

# Skip a problematic revert
git revert --skip

# Abort revert operation
git revert --abort
```

### Real-World Example

**Scenario: Buggy feature was merged to main and needs to be undone**

```bash
# View recent commits
git log --oneline -10
# Output:
# abc1234 - Add new payment feature (BAD - has bugs)
# def5678 - Fixed typo in header
# ghi9012 - Merged PR: new services section

# Safely revert the buggy commit
git revert abc1234

# Git creates a new "revert commit"
# Commit message: "Revert 'Add new payment feature'"

# The history looks like:
# ➜ Revert "Add new payment feature" (new commit)
# ➜ Add new payment feature (original - still in history)
# ➜ Fixed typo in header
# ➜ Merged PR: new services section

# Push the revert
git push origin main

# The bug is reverted, but full history is preserved
# Team can see what was reverted and why
```

### Revert Multiple Commits

```bash
# Multiple commits to revert
git log --oneline
# abc1234 - Bad commit 3
# def5678 - Bad commit 2
# ghi9012 - Bad commit 1
# jkl3456 - Good state before

# Revert all three (creates 3 new commits)
git revert abc1234 def5678 ghi9012

# Or revert range
git revert ghi9012^..abc1234

# Or revert without committing each
git revert -n abc1234 def5678 ghi9012
git add .
git commit -m "revert: remove problematic feature set"
```

### Revert vs Reset

```bash
# ✓ Use revert for shared/public branches
git revert abc1234  # Creates new "revert" commit

# ❌ Never reset public commits
git reset --hard abc1234  # Only for local branches!

# History comparison:
# REVERT (safe for team):
# ➜ Revert commit X
# ➜ Commit X (still there)
# ➜ Previous commit

# RESET (unsafe for team):
# ➜ Commit X (REMOVED from history)
# ➜ Previous commit
# (Team's history broken!)
```

---

## 🔄 git reset

**Purpose:** Move HEAD pointer and optionally discard commits/changes.

⚠️ **WARNING:** Use only on local branches! Never on shared/public branches!

### Three Reset Modes

#### 1. Soft Reset (`--soft`)
Keeps changes in staging area.

```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Scenario: Committed too early
git log --oneline
# abc1234 - Added form validation
# def5678 - Previous work

# Undo the commit but keep changes
git reset --soft HEAD~1

# Now you can:
git status
# Changes to be committed:
#   - form validation code

# Make additional changes
echo "more code" >> index.html

# Recommit with full changes
git add .
git commit -m "feat: add comprehensive form validation with error handling"
```

#### 2. Mixed Reset (`--mixed`) - Default
Keeps changes in working directory (unstaged).

```bash
# Undo last commit and unstage changes (DEFAULT)
git reset HEAD~1
# Same as: git reset --mixed HEAD~1

# Scenario: Need to reorganize commits
git log --oneline
# abc1234 - Changed forms and styling
# def5678 - Previous work

# Undo and unstage everything
git reset HEAD~1

# Check status
git status
# Changes not staged for commit:
#   modified: forms.js
#   modified: styles.css

# Stage selectively
git add forms.js
git commit -m "feat: enhance form validation"

git add styles.css
git commit -m "style: improve form styling"

# Now history is organized better
```

#### 3. Hard Reset (`--hard`)
Discards all changes. **Use with extreme caution!**

```bash
# Completely undo last commit and discard changes
git reset --hard HEAD~1

# Reset to specific commit
git reset --hard abc1234

# Reset to remote version (discard all local)
git reset --hard origin/main

# ❌ Dangerous - data loss!
git reset --hard HEAD~5  # Discards last 5 commits!
```

### Real-World Examples

**Example 1: Fix recent local commits**

```bash
# You made commits locally but want to redo them
git log --oneline
# abc1234 - WIP: form stuff
# def5678 - WIP: styles
# ghi9012 - Previous good commit

# Undo last 2 commits but keep changes
git reset --soft HEAD~2

# All changes are staged and ready to recommit
git status
# Changes to be committed:
#   modified: index.html
#   modified: css/styles.css

# Create one clean commit
git reset HEAD  # Unstage everything

# Organize and commit properly
git add index.html
git commit -m "feat: add form validation"

git add css/styles.css
git commit -m "style: improve form appearance"
```

**Example 2: Undo staging specific files**

```bash
# You staged files accidentally
git add forms.js database.js config.js

git status
# Changes to be committed:
#   modified: forms.js
#   modified: database.js
#   modified: config.js

# Unstage only config.js
git reset HEAD config.js

# Now only forms.js and database.js are staged
```

**Example 3: Recovery after wrong reset**

```bash
# Oh no! You did hard reset and lost commits!
git reset --hard HEAD~3

# Don't panic! Git keeps a record in reflog
git reflog

# Output shows:
# abc1234 HEAD@{0}: reset: moving to HEAD~3
# def5678 HEAD@{1}: commit: my important work
# ghi9012 HEAD@{2}: commit: previous work

# Recover the lost commit
git reset --hard def5678

# Your commits are back!
```

### Reset Safety Tips

```bash
# Always backup before hard reset
git branch backup-branch

# Use reflog to see all actions
git reflog

# Verify before resetting
git log --oneline -5

# Only reset local commits
git log --oneline
git log --oneline origin/main

# Make sure remote has different commits
# Then it's safe to reset

# For team branches: NEVER hard reset
# Use revert instead
```

---

## 🔀 Practical Workflows

### Workflow 1: Feature Development

```bash
# 1. Create feature branch
git checkout -b feature/contact-form-improvements

# 2. Work on feature (make commits)
git add .
git commit -m "feat: add email validation"
git add .
git commit -m "feat: add success message"

# 3. Need to fix something in main urgently
git stash save "WIP: contact form improvements"

# 4. Switch to main
git checkout main

# 5. Create bugfix branch
git checkout -b bugfix/critical-nav-issue

# 6. Make fix and commit
git add .
git commit -m "fix: resolve navigation menu toggle"

# 7. Push bugfix
git push origin bugfix/critical-nav-issue

# 8. Switch back to feature
git checkout feature/contact-form-improvements

# 9. Retrieve stashed work
git stash pop

# 10. Continue development
git add .
git commit -m "feat: add form submission feedback"

# 11. Push feature
git push origin feature/contact-form-improvements
```

### Workflow 2: Cherry-Pick Bugfix to Multiple Branches

```bash
# Bugfix committed on develop
git checkout develop
git log --oneline | head -3
# abc1234 - fix: resolve email validation bug
# def5678 - Previous commit
# ...

# Apply to main (production)
git checkout main
git cherry-pick abc1234
git push origin main

# Apply to v1.2-stable branch
git checkout v1.2-stable
git cherry-pick abc1234
git push origin v1.2-stable

# Apply to v1.1-stable branch
git checkout v1.1-stable
git cherry-pick abc1234
git push origin v1.1-stable

# Bugfix is now in all branches
```

### Workflow 3: Organizing Messy Commits

```bash
# You have messy work history
git log --oneline
# abc1234 - WIP: styling
# def5678 - form stuff
# ghi9012 - WIP: validation
# jkl3456 - Good commit

# Clean it up
git reset --soft jkl3456

# All changes are staged
git status
# Changes to be committed:
#   modified: index.html
#   modified: css/styles.css
#   ...

# Create organized commits
git reset HEAD *

# Stage and commit each component
git add css/
git commit -m "style: improve form styling"

git add js/validation.js
git commit -m "feat: add form validation"

git add index.html
git commit -m "feat: implement contact form"

# Now history is clean!
```

### Workflow 4: Undoing Bad Merge

```bash
# Bad merge happened on main
git log --oneline
# abc1234 - Merge branch 'bad-feature' (BAD!)
# def5678 - Previous good state
# ...

# For public branch: use revert
git revert -m 1 abc1234

# This creates a "revert merge" commit
# History is preserved for team

# For local branch: use reset
git reset --hard def5678

# Push changes
git push origin main
```

---

## 📊 Command Comparison Table

| Task | Command | Safe for Team? | Reversible? |
|------|---------|----------------|-------------|
| Save work temporarily | `git stash` | ✅ Yes | ✅ Yes |
| Apply specific commit | `git cherry-pick` | ✅ Yes | ✅ Yes |
| Undo on shared branch | `git revert` | ✅ Yes | ✅ Yes |
| Undo soft locally | `git reset --soft` | ❌ No | ✅ Yes |
| Undo mixed locally | `git reset --mixed` | ❌ No | ✅ Yes |
| Discard changes | `git reset --hard` | ❌ No | ⚠️ Maybe |

---

## 🚨 Emergency Recovery

### Lost Commits?

```bash
# Check reflog
git reflog

# Find your commits
git log -p <commit>

# Recover
git reset --hard <commit>
```

### Wrong Revert?

```bash
# Revert the revert
git revert HEAD

# Or reset if not pushed
git reset --hard HEAD~1
```

### Accidentally Deleted Branch?

```bash
# Find it in reflog
git reflog

# Recreate the branch
git branch recover-branch <commit>
```

---

## ✅ Best Practices Summary

1. **Use stash for temporary work**
   ```bash
   git stash save "descriptive message"
   ```

2. **Cherry-pick for surgical changes**
   ```bash
   git cherry-pick commit-hash
   ```

3. **Revert for public branches**
   ```bash
   git revert commit-hash  # Creates new commit
   ```

4. **Reset only for local work**
   ```bash
   git reset --soft HEAD~1  # Safe, keeps changes
   ```

5. **Always communicate with team**
   - Stash is local
   - Cherry-pick affects shared history
   - Revert affects shared history
   - Reset breaks team workflows

---

## 📚 Additional Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub's Git Guide](https://docs.github.com/en/get-started/using-git)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Oh Shit, Git!?!](https://ohshitgit.com) - Emergency solutions

---

**Remember:** When in doubt, create a backup branch before trying anything risky!

```bash
git branch backup-$(date +%Y%m%d)
```

---

**Last Updated:** May 14, 2026
**Version:** 1.0.0
