---
kind: "project-document"
title: "Api-documentation"
collection: "TrustX"
topic: "Frontend"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/trustx/docs/api-documentation.md"]
tags: ["career/library","career/project-docs"]
---

# Api-documentation

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# TrustX API Documentation

## API Overview

TrustX interacts with several APIs to manage compliance data, user information, and graph visualization. This document provides details about these API endpoints, their parameters, and expected responses.

## Authentication

All API requests require authentication using Auth0 tokens. The tokens are obtained during the authentication process and included in the request headers.

### Authentication Headers

```
Authorization: Bearer {access_token}
Content-Type: application/json
Accept: application/json
X-Tenant-Name: {tenant_name}
```

## REST API Endpoints

### Compliance Policies API

Base URL: `{REACT_APP_API_URL}/compliance/policies`

#### Get All Policies

- **Endpoint**: `GET /compliance/policies`
- **Description**: Retrieves all policies for the authenticated user's tenant
- **Parameters**: None
- **Response**: Array of policy objects
  ```json
  [
    {
      "id": "string",
      "title": "string",
      "description": "string",
      "status": "string",
      "owner": "string",
      "last_updated": "string",
      "trust_services_criteria": ["string"],
      "document_id": "string"
    }
  ]
  ```

#### Get Policy by ID

- **Endpoint**: `GET /compliance/policies/{policy_id}`
- **Description**: Retrieves a specific policy by ID
- **Parameters**: 
  - `policy_id` (path): The ID of the policy to retrieve
- **Response**: Policy object
  ```json
  {
    "id": "string",
    "title": "string",
    "description": "string",
    "status": "string",
    "owner": "string",
    "last_updated": "string",
    "trust_services_criteria": ["string"],
    "document_id": "string"
  }
  ```

#### Create Policy

- **Endpoint**: `POST /compliance/policies`
- **Description**: Creates a new policy
- **Request Body**:
  ```json
  {
    "title": "string",
    "description": "string",
    "status": "string",
    "owner": "string",
    "trust_services_criteria": ["string"]
  }
  ```
- **Response**: Created policy object with ID

#### Update Policy

- **Endpoint**: `PUT /compliance/policies/{policy_id}`
- **Description**: Updates an existing policy
- **Parameters**: 
  - `policy_id` (path): The ID of the policy to update
- **Request Body**:
  ```json
  {
    "title": "string",
    "description": "string",
    "status": "string",
    "owner": "string",
    "trust_services_criteria": ["string"]
  }
  ```
- **Response**: Updated policy object

#### Delete Policy

- **Endpoint**: `DELETE /compliance/policies/{policy_id}`
- **Description**: Deletes a policy
- **Parameters**: 
  - `policy_id` (path): The ID of the policy to delete
- **Response**: Success message

### Compliance Controls API

Base URL: `{REACT_APP_API_URL}/compliance/controls`

#### Get All Controls

- **Endpoint**: `GET /compliance/controls`
- **Description**: Retrieves all controls
- **Query Parameters**:
  - `framework` (optional): Filter by framework (e.g., "soc2")
  - `category` (optional): Filter by category code
  - `point_of_focus_id` (optional): Filter by point of focus ID
- **Response**: Array of control objects
  ```json
  [
    {
      "control_id": "string",
      "control_name": "string",
      "control_description": "string",
      "objective_id": "number",
      "objective_code": "string",
      "objective_title": "string",
      "status": "string",
      "owner_name": "string",
      "last_reviewed": "string",
      "framework": "string"
    }
  ]
  ```

#### Get Control by ID

- **Endpoint**: `GET /compliance/controls/{control_id}`
- **Description**: Retrieves a specific control by ID
- **Parameters**: 
  - `control_id` (path): The ID of the control to retrieve
- **Response**: Control object

#### Get Control Implementations

- **Endpoint**: `GET /compliance/controls/implementations`
- **Description**: Retrieves implementations for controls
- **Query Parameters**:
  - `control_id` (optional): Filter by control ID
- **Response**: Array of implementation objects

#### Get Control Evidence

- **Endpoint**: `GET /compliance/controls/{control_id}/evidence`
- **Description**: Retrieves evidence for a specific control
- **Parameters**: 
  - `control_id` (path): The ID of the control
- **Response**: Array of evidence objects

#### Get Control Exceptions

- **Endpoint**: `GET /compliance/controls/{control_id}/exceptions`
- **Description**: Retrieves exceptions for a specific control
- **Parameters**: 
  - `control_id` (path): The ID of the control
- **Response**: Array of exception objects

#### Get Frameworks

- **Endpoint**: `GET /compliance/controls/frameworks`
- **Description**: Retrieves available compliance frameworks
- **Response**: Array of framework objects

### Documents API

