# tictactoe Bootstrap

This repository contains the bootstrap configuration for tictactoe project, setting up GitHub OIDC authentication with AWS.

## Prerequisites

- AWS CLI configured
- Terraform installed

## Setup

1. Initialize Terraform:
```bash
cd terraform
terraform init
```

2. Apply the configuration:
```bash
terraform apply
```

3. Note the role ARN from the output:
```bash
terraform output github_actions_role_arn
```

4. Use this role ARN in your GitHub Actions workflows:
```yaml
jobs:
  deploy:
    permissions:
      id-token: write
      contents: read
    steps:
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          role-to-assume: <role_arn_from_output>
          aws-region: us-east-1
```

## Resources Created

- GitHub OIDC Provider
- IAM Role for GitHub Actions with necessary permissions
