---
kind: "project-document"
title: "Neel Trust X ATAP Comprehensive Handoff Document"
collection: "TrustX"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/Samay Experience Repos (TrustX platform)/Neel_TrustX_ATAP_Comprehensive_Handoff_Document.md","Samay + Trustx experience/TrustxRepos/Neel_TrustX_ATAP_Comprehensive_Handoff_Document.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Neel Trust X ATAP Comprehensive Handoff Document

[[The Climb/Career Library/Career Library]]

# 🔁 TrustX ATAP – Engineering Documentation Handoff

**Owner:** Neel  
**Last Updated:** June 22, 2025  
**Reviewed By:** To be Reviewed by Rama  
**Module(s):** AWS Infrastructure, Profile-360 Pipeline, Automated Control Testing, Multi-tenant Architecture, AppRunner Services, Frontend Controls UI, Document Editor, Integrations, Lambda Functions

---

## 📋 1. Summary of Work

### Modules Owned:
- AWS Infrastructure & CDK Stacks
- Profile-360 Data Pipeline (Lambda Functions & Step Functions)
- Automated Control Testing System
- AppRunner Services for AI Query Processing
- Integration Services (GitHub, JIRA, EntraID)
- Frontend Controls UI & Compliance Interface
- Document Editor & Management System
- Policy Management Interface
- Lambda Functions Suite (Documents, List, Configure, Delete, Sync, Scheduler)

### Brief Overview:
Neel has helped implement a comprehensive AWS-based infrastructure for TrustX ATAP, including:

- **Profile-360 Pipeline:** Multi-tenant data processing pipeline that collects, formats, and ingests data from GitHub, JIRA, and EntraID into Neo4j databases for AI-powered compliance analysis
- **Automated Control Testing:** End-to-end system that automatically tests compliance controls (like TX-MON04.01) by collecting AWS infrastructure data, integration data, and document embeddings, then using LLM analysis to generate compliance scores and evidence
- **Multi-tenant Architecture:** Strict tenant isolation with dynamic tenant resolution from RDS PostgreSQL, tenant-specific S3 buckets, and separate Neo4j databases per tenant
- **AppRunner Services:** Containerized services for natural language to Cypher query processing with JWT authentication and VPC connectivity
- **Frontend Controls UI:** Complete React-based compliance controls interface with automated testing integration, comments system, evidence management, and status updates
- **Document Editor:** Rich text document editing capabilities for compliance documentation and policy management
- **Integration Services:** Comprehensive integration with GitHub, JIRA, and EntraID for data collection and synchronization
- **Lambda Functions Suite:** Complete set of serverless functions for document management, integration configuration, data synchronization, and scheduled operations

---

## ✅ 2. Feature Breakdown & Status

| Feature Name | Description | Status | Notes/Details |
|--------------|-------------|--------|---------------|
| **Profile-360 Data Pipeline** | Multi-tenant data collection, formatting, and Neo4j ingestion from GitHub, JIRA, EntraID | Refactored profile 360 to be a part of AWS CDK and made step functions a part of AWS CDK | Step Functions orchestration, scheduled execution, error handling |
| **Automated Control Testing** | End-to-end compliance control testing with LLM analysis and evidence generation | Lambda workflow that accepts with a control context performs data collections from AWS sources, data dumps and embeddings and generates compliance reports | Successfully testing TX-MON04.01, ready for generic control expansion |
| **Multi-tenant Architecture** | Tenant isolation, dynamic resolution, separate databases per tenant | Made profile 360 component multi-tenant in apprunner Flask API, and in AWS backend to resolve tenants from RDS | RDS tenant lookup, tenant-specific S3 buckets, Neo4j credentials from Secrets Manager |
| **AppRunner Query Service** | Apprunner is now a part of CDK and the repo is moved into AWS | Added tenant resolution from RDS in apprunner stack | VPC connectivity, psycopg2 conflict resolution, LangChain .invoke() implementation |
| **GraphQL Services** | Major Database refactor related to controls and added new GraphQL endpoints | Control details page currently uses these graphql methods | Fetching all controls, control details, tests, results, evidences, comments, policies |
| **Frontend Controls UI** | Complete React-based compliance controls interface | UI for controls dashboard, controls detail page, comments section | Controls listing, detail pages, automated testing, comments, evidence management |
| **Document Editor & Management** | Rich text document editing for compliance documentation | Loss of Formatting due to conversion from binary to Document Specific Format | Need library/service for format conversion with 0% formatting loss |
| **Integration Services** | GitHub, JIRA, EntraID integration for data collection | Can add new orgs, delete, sync and choose org scope | Real-time data synchronization, API integrations, error handling |
| **Policy Management Interface** | Policy creation, editing, and management system | Incomplete | Bugs in ineffect-draft-template, database inconsistencies, version control interface required |
| **Document Lambda Function** | Complete document management with S3 integration and CRUD operations | Can store retrieve normal and policy type documents and parse/convert to different file formats | Binary file to document format conversion with formatting preservation needed |
| **List Lambda Function** | List Lambda Function used to list ORGs of each integration | Can List Orgs | List orgs from s3 |
| **Configure Lambda Function** | Configure Lambda Function used to configure new ORGs for integrations | Can add new orgs | Can add features like immediate credential validation |
| **Delete Lambda Function** | Delete Lambda Function used to delete existing ORGs of integrations | Deletes specific Orgs | Delete existing org by deleting config info and secrets |
| **Sync Lambda Function** | Sync Lambda Function used to refresh ORGs of integrations | Would fetch orgs for that specific integration | Sync org info serves as refresh by looking up orgs in s3 |
| **Scheduler Lambda Function** | Scheduler Lambda Function used to schedule data dumps of integrations in S3 buckets | Scheduler function currently stores clean dumps | Scheduler lambda hits APIs of Entra, Jira and Github periodically |

