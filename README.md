# Github-actions2
CI/CD Multi-Environment Pipeline (GitHub Actions)

This task implements a CI/CD pipeline using GitHub Actions with separate staging and production environments, including a manual approval gate before production deployment.

Workflow Summary

The pipeline follows this flow:

Code Push / Pull Request
        ↓
Build & Test
        ↓
Deploy to Staging Environment
        ↓
Run Smoke Tests
        ↓
Manual Approval (GitHub Environment Protection)
        ↓
Deploy to Production Environment


Staging Deployment:

Trigger
Automatically triggered on every push or pull request to the repository
What happens
Code is built and tested
Application is deployed to staging environment
Smoke tests are executed to verify deployment health
Secret Used
STAGING_KEY
Purpose
Used for testing and validation before production release

Production Deployment:
Trigger
Triggered only after:
Successful staging deployment
Manual approval from GitHub Environment protection rules
What happens
Final deployment is executed to production environment
Uses production-specific configuration
Secret Used
PROD_KEY
Purpose
Live environment for end users
GitHub Secrets Configuration

Two separate secrets are configured for secure deployment:

STAGING_KEY → used in staging environment
PROD_KEY → used in production environment

Secrets are stored securely in:

GitHub Repository → Settings → Secrets and variables → Actions
Approval Gate (Production Protection)

Production deployment is protected using GitHub Environments:

Manual approval is required before production job runs
Prevents accidental or unverified deployments

Configured at:

Settings → Environments → production → Required reviewers
Testing the Pipeline
Step-by-step flow tested:
Code pushed to repository
GitHub Actions triggered automatically
Staging deployment executed
Smoke tests verified staging environment
Manual approval triggered for production
Production deployment executed successfully after approval