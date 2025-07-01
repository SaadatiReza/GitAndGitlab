# How to Create a simple Git project
You could create a repository in two main ways
* Create a directory then switch to the new directory then execute the below command
```bash
git init
```
* You could automatically create and initiate git repository at the same time with the below command.
```bash
git init "the name of the repo"
```

# File  Lifecycle

There are 4 different state for each file in git.
* Untracked
* Unmodified
* Modified
* Staged


# Git configurations can be set at three levels
* system --> For running Operation System
* global --> For a certain User
* local --> For a specified Repository

You can check the set config in operating system with the below command
``` 
git config --list
```
You can set the credential for user in global wide with the below command
```
git config --global user.name ""
git config --global user.email ""
```
you could set this configuration at local level
```
git config --local user.name ""
git config --local user.email ""
```

keep in mind that when you set the configuration in local level this configuration will be kept in **.git** directory,however, when it comes to global level, this configuration will be placed in **$HOME/.gitconfig**



# Git Working Directory and Git Bare
The Git working directory (or working tree) is where you actively work on your files—it's a checked-out copy of one version of the project, with a .git directory inside it that stores the repository’s history and metadata. In contrast, a bare Git repository has no working directory and only contains the contents of the .git directory; it's typically used on remote servers as a central repo for collaboration, because you can’t edit files or run builds directly in it. The key difference is: the working directory is for active development, while a bare repository is for sharing and syncing code.

#### How to create a bare repository
```bash
git init --bare ""
```

# Git detach Head

A git detached HEAD state occurs when you check out a specific commit (or tag) directly instead of a branch. In this state, Git’s HEAD points to a commit rather than a branch, meaning you are no longer working on a named branch. Any changes you make or new commits you create in this state won't belong to any branch, and they can be lost if you switch branches unless you explicitly create a new branch from that point. It's useful for inspecting past versions or experimenting without affecting the current branches.

# Content of .git directory
| Name             | Type      | Description                                                                                        |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------- |
| `HEAD`           | File      | Points to the current branch (e.g., `ref: refs/heads/main`).                                       |
| `config`         | File      | Repository-specific Git configuration (similar to global `.gitconfig`).                            |
| `description`    | File      | Description used by GitWeb; mostly irrelevant for general Git usage.                               |
| `index`          | File      | The staging area; tracks what will be included in the next commit.                                 |
| `hooks/`         | Directory | Contains sample client-side hook scripts that run on Git actions (e.g., `pre-commit`, `pre-push`). |
| `info/`          | Directory | Includes auxiliary information, like excluded file patterns in `exclude`.                          |
| `objects/`       | Directory | Contains all content (commits, trees, blobs, tags) in Git’s internal storage format.               |
| `refs/`          | Directory | Contains references (branches, tags, remotes).                                                     |
| `logs/`          | Directory | History of updates to branch references (useful for recovery with `reflog`).                       |
| `branches/`      | Directory | Obsolete feature; rarely used in modern Git.                                                       |
| `packed-refs`    | File      | A flat file storing refs for performance when many refs exist.                                     |
| `FETCH_HEAD`     | File      | Records the branch heads fetched from a remote.                                                    |
| `ORIG_HEAD`      | File      | Stores the previous `HEAD`, used to undo complex operations like merges.                           |
| `MERGE_HEAD`     | File      | Temporarily holds commit(s) being merged. Deleted after merge finishes.                            |
| `COMMIT_EDITMSG` | File      | Stores the message from the last commit (used by commit editor).                                   |


### Notes
The .git directory should never be edited manually unless you understand the risks.

Everything Git tracks is stored in objects/, referenced by SHA-1 hashes.

The refs/heads/ subdirectory contains local branches (e.g., refs/heads/main).

HEAD can be either a symbolic ref or a detached SHA-1 reference in detached HEAD state.

# Difference between info/exclude and .gitignore

The difference between .gitignore and info/exclude lies in their purpose and scope: .gitignore is a project-level file that is typically committed to the repository to share ignore rules with all collaborators, while info/exclude is a local-only ignore file found inside the .git/info directory and is not committed to version control. Use .gitignore for patterns that should be consistently ignored across all environments, and info/exclude for temporary or personal ignore rules that apply only to your local clone of the repository.

# How to read Git objects file
```bash
# List object directories (first two characters of object hash)
ls .git/objects

# Example: suppose you have an object with hash ab1234...

# You can read the object using git cat-file
git cat-file -p ab1234
```
* Git stores objects in .git/objects under subdirectories named by the first two characters of the SHA-1 hash. The remaining 38 characters form the filename.

* For example, object ab1234... is stored as: .git/objects/ab/1234...

* You should not try to manually assemble the path — just use the full hash with git cat-file -p <hash>.


