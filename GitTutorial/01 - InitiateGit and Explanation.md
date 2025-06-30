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