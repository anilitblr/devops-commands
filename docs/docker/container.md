# Container Commands

## attach

Attach local standard input, output, and error streams to a running container.

### Syntax

```bash
docker attach [OPTIONS] CONTAINER
```

### Common Options

| Option | Description |
|--------|-------------|
| `--detach-keys` | Override the key sequence for detaching |
| `--no-stdin` | Do not attach STDIN |
| `--sig-proxy` | Proxy all received signals (default true) |

### Examples

```bash
# Attach to a running container
docker attach my-container

# Attach without STDIN
docker attach --no-stdin my-container

# Custom detach keys
docker attach --detach-keys="ctrl-x" my-container
```

---

## commit

Create a new image from a container's changes.

### Syntax

```bash
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --author` | Author |
| `-c, --change` | Apply Dockerfile instruction |
| `-m, --message` | Commit message |
| `-p, --pause` | Pause container during commit (default true) |

### Examples

```bash
# Commit container to image
docker commit my-container my-image:v1

# Commit with message and author
docker commit -m "Added config" -a "John Doe" my-container my-image:v1

# Commit with Dockerfile changes
docker commit -c 'CMD ["nginx"]' my-container my-image:v1

# Commit without pausing
docker commit --pause=false my-container my-image:v1
```

---

## cp

Copy files/folders between a container and the local filesystem.

### Syntax

```bash
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH
docker cp [OPTIONS] SRC_PATH CONTAINER:DEST_PATH
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --archive` | Archive mode (preserve permissions) |
| `-L, --follow-link` | Follow symbolic links |
| `-q, --quiet` | Suppress progress output |

### Examples

```bash
# Copy from container to host
docker cp my-container:/app/config.json ./config.json

# Copy from host to container
docker cp ./config.json my-container:/app/config.json

# Copy directory
docker cp my-container:/app/logs ./logs

# Archive mode (preserve permissions)
docker cp -a my-container:/app ./backup
```

---

## create

Create a new container (without starting it).

### Syntax

```bash
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--name` | Assign a name to the container |
| `-p, --publish` | Publish container port(s) |
| `-v, --volume` | Bind mount a volume |
| `-e, --env` | Set environment variables |
| `--network` | Connect to a network |
| `-it` | Interactive with TTY |

### Examples

```bash
# Create a container
docker create --name my-container nginx

# Create with port mapping
docker create -p 8080:80 --name web nginx

# Create with volume
docker create -v /data:/app/data --name app myimage

# Create and get container ID
docker create nginx
```

---

## diff

Inspect changes to files or directories on a container's filesystem.

### Syntax

```bash
docker diff CONTAINER
```

### Output Symbols

| Symbol | Description |
|--------|-------------|
| `A` | File or directory was added |
| `D` | File or directory was deleted |
| `C` | File or directory was changed |

### Examples

```bash
# Show filesystem changes
docker diff my-container
```

---

## export

Export a container's filesystem as a tar archive.

### Syntax

```bash
docker export [OPTIONS] CONTAINER
```

### Common Options

| Option | Description |
|--------|-------------|
| `-o, --output` | Write to a file |

### Examples

```bash
# Export to stdout
docker export my-container > container.tar

# Export to file
docker export -o container.tar my-container
```

---

## kill

Kill one or more running containers.

### Syntax

```bash
docker kill [OPTIONS] CONTAINER [CONTAINER...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-s, --signal` | Signal to send (default "KILL") |

### Examples

```bash
# Kill a container
docker kill my-container

# Kill multiple containers
docker kill container1 container2

# Send specific signal
docker kill -s SIGTERM my-container

# Kill all running containers
docker kill $(docker ps -q)
```

---

## logs

Fetch the logs of a container.

### Syntax

```bash
docker logs [OPTIONS] CONTAINER
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --follow` | Follow log output |
| `--since` | Show logs since timestamp |
| `--until` | Show logs before timestamp |
| `-n, --tail` | Number of lines from the end |
| `-t, --timestamps` | Show timestamps |

### Examples

```bash
# Show all logs
docker logs my-container

# Follow logs
docker logs -f my-container

# Show last 100 lines
docker logs --tail 100 my-container

# Show logs with timestamps
docker logs -t my-container

# Show logs since time
docker logs --since 2024-01-01T00:00:00 my-container

# Show logs from last 30 minutes
docker logs --since 30m my-container
```

---

## pause

Pause all processes within one or more containers.

### Syntax

