# Docker Commands

Quick reference for common Docker commands organized by category.

## Categories

- [Common](docker/common.md) - run, exec, ps, build, bake, pull, push, images, login, logout, search, version, info
- [Container](docker/container.md) - attach, commit, cp, create, diff, export, kill, logs, pause, port, rename, restart, rm, start, stats, stop, top, unpause, update, wait
- [Image](docker/image.md) - history, import, inspect, load, rmi, save, tag
- [Network](docker/network.md) - network create/ls/rm/connect/disconnect/inspect/prune
- [Volume](docker/volume.md) - volume create/ls/rm/inspect/prune
- [Compose](docker/compose.md) - up, down, ps, logs, build, exec, restart, pull
- [System](docker/system.md) - system df/prune/info, events
- [Swarm](docker/swarm.md) - init, join, leave, update

## Quick Reference

### Common

| Command | Description |
|---------|-------------|
| `run` | Create and run a new container from an image |
| `exec` | Execute a command in a running container |
| `ps` | List containers |
| `build` | Build an image from a Dockerfile |
| `bake` | Build from a file |
| `pull` | Download an image from a registry |
| `push` | Upload an image to a registry |
| `images` | List images |
| `login` | Authenticate to a registry |
| `logout` | Log out from a registry |
| `search` | Search Docker Hub for images |
| `version` | Show the Docker version information |
| `info` | Display system-wide information |

### Container

| Command | Description |
|---------|-------------|
| `attach` | Attach local standard input, output, and error streams to a running container |
| `commit` | Create a new image from a container's changes |
| `cp` | Copy files/folders between a container and the local filesystem |
| `create` | Create a new container |
| `diff` | Inspect changes to files or directories on a container's filesystem |
| `export` | Export a container's filesystem as a tar archive |
| `kill` | Kill one or more running containers |
| `logs` | Fetch the logs of a container |
| `pause` | Pause all processes within one or more containers |
| `port` | List port mappings or a specific mapping for the container |
| `rename` | Rename a container |
| `restart` | Restart one or more containers |
| `rm` | Remove one or more containers |
| `start` | Start one or more stopped containers |
| `stats` | Display a live stream of container(s) resource usage statistics |
| `stop` | Stop one or more running containers |
| `top` | Display the running processes of a container |
| `unpause` | Unpause all processes within one or more containers |
| `update` | Update configuration of one or more containers |
| `wait` | Block until one or more containers stop, then print their exit codes |

### Image

| Command | Description |
|---------|-------------|
| `history` | Show the history of an image |
| `import` | Import the contents from a tarball to create a filesystem image |
| `inspect` | Return low-level information on Docker objects |
| `load` | Load an image from a tar archive or STDIN |
| `rmi` | Remove one or more images |
| `save` | Save one or more images to a tar archive |
| `tag` | Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE |

### Network

| Command | Description |
|---------|-------------|
| `network create` | Create a network |
| `network ls` | List networks |
| `network rm` | Remove one or more networks |
| `network connect` | Connect a container to a network |
| `network disconnect` | Disconnect a container from a network |
| `network inspect` | Display detailed information on networks |
| `network prune` | Remove all unused networks |

### Volume

| Command | Description |
|---------|-------------|
| `volume create` | Create a volume |
| `volume ls` | List volumes |
| `volume rm` | Remove one or more volumes |
| `volume inspect` | Display detailed information on volumes |
| `volume prune` | Remove unused local volumes |

### Compose

| Command | Description |
|---------|-------------|
| `compose up` | Create and start containers |
| `compose down` | Stop and remove containers, networks |
| `compose ps` | List containers |
| `compose logs` | View output from containers |
| `compose build` | Build or rebuild services |
| `compose exec` | Execute a command in a running container |
| `compose restart` | Restart service containers |
| `compose pull` | Pull service images |

### System

| Command | Description |
|---------|-------------|
| `system df` | Show Docker disk usage |
| `system prune` | Remove unused data |
| `system info` | Display system-wide information |
| `events` | Get real time events from the server |

### Swarm

| Command | Description |
|---------|-------------|
| `swarm init` | Initialize a swarm |
| `swarm join` | Join a swarm as a node |
| `swarm leave` | Leave the swarm |
| `swarm update` | Update the swarm |
