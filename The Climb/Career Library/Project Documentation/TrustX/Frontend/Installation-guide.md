---
kind: "project-document"
title: "Installation-guide"
collection: "TrustX"
topic: "Frontend"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/trustx/docs/installation-guide.md"]
tags: ["career/library","career/project-docs"]
---

# Installation-guide

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# TrustX Installation Guide

This guide provides step-by-step instructions for setting up the TrustX application for development and production environments.

## Prerequisites

Before you begin, ensure you have the following installed:

- Node.js (v22.0.0 or higher)
- npm (v10.0.0 or higher)
- Git

## Development Environment Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-organization/trustx.git
cd trustx
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env.local` file in the root directory based on the `.env.example` template:

```bash
cp .env.example .env.local
```

Edit the `.env.local` file and fill in the required values:

```
# Auth0 Configuration
REACT_APP_AUTH0_DOMAIN=your-domain.auth0.com
REACT_APP_AUTH0_CLIENT_ID=your-client-id
REACT_APP_AUTH0_AUDIENCE=your-audience

# API Configuration
REACT_APP_API_URL=http://localhost:3001

# Application Name
REACT_APP_NAME=TrustX
```

### 4. Auth0 Configuration

1. Create an Auth0 account if you don't have one already
2. Create a new application in Auth0 dashboard
3. Configure the application settings:
   - Application Type: Single Page Application
   - Allowed Callback URLs: `http://localhost:3000`
   - Allowed Logout URLs: `http://localhost:3000`
   - Allowed Web Origins: `http://localhost:3000`
4. Create an API in Auth0 dashboard
5. Configure the API settings:
   - Identifier: This will be your `REACT_APP_AUTH0_AUDIENCE` value
   - Permissions: Define necessary permissions for your application

### 5. Start the Development Server

```bash
npm start
```

The application will be available at `http://localhost:3000`.

## Production Deployment

### 1. Build the Application

```bash
npm run build
```

This will create a `build` directory with optimized production files.

### 2. Configure Environment Variables for Production

Create a `.env.production` file with production-specific values:

```
REACT_APP_AUTH0_DOMAIN=your-production-domain.auth0.com
REACT_APP_AUTH0_CLIENT_ID=your-production-client-id
REACT_APP_AUTH0_AUDIENCE=your-production-audience
REACT_APP_API_URL=https://api.your-domain.com
REACT_APP_NAME=TrustX
```

### 3. Deploy the Build Directory

Deploy the contents of the `build` directory to your hosting provider. Some common options include:

- **Netlify**:
  - Connect your GitHub repository
  - Configure build settings: `npm run build`
  - Set environment variables in the Netlify dashboard

- **Vercel**:
  - Connect your GitHub repository
  - Vercel will automatically detect React and configure the build

- **AWS S3 + CloudFront**:
  - Upload the build directory to an S3 bucket
  - Configure CloudFront for content delivery
  - Set up proper cache headers

### 4. Configure Auth0 for Production

Update your Auth0 application settings with production URLs:
- Allowed Callback URLs: `https://your-production-domain.com`
- Allowed Logout URLs: `https://your-production-domain.com`
- Allowed Web Origins: `https://your-production-domain.com`

## Backend API Configuration

The TrustX frontend requires a backend API to function properly. You can either:

1. Use the existing TrustX API services (if you have access)
2. Implement your own backend services based on the API documentation

### Connecting to Existing API Services

If you have access to the TrustX API services, simply configure the `REACT_APP_API_URL` environment variable to point to the appropriate endpoint:

```
REACT_APP_API_URL=https://api.trustx.cloud
```

### Implementing Your Own Backend

If you need to implement your own backend services, refer to the [[The Climb/Career Library/Project Documentation/TrustX/Frontend/Api-documentation|API Documentation]] for details on the required endpoints and data structures.

## Neo4j Integration

TrustX uses Neo4j for graph visualization. To set up Neo4j:

1. Create a Neo4j database instance (cloud or self-hosted)
2. Update the connection details in your application code
3. Replace the hardcoded credentials in `src/components/Neo4jVisualizer.js` with environment variables:

```javascript
const driver = neo4j.driver(
  process.env.REACT_APP_NEO4J_URI,
  neo4j.auth.basic(
    process.env.REACT_APP_NEO4J_USER,
    process.env.REACT_APP_NEO4J_PASSWORD
  )
);
```

Add these variables to your `.env.local` file:

```
REACT_APP_NEO4J_URI=neo4j+s://your-neo4j-instance.io
REACT_APP_NEO4J_USER=neo4j
REACT_APP_NEO4J_PASSWORD=your-password
```

## Troubleshooting

### Common Issues

#### CORS Errors

If you encounter CORS errors when connecting to the API:

1. Ensure the API server has CORS configured to allow requests from your frontend origin
2. Check that your API requests include the proper headers
3. For local development, you may need to use a CORS proxy

#### Authentication Issues

If you experience authentication problems:

1. Verify your Auth0 configuration in the `.env.local` file
2. Check that your Auth0 application settings match your application URLs
3. Ensure the Auth0 audience matches the API identifier

#### API Connection Issues

If the application cannot connect to the API:

1. Verify the `REACT_APP_API_URL` is correct
2. Check that the API server is running and accessible
3. Ensure your network allows connections to the API endpoint

## Next Steps

After installation, you may want to:

1. Review the [[The Climb/Career Library/Project Documentation/TrustX/Frontend/Security-vulnerabilities|Security Vulnerabilities]] document to address any security concerns
2. Explore the [[The Climb/Career Library/Project Documentation/TrustX/Frontend/Architecture|Architecture]] documentation to understand the system design
3. Refer to the [[The Climb/Career Library/Project Documentation/TrustX/Frontend/Api-documentation|API Documentation]] for details on available endpoints


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/trustx/docs/installation-guide.md) · Samay + Trustx experience/TrustxRepos/trustx/docs/installation-guide.md

Project code and dependencies remain outside the vault. No source commands were executed.
