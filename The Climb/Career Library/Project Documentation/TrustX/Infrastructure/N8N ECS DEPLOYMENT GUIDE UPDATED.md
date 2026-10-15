---
kind: "project-document"
title: "N8N ECS DEPLOYMENT GUIDE UPDATED"
collection: "TrustX"
topic: "Infrastructure"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/N8N_ECS_DEPLOYMENT_GUIDE_UPDATED.md"]
tags: ["career/library","career/project-docs"]
---

# N8N ECS DEPLOYMENT GUIDE UPDATED

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# N8N Deployment Guide for AWS ECS

This guide explains how to deploy n8n workflow automation tool to AWS ECS (Elastic Container Service) with proper data persistence, database configuration, S3 access, and API Gateway integration.

## Overview

The deployment consists of:

1. **Docker Container**: n8n workflow automation tool containerized with Docker
2. **ECS Fargate**: Serverless compute engine for containers
3. **EFS Volume**: Persistent storage for n8n workflows and data
4. **PostgreSQL Database**: External database for n8n data
5. **Secrets Manager**: Secure storage for database credentials
6. **API Gateway**: REST API for accessing the n8n service
7. **S3 Access**: Permissions to access S3 buckets

## Prerequisites

- AWS CLI installed and configured with appropriate permissions
- Docker installed with buildx support (Docker Desktop recommended)
- Node.js and npm installed
- AWS CDK installed (`npm install -g aws-cdk`)
- PostgreSQL database accessible from your VPC
- Existing VPC with private subnets (optional)
- Existing security groups (optional)

## Deployment Steps

### 1. Set Up Database Credentials in AWS Secrets Manager

Create a secret in AWS Secrets Manager with your database credentials:

```bash
./scripts/create-n8n-db-secret.sh dev us-east-2 my-postgres.example.com n8n n8n_user password
```

This script will create a secret with the following structure:

```json
{
  "DB_TYPE": "postgresdb",
  "DB_POSTGRESDB_HOST": "my-postgres.example.com",
  "DB_POSTGRESDB_DATABASE": "n8n",
  "DB_POSTGRESDB_USER": "n8n_user",
  "DB_POSTGRESDB_PASSWORD": "password",
  "DB_POSTGRESDB_PORT": "5432",
  "DB_POSTGRESDB_SCHEMA": "public"
}
```

### 2. Set Up Docker Buildx for Multi-Platform Builds

Run the setup script to ensure Docker buildx is properly configured:

```bash
./scripts/setup-docker-buildx.sh
```

### 3. Deploy to ECS

Use the deployment script with your desired environment, region, and optional parameters:

```bash
./scripts/deploy-tests-framework-ecs.sh dev us-east-2 \
  --vpc-id=vpc-123456789 \
  --db-secret-arn=arn:aws:secretsmanager:us-east-2:123456789012:secret:dev/n8n/db-credentials \
  --s3-buckets=my-bucket-1,my-bucket-2 \
  --private-subnets=subnet-123,subnet-456 \
  --security-group=sg-123456
```

Parameters:
- `dev`: Environment name
- `us-east-2`: AWS region
- `--vpc-id`: Your VPC ID (optional, will use default if not provided)
- `--db-secret-arn`: The ARN of the database secret created in step 1
- `--s3-buckets`: Comma-separated list of S3 bucket names to grant access to
- `--private-subnets`: Comma-separated list of private subnet IDs to deploy into
- `--security-group`: Security group ID to use for the ECS tasks

### 4. Access the Application

After deployment completes, the script will output two URLs:

1. **Load Balancer URL**: Direct access to the n8n service
   ```
   http://tests-framework-dev-lb-123456789.us-east-2.elb.amazonaws.com
   ```

2. **API Gateway URL**: Access through API Gateway
   ```
   https://abcdef1234.execute-api.us-east-2.amazonaws.com/dev/
   ```

## Architecture Details

### ECS Configuration

- **Task Definition**: Fargate task with 1 vCPU and 2GB memory
- **Service**: Single task with public IP assignment (or private subnets if specified)
- **Security Groups**: Uses existing security group or creates a new one

### EFS Configuration

- **File System**: General purpose EFS with bursting throughput
- **Access Point**: Configured with proper permissions for n8n
- **Mount Point**: Mounted at `/home/node/.n8n` in the container

### Database Configuration

- **Connection**: Uses environment variables from AWS Secrets Manager
- **Security**: Database credentials are securely stored and accessed

### API Gateway Configuration

- **REST API**: Configured to proxy all requests to the n8n service
- **Logging**: Comprehensive access logs in CloudWatch
- **CORS**: Configured to allow cross-origin requests

### S3 Access

- **IAM Permissions**: Task role has permissions to access specified S3 buckets
- **Actions**: ListBucket, GetObject, PutObject, DeleteObject

## Troubleshooting

### Platform Compatibility Issues

If you encounter the error:
```
CannotPullContainerError: pull image manifest has been retried 5 time(s): image Manifest does not contain descriptor matching platform 'linux/amd64'
```

Make sure Docker buildx is properly set up by running:
```bash
./scripts/setup-docker-buildx.sh
```

### Database Connection Issues

If n8n can't connect to the database:

1. Check that the database is accessible from the VPC
2. Verify the database credentials in the AWS Secrets Manager
3. Check the ECS task logs for specific error messages

### EFS Mount Issues

If the EFS volume doesn't mount properly:

1. Check that the security groups allow NFS traffic (port 2049)
2. Verify that the EFS access point is configured correctly
3. Check the ECS task logs for mount errors

## Maintenance

### Updating n8n

To update n8n to a newer version:

1. Update the version in the Dockerfile-simple file
2. Run the deployment script again

### Backing Up Data

The n8n data is stored in two places:

1. **Workflows and Credentials**: In the EFS volume
2. **Execution History**: In the PostgreSQL database

To back up:
- Use AWS Backup for the EFS volume
- Use standard PostgreSQL backup procedures for the database

## Security Considerations

1. **Authentication**: Consider enabling basic authentication for production environments
2. **HTTPS**: API Gateway provides HTTPS by default
3. **Network Security**: Use private subnets and security groups to restrict access
4. **Secrets**: Use AWS Secrets Manager for sensitive information

## Conclusion

You now have a fully functional n8n deployment on AWS ECS with:
- Proper data persistence using EFS
- Database integration with PostgreSQL
- Platform compatibility with ECS
- API Gateway integration
- S3 access permissions
- Scalable infrastructure using AWS managed services


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/N8N_ECS_DEPLOYMENT_GUIDE_UPDATED.md) · Samay + Trustx experience/TrustxRepos/AWS/N8N_ECS_DEPLOYMENT_GUIDE_UPDATED.md

Project code and dependencies remain outside the vault. No source commands were executed.
