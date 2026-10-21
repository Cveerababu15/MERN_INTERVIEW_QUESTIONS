# Docker — Interview Questions & Answers

Docker is a platform used to **package applications and their dependencies into containers** so they can run consistently across different environments.

For a MERN developer:

```text
Application
   ↓
Docker Image
   ↓
Docker Container
   ↓
Application Runs
```

---

## 1. What is Docker?

Docker is a platform for creating, packaging, and running applications inside containers.

It solves the common problem:

> "It works on my machine, but not on another machine."

Docker provides a consistent environment for the application.

---

## 2. What is a Container?

A container is a running instance of a Docker image.

It contains the application and the dependencies required to run it.

```text
Docker Image
      ↓
Docker Container
      ↓
Running Application
```

---

## 3. What is a Docker Image?

A Docker image is a read-only template used to create containers.

It contains things such as:

* Application code
* Runtime
* Dependencies
* Configuration required to run the application

Example:

```text
Node.js Image
     +
Application Code
     +
Dependencies
     ↓
Docker Image
```

---

## 4. Image vs Container

| Image                     | Container              |
| ------------------------- | ---------------------- |
| Template                  | Running instance       |
| Read-only                 | Running environment    |
| Used to create containers | Created from an image  |
| Can be shared             | Can be started/stopped |

Simple example:

```text
Image → Blueprint
Container → Actual running application
```

---

## 5. What is a Dockerfile?

A Dockerfile is a text file containing instructions for building a Docker image.

Example:

```dockerfile
FROM node:20

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

EXPOSE 5000

CMD ["npm", "start"]
```

---

## 6. Explain the Dockerfile above.

```dockerfile
FROM node:20
```

Uses Node.js as the base image.

```dockerfile
WORKDIR /app
```

Sets the working directory.

```dockerfile
COPY package*.json ./
```

Copies package files.

```dockerfile
RUN npm ci
```

Installs dependencies.

```dockerfile
COPY . .
```

Copies application source code.

```dockerfile
EXPOSE 5000
```

Documents the port used by the application.

```dockerfile
CMD ["npm", "start"]
```

Starts the application.

---

## 7. What is Docker Hub?

Docker Hub is a registry where Docker images can be stored and shared.

Typical flow:

```text
Build Image
    ↓
Docker Hub
    ↓
Pull Image
    ↓
Run Container
```

---

## 8. What is a Docker Registry?

A Docker registry stores Docker images.

Examples:

* Docker Hub
* GitHub Container Registry
* Amazon ECR

---

## 9. What are common Docker commands?

### Check Docker version

```bash
docker --version
```

### Build an image

```bash
docker build -t my-app .
```

### List images

```bash
docker images
```

### Run a container

```bash
docker run my-app
```

### List running containers

```bash
docker ps
```

### Stop a container

```bash
docker stop <container-id>
```

### Remove a container

```bash
docker rm <container-id>
```

### Remove an image

```bash
docker rmi <image-id>
```

---

## 10. What does `docker build` do?

`docker build` creates a Docker image from a Dockerfile.

Example:

```bash
docker build -t my-node-app .
```

Flow:

```text
Dockerfile
    ↓
docker build
    ↓
Docker Image
```

---

## 11. What does `docker run` do?

`docker run` creates and starts a container from an image.

Example:

```bash
docker run my-node-app
```

Flow:

```text
Docker Image
     ↓
docker run
     ↓
Container
```

---

## 12. How do you map ports in Docker?

A container can run on one port while the host exposes another port.

Example:

```bash
docker run -p 5000:5000 my-node-app
```

Format:

```text
-p HOST_PORT:CONTAINER_PORT
```

Example:

```text
5000:5000
```

means:

```text
Host Port       → 5000
Container Port  → 5000
```

---

## 13. What is Docker Volume?

A volume provides persistent storage for containers.

Normally, container data can be lost when a container is removed.

Volumes allow data to persist.

```text
Container
    ↓
Volume
    ↓
Persistent Data
```

---

## 14. What is Docker Network?

Docker networks allow containers to communicate with each other.

Example:

```text
Frontend Container
        ↓
Docker Network
        ↓
Backend Container
        ↓
MongoDB Container
```

---

## 15. What is Docker Compose?

Docker Compose is used to define and run multiple containers together.

For example:

```text
Frontend
Backend
MongoDB
```

can be managed as one application.

A Compose configuration is commonly stored in:

