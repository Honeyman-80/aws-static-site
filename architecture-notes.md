# Architecture Notes

## CloudFront + S3

CloudFront acts as the public frontend CDN.

S3 remains private.

Users do NOT access S3 directly.

CloudFront accesses S3 using OAC (Origin Access Control).

---

## OAC

OAC allows CloudFront to securely access the S3 bucket.

Bucket policy allows:

- CloudFront service
- specific CloudFront distribution ARN

This prevents public S3 access.

---

## Cache Invalidation

CloudFront caches files globally.

Updating S3 does not always instantly update users.

Invalidations force CloudFront to fetch fresh files.

Example invalidation paths:

/index.html
/*
/images/*

---

## GitHub Actions

GitHub Actions creates temporary Linux runner VMs.

Workflow steps execute inside the runner.

The runner:
- downloads repo
- authenticates to AWS
- uploads files
- invalidates CloudFront

---

## IAM User (Old Method)

Originally deployment used:

- IAM user
- access keys stored in GitHub secrets

GitHub authenticated directly using long-term credentials.

This worked but was less secure.

---

## OIDC + IAM Role (New Method)

GitHub now uses OIDC federation.

GitHub requests temporary identity token.

AWS trusts GitHub identity provider.

AWS STS issues temporary credentials.

GitHub temporarily assumes IAM role.

No long-term AWS keys required.

---

## Important Mental Models

### Identity Provider
Trusted external identity source.

### IAM Role
Temporary assumable permissions set.

### STS
Issues temporary credentials.

### GitHub Actions Runner
Temporary VM that executes workflow.

### AWS CLI
Tool that makes AWS API calls.

---

## Important Realization

Most cloud systems communicate through:
- API calls
- IAM permissions
- temporary credentials
- automation workflows
