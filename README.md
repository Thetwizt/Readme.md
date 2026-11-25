# Landmark Internal DevOps Platform

## Overview

Landmark Internal DevOps Platform is a hands-on DevOps project demonstrating an automated application delivery workflow using AWS, Jenkins, Terraform and Docker.

The project uses a Node.js web application to demonstrate continuous integration, container image management, infrastructure provisioning and remote application deployment.

## Architecture

**Developer → GitHub → Jenkins → Amazon ECR → EC2 Docker Host → Web Application**

The application is hosted on an AWS EC2 Docker host. An Application Load Balancer and target group are also configured to provide an entry point for application traffic.

## Technology Stack

| Category | Technologies |
|---|---|
| Cloud | AWS |
| CI/CD | Jenkins |
| Infrastructure as Code | Terraform |
| Containers | Docker |
| Container Registry | Amazon ECR |
| Compute | Amazon EC2 |
| Load Balancing | AWS Application Load Balancer |
| Operating System | Linux |
| Scripting | Bash |
| Application | Node.js |
| Version Control | Git, GitHub |

## Repository Structure

```text
landmark-internal-devops-platform/
│
├── ci-cd/
│   └── Jenkinsfile
│
├── docs/
│   └── architecture.md
│
├── scripts/
│   └── docker-build.sh
│
├── services/
│   └── web-app/
│       ├── app.js
│       ├── Dockerfile
│       └── package.json
│
├── terraform/
│
└── k8s/
```

## CI/CD Pipeline

The Jenkins pipeline automates the following stages:

1. Authenticates with Amazon Elastic Container Registry (ECR).
2. Builds a Docker image using the application Dockerfile.
3. Tags the image using the Jenkins build number.
4. Pushes the versioned image to Amazon ECR.
5. Connects to the remote EC2 Docker host using SSH credentials.
6. Authenticates the Docker host with ECR.
7. Pulls the new image and replaces the existing application container.
8. Checks whether the deployed application responds successfully.

## AWS Infrastructure

The project uses AWS infrastructure components including:

- EC2 instances for Jenkins and application hosting.
- IAM roles and permissions for AWS service access.
- Security groups to control network traffic.
- Amazon ECR for Docker image storage.
- Application Load Balancer and target group for application traffic routing.
- Terraform for infrastructure provisioning and management.

## Practical Engineering and Troubleshooting

During implementation, the project involved troubleshooting:

- Jenkins and EC2 SSH connectivity.
- AWS IAM permissions and ECR authentication.
- Docker daemon permissions and container management.
- EC2 public IP and infrastructure changes.
- Application Load Balancer target health.
- Availability-zone and subnet configuration.

## Security Notes

- AWS credentials and private SSH keys must not be committed to GitHub.
- Jenkins credentials are used for SSH authentication.
- EC2 IAM roles provide instance-level AWS access.
- Terraform state files should be stored securely and excluded from public source control.

## Project Scope and Limitations

This project demonstrates a practical AWS-based CI/CD deployment workflow.

The current deployment replaces the running application container during deployment, so a period of downtime may occur.

The presence of Kubernetes configuration in the repository does not, by itself, establish that a Kubernetes deployment is operational.
