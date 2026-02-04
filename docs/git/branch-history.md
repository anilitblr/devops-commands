# Grow, Mark and Tweak Your Common History

## branch

List, create, or delete branches.

### Syntax

```bash
git branch [options] [<branchname>] [<start-point>]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all` | List both local and remote branches |
| `-r, --remotes` | List remote-tracking branches |
| `-d, --delete` | Delete a branch (must be merged) |
| `-D` | Force delete a branch |
| `-m, --move` | Rename a branch |
| `-c, --copy` | Copy a branch |
| `-v, --verbose` | Show sha1 and commit subject |
| `--merged` | List branches merged into current |
| `--no-merged` | List branches not merged |

### Examples

```bash
# List local branches
git branch

# List all branches (local and remote)
git branch -a

# Create a new branch
git branch feature-name

# Delete a merged branch
git branch -d feature-name

# Force delete a branch
git branch -D feature-name

# Rename current branch
git branch -m new-name

# Rename a specific branch
git branch -m old-name new-name

# List merged branches
git branch --merged

# Show branches with last commit info
git branch -v
```

---

## commit

Record changes to the repository.

### Syntax

```bash
git commit [options]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-m <msg>` | Commit message |
| `-a, --all` | Automatically stage modified files |
| `--amend` | Amend the previous commit |
| `-v, --verbose` | Show diff in commit message editor |
| `--no-edit` | Use previous commit message (with --amend) |
| `--allow-empty` | Allow empty commit |
| `-S, --gpg-sign` | GPG sign the commit |

### Examples

```bash
# Commit staged changes
git commit -m "Add new feature"

# Stage all modified files and commit
git commit -am "Fix bug"

# Amend the last commit
git commit --amend

# Amend without changing the message
git commit --amend --no-edit

# Multi-line commit message
git commit -m "Subject line" -m "Body paragraph"

# Commit with verbose diff
git commit -v

# Create an empty commit
git commit --allow-empty -m "Trigger CI"
```

---

## merge

Join two or more development histories together.

### Syntax

```bash
git merge [options] [<commit>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--no-ff` | Create a merge commit even for fast-forward |
| `--ff-only` | Only allow fast-forward merges |
| `--squash` | Squash commits into one |
| `--abort` | Abort current merge |
| `--continue` | Continue after resolving conflicts |
| `-m <msg>` | Merge commit message |
| `--no-commit` | Merge but don't commit |

### Examples

```bash
# Merge a branch into current branch
git merge feature-branch

# Merge with a merge commit (no fast-forward)
git merge --no-ff feature-branch

# Only merge if fast-forward is possible
git merge --ff-only feature-branch

# Squash merge
git merge --squash feature-branch

# Merge with custom message
git merge -m "Merge feature X" feature-branch

# Abort a merge with conflicts
git merge --abort

# Continue after resolving conflicts
git merge --continue
```

---

## rebase

Reapply commits on top of another base tip.

### Syntax

```bash
git rebase [options] [<upstream> [<branch>]]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-i, --interactive` | Interactive rebase |
| `--onto <newbase>` | Rebase onto a different base |
| `--continue` | Continue after resolving conflicts |
| `--abort` | Abort rebase |
| `--skip` | Skip current patch |
| `-x <cmd>` | Execute command after each commit |
| `--autosquash` | Auto-apply fixup/squash commits |

### Examples

```bash
# Rebase current branch onto main
git rebase main

# Interactive rebase last 3 commits
git rebase -i HEAD~3

# Rebase onto a different base
git rebase --onto main feature-base feature

# Continue after resolving conflicts
git rebase --continue

# Abort the rebase
git rebase --abort

# Skip the current commit
git rebase --skip

# Run tests after each commit
git rebase -x "npm test" main
```

---

## reset

Reset current HEAD to the specified state.

### Syntax

```bash
git reset [options] [<commit>]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--soft` | Keep changes staged |
| `--mixed` | Keep changes unstaged (default) |
| `--hard` | Discard all changes |
| `--merge` | Reset but keep uncommitted changes |
| `--keep` | Reset but abort if uncommitted changes conflict |

### Examples

```bash
# Unstage all files (keep changes)
git reset

# Unstage a specific file
git reset HEAD filename.txt

# Soft reset (keep changes staged)
git reset --soft HEAD~1

# Mixed reset (keep changes unstaged)
git reset --mixed HEAD~1

# Hard reset (discard all changes)
git reset --hard HEAD~1

# Reset to a specific commit
git reset --hard abc1234

# Reset to remote branch state
git reset --hard origin/main
```

---

## switch

Switch branches.

### Syntax

```bash
git switch [options] <branch>
```

### Common Options

| Option | Description |
|--------|-------------|
| `-c, --create` | Create and switch to new branch |
| `-C, --force-create` | Force create (reset if exists) |
| `-d, --detach` | Switch to a commit in detached HEAD |
| `--discard-changes` | Discard local changes |
| `--guess` | Guess remote branch (default) |

### Examples

```bash
# Switch to an existing branch
git switch main

# Create and switch to a new branch
git switch -c feature-branch

# Create branch from a specific point
git switch -c feature-branch origin/main

# Force create (reset if exists)
git switch -C feature-branch

# Switch to a commit (detached HEAD)
git switch -d abc1234

# Discard local changes when switching
git switch --discard-changes main
```

---

## tag

Create, list, delete or verify a tag object signed with GPG.

### Syntax

```bash
git tag [options] [<tagname>] [<commit>]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --annotate` | Create an annotated tag |
| `-m <msg>` | Tag message |
| `-d, --delete` | Delete a tag |
| `-l, --list` | List tags |
| `-f, --force` | Replace existing tag |
| `-s, --sign` | GPG sign the tag |
| `-v, --verify` | Verify GPG signature |

### Examples

```bash
# List all tags
git tag

# List tags matching pattern
git tag -l "v1.*"

# Create a lightweight tag
git tag v1.0.0

# Create an annotated tag
git tag -a v1.0.0 -m "Version 1.0.0"

# Tag a specific commit
git tag -a v1.0.0 abc1234 -m "Version 1.0.0"

# Delete a local tag
git tag -d v1.0.0

# Delete a remote tag
git push origin --delete v1.0.0

# Push a tag to remote
git push origin v1.0.0

# Push all tags
git push origin --tags
```
