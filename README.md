# Git & GitHub – Day 6

Today I learned advanced Git and GitHub concepts related to:

```text
Collaboration
Branching
Code Management
Commit Management
Repository Administration
Project Management
```

---

# 1. Git Fork

A **Fork** creates a copy of another user's GitHub repository under your own GitHub account.

### Fork

```text
Other User's GitHub Repository
            ↓
           Fork
            ↓
Your GitHub Repository
```

### Fork vs Clone

| Fork                                       | Clone                                 |
| ------------------------------------------ | ------------------------------------- |
| GitHub → GitHub                            | GitHub → Local Machine                |
| Creates a repository under your account    | Downloads repository to your computer |
| Mainly used for collaboration/contribution | Used for local development            |

### Fork Workflow

```text
Original Repository
        ↓
       Fork
        ↓
Your GitHub Repository
        ↓
      Clone
        ↓
Local Machine
```

Forking is commonly used when contributing to a repository that you do not directly own.

---

# 2. Pull Request

A **Pull Request (PR)** is used to propose changes to another branch or repository.

### Typical Workflow

```text
Fork Repository
       ↓
Clone Repository
       ↓
Create Branch
       ↓
Modify Code
       ↓
Commit Changes
       ↓
Push Changes
       ↓
Create Pull Request
       ↓
Code Review
       ↓
Merge / Close
```

The repository owner can:

```text
Review
Comment
Request Changes
Merge
Close
```

---

# 3. Squash and Merge

**Squash and Merge** combines multiple commits into a single commit before merging.

Example:

```text
Before:

Commit A
Commit B
Commit C
Commit D
     ↓
Squash
     ↓
Single Commit
```

### Why use Squash?

It can help create a cleaner commit history when a branch contains many small or work-in-progress commits.

Example:

```text
Feature Branch

Commit 1
Commit 2
Fix issue
Fix again
Update code
Final fix

        ↓
    Squash & Merge

        ↓

Feature completed
```

---

# 4. Rebase and Merge

**Rebase and Merge** places the branch commits on top of the updated target branch history while retaining the individual commits.

Conceptually:

```text
Before:

main
  A---B
       \
        C---D
         feature
```

After rebase:

```text
main
  A---B---C'---D'
```

The commits remain separate, but their commit IDs change because the commits are recreated on the new base.

---

# 5. Rename a Git Branch

Create a branch:

```bash
git branch dev1branch
```

Rename the branch:

```bash
git branch -m dev1branch testbranch
```

Switch to the renamed branch:

```bash
git checkout testbranch
```

Modern alternative:

```bash
git switch testbranch
```

Push the branch to GitHub:

```bash
git push origin testbranch
```

### Workflow

```text
dev1branch
     ↓
Rename
     ↓
testbranch
     ↓
Push
     ↓
GitHub
```

---

# 6. Git Revert

`git revert` creates a **new commit** that reverses the changes introduced by an earlier commit.

Example:

```bash
git revert <commit-id>
```

### Important Concept

Revert does not normally delete the previous commit.

Instead:

```text
Commit A
   ↓
Commit B
   ↓
Commit C
   ↓
Revert Commit C
   ↓
New Commit
```

This makes `git revert` useful when changes have already been shared with others.

---

# 7. Git Clean

`git clean` removes **untracked files** from the working directory.

### Preview files first

```bash
git clean -n
```

This shows what would be removed without actually deleting anything.

### Delete untracked files

```bash
git clean -f
```

### Workflow

```text
Untracked Files
      ↓
git clean -n
      ↓
Review
      ↓
git clean -f
      ↓
Files Removed
```

> Use `git clean` carefully because deleted untracked files are not restored by normal Git history.

---

# 8. Git Cherry-Pick

`git cherry-pick` allows us to apply a **specific commit** from one branch to another.

Command:

```bash
git cherry-pick <commit-id>
```

### Example

```text
Branch A

Commit A
Commit B
Commit C
```

Suppose we only need `Commit B`.

```text
Branch A
   |
   └── Commit B
           ↓
      cherry-pick
           ↓
Branch B
   |
   └── Commit B
```

### Use Case

Cherry-pick is useful when we need a selected change instead of merging the entire branch.

