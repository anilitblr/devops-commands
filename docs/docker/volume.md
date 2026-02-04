# Volume Commands

## volume create

Create a volume.

### Syntax

```bash
docker volume create [OPTIONS] [VOLUME]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-d, --driver` | Specify volume driver (default "local") |
| `--label` | Set metadata for a volume |
| `-o, --opt` | Set driver specific options |
| `--name` | Specify volume name |

### Examples

```bash
# Create a volume
docker volume create my-volume

# Create with specific driver
docker volume create -d local my-volume

# Create with labels
docker volume create --label env=production my-volume

# Create with driver options
docker volume create -o type=tmpfs -o device=tmpfs -o o=size=100m my-tmpfs

# Create NFS volume
docker volume create -d local \
  -o type=nfs \
  -o o=addr=192.168.1.1,rw \
  -o device=:/path/to/dir \
  nfs-volume
```

---

## volume ls

List volumes.

### Syntax

```bash
docker volume ls [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --filter` | Provide filter values |
| `--format` | Format output using Go template |
| `-q, --quiet` | Only display volume names |

### Examples

```bash
# List all volumes
docker volume ls

# List only volume names
docker volume ls -q

# Filter by driver
docker volume ls -f driver=local

# Filter by name
docker volume ls -f name=my-volume

# Filter dangling volumes
docker volume ls -f dangling=true

# Custom format
docker volume ls --format "{{.Name}}: {{.Driver}}"

# Filter by label
docker volume ls -f label=env=production
```

---

## volume rm

Remove one or more volumes.

### Syntax

```bash
docker volume rm [OPTIONS] VOLUME [VOLUME...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force the removal |

### Examples

```bash
# Remove a volume
docker volume rm my-volume

# Remove multiple volumes
docker volume rm volume1 volume2

# Force remove
docker volume rm -f my-volume

# Remove all unused volumes
docker volume rm $(docker volume ls -q -f dangling=true)
```

---

## volume inspect

Display detailed information on one or more volumes.

### Syntax

```bash
docker volume inspect [OPTIONS] VOLUME [VOLUME...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --format` | Format output using Go template |

### Examples

```bash
# Inspect a volume
docker volume inspect my-volume

# Inspect multiple volumes
docker volume inspect volume1 volume2

# Get mount point
docker volume inspect -f '{{.Mountpoint}}' my-volume

# Get driver
docker volume inspect -f '{{.Driver}}' my-volume

# Get labels
docker volume inspect -f '{{json .Labels}}' my-volume

# Get creation time
docker volume inspect -f '{{.CreatedAt}}' my-volume
```

---

## volume prune

Remove unused local volumes.

### Syntax

```bash
docker volume prune [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all` | Remove all unused volumes, not just anonymous ones |
| `-f, --force` | Do not prompt for confirmation |
| `--filter` | Provide filter values |

### Examples

```bash
# Remove unused volumes (with prompt)
docker volume prune

# Remove without prompt
docker volume prune -f

# Remove all unused volumes
docker volume prune -a -f

# Remove volumes with filter
docker volume prune -f --filter "label!=keep"
```
