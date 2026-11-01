# CI/CD Pipeline & Automated Local Deployment Workflow

![GitHub Actions Status](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-blue?logo=githubactions)
![Docker](https://img.shields.io/badge/Container-Docker-2496ED?logo=docker)
![Node.js](https://img.shields.io/badge/Backend-Node.js-339933?logo=nodedotjs)
![WSL2](https://img.shields.io/badge/Environment-WSL2%20Ubuntu-E95420?logo=ubuntu)

An end-to-end DevOps automation showcase demonstrating Continuous Integration (CI) using **GitHub Actions** and Continuous Deployment (CD) execution within a **WSL2 (Windows Subsystem for Linux)** environment.

---

## Architecture & Workflow Overview

```text
 [ Developer Workstation (WSL2) ] 
               │
               │  git push main
               ▼
     [ GitHub Repository ] 
               │
               └─► [ GitHub Actions CI Pipeline ]
                         │
                         ├─► 1. Checkout Code
                         ├─► 2. Setup Docker Buildx
                         ├─► 3. Build Multi-Stage Docker Image
                         └─► 4. Push Image to Docker Hub Registry
                                    │
                                    ▼
                     [ Docker Hub Container Registry ]
                                    │
                                    │  docker pull & run
                                    ▼
                     [ Live Deployment on WSL2 Environment ]
```
## Key Features
* Multi-Stage Docker Building: Reduces image size and overhead using standard Alpine Linux images and non-root execution.
* Automated CI Workflow: Triggers build, version tagging (latest and commit SHA), and container publishing on every push to the main branch.
* Secure Token Authentication: Uses GitHub Repository Secrets (DOCKER_USERNAME & DOCKER_PASSWORD) to handle registry authentications securely.
* Local CD Execution: Enables pull and deployment testing directly within a WSL environment without cloud infrastructure overhead.

## Tech Stack
* Application: Node.js, Express.js
* Containerization: Docker Engine, Docker Buildx
* CI/CD Orchestration: GitHub Actions
* Registry: Docker Hub
* Development Environment: Windows 11 / WSL2 (Ubuntu)

## Local Deployment Guide (WSL2)
1. Prerequisites
Ensure you have Docker Engine active inside your WSL2 setup:
```bash
docker --version
```
2. Pulling and Running the Published Image
Once the GitHub Actions workflow succeeds, pull and run the container locally:
```bash
# Pull the latest published image
docker pull kevin261003/portfolio-app:latest

# Run the container mapping to port 3000
docker run -d -p 3000:3000 --name portfolio-app kevin261003/portfolio-app:latest
```
3. Testing Endpoint Responses
```bash
# Root endpoint test
curl http://localhost:3000/

# Health check test
curl http://localhost:3000/health
```

## API Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/` | App Status Info |
| `GET` | `/health` | Health Check Route |

---

## Author

* **GitHub:** [@Kevin-2603](https://github.com/Kevin-2603)
* **Docker Hub:** [@kevin261003](https://hub.docker.com/u/kevin261003)
