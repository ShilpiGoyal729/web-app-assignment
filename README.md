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

## Installation Verification
```bash
docker --version
docker info
docker run hello-world
## Image Creation
