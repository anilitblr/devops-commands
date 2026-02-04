# Collaborate

## fetch

Download objects and refs from another repository.

### Syntax

```bash
git fetch [options] [<repository> [<refspec>...]]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--all` | Fetch from all remotes |
| `-p, --prune` | Remove deleted remote branches |
| `--tags` | Fetch all tags |
| `--no-tags` | Don't fetch tags |
| `--depth=<n>` | Limit fetching to specified depth |
| `--dry-run` | Show what would be done |

### Examples

```bash
# Fetch from origin
git fetch

# Fetch from a specific remote
git fetch upstream

# Fetch all remotes
git fetch --all

# Fetch and prune deleted branches
git fetch -p

# Fetch a specific branch
git fetch origin main

# Fetch all tags
git fetch --tags

# Shallow fetch
git fetch --depth=1
```

---

## pull

Fetch from and integrate with another repository or a local branch.

### Syntax

```bash
git pull [options] [<repository> [<refspec>...]]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--rebase` | Rebase instead of merge |
| `--no-rebase` | Merge instead of rebase |
| `--ff-only` | Only fast-forward |
| `--no-ff` | Create merge commit |
| `--autostash` | Stash changes before pull |
| `--all` | Fetch from all remotes |

### Examples

```bash
# Pull from tracked remote branch
git pull

# Pull from a specific remote and branch
git pull origin main

# Pull with rebase
git pull --rebase

# Pull with rebase and autostash
git pull --rebase --autostash

# Fast-forward only
git pull --ff-only

# Pull from all remotes
git pull --all
```

---

## push

Update remote refs along with associated objects.

### Syntax

```bash
git push [options] [<repository> [<refspec>...]]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-u, --set-upstream` | Set upstream for the branch |
| `-f, --force` | Force push (use with caution) |
| `--force-with-lease` | Safer force push |
| `--all` | Push all branches |
| `--tags` | Push all tags |
| `-d, --delete` | Delete remote branch |
| `--dry-run` | Show what would be pushed |

### Examples

```bash
# Push to tracked remote branch
git push

# Push and set upstream
git push -u origin feature-branch

# Push to a specific remote and branch
git push origin main

# Force push (dangerous)
git push -f origin feature-branch

# Safer force push
git push --force-with-lease origin feature-branch

# Push all branches
git push --all

# Push all tags
git push --tags

# Delete a remote branch
git push -d origin feature-branch

# Push to multiple remotes
git push origin main && git push upstream main
```
