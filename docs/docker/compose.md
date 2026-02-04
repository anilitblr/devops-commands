# Docker Compose Commands

## compose up

Create and start containers.

### Syntax

```bash
docker compose up [OPTIONS] [SERVICE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-d, --detach` | Run containers in background |
| `--build` | Build images before starting containers |
| `--force-recreate` | Recreate containers even if unchanged |
| `--no-deps` | Don't start linked services |
| `--no-build` | Don't build images |
| `--remove-orphans` | Remove containers not defined in Compose file |
| `--scale` | Scale SERVICE to NUM instances |
| `-f, --file` | Specify Compose file |
| `--wait` | Wait for services to be running/healthy |

### Examples

```bash
# Start all services
docker compose up

# Start in detached mode
docker compose up -d

# Build and start
docker compose up --build

# Start specific services
docker compose up web db

# Force recreate containers
docker compose up --force-recreate

# Scale a service
docker compose up -d --scale web=3

# Use specific compose file
docker compose -f docker-compose.prod.yml up -d

# Remove orphan containers
docker compose up -d --remove-orphans

# Wait for healthy state
docker compose up -d --wait
```

---

## compose down

Stop and remove containers, networks.

### Syntax

```bash
docker compose down [OPTIONS] [SERVICES]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--rmi` | Remove images (all or local) |
| `-v, --volumes` | Remove named volumes |
| `--remove-orphans` | Remove containers not defined in Compose file |
| `-t, --timeout` | Shutdown timeout in seconds (default 10) |

### Examples

```bash
# Stop and remove containers
docker compose down

# Remove volumes as well
docker compose down -v

# Remove images too
docker compose down --rmi all

# Remove only local images
docker compose down --rmi local

# Remove orphan containers
docker compose down --remove-orphans

# With timeout
docker compose down -t 30
```

---

## compose ps

List containers.

### Syntax

```bash
docker compose ps [OPTIONS] [SERVICE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all` | Show all stopped containers |
| `--format` | Format output (table, json) |
| `-q, --quiet` | Only display container IDs |
| `--status` | Filter by status |
| `--services` | Display services |

### Examples

```bash
# List running containers
docker compose ps

# List all containers including stopped
docker compose ps -a

# List only container IDs
docker compose ps -q

# Filter by status
docker compose ps --status running

# JSON format
docker compose ps --format json

# List services only
docker compose ps --services
```

---

## compose logs

View output from containers.

### Syntax

```bash
docker compose logs [OPTIONS] [SERVICE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --follow` | Follow log output |
| `--since` | Show logs since timestamp |
| `--until` | Show logs until timestamp |
| `-n, --tail` | Number of lines from end |
| `-t, --timestamps` | Show timestamps |
| `--no-color` | Disable color output |

### Examples

```bash
# View all logs
docker compose logs

# Follow logs
docker compose logs -f

# Logs for specific service
docker compose logs web

# Last 100 lines
docker compose logs --tail 100

# With timestamps
docker compose logs -t

# Logs since time
docker compose logs --since 30m

# Follow specific services
docker compose logs -f web db
```

---

## compose build

Build or rebuild services.

### Syntax

```bash
docker compose build [OPTIONS] [SERVICE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--build-arg` | Set build-time variables |
| `--no-cache` | Do not use cache |
| `--pull` | Always pull newer versions |
| `--push` | Push images after building |
| `-q, --quiet` | Don't print anything |
| `--parallel` | Build images in parallel |

### Examples

```bash
# Build all services
docker compose build

# Build specific service
docker compose build web

# Build without cache
docker compose build --no-cache

# Build with build arg
docker compose build --build-arg VERSION=1.0

# Pull latest base images
docker compose build --pull

# Build and push
docker compose build --push

# Quiet build
docker compose build -q
```

---

## compose exec

Execute a command in a running container.

### Syntax

```bash
docker compose exec [OPTIONS] SERVICE COMMAND [ARGS...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-d, --detach` | Run in background |
| `-e, --env` | Set environment variables |
| `-i, --interactive` | Keep STDIN open (default true) |
| `-T, --no-TTY` | Disable pseudo-TTY |
| `-u, --user` | Run as specified user |
| `-w, --workdir` | Working directory |
| `--index` | Index of container if scaled |

### Examples

```bash
# Execute bash in a service
docker compose exec web bash

# Run a command
docker compose exec web ls -la

# Run as root
docker compose exec -u root web whoami

# Set environment variable
docker compose exec -e DEBUG=1 web env

# Execute in specific container when scaled
docker compose exec --index 2 web bash

# Non-interactive command
docker compose exec -T web cat /etc/hosts
```

---

## compose restart

Restart service containers.

### Syntax

```bash
docker compose restart [OPTIONS] [SERVICE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-t, --timeout` | Shutdown timeout in seconds (default 10) |
| `--no-deps` | Don't restart dependent services |

### Examples

```bash
# Restart all services
docker compose restart

# Restart specific service
docker compose restart web

# Restart with timeout
docker compose restart -t 30 web

# Restart multiple services
docker compose restart web db cache
```

---

## compose pull

Pull service images.

### Syntax

```bash
docker compose pull [OPTIONS] [SERVICE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--ignore-buildable` | Ignore images that can be built |
| `--ignore-pull-failures` | Pull what it can, ignore failures |
| `-q, --quiet` | Pull without printing progress |
| `--include-deps` | Also pull dependencies |

### Examples

```bash
# Pull all images
docker compose pull

# Pull specific service
docker compose pull web

# Pull quietly
docker compose pull -q

# Pull including dependencies
docker compose pull --include-deps web

# Ignore failures
docker compose pull --ignore-pull-failures
```
