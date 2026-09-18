## Git & GitHub

### Setup & Status

```bash
git init
```
To initialize a brand-new, local Git repository.

```bash
git status
```
To display the current state of your working directory and staging area.

### Staging & Committing

```bash
git add .
```
To move changes from your working directory to the staging area.

```bash
git commit -m "enter your message"
```
To permanently save your staged changes to the local repository history along with a custom descriptive message.

```bash
git log
```
To view the commit history of a Git repository.

```
A---B---C  (main)
```
Each letter is a commit; `git log` walks this chain from newest to oldest.

### Undoing Changes

```bash
git restore --staged <file_name>
```
To unstage a file that you have previously added to the staging area (using `git add`).

```bash
git reset <commit_id>
```
Rewinds your current branch history back to the specified commit.

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

```bash
git stash
```
Temporarily save (or "stash") changes you've made to your working directory so you can work on something else, without having to commit them.

```bash
git stash pop
```
Reapply your most recently saved (stashed) changes back to your working directory while simultaneously removing that entry from your stash history.

```bash
git stash clear
```
Deletes all saved stashes from your repository at once.

### Remotes

```bash
git remote add origin <url>
git push origin main
```
Connect your local Git repository to a newly created remote repository, then push your commits up to it.

```bash
git remote -v
```
Lists the remote repositories your local repo is connected to, along with their URLs.

### Forking & Cloning

```bash
git clone <url>
```
Forking and cloning to local.

```bash
git remote add upstream <url>
```
From where the repo has been forked.

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

```bash
git branch <branch_name>
```
Creates a new branch.

```bash
git checkout <branch_name>
```
The HEAD will point to the created branch.

```
main:      A---B---C
                     \
new_branch:           (HEAD now here, ready for new commits)
```

> One branch, one PR.

```bash
git push origin -f <branch_name>
```
Force push to the remote repository.

### Syncing a Fork with Upstream

```bash
git fetch --all --prune
git reset --hard upstream/main
git push origin main
```

```bash
git pull origin main
git push origin main
```

### Rebasing

> Can merge multiple commits by stashing.

```bash
git rebase -i <commit_id>
```
Opens an interactive rebase, letting you rewrite commit history using the **pick/squash** technique — pick keeps a commit as-is, squash folds it into the commit before it.

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

Happens when Git can't automatically combine changes from two branches because they both edited the same lines — you resolve them by hand, then `git add` the fixed files and commit.

```
main:      A---B---C-------M
                \          /
feature:         D----E---/
```
`M` is the merge commit, created once conflicts are resolved.
