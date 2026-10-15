---
kind: "project-document"
title: "Step Functions Overview"
collection: "TrustX"
topic: "Infrastructure/Control Testing"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/AWS/src/automated-control-testing/StepFunctions/README.md"]
tags: ["career/library","career/project-docs"]
---

# Step Functions Overview

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# Automated Control Testing Step Functions

This directory contains the Step Functions workflow definition for automated control testing.

## Workflow Overview

The automated control testing workflow performs the following steps:

1. **Initialize Testing**: Set up the testing session and prepare metadata
2. **Get All Tenants**: Query the database to get all tenant schemas for testing
3. **Process Tenants**: Execute control testing for each tenant in parallel (with concurrency limits)
4. **Generate Report**: Consolidate results and generate a comprehensive compliance report

## Control CC7.1 Testing

The workflow specifically tests control CC7.1 (System Monitoring) which focuses on:

- Detection and monitoring procedures to identify configuration changes
- Identification of new vulnerabilities  
- Susceptibilities to newly discovered vulnerabilities

## Data Sources

For each tenant, the workflow collects and analyzes data from:

- **AWS Infrastructure**: CloudTrail, Config rules, VPC Flow Logs, CloudWatch
- **Integrations**: JIRA (security issues), GitHub (security commits), Entra ID (access logs)
- **Tenant Configuration**: Monitoring setups, recent changes, vulnerability scans
- **Historical Data**: Previous test results and implementation status

## LLM Analysis

The workflow uses AWS Bedrock (Claude 3 Sonnet) to:

- Analyze collected data against control requirements
- Identify compliance gaps and strengths
- Generate specific recommendations
- Calculate compliance scores

## Scheduling

The workflow is scheduled to run daily at 2 AM UTC via EventBridge rules.

## Output

Results are stored in:
- Tenant-specific S3 buckets: `s3://tenant-{id}/automated-testing/CC7.1/{timestamp}/`
- Consolidated reports: `s3://automated-testing-{env}-{region}/reports/CC7.1/{timestamp}/`
- Database evidence records for audit trails


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/AWS/src/automated-control-testing/StepFunctions/README.md) · Samay + Trustx experience/TrustxRepos/AWS/src/automated-control-testing/StepFunctions/README.md

Project code and dependencies remain outside the vault. No source commands were executed.
