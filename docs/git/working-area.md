# Start a Working Area

## clone

Clone a repository into a new directory.

### Syntax

```bash
git clone [options] <repository> [<directory>]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-b <branch>` | Clone a specific branch |
| `--depth <n>` | Create a shallow clone with history truncated to n commits |
| `--single-branch` | Clone only the history leading to the tip of a single branch |
| `--recurse-submodules` | Initialize and clone submodules |
| `--bare` | Create a bare repository |
| `--mirror` | Create a mirror clone (bare repo with remote tracking) |

### Examples

```bash
# Clone a repository
git clone https://github.com/user/repo.git

# Clone into a specific directory
git clone https://github.com/user/repo.git my-project

# Clone a specific branch
git clone -b develop https://github.com/user/repo.git

# Shallow clone (only latest commit)
git clone --depth 1 https://github.com/user/repo.git

# Clone with submodules
git clone --recurse-submodules https://github.com/user/repo.git
```

---

## init

Create an empty Git repository or reinitialize an existing one.

### Syntax

```bash
git init [options] [<directory>]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--bare` | Create a bare repository |
| `-b <branch>` | Use specified name for the initial branch |
| `--initial-branch=<name>` | Same as `-b` |
| `--template=<dir>` | Specify the template directory |

### Examples

```bash
# Initialize a new repository in current directory
git init

# Initialize in a specific directory
git init my-project

# Initialize with a custom default branch name
git init -b main

# Create a bare repository
git init --bare my-project.git
```
