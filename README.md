# 🚀 DevOps End-to-End Project

---

# 📌 Project Overview

The assignment was completed on macOS. Since WSL2 is only available on Windows, macOS Terminal (Unix-based environment) was used to demonstrate Linux command-line operations. Docker, Nginx, SSL, GitHub Actions, and all remaining DevOps tasks were successfully implemented on macOS.

This project demonstrates a complete DevOps workflow covering development, containerization, deployment, automation, and troubleshooting using industry-standard tools.

It includes building and deploying a web application using Docker, managing multi-container setups with Docker Compose, configuring Nginx as a reverse proxy, enabling HTTPS with SSL certificates, and automating workflows using a GitHub Actions CI/CD pipeline.

All tasks were performed on macOS using its Unix-based terminal, which supports Linux-like commands, allowing smooth execution of all DevOps operations without requiring a separate Linux/WSL environment.

---

# 🖥️ Environment Setup

## Operating System
- macOS (Unix-based terminal)

## Tools Used
- Docker Desktop
- Git & GitHub
- Nginx (container-based setup)
- OpenSSL (for SSL certificates)

## Linux Environment Note
Instead of WSL2/Ubuntu installation, macOS Terminal was used as it natively supports Linux commands and provides an equivalent environment for DevOps practice.

---

# 🐳 Docker Setup

## Docker Installation Steps (macOS)

- Download Docker Desktop from the official Docker website  
- Open the `.dmg` file  
- Drag Docker into Applications  
- Launch Docker Desktop  
- Accept license agreement and complete setup  
- Wait for Docker Engine to start  
- Verify installation using CLI  

---

## Installation Verification

```bash
docker --version
docker info
docker run hello-world
Build Docker Image
docker build -t web-image:v1 .
Run Docker Container
docker run -p 8080:80 web-image:v1
Key Concepts
Image → A read-only blueprint or template used to create containers
Container → A running instance of a Docker image that executes the application in an isolated environment
Volume → A mechanism used to persist data outside the container
Network → A communication layer that allows multiple containers to connect and interact with each other securely
🧩 Docker Compose Setup

Created docker-compose.yml

Command to run Docker Compose:
docker compose up -d
Services:
Web Application Container
MySQL Database Container
Architecture Flow:

Browser → Web Container → Docker Network → MySQL Container

🌐 Nginx Configuration (Reverse Proxy)

Nginx acts as a reverse proxy that routes incoming requests to backend application containers.

Flow:

Client → Nginx → Web Application Container

Benefits:
Security
Load balancing
Single entry point for applications
Scalability
🔐 SSL Configuration (HTTPS)

SSL was configured using a self-signed certificate inside Nginx.

HTTP requests are redirected to HTTPS.

Note:
Browser shows a warning because self-signed certificates are not issued by trusted Certificate Authorities.

💾 Backup & Restore Process
Backup Commands:
docker save -o image.tar web-image:v1
docker exec mysql-container mysqldump -u root -p appdb > db.sql
Restore Commands:
docker load -i image.tar
cat db.sql | docker exec -i mysql-container mysql -u root -p appdb
🔄 CI/CD Setup (GitHub Actions)
Workflow:

GitHub Push → GitHub Actions → Build Docker Image → Run Container → Validate

Workflow File:

.github/workflows/docker-ci.yml

Trigger:

Automatically runs on every push to main branch

🏗️ Architecture Diagram

Developer
↓
GitHub Repository
↓
GitHub Actions CI/CD Pipeline
↓
Docker Image Build
↓
Containers (Web Application + Database)
↓
Nginx Reverse Proxy
↓
HTTPS Browser Access

🚀 Final Outcome

This project demonstrates a complete DevOps lifecycle from development → containerization → deployment → CI/CD automation → monitoring → troubleshooting using real-world DevOps tools and workflows.
