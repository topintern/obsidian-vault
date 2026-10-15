---
kind: "project-document"
title: "SOC2 Lambda Overview"
collection: "TrustX"
topic: "Infrastructure"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/src/soc2-lambda/README.md"]
tags: ["career/library","career/project-docs"]
---

# SOC2 Lambda Overview

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# SOC2 AppSync GraphQL API

This directory contains the implementation of the SOC2 AppSync GraphQL API for the TrustX platform.

## Overview

The SOC2 AppSync GraphQL API provides a GraphQL interface for managing SOC2 compliance data, including:

- SOC2 categories
- SOC2 controls
- Implementation status
- Control evidence

## Architecture

The API is built using AWS AppSync, which is a fully managed GraphQL service. It uses the following AWS services:

- **AWS AppSync**: Provides the GraphQL API endpoint and schema
- **AWS Lambda**: Resolves GraphQL queries and mutations
  - Uses environment-specific Lambda layers:
    - **Dev Environment**:
      - `arn:aws:lambda:us-east-2:898466741470:layer:psycopg2-py39:1` for PostgreSQL connectivity
      - `arn:aws:lambda:us-east-2:533267024692:layer:db-utils-6f6310dc:4` for database utilities and JWT validation
    - **Other Environments**:
      - Uses layers from ConfigureLambdaStack
- **Amazon RDS**: Stores SOC2 compliance data
- **AWS Secrets Manager**: Manages database credentials

## Database Schema

The API uses two main tables:

1. **soc2_categories**: Stores information about SOC2 categories
   - `code`: Category code (e.g., CC, A, C, PI, P)
   - `name`: Category name
   - `description`: Category description
   - `weight`: Category weight (for reporting)
   - `tenant_id`: Tenant identifier for multi-tenancy

2. **soc2_controls**: Stores information about SOC2 controls
   - `id`: Control ID
   - `name`: Control name
   - `description`: Control description
   - `category_code`: Reference to category
   - `status`: Implementation status (IMPLEMENTED, IN_PROGRESS, NOT_IMPLEMENTED)
   - `owner`: Control owner
   - `last_tested`: Date of last test
   - `evidence`: JSON array of evidence links
   - `test_pass_rate`: Test pass rate percentage
   - `exceptions`: Number of exceptions
   - `tenant_id`: Tenant identifier for multi-tenancy

## GraphQL Schema

The GraphQL schema defines the following types:

- `SOC2Category`: Represents a SOC2 category
- `SOC2Control`: Represents a SOC2 control
- `SOC2ImplementationStatus`: Represents the overall implementation status
- `ImplementationStatus`: Enum for control status (IMPLEMENTED, IN_PROGRESS, NOT_IMPLEMENTED)

And the following operations:

- Queries:
  - `getSOC2Categories`: Get all SOC2 categories
  - `getSOC2Controls`: Get all SOC2 controls
  - `getSOC2ControlsByCategory`: Get controls for a specific category
  - `getSOC2ImplementationStatus`: Get overall implementation status

- Mutations:
  - `createSOC2Control`: Create a new SOC2 control
  - `updateSOC2ControlStatus`: Update the status of a SOC2 control

## Deployment

To deploy the SOC2 AppSync GraphQL API, run the following command:

```bash
./scripts/deploy-soc2-appsync.sh [--env=<environment>] [--region=<aws-region>] [--account=<aws-account-id>]
```

Examples:
```bash
# Deploy to dev environment
./scripts/deploy-soc2-appsync.sh --env=dev

# Deploy to staging environment
./scripts/deploy-soc2-appsync.sh --env=stg
```

This script will:
1. Build the CDK project
2. Deploy the SOC2 AppSync stack with the specified environment context

Note: Database setup is handled outside of this repository. The script assumes that the necessary database tables already exist.

## Accessing the GraphQL API

After deployment, the stack will output the GraphQL API URL. You can use this URL in your frontend application by setting the `REACT_APP_GRAPHQL_ENDPOINT` environment variable:

```
REACT_APP_GRAPHQL_ENDPOINT=https://your-appsync-api-endpoint.amazonaws.com/graphql
```

You can retrieve the URL using the AWS CLI:

```bash
aws cloudformation describe-stacks --stack-name <env>-soc2-appsync-stack --query "Stacks[0].Outputs[?OutputKey=='GraphQLApiUrl'].OutputValue" --output text
```

Or view it in the AWS Console under CloudFormation > Stacks > <env>-soc2-appsync-stack > Outputs.

### Environments

- **dev**: Uses existing infrastructure
  - VPC ID: vpc-069dd170c05827f66
  - Private Subnets: subnet-06b253809582a469e, subnet-02cf7012224081bb2
  - Security Group: sg-09e025b93aa49459c
  - Database: Uses existing RDS instance with pre-created schema
  - Secret: Uses existing Secrets Manager secret for database credentials
  - Note: Database schema creation is skipped for dev environment

- **stg**: Creates new infrastructure
  - Creates new VPC and security groups
  - Creates new RDS instance
  - Creates new Secrets Manager secret for database credentials

## Authentication

The API supports two authentication methods:

1. **API Key Authentication**: For development and testing purposes
   - The API key is generated during deployment and output as `GraphQLApiKey`
   - Include the API key in the `x-api-key` header

2. **Auth0 JWT Authentication**: For production use
   - The API is configured to use Auth0 as an OIDC provider
   - Each request must include an Auth0 JWT token in the Authorization header
   - The JWT token must be issued by the Auth0 domain specified in the environment config
   - The audience must match the audience specified in the environment config

## CORS Considerations

If you're accessing the GraphQL API from a different domain than where it's hosted, you may need to handle CORS. This can be done at the client level by using appropriate headers in your requests.

## Multi-tenancy

The API supports multi-tenancy by including a tenant ID in all database queries. The tenant ID is extracted from the request headers.

## Development

To develop the API locally:

1. Install dependencies:
   ```bash
   npm install
   ```

2. Build the project:
   ```bash
   npm run build
   ```

3. Deploy to your development environment:
   ```bash
   ENV=dev ./scripts/deploy-soc2-appsync.sh
   ```


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/src/soc2-lambda/README.md) · Samay + Trustx experience/TrustxRepos/AWS/src/soc2-lambda/README.md

Project code and dependencies remain outside the vault. No source commands were executed.
