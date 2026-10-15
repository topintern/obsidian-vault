---
kind: "project-document"
title: "Profile360-s3-permissions-fix"
collection: "TrustX"
topic: "Infrastructure/Profile360"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-s3-permissions-fix.md"]
tags: ["career/library","career/project-docs"]
---

# Profile360-s3-permissions-fix

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Profile 360 S3 Permissions Fix

## Issue Summary

The Step Functions execution was failing with an S3 access denied error:

```
An error occurred (AccessDenied) when calling the GetObject operation: 
User: arn:aws:sts::533267024692:assumed-role/dev-profile360-stack-Profile360LambdaRole676427CA-HjYgqvxdKit8/dev-entra-data-formatting 
is not authorized to perform: s3:GetObject on resource: 
"arn:aws:s3:::tenant-876131/applications/EntraID/86781cf0-cd87-4878-a0d1-db321fb0f95f/2025-03-24_18-13-25/EntraUsers.json" 
because no identity-based policy allows the s3:GetObject action
```

## Root Cause

The Lambda functions in the Profile360 stack were missing S3 permissions to access the `tenant-876131` bucket where the Profile 360 data is stored.

## Solution Applied

### 1. Added S3 Permissions to Lambda Role

Updated the `Profile360LambdaRole` in `AWS/lib/profile360-stack.ts` to include S3 permissions:

```typescript
// Add permissions for S3 access (Profile360 data bucket)
lambdaRole.addToPolicy(new iam.PolicyStatement({
  actions: [
    's3:GetObject',
    's3:PutObject', 
    's3:ListBucket',
    's3:DeleteObject'
  ],
  resources: [
    'arn:aws:s3:::tenant-876131',
    'arn:aws:s3:::tenant-876131/*'
  ],
}));
```

### 2. Enhanced Lambda Functions with Environment Variables

Updated all Lambda functions to use environment variables instead of hardcoded values:

#### Entra Data Formatting Lambda
- **S3_BUCKET**: `tenant-876131`
- **BASE_PREFIX**: `applications/EntraID/86781cf0-cd87-4878-a0d1-db321fb0f95f`
- **INPUT_FILE**: `EntraUsers.json`
- **OUTPUT_FILE**: `ProcessedUsers.json`

#### Entra to Neo4j Lambda
- **S3_BUCKET**: `tenant-876131`
- **BASE_PREFIX**: `applications/EntraID/86781cf0-cd87-4878-a0d1-db321fb0f95f`
- **CONSOLIDATED_FILE**: `ConsolidatedUsers.json`
- **NEO4J_URI**: `neo4j+s://52ed4289.databases.neo4j.io`
- **NEO4J_USER**: `neo4j`
- **NEO4J_PASSWORD**: `yAm9Mrh1lxADXS6CwnfvchtDogcS9VxzBN3TYof2sIQ`

#### GitHub to Neo4j Lambda
- **S3_BUCKET**: `tenant-876131`
- **BASE_PREFIX**: `applications/Github/TrustxInc`
- **NEO4J_URI**: `neo4j+s://52ed4289.databases.neo4j.io`
- **NEO4J_USER**: `neo4j`
- **NEO4J_PASSWORD**: `yAm9Mrh1lxADXS6CwnfvchtDogcS9VxzBN3TYof2sIQ`

#### Jira Data Formatting Lambda
- **S3_BUCKET**: `tenant-876131`
- **BASE_PREFIX**: `applications/Jira/TrustxInc`
- **OUTPUT_FILE**: `consolidated_jira_users.json`
- **JIRA_USERS_FILE**: `Atlassian_Jira_Users.json`
- **JIRA_ROLES_FILE**: `Atlassian_User_Roles.json`

#### Jira to Neo4j Lambda
- **S3_BUCKET**: `tenant-876131`
- **BASE_PREFIX**: `applications/Jira/TrustxInc`
- **NEO4J_URI**: `neo4j+s://52ed4289.databases.neo4j.io`
- **NEO4J_USER**: `neo4j`
- **NEO4J_PASSWORD**: `yAm9Mrh1lxADXS6CwnfvchtDogcS9VxzBN3TYof2sIQ`

### 3. Improved Error Handling in Lambda Functions

Enhanced the `Entra_Data_Formatting.py` function with:

- **Environment Variable Support**: Uses `os.environ.get()` for configuration
- **Dynamic Path Resolution**: Can find the latest date folder automatically
- **Better Error Handling**: Comprehensive try-catch blocks with detailed logging
- **Flexible Input/Output**: Supports custom file names via event parameters

#### Key Improvements:

```python
# Environment variables with defaults
BUCKET = os.environ.get('S3_BUCKET', 'tenant-876131')
BASE_PREFIX = os.environ.get('BASE_PREFIX', "applications/EntraID/86781cf0-cd87-4878-a0d1-db321fb0f95f")
DATE_FOLDER = os.environ.get('DATE_FOLDER', "2025-03-24_18-13-25")
INPUT_FILE = os.environ.get('INPUT_FILE', "EntraUsers.json")
OUTPUT_FILE = os.environ.get('OUTPUT_FILE', "ProcessedUsers.json")

# Dynamic folder detection
def get_latest_folder(bucket, prefix):
    """Get the latest date folder in the given prefix"""
    # Implementation finds the most recent date folder automatically

# Enhanced lambda handler
def lambda_handler(event=None, context=None):
    """Main Lambda handler with error handling"""
    # Supports event parameters for custom configuration
    # Provides detailed error messages and logging
    # Returns structured response with execution details
```

