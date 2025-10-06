# Modules Directory

The `modules/` directory contains **reusable Infrastructure-as-Code (IaC)** components written in [OpenTofu](https://opentofu.org), designed to promote consistency, maintainability, and scalability across multiple environments and applications.

Each module encapsulates a specific piece of infrastructure — such as IAM roles, S3 buckets, VPCs, or databases — and defines its own inputs, outputs, and resources.  
Modules are versioned, documented, and can be composed together within environment definitions under the `envs/` directory.

