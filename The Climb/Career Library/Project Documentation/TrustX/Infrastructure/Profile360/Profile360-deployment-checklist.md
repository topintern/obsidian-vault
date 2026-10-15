---
kind: "project-document"
title: "Profile360-deployment-checklist"
collection: "TrustX"
topic: "Infrastructure/Profile360"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-deployment-checklist.md"]
tags: ["career/library","career/project-docs"]
---

# Profile360-deployment-checklist

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Profile 360 Deployment Checklist

## Pre-Deployment Verification

### ✅ Code Quality Checks
- [ ] TypeScript compilation successful (`npm run build`)
- [ ] Step Functions workflow validation passed (`npm run test:workflow`)
- [ ] No linting errors or warnings
- [ ] All imports and dependencies resolved

### ✅ Configuration Verification
- [ ] Environment variables configured for all Lambda functions
- [ ] S3 bucket permissions added to Lambda role
- [ ] Neo4j connection details configured
- [ ] Step Functions workflow template loads correctly

### ✅ Infrastructure Validation
- [ ] CDK stack synthesizes without errors
- [ ] IAM roles and policies defined correctly
- [ ] VPC and security group configurations verified
- [ ] Lambda layer dependencies available

## Deployment Steps

### 1. Build and Test
```bash
cd AWS

# Build the project
npm run build

# Test Step Functions workflow
npm run test:workflow

# Verify CDK synthesis
cdk synth stg-profile360-stack --context imageTag=latest --quiet
```

### 2. Deploy Infrastructure
```bash
# Deploy the Profile360 stack
cdk deploy stg-profile360-stack --context imageTag=latest

# Verify deployment
./scripts/verify-profile360-deployment.sh stg
```

### 3. Validate S3 Permissions
```bash
# Check Lambda role permissions
aws iam get-role-policy \
  --role-name stg-profile360-stack-Profile360LambdaRole \
  --policy-name S3AccessPolicy

# Verify S3 bucket access
aws s3 ls s3://tenant-876131/applications/ --recursive
```

## Post-Deployment Testing

### ✅ Manual Function Testing
```bash
# Test individual Lambda functions
aws lambda invoke \
  --function-name stg-entra-data-formatting \
  --payload '{"bucket": "tenant-876131"}' \
  response.json

# Check response
cat response.json
```

### ✅ Step Functions Testing
```bash
# Start manual execution
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:us-east-2:533267024692:stateMachine:stg-profile360-pipeline \
  --name "deployment-test-$(date +%s)" \
  --input '{
    "source": "deployment-test",
    "environment": "stg",
    "bucket": "tenant-876131"
  }'

# Monitor execution
aws stepfunctions list-executions \
  --state-machine-arn arn:aws:states:us-east-2:533267024692:stateMachine:stg-profile360-pipeline \
  --max-items 5
```

### ✅ Data Validation
```bash
# Check processed files in S3
aws s3 ls s3://tenant-876131/applications/EntraID/ --recursive

# Verify Neo4j data ingestion
# (Check Neo4j browser or run Cypher queries)
```

### ✅ Monitoring Setup
```bash
# Check CloudWatch log groups
aws logs describe-log-groups \
  --log-group-name-prefix "/aws/lambda/stg-"

# Verify Step Functions metrics
aws cloudwatch get-metric-statistics \
  --namespace AWS/States \
  --metric-name ExecutionsSucceeded \
  --dimensions Name=StateMachineArn,Value=arn:aws:states:us-east-2:533267024692:stateMachine:stg-profile360-pipeline \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 3600 \
  --statistics Sum
```

## Rollback Plan

### If Deployment Fails
```bash
# Check deployment status
cdk list --context imageTag=latest

# Rollback to previous version
cdk destroy stg-profile360-stack --context imageTag=latest

# Redeploy previous working version
git checkout <previous-commit>
cdk deploy stg-profile360-stack --context imageTag=latest
```

### If Step Functions Fail
```bash
# Disable scheduled rule
aws events disable-rule --name stg-profile360-daily-sync

# Check execution errors
aws stepfunctions describe-execution \
  --execution-arn <failed-execution-arn>

# Fix issues and re-enable
aws events enable-rule --name stg-profile360-daily-sync
```

## Environment-Specific Considerations

### Development Environment
- [ ] Use test data sets
- [ ] Enable verbose logging
- [ ] Shorter timeout values for faster feedback
- [ ] Manual execution only (disable scheduled rule)

