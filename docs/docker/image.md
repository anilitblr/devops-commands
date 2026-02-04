# Image Commands

## history

Show the history of an image.

### Syntax

```bash
docker history [OPTIONS] IMAGE
```

### Common Options

| Option | Description |
|--------|-------------|
| `--format` | Format output using Go template |
| `-H, --human` | Print sizes and dates in human readable format (default true) |
| `--no-trunc` | Don't truncate output |
| `-q, --quiet` | Only show image IDs |

### Examples

```bash
# Show image history
docker history nginx

# Show full output
docker history --no-trunc nginx

# Show only layer IDs
docker history -q nginx

# Custom format
docker history --format "{{.ID}}: {{.CreatedBy}}" nginx
```

---

## import

Import the contents from a tarball to create a filesystem image.

### Syntax

```bash
docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-c, --change` | Apply Dockerfile instruction |
| `-m, --message` | Set commit message |
| `--platform` | Set platform |

### Examples

```bash
# Import from tar file
docker import container.tar myimage:latest

# Import from URL
docker import https://example.com/image.tar myimage:latest

# Import from stdin
cat container.tar | docker import - myimage:latest

# Import with Dockerfile changes
docker import -c 'CMD ["bash"]' container.tar myimage:latest

# Import with message
docker import -m "Imported from backup" container.tar myimage:latest
```

---

## inspect

Return low-level information on Docker objects.

### Syntax

```bash
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --format` | Format output using Go template |
| `-s, --size` | Display total file sizes (for containers) |
| `--type` | Return JSON for specified type |

### Examples

```bash
# Inspect an image
docker inspect nginx

# Inspect a container
docker inspect my-container

# Get specific field
docker inspect -f '{{.Config.Env}}' my-container

# Get IP address
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' my-container

# Get image ID
docker inspect -f '{{.Id}}' nginx

# Inspect multiple objects
docker inspect container1 container2 nginx

# Get mount points
docker inspect -f '{{json .Mounts}}' my-container

# Inspect with size info
docker inspect -s my-container
```

---

## load

Load an image from a tar archive or STDIN.

### Syntax

```bash
docker load [OPTIONS]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-i, --input` | Read from tar archive file |
| `-q, --quiet` | Suppress the load output |

### Examples

```bash
# Load from file
docker load -i myimage.tar

# Load from stdin
docker load < myimage.tar

# Load with progress
cat myimage.tar | docker load

# Quiet mode
docker load -q -i myimage.tar
```

---

## rmi

Remove one or more images.

### Syntax

```bash
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force removal |
| `--no-prune` | Do not delete untagged parents |

### Examples

```bash
# Remove an image
docker rmi nginx

# Remove by image ID
docker rmi abc123def

# Force remove
docker rmi -f nginx

# Remove multiple images
docker rmi nginx alpine ubuntu

# Remove all unused images
docker rmi $(docker images -q -f dangling=true)

# Remove all images
docker rmi -f $(docker images -q)
```

---

## save

Save one or more images to a tar archive.

### Syntax

```bash
docker save [OPTIONS] IMAGE [IMAGE...]
```

### Common Options

| Option | Description |
|--------|-------------|
| `-o, --output` | Write to file |

### Examples

```bash
# Save to file
docker save -o nginx.tar nginx

# Save to stdout
docker save nginx > nginx.tar

# Save multiple images
docker save -o images.tar nginx alpine ubuntu

# Save with specific tag
docker save -o myapp.tar myapp:v1.0

# Compress while saving
docker save nginx | gzip > nginx.tar.gz
```

---

## tag

Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE.

### Syntax

```bash
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

### Examples

```bash
# Tag with new name
docker tag nginx my-nginx

# Tag with version
docker tag myapp myapp:v1.0

# Tag for registry
docker tag myapp registry.example.com/myapp:latest

# Tag for Docker Hub
docker tag myapp username/myapp:latest

# Tag specific version for registry
docker tag myapp:v1.0 gcr.io/project/myapp:v1.0
```
