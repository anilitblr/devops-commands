# Network Commands

## network create

Create a network.

### Syntax

```bash
docker network create [OPTIONS] NETWORK
```

### Common Options

| Option | Description |
|--------|-------------|
| `-d, --driver` | Driver to manage the network (default "bridge") |
| `--gateway` | IPv4 or IPv6 gateway for the subnet |
| `--ip-range` | Allocate container IP from a sub-range |
| `--subnet` | Subnet in CIDR format |
| `--ipv6` | Enable IPv6 networking |
| `-o, --opt` | Set driver specific options |
| `--attachable` | Enable manual container attachment |
| `--internal` | Restrict external access to the network |
| `--label` | Set metadata on a network |

### Examples

```bash
# Create a bridge network
docker network create my-network

# Create with specific driver
docker network create -d bridge my-bridge

# Create with subnet
docker network create --subnet 172.20.0.0/16 my-network

# Create with gateway
docker network create --subnet 172.20.0.0/16 --gateway 172.20.0.1 my-network

# Create overlay network (Swarm)
docker network create -d overlay my-overlay

# Create internal network
docker network create --internal my-internal

# Create with driver options
docker network create -o "com.docker.network.bridge.enable_ip_masquerade=true" my-network
```

---

## network ls

List networks.

### Syntax

```bash
docker network ls [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --filter` | Filter output |
| `--format` | Format output using Go template |
| `--no-trunc` | Do not truncate output |
| `-q, --quiet` | Only display network IDs |

### Examples

```bash
# List all networks
docker network ls

# List only network IDs
docker network ls -q

# Filter by driver
docker network ls -f driver=bridge

# Filter by name
docker network ls -f name=my-network

# Custom format
docker network ls --format "{{.Name}}: {{.Driver}}"
```

---

## network rm

Remove one or more networks.

### Syntax

```bash
docker network rm NETWORK [NETWORK...]
```

### Examples

```bash
# Remove a network
docker network rm my-network

# Remove multiple networks
docker network rm network1 network2

# Remove all unused networks
docker network rm $(docker network ls -q -f dangling=true)
```

---

## network connect

Connect a container to a network.

### Syntax

```bash
docker network connect [OPTIONS] NETWORK CONTAINER
```

### Common Options

| Option | Description |
|--------|-------------|
| `--alias` | Add network-scoped alias for the container |
| `--ip` | IPv4 address |
| `--ip6` | IPv6 address |
| `--link` | Add link to another container |

### Examples

```bash
# Connect container to network
docker network connect my-network my-container

# Connect with specific IP
docker network connect --ip 172.20.0.10 my-network my-container

# Connect with alias
docker network connect --alias db my-network my-container

# Connect running container
docker network connect my-network $(docker ps -q -f name=web)
```

---

## network disconnect

Disconnect a container from a network.

### Syntax

```bash
docker network disconnect [OPTIONS] NETWORK CONTAINER
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force the container to disconnect |

### Examples

```bash
# Disconnect container from network
docker network disconnect my-network my-container

# Force disconnect
docker network disconnect -f my-network my-container
```

---

## network inspect

Display detailed information on one or more networks.

### Syntax

```bash
docker network inspect [OPTIONS] NETWORK [NETWORK...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --format` | Format output using Go template |
| `-v, --verbose` | Verbose output for diagnostics |

### Examples

```bash
# Inspect a network
docker network inspect my-network

# Inspect multiple networks
docker network inspect bridge host

# Get specific field
docker network inspect -f '{{.IPAM.Config}}' my-network

# Get containers in network
docker network inspect -f '{{json .Containers}}' my-network

# Get subnet
docker network inspect -f '{{range .IPAM.Config}}{{.Subnet}}{{end}}' my-network
```

---

## network prune

Remove all unused networks.

### Syntax

```bash
docker network prune [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Do not prompt for confirmation |
| `--filter` | Provide filter values |

### Examples

```bash
# Remove unused networks (with prompt)
docker network prune

# Remove without prompt
docker network prune -f

# Remove networks older than 24h
docker network prune -f --filter "until=24h"
```
