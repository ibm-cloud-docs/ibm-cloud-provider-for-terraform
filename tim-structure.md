---

copyright:
  years: 2025, 2026
  lastupdated: "2026-01-21"

keywords: Terraform IBM Modules, code structure, Terraform IBM Modules structure, module structure, module code

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Understanding the Terraform IBM Module Structure
{: #understand-tim-structure}


The [Terraform IBM Modules](https://registry.terraform.io/namespaces/terraform-ibm-modules)(TIM) is a curated collection of reusable, production-ready Terraform modules designed to simplify the creation, management, and versioning of complex, compliant environments on {{site.data.keyword.cloud_notm}}. Each module follows a standardized structure based on [HashiCorp's module development guidelines](https://developer.hashicorp.com/terraform/language/modules/develop/structure){: external}, enhanced with IBM Cloud best practices for enterprise deployments.

This document provides a comprehensive guide to understanding the TIM module code structure, helping you effectively consume, contribute to, and extend these modules in your infrastructure-as-code projects.

## Audience
{: #tim-structure-audience}

This document focuses on understanding the structure and organization of Terraform IBM Modules (TIM) modules. It's designed for developers and architects who want to effectively consume and work with these modules in their IaC projects.

## Objectives
{: #tim-structure-objectives}

At the end, you'll understand:

- How to navigate module repositories
- Where to find module code, documentation, diagrams, and usage examples
- The purpose of different directories (examples, modules, solutions)
- How to use root-level modules vs submodules


## Navigating a Terraform IBM Module
{: #navigating-tim-module}

Start by identifying the IBM Cloud service you want to provision (such as Object Storage, Databases, or Virtual Private Cloud) and locate the corresponding module in the [terraform-ibm-modules](https://registry.terraform.io/namespaces/terraform-ibm-modules) organization. For example, use [`terraform-ibm-cos`](https://registry.terraform.io/modules/terraform-ibm-modules/cos/ibm/latest) for IBM Cloud Object Storage, or [`terraform-ibm-cloud-monitoring`](https://registry.terraform.io/modules/terraform-ibm-modules/cloud-monitoring/ibm/latest) for IBM Cloud Monitoring.

## Module Structure
{: #tim-structure}

Get the source code of a TIM module either from the [Terraform registry](https://registry.terraform.io/namespaces/terraform-ibm-modules) or [GitHub Org](https://github.com/terraform-ibm-modules). When working with a TIM module, the following key directories and files are commonly used:

```
terraform-ibm-<module-name>/
├── examples/                         # Usage examples
│   ├── example-1/
│   └── example-2/
├── modules/                          # Nested submodules
│   ├── submodule-a/
│   └── submodule-b/
├── main.tf                           # Root module - primary resource definitions
├── variables.tf                      # Input variable declarations
├── outputs.tf                        # Output value declarations
├── version.tf                        # Provider and Terraform version constraints
├── README.md                         # Module documentation
```

Module repositories also contain additional development and CI/CD tooling (workflows, build automation, etc.) that are primarily relevant to module contributors.

### Root-level module files
{: #module-root-code}

The root-level module code contains the core Terraform configuration files that serves as the primary interface for consuming the module. It includes the following:

| File | Purpose |
|------|---------|
| `main.tf` | Primary resource definitions and module logic |
| `variables.tf` | Input variable declarations with types, descriptions, and validations |
| `outputs.tf` | Output values exposed to use by other configurations |
| `version.tf` | Terraform and provider version constraints |

You consume this module by referencing it in a `module` block within your own Terraform configuration (your working directory where you run `terraform plan` and `terraform apply`). The module repository itself is not meant to be deployed directly.
{: note}

### Module documentation
{: #module-documentation}

Every TIM module includes a `README` file at the root level that serves as the primary documentation and entry point for users. Before using a module into your project, review its documentation(README) to understand the key details. The README provides comprehensive documentation including:

- **Module description** and key features
- **Usage instructions** for consuming the module from the Terraform registry
- **Required IAM permissions** needed to deploy resources
- **Requirements** for Terraform and provider versions
- **Inputs and Outputs** variables details
- Links to **examples** and **submodules**

Always check the required IAM permissions before using a module.
{: tip}

### Usage example
{: #timstructure-module-usage}

The usage example provides a reference implementation that demonstrates how to consume the module. It helps users understand required inputs, optional parameters, and common configuration patterns. The following is an example shown for a Cloud Object Storage module.

```hcl
# Creates a COS instance and a bucket
module "my_service" {
  source = "terraform-ibm-modules/cos/ibm"
  version = "X.Y.Z" # Replace "X.Y.Z" with a release version to lock into a specific release
  resource_group_id = "xxXXxxXXxXXXXxxXxxxXXXxXXXX"
  region = "us-south"
  cos_instance_name = "my-cos-instance"
  bucket_name = "my-cos-bucket"
  existing_kms_instance_guid = "xxxxxxxx-XXXX-XXXX-XXXX-xxxxxxxx"
  kms_key_crn = "crn:v1:bluemix:public:kms:us-south:a/xXXXxxXXxXXXXxxXxxxXXXxXXXX:xxxxxx-XXXX-XXXX-XXXX-xxxxxx:key:xxxxxx-XXXX-XXXX-XXXX-xxxxxx"
}
```

### Examples
{: #module-examples}

The `examples/` directory contains working demonstrations of how to use the module. Each example is a complete, runnable Terraform configuration.

```
examples/
├── basic/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── provider.tf
│   ├── version.tf
│   └── README.md
```

The modules include multiple examples, ranging from basic to advanced. It also contains README that explains all the supported features by that example.

### Submodules
{: #tim-submodules}

The `modules/` directory contains nested modules (submodules) that provide focused functionality. Submodules enable composition and code reuse within the module.

```
modules/
├── submodule-1/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── version.tf
│   └── README.md
```

The submodules allow users to use specific functionality without deploying the entire root module. It can be referenced directly from the Terraform registry using the double-slash notation:

```
source = "terraform-ibm-modules/<module-name>/ibm//modules/<submodule-name>"
```

## Next steps
{: #tim-structure-next-steps}

Now that you understand the TIM module structure, you can:

1. **Explore available modules** — Browse the [Terraform Registry](https://registry.terraform.io/namespaces/terraform-ibm-modules) or [Terraform IBM Modules GitHub Org](https://github.com/terraform-ibm-modules/).

2. **Deploy your first module** — Start with a basic example and customize for your environment. Refer the instructions [here](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-deploy-tim-module).

3. **Join the community** — Engage with other TIM users through GitHub issues and discussions.


## Feedback
{: #feedback}

If you have questions or feedback for any specific module, open an issue in the relevant module repository.