```text
docker-compose.yml
```

or:

```text
compose.yml
```

---

## 16. Why use Docker Compose for MERN?

A MERN application may contain multiple services:

```text
React
Node/Express
MongoDB
```

Docker Compose allows these services to be configured and started together.

Example:

```text
Docker Compose
      │
      ├── Frontend
      ├── Backend
      └── MongoDB
```

---

## 17. What is `.dockerignore`?

`.dockerignore` specifies files that should not be copied into the Docker image.

Example:

```text
node_modules
.env
.git
npm-debug.log
```

It helps reduce image size and prevents unnecessary or sensitive files from being copied.

---

## 18. What is the difference between Docker and a Virtual Machine?

| Docker                | Virtual Machine              |
| --------------------- | ---------------------------- |
| Uses containers       | Uses virtual machines        |
| Shares host OS kernel | Includes a complete guest OS |
| Lightweight           | Heavier                      |
| Starts quickly        | Usually slower               |
| Uses fewer resources  | Uses more resources          |

Simple explanation:

```text
VM
Hardware
 ↓
Hypervisor
 ↓
Guest OS
 ↓
Application
```

Docker:

```text
Hardware
 ↓
Host OS
 ↓
Docker
 ↓
Container
 ↓
Application
```

---

## 19. Why is Docker useful in development?

Docker provides a consistent environment.

Without Docker:

```text
Developer A
Node version X
Dependency version X
```

Developer B:

```text
Node version Y
Dependency version Y
```

This can cause compatibility problems.

With Docker:

```text
Docker Image
     ↓
Same Environment
     ↓
Developer
     ↓
Testing
     ↓
Production
```

---

## 20. How is Docker used in CI/CD?

Docker can be part of a CI/CD pipeline.

Example:

```text
Developer
   ↓
Git Push
   ↓
CI/CD
   ↓
Run Tests
   ↓
Build Docker Image
   ↓
Push Image to Registry
   ↓
Deploy Container
   ↓
Production
```

---

## 21. What is a Docker Tag?

A tag identifies a particular version of an image.

Example:

```bash
docker build -t my-app:1.0 .
```

Here:

```text
my-app → Image name
1.0    → Tag
```

Another example:

```text
my-app:latest
my-app:1.0
my-app:2.0
```

---

## 22. What is a multi-stage Docker build?

A multi-stage build uses multiple stages in a Dockerfile.

It is commonly used to keep the final image smaller.

Example concept:

```text
Stage 1
Build Application
      ↓
Stage 2
Copy Production Files
      ↓
Smaller Final Image
```

This is especially useful for frontend applications.

---

## 23. Should `.env` be copied into a Docker image?

Generally, sensitive `.env` files should not be copied into the image.

Avoid:

```dockerfile
COPY .env .
```

Instead, provide configuration through the deployment environment or Docker runtime configuration.

---

## 24. How would you Dockerize a Node.js application?

Basic process:

```text
1. Create Dockerfile
2. Choose Node.js base image
3. Set WORKDIR
4. Copy package files
5. Install dependencies
6. Copy source code
7. Expose application port
8. Define start command
9. Build image
10. Run container
```

Commands:

```bash
docker build -t node-api .
```

Then:

```bash
docker run -p 5000:5000 node-api
```

---

# Docker Interview Checklist

Understand these concepts:

* [ ] Docker
* [ ] Container
* [ ] Docker Image
* [ ] Dockerfile
* [ ] Docker Hub
* [ ] Docker Registry
* [ ] `docker build`
* [ ] `docker run`
* [ ] `docker ps`
* [ ] Port Mapping
* [ ] Volume
* [ ] Network
* [ ] Docker Compose
* [ ] `.dockerignore`
* [ ] Docker vs VM
* [ ] Docker in CI/CD
* [ ] Image Tags
* [ ] Multi-stage Builds
* [ ] Environment Variables
* [ ] Dockerizing Node.js

---

# Final Docker Flow

```text
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
Docker Registry
    ↓
docker pull
    ↓
Docker Container
    ↓
Running Application
```

### MERN + Docker

```text
              Docker Compose
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
    Frontend     Backend      MongoDB
    Container    Container    Container
        │           │           │
        └───────────┴───────────┘
                Network
```

> **Interview Goal:** Be able to clearly explain Docker, images, containers, Dockerfiles, basic commands, Compose, networking, volumes, and how Docker fits into a CI/CD pipeline.
