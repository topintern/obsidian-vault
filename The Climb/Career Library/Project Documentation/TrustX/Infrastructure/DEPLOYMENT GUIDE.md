---
kind: "project-document"
title: "DEPLOYMENT GUIDE"
collection: "TrustX"
topic: "Infrastructure"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/DEPLOYMENT_GUIDE.md"]
tags: ["career/library","career/project-docs"]
---

# DEPLOYMENT GUIDE

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# N8N Deployment Guide for AWS ECS

This guide explains how to deploy the n8n workflow automation tool to AWS ECS (Elastic Container Service) using the provided scripts.

## Prerequisites

- AWS CLI installed and configured with appropriate permissions
- Docker installed with buildx support (Docker Desktop recommended)
- Node.js and npm installed
- AWS CDK installed (`npm install -g aws-cdk`)

## Deployment Steps

### 1. Set Up Docker Buildx for Multi-Platform Builds

Run the setup script to ensure Docker buildx is properly configured:

```bash
./scripts/setup-docker-buildx.sh
```

This script:
- Checks if Docker buildx is available
- Creates a new builder instance if needed
- Sets up multi-platform build support

### 2. Deploy to ECS

Use the deployment script with your desired environment and region:

```bash
./scripts/deploy-tests-framework-ecs.sh dev us-east-2
```

Replace `dev` with your environment name and `us-east-2` with your desired AWS region.

The script will:
1. Log in to Amazon ECR
2. Build a Docker image specifically for the linux/amd64 platform
3. Push the image to ECR
4. Deploy the CDK stack to create the ECS service

### 3. Access the Application

After deployment completes, the script will output the URL where you can access the n8n application.

## Troubleshooting

### Platform Compatibility Issues

If you encounter the error:
```
CannotPullContainerError: pull image manifest has been retried 5 time(s): image Manifest does not contain descriptor matching platform 'linux/amd64'
```

This means the Docker image was not built for the correct platform. Make sure:

1. You're using the updated deployment script that includes the `--platform linux/amd64` flag
2. Docker buildx is properly set up
3. The Dockerfile includes the platform specification

### ECR Repository Issues

If the repository doesn't exist, create it first:

```bash
aws ecr create-repository --repository-name trustx/tests-framework-dev --image-scanning-configuration scanOnPush=true --region us-east-2
```

Replace `dev` with your environment name and `us-east-2` with your desired AWS region.

### CDK Deployment Issues

If CDK deployment fails, check:

1. Your AWS credentials are valid
2. You have the necessary permissions
3. The VPC ID in the stack configuration exists in your account

## Maintenance

### Updating the Application

To update the application:

1. Make your changes to the application code
2. Run the deployment script again
3. The new image will be built, pushed, and deployed

### Monitoring

Monitor your ECS service through:
- AWS ECS Console
- CloudWatch Logs
- CloudWatch Alarms

## Additional Resources

- [AWS ECS Documentation](https://docs.aws.amazon.com/ecs/)
- [Docker Buildx Documentation](https://docs.docker.com/buildx/working-with-buildx/)
- [N8N Documentation](https://docs.n8n.io/)


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/DEPLOYMENT_GUIDE.md) · Samay + Trustx experience/TrustxRepos/AWS/DEPLOYMENT_GUIDE.md

Project code and dependencies remain outside the vault. No source commands were executed.