---

# 9. Git Tags

Git tags are used to mark important points in Git history.

They are commonly used for:

```text
Releases
Versions
Milestones
Production Versions
```

View commit history:

```bash
git log --oneline
```

Create a tag:

```bash
git tag tagname commitid
```

Example:

```bash
git tag dev/prod 0620179
```

View tags:

```bash
git tag
```

### Example

```text
Commit A
   ↓
Commit B
   ↓
Commit C
   ↓
v1.0
   ↓
Commit D
   ↓
Commit E
   ↓
v2.0
```

Tags help identify important versions of a project.

---

# 10. .gitignore

`.gitignore` specifies files and directories that Git should not track.

Create the file:

```bash
vi .gitignore
```

Add a file:

```text
file1.txt
```

Check the repository:

```bash
git status
```

### Example

```text
Project
│
├── app.java
├── README.md
├── password.txt
└── .gitignore
```

`.gitignore` can be configured to prevent files such as:

```text
Log files
Temporary files
Build output
Environment files
IDE files
Secrets
```

from being tracked.

> `.gitignore` does not remove a file that is already being tracked. If a file was previously committed, it must be removed from Git tracking separately.

---

# 11. Delete and Restore a Branch

## Delete Local Branch

```bash
git branch -D branchname
```

The `-D` option force-deletes the branch.

---

## Recover a Deleted Branch

Git's `reflog` can help locate commits that are no longer referenced by a branch.

View reflog:

```bash
git reflog
```

Find the required commit ID and create a new branch:

```bash
git checkout -b dev <commit-id>
```

Modern alternative:

```bash
git switch -c dev <commit-id>
```

### Recovery Flow

```text
Branch Deleted
      ↓
git reflog
      ↓
Find Commit
      ↓
Create New Branch
      ↓
Recovered Work
```

---

# 12. Git Log vs Git Reflog

| Git Log                                 | Git Reflog                                |
| --------------------------------------- | ----------------------------------------- |
| Shows commit history                    | Shows local reference movements           |
| Used to inspect project history         | Useful for recovery                       |
| Shows reachable commit history          | Records movements of HEAD and refs        |
| Useful for normal history investigation | Useful after accidental changes/deletions |

### Git Log

```bash
git log
```

### Git Reflog

```bash
git reflog
```

Simple difference:

```text
git log
   ↓
Project Commit History

git reflog
   ↓
Local HEAD / Reference History
```

---

# 13. GitHub Pages

**GitHub Pages** can be used to host websites from GitHub repositories.

### Basic Workflow

```text
Create Repository
       ↓
Add Website Files
       ↓
index.html
       ↓
Repository Settings
       ↓
Pages
       ↓
Select Branch / Folder
       ↓
Deploy
       ↓
Website URL
```

Example project:

```text
website/
│
├── index.html
├── style.css
└── script.js
```

GitHub Pages is useful for hosting static websites and documentation.

---

# 14. GitHub Repository Visibility

A GitHub repository can generally be configured as:

```text
Public
Private
```

### Change Visibility

Navigate to:

```text
Repository
    ↓
Settings
    ↓
Danger Zone
    ↓
Change Visibility
```

### Public Repository

The repository can be viewed publicly.

### Private Repository

Access is restricted to authorized users.

---

# 15. GitHub Collaborators

Collaborators can be given access to work on a repository.

Typical navigation:

```text
Repository
    ↓
Settings
    ↓
Collaborators
    ↓
Add People
```

Depending on the repository and organization settings, different permissions may be available.

---

# 16. GitHub Projects

**GitHub Projects** can be used for task and project management.

Projects can help teams organize work using:

```text
Tasks
Issues
Assignees
Dates
Status
Priorities
```

Example:

| Task      | Assignee    | Status      |
| --------- | ----------- | ----------- |
| Create UI | Developer 1 | In Progress |
| Fix Bug   | Developer 2 | Todo        |
| Testing   | QA          | Done        |

Access and permissions can be managed through the relevant project settings.

---

# 17. Branching Strategy

A project can use different types of branches depending on the team's workflow.

## Long-Lived Branches

Examples:

```text
main
master
```

These branches generally represent stable or important development lines.

---