```bash
docker pause CONTAINER [CONTAINER...]
```

### Examples

```bash
# Pause a container
docker pause my-container

# Pause multiple containers
docker pause container1 container2
```

---

## port

List port mappings or a specific mapping for the container.

### Syntax

```bash
docker port CONTAINER [PRIVATE_PORT[/PROTO]]
```

### Examples

```bash
# List all port mappings
docker port my-container

# Show specific port mapping
docker port my-container 80

# Show TCP port mapping
docker port my-container 80/tcp
```

---

## rename

Rename a container.

### Syntax

```bash
docker rename CONTAINER NEW_NAME
```

### Examples

```bash
# Rename a container
docker rename old-name new-name
```

---

## restart

Restart one or more containers.

### Syntax

```bash
docker restart [OPTIONS] CONTAINER [CONTAINER...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-s, --signal` | Signal to send before stopping |
| `-t, --time` | Seconds to wait before killing (default 10) |

### Examples

```bash
# Restart a container
docker restart my-container

# Restart with timeout
docker restart -t 30 my-container

# Restart multiple containers
docker restart container1 container2

# Restart all running containers
docker restart $(docker ps -q)
```

---

## rm

Remove one or more containers.

### Syntax

```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force removal of running container |
| `-l, --link` | Remove the specified link |
| `-v, --volumes` | Remove anonymous volumes |

### Examples

```bash
# Remove a stopped container
docker rm my-container

# Force remove a running container
docker rm -f my-container

# Remove container and its volumes
docker rm -v my-container

# Remove all stopped containers
docker rm $(docker ps -aq -f status=exited)

# Remove all containers
docker rm -f $(docker ps -aq)
```

---

## start

Start one or more stopped containers.

### Syntax

```bash
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --attach` | Attach STDOUT/STDERR |
| `-i, --interactive` | Attach STDIN |

### Examples

```bash
# Start a container
docker start my-container

# Start and attach
docker start -a my-container

# Start interactively
docker start -ai my-container

# Start multiple containers
docker start container1 container2
```

---

## stats

Display a live stream of container(s) resource usage statistics.

### Syntax

```bash
docker stats [OPTIONS] [CONTAINER...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all` | Show all containers |
| `--format` | Format output using Go template |
| `--no-stream` | Disable streaming stats |
| `--no-trunc` | Do not truncate output |

### Examples

```bash
# Show stats for all running containers
docker stats

# Show stats for specific containers
docker stats container1 container2

# Show single snapshot (no stream)
docker stats --no-stream

# Custom format
docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"

# Show all containers including stopped
docker stats -a
```

---

## stop

Stop one or more running containers.

### Syntax

```bash
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-s, --signal` | Signal to send (default "SIGTERM") |
| `-t, --time` | Seconds to wait before killing (default 10) |

### Examples

```bash
# Stop a container
docker stop my-container

# Stop with timeout
docker stop -t 30 my-container

# Stop multiple containers
docker stop container1 container2

# Stop all running containers
docker stop $(docker ps -q)
```

---

## top

Display the running processes of a container.

### Syntax

```bash
docker top CONTAINER [ps OPTIONS]
```

### Examples

```bash
# Show running processes
docker top my-container

# Show with ps options
docker top my-container aux

# Show with custom format
docker top my-container -o pid,user,comm
```

---

## unpause

Unpause all processes within one or more containers.

### Syntax

```bash
docker unpause CONTAINER [CONTAINER...]
```

### Examples

```bash
# Unpause a container
docker unpause my-container

# Unpause multiple containers
docker unpause container1 container2
```

---

## update

Update configuration of one or more containers.

### Syntax

```bash
docker update [OPTIONS] CONTAINER [CONTAINER...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--cpus` | Number of CPUs |
| `--memory, -m` | Memory limit |
| `--memory-swap` | Swap limit |
| `--restart` | Restart policy |
| `--pids-limit` | Tune container pids limit |

### Examples

```bash
# Update memory limit
docker update --memory 512m my-container

# Update CPU limit
docker update --cpus 2 my-container

# Update restart policy
docker update --restart unless-stopped my-container

# Update multiple settings
docker update --memory 1g --cpus 2 my-container
```

---

## wait

Block until one or more containers stop, then print their exit codes.

### Syntax

```bash
docker wait CONTAINER [CONTAINER...]
```

### Examples

```bash
# Wait for a container to stop
docker wait my-container

# Wait for multiple containers
docker wait container1 container2
```
