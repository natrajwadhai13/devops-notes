---
title: "• Terraform"
nav_order: 1
parent: "6. Cloud Automation Tools"
has_children: true
---

## Terraform Syllabus — DevOps / Cloud Automation

### Module 1: Terraform Fundamentals

- What is Terraform?
- Why Infrastructure as Code (IaC)?
- Terraform vs Ansible
- Terraform vs CloudFormation
- Terraform architecture
- Terraform workflow
- Declarative vs imperative approach
- Terraform use cases
- Terraform limitations

### Module 2: Installation & Setup

- Terraform installation
- Terraform CLI
- Terraform version
- Terraform upgrade/downgrade
- VS Code Terraform extension
- Terraform documentation
- First Terraform project

Important commands:

```bash
terraform version
terraform init
terraform validate
terraform fmt
terraform plan
terraform apply
terraform destroy
```

---

### Module 3: Terraform Configuration Language (HCL)

- HCL syntax
- Blocks
- Arguments
- Attributes
- Comments
- Strings
- Numbers
- Booleans
- Lists
- Maps
- Sets
- Objects
- Tuples

Example:

```hcl
resource "aws_instance" "web" {
  ami           = "ami-xxxxxxxx"
  instance_type = "t2.micro"
}
```

---

### Module 4: Providers

- What is a provider?
- Provider configuration
- AWS provider
- Azure provider
- GCP provider
- Provider version
- Provider aliases
- Multiple providers

Example:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}
```

---

### Module 5: Resources

- What is a resource?
- Resource syntax
- Resource arguments
- Resource attributes
- Resource dependencies
- Implicit dependency
- Explicit dependency using `depends_on`
- Resource lifecycle

Example:

```hcl
resource "aws_s3_bucket" "app" {
  bucket = "my-app-bucket"
}
```

---

### Module 6: Data Sources

- What is a data source?
- Resource vs data source
- Fetching existing infrastructure
- AWS AMI lookup
- Existing VPC lookup
- Existing subnet lookup

Example:

```hcl
data "aws_ami" "amazon_linux" {
  most_recent = true

  owners = ["amazon"]
}
```

---

### Module 7: Variables

- Input variables
- Variable declaration
- Variable types
- Default values
- Variable validation
- Sensitive variables
- Environment variables
- `.tfvars`
- `terraform.tfvars`
- `*.auto.tfvars`

Example:

```hcl
variable "instance_type" {
  type    = string
  default = "t2.micro"
}
```

---

### Module 8: Outputs

- Output variables
- Output values
- Referencing outputs
- Sensitive outputs
- Outputs between modules

```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

---

### Module 9: Local Values

- What are locals?
- Local expressions
- Reusing values
- Locals vs variables

```hcl
locals {
  environment = "dev"
  project     = "myapp"
}
```

---

### Module 10: Expressions & Functions

- Expressions
- Arithmetic expressions
- Conditional expressions
- String interpolation
- Built-in functions
- `lookup()`
- `length()`
- `join()`
- `split()`
- `concat()`
- `merge()`
- `contains()`
- `file()`
- `templatefile()`

---

### Module 11: Conditional Logic

- Conditional operator
- `count`
- Conditional resources
- Environment-based configuration

```hcl
count = var.environment == "prod" ? 3 : 1
```

---

### Module 12: Loops & Dynamic Blocks

Very important for interviews.

- `count`
- `for_each`
- `for` expressions
- `dynamic` blocks
- `each.key`
- `each.value`

Example:

```hcl
resource "aws_s3_bucket" "bucket" {
  for_each = var.buckets

  bucket = each.value
}
```

---

### Module 13: Terraform State

🔥 **Very important**

- What is Terraform state?
- `terraform.tfstate`
- State management
- Desired state
- Current state
- State locking
- State refresh
- State drift
- State file security
- State backup

Commands:

```bash
terraform state list
terraform state show
terraform state mv
terraform state rm
terraform state pull
terraform state push
```

---

### Module 14: Remote Backend

- Local backend
- Remote backend
- AWS S3 backend
- State locking
- Remote state
- Backend configuration
- Backend migration

Typical architecture:

```text
Developer
    ↓
Terraform
    ↓
AWS S3
    ↓
Terraform State
```

For production AWS, understand the current S3 backend/state-locking approach rather than relying only on older DynamoDB-locking tutorials.

---

### Module 15: Terraform Modules

🔥 **Very important for real projects**

- What is a module?
- Root module
- Child module
- Module structure
- Module inputs
- Module outputs
- Module dependencies
- Local modules
- Terraform Registry modules
- Reusable modules

Example:

```text
terraform-project/
├── main.tf
├── variables.tf
├── outputs.tf
├── providers.tf
└── modules/
    ├── vpc/
    ├── ec2/
    └── security-group/
```

---

### Module 16: Resource Lifecycle

- `create_before_destroy`
- `prevent_destroy`
- `ignore_changes`
- `replace_triggered_by`
- Resource replacement
- Immutable infrastructure

Example:

```hcl
lifecycle {
  create_before_destroy = true
}
```

---

### Module 17: Provisioners

- `local-exec`
- `remote-exec`
- `file`
- Provisioner limitations
- Why provisioners should generally be avoided when better alternatives exist

