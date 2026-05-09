# AWS Static Site with CloudFront + GitHub Actions + OIDC

## Project Overview

This project hosts a static website in AWS using:

- Amazon S3
- Amazon CloudFront
- GitHub Actions CI/CD
- IAM OIDC role assumption

The site automatically deploys when code is pushed to GitHub.

---

## Architecture

Developer
↓
GitHub Repository
↓
GitHub Actions
↓
OIDC Role Assumption
↓
AWS STS Temporary Credentials
↓
S3 Static Site Bucket
↓
CloudFront CDN
↓
Users

---

## AWS Services Used

### S3
Used to store website files.

### CloudFront
Used as CDN and HTTPS frontend.

### IAM
Used for permissions and role assumption.

### STS
Used to issue temporary credentials during OIDC authentication.

---

## GitHub Actions Workflow

The deployment workflow:

1. Runs when code is pushed to `main`
2. GitHub Actions runner starts
3. GitHub assumes AWS IAM role using OIDC
4. Files sync to S3
5. CloudFront cache invalidation runs

---

## Security Concepts Learned

- Private S3 buckets
- CloudFront OAC
- IAM roles
- OIDC federation
- Temporary credentials
- Least privilege access
- CI/CD authentication

---

## Files

### index.html
Frontend website file.

### .github/workflows/main.yml
GitHub Actions deployment workflow.

---

## Lessons Learned

- CloudFront caches content globally
- Cache invalidation forces fresh content
- GitHub Actions runners are temporary Linux VMs
- IAM roles are assumed temporarily
- OIDC replaces long-term AWS keys
- AWS services communicate mostly through APIs
