# Workflow Guidelines

This document provides detailed instructions and guidelines for developers working with the CI/CD pipeline in this PoC repository.

---

## Table of Contents

1. [Branch Strategy](#branch-strategy)
2. [Creating a Feature Branch](#creating-a-feature-branch)
3. [Pull Request Process](#pull-request-process)
4. [Code Review Requirements](#code-review-requirements)
5. [Deployment Workflows](#deployment-workflows)
6. [Environment Promotion](#environment-promotion)
7. [Release Management](#release-management)

---

## Branch Strategy

### Branch Structure

```
main (protected) ←─┐
                    │ Pull Requests only, requires approval
feature/issue-XXX  ├─→ Test Workflow runs on every commit
                    │
feature/issue-YYY   ├─→ Test Workflow runs on every commit
```

### Protected Branch Rules

**Main branch** (`main`) is protected with the following rules:

1. ✅ **Require a pull request before merging** - Never direct commits
2. ✅ **Require approval from at least one reviewer** - No auto-merge without review
3. ✅ **Require status checks to pass** - Tests must pass before merge
4. ✅ **Dismiss stale pull request approvals when new commits are pushed** - Always re-review

### Feature Branch Naming Convention

Use the following naming pattern:
```
feature/issue-{issue-number}
feature/issue-{issue-number}-{short-description}
```

**Examples:**
- `feature/issue-123`
- `feature/issue-456-user-authentication`
- `feature/issue-789-fix-login-bug`

**Never use:**
- ❌ `main` or `master` for development
- ❌ Personal branches without issue reference (`john-work`, etc.)
- ❌ Branches without a clear purpose

---

## Creating a Feature Branch

### Step 1: Create GitHub Issue

Before starting any work:

1. Open [GitHub Issues](<https://github.com/your-org/repo/issues>)
2. Create a new issue with:
   - **Title**: Clear description of the change
   - **Description**: What is being changed, why, and acceptance criteria
   - **Labels**: Appropriate labels (`bug`, `feature`, `enhancement`)

**Example Issue:**
```markdown
## Title
Fix login page loading timeout on high-latency networks

## Description
The login page times out when network latency exceeds 200ms. Need to implement retry logic with exponential backoff.

## Acceptance Criteria
- [ ] Login page retries up to 3 times on timeout
- [ ] Retry delay increases exponentially (1s, 2s, 4s)
- [ ] User sees a progress indicator during retry attempts
- [ ] Tests pass in CI/CD pipeline
```

### Step 2: Create Feature Branch

Create your feature branch from `main`:

```bash
# Switch to main branch
git checkout main

# Pull latest changes (ensure you're up to date)
git pull origin main

# Create feature branch
git checkout -b feature/issue-123-fix-login-timeout

# Commit initial state
git add .
git commit -m "chore: initial commit for issue-123"
git push origin feature/issue-123-fix-login-timeout
```

### Step 3: Make Changes and Commit

Develop your changes with clear, conventional commits:

```bash
# Example commit messages
git commit -m "feat: implement retry logic for login endpoint"
git commit -m "test: add unit tests for retry mechanism"
git commit -m "fix: handle edge case where user aborts retry"
```

**Commit message best practices:**
- Use conventional commits format (`feat:`, `fix:`, `chore:`, etc.)
- Reference the issue number in commits if applicable
- Keep messages concise but descriptive
- Don't include sensitive information

### Step 4: Test Workflow Runs

Every time you push to your feature branch, the **Test Workflow** runs automatically.

#### What the Test Workflow Does:

1. ✅ Checks out your code
2. ✅ Runs linting (ESLint, Prettier)
3. ✅ Runs unit tests
4. ✅ Runs integration tests
5. ✅ Builds the application
6. ✅ Uploads build artifacts to Azure Blob Storage
7. ✅ Reports results back to GitHub Actions

#### Interpreting Test Results:

**All Tests Pass ✅**
```
Job Summary: Success ✓
Build Artifacts uploaded successfully
Ready for pull request review
```

**Tests Fail ❌**
```
Job Summary: Failure ✗
Failed tests:
  - Unit test: retry-mechanism.spec.js
  - Integration test: login-flow.e2e.ts

Action Required: Fix failing tests before proceeding
```

---

## Pull Request Process

### Step 1: Submit Pull Request

Once tests pass, create a pull request from your feature branch to `main`:

```bash
# Create PR on GitHub web UI (recommended)
# or use CLI with gh command
gh pr create --title "Fix login timeout - issue-123" \
             --body "Addresses the login timeout issue..."
```

### Step 2: PR Template Requirements

Every pull request must include:

**Title:**
- Follows conventional commits format
- References issue number
- **Example**: `feat(login): implement retry logic for high-latency networks`

**Description Template:**
```markdown
## Description
Addresses the login timeout issue by implementing retry logic with exponential backoff.

## Changes
- Added retry mechanism to login service
- Implemented exponential backoff (1s, 2s, 4s)
- Added user progress indicator during retries
- Updated error handling

## Testing
- ✅ Unit tests pass
- ✅ Integration tests pass
- ✅ E2E tests pass
- Manually tested in dev environment: [link]

## Related Issues
Closes #123
```

### Step 3: PR Review Requirements

**Review Checklist:**

Reviewers should check:
- [ ] Code follows project conventions and style guidelines
- [ ] All tests pass (check status)
- [ ] Changes are minimal and focused on the issue
- [ ] Documentation is updated if needed
- [ ] No sensitive information exposed
- [ ] Pull request description is clear

**Approval Requirements:**
- ✅ At least one approved review required
- ⏳ Optional: Second review for critical changes
- ❌ No auto-approve without review

### Step 4: Review and Merge

**After Approval:**

1. Requestor clicks "Ready to review" if status checks pass
2. Approver leaves approval comment
3. Requestor merges the pull request (or designated merge admin does)

**Merge Options:**
- **Squash and Merge**: Recommended for clean history
- **Rebase and Merge**: Alternative option
- **Create a Merge Commit**: Less preferred for main branch

---

## Code Review Requirements

### Required Reviews

| Change Type | Reviewers Required | Timeframe |
|-------------|-------------------|-----------|
| Bug fixes | 1 reviewer | Immediate |
| Feature additions | 1+ reviewers | Within 24 hours |
| Security changes | 2 reviewers | Within 12 hours |
| Architecture changes | 2+ reviewers, tech lead | Within 24 hours |

### Reviewer Responsibilities

Reviewers must:
1. ✅ Verify code quality and standards compliance
2. ✅ Check for security vulnerabilities
3. ✅ Ensure tests cover new functionality
4. ✅ Validate that changes meet acceptance criteria
5. ✅ Provide clear feedback on required fixes

### Requester Responsibilities

Requestors should:
1. ✅ Wait for pending reviews before making more commits (squash merge)
2. ✅ Respond promptly to reviewer feedback
3. ✅ Make requested changes and push to feature branch
4. ✅ Test locally after implementing feedback
5. ✅ Re-request review when changes are complete

---

## Deployment Workflows

### Deploy Workflow Triggers

The **Deploy Workflow** runs in two scenarios:

1. **Automatic**: When a PR is approved, merged, and deployed to `main`
2. **Manual**: Triggered via GitHub Actions UI after deployment approval

### Pre-Deployment Checks

Before deployment, the workflow ensures:
- ✅ All status checks pass (tests)
- ✅ PR has at least one approval
- ✅ No conflicting merges on main branch
- ✅ Target environment is in maintenance window (if configured)

### Deployment Steps

1. **Download Artifacts**: Fetch build outputs from CI storage
2. **Run Production Tests**: Execute full test suite against staging environment
3. **Deploy to Azure**: Upload and deploy to target Azure App Service / Blob Storage
4. **Health Checks**: Verify service is running and responding correctly
5. **Smoke Tests**: Run basic functionality tests on deployed application
6. **Success Notification**: Send alert to deployment channel

### Deployment Statuses

**Successful Deployment ✅**
```
Deployment completed successfully ✓
Environment: prod.environment.app
Last deployed: 2026-09-09 14:32 UTC
Version: v1.2.3
```

**Failed Deployment ❌**
```
Deployment failed ✗
Error: Health check endpoint returned 503
Action: Automatic rollback initiated
Previous version restored: v1.2.2
```

---

## Environment Promotion

### Current PoC Scope (Dev → Prod)

This PoC demonstrates deployment from **dev to prod** directly. In production, the full flow would be:

```
Development (dev.environment.app) → QA (qa.environment.app) 
→ Pre-Production (pre-prod.environment.app) → Production (prod.environment.app)
```

### Environment-Specific Configurations

Each environment has its own configuration files:

| File | Purpose | Example Value |
|------|---------|---------------|
| `.env.development` | Development settings | `NODE_ENV=development` |
| `.env.qa` | QA testing settings | `NODE_ENV=qa` |
| `.env.preprod` | Pre-prod testing | `NODE_ENV=pre-production` |
| `.env.production` | Production settings | `NODE_ENV=production` |

### Environment Variables

```bash
# Development
AZURE_STATIC_WEB_APP_URL=https://dev.environment.app
AZURE_BLOB_CONTAINER=dev-content

# Production  
AZURE_STATIC_WEB_APP_URL=https://prod.environment.app
AZURE_BLOB_CONTAINER=prod-content
```

---

## Release Management

### Versioning Strategy

Use semantic versioning for releases:

```
MAJOR.MINOR.PATCH-RELEASE-BUILD
v1.0.0-beta.1+gabcdef123456789
```

**Examples:**
- `v1.0.0` - Stable release to production
- `v1.0.0-alpha.1` - Initial alpha build
- `v1.0.0-beta.1+gc123def456789` - Beta build with commit hash

### Release Checklist

Before releasing:

1. ✅ All tests pass in target environment
2. ✅ Smoke tests confirm basic functionality
3. ✅ Health checks return green
4. ✅ Monitoring shows no errors or anomalies
5. ✅ Deployment logs are reviewed
6. ✅ Stakeholders notified of deployment

### Rollback Procedure

If a deployment fails:

1. **Automatic Rollback** (if configured):
   - Previous version automatically restored
   - Deployment failure logged
   - Team notified

2. **Manual Rollback**:
   ```bash
   # Via Azure Portal / Kudu
   git checkout <previous-commit>
   az appservice deployment create \
     --name <app-name> \
     --source-url <git-url> \
     --branch main
   ```

---

## Emergency Procedures

### Hotfix Branching

For critical production issues:

1. Create hotfix branch from `main`:
   ```bash
   git checkout -b hotfix/issue-XXX-hotfix-name main
   ```

2. Follow same PR and review process

3. Deploy with highest priority approval

### Emergency Deployment

If automated workflow fails:

1. Contact release manager
2. Review deployment logs in Azure Monitor
3. Manually trigger rollback via Azure Portal
4. Investigate root cause
5. Update automation after investigation

---

## Best Practices Summary

### ✅ DOs

- Always create a GitHub issue before starting work
- Use feature branches with proper naming convention
- Commit frequently with clear messages
- Write tests alongside new code
- Request reviews from experienced team members
- Address all review feedback promptly
- Monitor deployment status and alerts
- Update documentation after making changes

### ❌ DON'Ts

- Never commit directly to `main`
- Never bypass required reviews or approvals
- Never deploy without checking test results
- Never ignore failing tests
- Never expose secrets in code or PR descriptions
- Never merge before acceptance criteria are met
- Never skip documentation updates

---

## Support and Resources

### Documentation

| Document | Purpose |
|----------|---------|
| [architecture-summary.md](<docs/architecture-summary.md>) | Azure infrastructure options |
| [assumptions.md](<docs/assumptions.md>) | Organizational and technical assumptions |
| This document | Workflow procedures and best practices |

### Getting Help

- **Technical Issues**: Check GitHub Actions logs, review error messages
- **Process Questions**: Refer to documentation or ask team lead
- **Emergency Deployments**: Contact release manager on-call

---

*Last updated: 2026-09-09*

**Note**: This PoC demonstrates the full workflow. Production implementations may add additional stages (QA, pre-prod) between development and production environments.