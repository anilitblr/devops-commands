# System Commands

## system df

Show Docker disk usage.

### Syntax

```bash
docker system df [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--format` | Format output using Go template |
| `-v, --verbose` | Show detailed information |

### Examples

```bash
# Show disk usage
docker system df

# Verbose output
docker system df -v

# Custom format
docker system df --format "{{.Type}}: {{.Size}}"

# JSON format
docker system df --format '{{json .}}'
```

---

## system prune

Remove unused data.

### Syntax

```bash
docker system prune [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all` | Remove all unused images, not just dangling |
| `-f, --force` | Do not prompt for confirmation |
| `--filter` | Provide filter values |
| `--volumes` | Prune anonymous volumes |

### Examples

```bash
# Remove unused data (with prompt)
docker system prune

# Remove without prompt
docker system prune -f

# Remove all unused images (not just dangling)
docker system prune -a

# Remove volumes as well
docker system prune --volumes

# Full cleanup
docker system prune -a --volumes -f

# Remove items older than 24 hours
docker system prune -f --filter "until=24h"
```

---

## system info

Display system-wide information.

### Syntax

```bash
docker system info [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --format` | Format output using Go template |

### Examples

```bash
# Show system info
docker system info

# Get specific info
docker system info --format '{{.ServerVersion}}'

# Get storage driver
docker system info --format '{{.Driver}}'

# Get number of containers
docker system info --format '{{.Containers}}'

# Get OS type
docker system info --format '{{.OSType}}'

# JSON format
docker system info --format '{{json .}}'
```

---

## events

Get real-time events from the server.

### Syntax

```bash
docker events [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --filter` | Filter output based on conditions |
| `--format` | Format output using Go template |
| `--since` | Show events since timestamp |
| `--until` | Show events until timestamp |

### Event Types

| Type | Description |
|------|-------------|
| `container` | Container events (start, stop, die, etc.) |
| `image` | Image events (pull, push, delete, etc.) |
| `volume` | Volume events (create, destroy, mount, etc.) |
| `network` | Network events (create, connect, disconnect, etc.) |
| `daemon` | Daemon events (reload) |

### Examples

```bash
# Stream all events
docker events

# Filter by container
docker events -f container=my-container

# Filter by event type
docker events -f type=container

# Filter by action
docker events -f event=start

# Filter by image
docker events -f image=nginx

# Events since time
docker events --since '2024-01-01T00:00:00'

# Events in time range
docker events --since '10m' --until '5m'

# Custom format
docker events --format '{{.Time}} {{.Type}} {{.Action}}'

# JSON format
docker events --format '{{json .}}'

# Multiple filters
docker events -f type=container -f event=start -f event=stop
```
