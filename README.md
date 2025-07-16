                                                       # Docker Node.js Application Guide

A comprehensive guide on how to dockerize a Node.js application with practical examples and common commands.

## Table of Contents
- [Building Docker Images](#building-docker-images)
- [Running Containers](#running-containers)
- [Container Management](#container-management)
- [Image Management](#image-management)
- [Container Inspection](#container-inspection)
- [Environment Variables](#environment-variables)
- [Docker Hub Integration](#docker-hub-integration)
- [Docker Compose](#docker-compose)

## Building Docker Images

### Basic Build Command
```bash
docker build -t youtube-nodejs .
```

**Command Breakdown:**
- `-t` : Tags the image with a name
- `.` : Indicates the Dockerfile is in the current directory

After running this command, a custom image will be created locally. You can view it in Docker Desktop under the "Images" section.

## Running Containers

### Basic Run Command
```bash
docker run -it youtube-nodejs
```

**Note:** This command alone won't make your application accessible from localhost.

### Running with Port Mapping
```bash
docker run -it -p 8000:8000 youtube-nodejs
```

**Command Breakdown:**
- `-it` : Interactive terminal mode
- `-p 8000:8000` : Maps local port 8000 to container port 8000
- Format: `local_port:container_port`

**Access your application:** http://localhost:8000

## Container Management

### Stop a Container
```bash
docker stop <container_id>
```

### Remove a Container
```bash
docker rm <container_id>
```

## Image Management

### Remove an Image
```bash
docker rmi <image_name>
```

## Container Inspection

### Access Container File System
```bash
docker exec -it <container_id> bash
```

**Example:**
```bash
docker exec -it 5f831e50e32f77e428530d9 bash
```

Once inside the container, use `ls` to see the folder structure.

### View Environment Variables
```bash
docker exec -it <container_id> env
```

**Example:**
```bash
docker exec -it 5f831e50e32f77e428530d9 env
```

## Environment Variables

### Running with Custom Environment Variables
```bash
docker run -it -e PORT=4000 -p 4000:4000 youtube-nodejs
```

**Command Breakdown:**
- `-e PORT=4000` : Sets environment variable PORT to 4000
- `-p 4000:4000` : Maps local port 4000 to container port 4000

## Docker Hub Integration

### Push to Docker Hub Repository

1. **Login to Docker Hub:**
   ```bash
   docker login
   ```

2. **Build and Tag Image:**
   ```bash
   docker build -t sanjeebskn/youtube-nodejs .
   ```

3. **Push to Repository:**
   ```bash
   docker push sanjeebskn/youtube-nodejs
   ```

## Docker Compose

Docker Compose is used to define and run multi-container Docker applications using a YAML configuration file.

### Docker Compose File
Create a `docker-compose.yml` file in your project root to define services, networks, and volumes.

### Running with Docker Compose
```bash
# Build and run in detached mode
docker-compose up -d --build

# Alternative command
docker compose up
```

**Command Options:**
- `-d` : Detached mode (runs in background)
- `--build` : Build images before starting containers

### Stopping Docker Compose Services
```bash
# Stop services
docker compose stop

# Stop and remove containers
docker compose down
```

## Quick Reference

| Command | Description |
|---------|-------------|
| `docker build -t <name> .` | Build image with tag |
| `docker run -it -p <local>:<container> <image>` | Run container with port mapping |
| `docker stop <container_id>` | Stop container |
| `docker rm <container_id>` | Remove container |
| `docker rmi <image_name>` | Remove image |
| `docker exec -it <container_id> bash` | Access container shell |
| `docker exec -it <container_id> env` | View environment variables |
| `docker compose up -d --build` | Start services with Docker Compose |
| `docker compose down` | Stop and remove Compose services |

## Prerequisites

- Docker installed on your system
- Node.js application with a Dockerfile
- Docker Hub account (for pushing images)

## Best Practices

1. Always use specific tags for your images
2. Use port mapping to access containerized applications
3. Clean up unused containers and images regularly
4. Use Docker Compose for multi-container applications
5. Store sensitive data in environment variables, not in the image
