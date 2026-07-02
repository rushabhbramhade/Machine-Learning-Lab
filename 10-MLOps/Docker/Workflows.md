# Workflows of Docker in Project

<img width="903" height="458" alt="image" src="https://github.com/user-attachments/assets/1217678f-a160-4141-b54a-a26a6ea84ae3" />

Your team is building an AI Chat Application.

```text
AI-Chat/
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
│
├── frontend/
├── docker-compose.yml
└── README.md
```

Your Tech Lead says:

> "hey, add JWT Authentication to the backend."

Now let's walk through your diagram.

## PART 1 — Bottom Diagram (Developer Side)

This is **you** working on your computer.

```text
Dockerfile
      │
   Build
      │
    Image
      │
    Run
      │
 Container
```

This happens every day while developing.

### Step 1 — Write Your Code

You open VS Code.

You modify:

- `backend/app.py`

You add:

- JWT Authentication

Nothing Docker-related yet.

### Step 2 — Dockerfile

Now Docker needs instructions.

You create a `Dockerfile`.

Example:

```dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["uvicorn", "app:app"]
```

#### Think like this

Imagine you're giving instructions to a robot.

You tell the robot:

- Use Python 3.12
- Copy my project
- Install packages
- Start FastAPI

That robot is Docker.

### Step 3 — Build Image

Now you tell Docker:

```bash
docker build -t backend .
```

Let's understand every word:

- `docker` → Use Docker.
- `build` → Create an image.
- `-t` → Tag, or give the image a name.
- `backend` → Image name.
- `.` → Current folder.

What happens?

Docker reads the `Dockerfile` line by line:

- `FROM python` → install Python
- `COPY` → copy project
- `RUN` → install libraries
- `CMD` → remember start command

Finally, Docker creates the `backend` image.

**Important:** at this moment, your application is not running.

An image is only a package.

Think:

- Image = game installed, not playing
- Image = movie downloaded, not playing

### Step 4 — Run Container

Now you want to test your application.

Command:

```bash
docker run -p 8000:8000 backend
```

Now Docker says:

- Take image
- Create container
- Start application

Now FastAPI is running.

Browser:

```text
localhost:8000
```

works.

#### What is a container?

Container = running application.

- Image → Container
- Recipe → Cooked food
- Game installed → Game running

### Why don't we run the Dockerfile directly?

Many beginners ask this.

Because Dockerfile is only instructions.

Imagine a cake recipe.

Can you eat the recipe?

No.

You first bake the cake.

So the flow is:

- Dockerfile
- Image
- Container

### When does the build happen?

The green arrow in your diagram means:

```text
Dockerfile → Build → Image
```

This happens only when:

- You changed dependencies
- You changed the Dockerfile
- It is the first time building

Command:

```bash
docker build -t backend .
```

Suppose tomorrow you change only Python code:

```python
return {"Hello": "Rushabh"}
```

to

```python
return {"Hello": "OpenAI"}
```

Do you need to rebuild?

Sometimes no.

Why?

Because during development, many projects mount source code into the container using Docker Compose volumes. The running container sees your code changes immediately, and FastAPI with `--reload` automatically reloads the app.

You rebuild only if you changed things like:

- Dockerfile
- `requirements.txt`
- Base image
- System packages

## Move to the Top Diagram

This is not you.

This is your teammate.

```text
Docker Hub
   ↓
Pull
   ↓
Image
   ↓
Run
   ↓
Container
```

Imagine you finished JWT Authentication.

Now your Tech Lead says:

> Push your Docker image.

Command:

```bash
docker push company/backend:v1
```

Now:

- Your laptop → Docker Hub → image stored

Docker Hub is like GitHub.

Difference:

- GitHub stores source code
- Docker Hub stores Docker images

### Another developer joins

Tomorrow a new developer joins.

He does not build the image.

Instead, he downloads it.

Command:

```bash
docker pull company/backend:v1
```

Meaning:

- Docker Hub → download image

Now he has the exact same image.

Then he starts it:

```bash
docker run company/backend:v1
```

Container starts.

No installing Python.

No installing FastAPI.

No installing dependencies.

Everything already exists.

## Real company timeline

### You

Morning:

- Write code
- `docker build -t backend .`
- image created
- `docker run -p 8000:8000 backend`
- test API
- works
- `docker push company/backend:v1`
- go home 😄

### Another developer

Next day:

- He comes
- Runs `docker pull company/backend:v1`
- downloads image
- Runs `docker run -p 8000:8000 company/backend:v1`
- project works

He never built anything.

## Every arrow explained

### Dockerfile → Build

When?

- When creating a new image
- After changing the Dockerfile or dependencies

Command:

```bash
docker build -t backend .
```

Why?

Because Docker needs to package your application.

### Build → Image

Docker creates the backend image.

Image contains:

- Python
- Libraries
- FastAPI
- Your code
- Everything

### Image → Run

Command:

```bash
docker run backend
```

Why?

Because an image alone cannot execute.

You need a running instance.

### Run → Container

Now the application is live.

Browser:

```text
localhost:8000
```

works.

### Image → Push

Command:

```bash
docker push company/backend:v1
```

Why?

To share your packaged application with others.

### Registry/Hub

Stores images.

Exactly like:

- GitHub stores code
- Docker Hub stores images

### Pull

Command:

```bash
docker pull company/backend:v1
```

Why?

To download someone else's image.

### Run again

Downloaded image → run → container.

Works immediately.

## Entire story in one flow

```text
👨‍💻 YOU (Developer)

Write Code
     │
     ▼
Create Dockerfile
     │
     ▼
docker build -t backend .
     │
     ▼
Docker Image Created
     │
     ▼
docker run -p 8000:8000 backend
     │
     ▼
Test Your Application
     │
     ▼
docker push company/backend:v1
     │
     ▼
──────────── Docker Hub ────────────
     ▲
     │
docker pull company/backend:v1
     │
     ▼
👨‍💻 Another Developer
     │
     ▼
docker run -p 8000:8000 company/backend:v1
     │
     ▼
Application Runs Exactly the Same
```

## Industry reality

The diagram shows the core Docker lifecycle, but in real projects, developers usually do not manually run `docker build`, `docker run`, and `docker push` every day.

Instead, they use Docker Compose during development:

```bash
docker compose up --build
```

This command:

- Builds images if needed
- Creates containers
- Starts all services like backend, database, Redis, and frontend
- Connects them to the same network

When code is merged into GitHub, the CI/CD pipeline automatically performs:

```text
Git Push
   │
   ▼
GitHub Actions / Jenkins
   │
   ▼
docker build
   │
   ▼
Run Tests
   │
   ▼
docker push
   │
   ▼
Deploy to Server
```

So in a professional environment:

- Developers mostly use `docker compose up`, `docker compose down`, `docker compose logs`, and `docker compose exec`.
- CI/CD systems usually handle `docker build` and `docker push`.
- Servers use `docker pull` to download the new image and run the updated application.
