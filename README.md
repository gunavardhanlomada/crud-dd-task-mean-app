# CRUD MEAN Application – Dockerized with CI/CD

## Project Overview

This project demonstrates a fully containerized **MEAN Stack (MongoDB, Express, Angular, Node.js)** CRUD application deployed on a cloud-based Ubuntu VM using:

- Docker & Docker Compose  
- Nginx Reverse Proxy  
- Cloud Ubuntu Virtual Machine  
- GitHub Actions CI/CD Pipeline  
- Docker Hub Image Registry  

The entire application is accessible via **Port 80** using Nginx.

---

# Architecture Overview

```
Developer Push to GitHub
        ↓
GitHub Actions CI/CD
        ↓
Build Docker Images
        ↓
Push to Docker Hub
        ↓
SSH into Ubuntu VM
        ↓
Docker Compose Pull & Restart
        ↓
Nginx (Port 80)
        ↓
Frontend → Backend → MongoDB
```

---

# Docker Configuration

## Services Included

| Service   | Description |
|-----------|------------|
| mongodb   | MongoDB 7 container with healthcheck |
| backend   | Node.js + Express REST API |
| frontend  | Angular application |
| nginx     | Reverse proxy exposed on port 80 |

---

# Project Structure

```
crud-dd-task-mean-app/
│
├── backend/
│   └── Dockerfile
│
├── frontend/
│   └── Dockerfile
│
├── nginx/
│   └── default.conf
│
├── docker-compose.yml
│
├── .github/workflows/
│   └── main.yml
│
└── README.md
```

---

# Local Setup Instructions

## Clone Repository

```bash
git clone https://github.com/<your-username>/crud-dd-task-mean-app.git
cd crud-dd-task-mean-app
```

---

## Install Docker & Docker Compose (Ubuntu)

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
```

---

## Run Application

```bash
docker-compose up -d
```

Application will be available at:

```
http://<PUBLIC_IP_ADDRESS>
```

---

# MongoDB Configuration

- Version: MongoDB 7  
- Healthcheck enabled  
- Backend connects using:

```
mongodb://mongodb:27017/cruddb
```

No `localhost` is used inside containers.

---

# Nginx Reverse Proxy

Configured to expose the entire application via port 80.

### Routing:

- `/` → Frontend  
- `/api` → Backend  

Configuration file:

```
nginx/default.conf
```


---

# CI/CD Pipeline (GitHub Actions)

Workflow file location:

```
.github/workflows/deploy.yml
```

## Pipeline Steps

1. Triggered on push to `main`
2. Login to Docker Hub using Access Token
3. Build backend image
4. Build frontend image
5. Push images to Docker Hub
6. SSH into Ubuntu VM
7. Pull latest images
8. Restart containers using Docker Compose

This ensures automatic deployment on every push.

---

# GitHub Secrets Used

Configured in:

GitHub Repository → Settings → Secrets

- DOCKER_USERNAME
- DOCKER_PASSWORD (Docker Hub Access Token)
- VM_HOST
- VM_USER
- SSH_PRIVATE_KEY

No sensitive information is stored in the repository.

---

# Infrastructure Details

- Ubuntu/debian Virtual Machine (Cloud-based)
- Docker Engine
- Docker Compose
- MongoDB (Containerized)
- Nginx Reverse Proxy
- GitHub Actions CI/CD
- Docker Hub Registry

---

# 🛠 Production Best Practices Implemented

- MongoDB healthcheck configured
- Backend waits for database readiness
- Reverse proxy setup for unified access
- Environment variables used for configuration
- SSH key-based secure deployment
- Docker Hub Access Token used instead of password

---

# 📸 Screenshots (Included in Repository)

The repository includes screenshots demonstrating:

- Successful GitHub Actions workflow execution
- Docker image build and push logs
- Docker Hub repositories
- Running containers on VM (`docker ps`)
- Working application UI in browser
- Nginx configuration
- Infrastructure setup

---

# Application Access

After deployment, open:
Public IP Address

```
http://34.121.93.182
```
