# Environments Directory

<p>The `envs/` directory contains **environment-specific infrastructure definitions** that compose one or more reusable modules from the [`modules/`](../modules) folder.  </p>
<p>Each environment (e.g., `dev`, `int`, `prod`) defines how the infrastructure should be instantiated for that stage of the deployment lifecycle.</p>

---

## Structure

```
envs/
├── dev/
│ ├── main.tf # Environment composition file importing modules
│ ├── variables.tf # Environment-specific variable definitions
│ ├── terraform.tfvars # Variable values for this environment
│ ├── outputs.tf # Outputs for referencing in CI/CD or other stacks
│ └── README.md # Optional environment-specific notes
├── int/
│ └── ...
├── prod/
│ └── ...
└── README.md
```

Each subfolder under `envs/` represents a **fully deployable environment**, typically linked to a GitHub environment or AWS account.

---

## Purpose

<p>The purpose of this folder is to define how **individual modules** come together to form a complete environment.  </p>
<p>For example, your `dev` environment might include IAM roles, Secrets Manager access, and a Postgres database, while `prod` includes the same modules with stricter permissions and different variable values.</p>

## Workflow

| Command            | Description                                             |
|---------------------|---------------------------------------------------------|
| tofu init           | Initialize the working directory and provider plugins   |
| tofu fmt -recursive | Format all configuration files                          |
| tofu plan           | Preview the infrastructure changes for this environment |
| tofu apply          | Deploy resources                                        |
| tofu destroy        | Tear down environment resources when no longer needed   |

## Testing Environments

Each environment should be tested using Terratest, focusing on validating key outputs such as IAM role creation, Secrets Manager access, or RDS connectivity.

For example:
```bash
gotestsum -- -run TestIamDeveloperRole -v -timeout 30m ./tests
```

## Best Practices

* Maintain consistent folder naming (dev, int, prod) across repositories.
* Do not hardcode credentials — use OpenTofu variables or GitHub OIDC for authentication.
* Run tofu validate, tflint, and tfsec checks before applying.
* Treat each environment as immutable — changes should flow from dev → int → prod through pull requests.
* Keep all environment secrets in a Secrets Manager, never committed to source control.