---
kind: "project-document"
title: "API Reference"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/api_reference.md"]
tags: ["career/library","career/project-docs"]
---

# API Reference

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# API Reference

This document provides a comprehensive reference for all API endpoints.

## Example Management

### Add Example

**Endpoint:** `POST /add_example`

**Request Body:**
```json
{
  "prompt": "Show me John's profile",
  "completion": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u",
  "tags": ["profile", "user", "search"]
}
```

**Response:**
```json
{
  "message": "Example added",
  "example": {
    "id": "ex_1_1620000000",
    "prompt": "Show me John's profile",
    "completion": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u",
    "tags": ["profile", "user", "search"],
    "created_at": "2023-01-01T12:00:00.000Z",
    "active": true
  },
  "total_examples": 1
}
```

### Get Examples

**Endpoint:** `GET /get_examples`

**Query Parameters:**
- `tags` (optional): Comma-separated list of tags to filter by
- `require_all_tags` (optional): If "true", examples must have all specified tags
- `active_only` (optional): If "true", only active examples are returned

**Response:**
```json
{
  "examples": [
    {
      "id": "ex_1_1620000000",
      "prompt": "Show me John's profile",
      "completion": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u",
      "tags": ["profile", "user", "search"],
      "created_at": "2023-01-01T12:00:00.000Z",
      "active": true
    }
  ],
  "count": 1
}
```

### Toggle Example Status

**Endpoint:** `POST /toggle_example`

**Request Body:**
```json
{
  "example_id": "ex_1_1620000000",
  "active": false
}
```

**Response:**
```json
{
  "message": "Example ex_1_1620000000 deactivated"
}
```

### Add Tags to Example

**Endpoint:** `POST /add_tags`

**Request Body:**
```json
{
  "example_id": "ex_1_1620000000",
  "tags": ["profile", "user"]
}
```

**Response:**
```json
{
  "message": "Tags added to example ex_1_1620000000"
}
```

### Clear Examples

**Endpoint:** `POST /clear_examples`

**Response:**
```json
{
  "message": "All training examples cleared."
}
```

### Get System Message

**Endpoint:** `GET /get_system_message`

**Response:**
```json
{
  "system_message": "You are a helpful assistant that writes Cypher queries."
}
```

### Set System Message

**Endpoint:** `POST /set_system_message`

**Request Body:**
```json
{
  "system_message": "You are a helpful assistant that writes Cypher queries for a Neo4j graph database."
}
```

**Response:**
```json
{
  "message": "System message updated",
  "system_message": "You are a helpful assistant that writes Cypher queries for a Neo4j graph database."
}
```

## Finetuning

### Trigger Finetuning

**Endpoint:** `POST /trigger_finetune`

**Request Body (Using Stored Examples):**
```json
{
  "use_stored_examples": true,
  "base_model": "gpt-3.5-turbo",
  "tags": ["profile", "user"],
  "require_all_tags": false,
  "version_name": "pre_finetune_v1"
}
```

**Request Body (Using Custom Training Data):**
```json
{
  "training_data": [
    {
      "messages": [
        {
          "role": "system",
          "content": "You are a helpful assistant that writes Cypher queries."
        },
        {
          "role": "user",
          "content": "Show me John's profile"
        },
        {
          "role": "assistant",
          "content": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u"
        }
      ]
    }
  ],
  "base_model": "gpt-3.5-turbo"
}
```

**Response:**
```json
{
  "job_id": "ftjob-abc123",
  "status": "created",
  "model": "gpt-3.5-turbo",
  "created_at": 1672531200
}
```

### Check Finetuning Status

**Endpoint:** `GET /finetune_status`

**Query Parameters:**
- `job_id` (required): The ID of the finetuning job

**Response:**
```json
{
  "id": "ftjob-abc123",
  "status": "succeeded",
  "model": "gpt-3.5-turbo",
  "created_at": 1672531200,
  "fine_tuned_model": "ft:gpt-3.5-turbo-0125:personal::abc123",
  "hyperparameters": {
    "n_epochs": "3",
    "batch_size": "1",
    "learning_rate_multiplier": "2"
  }
}
```

### List Finetuning Jobs

**Endpoint:** `GET /list_finetune_jobs`

**Query Parameters:**
- `limit` (optional): Maximum number of jobs to return (default: 10)

**Response:**
```json
{
  "jobs": [
    {
      "id": "ftjob-abc123",
      "status": "succeeded",
      "model": "gpt-3.5-turbo",
      "created_at": 1672531200,
      "fine_tuned_model": "ft:gpt-3.5-turbo-0125:personal::abc123"
    }
  ]
}
```

## Version Management

### Save Version

**Endpoint:** `POST /save_version`

**Request Body:**
```json
{
  "version_name": "my_version_1"
}
```

**Response:**
```json
{
  "message": "Version saved",
  "version_id": "my_version_1"
}
```

### List Versions

**Endpoint:** `GET /list_versions`

**Response:**
```json
{
  "versions": [
    {
      "version_id": "my_version_1",
      "created_at": "2023-01-01T12:00:00.000Z",
      "example_count": 10,
      "system_message": "You are a helpful assistant that writes Cypher queries."
    }
  ],
  "count": 1
}
```

### Load Version

**Endpoint:** `POST /load_version`

**Request Body:**
```json
{
  "version_id": "my_version_1"
}
```

**Response:**
```json
{
  "message": "Version my_version_1 loaded successfully"
}
```

## Query Processing

### Process Query

**Endpoint:** `POST /query`

**Request Body:**
```json
{
  "query": "Show me John's profile"
}
```

**Response:**
```json
{
  "query": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u"
}
```

## Web Interface

### Finetuning Management Interface

**Endpoint:** `GET /finetuning`

**Response:** HTML page for managing finetuning

### Health Check

**Endpoint:** `GET /health`

**Response:**
```json
{
  "status": "healthy"
}
```

## Error Responses

All endpoints may return error responses in the following format:

```json
{
  "error": "Error message describing the issue"
}
```

Common HTTP status codes:

- `200 OK`: Request successful
- `400 Bad Request`: Invalid request parameters
- `404 Not Found`: Resource not found
- `500 Internal Server Error`: Server-side error


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/api_reference.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/api_reference.md

Project code and dependencies remain outside the vault. No source commands were executed.
