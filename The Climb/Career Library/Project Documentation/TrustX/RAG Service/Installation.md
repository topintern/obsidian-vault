---
kind: "project-document"
title: "Installation"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/installation.md"]
tags: ["career/library","career/project-docs"]
---

# Installation

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Installation and Setup

This guide provides instructions for installing and setting up the Flask API for Neo4j and OpenAI integration.

## Prerequisites

- Python 3.8 or higher
- Neo4j database (local or cloud)
- OpenAI API key
- Git (optional, for cloning the repository)

## Installation Steps

### 1. Clone or Download the Repository

```bash
git clone https://github.com/yourusername/flask-api.git
cd flask-api
```

Or download and extract the ZIP file from the repository.

### 2. Create a Virtual Environment

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows
venv\\Scripts\\activate
# On macOS/Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the root directory with the following variables:

```
OPENAI_API_KEY=your_openai_api_key
NEO4J_URI=your_neo4j_uri
NEO4J_USER=your_neo4j_username
NEO4J_PASSWORD=your_neo4j_password
DEBUG=True
PORT=5000
```

Alternatively, you can set these variables directly in the `config.py` file.

### 5. Initialize the Data Directory

```bash
# Create the data directory structure
mkdir -p data/training_data/versions
```

### 6. Run the Application

```bash
python app.py
```

The application will start on `http://localhost:5000` by default.

## Docker Installation

### 1. Build the Docker Image

```bash
docker build -t flask-api .
```

### 2. Run the Docker Container

```bash
docker run -p 5000:5000 \
  -e OPENAI_API_KEY=your_openai_api_key \
  -e NEO4J_URI=your_neo4j_uri \
  -e NEO4J_USER=your_neo4j_username \
  -e NEO4J_PASSWORD=your_neo4j_password \
  -v $(pwd)/data:/app/data \
  flask-api
```

## Configuration Options

### config.py

The `config.py` file contains the following configuration options:

```python
# OpenAI API key
OPENAI_API_KEY = os.environ.get("OPENAI_API_KEY", "your_default_api_key")

# Neo4j database connection settings
NEO4J_URI = os.environ.get("NEO4J_URI", "neo4j://localhost:7687")
NEO4J_USER = os.environ.get("NEO4J_USER", "neo4j")
NEO4J_PASSWORD = os.environ.get("NEO4J_PASSWORD", "password")

# Application settings
DEBUG = os.environ.get("DEBUG", "True").lower() == "true"
PORT = int(os.environ.get("PORT", 5000))

# Data paths
DATA_DIR = os.environ.get("DATA_DIR", "data")
TRAINING_DATA_DIR = os.path.join(DATA_DIR, "training_data")
```

You can modify these settings directly in the file or by setting environment variables.

## Verifying the Installation

### 1. Check the Server Status

Access the health check endpoint:

```bash
curl http://localhost:5000/health
```

You should receive a response like:

```json
{
  "status": "healthy"
}
```

### 2. Access the Web Interface

Open a web browser and navigate to:

```
http://localhost:5000/finetuning
```

You should see the finetuning management interface.

## Troubleshooting

### Common Installation Issues

1. **Missing Dependencies**
   - Error: `ModuleNotFoundError: No module named 'flask'`
   - Solution: Ensure you've activated the virtual environment and installed all dependencies with `pip install -r requirements.txt`

2. **Database Connection Issues**
   - Error: `Failed to connect to Neo4j database`
   - Solution: Verify your Neo4j URI, username, and password. Ensure the Neo4j database is running and accessible.

3. **OpenAI API Key Issues**
   - Error: `Invalid API key provided`
   - Solution: Check that your OpenAI API key is valid and correctly set in the configuration.

4. **Port Already in Use**
   - Error: `Address already in use`
   - Solution: Change the port in `config.py` or stop the process using the current port.

### Getting Help

If you encounter issues not covered in this guide:

1. Check the server logs for detailed error messages
2. Review the source code in the relevant module
3. Consult the documentation for the specific component (Flask, Neo4j, OpenAI)
4. Search for similar issues in the project's issue tracker


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/installation.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/installation.md

Project code and dependencies remain outside the vault. No source commands were executed.
