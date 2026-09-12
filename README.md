# Git-GitHub-Day-6
Today I learned advanced Git and GitHub concepts related to collaboration, branching, code management, and repository administration.

1. Git Fork

A Fork creates a copy of another user's GitHub repository in your own GitHub account.

Fork vs Clone:

Fork: GitHub repository → another GitHub account
Clone: GitHub repository → local machine

Forking is useful when contributing to someone else's project without directly modifying their repository.

2. Pull Request (PR)

A Pull Request is used to propose changes to another repository or branch.

Typical workflow:

Fork the repository.
Modify the code in your fork.
Commit the changes.
Create a Pull Request.
Repository owner reviews the changes.
Owner can comment, merge, or close the PR.
3. Squash and Merge

Squash and Merge combines multiple commits into a single commit.

It is useful when a branch contains many small or work-in-progress commits and we want a clean commit history.

4. Rebase and Merge

Rebase and Merge keeps the individual commits while placing the branch changes on top of the target branch history.

5. Rename a Branch
git branch dev1branch
git branch -m dev1branch testbranch
git checkout testbranch

Push the branch:

git push origin testbranch
6. Git Revert

Git Revert creates a new commit that reverses the changes introduced by an earlier commit.

In GitHub, a Pull Request can also be reverted after it has been merged.

7. Git Clean

git clean removes untracked files.

Preview first:

git clean -n

Delete untracked files:

git clean -f
8. Cherry-Pick

Cherry-pick allows us to apply a specific commit from one branch to another.

git cherry-pick <commit-id>

This is useful when we need selected changes instead of merging an entire branch.

9. Git Tag

Tags are used to mark important points in Git history, such as releases.

git log --oneline
git tag tagname commitid

Example:

git tag dev/prod 0620179
10. .gitignore

.gitignore specifies files or folders that should not be tracked by Git.

Example:

vi .gitignore

Add:

file1.txt

Then check:

git status
11. Delete and Restore Branch

Delete a local branch:

git branch -D branchname

To recover a deleted branch, use:

git reflog
git checkout -b dev <commit-id>
Git Log vs Git Reflog
Git Log	Git Reflog
Shows reachable commit history	Shows movements of HEAD and references
Used to inspect project history	Useful for recovering lost commits
Mainly follows repository history	Records local reference movements
12. GitHub Pages

GitHub Pages can be used to host a website from a GitHub repository.

Basic workflow:

Create a repository.
Add index.html.
Go to Settings → Pages.
Select the required branch and folder.
Save and access the generated website URL.
13. Repository Visibility

A GitHub repository can be changed between:

Public
Private

This can be managed from:

Repository → Settings → Danger Zone → Change Visibility

14. Collaborators

To add developers to a repository:

Repository → Settings → Collaborators → Add people

15. GitHub Projects

GitHub Projects can be used for team task management.

Tasks can be created and assigned to team members with fields such as:

Task
Assignee
Start date
End date

Permissions can be managed through Project Settings → Manage Access.

16. Branching Strategy
Long-Living Branches
main
master
Short-Living Branches
feature/*
bugfix/*
Other temporary development branches
Key Takeaways

Today I learned how Git and GitHub support:

Collaborative development
Forking and Pull Requests
Code review
Branch management
Selective commit integration
Commit history management
Recovery from Git mistakes
Repository collaboration
Website hosting
Project and task management

Git + GitHub are essential foundations for modern DevOps workflows.
