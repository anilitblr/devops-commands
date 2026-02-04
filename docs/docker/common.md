# Common Commands

## run

Create and run a new container from an image.

### Syntax

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-d, --detach` | Run container in background |
| `-it` | Interactive mode with TTY |
| `--name` | Assign a name to the container |
| `-p, --publish` | Publish container port(s) to host |
| `-v, --volume` | Bind mount a volume |
| `-e, --env` | Set environment variables |
| `--rm` | Automatically remove container when it exits |
| `--network` | Connect to a network |
| `-w, --workdir` | Working directory inside the container |
| `--restart` | Restart policy (no, always, on-failure, unless-stopped) |

### Examples

```bash
# Run a container interactively
docker run -it ubuntu bash

# Run in detached mode with port mapping
docker run -d -p 8080:80 nginx

# Run with environment variables
docker run -e MYSQL_ROOT_PASSWORD=secret mysql

# Run with volume mount
docker run -v /host/path:/container/path nginx

# Run with name and auto-remove
docker run --rm --name my-app alpine echo "Hello"

# Run with multiple options
docker run -d --name web -p 80:80 -v ./html:/usr/share/nginx/html nginx

# Run with resource limits
docker run -d --memory=512m --cpus=1 nginx

# Run with restart policy
docker run -d --restart=unless-stopped nginx
```

---

## exec

Execute a command in a running container.

### Syntax

```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-d, --detach` | Run command in background |
| `-e, --env` | Set environment variables |
| `-i, --interactive` | Keep STDIN open |
| `-t, --tty` | Allocate a pseudo-TTY |
| `-u, --user` | Username or UID |
| `-w, --workdir` | Working directory inside the container |

### Examples

```bash
# Open a bash shell in a running container
docker exec -it container_name bash

# Run a command in a container
docker exec container_name ls -la

# Run as a specific user
docker exec -u root container_name whoami

# Set working directory
docker exec -w /app container_name pwd

