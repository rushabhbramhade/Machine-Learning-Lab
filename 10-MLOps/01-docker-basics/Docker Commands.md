# Docker Image Commands

## 1. List All Local Images

Shows all Docker images stored on your computer.

```bash
docker images
```

**Example Output:**

```
REPOSITORY      TAG      IMAGE ID       CREATED       SIZE
python          3.12     abcd1234       2 days ago    1.2GB
postgres        latest   efgh5678       5 days ago    450MB
nginx           latest   ijkl9012       1 week ago    190MB
```

**Columns Description:**

| Column     | Meaning                    |
|------------|----------------------------|
| REPOSITORY | Image name                 |
| TAG        | Version of the image       |
| IMAGE ID   | Unique ID of the image     |
| CREATED    | When the image was created |
| SIZE       | Disk space used            |

---

## 2. Delete an Image

```bash
docker rmi <image_name>
```

**Examples:**

```bash
docker rmi python
docker rmi postgres
```

> **Important:** If a container is still using the image, Docker won't let you delete it until the container is stopped and removed.

---

## 3. Remove Unused Images

Deletes unused (dangling) images. A dangling image is an image that is not being used by any container and isn't tagged properly.

```bash
docker image prune
```

---

## 4. Build an Image from a Dockerfile

Creates a Docker image from your project's Dockerfile.

```bash
docker build -t <image_name>:<version> .
```

**Example Project Structure:**

```
FastAPI-App/
├── Dockerfile
├── main.py
└── requirements.txt
```

**Usage:**

```bash
docker build -t fastapi-app:v1 .
```

---

## 5. Build Without Cache

Builds the image without using the cache.

```bash
docker build --no-cache -t <image_name>:<version> .
```

---

## Summary

| Command                                    | Purpose                                  | When to Use                     |
|--------------------------------------------|------------------------------------------|---------------------------------|
| `docker images`                            | Show all local images                    | Check available images          |
| `docker rmi <image>`                       | Delete a specific image                  | Remove unused images            |
| `docker image prune`                       | Remove dangling/unused images            | Free disk space                 |
| `docker build -t app:v1 .`                 | Build a new image from a Dockerfile      | Create or update an image       |
| `docker build --no-cache -t app:v1 .`      | Build a fresh image without cached layers| Force a clean rebuild           |

Think of Docker images like books on a bookshelf:

docker images → 📚 Show all books on the shelf.
docker rmi python → 🗑️ Throw away one specific book.
docker image prune → 🧹 Clean up old, forgotten books nobody uses anymore.
docker build -t app:v1 . → ✍️ Write and publish a new book from your manuscript (the Dockerfile and your code).
docker build --no-cache ... → 🆕 Rewrite the entire book from scratch, ignoring any previous drafts.


CONTAINER :

1. List All Containers 

docker ps -a // Shows all containers, including stopped ones.

Example
docker ps -a

Output

CONTAINER ID   IMAGE       STATUS
ab1234         nginx       Up 10 minutes
cd5678         postgres    Exited (0)
ef9012         redis       Exited (137)
Meaning of Output
Column	Meaning
CONTAINER ID	Unique ID of the container
IMAGE	Which image created this container
STATUS	Running or Stopped

2. List Running Containers

docker ps // Shows only running containers.

Example
docker ps

Output

CONTAINER ID   IMAGE       STATUS
ab1234         nginx       Up 10 minutes

3. Create and Run a Container

docker run <image_name>