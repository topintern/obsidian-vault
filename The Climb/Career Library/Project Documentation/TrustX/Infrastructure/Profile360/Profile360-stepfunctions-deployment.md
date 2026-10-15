---
kind: "project-document"
title: "Profile360-stepfunctions-deployment"
collection: "TrustX"
topic: "Infrastructure/Profile360"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-stepfunctions-deployment.md"]
tags: ["career/library","career/project-docs"]
---

# Profile360-stepfunctions-deployment

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Profile 360 Step Functions Deployment Guide

## Overview

This guide covers the deployment and management of the Profile 360 Step Functions-based data pipeline that orchestrates Lambda functions for automated data ingestion from multiple sources into Neo4j.

## Architecture Changes

### Before: Manual Lambda Execution
- Individual Lambda functions triggered manually or via API calls
- No orchestration or error handling
- Limited visibility into pipeline status

### After: Step Functions Orchestration
- Automated pipeline execution via EventBridge scheduler
- Parallel processing for improved performance
- Built-in error handling and retry logic
- Complete execution visibility and monitoring

## Deployment Steps

### 1. Prerequisites

Ensure you have the following installed and configured:
```bash
# Install AWS CDK CLI
npm install -g aws-cdk

# Install TypeScript
npm install -g typescript

# Verify AWS CLI configuration
aws sts get-caller-identity
```

### 2. Update Dependencies

Add Step Functions dependencies to your CDK project:
```bash
cd AWS
npm install @aws-cdk/aws-stepfunctions @aws-cdk/aws-stepfunctions-tasks @aws-cdk/aws-events @aws-cdk/aws-events-targets
```

### 3. Deploy the Updated Stack

```bash
# Deploy only the Profile360 stack
cdk deploy {environment}-profile360-stack

# Or deploy all stacks
cdk deploy --all
```

### 4. Verify Deployment

Check that all resources were created successfully:
```bash
# List Step Functions state machines
aws stepfunctions list-state-machines

# List EventBridge rules
aws events list-rules --name-prefix {environment}-profile360

# Check Lambda functions
aws lambda list-functions --query 'Functions[?contains(FunctionName, `profile360`) || contains(FunctionName, `entra`) || contains(FunctionName, `github`) || contains(FunctionName, `jira`)]'
```

## Step Functions Configuration

### State Machine Definition

The state machine includes the following components:

#### 1. Data Formatting Parallel Stage
```json
{
  "Type": "Parallel",
  "Branches": [
    {
      "StartAt": "EntraDataFormattingTask",
      "States": {
        "EntraDataFormattingTask": {
          "Type": "Task",
          "Resource": "arn:aws:lambda:region:account:function:env-entra-data-formatting",
          "End": true
        }
      }
    },
    {
      "StartAt": "JiraDataFormattingTask", 
      "States": {
        "JiraDataFormattingTask": {
          "Type": "Task",
          "Resource": "arn:aws:lambda:region:account:function:env-jira-data-formatting",
          "End": true
        }
      }
    }
  ]
}
```

#### 2. Neo4j Ingestion Parallel Stage
```json
{
  "Type": "Parallel",
  "Branches": [
    {
      "StartAt": "EntraToNeo4jTask",
      "States": {
        "EntraToNeo4jTask": {
          "Type": "Task",
          "Resource": "arn:aws:lambda:region:account:function:env-entra-to-neo4j",
          "End": true
        }
      }
    },
    {
      "StartAt": "GithubToNeo4jTask",
      "States": {
        "GithubToNeo4jTask": {
          "Type": "Task", 
          "Resource": "arn:aws:lambda:region:account:function:env-github-to-neo4j",
          "End": true
        }
      }
    },
    {
      "StartAt": "JiraToNeo4jTask",
      "States": {
        "JiraToNeo4jTask": {
          "Type": "Task",
          "Resource": "arn:aws:lambda:region:account:function:env-jira-to-neo4j", 
          "End": true
        }
      }
    }
  ]
}
```

### Error Handling Configuration

Each Lambda task includes retry and error handling:
```json
{
  "Type": "Task",
  "Resource": "arn:aws:lambda:...",
  "Retry": [
    {
      "ErrorEquals": ["Lambda.ServiceException", "Lambda.AWSLambdaException"],
      "IntervalSeconds": 2,
      "MaxAttempts": 3,
      "BackoffRate": 2.0
    }
  ],
  "Catch": [
    {
      "ErrorEquals": ["States.ALL"],
      "Next": "Profile360PipelineFailure"
    }
  ]
}
```

## EventBridge Scheduling

### Schedule Configuration

The pipeline runs daily at 2:00 AM UTC:
```typescript
schedule: events.Schedule.cron({
  minute: '0',
  hour: '2', 
  day: '*',
  month: '*',
  year: '*',
})
```

### Custom Schedule Options

To modify the schedule, update the CDK code:
```typescript
// Run every 6 hours
schedule: events.Schedule.rate(cdk.Duration.hours(6))

// Run weekly on Sundays at 3 AM
schedule: events.Schedule.cron({
  minute: '0',
  hour: '3',
  weekDay: 'SUN'
})

// Run monthly on the 1st at midnight
schedule: events.Schedule.cron({
  minute: '0', 
  hour: '0',
  day: '1'
})
```

## Manual Execution

### Via AWS Console
1. Navigate to Step Functions in AWS Console
2. Select the `{environment}-profile360-pipeline` state machine
3. Click "Start execution"
4. Provide input JSON (optional):
```json
{
  "source": "manual",
  "timestamp": "2024-01-15T10:30:00Z",
  "environment": "production"
}
```

