# Phase 3 – Infrastructure as Code (Terraform & AWS) Screenshots

This document provides visual proof of cloud infrastructure provisioning and
automated deployment using Terraform and AWS. Phase 3 demonstrates the ability
to provision infrastructure as code and deploy the application to a live cloud
environment using the existing CI/CD pipeline.

The **deployment behavior** is controlled using a pipeline configuration variable
(`DEPLOY_TARGET=aws`), which enables cloud-specific deployment logic and
redeploys the application on the AWS EC2 instance using Docker Compose.

---

## Image 1: Terraform Infrastructure Provisioning

**Technical Description:**  
This terminal view demonstrates the successful execution of `terraform apply`,
which provisions the AWS infrastructure required for deployment. The output
confirms the creation of the EC2 instance and associated Security Group
resources.

**Infrastructure Validation:**  
Terraform outputs include the generated `ec2_public_ip`, which is used to
access the deployed application and validate the final production setup.

<img width="1920" height="1080" alt="Phase 3-1" src="https://github.com/user-attachments/assets/c1bb774b-0012-498a-b1c6-304271485453" />

---

## Image 2: Initial Cloud Environment Verification

**Technical Description:**  
This browser view confirms the application is accessible using the AWS EC2
public IP address (`13.201.8.30`). The displayed “Backend Online” status verifies
that the cloud infrastructure is correctly configured and reachable over HTTP.

**Network Validation:**  
Successful access confirms that the Security Group rules allow inbound traffic
on the required ports and that the application is running correctly on the
cloud instance.

<img width="1920" height="1080" alt="Phase 3-2" src="https://github.com/user-attachments/assets/79bda5a8-7896-440b-bc4e-9067f94468a8" />

---

## Image 3: Automated Deployment Configuration Change

**Technical Description:**  
This IDE view captures a frontend configuration change, specifically modifying
the `<h1>` text color. The change is intentionally introduced to validate the
push-to-deploy behavior of the CI/CD pipeline in the cloud environment.

**Deployment Strategy:**  
A simple git commit and push initiates the complete build and redeployment
process, demonstrating continuous delivery to the AWS EC2 instance.

<img width="1920" height="1080" alt="Phase 3-3" src="https://github.com/user-attachments/assets/801108b9-4f1f-45c9-9018-32dc033ba6a4" />

---

## Image 4: Cloud-Targeted CI/CD Workflow Execution

**Technical Description:**  
The GitHub Actions dashboard shows a successful execution of the CI/CD workflow
targeting the AWS EC2 environment. The pipeline rebuilds Docker images, pushes
them to the registry, and deploys them to the cloud server.

**Automation Confirmation:**  
The successful workflow run confirms seamless integration between CI/CD,
container registry, and cloud infrastructure.

📁 <img width="1920" height="1080" alt="Phase 3-4" src="https://github.com/user-attachments/assets/e2f97a61-582e-4ec3-b112-7df0bdc4de1e" />

---

## Image 5: AWS Management Console – Instance Status

**Technical Description:**  
This view of the AWS EC2 dashboard confirms that the Terraform-provisioned
instance (`terraform-app-server`) is in a `Running` state with all system and
instance status checks passed.

**Infrastructure Verification:**  
The instance type (`t3.micro`) and public IP mapping align with the Terraform
configuration and output values, confirming infrastructure consistency.

<img width="1920" height="1080" alt="Phase 3-5" src="https://github.com/user-attachments/assets/55afdafd-cf74-457e-83a7-71cfeeb61f47" />

---

## Image 6: Final Production Deployment Verification

**Technical Description:**  
This image displays the live application running on AWS with the updated pink
header applied. It confirms that the most recent code change was successfully
deployed to the production environment.

**End-to-End Validation:**  
This serves as definitive proof that Infrastructure as Code (Terraform),
containerization, and the CI/CD pipeline are fully integrated and functioning
correctly in a real cloud environment.

<img width="1920" height="1080" alt="Phase 3-6" src="https://github.com/user-attachments/assets/3d43658a-4a8c-4ba8-80b2-f1a1845ec826" />

---

## Phase 3 Summary

Phase 3 successfully demonstrates:
- Infrastructure provisioning using Terraform
- Secure and reproducible AWS EC2 setup
- Cloud-based automated deployments
- CI/CD pipeline reuse across environments
- End-to-end validation of a production-ready workflow
