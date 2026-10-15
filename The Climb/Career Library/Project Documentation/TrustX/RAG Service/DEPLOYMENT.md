---
kind: "project-document"
title: "DEPLOYMENT"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/DEPLOYMENT.md"]
tags: ["career/library","career/project-docs"]
---

# DEPLOYMENT

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Deployment Guide

This guide provides instructions for deploying the Flask API to AWS App Runner using Docker and ECR.

## Deployment Workflow

### 1. Push code to GitHub

Push code to the GitHub repository named "AppRunner".

### 2. Build and Push Docker Image

Run the following commands to build and push the Docker image to ECR:

```bash
# Login to ECR
aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 533267024692.dkr.ecr.us-east-2.amazonaws.com

# Build Docker image for AWS Linux AMD64 architecture
docker build --platform linux/amd64 -t flaskbackendapi .

# Tag the image
docker tag flaskbackendapi:latest 533267024692.dkr.ecr.us-east-2.amazonaws.com/flaskbackendapi:latest

# Push to ECR
docker push 533267024692.dkr.ecr.us-east-2.amazonaws.com/flaskbackendapi:latest
```

### 3. AWS App Runner Configuration

The application is configured to run on AWS App Runner with the following settings:

- **Service name**: NL_TO_CYPHER
- **Port**: 5000
- **Environment variables**:
  - `OPENAI_API_KEY`: OpenAI API key
  - `NEO4J_URI`: Neo4j database URI
  - `NEO4J_USER`: Neo4j username
  - `NEO4J_PASSWORD`: Neo4j password

### 4. Troubleshooting

#### Neo4j Connection Issues

If you encounter a 503 Service Unavailable error or Neo4j connection issues:

1. Verify the Neo4j credentials in the AWS App Runner environment variables
2. Check the App Runner logs for detailed error messages
3. Use the `/check-neo4j` endpoint to verify the connection status

#### Dependency Conflicts

If you encounter dependency conflicts during Docker build:

1. Make sure the OpenAI version in requirements.txt is set to `openai>=1.6.1,<2.0.0`
2. Try building with the `--no-cache` flag:

```bash
docker build --no-cache --platform linux/amd64 -t flaskbackendapi .
```

### 5. Updating the Deployment

When you make changes to the application:

1. Push the changes to GitHub
2. Build and push a new Docker image to ECR
3. AWS App Runner will automatically deploy the new image


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/DEPLOYMENT.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/DEPLOYMENT.md

Project code and dependencies remain outside the vault. No source commands were executed.
