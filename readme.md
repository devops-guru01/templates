# Flexible EKS Deployment GitHub Actions Workflow

This repository contains a flexible GitHub Actions workflow for deploying applications to Amazon EKS (Elastic Kubernetes Service). The workflow automates the process of building a Docker image, pushing it to Amazon ECR (Elastic Container Registry), and deploying it to an EKS cluster.

## Features

- Configurable deployment branch
- Customizable AWS region, ECR repository, and EKS cluster name
- Secure handling of AWS credentials
- Flexible image tagging
- Customizable kubectl version
- Adaptable deployment step

## Prerequisites

Before using this workflow, ensure you have the following:

1. An AWS account with appropriate permissions for ECR and EKS
2. An EKS cluster set up in your AWS account
3. An ECR repository created in your AWS account
4. AWS CLI configured with the necessary credentials
5. kubectl installed and configured to interact with your EKS cluster

## Setup

1. Copy the workflow YAML file to your repository's `.github/workflows/` directory.
2. Set up the following secrets in your GitHub repository settings:
   - `AWS_ACCESS_KEY_ID`: Your AWS access key ID
   - `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key

3. Customize the workflow by setting the following variables in your GitHub repository settings or directly in the workflow file:
   - `DEPLOY_BRANCH` (default: 'main'): The branch that triggers the deployment
   - `AWS_REGION` (default: 'us-west-2'): Your AWS region
   - `ECR_REPOSITORY` (default: 'my-app'): Your ECR repository name
   - `SERVICE_NAME` (default: 'MyService'): Your service name
   - `EKS_CLUSTER_NAME` (default: 'my-cluster'): Your EKS cluster name
   - `ENVIRONMENT` (default: 'production'): The deployment environment
   - `KUBECTL_VERSION` (default: 'latest'): The kubectl version to use

## Usage

Once set up, the workflow will automatically run when you push to the specified deployment branch. You can also manually trigger the workflow from the "Actions" tab in your GitHub repository.

## Customization

### Deployment Command

Replace the placeholder deployment command in the "Deploy to EKS" step with your actual deployment logic. For example:

```yaml
- name: Deploy to EKS
  env:
    ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
    IMAGE_TAG: ${{ env.SERVICE_NAME }}-${{ github.sha }}
  run: |
    kubectl set image deployment/${{ env.SERVICE_NAME }} ${{ env.SERVICE_NAME }}=$ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
```

### Additional Steps

You can add more steps to the workflow as needed, such as running tests, performing database migrations, or notifying external services.

## Troubleshooting

If you encounter issues with the workflow:

1. Check the workflow run logs in the GitHub Actions tab of your repository.
2. Ensure all required secrets and variables are correctly set.
3. Verify that your AWS credentials have the necessary permissions.
4. Check that your EKS cluster and ECR repository are correctly configured and accessible.

## Contributing

Contributions to improve the workflow are welcome. Please feel free to submit issues or pull requests.

## License

This workflow is available under the [MIT License](LICENSE).