---

## 🔐 3. Access & Credentials

| Resource | Credential | Access Type | Notes |
|----------|------------|-------------|-------|
| **GitHub** | neel-assurex | Admin | Github access |
| **Google** | neel@assurexinc.com | Admin | For Atlassian, Jira, Google workspace, Trustx platform |
| **Entra** | neel@nagarur.net | Admin | For Entra Admin console |
| **JIRA** | neel@assurexinc.com | Admin | Jira platform |
| **AWS** | neel-trustx | Dev | Orchestrates data pipeline execution |
| **Trustx** | neel@assurexinc.com (trustx), neel+trustxinc@assurexinc.com (trustxinc) | Admin | Trustx platform access |
| **Augment Code** | neel@assurexinc.com | Admin | Google account login |

> All AWS resources are in us-east-2 region. PostgreSQL, Neo4j credentials are stored in AWS Secrets Manager with tenant-specific keys.

---

## 🧠 4. Technical Architecture

### 4.1 Database Schema

**Tables Created/Used:**
- controls (compliance controls public schema)
- control_implementations
- control_evidences
- control_tests
- control_test_results
- document_embeddings
- documents (document metadata and references)
- users
- comments
- policies

**Schema Notes:**
> Multi-tenant architecture with tenant-specific schemas (tenant_251967, tenant_876131). Each tenant has isolated data in PostgreSQL and separate Neo4j databases. Document embeddings stored with S3 keys for reference. Document content stored in S3 with metadata in PostgreSQL.

### 4.2 Backend - Lambda Functions

**Services Used:**
- AWS Lambda (Python) - Profile-360 pipeline, automated control testing, document management, integrations
- AWS Step Functions - Pipeline orchestration
- AWS AppRunner - AI query service
- PostgreSQL RDS - Tenant and compliance data
- Neo4j - Graph databases per tenant
- S3 - Document storage and results
- AWS Secrets Manager - Neo4j credentials

**Document Lambda Function (manageDocuments.py):**

| Feature | Description | Implementation |
|---------|-------------|----------------|
| CRUD Operations | Complete Create, Read, Update, Delete operations for documents | RESTful API with GET, POST, PUT, DELETE methods |
| S3 Integration | Document content storage in S3 with metadata in PostgreSQL | Automatic S3 upload/download with content type detection |
| Multi-format Support | Support for JSON, text, binary files, images, PDFs | Content-type based processing with base64 encoding for binary |
| Policy Documents | Special handling for policy document types | Policy-specific database operations and S3 storage |
| Version Control | Document versioning and update tracking | Timestamp-based versioning with S3 metadata |
| Error Handling | Comprehensive error handling and logging | Try-catch blocks with detailed error messages and rollback |
| Multi-tenant Support | Tenant-aware document operations | Tenant-specific S3 buckets and database schemas |

