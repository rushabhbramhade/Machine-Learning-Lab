# 🐳 Docker Quick Notes (Beginner Friendly)

## What is Docker?
Docker packages your application **with everything it needs** (Python, libraries, dependencies, configs) so it runs the **same everywhere**.

**Memory:** 📦 *Pack once → Run anywhere.*


# Core Concepts

## Docker Image 📦
A **blueprint/template** of your application.

- Contains OS, Python, libraries, code
- Not running
- Can create many containers

```
Image
  ↓ docker run
Container
```

## Docker Container 🚀
A **running instance** of an image.

- Running application
- Can start, stop, delete
- Multiple containers can come from one image


## Docker Hub 🌐

An online store for Docker Images.

- Download official images
- Upload your own images
- Similar to GitHub, but stores images instead of code

```
Docker Hub
     ↓ docker pull
Image
     ↓ docker run
Container
```


## Docker Desktop 💻

Software installed on your computer.

Responsibilities:
- Runs Docker Engine
- Builds images
- Runs containers
- Pulls images from Docker Hub

**Remember**

- Docker Hub = Stores Images
- Docker Desktop = Runs Images


# Image vs Container

| Image | Container |
|-------|-----------|
| Blueprint | Running App |
| Read-only | Running |
| Stored | Executing |
| Can create many containers | Created from image |

# requirements.txt

Lists Python packages.

Example:

```txt
fastapi==0.116.0
uvicorn==0.35.0
redis==6.2.0
```

Install:

```bash
pip install -r requirements.txt
```


# Dockerfile

Recipe for building an image.

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["uvicorn","main:app","--host","0.0.0.0","--port","8000"]
```

Build:

```bash
docker build -t myapp:v1 .
```

# Docker Image Commands

| Command | Purpose |
|---------|---------|
| `docker images` | Show local images |
| `docker rmi IMAGE` | Delete image |
| `docker image prune` | Remove unused images |
| `docker build -t app:v1 .` | Build image |
| `docker build --no-cache -t app:v1 .` | Fresh build |

# Docker Container Commands

| Command | Purpose |
|---------|---------|
| `docker ps` | Running containers |
| `docker ps -a` | All containers |
| `docker run IMAGE` | Create & run container |
| `docker run -d IMAGE` | Run in background |
| `docker run --name myapp IMAGE` | Custom name |
| `docker run -p 8000:8000 IMAGE` | Port mapping |
| `docker run -e KEY=value IMAGE` | Environment variable |
| `docker start NAME` | Start container |
| `docker stop NAME` | Stop container |
| `docker inspect NAME` | Details |
| `docker rm NAME` | Delete container |


# Docker Workflow

```text
Write Code
    ↓
requirements.txt
    ↓
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
docker run
    ↓
Docker Container
```

# Best Practices

- Pin package versions.
- Use `python:3.12-slim`.
- Copy `requirements.txt` before project files.
- Use `.dockerignore`.
- Name containers with `--name`.
- Use `-d` for servers.
- Use `-p` to access apps.

<<<<<<< Updated upstream
=======

>>>>>>> Stashed changes
# Quick Memory

- 📦 Image = Blueprint
- 🚀 Container = Running App
- 🌐 Docker Hub = Image Store
- 💻 Docker Desktop = Docker Software
- 📄 requirements.txt = Python package list
- 🧾 Dockerfile = Recipe to build image
