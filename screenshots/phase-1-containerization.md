# Phase 1 – Containerization Screenshots

This document provides visual proof of the successful containerization of the
full-stack application using Docker and Docker Compose, following industry
best practices such as multi-stage builds, non-root users, and optimized images.

---

## Image 1: Optimized Multi-Stage Backend Dockerfile
**Technical Description:**  
This image showcases the multi-stage Docker build for the Django backend.
A dedicated builder stage is used to install Python dependencies in an
isolated environment, after which only the required application files
and dependencies are copied into a lightweight `python:3.11-slim`
runtime image.

**Security & Best Practice:**  
A non-root user (`appuser`) is created and assigned ownership of the `/app`
directory. This ensures the backend service runs without administrative
privileges, reducing the container’s attack surface.

<img width="1920" height="1080" alt="Phase 1-1" src="https://github.com/user-attachments/assets/47fda9e9-5927-406c-a548-52bc7d0be872" />

---

## Image 2: Production-Ready Frontend Dockerfile

**Technical Description:**  
The frontend uses a Node.js `20-alpine` builder stage to compile the
React + TypeScript application into static assets using Vite.
An `ARG` instruction is used to inject the `VITE_API_URL` at build time,
allowing environment-specific backend configuration.

**Deployment Strategy:**  
The final image uses `nginx:alpine` to serve static files efficiently.
A custom `nginx.conf` handles routing, and file permissions are adjusted
to ensure Nginx runs as a non-root user.

<img width="1920" height="1080" alt="Phase 1-2" src="https://github.com/user-attachments/assets/67d14f8b-fd3a-4605-858e-528271335e6b" />

---

## Image 3: Docker Compose Orchestration & Logs

**Technical Description:**  
This screenshot confirms successful orchestration of the full-stack
environment using Docker Compose. Both `django-backend` and
`react-frontend` containers are launched within a shared bridge network.

**Status Verification:**  
Container logs show the backend initializing correctly and the Nginx
server starting without errors, validating service discovery, environment
variables, and inter-container communication.

<img width="1920" height="1080" alt="Phase 1-3" src="https://github.com/user-attachments/assets/20fcd834-8109-4864-8489-39bb2d930c41" />

---

## Image 4: Full-Stack Integration – Live Application View

**Technical Description:**  
This image verifies the complete system running at `http://localhost:3000`.
The React UI successfully displays the backend connectivity status,
confirming cross-container API communication.

**UX/UI Validation:**  
The rendered message **“Hello World from Django Backend!”** proves that
CORS configuration, API routing, and frontend environment variables
are correctly handled in the containerized setup.

<img width="1920" height="1031" alt="Phase 1-4" src="https://github.com/user-attachments/assets/c0e9c3a5-980e-45d9-b98f-62d31f850385" />

---

## Image 5: REST API Endpoint Validation (Postman)

**Technical Description:**  
This screenshot demonstrates direct backend validation using Postman.
A request to `http://localhost:8000/api/hello/` returns an HTTP `200 OK`
response, confirming the Django REST API is reachable and functional.

**Data Integrity:**  
The JSON payload response verifies that the backend logic is intact and
that the application server (Django/Gunicorn) is correctly exposed via
Docker port mapping.

<img width="1920" height="1080" alt="Phase 1-5" src="https://github.com/user-attachments/assets/055b2c0d-158b-49cc-9125-b4a57b3637ce" />
