---
kind: "project-document"
title: "N8n-ecs-troubleshooting"
collection: "TrustX"
topic: "Infrastructure"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/docs/n8n-ecs-troubleshooting.md"]
tags: ["career/library","career/project-docs"]
---

# N8n-ecs-troubleshooting

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# N8N ECS Deployment Troubleshooting Guide

This document provides solutions for common issues encountered when deploying n8n to AWS ECS.

## Architecture Mismatch Issues

### Problem 1: "exec /sbin/tini: exec format error"

When deploying n8n on ECS, you see the following error in CloudWatch logs:

```
exec /sbin/tini: exec format error
```

This error occurs when there's an architecture mismatch between the container image and the ECS host system. Specifically:

1. The Docker image was built or pulled on an ARM64 system (like an M1/M2 Mac)
2. The image was pushed to ECR without specifying the target platform
3. ECS tries to run the ARM64 image on AMD64 (x86_64) hardware

### Problem 2: "image Manifest does not contain descriptor matching platform 'linux/amd64'"

You might also see this error in the ECS task status:

```
CannotPullContainerError: pull image manifest has been retried 5 time(s): image Manifest does not contain descriptor matching platform 'linux/amd64'
```

This occurs when the image in ECR doesn't have a manifest for the AMD64 platform, which is what ECS is trying to use.

### Solution

Use one of the following approaches to ensure you're using the correct architecture:

#### Option 1: Use the default approach (recommended)

```bash
./scripts/deploy-tests-framework-ecs.sh dev us-east-2 [other options]
```

This approach pulls the n8n image specifically by its AMD64 digest, ensuring you get the correct architecture.

#### Option 2: Use the custom Dockerfile with buildx

```bash
./scripts/deploy-tests-framework-ecs.sh dev us-east-2 --use-custom-dockerfile=true [other options]
```

This approach uses Docker buildx to build and push a multi-architecture image, ensuring the AMD64 platform is available.

### Technical Details

When working with Docker on ARM-based systems (like M1/M2 Macs), Docker will by default pull or build images for the host architecture (ARM64). However, AWS ECS typically runs on x86_64/AMD64 instances.

The updated deployment script handles this in two ways:
1. For the default approach, it pulls the image by its specific AMD64 digest
2. For the custom Dockerfile approach, it uses Docker buildx to build for the AMD64 platform

Both approaches ensure that the image in ECR has the correct architecture manifest for ECS to use.

## ECR Image Issues

### Problem

ECS task status shows "Task is stopping" with errors like:

```
CannotPullContainerError: pull image manifest has been retried 5 time(s): image Manifest does not contain descriptor matching platform 'linux/amd64'
```

or

```
CannotPullContainerError: Error response from daemon: manifest for 123456789012.dkr.ecr.us-east-2.amazonaws.com/trustx/tests-framework-dev:latest not found: manifest unknown
```

### Solution

These errors indicate issues with the ECR repository or the image. Use the provided scripts to diagnose and fix the issues:

1. Check the ECR repository and image:
   ```bash
   ./scripts/check-ecr-image.sh dev us-east-2
   ```
   This will verify that the ECR repository exists and contains an image with the correct architecture.

2. Fix ECR image issues:
   ```bash
   ./scripts/fix-ecr-image.sh dev us-east-2
   ```
   This will create the ECR repository if it doesn't exist, build and push a new image with the correct architecture, and force a new deployment of the ECS service.

### Technical Details

The ECR repository is referenced in the CDK stack using:
```typescript
const repository = ecr.Repository.fromRepositoryName(
  this,
  'TestsFrameworkRepository',
  `trustx/tests-framework-${env}`
);
```

This assumes that the repository already exists. The deployment script creates the repository if it doesn't exist, but if there are issues with the repository or the image, the ECS task will fail to start.

## Database Secret Issues

### Problem

ECS task fails to start with errors like:

```
ResourceInitializationError: unable to pull secrets or registry auth: execution resource retrieval failed: unable to retrieve secret from asm: service call has been retried 1 time(s): retrieved secret from Secrets Manager did not contain json key DB_TYPE
```

### Solution

