---
kind: "project-document"
title: "Troubleshooting"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/troubleshooting.md"]
tags: ["career/library","career/project-docs"]
---

# Troubleshooting

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Troubleshooting Guide

This guide provides solutions for common issues you might encounter when using the Flask API.

## API Issues

### Connection Issues

**Problem**: Unable to connect to the API server.

**Solutions**:
1. Verify the server is running with `python app.py`
2. Check if the port is already in use by another application
3. Ensure your firewall is not blocking the connection
4. Try accessing the health endpoint: `GET /health`

### Authentication Issues

**Problem**: API requests are failing with authentication errors.

**Solutions**:
1. Check that your OpenAI API key is valid and not expired
2. Verify the API key is correctly set in `config.py`
3. Ensure the Neo4j credentials are correct
4. Check for any rate limiting or quota issues with OpenAI

## Example Management Issues

### Examples Not Saving

**Problem**: Unable to add new examples.

**Solutions**:
1. Check that the data directory exists and is writable
2. Verify the request format is correct
3. Check server logs for detailed error messages
4. Ensure the example has both prompt and completion fields

### Examples Not Loading

**Problem**: Unable to retrieve examples.

**Solutions**:
1. Verify the examples file exists in the data directory
2. Check that the file has the correct format
3. Ensure the file permissions allow reading
4. Try clearing browser cache if using the web interface

## Finetuning Issues

### Job Creation Fails

**Problem**: Unable to create a finetuning job.

**Solutions**:
1. Verify you have sufficient examples (at least 10 recommended)
2. Check that your OpenAI API key has finetuning permissions
3. Ensure you have sufficient quota for finetuning
4. Verify the examples follow OpenAI's guidelines

### Job Status Not Updating

**Problem**: Finetuning job status is not updating.

**Solutions**:
1. Check that the job ID is correct
2. Verify your OpenAI API key is still valid
3. Allow sufficient time for the job to process (can take hours)
4. Check the OpenAI dashboard for job status

### Poor Model Performance

**Problem**: Finetuned model is not performing well.

**Solutions**:
1. Review the quality and diversity of your examples
2. Ensure your examples are consistent in format
3. Add more examples for underrepresented query patterns
4. Check that your system message is appropriate

## Version Management Issues

### Version Not Saving

**Problem**: Unable to save a version.

**Solutions**:
1. Check that the versions directory exists and is writable
2. Verify the version name does not contain invalid characters
3. Ensure there is sufficient disk space
4. Check server logs for detailed error messages

### Version Not Loading

**Problem**: Unable to load a version.

**Solutions**:
1. Verify the version ID is correct
2. Check that the version file exists in the versions directory
3. Ensure the version file has the correct format
4. Check file permissions

## Web Interface Issues

### Interface Not Loading

**Problem**: Web interface is not loading.

**Solutions**:
1. Verify the Flask server is running
2. Check that you're accessing the correct URL
3. Clear browser cache and reload
4. Try a different browser

### Actions Not Working

**Problem**: Buttons or actions in the web interface are not working.

**Solutions**:
1. Check browser console for JavaScript errors
2. Verify that the API endpoints are accessible
3. Ensure you have the necessary permissions
4. Try disabling browser extensions

## Neo4j Issues

### Connection Failures

**Problem**: Unable to connect to Neo4j database.

**Solutions**:
1. Verify the Neo4j URI, username, and password
2. Ensure the Neo4j database is running
3. Check network connectivity to the database
4. Verify firewall settings

### Query Execution Failures

**Problem**: Cypher queries are failing to execute.

**Solutions**:
1. Check the syntax of the generated Cypher query
2. Verify the database schema matches what the model expects
3. Ensure the database has the necessary indexes
4. Check for any constraints that might be violated

## OpenAI API Issues

### Rate Limiting

**Problem**: Encountering rate limits with the OpenAI API.

**Solutions**:
1. Implement request throttling
2. Upgrade your OpenAI plan for higher rate limits
3. Cache responses where appropriate
4. Batch requests when possible

### API Changes

**Problem**: API responses have changed or endpoints are not working.

**Solutions**:
1. Check the OpenAI API documentation for changes
2. Update the code to match the latest API version
3. Join the OpenAI developer community for updates
4. Check for any deprecation notices

## Logging and Debugging

### Enabling Debug Mode

To enable debug mode for more detailed logging:

1. Set `DEBUG=True` in `config.py` or as an environment variable
2. Restart the Flask server
3. Check the console output for detailed logs

### Checking Logs

To check the server logs:

1. Look at the console output where the server is running
2. Check any log files in the project directory
3. Use a tool like `tail -f` to follow logs in real-time

### Common Log Messages

- `[INFO]` messages provide information about normal operation
- `[WARNING]` messages indicate potential issues that don't affect functionality
- `[ERROR]` messages indicate problems that need attention
- `[SUCCESS]` messages confirm successful operations

## Getting Additional Help

If you're still experiencing issues:

1. Check the documentation for the specific component (Flask, Neo4j, OpenAI)
2. Search for similar issues in the project's issue tracker
3. Consult the OpenAI community forums for finetuning-specific issues
4. Reach out to the project maintainers for support


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/troubleshooting.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/troubleshooting.md

Project code and dependencies remain outside the vault. No source commands were executed.
