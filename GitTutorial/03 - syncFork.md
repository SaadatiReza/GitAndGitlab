# syncFork

A command or process to synchronize your forked repository with the original (upstream) repository to keep your copy updated.

### Typical Usage

```bash
git remote add upstream https://github.com/original-owner/repo.git
git fetch upstream
git checkout main
git merge upstream/main
```
# Pull and Merge Request
Pull Request (PR) is a method of submitting contributions to a project. You create a PR to propose changes you've made in a fork or branch.

Steps to Create a PR
* Fork the repository or create a feature branch.

* Push your commits to your fork or branch.

* Open a pull request on GitHub/GitLab/Bitbucket to merge your branch into the main repository.

# Git Rebase
git rebase is similar to merging, but instead of creating a new merge commit, it reapplies commits on top of another base commit. This results in a linear history.

## Key Differences from Merge
* **Merge** retains history and shows a diverging/converging tree.

* **Rebase** rewrites history as if the work was done on top of the target branch.

## NOTE:
After executing the rebase command, you should run the merge command only if necessary, such as when rebasing a feature branch and then integrating it into the main branch.
```bash
git rebase -i HEAD~3
```
This opens an editor where you can choose to pick, squash, or reword each commit.

## Advanced Rebase
Use interactive mode to clean up commit history before merging or submitting a PR.
```bash
git rebase -i origin/main
```
# squash
Squashing combines multiple commits into a single commit.
```bash
pick e3a1b35 Add user login
squash 7ac9a67 Fix typo in login logic
squash 51b1ab2 Refactor login validation
```

# Cherry-pick
Apply a specific commit from one branch onto another branch.
```bash
git checkout main
git cherry-pick <commit-hash>
```
Useful when you want to copy a specific fix or feature without merging the entire branch.

# squash merge
Perform a squash during merge to combine all changes into a single commit.
```bash
git merge --squash feature-branch
git commit -m "Merged feature-branch with squash"
```
This keeps history clean with one commit for the whole feature.

# git stash
Temporarily shelves (or stashes) changes you've made to your working directory.
```bash
git stash            # Save current changes
git stash list       # List all stashes
git stash apply      # Apply the latest stash (keeps stash)
git stash pop        # Apply and remove the latest stash
git stash drop       # Remove a specific stash
```
Useful for cleaning your workspace or switching branches without committing unfinished work.

