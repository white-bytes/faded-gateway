# CI/CD Pipeline Documentation

This directory contains GitHub Actions workflows for the faded-gateway project.

## Workflows

### 1. CI Workflow (`ci.yml`)
**Triggers:** Push and Pull Requests to `main` and `develop` branches

**Purpose:** Continuous Integration testing across multiple Node.js versions

**Steps:**
- Checks out the repository
- Sets up Node.js (versions 18.x and 20.x)
- Caches yarn dependencies for faster builds
- Installs dependencies with frozen lockfile
- Builds the project
- Uploads build artifacts (Node 20.x only)

### 2. Deploy Workflow (`deploy.yml`)
**Triggers:** Push to `main` branch or manual workflow dispatch

**Purpose:** Automated deployment to GitHub Pages

**Steps:**
- Builds the project
- Configures GitHub Pages
- Uploads the build artifact
- Deploys to GitHub Pages

**Requirements:**
- GitHub Pages must be enabled in repository settings
- GitHub Pages source should be set to "GitHub Actions"

### 3. PR Checks Workflow (`pr-checks.yml`)
**Triggers:** Pull request events (opened, synchronized, reopened)

**Purpose:** Validates pull requests before merging

**Steps:**
- Checks out the repository
- Sets up Node.js 20
- Installs dependencies
- Builds the project
- Verifies build output exists

### 4. CodeQL Security Scanning (`codeql.yml`)
**Triggers:** Push/PR to `main`/`develop`, Weekly schedule (Monday 00:00 UTC)

**Purpose:** Automated security vulnerability scanning

**Steps:**
- Scans JavaScript/TypeScript code for security vulnerabilities
- Reports findings in the Security tab
- Runs weekly to catch newly discovered vulnerabilities

### 5. Dependency Review (`dependency-review.yml`)
**Triggers:** Pull requests to `main` branch

**Purpose:** Reviews dependency changes for known vulnerabilities

**Steps:**
- Checks new/updated dependencies against GitHub Advisory Database
- Fails on moderate or higher severity vulnerabilities
- Helps prevent introducing vulnerable dependencies

## Setup Instructions

### For GitHub Pages Deployment

1. Go to your repository Settings
2. Navigate to Pages section (under "Code and automation")
3. Set Source to "GitHub Actions"
4. The deploy workflow will automatically deploy on pushes to `main`

### For CodeQL Analysis

CodeQL is automatically configured and will start running on the next push or PR. Results will appear in the Security tab under "Code scanning alerts".

### Branch Protection (Recommended)

Consider setting up branch protection rules for `main`:

1. Go to Settings → Branches → Add rule
2. Branch name pattern: `main`
3. Enable:
   - Require a pull request before merging
   - Require status checks to pass before merging
   - Select status checks: `build`, `validate`
   - Require branches to be up to date before merging

## Workflow Status Badges

Add these to your README.md to display workflow status:

```markdown
[![CI](https://github.com/white-bytes/faded-gateway/actions/workflows/ci.yml/badge.svg)](https://github.com/white-bytes/faded-gateway/actions/workflows/ci.yml)
[![Deploy](https://github.com/white-bytes/faded-gateway/actions/workflows/deploy.yml/badge.svg)](https://github.com/white-bytes/faded-gateway/actions/workflows/deploy.yml)
[![CodeQL](https://github.com/white-bytes/faded-gateway/actions/workflows/codeql.yml/badge.svg)](https://github.com/white-bytes/faded-gateway/actions/workflows/codeql.yml)
```

## Troubleshooting

### Build Failures
- Check that all dependencies are properly listed in `package.json`
- Verify `yarn.lock` is committed to the repository
- Review build logs in the Actions tab

### Deployment Issues
- Ensure GitHub Pages is enabled in repository settings
- Verify the workflow has necessary permissions (pages: write)
- Check that the build produces output in the `dist/` directory

### Security Alerts
- Review CodeQL findings in the Security tab
- Address high-severity issues promptly
- False positives can be dismissed with explanation

## Maintenance

- Workflows use latest GitHub Actions (v4 for checkout/setup-node, v3 for CodeQL)
- Update action versions periodically for security and features
- Review and update Node.js versions in matrix as needed
