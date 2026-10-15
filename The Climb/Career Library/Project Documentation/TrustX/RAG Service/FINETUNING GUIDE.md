---
kind: "project-document"
title: "FINETUNING GUIDE"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/FINETUNING_GUIDE.md"]
tags: ["career/library","career/project-docs"]
---

# FINETUNING GUIDE

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Advanced Finetuning Guide

This guide explains how to use the enhanced finetuning functionality in the Flask API, including example versioning, tagging, and selective finetuning.

## Table of Contents

1. [Overview](#overview)
2. [Web Interface](#web-interface)
3. [Managing Examples](#managing-examples)
4. [Versioning Examples](#versioning-examples)
5. [Tagging Examples](#tagging-examples)
6. [Selective Finetuning](#selective-finetuning)
7. [API Reference](#api-reference)
8. [Implementation Details](#implementation-details)

## Overview

The enhanced finetuning system provides the following features:

- **Example Management**: Add, view, and manage training examples with metadata
- **Versioning**: Save and restore different versions of your training data
- **Tagging**: Organize examples with tags for better management
- **Selective Finetuning**: Choose which examples to include in finetuning based on tags or active status
- **Status Tracking**: Monitor the status of finetuning jobs

## Web Interface

Access the advanced finetuning interface at:

```
http://localhost:5001/advanced_finetuning
```

The interface is organized into four tabs:

1. **Examples**: Add, view, and manage training examples
2. **Versions**: Save and load different versions of your training data
3. **Finetune**: Trigger finetuning with selected examples
4. **Jobs**: View and manage finetuning jobs

## Managing Examples

### Adding Examples

1. Go to the **Examples** tab
2. Fill in the prompt (user query) and completion (Cypher query)
3. Optionally add tags (comma-separated)
4. Click "Add Example"

Each example is stored with:
- Unique ID
- Prompt and completion
- Tags
- Creation timestamp
- Active status (whether it will be included in finetuning)

### Viewing Examples

1. Go to the **Examples** tab
2. Click "Load Examples"
3. Optionally filter by tags or active status

### Activating/Deactivating Examples

1. Load examples
2. Click "Activate" or "Deactivate" on any example
3. Inactive examples will not be included in finetuning unless specifically selected

### Setting System Message

The system message is used as the system prompt for all examples during finetuning:

1. Go to the **Examples** tab
2. Enter your system message
3. Click "Update System Message"

## Versioning Examples

Versioning allows you to save and restore different sets of examples.

### Saving a Version

1. Go to the **Versions** tab
2. Enter a name for the version
3. Click "Save Version"

Alternatively, from the Examples tab:
1. Click "Save as Version"
2. Enter a name when prompted

### Loading a Version

1. Go to the **Versions** tab
2. Click "Refresh Versions" to see all saved versions
3. Find the version you want to load
4. Click "Load This Version"

This will replace your current examples with the ones from the selected version.

### Automatic Versioning

The system automatically creates versions in certain situations:
- Before clearing all examples
- Before starting a finetuning job (if using stored examples)

## Tagging Examples

Tags help organize examples and allow selective finetuning.

### Adding Tags When Creating Examples

1. When adding a new example, enter comma-separated tags in the "Tags" field

### Adding Tags to Existing Examples

1. Load examples
2. Click "Add Tags" on any example
3. Enter comma-separated tags when prompted

### Filtering Examples by Tags

1. Enter tags in the "Filter by Tags" field
2. Optionally check "Require all tags" to show only examples with all specified tags
3. Click "Load Examples"

## Selective Finetuning

You can choose which examples to include in finetuning based on tags or active status.

### Finetuning with All Active Examples

1. Go to the **Finetune** tab
2. Leave the "Filter by Tags" field empty
3. Click "Start Finetuning"

### Finetuning with Tagged Examples

1. Go to the **Finetune** tab
2. Enter tags in the "Filter by Tags" field
3. Optionally check "Require all tags"
4. Click "Start Finetuning"

### Checking Finetuning Status

1. Go to the **Finetune** tab
2. Enter the job ID
3. Click "Check Status"

Or:
1. Go to the **Jobs** tab
2. Click "List Jobs"
3. Click "Check Status" on any job

## API Reference

### Example Management

#### Add Example
```
POST /add_example
{
  "prompt": "Show me John's profile",
  "completion": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u",
  "tags": ["profile", "user", "search"]
}
```

#### Get Examples
```
GET /get_examples
GET /get_examples?tags=profile,user&require_all_tags=true
GET /get_examples?active_only=true
```

#### Toggle Example Status
```
POST /toggle_example
{
  "example_id": "ex_1_1620000000",
  "active": true
}
```

#### Add Tags to Example
```
POST /add_tags
{
  "example_id": "ex_1_1620000000",
  "tags": ["profile", "user"]
}
```

#### Clear Examples
```
POST /clear_examples
```

### System Message

#### Get System Message
```
GET /get_system_message
```

#### Set System Message
```
POST /set_system_message
{
  "system_message": "You are a helpful assistant that writes Cypher queries."
}
```

### Versioning

#### Save Version
```
POST /save_version
{
  "version_name": "my_version_1"
}
```

#### List Versions
```
GET /list_versions
```

#### Load Version
```
POST /load_version
{
  "version_id": "my_version_1"
}
```

### Finetuning

#### Trigger Finetuning
```
POST /trigger_finetune
{
  "use_stored_examples": true,
  "base_model": "gpt-3.5-turbo",
  "tags": ["profile", "user"],
  "require_all_tags": false,
  "version_name": "pre_finetune_v1"
}
```

#### Check Finetuning Status
```
GET /finetune_status?job_id=ftjob-abc123
```

#### List Finetuning Jobs
```
GET /list_finetune_jobs
```

## Implementation Details

### Directory Structure

The system creates the following directory structure:

```
training_data/
├── current_examples.json     # Current active examples
├── system_message.txt        # System message
└── versions/                 # Saved versions
    ├── version_20230101_120000.json
    ├── my_version_1.json
    └── ...
```

### Example Format

Examples are stored in the following format:

```json
{
  "id": "ex_1_1620000000",
  "prompt": "Show me John's profile",
  "completion": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u",
  "tags": ["profile", "user", "search"],
  "created_at": "2023-01-01T12:00:00.000Z",
  "active": true
}
```

### Version Format

Versions are stored with metadata:

```json
{
  "metadata": {
    "version_id": "my_version_1",
    "created_at": "2023-01-01T12:00:00.000Z",
    "example_count": 10,
    "system_message": "You are a helpful assistant that writes Cypher queries."
  },
  "examples": [
    {
      "id": "ex_1_1620000000",
      "prompt": "Show me John's profile",
      "completion": "MATCH (u:User) WHERE toLower(u.name) CONTAINS 'john' RETURN u",
      "tags": ["profile", "user", "search"],
      "created_at": "2023-01-01T12:00:00.000Z",
      "active": true
    },
    ...
  ]
}
```

### Conversion to OpenAI Format

When triggering finetuning, examples are converted to the OpenAI chat format:

```json
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
```


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/FINETUNING_GUIDE.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/FINETUNING_GUIDE.md

Project code and dependencies remain outside the vault. No source commands were executed.
