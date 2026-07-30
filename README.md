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

## Required GitHub Variables

Set these GitHub Actions variables in the repository or in an environment such as dev/qa/prod:

- GCP_PROJECT_ID
- GCP_BUCKET_NAME
- GCP_WORKLOAD_IDENTITY_PROVIDER
- GCP_SERVICE_ACCOUNT

The workflow uses the job-level environment name `dev`. Change it to `qa` or `prod` if you want separate environments.

## How WIF authentication works

GitHub Actions authenticates to GCP through Workload Identity Federation (WIF). The workflow uses the GitHub OIDC token and exchanges it with Google for short-lived credentials tied to a GCP service account. Terraform then uses those credentials through the Google provider without storing a JSON key in GitHub.

## GCP setup for WIF

1. Create a Workload Identity Pool in GCP IAM.
2. Create a Workload Identity Provider for GitHub Actions.
3. Create a service account in GCP.
4. Grant that service account the IAM role needed for Terraform, for example `roles/storage.admin`.
5. Add the GitHub repository or environment principal set to the service account binding.
6. Add the provider and service account values as GitHub Actions variables.

## Local usage

```bash
terraform init
terraform validate
terraform plan -var="project_id=YOUR_PROJECT_ID" -var="bucket_name=YOUR_BUCKET_NAME"
terraform apply -var="project_id=YOUR_PROJECT_ID" -var="bucket_name=YOUR_BUCKET_NAME"
```
# terraform