### Staging Environment
- [ ] Production-like data volumes
- [ ] Full pipeline testing
- [ ] Performance monitoring
- [ ] Scheduled execution enabled

### Production Environment
- [ ] Production data sources
- [ ] Optimized timeout and memory settings
- [ ] Comprehensive monitoring and alerting
- [ ] Backup and disaster recovery procedures

## Success Criteria

### ✅ Infrastructure Deployment
- [ ] All Lambda functions deployed successfully
- [ ] Step Functions state machine created
- [ ] EventBridge rule configured and enabled
- [ ] IAM roles and policies applied correctly
- [ ] CloudWatch log groups created

### ✅ Functional Testing
- [ ] Individual Lambda functions execute without errors
- [ ] Step Functions pipeline completes successfully
- [ ] Data is processed and stored correctly in S3
- [ ] Neo4j database receives and stores data properly
- [ ] Scheduled execution works as expected

### ✅ Performance Validation
- [ ] Pipeline execution time within acceptable limits
- [ ] Memory usage optimized for cost efficiency
- [ ] No timeout errors or resource constraints
- [ ] Parallel processing working correctly

### ✅ Monitoring and Observability
- [ ] CloudWatch metrics available
- [ ] Log aggregation working
- [ ] Error notifications configured
- [ ] Performance dashboards accessible

## Common Issues and Solutions

### S3 Access Denied
**Symptoms**: Lambda functions fail with S3 permission errors
**Solution**: Verify IAM role has correct S3 permissions
```bash
aws iam get-role-policy --role-name <role-name> --policy-name S3AccessPolicy
```

### Step Functions Timeout
**Symptoms**: State machine execution times out
**Solution**: Increase timeout or optimize Lambda functions
```typescript
timeout: cdk.Duration.hours(2), // Increase if needed
```

### Neo4j Connection Issues
**Symptoms**: Database ingestion fails
**Solution**: Verify Neo4j credentials and network connectivity
```python
# Test connection in Lambda function
driver = GraphDatabase.driver(NEO4J_URI, auth=basic_auth(NEO4J_USER, NEO4J_PASSWORD))
```

### Missing Environment Variables
**Symptoms**: Lambda functions use default values instead of configured ones
**Solution**: Check CDK environment variable configuration
```typescript
environment: {
  S3_BUCKET: 'tenant-876131',
  // ... other variables
}
```

## Maintenance Tasks

### Daily
- [ ] Monitor Step Functions execution status
- [ ] Check CloudWatch logs for errors
- [ ] Verify data processing completion

### Weekly
- [ ] Review performance metrics
- [ ] Check S3 storage usage and costs
- [ ] Validate data quality in Neo4j

### Monthly
- [ ] Update Lambda function dependencies
- [ ] Review and optimize resource allocation
- [ ] Test disaster recovery procedures
- [ ] Update documentation

## Contact Information

### Support Escalation
- **Infrastructure Issues**: AWS CDK Team
- **Lambda Function Issues**: Backend Development Team
- **Step Functions Issues**: DevOps Team
- **Data Quality Issues**: Data Engineering Team
- **Neo4j Issues**: Database Administration Team

### Emergency Contacts
- **On-Call Engineer**: [Contact Information]
- **Team Lead**: [Contact Information]
- **Product Owner**: [Contact Information]

## Documentation References

- [[The Climb/Career Library/Project Documentation/TrustX/Infrastructure/Profile360/Profile360-architecture-guide|Profile 360 Architecture Guide]]
- [[The Climb/Career Library/Project Documentation/TrustX/Infrastructure/Profile360/Profile360-stepfunctions-deployment|Step Functions Deployment Guide]]
- [[The Climb/Career Library/Project Documentation/TrustX/Infrastructure/Profile360/Profile360-s3-permissions-fix|S3 Permissions Fix]]
- [[The Climb/Career Library/Project Documentation/TrustX/Infrastructure/Profile360/Profile360-stepfunctions-code-organization|Code Organization Guide]]
- [[The Climb/Career Library/Project Documentation/TrustX/Infrastructure/Profile360/Profile360-system-overview|System Overview]]


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/docs/profile360-deployment-checklist.md) · Samay + Trustx experience/TrustxRepos/AWS/docs/profile360-deployment-checklist.md

Project code and dependencies remain outside the vault. No source commands were executed.