### Via AWS CLI
```bash
# Start execution with default input
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:us-east-2:123456789012:stateMachine:prod-profile360-pipeline \
  --name "manual-execution-$(date +%s)"

# Start execution with custom input
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:us-east-2:123456789012:stateMachine:prod-profile360-pipeline \
  --name "manual-execution-$(date +%s)" \
  --input '{"source": "manual", "debug": true}'
```

### Via CDK/TypeScript
```typescript
import { SFNClient, StartExecutionCommand } from "@aws-sdk/client-sfn";

const client = new SFNClient({ region: "us-east-2" });
const command = new StartExecutionCommand({
  stateMachineArn: "arn:aws:states:us-east-2:123456789012:stateMachine:prod-profile360-pipeline",
  input: JSON.stringify({
    source: "api",
    timestamp: new Date().toISOString()
  })
});

const response = await client.send(command);
```

## Monitoring and Troubleshooting

### CloudWatch Metrics

Key metrics to monitor:
- **ExecutionsFailed**: Number of failed executions
- **ExecutionsSucceeded**: Number of successful executions  
- **ExecutionTime**: Duration of pipeline executions
- **ExecutionsTimedOut**: Number of timed-out executions

### CloudWatch Alarms

Set up alarms for critical metrics:
```bash
# Create alarm for failed executions
aws cloudwatch put-metric-alarm \
  --alarm-name "Profile360-Pipeline-Failures" \
  --alarm-description "Alert when Profile360 pipeline fails" \
  --metric-name ExecutionsFailed \
  --namespace AWS/States \
  --statistic Sum \
  --period 300 \
  --threshold 1 \
  --comparison-operator GreaterThanOrEqualToThreshold \
  --dimensions Name=StateMachineArn,Value=arn:aws:states:region:account:stateMachine:profile360-pipeline
```

### Execution History

View execution details:
```bash
# List recent executions
aws stepfunctions list-executions \
  --state-machine-arn arn:aws:states:region:account:stateMachine:profile360-pipeline \
  --max-items 10

# Get execution details
aws stepfunctions describe-execution \
  --execution-arn arn:aws:states:region:account:execution:profile360-pipeline:execution-name

# Get execution history
aws stepfunctions get-execution-history \
  --execution-arn arn:aws:states:region:account:execution:profile360-pipeline:execution-name
```

### Common Issues and Solutions

#### 1. Lambda Function Timeouts
**Symptom**: Tasks fail with timeout errors
**Solution**: Increase Lambda timeout or optimize function code
```typescript
timeout: cdk.Duration.minutes(5), // Increase from 30 seconds
memorySize: 512, // Increase memory for better performance
```

#### 2. S3 Data Not Available
**Symptom**: Lambda functions fail to find input data
**Solution**: Verify S3 bucket structure and data upload process
```bash
# Check S3 data availability
aws s3 ls s3://tenant-876131/applications/EntraID/ --recursive
```

#### 3. Neo4j Connection Issues
**Symptom**: Database ingestion tasks fail
**Solution**: Verify Neo4j credentials and network connectivity
```python
# Test Neo4j connection
from neo4j import GraphDatabase
driver = GraphDatabase.driver("neo4j+s://52ed4289.databases.neo4j.io", auth=("neo4j", "password"))
with driver.session() as session:
    result = session.run("RETURN 1")
    print(result.single()[0])
```

#### 4. Parallel Execution Failures
**Symptom**: Some branches succeed while others fail
**Solution**: Review individual Lambda logs and adjust retry policies
```json
{
  "Retry": [
    {
      "ErrorEquals": ["States.TaskFailed"],
      "IntervalSeconds": 5,
      "MaxAttempts": 5,
      "BackoffRate": 2.0
    }
  ]
}
```

## Performance Optimization

### Parallel Execution Benefits
- **Data Formatting**: Entra and Jira formatting run simultaneously
- **Neo4j Ingestion**: All three sources (Entra, GitHub, Jira) ingest in parallel
- **Total Time Reduction**: ~60% faster than sequential execution

### Resource Optimization
- **Lambda Memory**: Adjust based on data volume
- **Concurrent Executions**: Set reserved concurrency for predictable performance
- **Step Functions Express**: Consider Express workflows for high-frequency executions

## Cost Analysis

### Step Functions Pricing
- **Standard Workflows**: $0.025 per 1,000 state transitions
- **Express Workflows**: $1.00 per 1 million requests + duration charges

### Estimated Monthly Costs (Daily Execution)
- **State Transitions**: ~15 transitions per execution × 30 days = 450 transitions/month
- **Cost**: 450 × $0.025/1000 = $0.01/month
- **Lambda Costs**: Existing Lambda execution costs remain the same
- **EventBridge**: $1.00 per 1 million events (negligible for daily execution)

## Migration from Manual Execution

### Backward Compatibility
- All existing Lambda functions remain unchanged
- Manual execution still supported via AWS Console or API
- Gradual migration possible by running both approaches in parallel

### Testing Strategy
1. **Development Environment**: Test Step Functions with sample data
2. **Staging Environment**: Run parallel executions (manual + Step Functions)
3. **Production Environment**: Switch to Step Functions after validation

### Rollback Plan
If issues arise, you can quickly disable the scheduled rule:
```bash
# Disable the scheduled rule
aws events disable-rule --name {environment}-profile360-daily-sync

# Re-enable manual execution processes
# (No changes needed - Lambda functions remain accessible)
```


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/docs/profile360-stepfunctions-deployment.md) · Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-stepfunctions-deployment.md

Project code and dependencies remain outside the vault. No source commands were executed.
