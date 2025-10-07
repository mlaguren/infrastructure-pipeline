# OpenTofu Infrastructure Setup

<p>This repository defines **Infrastructure-as-Code (IaC)** for provisioning and managing AWS resources using [OpenTofu](https://opentofu.org).  </p>
It establishes a **modular, reusable, and testable** foundation for cloud environments — from IAM roles to databases, networking, secrets management, etc.

---

## Overview

The repository is structured to support multiple environments (`dev`, `int`, `prod`) and promotes best practices in:
- **OpenTofu module design**  
- **Environment composition**  
- **GitHub Actions-based CI/CD**
- **Terratest validation**
- **Security scanning and linting**

---

## Repository Structure
```
├── modules/ # Reusable OpenTofu building blocks (IAM, S3, RDS, etc.)
│ └── README.md
├── envs/ # Environment compositions (dev, int, prod)
│ └── README.md
├── scripts/ # Helper scripts for local and CI/CD workflows
│ └── README.md
├── tests/ # Terratest unit tests for modules and environments
├── .github/workflows # CI/CD pipelines for linting, testing, and deployment
└── README.md # This file
```


---

## Getting Started

### Prerequisites

Make sure the following tools are installed:

| Tool | Purpose | Install Command |
|------|----------|----------------|
| [OpenTofu](https://opentofu.org/docs) | Infrastructure provisioning | `brew install opentofu` |
| [tflint](https://github.com/terraform-linters/tflint) | Linting OpenTofu code | `brew install tflint` |
| [tfsec](https://github.com/aquasecurity/tfsec) | Security scanning | `brew install tfsec` |
| [gotestsum](https://github.com/gotestyourself/gotestsum) | Test runner for Terratest | `brew install gotestsum` |

You’ll also need:
- An AWS account and profile configured in `~/.aws/credentials`
- (Optional) GitHub OIDC Role configured for CI/CD deployments

---
## Setting Up Github OIDC

See [OpenID-Connect Overview Page](https://github.com/mlaguren/infrastructure-pipeline/wiki/OpenID-Connect-(OIDC)-Overview)

