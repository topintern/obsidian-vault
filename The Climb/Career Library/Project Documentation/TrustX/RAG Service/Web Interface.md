---
kind: "project-document"
title: "Web Interface"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/web_interface.md"]
tags: ["career/library","career/project-docs"]
---

# Web Interface

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Web Interface

The Web Interface provides a user-friendly way to interact with the API.

## Accessing the Interface

**URL:** `http://localhost:5000/finetuning`

This interface provides a comprehensive dashboard for managing training examples, versions, and finetuning jobs.

## Interface Sections

### Examples Tab

Examples Tab *(referenced file is absent from this source snapshot)*

The Examples tab allows you to:

1. **Add Examples**
   - Enter prompt and completion
   - Add tags for organization
   - Submit new examples

2. **View Examples**
   - See all stored examples
   - Filter by tags
   - Toggle active/inactive status

3. **Manage System Message**
   - View current system message
   - Update system message

### Versions Tab

Versions Tab *(referenced file is absent from this source snapshot)*

The Versions tab allows you to:

1. **Save Versions**
   - Create named versions of your training data
   - Add descriptions for reference

2. **View Versions**
   - See all saved versions
   - View version details (creation time, example count)

3. **Load Versions**
   - Restore previous versions
   - Replace current examples with a saved version

### Finetune Tab

Finetune Tab *(referenced file is absent from this source snapshot)*

The Finetune tab allows you to:

1. **Start Finetuning**
   - Select base model
   - Filter examples by tags
   - Trigger finetuning job

2. **Check Status**
   - Enter job ID
   - View job status and details
   - See finetuned model ID when complete

### Jobs Tab

Jobs Tab *(referenced file is absent from this source snapshot)*

The Jobs tab allows you to:

1. **List Jobs**
   - See all finetuning jobs
   - View job status and creation time

2. **Check Job Details**
   - View detailed job information
   - Access finetuned model ID

## Using the Interface

### Adding and Managing Examples

1. Go to the Examples tab
2. Fill in the prompt and completion fields
3. Add relevant tags
4. Click "Add Example"
5. Use the filter options to find specific examples
6. Toggle example status as needed

### Creating and Managing Versions

1. Go to the Versions tab
2. Enter a name for your version
3. Click "Save Version"
4. View all saved versions
5. Click "Load This Version" to restore a version

### Starting and Monitoring Finetuning

1. Go to the Finetune tab
2. Select the base model
3. Optionally filter examples by tags
4. Click "Start Finetuning"
5. Note the job ID for status checking
6. Use the "Check Status" section to monitor progress

### Viewing Finetuning Jobs

1. Go to the Jobs tab
2. Click "List Jobs" to see all jobs
3. Click "Check Status" on any job to view details
4. Note the finetuned model ID for successful jobs

## Best Practices

1. **Regular Updates**: Regularly add new examples to improve model performance
2. **Version Control**: Save versions before making significant changes
3. **Selective Finetuning**: Use tags to finetune on specific subsets of examples
4. **Status Monitoring**: Regularly check the status of finetuning jobs
5. **Documentation**: Keep notes on different versions and finetuning jobs

## Troubleshooting

### Common Issues

1. **Interface Not Loading**
   - Check that the Flask server is running
   - Verify that you're accessing the correct URL
   - Clear browser cache and reload

2. **Actions Not Working**
   - Check browser console for JavaScript errors
   - Verify that the API endpoints are accessible
   - Ensure you have the necessary permissions

3. **Display Issues**
   - Try a different browser
   - Adjust browser zoom level
   - Disable browser extensions that might interfere


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/web_interface.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/web_interface.md

Project code and dependencies remain outside the vault. No source commands were executed.
