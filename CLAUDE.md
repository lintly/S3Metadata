# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a proof-of-concept (POC) repository for managing S3 metadata using Terraform. The project focuses on demonstrating approaches to handling S3 object metadata and bucket configurations through infrastructure-as-code.

## Commands

### Terraform Workflow

```bash
# Initialize Terraform (downloads providers and modules)
terraform init

# Validate configuration syntax
terraform validate

# Format Terraform files
terraform fmt -recursive

# Plan changes (see what will be created/modified)
terraform plan

# Apply changes
terraform apply

# Destroy infrastructure
terraform destroy

# Show current state
terraform show
```

### Working with Terraform State

```bash
# List resources in state
terraform state list

# Show specific resource details
terraform state show <resource_address>

# Import existing S3 resources
terraform import aws_s3_bucket.example bucket-name
```

## Architecture Notes

This is a POC repository for exploring S3 metadata management patterns. Key considerations when developing in this codebase:

- **State Management**: Terraform state may contain sensitive metadata about S3 objects. Consider using remote state backends (e.g., S3 + DynamoDB) for collaboration.

- **S3 Metadata Patterns**: S3 supports both system metadata (Content-Type, Cache-Control, etc.) and custom user-defined metadata (x-amz-meta-* headers). Terraform's `aws_s3_object` resource handles both types.

- **Bucket vs Object Metadata**: Distinguish between bucket-level metadata (tags, policies, versioning settings) and object-level metadata (individual file metadata, tags, storage class).

## Terraform Best Practices for This Project

- Use variables for environment-specific values (bucket names, regions, metadata values)
- Organize resources by functionality (buckets, objects, policies, lifecycle rules)
- Use Terraform workspaces or separate state files for different environments
- Tag all resources consistently for cost tracking and organization
