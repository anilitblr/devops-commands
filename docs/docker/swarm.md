# Swarm Commands

## swarm init

Initialize a swarm.

### Syntax

```bash
docker swarm init [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--advertise-addr` | Advertised address |
| `--autolock` | Enable manager autolocking |
| `--cert-expiry` | Validity period for node certificates (default 2160h0m0s) |
| `--data-path-addr` | Address for data path traffic |
| `--data-path-port` | Port for data path traffic (default 4789) |
| `--default-addr-pool` | Default address pool in CIDR format |
| `--dispatcher-heartbeat` | Dispatcher heartbeat period (default 5s) |
| `--external-ca` | External CA |
| `--force-new-cluster` | Force create a new cluster from current state |
| `--listen-addr` | Listen address (default 0.0.0.0:2377) |
| `--max-snapshots` | Number of additional Raft snapshots to retain |
| `--snapshot-interval` | Number of log entries between Raft snapshots (default 10000) |
| `--task-history-limit` | Task history retention limit (default 5) |

### Examples

```bash
# Initialize a swarm
docker swarm init

# Initialize with specific advertise address
docker swarm init --advertise-addr 192.168.1.100

# Initialize with autolock enabled
docker swarm init --autolock

# Initialize with custom address pool
docker swarm init --default-addr-pool 10.10.0.0/16

# Initialize with specific listen address
docker swarm init --listen-addr 0.0.0.0:2377

# Force new cluster (recovery)
docker swarm init --force-new-cluster
```

---

## swarm join

Join a swarm as a node.

### Syntax

```bash
docker swarm join [OPTIONS] HOST:PORT
```

### Common Options

| Option | Description |
|--------|-------------|
| `--advertise-addr` | Advertised address |
| `--availability` | Availability of the node (active, pause, drain) |
| `--data-path-addr` | Address for data path traffic |
| `--listen-addr` | Listen address |
| `--token` | Token for entry into the swarm |

### Examples

```bash
# Join as a worker
docker swarm join --token SWMTKN-1-xxx 192.168.1.100:2377

# Join as a manager
docker swarm join --token SWMTKN-1-xxx-manager 192.168.1.100:2377

# Join with specific advertise address
docker swarm join --advertise-addr 192.168.1.101 --token SWMTKN-1-xxx 192.168.1.100:2377

# Join with drain availability
docker swarm join --availability drain --token SWMTKN-1-xxx 192.168.1.100:2377
```

### Get Join Tokens

```bash
# Get worker join token
docker swarm join-token worker

# Get manager join token
docker swarm join-token manager

# Get only the token (quiet)
docker swarm join-token -q worker

# Rotate worker token
docker swarm join-token --rotate worker
```

---

## swarm leave

Leave the swarm.

### Syntax

```bash
docker swarm leave [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force leave (even if this is the last manager) |

### Examples

```bash
# Leave the swarm (worker)
docker swarm leave

# Force leave (manager)
docker swarm leave --force
```

---

## swarm update

Update the swarm.

### Syntax

```bash
docker swarm update [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `--autolock` | Change manager autolocking setting |
| `--cert-expiry` | Validity period for node certificates |
| `--dispatcher-heartbeat` | Dispatcher heartbeat period |
| `--external-ca` | External CA |
| `--max-snapshots` | Number of additional Raft snapshots to retain |
| `--snapshot-interval` | Number of log entries between Raft snapshots |
| `--task-history-limit` | Task history retention limit |

### Examples

```bash
# Enable autolock
docker swarm update --autolock=true

# Disable autolock
docker swarm update --autolock=false

# Update certificate expiry
docker swarm update --cert-expiry 720h

# Update task history limit
docker swarm update --task-history-limit 10

# Update dispatcher heartbeat
docker swarm update --dispatcher-heartbeat 10s
```

---

## Additional Swarm Management Commands

### Node Management

```bash
# List nodes
docker node ls

# Inspect a node
docker node inspect <node>

# Promote worker to manager
docker node promote <node>

# Demote manager to worker
docker node demote <node>

# Update node availability
docker node update --availability drain <node>

# Remove a node
docker node rm <node>
```

### Service Management

```bash
# Create a service
docker service create --name web -p 80:80 nginx

# List services
docker service ls

# Inspect a service
docker service inspect web

# View service logs
docker service logs web

# Scale a service
docker service scale web=5

# Update a service
docker service update --image nginx:latest web

# Remove a service
docker service rm web
```

### Stack Management

```bash
# Deploy a stack
docker stack deploy -c docker-compose.yml mystack

# List stacks
docker stack ls

# List stack services
docker stack services mystack

# List stack tasks
docker stack ps mystack

# Remove a stack
docker stack rm mystack
```
