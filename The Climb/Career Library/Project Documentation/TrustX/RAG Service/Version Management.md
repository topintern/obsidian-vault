---
kind: "project-document"
title: "Version Management"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/version_management.md"]
tags: ["career/library","career/project-docs"]
---

# Version Management

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Version Management

The Version Management functionality allows you to save and restore different versions of your training data.

## Saving a Version

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

## Listing Versions

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

## Loading a Version

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

## Version Storage

Versions are stored in the `data/training_data/versions` directory. Each version is a JSON file containing:

1. **Metadata**: Information about the version (ID, creation time, example count, system message)
2. **Examples**: The complete set of examples at the time the version was created

## Automatic Versioning

The system automatically creates versions in certain situations:

1. **Before Clearing Examples**: A backup version is created before clearing all examples
2. **Before Finetuning**: A version is created before starting a finetuning job (if using stored examples)

## Use Cases

### Experiment Tracking

Save versions before making significant changes to your training data to track experiments.

### Backup and Recovery

Use versions as backups to recover from accidental data loss or corruption.

### A/B Testing

Create different versions of your training data to compare model performance.

### Iterative Development

Save versions at different stages of development to track progress.

## Best Practices

1. **Descriptive Names**: Use descriptive names for your versions
2. **Regular Backups**: Save versions regularly to prevent data loss
3. **Version Notes**: Include information about the purpose or content of each version
4. **Clean Up**: Remove unnecessary versions to save storage space
5. **Testing**: Test loaded versions to ensure data integrity

## Troubleshooting

### Common Issues

1. **Version Not Found**
   - Check that the version ID is correct
   - Verify that the version file exists in the versions directory
   - Ensure you have permission to access the file

2. **Loading Fails**
   - Check that the version file is not corrupted
   - Verify that the version file has the correct format
   - Ensure the system has sufficient memory to load the version

3. **Saving Fails**
   - Check that you have permission to write to the versions directory
   - Verify that there is sufficient disk space
   - Ensure the version name does not contain invalid characters


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/version_management.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/version_management.md

Project code and dependencies remain outside the vault. No source commands were executed.
