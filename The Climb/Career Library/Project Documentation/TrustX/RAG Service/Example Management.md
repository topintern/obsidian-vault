---
kind: "project-document"
title: "Example Management"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/example_management.md"]
tags: ["career/library","career/project-docs"]
---

# Example Management

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Example Management

The Example Management functionality allows you to create, retrieve, update, and delete training examples for finetuning OpenAI models.

## Adding Examples

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

## Retrieving Examples

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

## Toggling Example Status

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

## Adding Tags to Examples

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

## Clearing Examples

**Endpoint:** `POST /clear_examples`

**Response:**
```json
{
  "message": "All training examples cleared."
}
```

## System Message Management

**Get System Message Endpoint:** `GET /get_system_message`

**Response:**
```json
{
  "system_message": "You are a helpful assistant that writes Cypher queries."
}
```

**Set System Message Endpoint:** `POST /set_system_message`

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

## Best Practices

1. **Consistent Format**: Ensure all examples follow the same format and style
2. **Diverse Examples**: Include a variety of query patterns to improve model generalization
3. **Meaningful Tags**: Use descriptive tags to organize examples by type or purpose
4. **Active Management**: Regularly review and update examples to improve quality
5. **System Message**: Keep the system message consistent with your use case


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/example_management.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/example_management.md

Project code and dependencies remain outside the vault. No source commands were executed.
