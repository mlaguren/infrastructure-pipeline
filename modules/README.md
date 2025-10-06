# Modules Directory

The `modules/` directory contains **reusable Infrastructure-as-Code (IaC)** components written in [OpenTofu](https://opentofu.org), designed to promote consistency, maintainability, and scalability across multiple environments and applications.

Each module encapsulates a specific piece of infrastructure — such as IAM roles, S3 buckets, VPCs, or databases — and defines its own inputs, outputs, and resources.  
Modules are versioned, documented, and can be composed together within environment definitions under the `envs/` directory.

```
modules/
├── iam/ # IAM roles, policies, and OIDC trust relationships
```

Each subfolder represents a standalone OpenTofu module.  
Modules can be combined to build complete environments in the `envs/` directory (e.g., `envs/dev/main.tf`).

---

##  Module Design Principles

- **Reusable** — Encapsulates a single responsibility (e.g., IAM, S3, RDS).
- **Composable** — Can be integrated easily into multiple environments.
- **Configurable** — Uses `variables.tf` for all tunable parameters.
- **Tested** — Each module includes Terratest unit tests under `/tests`.
- **Validated** — Passes `tofu fmt`, `tflint`, and `tfsec` checks before deployment.

---

##  Usage Example

A typical environment (e.g., `envs/dev/main.tf`) can call a module like this:

```hcl
module "iam_developer_role" {
  source = "../../modules/iam"

  role_name     = "fabrion-developer"
  github_org    = "fabrionai"
  github_repos  = ["monorepo", "infra"]
  secrets_prefix = "fabrion/dev/"
}
```
Testing

Each module should include a matching test file under the tests/ directory using Terratest:

```tests/
└── iam_test.go
```

You can run all module tests with:

```bash
gotestsum --format testname -- -v -timeout 30m ./tests
```
# Best Practices

* Always include README.md, variables.tf, outputs.tf, and main.tf in each module.
* Avoid hardcoding values; expose configuration through variables.
* Keep outputs minimal and meaningful.
* Run tofu fmt, tflint, and tfsec locally before committing changes.
* Use semantic versioning when tagging modules for reuse across repositories.

# References

OpenTofu Documentation

AWS Provider Docs

Terratest Framework

TFLint Ruleset

Purpose:

The modules/ folder serves as the building blocks for your infrastructure.
Every environment — whether development, integration, or production — should compose from these modules for consistency and ease of maintenance.
