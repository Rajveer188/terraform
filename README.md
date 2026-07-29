# Terraform GCP GitHub Actions Hands-on

This example provisions a Google Cloud Storage bucket using Terraform and GitHub Actions.

## Flow

1. Open a PR
2. GitHub Actions runs:
   - terraform fmt
   - terraform validate
   - terraform plan
3. Review the plan
4. Approve and merge
5. GitHub Actions runs terraform apply
6. The GCP resource is updated

## Required GitHub Secrets

Set these repository secrets in GitHub:

- GCP_PROJECT_ID
- GCP_BUCKET_NAME
- GOOGLE_CREDENTIALS

## Local usage

```bash
terraform init
terraform validate
terraform plan -var="project_id=YOUR_PROJECT_ID" -var="bucket_name=YOUR_BUCKET_NAME"
terraform apply -var="project_id=YOUR_PROJECT_ID" -var="bucket_name=YOUR_BUCKET_NAME"
```
# terraform