**Key Document Lambda Features:**
- **S3 Content Storage:** Document content stored in S3 with automatic content-type detection and proper file extensions
- **Database Metadata:** Document metadata (title, description, type, etc.) stored in PostgreSQL for fast querying
- **Binary File Support:** Handles images, PDFs, and other binary files with base64 encoding for API responses
- **Policy Integration:** Special handling for policy documents with dedicated database operations
- **Content Validation:** Validates document content and handles empty or invalid content gracefully
- **Cleanup Operations:** Automatic cleanup of S3 objects when documents are deleted
- **JWT Authentication:** Secure access with JWT token validation

> Document Lambda supports multi-tenancy with automatic tenant discovery from RDS. All document content is stored in tenant-specific S3 buckets with comprehensive error handling and logging.

### 4.3 Frontend

**Major Components Developed:**
- **FocusAreaDetail.jsx** - Main control detail page with automated testing integration
- **Controls UI Components** - Complete controls listing and management interface
- **Comments System** - Comments and evidence management for controls
- **Status Update System** - Control status management and tracking
- **Document Editor** - Rich text editing for compliance documents and policies
- **Policy Management** - Policy creation, editing, and frame management
- **Integration Pages** - UI for managing GitHub, JIRA, and EntraID integrations
- **Security Headers** - CSP configuration and security policy management

**Key Frontend Features:**

| Feature | Description | Branch/PR |
|---------|-------------|-----------|
| Automated Control Testing | Test Control button with API integration to Lambda backend | #101 - Add automated control testing integration |
| Control Policies UI | Policy management interface for compliance controls | #99 - control-policies |
| Comments & Evidence UI | Comments section and evidence management for controls | #98 - comments and evidences ui |
| Control Detail Pages | Comprehensive control detail view with all metadata | #94 - control detail page |
| Controls UI Redesign | Modern, responsive controls interface design | #92 - controls-ui-new-design |
| Status Update Backend | GraphQL integration for control status management | #96 - status update backend |
| Document Editor | Rich text document editing with version control | document-edit-ui branch |
| Documents Management | Document listing, upload, and management interface | documents-v1 branch |
| EntraID Integration | Frontend interface for EntraID integration management | entra-id-integration branch |
| Policy Frames | Policy frame management and editing interface | Policy-Frames-addition branch |
| Policy Edit/View | Policy editing and viewing modes | Policy-Edit-View branch |
| Security Headers | CSP fixes for blob URLs, worker sources, CDN support | Multiple commits - headers fixes |

**Deployment:**
> React application deployed via standard build process. Frontend connects to backend APIs for control testing functionality. Includes comprehensive security headers and CSP configuration. Document editor supports rich text editing with Material-UI components.

---

## 🚀 5. Deployment Instructions

### For AWS Infrastructure:
1. cd AWS
2. npm install
3. npm run build
4. cdk deploy --all

### For Lambda Stacks in AWS:
1. Deploy any stack by ex: - Profile360Stack by cd AWS && ./scripts/deploy-profile-360-stack.sh --env=dev

### For Frontend:
1. cd trustx
2. npm install
3. npm run build

---

## 🛠️ 6. Local Dev Setup

1. Clone repositories: AWS, trustx, integration
2. Install dependencies: npm install in each repo
3. Configure AWS credentials for us-east-2 region
4. Set up local PostgreSQL connection for testing

---

## 🧾 7. Known Issues & TODOs

| Area | Description | Suggested Fix / Next Steps |
|------|-------------|----------------------------|
| **Document Editor** | Rich text editor may need additional features | Loss of Formatting due to conversion from binary to Document Specific Format. Need a solution to preserve 100% formatting |
| **Policy Management Interface** | Bugs in ineffect-draft-template. Database inconsistencies | Fix Database inconsistencies, according to the holistic definition of ineffect-draft-template functionality. Version control interface of policies required |
| **Automated Testing of Controls** | For automated testing of controls we have tried various ways through API calls and n8n. Now through lambdas we have a workflow that can accept any control and perform source collection and autonomous analysis | Right now, some prompts are hardcoded with cc7.1, but this needs to be tweaked to make it generic using the input control id. Generated documents are stored in s3 tenant bucket in automated-testing folder |

---

## 📌 8. Suggested Improvements / Future Work

