---
kind: "project-document"
title: "N8n-cdk-deployment-guide"
collection: "TrustX"
topic: "Infrastructure"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/docs/n8n-cdk-deployment-guide.md"]
tags: ["career/library","career/project-docs"]
---

# N8n-cdk-deployment-guide

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# n8n CDK Deployment Guide

This guide explains how to deploy the n8n workflow automation tool using AWS CDK (Cloud Development Kit).

## Prerequisites

Before you begin, ensure you have the following:

1. **AWS CLI** installed and configured with appropriate permissions
2. **Node.js and npm** installed (version 14.x or later recommended)
3. **AWS CDK** installed globally: `npm install -g aws-cdk`
4. **Docker** installed and running (for building the container image)
5. **Docker Buildx** support (included in Docker Desktop)

## Deployment Options

There are several scripts available for deploying n8n with CDK:

### 1. Standard CDK Deployment

The most straightforward way to deploy n8n is using the CDK deployment script:

```bash
./scripts/deploy-n8n-cdk.sh dev us-east-2
```

This script:
- Builds and pushes the Docker image to ECR
- Deploys the CDK stack with all necessary resources
- Waits for the service to become available
- Outputs the URL where you can access n8n

### 2. Deployment with Custom Parameters

You can customize the deployment with various parameters:

```bash
./scripts/deploy-n8n-cdk.sh dev us-east-2 \
  --vpc-id=vpc-123456789 \
  --s3-buckets=bucket1,bucket2 \
  --private-subnets=subnet-123,subnet-456 \
  --security-group=sg-123456
```

Available parameters:
- `--vpc-id`: Specify a custom VPC ID
- `--s3-buckets`: Comma-separated list of S3 buckets to grant access to
- `--private-subnets`: Comma-separated list of private subnet IDs
- `--security-group`: Security group ID for the ECS tasks
- `--skip-image-build`: Skip building and pushing the Docker image
- `--cdk-debug`: Enable CDK debugging output

### 3. Skip Image Build

If you've already built and pushed the Docker image, you can skip that step:

```bash
./scripts/deploy-n8n-cdk.sh dev us-east-2 --skip-image-build
```

## What Gets Deployed

The CDK stack deploys the following resources:

1. **ECS Cluster**: A Fargate cluster to run the n8n container
2. **ECS Task Definition**: Defines the n8n container configuration
3. **ECS Service**: Runs and maintains the n8n task
4. **EFS File System**: Persistent storage for n8n workflows and data
5. **Application Load Balancer**: Routes traffic to the n8n service
6. **Security Groups**: Controls network access to the resources
7. **IAM Roles**: Provides necessary permissions
8. **CloudWatch Log Group**: Collects container logs

## HTTPS Configuration

The deployment automatically configures HTTPS with the following:

- HTTPS listener on port 443 with the specified ACM certificate
- HTTP to HTTPS redirection from port 80
- Recommended SSL security policy

## Checking Deployment Status

After deployment, you can check the status of the service:

```bash
./scripts/check-n8n-status.sh dev us-east-2
```

This will show:
- Service status
- Task status
- Load balancer URL
- Health check status

## Troubleshooting

If you encounter issues with the deployment, use these scripts:

```bash
# Check the CloudFormation stack status
./scripts/check-stack-status.sh dev us-east-2

# Check the ECS cluster and services
./scripts/check-ecs-cluster.sh dev us-east-2

# Check the n8n API
./scripts/check-n8n-api.sh dev us-east-2

# Fix a missing ECS service
./scripts/fix-missing-service.sh dev us-east-2
```

## Updating the Deployment

To update an existing deployment with a new n8n version:

```bash
# Update the version in src/tests-framework/Dockerfile-amd64
# Then run the deployment script again
./scripts/deploy-n8n-cdk.sh dev us-east-2
```

Or force a redeployment without changing the image:

```bash
./scripts/force-redeploy-n8n.sh dev us-east-2
```

## Destroying the Stack

When you're done with the n8n deployment, you can destroy the stack:

```bash
./scripts/destroy-n8n-cdk.sh dev us-east-2
```

This will:
- Destroy all resources created by the CDK stack
- Optionally delete the ECR repository
- Check for any remaining resources

To skip the confirmation prompt, use the `--force` flag:

```bash
./scripts/destroy-n8n-cdk.sh dev us-east-2 --force
```

## Manual CDK Commands

If you prefer to run CDK commands manually:

```bash
# Deploy the stack
npx cdk deploy dev-tests-framework-ecs-stack \
  --app 'npx ts-node bin/app.ts' \
  --context env=dev \
  --region=us-east-2 \
  --require-approval never

# Destroy the stack
npx cdk destroy dev-tests-framework-ecs-stack \
  --app 'npx ts-node bin/app.ts' \
  --context env=dev \
  --region=us-east-2 \
  --force
```

## CDK Stack Structure

The n8n CDK stack is defined in `lib/tests-framework-stack-ecs.ts` and includes:

- ECS Fargate service configuration
- EFS volume for persistent storage
- Load balancer with HTTPS support
- Security groups and IAM roles
- Environment variables for n8n configuration

## Customizing the Stack

To customize the stack beyond the available parameters:

1. Edit `lib/tests-framework-stack-ecs.ts` to modify the CDK stack definition
2. Edit `src/tests-framework/Dockerfile-amd64` to modify the container image
3. Deploy with the updated code using the deployment script


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/docs/n8n-cdk-deployment-guide.md) · Samay + Trustx experience/TrustxRepos/AWS/docs/n8n-cdk-deployment-guide.md

Project code and dependencies remain outside the vault. No source commands were executed.
