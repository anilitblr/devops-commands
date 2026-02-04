# Work on the Current Change

## add

Add file contents to the index (staging area).

### Syntax

```bash
git add [options] [<pathspec>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-A, --all` | Add all changes (new, modified, deleted) |
| `-u, --update` | Add modified and deleted files only (no new files) |
| `-p, --patch` | Interactively choose hunks to stage |
| `-n, --dry-run` | Show what would be added without actually adding |
| `-f, --force` | Allow adding ignored files |
| `-i, --interactive` | Interactive mode |

### Examples

```bash
# Add a specific file
git add filename.txt

# Add all files in a directory
git add src/

# Add all changes in the repository
git add -A

# Add all modified and deleted files (not new files)
git add -u

# Interactively stage parts of files
git add -p

# Add all .js files
git add *.js
```

---

## mv

Move or rename a file, a directory, or a symlink.

### Syntax

```bash
git mv [options] <source> <destination>
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force rename/move even if target exists |
| `-k` | Skip move/rename that would cause an error |
| `-n, --dry-run` | Show what would happen without making changes |
| `-v, --verbose` | Report names of files as they are moved |

### Examples

```bash
# Rename a file
git mv old-name.txt new-name.txt

# Move a file to a directory
git mv file.txt src/

# Move and rename
git mv src/old.txt lib/new.txt

# Force overwrite existing file
git mv -f source.txt destination.txt

# Dry run to see what would happen
git mv -n file.txt new-location/
```

---

## restore

Restore working tree files.

### Syntax

```bash
git restore [options] [<pathspec>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-s, --source=<tree>` | Restore from specified tree |
| `-S, --staged` | Restore the index (unstage) |
| `-W, --worktree` | Restore the working tree (default) |
| `-p, --patch` | Interactively select hunks to restore |

### Examples

```bash
# Discard changes in working directory
git restore filename.txt

# Unstage a file (keep changes in working directory)
git restore --staged filename.txt

# Restore file from a specific commit
git restore --source=HEAD~2 filename.txt

# Restore all files in current directory
git restore .

# Unstage all files
git restore --staged .

# Interactively restore parts of a file
git restore -p filename.txt
```

---

## rm

Remove files from the working tree and from the index.

### Syntax

```bash
git rm [options] [<pathspec>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force removal of files |
| `-n, --dry-run` | Show what would be removed |
| `-r` | Allow recursive removal |
| `--cached` | Remove from index only (keep in working tree) |

### Examples

```bash
# Remove a file from Git and filesystem
git rm filename.txt

# Remove from Git but keep local file
git rm --cached filename.txt

# Remove a directory recursively
git rm -r directory/

# Remove all .log files
git rm *.log

# Dry run to see what would be removed
git rm -n *.tmp

# Force remove modified file
git rm -f modified-file.txt
```
