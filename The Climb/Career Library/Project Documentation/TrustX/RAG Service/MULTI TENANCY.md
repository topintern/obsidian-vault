---
kind: "project-document"
title: "MULTI TENANCY"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/MULTI_TENANCY.md"]
tags: ["career/library","career/project-docs"]
---

# MULTI TENANCY

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Multi-Tenancy Implementation for Profile 360 AppRunner

## Overview

This document describes the multi-tenancy implementation for the Profile 360 AppRunner Flask API. The implementation follows the same pattern used in existing Lambda functions (document, policies, SOC2) to ensure consistency across the platform.

## Architecture

### 1. Database Layer (PostgreSQL)
- **public.tenants** table: Maps tenant names to tenant IDs
- **tenant_{id}** schemas: Each tenant has their own schema (e.g., `tenant_1`, `tenant_2`)
- Uses the existing `db_utils` layer for tenant resolution

### 2. Neo4j Layer
- Each tenant gets their own Neo4j database: `profile360_tenant_{id}`
- Separate Neo4j drivers are maintained per tenant
- Connection pooling and caching for performance

### 3. Authentication Layer
- JWT token validation using Auth0 (same as existing Lambdas)
- `X-Tenant-Name` header extraction from requests
- Tenant-to-tenant_id resolution using `db_utils.DatabaseOperations`

## API Endpoints

### Query Endpoint
```
POST /query
Headers:
  - Authorization: Bearer <jwt-token>
  - X-Tenant-Name: <tenant-name>
  - Content-Type: application/json

Body:
{
  "query": "Show me all users in the system"
}
```

### Tenant Management
```
GET /tenants
Headers:
  - Authorization: Bearer <jwt-token>

Response:
{
  "tenants": [
    {"tenant_id": "tenant-123", "name": "trustx"},
    {"tenant_id": "tenant-456", "name": "acme-corp"}
  ],
  "count": 2
}
```

### Tenant Status
```
GET /tenant/<tenant-name>/status
Headers:
  - Authorization: Bearer <jwt-token>
  - X-Tenant-Name: <tenant-name>

Response:
{
  "tenant": "trustx",
  "status": "connected",
  "message": "Successfully connected to Neo4j for tenant trustx"
}
```

### Health Check
```
GET /health

Response:
{
  "status": "healthy"
}
```

## Implementation Details

### MultiTenantNeo4jManager Class

```python
class MultiTenantNeo4jManager:
    def __init__(self):
        self.drivers = {}  # Cache drivers per tenant
        self.tenant_configs = {}  # Cache tenant configurations
    
    def get_tenant_id(self, tenant_name):
        """Get tenant_id from tenant_name using db_utils."""
        
    def get_driver(self, tenant_name):
        """Get or create a Neo4j driver for a specific tenant."""
        
    def list_tenants(self):
        """List all available tenants from the database."""
```

### Authentication Flow

1. **Extract Headers**: Get `X-Tenant-Name` and `Authorization` from request
2. **Validate JWT**: Use `db_utils.auth.validate_jwt()` with Auth0
3. **Resolve Tenant**: Use `db_utils.DatabaseOperations(tenant_name)` to get tenant_id
4. **Get Driver**: Create or retrieve cached Neo4j driver for tenant
5. **Process Request**: Execute query with tenant-specific driver

### Error Handling

- **Missing X-Tenant-Name**: Returns 400 Bad Request
- **Missing Authorization**: Returns 401 Unauthorized
- **Invalid JWT**: Returns 401 Unauthorized
- **Tenant Not Found**: Returns 400 Bad Request
- **Neo4j Connection Failed**: Returns 500 Internal Server Error

## Environment Variables

Required environment variables for multi-tenancy:

```bash
# PostgreSQL (for tenant resolution)
SECRET_ARN=arn:aws:secretsmanager:region:account:secret:name

# Neo4j (default configuration)
NEO4J_URI=neo4j+s://your-instance.databases.neo4j.io
NEO4J_USER=neo4j
NEO4J_PASSWORD=your-password

# Auth0 (for JWT validation)
AUTH0_DOMAIN=your-domain.auth0.com
AUTH0_AUDIENCE=your-api-audience
```

## Testing

Use the provided test script to verify multi-tenancy functionality:

```bash
# Update the test script with your JWT token
python test_multi_tenancy.py
```

## Deployment Considerations

### 1. Lambda Layers
The AppRunner container needs access to the `db_utils` layer:
- Copy `src/lambda_layers/db_utils/python` to the container
- Or mount as a volume in development

### 2. IAM Permissions
The AppRunner service needs:
- Secrets Manager read access for PostgreSQL credentials
- VPC access if PostgreSQL is in a private subnet

### 3. Neo4j Database Setup
Each tenant needs their own Neo4j database:
```cypher
CREATE DATABASE profile360_tenant_123;
CREATE DATABASE profile360_tenant_456;
```

## Security Considerations

1. **Tenant Isolation**: Each tenant's data is completely isolated in separate Neo4j databases
2. **JWT Validation**: All requests are validated against Auth0
3. **Connection Pooling**: Drivers are cached but isolated per tenant
4. **Error Messages**: Avoid leaking tenant information in error responses

## Future Enhancements

1. **Tenant-Specific Neo4j Instances**: Support different Neo4j clusters per tenant
2. **Rate Limiting**: Implement per-tenant rate limiting
3. **Monitoring**: Add tenant-specific metrics and logging
4. **Caching**: Implement tenant-aware caching layer
5. **Database Migration**: Tools for tenant database schema updates

## Troubleshooting

### Common Issues

1. **"db_utils not available"**: Ensure lambda layers are properly mounted
2. **"Tenant not found"**: Check tenant exists in `public.tenants` table
3. **"Neo4j connection failed"**: Verify Neo4j credentials and database exists
4. **"JWT validation failed"**: Check Auth0 configuration and token validity

### Debug Mode

Enable debug logging by setting:
```bash
DEBUG=true
```

This will provide detailed logs for tenant resolution and Neo4j connections.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/MULTI_TENANCY.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/MULTI_TENANCY.md

Project code and dependencies remain outside the vault. No source commands were executed.
