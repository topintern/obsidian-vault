---
kind: "project-document"
title: "Profile360-stepfunctions-code-organization"
collection: "TrustX"
topic: "Infrastructure/Profile360"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-stepfunctions-code-organization.md"]
tags: ["career/library","career/project-docs"]
---

# Profile360-stepfunctions-code-organization

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Profile 360 Step Functions Code Organization

## Overview

The Profile 360 Step Functions workflow is now organized as code within the `src/profile-360/StepFunctions/` directory, following the same pattern as the Lambda functions. This approach provides better maintainability, version control, and testing capabilities.

## Directory Structure

```
AWS/src/profile-360/
├── Entra/
│   ├── Entra_Data_Formatting.py
│   ├── Entra_to_Neo4j.py
│   └── requirements.txt
├── Github/
│   ├── Github_to_Neo4j.py
│   └── requirements.txt
├── Jira/
│   ├── Jira_Data_Formatting.py
│   ├── Jira_to_Neo4j.py
│   └── requirements.txt
└── StepFunctions/                    # ← NEW
    ├── profile360-pipeline.json     # Workflow definition
    ├── workflow-loader.ts           # TypeScript loader utility
    ├── test-workflow.ts             # Test script
    └── README.md                    # Documentation
```

## Key Files

### 1. `profile360-pipeline.json`
**Purpose**: Amazon States Language (ASL) definition of the Step Functions workflow

**Features**:
- Parallel data formatting stage (Entra ID + Jira)
- Parallel Neo4j ingestion stage (Entra ID + GitHub + Jira)
- Comprehensive error handling with retry logic
- Lambda ARN placeholders for environment-agnostic deployment

**Example Structure**:
```json
{
  "Comment": "Profile360 data ingestion and processing pipeline",
  "StartAt": "DataFormattingParallel",
  "States": {
    "DataFormattingParallel": {
      "Type": "Parallel",
      "Branches": [
        {
          "StartAt": "EntraDataFormattingTask",
          "States": {
            "EntraDataFormattingTask": {
              "Type": "Task",
              "Resource": "arn:aws:states:::lambda:invoke",
              "Parameters": {
                "FunctionName": "${EntraDataFormattingLambdaArn}",
                "Payload.$": "$"
              }
            }
          }
        }
      ]
    }
  }
}
```

### 2. `workflow-loader.ts`
**Purpose**: TypeScript utility for loading and processing the workflow definition

**Key Functions**:
- `loadWorkflowDefinition()`: Loads JSON and replaces Lambda ARN placeholders
- `validateWorkflowDefinition()`: Validates workflow structure
- `extractLambdaPlaceholders()`: Extracts placeholder names for validation
- `createLambdaArnMappings()`: Helper to create ARN mappings from CDK functions

**Usage in CDK**:
```typescript
import { Profile360WorkflowLoader, createLambdaArnMappings } from '../src/profile-360/StepFunctions/workflow-loader';

const lambdaArns = createLambdaArnMappings({
  entraDataFormattingLambda: this.entraDataFormattingLambda,
  entraToNeo4jLambda: this.entraToNeo4jLambda,
  // ... other functions
});

const workflowDefinition = Profile360WorkflowLoader.loadWorkflowDefinition(lambdaArns);
```

### 3. `test-workflow.ts`
**Purpose**: Comprehensive test script for validating the workflow definition

**Test Coverage**:
- ✅ Extract and validate Lambda placeholders
- ✅ Load workflow definition successfully
- ✅ Validate workflow structure
- ✅ Check for unresolved placeholders
- ✅ Validate state machine structure
- ✅ Verify error handling configuration
- ✅ Generate sample execution input

**Run Tests**:
```bash
npm run test:workflow
```

## Benefits of Code Organization

### 1. **Version Control**
- Step Functions definition is tracked in Git alongside Lambda code
- Easy to see workflow changes in pull requests
- Rollback capabilities for workflow modifications

### 2. **Environment Agnostic**
- Uses placeholders instead of hardcoded ARNs
- Same workflow definition works across dev/staging/production
- Automatic ARN replacement during deployment

### 3. **Validation and Testing**
- Automated validation of workflow structure
- Pre-deployment testing of workflow definition
- Catch errors before deployment

### 4. **Maintainability**
- Clear separation of concerns
- Easy to modify workflow without touching CDK code
- Documentation co-located with implementation

### 5. **Consistency**
- Follows same pattern as Lambda functions
- Consistent directory structure across all Profile 360 components
- Easy for developers to understand and navigate

## CDK Integration

### Updated Profile360Stack

The CDK stack now uses the workflow loader instead of defining the workflow inline:

```typescript
// Before: Inline workflow definition
const dataFormattingParallel = new stepfunctions.Parallel(this, 'DataFormattingParallel', {
  comment: 'Format data from multiple sources in parallel',
});
// ... many lines of workflow definition

// After: Load from file
const lambdaArns = createLambdaArnMappings({
  entraDataFormattingLambda: this.entraDataFormattingLambda,
  // ... other functions
});

const workflowDefinition = Profile360WorkflowLoader.loadWorkflowDefinition(lambdaArns);

this.profile360StateMachine = new stepfunctions.StateMachine(this, 'Profile360StateMachine', {
  definitionBody: stepfunctions.DefinitionBody.fromString(JSON.stringify(workflowDefinition)),
  // ... other properties
});
```

