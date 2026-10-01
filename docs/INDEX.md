# Documentation Index

Welcome to the dtap-automation PoC documentation. Use this index to navigate all available documentation.

---

## Quick Navigation

### For Developers Starting Today

| Document | Purpose | Read Time |
|----------|---------|-----------|
| [onboarding.md](<docs/onboarding.md>) | Get started in 5 minutes | 10 min read |
| [README.md](<../README.md>) | PoC overview and branch strategy | 5 min read |
| [assumptions.md](<docs/assumptions.md>) | Organizational context | 10 min read |

### For Understanding Workflows

| Document | Purpose | Read Time |
|----------|---------|-----------|
| [workflow-guidelines.md](<docs/workflow-guidelines.md>) | CI/CD procedures and rules | 15 min read |
| [visual-workflows.md](<docs/visual-workflows.md>) | Diagrams of all workflows | Visual reference |

### For Architecture Decisions

| Document | Purpose | Read Time |
|----------|---------|-----------|
| [architecture-summary.md](<docs/architecture-summary.md>) | Azure deployment options | 15 min read |
| [deployment-guidelines.md](<docs/deployment-guidelines.md>) | Deployment configuration | 20 min read |

### For Release Management

| Document | Purpose | Read Time |
|----------|---------|-----------|
| CHANGELOG.md | Version history and release notes | 5 min read |
| deployment-guidelines.md | Production release procedures | Refer as needed |

---

## Documentation by Category

### 📚 Core Documentation (Required Reading)

1. **[README.md](<../README.md>)**
   - PoC objectives and goals
   - Branch strategy overview
   - Quick start guide
   - Links to all other docs

2. **[docs/assumptions.md](<docs/assumptions.md>)**
   - Organizational structure
   - Technical stack assumptions
   - Process assumptions
   - Security considerations

3. **[docs/architecture-summary.md](<docs/architecture-summary.md>)**
   - Azure Blob Storage + Front Door option
   - Azure App Service option
   - Cost analysis and comparison
   - Pros/cons for each approach

### 🔄 Workflow Documentation (All Contributors)

4. **[docs/workflow-guidelines.md](<docs/workflow-guidelines.md>)**
   - Branch strategy rules
   - Feature branch creation
   - Pull request process
   - Code review requirements
   - Deployment workflows
   - Release management procedures

5. **[docs/visual-workflows.md](<docs/visual-workflows.md>)**
   - Complete branch strategy diagram
   - Pull request review workflow
   - Deployment pipeline architecture
   - Security & access control flow
   - Environment transition sequence
   - Quick reference decision tree

### 🚀 Deployment Documentation (Deployment Engineers)

6. **[docs/deployment-guidelines.md](<docs/deployment-guidelines.md>)**
   - Azure infrastructure setup
   - ARM/Bicep template examples
   - Environment-specific configurations
   - Health check procedures
   - Rollback procedures
   - Troubleshooting guide

### 🎯 Onboarding Documentation (New Contributors)

7. **[docs/onboarding.md](<docs/onboarding.md>)**
   - Quick start (5-minute setup)
   - First contribution walkthrough
   - Best practices checklist
   - Getting help resources

8. **[CHANGELOG.md](<../CHANGELOG.md>)**
   - Version history
   - Release notes
   - What's new in each release

---

## Documentation by Role

### Developer Roles

| Task | Primary Document | Reference Documents |
|------|------------------|--------------------|
| Creating new feature | [onboarding.md](<docs/onboarding.md>) → [workflow-guidelines.md](<docs/workflow-guidelines.md>) | [visual-workflows.md](<docs/visual-workflows.md>) |
| Writing tests | [workflow-guidelines.md](<docs/workflow-guidelines.md>) | README.md |
| Code review | [workflow-guidelines.md](<docs/workflow-guidelines.md>) | CHANGELOG.md |
| Creating PRs | [onboarding.md](<docs/onboarding.md>) → [workflow-guidelines.md](<docs/workflow-guidelines.md>) | README.md |

### DevOps/Release Engineering Roles

| Task | Primary Document | Reference Documents |
|------|------------------|--------------------|
| Deploying to production | [deployment-guidelines.md](<docs/deployment-guidelines.md>) | [architecture-summary.md](<docs/architecture-summary.md>) |
| Managing CI/CD pipelines | [workflow-guidelines.md](<docs/workflow-guidelines.md>) | CHANGELOG.md |
| Rollback procedures | [deployment-guidelines.md](<docs/deployment-guidelines.md>) | [visual-workflows.md](<docs/visual-workflows.md>) |

### Architecture/Design Roles

| Task | Primary Document | Reference Documents |
|------|------------------|--------------------|
| Selecting deployment architecture | [architecture-summary.md](<docs/architecture-summary.md>) | README.md |
| Cost analysis | [architecture-summary.md](<docs/architecture-summary.md>) | assumptions.md |
| Infrastructure planning | [deployment-guidelines.md](<docs/deployment-guidelines.md>) | [assumptions.md](<docs/assumptions.md>) |

---

## Documentation by Topic

### Branch Strategy

1. **[README.md](<../README.md>)** - Overview with visual diagram
2. **[docs/workflow-guidelines.md]** - Detailed rules and procedures
3. **[docs/visual-workflows.md]** - Complete workflow diagrams
4. **CHANGELOG.md** - Version history of branch strategy changes

### CI/CD Pipelines

1. **[docs/workflow-guidelines.md]** - Test and deploy workflows
2. **[docs/deployment-guidelines.md]** - Pipeline configuration details
3. **[docs/visual-workflows.md]** - Deployment pipeline architecture diagram
4. **deployment-guidelines.md** - Automation scripts and configurations

### Azure Infrastructure