Base URL: `{REACT_APP_API_URL}/compliance/documents`

#### Get All Documents

- **Endpoint**: `GET /compliance/documents`
- **Description**: Retrieves all documents
- **Response**: Array of document objects
  ```json
  [
    {
      "id": "string",
      "title": "string",
      "content": "base64_string",
      "content_type": "string",
      "metadata": {
        "author": "string",
        "version": "string"
      },
      "created_at": "string",
      "updated_at": "string"
    }
  ]
  ```

#### Get Document by ID

- **Endpoint**: `GET /compliance/documents/{document_id}`
- **Description**: Retrieves a specific document by ID
- **Parameters**: 
  - `document_id` (path): The ID of the document to retrieve
- **Response**: Document object

#### Create Document

- **Endpoint**: `POST /compliance/documents`
- **Description**: Creates a new document
- **Request Body**:
  ```json
  {
    "title": "string",
    "content": "base64_string",
    "content_type": "string",
    "document_type": "string",
    "metadata": {
      "author": "string",
      "version": "string"
    }
  }
  ```
- **Response**: Created document object with ID

#### Update Document

- **Endpoint**: `PUT /compliance/documents/{document_id}`
- **Description**: Updates an existing document
- **Parameters**: 
  - `document_id` (path): The ID of the document to update
- **Request Body**:
  ```json
  {
    "title": "string",
    "content": "base64_string",
    "content_type": "string",
    "metadata": {
      "author": "string",
      "version": "string"
    }
  }
  ```
- **Response**: Updated document object

#### Delete Document

- **Endpoint**: `DELETE /compliance/documents/{document_id}`
- **Description**: Deletes a document
- **Parameters**: 
  - `document_id` (path): The ID of the document to delete
- **Response**: Success message

### Neo4j Query API

Base URL: `{REACT_APP_API_URL}/Get_Cypher_Query`

#### Generate and Execute Cypher Query

- **Endpoint**: `POST /Get_Cypher_Query`
- **Description**: Generates a Cypher query from natural language and executes it
- **Request Body**:
  ```json
  {
    "query": "string"
  }
  ```
- **Response**: 
  ```json
  {
    "query": "string"
  }
  ```

### Chatbot API

Base URL: `{REACT_APP_API_URL}/api/chatbot`

#### Chat Interaction

- **Endpoint**: `POST /api/chatbot`
- **Description**: Sends a message to the chatbot and receives a response
- **Request Body**:
  ```json
  {
    "message": "string",
    "history": [
      {
        "role": "string",
        "content": "string"
      }
    ]
  }
  ```
- **Response**: 
  ```json
  {
    "response": "string",
    "documents": [
      {
        "id": "string",
        "title": "string",
        "content": "string"
      }
    ]
  }
  ```

## GraphQL API

The TrustX application also uses a GraphQL API for SOC2 framework data.

### Endpoint

- Production: `https://api.trustx.cloud/graphql`
- Development: `https://api-dev.trustx.cloud/graphql`
- Staging: `https://api-stg.trustx.cloud/graphql`

### Authentication

GraphQL requests can use either JWT authentication or API key authentication:

- JWT Authentication:
  ```
  Authorization: Bearer {token}
  Content-Type: application/json
  X-Tenant-Name: {tenant_name}
  ```

- API Key Authentication (development only):
  ```
  x-api-key: {api_key}
  Content-Type: application/json
  X-Tenant-Name: {tenant_name}
  ```

### Queries

#### Get SOC2 Categories

```graphql
query GetSOC2Categories {
  getSOC2Categories {
    code
    name
    description
    weight
    implemented
    inProgress
    notImplemented
    testPassRate
    exceptions
  }
}
```

#### Get SOC2 Controls

```graphql
query GetSOC2Controls($categoryCode: String) {
  getSOC2Controls(categoryCode: $categoryCode) {
    id
    name
    description
    status
    categoryCode
    implementation {
      id
      description
      status
    }
  }
}
```

## Error Handling

All APIs return standard HTTP status codes:

- 200: Success
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 500: Internal Server Error

Error responses include a JSON object with error details:

```json
{
  "error": "string",
  "message": "string",
  "status": "number"
}
```

## CORS Configuration

The API servers are configured to accept requests from the following origins:
- Production: `https://app.trustx.cloud`
- Development: `https://app-dev.trustx.cloud`
- Staging: `https://app-stg.trustx.cloud`
- Local development: `http://localhost:3000`

## Rate Limiting

API requests may be subject to rate limiting. When rate limits are exceeded, the API will return a 429 Too Many Requests status code.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/trustx/docs/api-documentation.md) · Samay + Trustx experience/TrustxRepos/trustx/docs/api-documentation.md

Project code and dependencies remain outside the vault. No source commands were executed.
