# 🐳 Docker — Complete Handbook: Basics to Advanced

> **The ultimate Docker guide for beginners, backend developers, DevOps engineers, and full-stack developers.**
> From your first container to production deployments — everything in one place.

---

## 📌 What is Docker?

**Docker** is an open-source platform that allows you to **package, ship, and run applications inside containers**. A container bundles your application code with everything it needs to run — runtime, libraries, system tools, and configuration — into a single, portable unit.

Before Docker, the classic developer problem was:
> *"It works on my machine."*

After Docker:
> *"Ship the machine."*

### What is Containerization?

**Containerization** is the process of packaging an application and its dependencies into a **container** — a lightweight, isolated environment that runs consistently across any infrastructure.

Think of a container like a **shipping container** on a cargo ship. The contents (your app) are isolated and standardized, so they can be transported to any port (server) and unloaded identically, regardless of what's outside.

### Virtual Machines vs Containers

| Feature | Virtual Machine (VM) | Docker Container |
|---------|----------------------|------------------|
| Boot time | Minutes | Seconds |
| Size | GBs (full OS) | MBs (just the app layer) |
| Isolation | Full hardware virtualization | Process-level isolation |
| Performance | Slower (hypervisor overhead) | Near-native |
| Portability | Heavy | Lightweight |
| OS | Each VM has its own OS | Shares host OS kernel |
| Use case | Full isolation, legacy apps | Microservices, modern apps |

```
Virtual Machine Stack:         Container Stack:
┌─────────────────────┐        ┌──────────────────────┐
│  App A  │  App B    │        │ App A  │ App B  │App C│
├─────────┼───────────┤        ├────────┴────────┴─────┤
│ Guest OS│ Guest OS  │        │      Docker Engine    │
├─────────┴───────────┤        ├───────────────────────┤
│     Hypervisor      │        │       Host OS         │
├─────────────────────┤        ├───────────────────────┤
│      Host OS        │        │     Infrastructure    │
├─────────────────────┤        └───────────────────────┘
│   Infrastructure    │
└─────────────────────┘
```

### Why Use Docker?

- 🚀 **Portability** — Run anywhere: your laptop, a teammate's machine, cloud, CI/CD
- 📦 **Consistency** — Eliminate "works on my machine" problems
- ⚡ **Lightweight** — Containers share the host kernel; no full OS per app
- 🔁 **Scalability** — Spin up multiple identical containers in seconds
- 🔒 **Isolation** — Each container is isolated; no dependency conflicts
- 🔄 **Fast deployment** — Build once, deploy everywhere

---

## 📖 Table of Contents