This error occurs when the AWS Secrets Manager secret doesn't contain all the required fields for n8n database configuration. Use the provided scripts to fix the issue:

1. Check and update the database secret:
   ```bash
   ./scripts/fix-db-secret.sh dev us-east-2 arn:aws:secretsmanager:us-east-2:123456789012:secret:dev/n8n/db-credentials
   ```
   This will check if all required fields are present in the secret and prompt you to update it if needed.

2. Or create a new database secret with all required fields:
   ```bash
   ./scripts/create-n8n-db-secret-complete.sh dev us-east-2 my-postgres.example.com n8n n8n_user password
   ```
   This will create a new secret with all the required fields for n8n.

### Technical Details

n8n requires the following fields in the database secret:
- `DB_TYPE`: The database type (should be "postgresdb")
- `DB_POSTGRESDB_HOST`: The database host
- `DB_POSTGRESDB_DATABASE`: The database name
- `DB_POSTGRESDB_USER`: The database username
- `DB_POSTGRESDB_PASSWORD`: The database password
- `DB_POSTGRESDB_PORT`: The database port (default: 5432)
- `DB_POSTGRESDB_SCHEMA`: The database schema (default: "public")

If any of these fields are missing, the ECS task will fail to start.

## Database Connection Issues

### Problem

n8n fails to connect to the PostgreSQL database, showing errors like:

```
Error: connect ECONNREFUSED 127.0.0.1:5432
```

### Solution

1. Verify that the database secret ARN is correctly passed to the deployment script
2. Check that the security group allows traffic from the ECS task to the database
3. Ensure the database credentials in the secret are correct

## EFS Mount Issues

### Problem

n8n container fails to start with errors related to mounting the EFS volume.

### Solution

1. Verify that the EFS security group allows NFS traffic (port 2049) from the ECS task security group
2. Check that the EFS access point is correctly configured
3. Ensure the ECS task execution role has permissions to mount the EFS volume

## Container Exit Issues

### Problem

ECS task status shows "Task is stopping" and "Essential container in task exited".

### Possible Causes and Solutions

#### 1. Permission Issues with EFS Mount

**Symptoms:**
- Container exits shortly after starting
- Logs show permission denied errors for `/home/node/.n8n`

**Solution:**
- Verify the EFS access point is configured with the correct UID/GID (1000/1000)
- Check that the ECS task execution role has permissions to mount the EFS volume
- Ensure the EFS security group allows NFS traffic from the ECS task security group

#### 2. Environment Variable Issues

**Symptoms:**
- Container exits with configuration errors
- Logs show missing or invalid environment variables

**Solution:**
- Check that all required environment variables are properly set in the task definition
- Verify that the database secret is correctly referenced
- Ensure the `N8N_USER_FOLDER` is set to `/home/node/.n8n`

#### 3. Memory/CPU Constraints

**Symptoms:**
- Container exits with OOM (Out of Memory) errors
- Task is killed by the system

**Solution:**
- Increase the memory allocation in the task definition
- Check for memory leaks in custom workflows
- Consider increasing CPU allocation if CPU throttling is occurring

#### 4. Database Connection Issues

**Symptoms:**
- Container exits after failing to connect to the database
- Logs show database connection errors

**Solution:**
- Verify that the database is accessible from the ECS task
- Check that the database credentials in the secret are correct
- Ensure the security group allows traffic from the ECS task to the database

### How to Get Container Logs

Use the provided script to retrieve logs from the failed container:

```bash
./scripts/get-ecs-logs.sh dev us-east-2
```

This will show the logs from the most recent task and provide information about why the container exited.

## API Gateway Connection Issues

### Problem

Unable to access n8n through the API Gateway URL.

### Solution

1. Verify that the API Gateway integration is correctly configured
2. Check that the security group allows traffic from the API Gateway to the ECS task
3. Ensure the health check path is correctly configured in the target group


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/docs/n8n-ecs-troubleshooting.md) · Samay + Trustx experience/TrustxRepos/AWS/docs/n8n-ecs-troubleshooting.md

Project code and dependencies remain outside the vault. No source commands were executed.
