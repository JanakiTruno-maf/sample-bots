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
   - Choose action: `create`, `destroy`, or `plan-and-apply`
   
   **Actions:**
   - `create`: Build image and deploy new infrastructure
   - `destroy`: Remove all infrastructure
   - `plan-and-apply`: Check for changes, show diff, and apply if approved

### GitLab CI
1. Set CI/CD variables:
   - `GCP_PROJECT_ID`: Your GCP project ID
   - `GCP_SA_KEY`: Base64 encoded service account JSON key
   - `TF_STATE_BUCKET`: GCS bucket name for Terraform state
   - `ACTION`: Set to `create` or `destroy` when running pipeline

2. Run pipeline manually from GitLab UI
   
   **Actions:**
   - `create`: Build image and deploy new infrastructure  
   - `destroy`: Remove all infrastructure
   - `plan-and-apply`: Two-stage process with manual approval between plan and apply

## Required GCP Permissions
Service account needs:
- Cloud Run Admin
- Storage Admin
- IAM Security Admin
- Service Account User

## Workflow Types

### Plan and Apply (Recommended for Production)
1. **Plan Stage**: Runs `terraform plan -out=tfplan`
2. **Diff Check**: Automatically stops if no changes detected
3. **Manual Approval**: Requires approval before applying changes (GitHub/GitLab)
4. **Apply Stage**: Runs `terraform apply tfplan` if approved

### Create/Destroy (Direct Actions)
- **Create**: Builds image and applies infrastructure directly
- **Destroy**: Removes all infrastructure directly

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