1. [Docker Architecture](#1-docker-architecture)
2. [Installation](#2-installation)
3. [Docker Core Concepts](#3-docker-core-concepts)
4. [Docker CLI Commands](#4-docker-cli-commands)
5. [Working with Images](#5-working-with-images)
6. [Dockerfile Deep Dive](#6-dockerfile-deep-dive)
7. [Containers In Depth](#7-containers-in-depth)
8. [Docker Volumes](#8-docker-volumes)
9. [Docker Networking](#9-docker-networking)
10. [Docker Compose](#10-docker-compose)
11. [Dockerizing Applications](#11-dockerizing-applications)
12. [Docker with Databases](#12-docker-with-databases)
13. [Docker Hub](#13-docker-hub)
14. [Advanced Docker](#14-advanced-docker)
15. [Security Best Practices](#15-security-best-practices)
16. [Performance Optimization](#16-performance-optimization)
17. [Debugging & Troubleshooting](#17-debugging--troubleshooting)
18. [Docker in Production](#18-docker-in-production)
19. [Docker vs Kubernetes](#19-docker-vs-kubernetes)
20. [Real-World Projects](#20-real-world-projects)
21. [Exercises & Challenges](#21-exercises--challenges)
22. [Conclusion & Resources](#22-conclusion--resources)

---

## 1. Docker Architecture

### How Docker Works

Docker uses a **client-server architecture**:

```
┌─────────────┐         ┌──────────────────────────────────────┐
│ Docker CLI  │─ REST ──▶         Docker Daemon (dockerd)       │
│  (client)   │  API    │                                        │
└─────────────┘         │  ┌─────────┐  ┌────────┐  ┌────────┐ │
                        │  │Containers│  │ Images │  │Volumes │ │
                        │  └─────────┘  └────────┘  └────────┘ │
                        └──────────────────────────────────────┘
                                           │
                                    ┌──────▼──────┐
                                    │  Docker Hub  │
                                    │  (Registry)  │
                                    └─────────────┘
```

### Core Components

| Component | Role |
|-----------|------|
| **Docker Client** | CLI tool you interact with (`docker run`, `docker build`) |
| **Docker Daemon (`dockerd`)** | Background service that manages containers, images, networks |
| **Docker Images** | Read-only templates used to create containers |
| **Docker Containers** | Running instances of images |
| **Docker Registry** | Storage for images (Docker Hub is the public registry) |

### Docker Engine

The **Docker Engine** is the core runtime — it includes:
- `dockerd` — the server-side daemon
- REST API — interface between client and daemon
- Docker CLI — the command-line client

### Docker Desktop

**Docker Desktop** is the GUI application for Mac and Windows. It bundles:
- Docker Engine
- Docker Compose
- Kubernetes (optional)
- Docker Dashboard (visual container management)

---

## 2. Installation

### Linux (Ubuntu/Debian)

```bash
# Update package index
sudo apt-get update

# Install prerequisites
sudo apt-get install -y ca-certificates curl gnupg lsb-release

# Add Docker's official GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Set up the repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Run Docker without sudo (log out and back in after this)
sudo usermod -aG docker $USER
```

### macOS

```bash
# Option 1: Download Docker Desktop from https://docs.docker.com/desktop/mac/
# Option 2: Using Homebrew
brew install --cask docker
```

### Windows

1. Enable WSL 2 (Windows Subsystem for Linux 2)
2. Download Docker Desktop from https://docs.docker.com/desktop/windows/
3. Install and restart

### Verify Installation

```bash
# Check Docker version
docker --version
# Output: Docker version 26.x.x, build abc1234

# Full version info
docker version

# System-wide info
docker info

# Run the hello-world test container
docker run hello-world
```

---

## 3. Docker Core Concepts

### Images

A **Docker image** is a read-only template — a blueprint for containers. It contains the OS layer, runtime, app code, and dependencies, stacked in layers.

```bash
# An image is like a class in OOP
# A container is like an instance of that class

docker pull nginx          # Pull official nginx image
docker images              # List all local images
```

### Containers

A **container** is a running instance of an image. Containers are isolated processes on the host OS.

```bash
docker run nginx           # Create and start a container from the nginx image
docker ps                  # List running containers
docker ps -a               # List ALL containers (including stopped)
```

### Image vs Container

| | Image | Container |
|--|-------|-----------|
| State | Static (read-only) | Dynamic (running/stopped) |
| Analogy | Recipe / Blueprint | The dish / Building |
| Stored | On disk | In memory + thin R/W layer |
| Created by | `docker build` | `docker run` |
| Can be pushed | ✅ Yes | ❌ No (commit first) |

### Volumes

A **volume** is persistent storage that exists outside the container's filesystem. Containers are ephemeral — when they stop, data is lost. Volumes solve this.

```bash
docker volume create mydata
docker run -v mydata:/app/data myapp
```

### Networks

**Docker networks** allow containers to communicate with each other and the outside world.

```bash
docker network ls
docker network create mynetwork
docker run --network mynetwork myapp
```

### Registries

A **registry** is a storage and distribution system for Docker images.

- **Docker Hub** — public registry (hub.docker.com)
- **AWS ECR** — Amazon's private registry
- **GitHub Container Registry** — ghcr.io
- **Self-hosted** — using Docker Registry image

---

## 4. Docker CLI Commands

### System Commands

```bash
docker version            # Show client and server version
docker info               # Display system-wide information
docker system df          # Disk usage by Docker
docker system prune       # Remove all unused data (careful!)
docker system prune -a    # Remove ALL unused images too
```

### Image Commands

```bash
docker images             # List local images
docker images -a          # Include intermediate images
docker pull nginx         # Pull latest nginx
docker pull nginx:1.25    # Pull specific version
docker rmi nginx          # Remove image
docker rmi nginx:1.25     # Remove specific tag
docker image prune        # Remove dangling (untagged) images
docker inspect nginx      # Detailed image info (JSON)
docker history nginx      # Show image layer history
```

### Container Commands

```bash
# Run commands
docker run nginx                      # Run in foreground
docker run -d nginx                   # Run in detached (background) mode
docker run -it ubuntu bash            # Interactive mode with terminal
docker run --name myapp nginx         # Give container a name
docker run -p 8080:80 nginx           # Map host:container port
docker run -e NODE_ENV=production app # Set environment variable
docker run --rm nginx                 # Remove container when it stops

# Lifecycle
docker ps                             # List running containers
docker ps -a                          # All containers
docker stop myapp                     # Graceful stop (SIGTERM)
docker kill myapp                     # Force stop (SIGKILL)
docker start myapp                    # Start stopped container
docker restart myapp                  # Stop then start

# Cleanup
docker rm myapp                       # Remove stopped container
docker rm -f myapp                    # Force remove running container
docker container prune                # Remove all stopped containers

# Interaction
docker exec -it myapp bash            # Open shell in running container
docker exec myapp ls /app             # Run command in container
docker logs myapp                     # View container logs
docker logs -f myapp                  # Follow (tail) logs
docker logs --tail 50 myapp           # Last 50 lines
docker stats                          # Live resource usage
docker stats myapp                    # Resource usage for one container
docker inspect myapp                  # Full container details (JSON)
docker cp myapp:/app/file.txt ./      # Copy file from container
docker cp ./file.txt myapp:/app/      # Copy file into container
```

### Quick Reference Card

```bash
# Build → Run → Stop → Remove workflow
docker build -t myapp .               # Build image from Dockerfile
docker run -d -p 3000:3000 myapp      # Run in background
docker stop $(docker ps -q)           # Stop all running containers
docker rm $(docker ps -aq)            # Remove all containers
docker rmi $(docker images -q)        # Remove all images
```

---

## 5. Working with Images

### Pulling Images

```bash
# Pull from Docker Hub (default registry)
docker pull ubuntu              # Latest Ubuntu
docker pull ubuntu:22.04        # Specific version (always pin versions in production)
docker pull node:20-alpine      # Node.js on Alpine Linux (smaller image)

# Pull from other registries
docker pull ghcr.io/owner/repo:tag
docker pull public.ecr.aws/nginx/nginx:latest
```

### Tagging Images

```bash
# Tag format: registry/username/imagename:version
docker tag myapp:latest myusername/myapp:1.0.0
docker tag myapp:latest myusername/myapp:latest

# Retag for a different registry
docker tag myapp:latest ghcr.io/myusername/myapp:latest
```

### Building Images

```bash
# Build from Dockerfile in current directory
docker build -t myapp .

# Build with specific Dockerfile
docker build -f Dockerfile.prod -t myapp:prod .

# Build with build arguments
docker build --build-arg NODE_ENV=production -t myapp .

# Build with no cache (forces fresh build)
docker build --no-cache -t myapp .
```

### Pushing Images to Docker Hub

```bash
# Login
docker login

# Push
docker push myusername/myapp:1.0.0
docker push myusername/myapp:latest
```

---

## 6. Dockerfile Deep Dive

### What is a Dockerfile?

A **Dockerfile** is a text file containing a series of instructions that Docker uses to build an image. Each instruction creates a new **layer** in the image.

### Full Dockerfile Reference

```dockerfile
# ─────────────────────────────────────────
# FROM — Set the base image (always first)
# ─────────────────────────────────────────
FROM node:20-alpine
# Use specific versions for reproducibility (never just "node:latest" in production)

# ─────────────────────────────────────────
# ARG — Build-time variables (NOT available at runtime)
# ─────────────────────────────────────────
ARG NODE_ENV=production
ARG APP_VERSION=1.0.0
# Usage: docker build --build-arg NODE_ENV=development .

# ─────────────────────────────────────────
# ENV — Runtime environment variables
# ─────────────────────────────────────────
ENV NODE_ENV=production
ENV PORT=3000
ENV APP_HOME=/app
# Available to the running container

# ─────────────────────────────────────────
# WORKDIR — Set working directory for subsequent commands
# ─────────────────────────────────────────
WORKDIR /app
# Creates /app if it doesn't exist. Prefer this over: RUN cd /app

# ─────────────────────────────────────────
# COPY — Copy files from host to image
# ─────────────────────────────────────────
COPY package*.json ./
# Copy package.json and package-lock.json first (layer caching trick)

COPY . .
# Copy everything else

# ─────────────────────────────────────────
# ADD — Like COPY but with extra powers (rarely needed)
# ─────────────────────────────────────────
ADD https://example.com/file.tar.gz /app/
# ADD can: fetch URLs and auto-extract .tar.gz files
# Prefer COPY for local files — it's explicit

# ─────────────────────────────────────────
# RUN — Execute commands during BUILD (creates a layer)
# ─────────────────────────────────────────
RUN npm ci --only=production
# Use npm ci (not npm install) in Docker — it's faster and uses package-lock.json

# Chain commands to reduce layers
RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*
# Clean up in the SAME RUN to keep layer small

# ─────────────────────────────────────────
# EXPOSE — Document which port the container listens on
# ─────────────────────────────────────────
EXPOSE 3000
# This is documentation only — it doesn't actually publish the port
# Use -p flag with docker run to publish: docker run -p 3000:3000 myapp

# ─────────────────────────────────────────
# CMD — Default command to run when container starts
# ─────────────────────────────────────────
CMD ["node", "server.js"]
# Exec form (preferred) — runs node directly, no shell overhead
# Can be overridden: docker run myapp node other-script.js

# ─────────────────────────────────────────
# ENTRYPOINT — Fixed command (CMD becomes arguments to it)
# ─────────────────────────────────────────
ENTRYPOINT ["node"]
CMD ["server.js"]
# Result: container runs "node server.js"
# docker run myapp other.js → runs "node other.js"
```

### CMD vs ENTRYPOINT

| | `CMD` | `ENTRYPOINT` |
|--|-------|--------------|
| Purpose | Default command | Fixed executable |
| Overridable | ✅ Yes (easy) | Partial (`--entrypoint` flag) |
| Used together | Provides default args to ENTRYPOINT | Sets the executable |
| Shell form | `CMD npm start` | `ENTRYPOINT npm start` |
| Exec form | `CMD ["npm", "start"]` | `ENTRYPOINT ["npm", "start"]` |

```dockerfile
# Pattern 1: CMD only (most common for apps)
CMD ["node", "server.js"]

# Pattern 2: ENTRYPOINT + CMD (for tools/CLIs)
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["postgres"]
# Runs: docker-entrypoint.sh postgres
# Override: docker run myimage mysql → runs: docker-entrypoint.sh mysql

# Pattern 3: ENTRYPOINT only
ENTRYPOINT ["node", "server.js"]
# Container always runs node server.js — no overriding the command
```

### COPY vs ADD

| | `COPY` | `ADD` |
|--|--------|-------|
| Copy local files | ✅ Yes | ✅ Yes |
| Fetch from URL | ❌ No | ✅ Yes |
| Auto-extract tar | ❌ No | ✅ Yes |
| Recommended | ✅ Prefer this | Only when you need tar extraction |
| Transparency | Explicit | Less predictable |

> ✅ **Rule of thumb:** Always use `COPY` unless you specifically need URL fetching or tar auto-extraction.

### .dockerignore

Like `.gitignore` — prevents unnecessary files from being sent to the build context:

```
# .dockerignore
node_modules
.git
.env
*.log
dist
coverage
.DS_Store
README.md
Dockerfile*
docker-compose*
```

> ⚠️ **Common Mistake:** Forgetting `.dockerignore`. Without it, `node_modules` (often hundreds of MB) gets sent to the build context on every build.

---

## 7. Containers In Depth

### Running Containers

```bash
# Basic run
docker run nginx

# Named container
docker run --name web-server nginx

# Detached mode (background)
docker run -d --name web-server nginx

# Interactive mode (for debugging, running shells)
docker run -it ubuntu bash
docker run -it --rm python:3.12 python  # --rm removes container on exit

# Port mapping: -p hostPort:containerPort
docker run -d -p 8080:80 nginx         # Access nginx at localhost:8080
docker run -d -p 3000:3000 -p 4000:4000 myapp  # Multiple ports
```

### Environment Variables

```bash
# Single variable
docker run -e DATABASE_URL="postgresql://localhost/mydb" myapp

# Multiple variables
docker run \
  -e NODE_ENV=production \
  -e PORT=3000 \
  -e API_KEY=secret \
  myapp

# From a file
docker run --env-file .env myapp
```

### Container Lifecycle

```
Created → Running → Paused → Running → Stopped → Removed
           ↑                              ↓
         start                          stop
                                          ↓
                                       (rm to delete)
```

```bash
docker create --name myapp nginx      # Create but don't start
docker start myapp                    # Start created container
docker pause myapp                    # Pause (freeze) container
docker unpause myapp                  # Resume
docker stop myapp                     # Graceful shutdown (SIGTERM, waits 10s, then SIGKILL)
docker kill myapp                     # Immediate kill (SIGKILL)
docker rm myapp                       # Delete stopped container
```

---

## 8. Docker Volumes

### Why Volumes?

Containers are **ephemeral** — when a container is removed, all data inside is lost. Volumes provide persistent storage that survives container restarts and removals.

### Types of Storage

| Type | Definition | Use Case |
|------|-----------|----------|
| **Named Volume** | Docker-managed storage at `/var/lib/docker/volumes/` | Databases, persistent app data |
| **Bind Mount** | Mount a host directory into the container | Dev: live code reload |
| **tmpfs Mount** | In-memory storage (Linux only) | Sensitive temp data |

### Named Volumes

```bash
# Create a volume
docker volume create mydata

# List volumes
docker volume ls

# Inspect a volume
docker volume inspect mydata

# Use in container
docker run -d \
  --name postgres-db \
  -v mydata:/var/lib/postgresql/data \
  postgres:16

# Remove volume (only when no containers use it)
docker volume rm mydata

# Remove all unused volumes
docker volume prune
```

### Bind Mounts

```bash
# Mount current directory into container (great for development)
docker run -d \
  -v $(pwd):/app \            # Bind mount: host path:container path
  -p 3000:3000 \
  node:20

# Using absolute path
docker run -v /home/user/myapp:/app node:20
```

### Volume vs Bind Mount

| | Named Volume | Bind Mount |
|--|-------------|------------|
| Managed by | Docker | Host OS |
| Path | Docker chooses | You specify host path |
| Portability | ✅ Portable | ❌ Host-specific |
| Performance | Better | Good |
| Best for | Production data | Development |
| Backed up | Needs manual setup | Easy (it's a folder) |

### Volume Best Practices

- ✅ Always use named volumes for databases in production
- ✅ Use bind mounts during development for live reloading
- ✅ Name volumes descriptively: `postgres-data`, `redis-cache`
- ✅ Back up volume data before removing containers
- ❌ Never store sensitive data in unnamed (anonymous) volumes

---

## 9. Docker Networking

### Default Networks

```bash
docker network ls
# NETWORK ID   NAME      DRIVER    SCOPE
# abc123       bridge    bridge    local   ← default for containers
# def456       host      host      local
# ghi789       none      null      local
```

### Network Types

#### Bridge Network (Default)

Containers on the same bridge network can communicate by container name. The default bridge doesn't support DNS by container name — use a **custom bridge**.

```bash
# Create custom bridge network (supports DNS)
docker network create mynetwork

# Connect containers to it
docker run -d --name app --network mynetwork myapp
docker run -d --name db --network mynetwork postgres

# "app" can reach "db" by hostname: db:5432
```

#### Host Network

Container uses the host's network directly — no isolation.

```bash
docker run --network host nginx
# nginx now listens on host port 80 directly
# Good for performance-critical apps, bad for isolation
```

#### Overlay Network

Used in Docker Swarm for multi-host container communication.

```bash
docker network create --driver overlay myoverlay
```

### Container Communication

```bash
# Without custom network — communicate by IP (fragile)
docker inspect container_name | grep IPAddress

# With custom network — communicate by name (recommended)
docker network create backend
docker run -d --name api --network backend myapi
docker run -d --name db --network backend postgres

# From inside "api" container:
# psql -h db -U postgres   ← "db" resolves to the postgres container's IP
```

### Connecting to Multiple Networks

```bash
# Container starts on network1
docker run -d --name myapp --network network1 myimage

# Connect it to network2 also
docker network connect network2 myapp

# Disconnect
docker network disconnect network1 myapp
```

---

## 10. Docker Compose

### What is Docker Compose?

**Docker Compose** is a tool for defining and running **multi-container applications** with a single YAML file. Instead of running multiple `docker run` commands, you declare everything in `docker-compose.yml`.

### Basic docker-compose.yml

```yaml
# docker-compose.yml
version: '3.8'

services:
  # Service 1: Node.js API
  api:
    build: .                          # Build from Dockerfile in current dir
    container_name: my-api
    ports:
      - "3000:3000"                   # host:container
    environment:
      - NODE_ENV=development
      - DATABASE_URL=postgresql://postgres:password@db:5432/mydb
    volumes:
      - .:/app                        # Bind mount for dev (live reload)
      - /app/node_modules             # Prevent host node_modules from overriding
    depends_on:
      - db                            # Start db first
    networks:
      - backend
    restart: unless-stopped

  # Service 2: PostgreSQL Database
  db:
    image: postgres:16-alpine         # Use official image
    container_name: my-postgres
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    volumes:
      - postgres-data:/var/lib/postgresql/data  # Named volume
    networks:
      - backend
    ports:
      - "5432:5432"                   # Expose to host (dev only)

  # Service 3: Redis Cache
  redis:
    image: redis:7-alpine
    container_name: my-redis
    networks:
      - backend

# Named volumes (Docker manages these)
volumes:
  postgres-data:

# Custom networks
networks:
  backend:
    driver: bridge
```

### Docker Compose Commands

```bash
# Start all services (build if needed)
docker compose up

# Start in detached mode (background)
docker compose up -d

# Build images without starting
docker compose build

# Rebuild images (even if unchanged)
docker compose build --no-cache

# Stop all services
docker compose down

# Stop and remove volumes (⚠️ destroys data)
docker compose down -v

# View running services
docker compose ps

# View logs
docker compose logs
docker compose logs -f api          # Follow API service logs

# Run a command in a service
docker compose exec api bash
docker compose exec db psql -U postgres

# Scale a service (run multiple instances)
docker compose up -d --scale api=3

# Restart a specific service
docker compose restart api
```

### Environment Variables in Compose

```yaml
# Method 1: Inline
environment:
  - NODE_ENV=production
  - PORT=3000

# Method 2: From .env file (automatic — Compose reads .env by default)
env_file:
  - .env
  - .env.local

# Method 3: Variable substitution (from host environment or .env)
environment:
  - DATABASE_URL=${DATABASE_URL}
```

```bash
# .env file
DATABASE_URL=postgresql://postgres:password@db:5432/mydb
REDIS_URL=redis://redis:6379
NODE_ENV=development
```

### Docker Compose vs Docker Swarm

| | Docker Compose | Docker Swarm |
|--|---------------|--------------|
| Scope | Single host | Multi-host cluster |
| Scaling | Manual (`--scale`) | Automated |
| Load balancing | ❌ | ✅ Built-in |
| Health management | Basic | Advanced |
| Use case | Development, single server | Production clusters |
| Complexity | Low | Medium |

---

## 11. Dockerizing Applications

### Node.js / Express.js App

```dockerfile
# Dockerfile (Development)
FROM node:20-alpine

WORKDIR /app

# Copy dependencies first (layer caching)
COPY package*.json ./
RUN npm ci

# Copy source
COPY . .

EXPOSE 3000

CMD ["node", "src/index.js"]
```

```dockerfile
# Dockerfile (Production — multi-stage)
# Stage 1: Build
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# Stage 2: Runtime (clean, small image)
FROM node:20-alpine AS runtime
WORKDIR /app

# Copy only production dependencies from builder
COPY --from=builder /app/node_modules ./node_modules
COPY . .

# Run as non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

EXPOSE 3000
CMD ["node", "src/index.js"]
```

### React App

```dockerfile
# Dockerfile for React (with Nginx serving)
# Stage 1: Build
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build                   # Produces /app/dist or /app/build

# Stage 2: Serve with Nginx
FROM nginx:alpine AS runtime
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

```nginx
# nginx.conf
events {}
http {
  server {
    listen 80;
    root /usr/share/nginx/html;
    index index.html;

    # Handle React Router (SPA)
    location / {
      try_files $uri $uri/ /index.html;
    }
  }
}
```

### Next.js App

```dockerfile
FROM node:20-alpine AS base

# Dependencies
FROM base AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

# Build
FROM base AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

# Runtime
FROM base AS runner
WORKDIR /app
ENV NODE_ENV=production

RUN addgroup -S nodejs && adduser -S nextjs -G nodejs
COPY --from=builder /app/public ./public
COPY --from=builder --chown=nextjs:nodejs /app/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static

USER nextjs
EXPOSE 3000
ENV PORT=3000
CMD ["node", "server.js"]
```

---

## 12. Docker with Databases

### PostgreSQL

```bash
# Quick start
docker run -d \
  --name postgres \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=mydb \
  -v postgres-data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:16-alpine

# Connect to it
docker exec -it postgres psql -U admin -d mydb
```

### MySQL

```bash
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=rootpassword \
  -e MYSQL_DATABASE=mydb \
  -e MYSQL_USER=user \
  -e MYSQL_PASSWORD=password \
  -v mysql-data:/var/lib/mysql \
  -p 3306:3306 \
  mysql:8.0

# Connect
docker exec -it mysql mysql -u user -p mydb
```

### MongoDB

```bash
docker run -d \
  --name mongodb \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=secret \
  -v mongo-data:/data/db \
  -p 27017:27017 \
  mongo:7

# Connect
docker exec -it mongodb mongosh -u admin -p secret
```

### Redis

```bash
docker run -d \
  --name redis \
  -v redis-data:/data \
  -p 6379:6379 \
  redis:7-alpine redis-server --appendonly yes  # Enable persistence

# Connect
docker exec -it redis redis-cli
```

### Full Stack: PostgreSQL + Node.js + Redis

```yaml
# docker-compose.yml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "3000:3000"
    environment:
      DATABASE_URL: postgresql://postgres:secret@db:5432/mydb
      REDIS_URL: redis://redis:6379
    depends_on:
      - db
      - redis
    networks:
      - app-network

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: mydb
    volumes:
      - postgres-data:/var/lib/postgresql/data
    networks:
      - app-network

  redis:
    image: redis:7-alpine
    volumes:
      - redis-data:/data
    networks:
      - app-network

volumes:
  postgres-data:
  redis-data:

networks:
  app-network:
```

---

## 13. Docker Hub

### Setup

```bash
# Create account at hub.docker.com, then:
docker login
# Enter username and password

# Login with token (more secure)
docker login -u myusername --password-stdin <<< "my-access-token"
```

### Push an Image

```bash
# Tag your image with your Docker Hub username
docker tag myapp myusername/myapp:1.0.0
docker tag myapp myusername/myapp:latest

# Push
docker push myusername/myapp:1.0.0
docker push myusername/myapp:latest
```

### Image Versioning Best Practices

```bash
# Use semantic versioning
docker tag myapp myusername/myapp:1.0.0     # Major.Minor.Patch
docker tag myapp myusername/myapp:1.0       # Minor tag (points to latest patch)
docker tag myapp myusername/myapp:1         # Major tag
docker tag myapp myusername/myapp:latest    # Always latest

# For CI/CD: tag with Git commit SHA for traceability
docker tag myapp myusername/myapp:$(git rev-parse --short HEAD)
```

---

## 14. Advanced Docker

### Multi-Stage Builds

Multi-stage builds produce **smaller final images** by separating the build environment from the runtime environment.

```dockerfile
# Without multi-stage: node:20 = ~1GB
# With multi-stage: node:20-alpine runtime = ~150MB

# Stage 1: Install and compile
FROM node:20 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build          # Compile TypeScript, etc.

# Stage 2: Production runtime
FROM node:20-alpine AS production
WORKDIR /app
# Copy ONLY what's needed from the builder stage
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package.json .

RUN adduser -D appuser
USER appuser

EXPOSE 3000
CMD ["node", "dist/index.js"]
```

```bash
# Build the final (production) stage only
docker build --target production -t myapp:prod .

# Build a specific intermediate stage (for debugging)
docker build --target builder -t myapp:debug .
```

### Health Checks

```dockerfile
# In Dockerfile
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1
```

```yaml
# In docker-compose.yml
services:
  api:
    image: myapp
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 10s
```

```bash
# Check health status
docker inspect --format='{{.State.Health.Status}}' myapp
# Output: healthy | unhealthy | starting
```

### Resource Limits

```yaml
# docker-compose.yml
services:
  api:
    image: myapp
    deploy:
      resources:
        limits:
          cpus: '0.5'        # 50% of one CPU core
          memory: 512M        # Maximum 512MB RAM
        reservations:
          cpus: '0.25'
          memory: 256M
```

```bash
# docker run
docker run -d \
  --memory="512m" \
  --cpus="0.5" \
  myapp
```

### Docker Secrets (Swarm Mode)

```bash
# Create a secret
echo "my-super-secret-db-password" | docker secret create db_password -

# Use in service
docker service create \
  --name myapp \
  --secret db_password \
  myimage

# Inside container, secret is at /run/secrets/db_password
```

### Docker Swarm (Orchestration)

```bash
# Initialize Swarm
docker swarm init

# Deploy a stack (like compose, but on a cluster)
docker stack deploy -c docker-compose.yml mystack

# Scale a service
docker service scale mystack_api=5

# List services
docker service ls
docker service ps mystack_api
```

---

## 15. Security Best Practices

### Non-Root Containers

```dockerfile
# ❌ Bad — runs as root by default
FROM node:20
RUN npm install -g myapp
CMD ["myapp"]

# ✅ Good — run as non-root user
FROM node:20-alpine
WORKDIR /app
COPY . .
RUN npm ci --only=production

# Create and switch to non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

CMD ["node", "server.js"]
```

### Secrets Management

```bash
# ❌ Never bake secrets into images
ENV API_KEY=secret123      # This is stored in image history!

# ✅ Pass secrets at runtime
docker run -e API_KEY=$API_KEY myapp

# ✅ Use Docker secrets (Swarm) or mounted secret files
docker run -v /run/secrets:/run/secrets:ro myapp
```

### Image Scanning

```bash
# Scan for vulnerabilities with Docker Scout (built-in)
docker scout cves myimage:latest

# Or use Trivy (open source)
trivy image myimage:latest

# Or Snyk
snyk container test myimage:latest
```

### Secure Dockerfile Patterns

```dockerfile
FROM node:20-alpine

# Pin exact versions
RUN apk add --no-cache curl=8.5.0-r0

# Avoid storing secrets in layers
# ❌ Bad
RUN curl -H "Authorization: Bearer secret" https://api.example.com

# ✅ Use build secrets (BuildKit)
# docker build --secret id=mytoken,src=token.txt .
RUN --mount=type=secret,id=mytoken \
    TOKEN=$(cat /run/secrets/mytoken) && \
    curl -H "Authorization: Bearer $TOKEN" https://api.example.com

# Read-only filesystem
# (set in docker run or compose)
```

```bash
# Run container with read-only filesystem
docker run --read-only --tmpfs /tmp myapp
```

---

## 16. Performance Optimization

### Layer Caching

Docker caches each layer. If a layer's instruction hasn't changed, Docker reuses the cache. **Order matters.**

```dockerfile
# ❌ Bad — changing any source file invalidates npm install cache
COPY . .
RUN npm install

# ✅ Good — npm install is cached unless package.json changes
COPY package*.json ./
RUN npm install        # Cached unless package files change
COPY . .               # Source changes here don't bust the npm cache
```

### Use Alpine Images

```dockerfile
# node:20 → ~1.1 GB
FROM node:20

# node:20-slim → ~240 MB
FROM node:20-slim

# node:20-alpine → ~130 MB (based on Alpine Linux — tiny musl libc)
FROM node:20-alpine
```

> ⚠️ **Caveat:** Alpine uses `musl libc` instead of `glibc`. Some npm packages with native bindings may need extra setup. Test before committing to Alpine.

### Minimize Layers

```dockerfile
# ❌ Separate RUN commands = separate layers
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y git
RUN rm -rf /var/lib/apt/lists/*

# ✅ Chain commands = one layer
RUN apt-get update && \
    apt-get install -y curl git && \
    rm -rf /var/lib/apt/lists/*
```

### Use .dockerignore

```
# .dockerignore — always include this
node_modules
.git
.env
*.log
dist
coverage
.next
__pycache__
*.pyc
```

### BuildKit (Faster Builds)

```bash
# Enable BuildKit (default in Docker Desktop)
DOCKER_BUILDKIT=1 docker build -t myapp .

# Or set permanently in Docker daemon config
# /etc/docker/daemon.json
{ "features": { "buildkit": true } }
```

---

## 17. Debugging & Troubleshooting

### Viewing Logs

```bash
# All logs
docker logs myapp

# Follow (like tail -f)
docker logs -f myapp

# Last N lines
docker logs --tail 100 myapp

# With timestamps
docker logs -t myapp

# Since a time
docker logs --since "2024-01-01T00:00:00" myapp
```

### Inspecting Containers

```bash
# Full JSON metadata
docker inspect myapp

# Get specific fields with format
docker inspect --format='{{.State.Status}}' myapp
docker inspect --format='{{.NetworkSettings.IPAddress}}' myapp
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' myapp

# Check environment variables
docker inspect --format='{{range .Config.Env}}{{println .}}{{end}}' myapp
```

### Getting a Shell Inside

```bash
# Running container
docker exec -it myapp bash        # If bash is available
docker exec -it myapp sh          # Alpine uses sh, not bash
docker exec -it myapp /bin/sh

# Start a stopped container interactively
docker start -ai myapp

# Override entrypoint to get a shell (debug a failing container)
docker run -it --entrypoint sh myimage
```

### Common Errors & Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `port is already allocated` | Host port in use | Change `-p` mapping or stop the conflicting process |
| `No such image` | Image not built/pulled | `docker pull` or `docker build` |
| `OCI runtime exec failed` | Command not found in container | Use `sh` instead of `bash` for Alpine |
| `Permission denied` | Running as wrong user | Check USER instruction, volume permissions |
| `cannot connect to Docker daemon` | Docker not running | Start Docker Desktop or `sudo systemctl start docker` |
| `no space left on device` | Docker disk full | `docker system prune` |
| Container exits immediately | CMD fails / app crashes | `docker logs myapp` to see error |

### Port Conflicts

```bash
# Find what's using a port
lsof -i :3000        # macOS/Linux
netstat -ano | findstr :3000  # Windows

# Kill the process or use a different host port
docker run -p 3001:3000 myapp  # Use 3001 on host instead
```

---

## 18. Docker in Production

### Production Best Practices

```dockerfile
# Production Dockerfile checklist:
FROM node:20-alpine                    # ✅ Small base image
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production           # ✅ No devDependencies
COPY . .
RUN adduser -D appuser && \
    chown -R appuser:appuser /app      # ✅ Non-root user
USER appuser
HEALTHCHECK CMD curl -f http://localhost:3000/health || exit 1  # ✅ Health check
EXPOSE 3000
CMD ["node", "src/index.js"]
```

```yaml
# Production compose
services:
  api:
    image: myusername/myapp:1.2.3    # ✅ Pin exact version
    restart: unless-stopped           # ✅ Auto-restart on crash
    read_only: true                   # ✅ Read-only filesystem
    tmpfs:
      - /tmp                          # ✅ Writable temp dir
    environment:
      NODE_ENV: production
    deploy:
      resources:
        limits:
          memory: 512M                # ✅ Memory limits
    logging:
      driver: "json-file"
      options:
        max-size: "10m"               # ✅ Log rotation
        max-file: "3"
```

### Docker with GitHub Actions (CI/CD)

```yaml
# .github/workflows/docker.yml
name: Build and Push Docker Image

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: |
            myusername/myapp:latest
            myusername/myapp:${{ github.sha }}
          cache-from: type=gha          # GitHub Actions cache
          cache-to: type=gha,mode=max
```

---

## 19. Docker vs Kubernetes

| Feature | Docker / Compose | Kubernetes |
|---------|-----------------|------------|
| Scope | Single host | Multi-host cluster |
| Orchestration | Basic (Swarm) | Advanced |
| Auto-scaling | ❌ Manual | ✅ Horizontal Pod Autoscaler |
| Self-healing | ❌ Basic restart | ✅ Full pod rescheduling |
| Load balancing | ❌ External needed | ✅ Built-in Service |
| Rolling updates | ❌ Manual | ✅ Automated |
| Learning curve | Low | High |
| Setup complexity | Minutes | Hours/days |
| Cost | Low | Higher |

### When to Use What

**Use Docker Compose when:**
- Single server deployment
- Development environments
- Small apps with 2-5 services
- You want simplicity

**Use Kubernetes when:**
- High availability is required
- You need auto-scaling
- Multi-region deployment
- 10+ services / microservices
- Team has DevOps expertise

> 💡 **Reality check:** Most startups and mid-size apps run fine on Docker Compose on a single server. Don't add Kubernetes complexity prematurely.

---

## 20. Real-World Projects

### Project 1: Dockerized REST API with PostgreSQL + Prisma

```yaml
# docker-compose.yml
version: '3.8'

services:
  api:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: rest-api
    ports:
      - "3000:3000"
    environment:
      DATABASE_URL: postgresql://postgres:secret@db:5432/appdb
      NODE_ENV: development
    volumes:
      - .:/app
      - /app/node_modules
    depends_on:
      db:
        condition: service_healthy      # Wait for DB health check to pass
    networks:
      - app-network
    command: npm run dev

  db:
    image: postgres:16-alpine
    container_name: postgres
    environment:
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: appdb
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - app-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  pgdata:

networks:
  app-network:
```

### Project 2: Nginx Reverse Proxy Setup

```yaml
version: '3.8'

services:
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./certbot/conf:/etc/letsencrypt:ro
    depends_on:
      - api
    networks:
      - frontend

  api:
    build: ./api
    expose:
      - "3000"              # Only expose internally, NOT to host
    networks:
      - frontend
      - backend

  db:
    image: postgres:16-alpine
    networks:
      - backend             # DB only accessible from backend network

networks:
  frontend:
  backend:
```

```nginx
# nginx/nginx.conf
events { worker_connections 1024; }

http {
  upstream api {
    server api:3000;        # "api" resolves to the api container
  }

  server {
    listen 80;
    server_name example.com;

    location / {
      proxy_pass http://api;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
  }
}
```

### Project 3: Microservices Setup

```yaml
version: '3.8'

services:
  # API Gateway
  gateway:
    build: ./gateway
    ports:
      - "80:3000"
    environment:
      USER_SERVICE_URL: http://users:3001
      ORDER_SERVICE_URL: http://orders:3002

  # User Service
  users:
    build: ./services/users
    expose:
      - "3001"
    environment:
      DATABASE_URL: postgresql://postgres:secret@users-db:5432/users
    depends_on:
      - users-db

  # Order Service
  orders:
    build: ./services/orders
    expose:
      - "3002"
    environment:
      DATABASE_URL: postgresql://postgres:secret@orders-db:5432/orders
    depends_on:
      - orders-db

  # Redis (shared message queue)
  redis:
    image: redis:7-alpine

  users-db:
    image: postgres:16-alpine
    environment:
      POSTGRES_DB: users
      POSTGRES_PASSWORD: secret
    volumes:
      - users-data:/var/lib/postgresql/data

  orders-db:
    image: postgres:16-alpine
    environment:
      POSTGRES_DB: orders
      POSTGRES_PASSWORD: secret
    volumes:
      - orders-data:/var/lib/postgresql/data

volumes:
  users-data:
  orders-data:
```

---

## 21. Exercises & Challenges

### 🟢 Beginner Exercises

1. **Hello Docker**: Run the `hello-world` container. Then run an `ubuntu` container interactively and explore the filesystem.

2. **Nginx Web Server**: Run an nginx container, map port 8080 to 80, and visit it in your browser.

3. **Environment Variables**: Run a `node:20-alpine` container with `NODE_ENV=development` set. Exec into it and verify the variable.

4. **Your First Dockerfile**: Write a Dockerfile for a simple Node.js app that prints "Hello from Docker!" when run.

### 🟡 Intermediate Exercises

5. **Volume Persistence**: Run a PostgreSQL container with a named volume. Insert data, stop and remove the container, start a new one with the same volume, and verify the data persists.

6. **Custom Network**: Create two containers on a custom network. Verify they can reach each other by container name using `ping` or `curl`.

7. **Docker Compose Setup**: Write a `docker-compose.yml` for a Node.js API + PostgreSQL + Redis stack. Include health checks for the database.

8. **Layer Caching**: Build an image, change a source file (not package.json), rebuild. Observe which layers are cached. Then change package.json and rebuild — observe the difference.

### 🔴 Advanced Exercises

9. **Multi-Stage Build**: Dockerize a TypeScript project with a multi-stage build. Stage 1 compiles TypeScript; Stage 2 runs the compiled JS on `node:alpine`. Compare the image sizes.

10. **Nginx Reverse Proxy**: Set up a full stack with Nginx as a reverse proxy in front of a Node.js API. The API should only be accessible through Nginx, not directly from the host.

11. **GitHub Actions CI/CD**: Create a GitHub Actions workflow that builds a Docker image on every push to `main`, runs tests inside the container, and pushes to Docker Hub if tests pass.

12. **Security Audit**: Take a Dockerfile you wrote earlier, identify every security issue (running as root, no .dockerignore, using `latest`, no health check), and fix all of them.

---

## 22. Conclusion & Resources

### 🗺️ Docker Learning Roadmap

```
Week 1: Foundations
  ├── Install Docker
  ├── Core concepts (image, container, volume, network)
  ├── Basic CLI commands
  └── Run pre-built images (nginx, postgres, redis)

Week 2: Building Images
  ├── Write your first Dockerfile
  ├── Dockerfile instructions (FROM, RUN, CMD, COPY, etc.)
  ├── Layer caching
  └── .dockerignore

Week 3: Compose & Networking
  ├── Docker Compose basics
  ├── Multi-container apps
  ├── Custom networks
  └── Volumes and persistence

Week 4: Production & Advanced
  ├── Multi-stage builds
  ├── Security hardening
  ├── Health checks & resource limits
  └── CI/CD with GitHub Actions
```

### 💡 Interview Tips

- **"What's the difference between CMD and ENTRYPOINT?"** → CMD provides defaults that can be overridden; ENTRYPOINT sets the fixed executable. Used together: ENTRYPOINT is the binary, CMD is default arguments.
- **"How do containers differ from VMs?"** → Containers share the host kernel and are process-isolated; VMs run a full OS via a hypervisor. Containers are faster and lighter.
- **"What is a Docker layer?"** → Each instruction in a Dockerfile creates a read-only layer. Layers are cached and shared between images.
- **"What's the N+1 problem in Docker?"** → Ans: there isn't one — but interviewers may ask about layer caching. Key insight: copy `package.json` before source code.
- **"How do you persist data in Docker?"** → Named volumes for production databases. Bind mounts for development. Never rely on the container's writable layer.
- **"What's multi-stage build?"** → Using multiple `FROM` statements to separate build and runtime environments, resulting in smaller, more secure final images.

### 📚 Recommended Resources

| Resource | Link |
|----------|------|
| 📖 Official Docker Docs | https://docs.docker.com |
| 🐳 Docker Hub | https://hub.docker.com |
| 📘 Docker Compose Docs | https://docs.docker.com/compose |
| ☸️ Kubernetes Docs | https://kubernetes.io/docs |
| 🎓 Play with Docker (free browser lab) | https://labs.play-with-docker.com |
| 🔷 Docker Security Guide | https://docs.docker.com/engine/security |
| 🛣️ DevOps Roadmap | https://roadmap.sh/devops |
| 🔍 Trivy (image scanner) | https://trivy.dev |

### 🎯 Final Notes

Docker is not just a tool — it's a **mindset shift** toward reproducible, portable infrastructure. Once you think in containers, deployment consistency stops being a problem.

Start by containerizing one small project. Then add a database. Then reach for Compose. Production patterns follow naturally.

> **Master the fundamentals — `docker run`, Dockerfile, Compose, and networking — and 90% of real-world Docker usage becomes straightforward.**

---

*Built with ❤️ for developers who ship. Corrections and contributions welcome.*
