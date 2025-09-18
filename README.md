# Cloud Run CI/CD Pipeline

Automated deployment pipeline for Cloud Run application using Terraform.

## Setup

### GitHub Actions
1. Set repository secrets:
   - `GCP_PROJECT_ID`: Your GCP project ID
   - `GCP_SA_KEY`: Base64 encoded service account JSON key
   - `TF_STATE_BUCKET`: GCS bucket name for Terraform state

2. Trigger workflow:
   - Go to Actions → Deploy Cloud Run App → Run workflow
   - Choose action: `create` or `destroy`

### GitLab CI
1. Set CI/CD variables:
   - `GCP_PROJECT_ID`: Your GCP project ID
   - `GCP_SA_KEY`: Base64 encoded service account JSON key
   - `TF_STATE_BUCKET`: GCS bucket name for Terraform state
   - `ACTION`: Set to `create` or `destroy` when running pipeline

2. Run pipeline manually from GitLab UI

## Required GCP Permissions
Service account needs:
- Cloud Run Admin
- Storage Admin
- IAM Security Admin
- Service Account User

## Files Structure
```
├── terraform/
│   ├── main.tf                 # Terraform configuration
│   └── terraform.tfvars.example # Example variables
├── .github/workflows/
│   └── deploy.yml              # GitHub Actions workflow
├── .gitlab-ci.yml              # GitLab CI pipeline
└── README.md                   # This file
```