# Examine the History and State

## bisect

Use binary search to find the commit that introduced a bug.

### Syntax

```bash
git bisect <subcommand> [options]
```

### Subcommands

| Subcommand | Description |
|------------|-------------|
| `start` | Start a bisect session |
| `bad` | Mark current commit as bad |
| `good` | Mark current commit as good |
| `reset` | End bisect session and return to original branch |
| `skip` | Skip current commit |
| `log` | Show bisect log |
| `run <script>` | Automate bisect with a script |

### Examples

```bash
# Start bisecting
git bisect start

# Mark current version as bad
git bisect bad

# Mark a known good commit
git bisect good v1.0.0

# After testing, mark as good or bad
git bisect good  # or git bisect bad

# End the bisect session
git bisect reset

# Automated bisect with a test script
git bisect run ./test-script.sh
```

---

## diff

Show changes between commits, commit and working tree, etc.

### Syntax

```bash
git diff [options] [<commit>] [--] [<path>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--staged, --cached` | Show staged changes |
| `--stat` | Show diffstat summary |
| `--name-only` | Show only names of changed files |
| `--name-status` | Show names and status of changed files |
| `--color-words` | Show word-level diff with colors |
| `-w, --ignore-all-space` | Ignore whitespace |

### Examples

```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Compare with a specific commit
git diff HEAD~3

# Compare two branches
git diff main..feature

# Compare two commits
git diff abc123 def456

# Show only file names
git diff --name-only

# Diff a specific file
git diff -- filename.txt

# Show summary statistics
git diff --stat
```

---

## grep

Print lines matching a pattern.

### Syntax

```bash
git grep [options] <pattern> [<pathspec>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-n, --line-number` | Show line numbers |
| `-c, --count` | Show count of matches per file |
| `-i, --ignore-case` | Case insensitive search |
| `-w, --word-regexp` | Match whole words only |
| `-e <pattern>` | Use pattern (allows multiple patterns) |
| `-l, --files-with-matches` | Show only file names |

### Examples

```bash
# Search for a pattern
git grep "TODO"

# Case insensitive search
git grep -i "error"

# Show line numbers
git grep -n "function"

# Search in specific files
git grep "pattern" -- "*.js"

# Count matches per file
git grep -c "import"

# Search for whole word
git grep -w "test"

# Search in a specific commit
git grep "pattern" HEAD~5
```

---

## log

Show commit logs.

### Syntax

```bash
git log [options] [<revision-range>] [-- <path>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-n <number>` | Limit number of commits |
| `--oneline` | Show each commit on one line |
| `--graph` | Show ASCII graph of branch history |
| `--all` | Show all branches |
| `--author=<pattern>` | Filter by author |
| `--since, --after` | Show commits after date |
| `--until, --before` | Show commits before date |
| `-p, --patch` | Show diff for each commit |
| `--stat` | Show file statistics |

### Examples

```bash
# Show commit history
git log

# Show last 5 commits
git log -5

# One-line format
git log --oneline

# Show graph with branches
git log --graph --oneline --all

# Filter by author
git log --author="John"

# Filter by date
git log --since="2024-01-01" --until="2024-12-31"

# Show commits affecting a file
git log -- filename.txt

# Show commits with diffs
git log -p

# Custom format
git log --pretty=format:"%h - %an, %ar : %s"
```

---

## show

Show various types of objects.

### Syntax

```bash
git show [options] [<object>...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--stat` | Show diffstat |
| `--name-only` | Show only names of changed files |
| `--name-status` | Show names and status of changed files |
| `--format=<format>` | Pretty-print format |
| `--no-patch` | Suppress diff output |

### Examples

```bash
# Show latest commit
git show

# Show a specific commit
git show abc1234

# Show a tag
git show v1.0.0

# Show a file from a commit
git show HEAD:filename.txt

# Show only stats
git show --stat

# Show only commit message (no diff)
git show --no-patch

# Show file names only
git show --name-only
```

---

## status

Show the working tree status.

### Syntax

```bash
git status [options]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-s, --short` | Short format output |
| `-b, --branch` | Show branch info in short format |
| `--long` | Long format output (default) |
| `--porcelain` | Machine-readable output |
| `-u, --untracked-files` | Show untracked files |
| `--ignored` | Show ignored files |

### Examples

```bash
# Show full status
git status

# Short format
git status -s

# Short format with branch info
git status -sb

# Show untracked files
git status -u

# Machine-readable output
git status --porcelain

# Show ignored files
git status --ignored
```
