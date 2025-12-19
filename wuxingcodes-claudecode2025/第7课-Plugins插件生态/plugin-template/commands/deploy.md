---
description: Deploy application to specified environment
argument-hint: [environment] [version]
---

# /deploy

## Purpose
Deploy the application to the specified environment with proper validation and rollback capability.

## Contract
**Inputs:**
- `$1` — ENVIRONMENT (staging|production) - Target deployment environment
- `$2` — VERSION (optional, string) - Specific version to deploy

**Outputs:**
- STATUS=<SUCCESS|FAILED>
- URL=<deployment-url>
- VERSION=<deployed-version>
- TIMESTAMP=<deployment-time>

## Instructions
1. Validate environment parameter (must be staging or production)
2. If no version specified, use latest stable version
3. Run pre-deployment checks:
   - Ensure all tests pass
   - Verify build is successful
   - Check environment readiness
4. Execute deployment script based on environment
5. Run post-deployment verification
6. Return deployment status and URL

## Pre-deployment Checklist
- [ ] All tests passing
- [ ] Build successful
- [ ] Database migrations applied (if needed)
- [ ] Environment variables configured
- [ ] SSL certificates valid (for production)

## Environment-specific Settings
- **staging**: Uses staging database and APIs
- **production**: Uses production resources with zero-downtime deployment

## Examples
- `/deploy staging` → Deploy latest version to staging
- `/deploy production v1.2.0` → Deploy specific version to production