# Set environment variable
docker exec -e MY_VAR=value container_name env
```

---

## ps

List containers.

### Syntax

```bash
docker ps [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all` | Show all containers (default shows just running) |
| `-f, --filter` | Filter output based on conditions |
| `--format` | Format output using Go template |
| `-n, --last` | Show n last created containers |
| `-q, --quiet` | Only display container IDs |
| `-s, --size` | Display total file sizes |

### Examples

```bash
# List running containers
docker ps

# List all containers
docker ps -a

# List only container IDs
docker ps -q

# List last 5 containers
docker ps -n 5

# Filter by status
docker ps -f status=exited

# Filter by name
docker ps -f name=web

# Custom format
docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"

# Show container sizes
docker ps -s
```

---

## build

Build an image from a Dockerfile.

### Syntax

```bash
docker build [OPTIONS] PATH | URL | -
```

### Common Options

| Option | Description |
|--------|-------------|
| `-t, --tag` | Name and optionally tag (name:tag) |
| `-f, --file` | Name of the Dockerfile |
| `--build-arg` | Set build-time variables |
| `--no-cache` | Do not use cache when building |
| `--target` | Set the target build stage |
| `--platform` | Set platform (linux/amd64, linux/arm64) |
| `-q, --quiet` | Suppress build output |

### Examples

```bash
# Build with tag
docker build -t myapp:latest .

# Build with specific Dockerfile
docker build -f Dockerfile.dev -t myapp:dev .

# Build with build arguments
docker build --build-arg VERSION=1.0 -t myapp .

# Build without cache
docker build --no-cache -t myapp .

# Build specific stage
docker build --target builder -t myapp:builder .

# Build for specific platform
docker build --platform linux/amd64 -t myapp .

# Build from URL
docker build -t myapp https://github.com/user/repo.git
```

---

## bake

Build from a file (Docker Buildx Bake).

### Syntax

```bash
docker buildx bake [OPTIONS] [TARGET...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --file` | Build definition file |
| `--set` | Override target value |
| `--push` | Push to registry |
| `--load` | Load into docker |
| `--no-cache` | Do not use cache |
| `--print` | Print the options without building |

### Examples

```bash
# Build using docker-bake.hcl
docker buildx bake

# Build specific target
docker buildx bake webapp

# Build with specific file
docker buildx bake -f docker-bake.json

# Override a variable
docker buildx bake --set *.platform=linux/amd64

# Print build options without building
docker buildx bake --print

# Build and push
docker buildx bake --push
```

---

## pull

Download an image from a registry.

### Syntax

```bash
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all-tags` | Download all tagged images |
| `--platform` | Set platform (linux/amd64, linux/arm64) |
| `-q, --quiet` | Suppress verbose output |

### Examples

```bash
# Pull latest tag
docker pull nginx

# Pull specific tag
docker pull nginx:1.25

# Pull by digest
docker pull nginx@sha256:abc123...

# Pull all tags
docker pull -a nginx

# Pull for specific platform
docker pull --platform linux/arm64 nginx

# Pull from different registry
docker pull gcr.io/project/image:tag
```

---

## push

Upload an image to a registry.

### Syntax

```bash
docker push [OPTIONS] NAME[:TAG]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all-tags` | Push all tags of an image |
| `-q, --quiet` | Suppress verbose output |

### Examples

```bash
# Push an image
docker push myregistry/myapp:latest

# Push all tags
docker push -a myregistry/myapp

# Push to Docker Hub
docker push username/myapp:v1.0

# Push to private registry
docker push registry.example.com/myapp:latest
```

---

## images

List images.

### Syntax

```bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-a, --all` | Show all images (including intermediate) |
| `-f, --filter` | Filter output based on conditions |
| `--format` | Format output using Go template |
| `-q, --quiet` | Only show image IDs |
| `--digests` | Show digests |

### Examples

```bash
# List all images
docker images

# List only image IDs
docker images -q

# Filter by reference
docker images nginx

# Filter dangling images
docker images -f dangling=true

# Show digests
docker images --digests

# Custom format
docker images --format "{{.Repository}}:{{.Tag}} - {{.Size}}"
```

---

## login

Authenticate to a registry.

### Syntax

```bash
docker login [OPTIONS] [SERVER]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-u, --username` | Username |
| `-p, --password` | Password |
| `--password-stdin` | Take password from stdin |

### Examples

```bash
# Login to Docker Hub (interactive)
docker login

# Login with username
docker login -u username

# Login with password from stdin (secure)
echo $PASSWORD | docker login -u username --password-stdin

# Login to private registry
docker login registry.example.com

# Login to AWS ECR
aws ecr get-login-password | docker login --username AWS --password-stdin 123456789.dkr.ecr.region.amazonaws.com
```

---

## logout

Log out from a registry.

### Syntax

```bash
docker logout [SERVER]
```

### Examples

```bash
# Logout from Docker Hub
docker logout

# Logout from specific registry
docker logout registry.example.com
```

---

## search

Search Docker Hub for images.

### Syntax

```bash
docker search [OPTIONS] TERM
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --filter` | Filter output based on conditions |
| `--format` | Format output using Go template |
| `--limit` | Max number of results (default 25) |
| `--no-trunc` | Don't truncate output |

### Examples

```bash
# Search for images
docker search nginx

# Limit results
docker search --limit 5 nginx

# Filter by stars
docker search -f stars=100 nginx

# Filter official images
docker search -f is-official=true nginx

# Show full description
docker search --no-trunc nginx
```

---

## version

Show the Docker version information.

### Syntax

```bash
docker version [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --format` | Format output using Go template |

### Examples

```bash
# Show version
docker version

# Show only client version
docker version --format '{{.Client.Version}}'

# JSON format
docker version --format '{{json .}}'
```

---

## info

Display system-wide information.

### Syntax

```bash
docker info [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --format` | Format output using Go template |

### Examples

```bash
# Show system info
docker info

# Show specific info
docker info --format '{{.ServerVersion}}'

# Show storage driver
docker info --format '{{.Driver}}'

# JSON format
docker info --format '{{json .}}'
```
