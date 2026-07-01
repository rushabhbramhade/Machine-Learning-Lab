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
