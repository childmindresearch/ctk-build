# CTK-Build Repository

This repository contains a GitHub Actions workflow for building, testing, and deploying components of the Clinician Toolkit (CTK) project.

## Overview

The workflow is triggered when a dependency is updated through `repository_dispatch`. These dependencies are: 1) [CTK-Functions](https://github.com/childmindresearch/ctk-functions), 2) [CTK-Webapp](https://github.com/childmindresearch/ctk-webapp), and 3) [cloai-service](https://github.com/childmindresearch/cloai-service).

## Workflow Stages

### 1. Build
- Checks out the repository that triggered the workflow
- Builds and pushes Docker images to Azure Container Registry (ACR)
- Tags images with both `latest` and SHA-specific tags

### 2. E2E Testing
- Runs end-to-end tests using the following services:
  - API (CTK Functions)
  - CLOAI Service
  - LanguageTool
  - PostgreSQL
- Executes integration tests using Playwright
- Records test results and uploads video artifacts

### 3. Deploy
- Deploys the latest versions of services to Azure Container Apps