# Git add Hunk
To add a hunk in Git, you can use interactive staging with the git add **-p** (or --patch) command. Here's how it works:
```
git add -p

```
| Option | Description                                      |
| ------ | ------------------------------------------------ |
| `y`    | Stage this hunk                                  |
| `n`    | Do **not** stage this hunk                       |
| `q`    | Quit; do not stage this or any further hunks     |
| `a`    | Stage this hunk and all the remaining ones       |
| `d`    | Do not stage this or any further hunks           |
| `s`    | Split this hunk into smaller hunks (if possible) |
| `e`    | Manually edit the hunk before staging            |
| `?`    | Show help for the options                        |


# git commit -am (add and commit at the same time)
git commit -am command is a shorthand for staging and committing tracked files in one step.
**Note** This doesn't work for Untracked files.

# git commit --amend
git commit --amend lets you modify the most recent commit — either its message, its contents, or both.
```
git add missing-file.js
git commit --amend --no-edit
```
#### Adds the new file to the last commit without changing its message

# git log
You can list the executed commit with below command.
```
git log
```
you can retrieve the certain number of commit as follows
```
git log -10
# it will also show the changes between commits
git log -p
# it shows the commits in one line for each
git log --oneline
git log --oneline 
git log --pretty=oneline 
git log --after="30 minutes ago"
git log --after="1 hour ago"
git log --after="1 days ago"
git log --before="Sun Jun 29 04:20:10 2025"
git log --before="Sun Jun 29 04:10:10 2025"
```



# Git Diff with HEAD
The command below shows the difference between the working directory and the last commit (referred to as HEAD):

```
git diff HEAD
```
This compares all files (both staged and unstaged changes) with the latest commit. It helps you see everything that has changed in your working directory, whether you've staged it or not.

If you want to narrow it down to a specific file:
```
git diff HEAD -- "file-name"
```
  
=======
# Remove File in git
If you use the native rm command in your directory, Git will detect the file removal as a change. You must then stage the deletion with git add and commit it:
```bash
rm "file-name"
git add "file-name"
git commit -m "Remove file-name"

```
Alternatively, you can use git rm, which removes the file and stages the deletion in one step:

```bash
git rm "file-name"
git commit -m "Remove file-name"
```


# Rename File
If you use the native mv command to rename a file, Git will treat this as a deletion of the old file and the creation of a new one. This change must be staged and committed manually.

To simplify this, you can use git mv, which renames the file and stages the change in one step:
```bash
git mv "old-name" "new-name"
git commit -m "Rename old-name to new-name"
```
# Git diff
The following command shows the differences between the working directory and the staged version (or the last committed version) of a specified file:
```
git diff "file-name"

```
This displays line-by-line changes that have been made to "file-name" since the last commit, but not yet staged. If you want to compare the staged version to the last commit, use:

```bash
git diff --cached "file-name"
```

# Git Diff with HEAD

The command below shows the difference between the working directory and the last commit (referred to as HEAD):
```
git diff HEAD
```

This compares all files (both staged and unstaged changes) with the latest commit. It helps you see everything that has changed in your working directory, whether you've staged it or not.

If you want to narrow it down to a specific file:
```
git diff HEAD -- "file-name"
```
=======

# Git Reset

The git reset command is used to undo changes by moving the HEAD and optionally modifying the index (staging area) and working directory.

This unstages files that were previously added with git add, but does not delete any changes in the working directory.


# Restore a File to the Last Committed Version
```
git checkout HEAD -- "file-name"

```
# git revert
The git revert command is used to undo a commit by creating a new commit that reverses the changes introduced by a previous one — without rewriting history.

# Difference Between git reset and git revert

| Feature                       | `git reset`                                                                                  | `git revert`                                                    |
| ----------------------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Purpose**                   | Moves `HEAD` to a previous commit and optionally modifies staging area and working directory | Creates a new commit that undoes changes from a previous commit |
| **History**                   | Rewrites history (destructive)                                                               | Preserves history (non-destructive)                             |
| **Commit Removed?**           | Yes (if you reset to an earlier commit)                                                      | No, original commit stays; changes are reversed                 |
| **Safe for Shared Branches?** | ❌ No (can confuse collaborators)                                                             | ✅ Yes (safe for public/shared branches)                         |
| **Working Directory**         | Can discard or keep changes, depending on flags (`--soft`, `--mixed`, `--hard`)              | Only affects content introduced by reverted commit              |
| **Creates New Commit?**       | ❌ Not unless followed by a new commit                                                        | ✅ Yes                                                           |

* Use git reset when you want to move the current branch backward, possibly discarding or unstaging changes — mostly for local, private changes.

* Use git revert when you want to safely undo a commit in a public or shared branch by creating a new commit that reverses the changes

