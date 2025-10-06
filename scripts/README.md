# Scripts Directory

The `scripts/` directory contains **utility shell scripts** used to manage and maintain the OpenTofu infrastructure locally and in CI/CD workflows.  
These scripts ensure consistency between **local development** and **GitHub Actions** runs by providing common commands for linting, testing, planning, and deploying environments.

---

## Purpose

While GitHub Actions automates most workflows, these scripts allow developers to:
- Run the same validation and deployment commands locally before committing changes.
- Test new environments without manually typing long `tofu` commands.
- Ensure consistent behavior between local CLI and CI/CD pipelines.

---
