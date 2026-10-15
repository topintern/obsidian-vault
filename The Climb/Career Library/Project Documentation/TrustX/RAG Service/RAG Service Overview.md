---
kind: "project-document"
title: "RAG Service Overview"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/README.md"]
tags: ["career/library","career/project-docs"]
---

# RAG Service Overview

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Flask API for Neo4j and OpenAI Integration

This project provides a Flask API that integrates Neo4j graph database with OpenAI's language models to:

1. Process natural language queries and convert them to Cypher queries
2. Manage training examples for finetuning
3. Finetune OpenAI models with custom examples

## Directory Structure

```
FlaskAPI/
├── app.py                  # Main application entry point
├── config.py               # Configuration settings
├── requirements.txt        # Dependencies
├── README.md               # Project documentation
├── Dockerfile              # Docker configuration
├── docs/                   # Documentation
│   └── FINETUNING_GUIDE.md # Finetuning documentation
├── src/                    # Source code
│   ├── api/                # API endpoints
│   │   ├── example_routes.py
│   │   ├── finetuning_routes.py
│   │   └── query_routes.py
│   ├── core/               # Core functionality
│   │   ├── db.py           # Database utilities
│   │   ├── example_store.py # Example management
│   │   ├── finetuning.py   # Finetuning utilities
│   │   └── prompt_engineering.py # Prompt engineering
│   └── utils/              # Utility functions
│       └── helpers.py
├── static/                 # Static assets
├── templates/              # HTML templates
│   └── finetuning.html     # Finetuning UI
└── data/                   # Data storage
    └── training_data/      # Training data
```

## Setup

1. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

2. Configure environment variables in `config.py`:
   - `OPENAI_API_KEY`: Your OpenAI API key
   - `NEO4J_URI`: URI for your Neo4j database
   - `NEO4J_USER`: Neo4j username
   - `NEO4J_PASSWORD`: Neo4j password

3. Run the application:
   ```
   python app.py
   ```

## API Endpoints

### Query Processing

- `POST /query`: Process a natural language query and convert it to a Cypher query

### Example Management

- `POST /add_example`: Add a training example
- `GET /get_examples`: Get all stored examples
- `POST /toggle_example`: Toggle the active status of an example
- `POST /add_tags`: Add tags to an example
- `POST /clear_examples`: Clear all examples
- `GET /get_system_message`: Get the system message
- `POST /set_system_message`: Set the system message

### Finetuning

- `POST /trigger_finetune`: Start a finetuning job
- `GET /finetune_status`: Check the status of a finetuning job
- `GET /list_finetune_jobs`: List all finetuning jobs
- `POST /save_version`: Save the current examples as a version
- `GET /list_versions`: List all saved versions
- `POST /load_version`: Load a specific version

### Web Interface

- `GET /finetuning`: Access the finetuning management interface

## Documentation

Detailed documentation is available in the [docs](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs) directory:

- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/Installation|Installation and Setup]]
- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/Example Management|Example Management]]
- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/Finetuning|Finetuning]]
- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/Query Processing|Query Processing]]
- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/Version Management|Version Management]]
- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/Web Interface|Web Interface]]
- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/API Reference|API Reference]]
- [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/Troubleshooting|Troubleshooting]]

See the [[The Climb/Career Library/Project Documentation/TrustX/RAG Service/RAG Service Documentation Index|Documentation Index]] for a complete overview.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/README.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/README.md

Project code and dependencies remain outside the vault. No source commands were executed.