---

### Module 18: Terraform Import

- Import existing infrastructure
- Import blocks
- Importing EC2
- Importing S3
- Importing VPC resources
- Managing imported resources

---

### Module 19: Terraform Drift

Understand what happens when someone manually changes infrastructure:

```text
Terraform
   ↓
State says: t3.micro
   ↓
AWS manually changed
   ↓
Actual: t3.medium
   ↓
terraform plan
   ↓
Detects difference
```

Learn:

- Drift detection
- Refresh
- Reconciliation
- `terraform plan`

---

### Module 20: Terraform Workspaces

- What are workspaces?
- Workspace commands
- Development environment
- Production environment
- Workspace limitations
- Workspace vs separate directories

Commands:

```bash
terraform workspace list
terraform workspace new dev
terraform workspace select dev
terraform workspace show
terraform workspace delete dev
```

---

### Module 21: Terraform Security

- Secrets management
- Sensitive variables
- State-file security
- AWS IAM
- Least privilege
- AWS credentials
- Environment variables
- Secret managers
- Terraform Cloud/HCP Terraform sensitive data
- `.gitignore`
- Never commit `terraform.tfstate`

---

### Module 22: Terraform Validation & Testing

- `terraform fmt`
- `terraform validate`
- `terraform plan`
- Terraform test
- Unit-style testing concepts
- Integration testing
- `tflint`
- Checkov
- tfsec

---

### Module 23: Terraform CI/CD

🔥 **Very important for DevOps**

Terraform + GitLab CI:

```text
Developer
   ↓
Git Push
   ↓
GitLab
   ↓
terraform fmt
   ↓
terraform validate
   ↓
terraform plan
   ↓
Manual Approval
   ↓
terraform apply
   ↓
AWS
```

Learn:

- Terraform in Jenkins
- Terraform in GitLab CI
- Terraform in GitHub Actions
- Plan stage
- Apply stage
- Approval
- State management
- Service accounts/IAM roles

---

### Module 24: Terraform Cloud / HCP Terraform

- HCP Terraform
- Organizations
- Workspaces
- Remote execution
- Variables
- Variable sets
- State management
- Run triggers
- VCS integration
- Policy concepts

---

### Module 25: Advanced Terraform

- Provider aliases
- Multiple AWS accounts
- Multiple AWS regions
- Cross-account deployment
- Dynamic blocks
- Advanced expressions
- Complex variable types
- Module composition
- Dependency management
- Large-scale Terraform architecture
- Performance optimization

---

# 🧪 Hands-on Projects

### Project 1 — EC2

Create:

```text
VPC
 ├── Subnet
 ├── Internet Gateway
 ├── Route Table
 ├── Security Group
 └── EC2
```

### Project 2 — Complete AWS Web Infrastructure

```text
Route53
   ↓
ALB
   ↓
EC2 / Auto Scaling
   ↓
RDS
```

Create everything using Terraform.

### Project 3 — Multi-Environment

```text
Terraform
 ├── dev
 ├── staging
 └── prod
```

Use:

- Variables
- `.tfvars`
- Modules
- Remote state

### Project 4 — Terraform + GitLab CI/CD

```text
GitLab
   ↓
Validate
   ↓
Plan
   ↓
Approval
   ↓
Apply
   ↓
AWS
```

### Project 5 — Production-Style Terraform

Build:

```text
VPC
├── Public Subnets
├── Private Subnets
├── NAT Gateway
├── Internet Gateway
├── Route Tables
├── Security Groups
│
├── ALB
├── Auto Scaling Group
├── EC2
│
└── RDS
```

With:

- Modules
- Remote backend
- State locking
- Variables
- Outputs
- `for_each`
- `count`
- IAM
- CI/CD
- Security scanning

---

# 🎯 Interview Priority

If your goal is **DevOps interviews**, don't give equal time to every topic.

### 🔴 Must Know

1. Terraform workflow
2. Providers
3. Resources
4. Variables
5. Outputs
6. Data sources
7. `count`
8. `for_each`
9. Functions
10. State
11. Remote backend
12. State locking
13. Modules
14. Lifecycle
15. Import
16. Drift
17. Workspaces
18. Terraform + CI/CD

### 🟡 Should Know

- Provisioners
- HCP Terraform
- Terraform testing
- `tflint`
- Checkov
- Multiple providers
- Cross-account deployment

### 🟢 Advanced

- Complex module architecture
- Multi-account AWS
- Multi-region
- Enterprise Terraform architecture
- Policy as Code
- Large-scale state management

**Recommended learning sequence:**

```text
Terraform Basics
      ↓
HCL
      ↓
Providers
      ↓
Resources
      ↓
Variables / Outputs
      ↓
Data Sources
      ↓
Functions / Expressions
      ↓
count / for_each
      ↓
State
      ↓
Remote Backend
      ↓
Modules
      ↓
Lifecycle
      ↓
Import / Drift
      ↓
Workspaces
      ↓
Security
      ↓
CI/CD
      ↓
Production Project
```

For your DevOps roadmap, **Terraform + AWS + Ansible + GitLab CI + Docker + Kubernetes** is a very strong practical combination.
