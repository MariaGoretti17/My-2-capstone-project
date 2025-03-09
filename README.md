# My-2-capstone-project
# Docker CI/CD Pipeline

This repository is part of my Capstone project for cloud engineering. The project involves setting up a Docker-based Continuous Integration/Continuous Deployment (CI/CD) pipeline that pushes Docker images to Amazon Elastic Container Registry (ECR) using GitHub Actions.

## Project Overview

The goal of this project is to build, tag, and push Docker images to Amazon ECR for different environments (Dev, Staging, and Prod). This is done through the use of a GitHub Actions workflow that automates the process. The pipeline triggers on changes to the repository and pushes the appropriate Docker image to the Amazon ECR repository.

## Technologies Used

- **Docker**: Containerization for the application.
- **GitHub Actions**: CI/CD pipeline to automate the build and push process.
- **Amazon Web Services (AWS)**:
  - **ECR**: For storing Docker images.
  - **IAM**: For managing permissions and credentials.
- **Node.js**: For building Docker images that run a Node.js application.

## Setup Instructions

### Prerequisites

- **GitHub** account and repository.
- **AWS** account with permissions to create ECR repositories and manage IAM users.
- **Docker** installed locally for building images.
- AWS **access keys** stored in GitHub secrets (e.g., `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`).

### Steps to Set Up

1. Clone the repository to your local machine.
2. Create a `Dockerfile` in your project to define the image's build instructions.
3. Configure GitHub Secrets for AWS access keys and region.
4. Set up GitHub Actions with a workflow defined in `.github/workflows/docker-pipeline.yml`. The workflow will trigger on pushes to the `docker-github-actions` branch and automate the Docker image build and push process to Amazon ECR.

## Workflow Details

The workflow defined in `.github/workflows/docker-pipeline.yml` does the following:

- Checks out the code from the repository.
- Configures AWS credentials using stored secrets.
- Logs into Amazon ECR using the `aws-actions/amazon-ecr-login` action.
- Sets a short commit SHA as the image tag.
- Builds and tags the Docker image with the commit SHA and `latest` tag.
- Pushes the Docker image to Amazon ECR with both tags.

## Troubleshooting

- If you encounter issues with the Docker build, ensure that your `Dockerfile` is correctly set up and that all dependencies are properly installed.
- If the workflow fails, check the GitHub Actions logs for detailed error messages. Common errors often involve incorrect AWS credentials or missing Docker configuration.

## How to Trigger the Workflow

- The workflow is triggered by **push** events to the `docker-github-actions` branch. Any push to this branch will automatically build and push a Docker image to Amazon ECR.
- You can manually trigger the workflow from the GitHub Actions interface if `workflow_dispatch` is enabled in your workflow file.