### Benefits in CDK
- **Cleaner Code**: CDK stack focuses on infrastructure, not workflow logic
- **Easier Testing**: Can test workflow definition independently
- **Better Error Messages**: Validation errors point to specific workflow issues

## Development Workflow

### 1. **Modify Workflow**
```bash
# Edit the workflow definition
vim src/profile-360/StepFunctions/profile360-pipeline.json

# Test the changes
npm run test:workflow
```

### 2. **Add New Lambda Function**
```bash
# 1. Add placeholder to JSON workflow
"Parameters": {
  "FunctionName": "${NewLambdaArn}",
  "Payload.$": "$"
}

# 2. Update TypeScript interfaces
export interface LambdaArnMappings {
  // ... existing mappings
  NewLambdaArn: string;
}

# 3. Update CDK stack to include new function
const lambdaArns = createLambdaArnMappings({
  // ... existing functions
  newLambda: this.newLambda,
});

# 4. Test the changes
npm run test:workflow
```

### 3. **Deploy Changes**
```bash
# Deploy the updated stack
cdk deploy dev-profile360-stack

# Verify deployment
./scripts/verify-profile360-deployment.sh dev
```

## Error Handling and Debugging

### Common Issues

#### 1. **Unresolved Placeholders**
```
Error: Unresolved placeholders in workflow definition: ${SomeLambdaArn}
```
**Solution**: Add the missing Lambda function to the ARN mappings

#### 2. **Invalid JSON Syntax**
```
Error: Invalid JSON in workflow definition: Unexpected token...
```
**Solution**: Validate JSON syntax using a JSON validator

#### 3. **Missing Required Properties**
```
Error: Missing required property in workflow definition: StartAt
```
**Solution**: Ensure all required ASL properties are present

### Debugging Tools

#### 1. **Workflow Validation**
```bash
npm run test:workflow
```

#### 2. **Raw Workflow Output**
```typescript
const rawWorkflow = Profile360WorkflowLoader.getRawWorkflowDefinition(lambdaArns);
console.log(rawWorkflow);
```

#### 3. **Placeholder Extraction**
```typescript
const placeholders = Profile360WorkflowLoader.extractLambdaPlaceholders();
console.log('Required placeholders:', placeholders);
```

## Best Practices

### 1. **Workflow Design**
- Keep parallel branches independent
- Use meaningful state names
- Include comprehensive error handling
- Add comments for complex logic

### 2. **Code Organization**
- One workflow per JSON file
- Use descriptive file names
- Keep related utilities in the same directory
- Document all placeholders and their purposes

### 3. **Testing**
- Run tests before every deployment
- Validate workflow structure
- Test with realistic Lambda ARNs
- Include edge cases in testing

### 4. **Version Control**
- Commit workflow changes with descriptive messages
- Tag releases for production deployments
- Review workflow changes in pull requests
- Keep documentation up to date

## Migration from Inline Definition

If you have existing Step Functions defined inline in CDK, here's how to migrate:

### 1. **Extract Current Definition**
```typescript
// Get current state machine definition
const currentDefinition = stateMachine.definition;
console.log(JSON.stringify(currentDefinition, null, 2));
```

### 2. **Create JSON File**
- Copy the definition to a new JSON file
- Replace hardcoded ARNs with placeholders
- Add proper error handling and retry logic

### 3. **Update CDK Stack**
- Remove inline workflow definition
- Add workflow loader import and usage
- Test the migration thoroughly

### 4. **Validate Migration**
```bash
# Test the new workflow definition
npm run test:workflow

# Deploy and verify
cdk deploy dev-profile360-stack
./scripts/verify-profile360-deployment.sh dev
```

## Future Enhancements

### 1. **Multiple Workflows**
- Support for different workflow variants
- Environment-specific workflow customizations
- A/B testing of workflow changes

### 2. **Advanced Validation**
- Schema validation against ASL specification
- Performance analysis and optimization suggestions
- Integration with AWS Step Functions Local

### 3. **Workflow Generation**
- Template-based workflow generation
- Dynamic workflow creation based on configuration
- Visual workflow editor integration

## Summary

The new Step Functions code organization provides:

✅ **Better Maintainability**: Workflow definition as code alongside Lambda functions
✅ **Environment Agnostic**: Placeholder-based ARN replacement
✅ **Comprehensive Testing**: Automated validation and testing
✅ **Version Control**: Full Git integration for workflow changes
✅ **Developer Experience**: Clear structure and documentation
✅ **Production Ready**: Robust error handling and monitoring

This approach makes the Profile 360 Step Functions workflow easier to maintain, test, and deploy across different environments while following infrastructure-as-code best practices.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/docs/profile360-stepfunctions-code-organization.md) · Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-stepfunctions-code-organization.md

Project code and dependencies remain outside the vault. No source commands were executed.