## Deployment Instructions

### 1. Deploy the Updated Stack

```bash
cd AWS

# Build the project
npm run build

# Deploy the Profile360 stack with S3 permissions
cdk deploy stg-profile360-stack --context imageTag=latest

# Or for other environments
cdk deploy dev-profile360-stack --context imageTag=latest
cdk deploy prod-profile360-stack --context imageTag=latest
```

### 2. Verify S3 Permissions

```bash
# Check that the Lambda role has S3 permissions
aws iam get-role-policy \
  --role-name stg-profile360-stack-Profile360LambdaRole \
  --policy-name S3AccessPolicy

# List Lambda functions to verify they exist
aws lambda list-functions \
  --query 'Functions[?contains(FunctionName, `profile360`) || contains(FunctionName, `entra`) || contains(FunctionName, `github`) || contains(FunctionName, `jira`)]'
```

### 3. Test Step Functions Execution

```bash
# Start a manual execution
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:us-east-2:533267024692:stateMachine:stg-profile360-pipeline \
  --name "test-execution-$(date +%s)" \
  --input '{
    "source": "manual-test",
    "environment": "stg",
    "bucket": "tenant-876131"
  }'

# Monitor the execution
aws stepfunctions describe-execution \
  --execution-arn arn:aws:states:us-east-2:533267024692:execution:stg-profile360-pipeline:test-execution-xxxxx
```

### 4. Verify Data Processing

```bash
# Check if processed files are created in S3
aws s3 ls s3://tenant-876131/applications/EntraID/86781cf0-cd87-4878-a0d1-db321fb0f95f/ --recursive

# Check Lambda function logs
aws logs tail /aws/lambda/stg-entra-data-formatting --follow
```

## Expected S3 Data Structure

The Lambda functions now expect the following S3 structure:

```
tenant-876131/
├── applications/
│   ├── EntraID/
│   │   └── 86781cf0-cd87-4878-a0d1-db321fb0f95f/
│   │       └── 2025-03-24_18-13-25/
│   │           ├── EntraUsers.json          # Input file
│   │           ├── ProcessedUsers.json      # Output from formatting
│   │           └── ConsolidatedUsers.json   # Final consolidated data
│   ├── GitHub/
│   │   └── TrustxInc/
│   │       └── {date-folder}/
│   │           └── github_users.json
│   └── Jira/
│       └── TrustxInc/
│           └── {date-folder}/
│               ├── Atlassian_Jira_Users.json
│               ├── Atlassian_User_Roles.json
│               └── consolidated_jira_users.json
```

## Troubleshooting

### Common Issues

#### 1. S3 Access Still Denied
```bash
# Check if the IAM policy was applied correctly
aws iam list-attached-role-policies --role-name stg-profile360-stack-Profile360LambdaRole
aws iam list-role-policies --role-name stg-profile360-stack-Profile360LambdaRole
```

#### 2. File Not Found Errors
```bash
# Verify the S3 structure matches expectations
aws s3 ls s3://tenant-876131/applications/ --recursive

# Check Lambda environment variables
aws lambda get-function-configuration --function-name stg-entra-data-formatting
```

#### 3. Step Functions Execution Fails
```bash
# Get detailed execution history
aws stepfunctions get-execution-history \
  --execution-arn arn:aws:states:us-east-2:533267024692:execution:stg-profile360-pipeline:execution-name \
  --max-items 50
```

### Validation Steps

1. **Verify S3 Permissions**: Lambda role should have `s3:GetObject`, `s3:PutObject`, `s3:ListBucket`, `s3:DeleteObject`
2. **Check Environment Variables**: All Lambda functions should have the correct S3 and Neo4j configuration
3. **Test Individual Functions**: Test each Lambda function independently before running the full pipeline
4. **Monitor CloudWatch Logs**: Check logs for detailed error messages and execution flow

## Security Considerations

### Current Implementation
- Neo4j credentials are stored as environment variables (not ideal for production)
- S3 bucket access is granted to all objects in the bucket

### Recommended Improvements
1. **Use AWS Secrets Manager** for Neo4j credentials
2. **Implement least-privilege S3 access** with more specific resource ARNs
3. **Add encryption** for sensitive data in transit and at rest
4. **Implement IAM roles** for cross-service access instead of hardcoded credentials

### Future Enhancements
1. **Parameter Store Integration**: Store configuration in AWS Systems Manager Parameter Store
2. **KMS Encryption**: Encrypt sensitive environment variables
3. **VPC Endpoints**: Use VPC endpoints for S3 access to keep traffic within AWS network
4. **Resource-based Policies**: Implement bucket policies for additional security layers

## Summary

The S3 permissions issue has been resolved by:

✅ **Adding S3 permissions** to the Lambda execution role
✅ **Enhancing Lambda functions** with environment variables and better error handling  
✅ **Improving code flexibility** with dynamic path resolution
✅ **Adding comprehensive logging** for better debugging
✅ **Maintaining backward compatibility** with existing data structures

The Profile 360 Step Functions pipeline should now execute successfully with proper S3 access and improved error handling.


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/docs/profile360-s3-permissions-fix.md) · Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-s3-permissions-fix.md

Project code and dependencies remain outside the vault. No source commands were executed.
