---
kind: "project-document"
title: "Query Processing"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/query_processing.md"]
tags: ["career/library","career/project-docs"]
---

# Query Processing

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Query Processing

The Query Processing functionality allows you to convert natural language queries to Cypher queries using OpenAI models.

## Processing Queries

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

## How It Works

1. **Input Processing**: The natural language query is analyzed to extract potential entity names
2. **Schema Retrieval**: The Neo4j database schema is retrieved to understand available nodes and relationships
3. **User Candidate Search**: If a name is detected, potential matching users are found in the database
4. **Prompt Construction**: A prompt is constructed with the query, schema, and user candidates
5. **LLM Invocation**: The prompt is sent to the OpenAI model
6. **Response Cleaning**: The response is cleaned and formatted as a valid Cypher query
7. **Return**: The Cypher query is returned to the client

## Example Queries

### User Profile Queries

**Natural Language**: "Show me John's profile"

**Generated Cypher**:
```cypher
MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u
```

### Relationship Queries

**Natural Language**: "Show me John's connections"

**Generated Cypher**:
```cypher
MATCH (u:User)-[r]-(n) WHERE toLower(u.name) CONTAINS 'john' RETURN u, r, n
```

### Property Queries

**Natural Language**: "What is John's email address?"

**Generated Cypher**:
```cypher
MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u.email
```

## Best Practices

1. **Clear Queries**: Use clear and specific natural language queries
2. **Entity Names**: Include entity names in your queries for better results
3. **Finetuning**: Finetune the model with examples specific to your database schema
4. **Schema Updates**: Update the model when your database schema changes
5. **Testing**: Test the model with a variety of queries to ensure accuracy

## Troubleshooting

### Common Issues

1. **Incorrect Queries**
   - Check that your database schema is correctly retrieved
   - Ensure entity names are clearly specified in the query
   - Consider finetuning the model with more examples

2. **Missing Entities**
   - Verify that the entities exist in your database
   - Check the spelling of entity names in your query
   - Ensure the database connection is working properly

3. **Performance Issues**
   - Large schemas may slow down query processing
   - Complex queries may take longer to generate
   - Consider optimizing your database schema for better performance


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/query_processing.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/query_processing.md

Project code and dependencies remain outside the vault. No source commands were executed.