## Short-Lived Branches

Examples:

```text
feature/*
bugfix/*
hotfix/*
```

These branches are generally created for specific tasks and merged after the work is completed.

---

# 18. Branching Example

```text
                  main
                   |
          ┌────────┴────────┐
          ↓                 ↓
     feature/login      feature/payment
          |                 |
       Development       Development
          |                 |
          └────────┬────────┘
                   ↓
              Pull Request
                   ↓
                 Review
                   ↓
                 Merge
                   ↓
                  main
```

---

# 19. Git Advanced Workflow

The concepts learned today can work together:

```text
GitHub Repository
        ↓
       Fork
        ↓
       Clone
        ↓
 Create Feature Branch
        ↓
    Make Changes
        ↓
      Commit
        ↓
       Push
        ↓
 Pull Request
        ↓
     Review
        ↓
Squash / Rebase / Merge
        ↓
       main
        ↓
       Tag
        ↓
      Release
```

---

# 20. Git Recovery Concepts

Git provides several commands for handling mistakes.

```text
Mistake
   |
   ├── Undo shared commit
   │       ↓
   │    git revert
   │
   ├── Recover deleted branch
   │       ↓
   │    git reflog
   │
   ├── Remove untracked files
   │       ↓
   │    git clean
   │
   └── Apply selected commit
           ↓
       git cherry-pick
```

---

# 21. Important Commands

| Command           | Purpose                               |
| ----------------- | ------------------------------------- |
| `git branch`      | List branches                         |
| `git branch -m`   | Rename branch                         |
| `git branch -D`   | Force delete branch                   |
| `git switch`      | Switch branches                       |
| `git merge`       | Merge branches                        |
| `git rebase`      | Reapply commits on another base       |
| `git revert`      | Create a commit that reverses changes |
| `git clean -n`    | Preview untracked files for removal   |
| `git clean -f`    | Remove untracked files                |
| `git cherry-pick` | Apply a specific commit               |
| `git tag`         | Create/list tags                      |
| `git log`         | View commit history                   |
| `git reflog`      | View local reference movements        |
| `git push`        | Upload commits                        |
| `git pull`        | Retrieve and integrate changes        |

---

# 22. GitHub Administration Concepts

Today I also learned basic GitHub repository administration:

```text
Repository Visibility
       ↓
Collaborators
       ↓
Permissions
       ↓
GitHub Projects
       ↓
GitHub Pages
       ↓
Branch Management
```

These features help manage repositories beyond simply storing source code.

---

# 23. Key Takeaways

Today I learned about:

```text
✓ Git Fork
✓ Pull Requests
✓ Squash and Merge
✓ Rebase and Merge
✓ Branch Renaming
✓ Git Revert
✓ Git Clean
✓ Git Cherry-Pick
✓ Git Tags
✓ .gitignore
✓ Branch Recovery
✓ Git Log
✓ Git Reflog
✓ GitHub Pages
✓ Repository Visibility
✓ GitHub Collaborators
✓ GitHub Projects
✓ Branching Strategies
```

---

# 24. What I Learned

The main focus of today's learning was **advanced Git and GitHub collaboration**.

I learned how developers can:

```text
Collaborate
    ↓
Create Branches
    ↓
Make Changes
    ↓
Review Code
    ↓
Merge Changes
    ↓
Manage Versions
    ↓
Recover From Mistakes
```

---

# 25. Git + GitHub in DevOps

Git and GitHub are important foundations for DevOps workflows.

A typical workflow can look like:

```text
Developer
    ↓
Git
    ↓
GitHub
    ↓
Pull Request
    ↓
Code Review
    ↓
Merge
    ↓
CI/CD
    ↓
Build
    ↓
Test
    ↓
Deploy
```

---

# 26. Final Learning Summary

The main concepts I practiced today were:

```text
Fork
  ↓
Branch
  ↓
Commit
  ↓
Push
  ↓
Pull Request
  ↓
Review
  ↓
Merge
  ↓
Tag
  ↓
Release
```

Git provides the version-control capabilities, while GitHub provides repository hosting, collaboration, code review, project management, and other development features.

**Day 6 Complete → Learn → Practice → Troubleshoot → Improve 🚀**
