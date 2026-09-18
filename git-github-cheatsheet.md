## Git & GitHub

### Setup & Status

To initialize a brand-new, local Git repository:
```bash
git init
```

To display the current state of your working directory and staging area:
```bash
git status
```

### Staging & Committing

To move changes from your working directory to the staging area:
```bash
git add .
```

To permanently save your staged changes to the local repository history along with a custom descriptive message:
```bash
git commit -m "enter your message"
```

To view the commit history of a Git repository:
```bash
git log
```
```
A---B---C  (main)
```
Each letter is a commit; `git log` walks this chain from newest to oldest.

### Undoing Changes

To unstage a file that you have previously added to the staging area (using `git add`):
```bash
git restore --staged <file_name>
```

Rewinds your current branch history back to the specified commit:
```bash
git reset <commit_id>
```
- **No flag (`--mixed`)**: Undoes the commit and unstages changes (files are safe).
- **Soft (`--soft`)**: Undoes the commit but keeps changes staged (files are safe).
- **Hard (`--hard`)**: Undoes the commit and destroys all changes (files are deleted).

```
Before reset:
A---B---C---D  (main, HEAD)

git reset --soft B
A---B  (main, HEAD)   [C and D's changes are staged]

git reset --hard B
A---B  (main, HEAD)   [C and D's changes are gone]
```

### Stashing

> Only the staged files can be stashed.

Temporarily save (or "stash") changes you've made to your working directory so you can work on something else, without having to commit them:
```bash
git stash
```

Reapply your most recently saved (stashed) changes back to your working directory while simultaneously removing that entry from your stash history:
```bash
git stash pop
```

Deletes all saved stashes from your repository at once:
```bash
git stash clear
```

### Remotes

Connect your local Git repository to a newly created remote repository, then push your commits up to it:
```bash
git remote add origin <url>
git push origin main
```

Lists the remote repositories your local repo is connected to, along with their URLs:
```bash
git remote -v
```

### Forking & Cloning

Forking and cloning to local:
```bash
git clone <url>
```

From where the repo has been forked, add a second remote so you can pull in updates from the original project:
```bash
git remote add upstream <url>
```

```
GitHub (upstream repo) --fork-->  Your GitHub (origin)
                                        |
                                     git clone
                                        |
                                        v
                                  Local machine
                                  ├── remote "origin"   -> your fork
                                  └── remote "upstream"  -> original repo
```

### Branching

Creates a new branch:
```bash
git branch <branch_name>
```

The HEAD will point to the created branch:
```bash
git checkout <branch_name>
```

```
main:      A---B---C
                     \
new_branch:           (HEAD now here, ready for new commits)
```

> One branch, one PR.

Force push to the remote repository. Use this when you've rewritten local history (e.g. after a rebase or hard reset) and need to overwrite the remote branch with your version:
```bash
git push origin -f <branch_name>
```

### Syncing a Fork with Upstream

Fetches all branches from every remote and removes references to branches that no longer exist upstream:
```bash
git fetch --all --prune
```
Resets your local `main` to exactly match `upstream/main`, discarding any local differences:
```bash
git reset --hard upstream/main
```
Pushes that reset state to your own fork on GitHub (`-f` may be needed if origin has diverged):
```bash
git push origin main
```

Alternatively, a simpler day-to-day sync when you just want to merge in the latest changes rather than force-overwrite:
```bash
git pull origin main
git push origin main
```

### Rebasing

> Can merge multiple commits by stashing.

Opens an interactive rebase, letting you rewrite commit history using the pick/squash technique:
```bash
git rebase -i <commit_id>
```
- **pick** keeps a commit as-is
- **squash** folds it into the commit before it, combining multiple commits into one

```
Before:
main:     A---B---C
                    \
feature:             D---E

After rebasing feature onto main:
main:     A---B---C
                    \
feature:             D'---E'
```

### Merge Conflicts

Happens when Git can't automatically combine changes from two branches because they both edited the same lines. You resolve them by hand, then `git add` the fixed files and commit:
```bash
git add <fixed_file>
git commit
```

```
main:      A---B---C-------M
                \          /
feature:         D----E---/
```
`M` is the merge commit, created once conflicts are resolved.