- **Generic Control Support:** Expand automated testing to accept any control ID and dynamically configure testing flow
- **Enhanced Data Sources:** Add additional sources and other compliance tools to data collection
- **LLM Fine-tuning:** Improve analysis quality with domain-specific training on compliance frameworks
- **Dashboard Integration:** Connect automated testing results to existing compliance dashboards
- **Parallel Processing:** Implement concurrent testing of multiple controls
- **Real-time Alerting:** Add notifications for compliance score changes
- **Performance Optimization:** Optimize data collection and processing for larger datasets
- **Frontend Enhancements:** Add real-time progress tracking, advanced filtering, and bulk operations
- **Document Collaboration:** Add real-time collaborative editing features to document editor
- **Advanced Integrations:** Expand integration capabilities to include more third-party services
- **Policy Automation:** Implement automated policy generation based on compliance requirements
- **Document Versioning:** Implement comprehensive document version control with diff capabilities
- **Bulk Document Operations:** Add support for bulk document upload, download, and management

---

## 📊 9. Code Contributions Summary

**GitHub Statistics (neel-assurex):**
- **AWS Repository:** 23+ commits including infrastructure, pipelines, and automated testing
- **trustx Repository:** 50+ commits including UI components, fixes, and API integrations
- **integration Repository:** Multiple commits for GitHub, JIRA, EntraID integration services

**Major Pull Requests & Branches:**

| Repository | Feature/Branch | Impact |
|------------|----------------|--------|
| AWS | Fix automated control testing: document embeddings search and S3 storage improvements | Complete automated testing system with 32+ document embeddings |
| AWS | Document Lambda Stack Implementation | Complete document management system with S3 integration and CRUD operations |
| trustx | Add automated control testing integration to FocusAreaDetail | Frontend integration with Lambda backend for control testing |
| trustx | control-policies | Policy management interface for compliance controls |
| trustx | comments and evidences ui | Comments system and evidence management |
| trustx | control detail page | Comprehensive control detail views |
| trustx | controls-ui-new-design | Modern, responsive controls interface with Material-UI components |
| trustx | document-edit-ui branch | Rich text document editor with editing capabilities |
| trustx | documents-v1 branch | Document management system with upload and organization |
| trustx | integration branch | Integration interface and management |
| trustx | Policy-Frames-addition branch | Policy frame management and editing system |
| trustx | Policy-Edit-View branch | Policy editing and viewing modes |

**Key Technical Achievements:**
- **50+ commits** across trustx repository with comprehensive UI development
- **Multiple feature branches** for document editing, policy management, and integrations
- **Material-UI integration** for modern, responsive design components
- **GraphQL client implementation** for efficient data fetching and management
- **Integration management** interfaces for external service connections
- **Scheduler Data Dumps** periodic data dumps from Entra, Jira and Github
- **Policy management system** with frame-based editing and viewing
- **Document Editor implementation** with CRUD operations and S3 integration
- **Multi-format document support** including binary files, images, and PDFs

---

## 🔍 10. AWS Dependabot Integration

**Recently Added:** AWS Dependabot data collection has been integrated into the automated control testing system to enhance security vulnerability detection.

**Implementation Details:**
- **AWS Inspector v2 Integration:** Collects vulnerability findings similar to Dependabot for AWS infrastructure
- **Security Hub Integration:** Aggregates security findings from multiple AWS security services
- **Vulnerability Data Collection:** Automatically collects and categorizes security vulnerabilities by severity (Critical, High, Medium, Low)
- **IAM Permissions:** Added necessary permissions for Inspector v2 and Security Hub access
- **Data Storage:** Vulnerability findings are stored alongside other compliance data for comprehensive analysis

**Key Features:**
- Real-time vulnerability scanning results
- Severity-based categorization and reporting
- Integration with existing compliance testing workflow
- Automated collection of security findings
- Enhanced compliance reporting with vulnerability context

This integration provides comprehensive security vulnerability data collection equivalent to Dependabot functionality within the AWS ecosystem, enhancing the overall compliance monitoring capabilities.

---

*This document serves as a comprehensive handoff for all work completed by Neel on the TrustX ATAP platform. For any questions or clarifications, please refer to the respective repositories or contact the development team.*


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Samay%20Experience%20Repos%20(TrustX%20platform)/Neel_TrustX_ATAP_Comprehensive_Handoff_Document.md) · Interview Prep company prep docs/Samay Experience Repos (TrustX platform)/Neel_TrustX_ATAP_Comprehensive_Handoff_Document.md
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/Neel_TrustX_ATAP_Comprehensive_Handoff_Document.md) · Samay + Trustx experience/TrustxRepos/Neel_TrustX_ATAP_Comprehensive_Handoff_Document.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
