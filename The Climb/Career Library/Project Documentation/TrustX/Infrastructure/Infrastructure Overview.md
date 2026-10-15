---
kind: "project-document"
title: "Infrastructure Overview"
collection: "TrustX"
topic: "Infrastructure"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/README.md"]
tags: ["career/library","career/project-docs"]
---

# Infrastructure Overview

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# AWS CDK Infrastructure

This repository contains AWS CDK infrastructure code for deploying all Trustx environments and services, including VPC, RDS, Lambda, and ECS/Fargate workloads (such as n8n and Postgres+AGE).

## Unified Deployment (All Stacks)

All stacks—including core infrastructure and ECS/Fargate services—are now deployed from a single entrypoint: `bin/app.ts`.

### Prerequisites
- Node.js (v14 or later)
- AWS CLI configured with appropriate credentials
- AWS CDK CLI installed (`npm install -g aws-cdk`)
- TypeScript (`npm install -g typescript`)

### Install Dependencies
```bash
npm install
```

### Deploy All Stacks (Dev Example)
To deploy all stacks for the `dev` environment in `us-east-2`:

```bash
npx cdk deploy --all --app 'npx ts-node bin/app.ts' --context env=dev --context imageTag=latest --region us-east-2 --require-approval never
```

- `--context env=dev` sets the environment (use `stg` or `prod` as needed)
- `--context imageTag=latest` sets the Docker image tag for ECS workloads (update as needed)
- `--region us-east-2` sets the AWS region
- `--require-approval never` disables approval prompts for IAM changes

**All core and ECS/Fargate stacks will be deployed in one command.**

### Destroy All Stacks
To destroy all stacks for the dev environment:
```bash
npx cdk destroy --all --app 'npx ts-node bin/app.ts' --context env=dev --region us-east-2 --force
```

## Environment Configuration

Environments and stack settings are managed in `config/environment-config.ts`. Update this file to change VPC, database, or ECS/Fargate settings for each environment.

## Troubleshooting
- Ensure your AWS credentials and region are correct.
- If you see Fargate configuration errors, check `memoryLimitMiB` and `cpu` in `config/environment-config.ts`.
- For ECS image updates, set `--context imageTag=<your-tag>` to deploy a new container version.

## Additional Resources
- See `DEPLOYMENT_GUIDE.md` and `N8N_ECS_DEPLOYMENT_GUIDE_UPDATED.md` for advanced ECS/n8n deployment and maintenance details.

---

For more details on stack structure and customization, see the documentation in the `docs/` folder.

## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/README.md) · Samay + Trustx experience/TrustxRepos/AWS/README.md

Project code and dependencies remain outside the vault. No source commands were executed.
