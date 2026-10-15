---
kind: "project-document"
title: "Finetuning"
collection: "TrustX"
topic: "RAG Service"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/finetuning.md"]
tags: ["career/library","career/project-docs"]
---

# Finetuning

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Finetuning

The Finetuning functionality allows you to create and manage finetuning jobs for OpenAI models.

## Triggering Finetuning

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

## Checking Finetuning Status

**Endpoint:** `GET /finetune_status?job_id=ftjob-abc123`

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

## Listing Finetuning Jobs

**Endpoint:** `GET /list_finetune_jobs?limit=10`

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

## Using the Finetuned Model

Once your model is finetuned, you can use it by updating your OpenAI API calls to use the finetuned model ID. The model ID will be available in the finetuning status response under the `fine_tuned_model` field once the finetuning is complete.

### Example OpenAI API Call

```python
import openai

response = openai.chat.completions.create(
    model="ft:gpt-3.5-turbo-0125:personal::abc123",  # Your finetuned model ID
    messages=[
        {"role": "system", "content": "You are a helpful assistant that writes Cypher queries."},
        {"role": "user", "content": "Show me John's profile"}
    ]
)

print(response.choices[0].message.content)
```

## Finetuning Process

1. **Preparation**: Collect and organize training examples
2. **Selection**: Choose which examples to include in the finetuning job
3. **Submission**: Trigger the finetuning job
4. **Monitoring**: Check the status of the job
5. **Deployment**: Use the finetuned model in your application

## Best Practices

1. **Quality over Quantity**: Focus on high-quality examples rather than just quantity
2. **Balanced Dataset**: Ensure your dataset covers a variety of query patterns
3. **Consistent Format**: Maintain consistency in the format of your examples
4. **Versioning**: Save versions of your examples before finetuning
5. **Iterative Approach**: Start with a small set of examples and gradually add more
6. **Testing**: Evaluate the finetuned model with test queries before deployment

## Troubleshooting

### Common Issues

1. **Job Fails to Start**
   - Check that your OpenAI API key is valid
   - Ensure you have sufficient quota for finetuning
   - Verify that your examples follow OpenAI's guidelines

2. **Poor Model Performance**
   - Review the quality and diversity of your examples
   - Check for inconsistencies in your training data
   - Consider adding more examples for underrepresented query patterns

3. **Job Takes Too Long**
   - Large datasets may take longer to process
   - Complex examples may increase training time
   - Check the OpenAI status page for any service issues


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/AppRunner/docs/finetuning.md) · Samay + Trustx experience/TrustxRepos/AWS/AppRunner/docs/finetuning.md

Project code and dependencies remain outside the vault. No source commands were executed.
