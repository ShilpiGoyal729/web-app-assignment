# 🚀 DevOps End-to-End Project

---

# 📌 Project Overview

The assignment was completed on macOS. Since WSL2 is only available on Windows, macOS Terminal (Unix-based environment) was used to demonstrate Linux command-line operations. Docker, Nginx, SSL, GitHub Actions, and all remaining DevOps tasks were successfully implemented on macOS.

This project demonstrates a complete DevOps workflow covering development, containerization, deployment, automation, and troubleshooting using industry-standard tools.

It includes building and deploying a web application using Docker, managing multi-container setups using Docker Compose, configuring Nginx as a reverse proxy, enabling HTTPS with SSL certificates, and automating workflows using a GitHub Actions CI/CD pipeline.

---

# 🖥️ Environment Setup

## Operating System
- macOS (Unix-based terminal)

## Tools Used
- Docker Desktop
- Git & GitHub
- Nginx
- OpenSSL

## Linux Environment Note
macOS Terminal was used instead of WSL2 since it already supports Linux commands.

---

# 🐳 Docker Setup

## Docker Installation Steps
- Download Docker Desktop
- Install and launch Docker
- Start Docker Engine
- Verify installation using CLI

---

## Installation Verification

```bash
docker --version
docker info
docker run hello-world
```
### Build Docker Image
```bash
docker build -t web-image:v1 .
```
### Run Docker Container
```bash
docker run -p 8080:80 web-image:v1
```

#### Key Concepts
**Image**  → Blueprint of application
**Container** → Running instance of image
**Volume** → Persistent storage
**Network** → Communication between containers


## Docker Compose Setup
### Command
```bash
docker compose up -d
```
**Services**
Web Application Container
MySQL Database Container
Architecture Flow

Browser → Web Container → Docker Network → MySQL Container

## Nginx Configuration

Nginx works as a reverse proxy that forwards requests to backend containers.

**Client → Nginx → Web Application Container**

## SSL Configuration
Self-signed SSL certificate used
HTTP redirected to HTTPS
Browser warning expected
## Backup & Restore Process
**Backup Commands**
```bash
docker save -o image.tar web-image:v1
docker exec mysql-container mysqldump -u root -p appdb > db.sql
```

**Restore Commands**
```bash
docker load -i image.tar
cat db.sql | docker exec -i mysql-container mysql -u root -p appdb
```
## CI/CD Setup (GitHub Actions)
#### Flow

**GitHub → Actions → Build → Run → Validate**

**Workflow File**

.github/workflows/docker-ci.yml

**Trigger**

Runs automatically on every push to main branch

# Architecture Diagram

Developer
↓
GitHub Repository
↓
GitHub Actions CI/CD Pipeline
↓
Docker Image Build
↓
Containers (Web + DB)
↓
Nginx Reverse Proxy
↓
HTTPS Browser Access

# Final Outcome

This project demonstrates a complete DevOps lifecycle from development to deployment, automation, monitoring, and troubleshooting using Docker, Nginx, SSL, and GitHub Actions.
