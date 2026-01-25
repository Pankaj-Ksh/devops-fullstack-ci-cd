## 1. Overview

This document describes the complete DevOps implementation for the
Full-Stack Deployment assessment. The project demonstrates containerization,
CI/CD automation, and cloud infrastructure provisioning using industry-standard
DevOps practices.

The application consists of:
- **Backend:** Django REST API
- **Frontend:** React (Vite + TypeScript)

The workflow is implemented in three phases:
1. Containerization using Docker
2. CI/CD automation using GitHub Actions
3. Cloud deployment using Terraform and AWS EC2

---

## 2. Local Setup Guide (Phase 1)

### Prerequisites
- Docker
- Docker Compose
- Git

### Access the Application

- **Frontend:** http://localhost:3000  
- **Backend API:** http://localhost:8000/api/hello/

### Environment Configuration

Environment variables are injected using **Docker** and **Docker Compose**.

### Example Environment Variables

- `DEBUG`
- `API_URL`
- `VITE_API_URL`

✅ No secrets are hardcoded in the repository.

---

## 3. Containerization Strategy (Best Practices)

### Backend (Django)

- Uses **multi-stage Docker builds** to reduce image size
- Final runtime image is based on `python:slim`
- Runs as a **non-root user** for improved security
- Only required application code and dependencies are copied into the final image

### Frontend (React)

- Uses a **Node.js builder stage** to compile and generate static assets
- Final image is based on **Nginx Alpine**
- Non-root execution enforced through proper file and directory permissions
- Build-time configuration handled using `VITE_API_URL`

### Image Optimization

- `.dockerignore` files are used to exclude unnecessary files and directories
- Multi-stage builds significantly reduce the final image size

---

## 4. CI/CD Pipeline (Phase 2 – Local Deployment)

### Trigger Mechanism

- The CI/CD workflow is triggered automatically on every push to the `main` branch

### Deployment Target (Phase 2)

- Deployment target is **local**
- Uses a **GitHub Actions self-hosted runner**
- Controlled via a pipeline variable: `DEPLOY_TARGET=local`

### Pipeline Steps

1. Checkout source code
2. Build Docker images
3. Push images to Docker Hub
4. Pull images on the self-hosted runner
5. Deploy containers using Docker Compose

### Automation Validation

- No manual steps are required after code push
- Any code change triggers a fresh deployment automatically
- Deployment verified through UI changes pushed to the repository

---

## 5. Infrastructure as Code (Phase 3 – AWS Cloud)

### Tooling

- **Terraform**
- **AWS EC2** (Amazon Linux)

### Resources Provisioned

- EC2 Instance
- Security Group

### Security Group Rules

Only the required ports are exposed:

| Port | Purpose |
|-----:|---------|
| 22   | SSH     |
| 80   | HTTP    |
| 443  | HTTPS   |

### Outputs

- Terraform outputs the **EC2 public IP**
- The public IP is used for:
  - Application deployment
  - Accessing the deployed application
 
---

## 6. CI/CD Pipeline (Phase 3 – AWS Deployment)

### Deployment Target (Phase 3)

- Deployment target is **AWS**
- Controlled using the pipeline variable: `DEPLOY_TARGET=aws`

### Deployment Flow

1. Push to the `main` branch
2. GitHub Actions pipeline is triggered automatically
3. Docker images are rebuilt and pushed to Docker Hub
4. AWS EC2 instance pulls the latest Docker images
5. Containers are redeployed using Docker Compose

### Cloud Deployment Validation

- UI changes are successfully reflected in the production environment
- Application is accessible via the **EC2 public IP**
- End-to-end CI/CD automation is fully verified

---

## 7. Security Practices

- Containers are configured to run as **non-root users**
- No secrets or credentials are hardcoded in the codebase
- **GitHub Secrets** are used to manage sensitive configuration values
- **Minimal port exposure** is enforced through AWS Security Groups
- `.gitignore` and `.dockerignore`

## 8. Assumptions
- AWS EC2 (Amazon Linux) was selected as the cloud provider.
- Docker Hub is used as the public container registry.
- HTTPS is not configured; the application is exposed over HTTP (port 80).
- Secrets are managed using GitHub Secrets and not committed to the repository.
- Terraform state is managed locally.
- Docker Compose is used for both local and cloud deployments.
- CI/CD deployment target is controlled using a pipeline variable
  (`DEPLOY_TARGET=local | aws`). files are used strategically to maintain a clean and secure repository
- Public container images do **not** contain any credentials or sensitive data

---

## 9. Screenshots Reference

Phase-wise screenshots are organized under the `/screenshots` directory:

- **Phase 1:** Containerization  
- **Phase 2:** CI/CD (Local)  
- **Phase 3:** Terraform & AWS  

Each phase includes only **key screenshots** that clearly demonstrate successful functionality and verification.

---
## 10. Issues Faced and Resolutions

### Issue 1: Frontend Unable to Fetch Backend API  

**Root Cause:**  
The frontend application was initially configured to call `localhost:8000` for backend API requests.  
Inside a Docker Compose network, `localhost` refers to the frontend container itself, not the backend service.

**Resolution:**  
Updated the frontend API configuration to use the **backend service name** defined in `docker-compose.yml` instead of `localhost`.

**Outcome:**  
The frontend successfully fetched data from the backend across container boundaries, confirming proper inter-container communication.

---

### Issue 2: Environment Variables Not Applied in Frontend Build  

**Root Cause:**  
The frontend API URL was defined as a runtime environment variable. However, **Vite requires environment variables at build time**, causing the application to use an incorrect or missing API endpoint.

**Resolution:**  
Updated the frontend Dockerfile to pass `VITE_API_URL` as a **build argument** during the image build process.

**Outcome:**  
The frontend correctly consumed the backend API endpoint after rebuilding the Docker image, ensuring consistent behavior across environments.

---

### Issue 3: CI/CD Pipeline Deployed Successfully but Old Containers Still Running  

**Root Cause:**  
During AWS deployment, existing containers on the EC2 instance were not stopped before redeployment. As a result, older containers continued serving traffic despite a successful CI/CD run.

**Resolution:**  
Updated the deployment step in the CI/CD pipeline to **explicitly stop and remove existing containers** before starting new ones using Docker Compose.

**Outcome:**  
The latest application version was deployed consistently on every pipeline execution, ensuring reliable and repeatable cloud deployments.


