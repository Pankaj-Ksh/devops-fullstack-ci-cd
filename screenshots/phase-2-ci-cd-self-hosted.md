# Phase 2 – CI/CD Pipeline Screenshots

This document provides visual proof of the Continuous Integration and
Continuous Deployment (CI/CD) pipeline implemented using GitHub Actions.
The pipeline automatically builds, pushes, and deploys the application
on every push to the `main` branch.

**Trigger & Deployment Target (Phase 2):**  
The CI/CD workflow is triggered automatically on every push to the `main`
branch. For Phase 2, the deployment target is configured as `local` using a
self-hosted GitHub Actions runner. This ensures that all build and deployment
steps execute directly on the local target environment via Docker Compose,
without relying on any cloud infrastructure.

---

## Image 1: GitHub Self-Hosted Runner Registration

**Technical Description:**  
This image captures the successful configuration and registration of a
GitHub Actions self-hosted runner. The runner is authenticated and connected
to the target repository, enabling workflows to execute directly on the
deployment environment.

**Automation Strategy:**  
Using a self-hosted runner allows deployments to be performed without relying
on third-party managed runners, demonstrating environment-level automation
and deployment control.

<img width="1920" height="1080" alt="Phase 2-1" src="https://github.com/user-attachments/assets/d6118024-d324-4b4a-9474-ae4b0562f2af" />

---

## Image 2: Version Control & Pipeline Trigger

**Technical Description:**  
This IDE view shows a git commit and push operation introducing a small visual
change (header text color). The change is intentionally made to validate that
every push to the repository triggers the CI/CD pipeline.

**CI/CD Validation:**  
This confirms the “trigger on push” requirement, proving that code changes
automatically initiate the delivery process without manual execution.

<img width="1920" height="1080" alt="Phase 2-2" src="https://github.com/user-attachments/assets/8d821b23-bfa5-42ea-a363-110b1c223189" />

---

## Image 3: Centralized Source Code & Workflow Configuration

**Technical Description:**  
This screenshot displays the GitHub repository structure, including the
`.github/workflows` directory containing the CI/CD workflow definition.
The commit history reflects recent changes deployed via the pipeline.

**Best Practice:**  
The repository acts as the single source of truth, storing all Dockerfiles,
workflow configurations, and deployment logic required for reproducible builds.

<img width="1920" height="1032" alt="Phase 2-3" src="https://github.com/user-attachments/assets/2f40c3a2-c3c0-4238-899b-1fd73093b238" />

---

## Image 4: Continuous Integration Workflow Execution

**Technical Description:**  
The GitHub Actions dashboard shows a successful execution of the
`phase2-ci-cd.yml` workflow, including build, push, and deployment steps.
The total execution time confirms an efficient and stable pipeline.

**Automation Confirmation:**  
This verifies that the pipeline reliably builds Docker images, pushes them to
the registry, and deploys them automatically on every push to `main`.

<img width="1920" height="1032" alt="Phase 2-4" src="https://github.com/user-attachments/assets/5ecccd41-4b8e-4050-8a8f-d20e4ce166f3" />

---

## Image 5: Production Environment Validation

**Technical Description:**  
This browser view displays the application running after deployment, showing
the updated UI change introduced in the previous commit. This confirms that
the new Docker images were built and redeployed successfully.

**Deployment Proof:**  
The visible update validates end-to-end automation—from source code change
to live deployment—without manual intervention.

<img width="1920" height="1080" alt="Phase 2-5" src="https://github.com/user-attachments/assets/995f6a71-77e7-4bf4-9e94-f6bcd9e179cb" />

---

## (Optional) Image 6: Container Runtime Management

**Technical Description:**  
This Docker Desktop view provides a high-level overview of the running
containers, including both the backend and frontend services.

**Operational Insight:**  
It confirms that the application containers are actively running using images
pulled from the public registry.

<img width="1920" height="1080" alt="Phase 2-6" src="https://github.com/user-attachments/assets/90a07f0a-0ccc-4d79-8a24-1bb47fa28105" />

---

## Phase 2 Summary

Phase 2 successfully demonstrates:
- Automated CI/CD execution on every push
- Use of a self-hosted GitHub Actions runner
- Automated Docker image build and push
- Zero-touch deployment process
- Verified application update after deployment