1. **[docs/architecture-summary.md]** - Architecture alternatives
2. **[docs/deployment-guidelines.md]** - Setup instructions
3. **[docs/assumptions.md]** - Technical assumptions
4. **[docs/visual-workflows.md]** - Security & access control diagram

### Quality Gates & Testing

1. **[docs/workflow-guidelines.md]** - Test workflow behavior
2. **[docs/deployment-guidelines.md]** - Health check configurations
3. **[README.md]** - Branch strategy overview

### Security

1. **[docs/assumptions.md]** - Security assumptions
2. **[docs/deployment-guidelines.md]** - Secrets management
3. **[docs/visual-workflows.md]** - Access control diagram
4. **[docs/workflow-guidelines.md]** - Security guidelines

---

## Learning Path

### Path 1: Quick Start (1 Hour)

```
1. README.md (5 min)
   ↓
2. docs/onboarding.md (15 min)
   ↓
3. docs/assumptions.md (10 min)
   ↓
4. docs/architecture-summary.md (15 min)
   ↓
5. docs/workflow-guidelines.md (20 min)
```

**Outcome:** Ready to make your first contribution!

---

### Path 2: Deep Dive (3-4 Hours)

```
1. README.md (5 min)
   ↓
2. docs/assumptions.md (10 min)
   ↓
3. docs/architecture-summary.md (15 min)
   ↓
4. docs/workflow-guidelines.md (20 min)
   ↓
5. docs/deployment-guidelines.md (20 min)
   ↓
6. docs/visual-workflows.md (review all diagrams - 30 min)
   ↓
7. CHANGELOG.md (5 min)
   ↓
8. docs/onboarding.md (15 min)
```

**Outcome:** Complete understanding of the PoC!

---

### Path 3: Role-Specific Deep Dives

#### For Developers

```
1. README.md
   ↓
2. docs/workflow-guidelines.md (focus on workflows)
   ↓
3. docs/onboarding.md
   ↓
4. docs/visual-workflows.md (review diagrams)
```

#### For DevOps Engineers

```
1. README.md
   ↓
2. docs/architecture-summary.md
   ↓
3. docs/deployment-guidelines.md
   ↓
4. docs/workflow-guidelines.md (focus on deployment workflows)
   ↓
5. docs/visual-workflows.md (review architecture diagram)
```

#### For Architects

```
1. docs/architecture-summary.md
   ↓
2. docs/deployment-guidelines.md
   ↓
3. docs/assumptions.md
   ↓
4. CHANGELOG.md (for history of architectural decisions)
```

---

## Search Keywords

| Keyword | Documents to Check |
|---------|-------------------|
| branch, pull request, merge | README.md, workflow-guidelines.md, visual-workflows.md |
| deploy, CI/CD, pipeline | workflow-guidelines.md, deployment-guidelines.md |
| Azure, infrastructure, architecture | architecture-summary.md, deployment-guidelines.md, visual-workflows.md |
| tests, quality gates, linting | workflow-guidelines.md, deployment-guidelines.md |
| secrets, security, authentication | assumptions.md, deployment-guidelines.md, visual-workflows.md |
| rollback, recovery | deployment-guidelines.md, visual-workflows.md |
| cost, pricing | architecture-summary.md |
| environments, staging, production | deployment-guidelines.md, assumptions.md |

---

## Document Status

| Document | Last Updated | Status |
|----------|--------------|--------|
| README.md | 2026-09-09 | ✅ Active |
| docs/architecture-summary.md | 2026-09-09 | ✅ Active |
| docs/assumptions.md | 2026-09-09 | ✅ Active |
| docs/workflow-guidelines.md | 2026-09-09 | ✅ Active |
| docs/visual-workflows.md | 2026-09-09 | ✅ Active |
| docs/deployment-guidelines.md | 2026-09-09 | ✅ Active |
| CHANGELOG.md | 2026-09-09 | ✅ Active |
| docs/onboarding.md | 2026-09-09 | ✅ Active |
| docs/INDEX.md | 2026-09-09 | ✅ This Document |

---

## Contributing to Documentation

### When to Update Documentation

Add or update documentation when:

- [ ] New feature or workflow added
- [ ] Architecture decisions change
- [ ] Configuration options change
- [ ] Process rules change
- [ ] Bug fixes affect workflow

### How to Update Documentation

1. Create issue documenting the change needed
2. Make changes in relevant document
3. Pull request for review
4. Update CHANGELOG.md if appropriate
5. Merge and deploy

---

## Getting Additional Help

### Within Documentation

- Check [onboarding.md](<docs/onboarding.md>) for "Getting Help" section
- Review troubleshooting sections in deployment-guidelines.md
- Look for links to external resources throughout docs

### Outside Documentation

- GitHub Issues: Report bugs, request features
- PRs: Request clarification on documentation
- Direct communication: Contact team leads or owners

---

## Document Templates

See these templates for creating new documentation:

1. **README.md** - Project overview template (already created)
2. **ARCHITECTURE.md** - Infrastructure design template
3. **CHANGELOG.md** - Release notes template (already created)
4. **CONTRIBUTING.md** - Contribution guidelines template

---

## External Resources

| Resource | URL | Purpose |
|----------|-----|---------|
| GitHub Actions Documentation | https://docs.github.com/actions | CI/CD workflows |
| Azure Static Web Apps | https://learn.microsoft.com/en-us/azure/static-web-apps | Alternative deployment option |
| Azure App Service | https://learn.microsoft.com/en-us/azure/app-service/ | App hosting details |
| Keep a Changelog | https://keepachangelog.com | Version documentation standard |

---

*Last updated: 2026-09-09*

**For the latest version, always check CHANGELOG.md for release notes.**