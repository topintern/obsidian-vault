---
kind: "project-document"
title: "Automated Control Testing Overview"
collection: "TrustX"
topic: "Infrastructure/Control Testing"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/src/automated-control-testing/README.md"]
tags: ["career/library","career/project-docs"]
---

# Automated Control Testing Overview

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Automated Control Testing System

This system provides automated testing for compliance controls using AWS Lambda, Step Functions, and LLM analysis via AWS Bedrock.

## Overview

The Automated Control Testing system performs scheduled compliance testing for control CC7.1 (System Monitoring) across all tenants. It collects data from multiple sources, analyzes it using AI, and generates comprehensive compliance reports.

## Architecture

```
EventBridge (Daily 2 AM UTC)
    ↓
Step Functions Workflow
    ↓
Lambda Function (Multi-tenant)
    ↓
Data Collection → LLM Analysis → Evidence Storage
```

## Components

### 1. Lambda Function (`lambda_function.py`)
- **Main Handler**: Orchestrates control testing workflow
- **Multi-Action Support**: Initialize, get tenants, test controls, generate reports
- **Error Handling**: Comprehensive logging and error recovery

### 2. Control Tester (`control_tester.py`)
- **CC7.1 Implementation**: System monitoring control testing
- **Data Collection**: AWS infrastructure, integrations, tenant configs
- **Compliance Assessment**: Scoring and status determination

### 3. LLM Analyzer (`llm_analyzer.py`)
- **AWS Bedrock Integration**: Claude 3 Sonnet model
- **Intelligent Analysis**: Control requirement assessment
- **Structured Output**: JSON-formatted compliance reports

### 4. Data Collectors
- **AWS Collector**: CloudTrail, Config, VPC Flow Logs, CloudWatch
- **Integration Collector**: JIRA, GitHub, Entra ID security data

## Control CC7.1 Testing

### Focus Areas
- **Configuration Change Detection**: CloudTrail logging, change monitoring
- **Vulnerability Identification**: AWS Config compliance, vulnerability scans
- **Monitoring Procedures**: CloudWatch alarms, log aggregation
- **Documentation**: Audit trails, incident response records
- **Response Capabilities**: Alert systems, remediation tracking

### Data Sources
1. **AWS Infrastructure**
   - CloudTrail events and configuration
   - AWS Config rules and compliance status
   - VPC Flow Logs configuration
   - CloudWatch alarms and metrics
   - Security group changes

2. **Integration APIs**
   - JIRA: Security-related issues and audit logs
   - GitHub: Security commits and advisories
   - Entra ID: Sign-in logs and conditional access

3. **Tenant Configuration**
   - Monitoring system configurations
   - Recent system changes
   - Vulnerability scan results

4. **Historical Data**
   - Previous test results
   - Control implementation status
   - Trend analysis

## Deployment

### Quick Start
```bash
# Deploy the stack
./scripts/deploy-automated-control-testing.sh --env=dev

# Verify deployment
./scripts/verify-automated-control-testing-deployment.sh dev

# Test the lambda
./scripts/test-automated-control-testing.sh dev
```

### Detailed Deployment
```bash
# With specific parameters
./scripts/deploy-automated-control-testing.sh \
  --env=stg \
  --region=us-east-2 \
  --control=CC7.1

# Check deployment status
aws cloudformation describe-stacks \
  --stack-name stg-automated-control-testing-stack
```

## Testing

### Manual Lambda Testing
```bash
# Test initialization
aws lambda invoke \
  --function-name dev-automated-control-testing \
  --payload '{"action":"initialize","control_id":"CC7.1"}' \
  response.json

# Test tenant control
aws lambda invoke \
  --function-name dev-automated-control-testing \
  --payload '{"action":"test_tenant_control","tenant_name":"your-tenant","control_id":"CC7.1"}' \
  response.json
```

### Step Functions Testing
```bash
# Start workflow execution
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:us-east-2:ACCOUNT:stateMachine:dev-automated-control-testing \
  --input '{"action":"initialize","control_id":"CC7.1"}'
```

## Configuration

### Environment Variables
- `SECRET_ARN`: RDS database secret ARN
- `ENVIRONMENT`: Deployment environment (dev/stg/prod)
- `REGION`: AWS region
- `ACCOUNT_ID`: AWS account ID

### Required Permissions
- **Bedrock**: Model invocation for LLM analysis
- **S3**: Tenant bucket access for evidence storage
- **Secrets Manager**: Integration credentials
- **CloudTrail/Config/CloudWatch**: AWS monitoring data
- **RDS**: Multi-tenant database access

## Monitoring

### CloudWatch Logs
```bash
# Monitor lambda execution
aws logs tail /aws/lambda/dev-automated-control-testing --follow

# Check Step Functions logs
aws logs tail /aws/stepfunctions/dev-automated-control-testing --follow
```

### Step Functions Console
- Monitor workflow executions
- View execution history
- Debug failed executions

### S3 Evidence Storage
- **Tenant Results**: `s3://tenant-{id}/automated-testing/CC7.1/{timestamp}/`
- **Consolidated Reports**: `s3://automated-testing-{env}-{region}/reports/CC7.1/{timestamp}/`

## Troubleshooting

### Common Issues

1. **Bedrock Access Denied**
   ```bash
   # Check Bedrock access
   aws bedrock list-foundation-models --region us-east-2
   
   # Request model access in AWS console if needed
   ```

2. **Database Connection Issues**
   ```bash
   # Verify secret exists
   aws secretsmanager get-secret-value --secret-id dev/app_user
   
   # Check VPC connectivity
   ```

3. **S3 Access Issues**
   ```bash
   # List tenant buckets
   aws s3 ls | grep tenant-
   
   # Check bucket permissions
   ```

### Debug Mode
Enable detailed logging by setting log level to DEBUG in the lambda environment variables.

## Extending the System

### Adding New Controls
1. Update `control_requirements` in `control_tester.py`
2. Add control-specific data collection logic
3. Update LLM prompts for new requirements
4. Test with new control ID

### Adding Data Sources
1. Create new collector in `data_collectors/`
2. Integrate with `collect_all_data()` method
3. Update LLM analysis prompts
4. Add required IAM permissions

## Scheduling

The system runs automatically daily at 2 AM UTC via EventBridge. To modify the schedule:

1. Update the cron expression in `automated-control-testing-stack.ts`
2. Redeploy the stack

## Security

- All credentials stored in AWS Secrets Manager
- VPC-based lambda execution
- Least privilege IAM policies
- Encrypted data storage in S3
- Audit trails in CloudTrail

## Support

For issues or questions:
1. Check CloudWatch logs for errors
2. Verify all prerequisites are met
3. Run verification script
4. Review AWS service quotas and limits


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/src/automated-control-testing/README.md) · Samay + Trustx experience/TrustxRepos/AWS/src/automated-control-testing/README.md

Project code and dependencies remain outside the vault. No source commands were executed.
