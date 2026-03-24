---

copyright:
  years: 2025, 2026
lastupdated: "2026-03-24"

keywords: infrastructure-as-code, terraform-ibm-modules, terraform, hcp, stacks, hashicorp, multi-region, orchestration

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: terraform, hcp, stacks
account-plan:
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}

# Deploy Terraform IBM modules using HCP Terraform stacks
{: #deploy-tim-using-hcp-stacks}
{: toc-content-type="tutorial"}
{: toc-services="terraform, hcp, stacks"}
{: toc-completion-time="1h"}

A step-by-step guide to use IBM-supported Terraform IBM Modules to deploy and manage multi-region infrastructure with HashiCorp Cloud Platform (HCP) Terraform [Stacks](https://developer.hashicorp.com/terraform/language/stacks){: external}.
{: shortdesc}

This tutorial walks you through creating infrastructure using reusable and secure Terraform IBM Modules with HCP Terraform Stacks. Stacks enable you to orchestrate multiple deployments across regions and environments from a single configuration, making it ideal for multi-region architectures, disaster recovery setups, and standardized infrastructure patterns. By leveraging Terraform IBM Modules with Stacks, you ensure your infrastructure follows IBM Cloud best practices and security standards while maintaining consistency across all deployments.

For a complete working example, refer to this [example](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/stacks){: external}, which demonstrates how to use Terraform IBM Modules with HCP Terraform Stacks.

## Objectives
{: #stacks_objectives}

In this tutorial, you will:

- **Understand HCP Terraform stacks:** Learn how stacks orchestrate multiple deployments from a single configuration using components and deployments.

- **Create stack components using Terraform IBM modules:** Build reusable components that leverage secure Terraform IBM Modules to define your infrastructure following IBM Cloud best practices.

- **Configure multi-region deployments:** Set up multiple deployments across different IBM Cloud regions using a single stack configuration.

- **Manage infrastructure at scale:** Use stacks to provision, update, and manage infrastructure consistently across multiple environments.

## Audience
{: #stacks-audience}

This tutorial is designed for Platform Engineers and DevOps teams who need to manage infrastructure across multiple regions or environments while maintaining consistency and following best practices.

## Prerequisites
{: #stacks-prerequisites}

1. An HCP Terraform account with Stacks enabled. Refer to [HCP Account](https://developer.hashicorp.com/hcp/docs/hcp/create-account){: external} for information about creating an account.
2. If you do not have one, create an {{site.data.keyword.cloud_notm}} [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration).
3. Familiarity with Terraform and basic infrastructure concepts.
4. Git repository to store your Stack configuration.
5. Terraform CLI installed locally to initialize the Stack configuration. Refer to [Getting started with Terraform on IBM Cloud](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started){: external} for installation instructions.

## Understand HCP Terraform stacks
{: #understand-stacks}
{: step}

HCP Terraform Stacks is an orchestration framework that allows you to manage multiple related deployments from a single configuration. Key concepts include:

- **Components:** Reusable infrastructure building blocks that encapsulate Terraform modules. Components define what resources to create.
- **Deployments:** Instances of your stack deployed to specific environments or regions. Each deployment can have different input values.
- **Stack configuration:** The collection of component definitions, provider configurations, and deployment specifications that define your infrastructure pattern.

Stacks use a declarative configuration language with `.tfstack.hcl`, `.tfdeploy.hcl`, and `.tfcomponent.hcl` files to define your infrastructure orchestration. For more information, see [Stack component configuration](https://developer.hashicorp.com/terraform/language/stacks/component/config){: external}.

## Create stack components using Terraform IBM modules
{: #stacks-create-components}
{: step}

This step explains how to create reusable stack components that leverage Terraform IBM modules. For a complete working example, refer to this [example](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/stacks){: external}.

### Set up your stack directory structure
{: #stacks-directory-structure}

To create a stack configuration for deploying Terraform IBM modules, you need to set up a directory structure with specific configuration files. The [stacks example](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/stacks){: external} provides a complete example of this structure.

**Key steps:**

1. **Create a project directory** for your stack configuration and initialize it as a Git repository:

    ```bash
    mkdir my-ibm-stack
    cd my-ibm-stack
    git init
    ```
    {: pre}

2. **Create stack configuration files** using the `.tfdeploy.hcl`, and `.tfcomponent.hcl` file extensions. These files define your infrastructure components, provider configurations, variables, and deployments. Your directory structure should look like:

    ```
    my-ibm-stack/
    ├── providers.tfcomponent.hcl
    ├── variables.tfcomponent.hcl
    ├── components.tfcomponent.hcl
    └── deployments.tfdeploy.hcl
    ```
    {: screen}

3. **Compose your infrastructure configuration** by creating the stack configuration files (`providers.tfcomponent.hcl`, `variables.tfcomponent.hcl`, `components.tfcomponent.hcl`, and `deployments.tfdeploy.hcl`). These files define your providers, variables, components using Terraform IBM modules Terraform IBM Modules, and deployment configurations.

4. **Run `terraform stacks init`** after creating your configuration files. This command:
   - Downloads and locks provider versions specified in your configuration
   - Generates a `.terraform.lock.hcl` file that ensures consistent provider versions across all deployments
   - Validates your stack configuration syntax

    ```bash
    terraform stacks init
    ```
    {: pre}

5. **Commit the `.terraform.lock.hcl` file** to your Git repository. This file must be committed before publishing your stack to HCP Terraform to prevent version drift and ensure compatibility across all deployments:

    ```bash
    git add .
    git commit -m "Add stack configuration and lock file"
    ```
    {: pre}

    You will use this Git repository to connect your stack configuration to HCP Terraform in the next steps.
    {: note}

## Publish your stack to HCP Terraform
{: #stacks-publish}
{: step}

1. Ensure you have run `terraform stacks init` and committed the `.terraform.lock.hcl` file as described in the previous steps.

2. Commit your stack configuration to Git:

    ```bash
    git add .
    git commit -m "Initial stack configuration with Terraform IBM modules"
    git push origin main
    ```
    {: pre}

    **Important:** Verify that your `.terraform.lock.hcl` file is included in this commit. HCP Terraform requires this file to ensure consistent provider versions across all deployments.

3. To create a new stack, follow these steps:

    * In HCP Terraform, navigate to your organization.
    * Click **Create stack**.
    * Connect to your VCS provider (GitHub, GitLab, etc.).
    * Select the repository containing your stack configuration.
    * Choose the branch (e.g., `main`).
    * Click **Create stack**.

4. After creating the stack, configure the following settings:
    * Set the **Stack name** (e.g., `ibm-multi-region-infrastructure`).
    * Add a **Description** explaining the stack's purpose.
    * Configure **Variable sets** to store your IBM Cloud API key securely.
    * Click **Save**.

## Create and configure variable sets
{: #stacks-variable-sets}
{: step}

Before deploying, create a variable set in HCP Terraform to store your IBM Cloud credentials:

To create a variable set, follow these steps:

1. In HCP Terraform, navigate to **Settings** > **Variable Sets**.
2. Click **Create variable set**.
3. Name it (e.g., `ibm-credentials`).
4. Add a variable:
    * **Key:** `ibmcloud_api_key`
    * **Value:** Your IBM Cloud API key
    * Mark as **Sensitive**
    * **Category:** Terraform
5. Apply the variable set to your stack.
6. Note the variable set ID (format: `varset-XXXXXXXXXX`) and update it in your `deployments.tfdeploy.hcl` file.

## Deploy your stack
{: #stacks-deploy}
{: step}

To deploy your stack, follow these steps:

1. In HCP Terraform, open your stack.
2. Click the **Fetch configuration from VCS** button to retrieve the latest configuration from your Git repository.
3. HCP Terraform stacks will automatically initiate the planning process for all defined deployments.
4. Review the available deployment runs displayed in the stack interface.
5. For each deployment you want to provision:
    * Review the plan output to verify the resources that will be created.
    * Click **Approve** to start the Terraform apply process for that specific deployment.
6. Monitor the deployment progress as resources are created across all approved deployments.

## Manage and update your stack
{: #stacks-manage}
{: step}

After deploying your stack, you can manage and update it as your infrastructure needs evolve. The following sections describe common management tasks:

### Add a new deployment

To add a new region, update your `deployments.tfdeploy.hcl` file with a new deployment block. Commit and push the changes to your Git repository. HCP Terraform will automatically detect the new deployment and allow you to plan and deploy it.

### Update components

To modify your infrastructure, update the `components.tfcomponent.hcl` file. Commit and push the changes to trigger an update in HCP Terraform.

### Destroy resources

To remove infrastructure from a specific deployment:

1. In HCP Terraform, navigate to your stack.
2. Select the deployment you want to destroy.
3. Click **Actions** > **Destroy**.
4. Confirm the destruction.

## Known limitations
{: #stacks-known-limitations}

While HCP Terraform stacks provides powerful orchestration capabilities, there are some limitations to be aware of when using it with Terraform IBM modules:

### Local-exec provisioner not supported

HCP Terraform stacks does not currently support the `local-exec` provisioner. This limitation is due to the way stack execution has been architected and designed, and there is currently no support available for using `local-exec` within stacks.

**Impact on Terraform IBM modules:**

Some Terraform IBM modules may include `local-exec` provisioners for tasks such as:
- Running post-deployment scripts
- Configuring resources that require CLI commands
- Executing local validation or setup tasks

Before selecting a Terraform IBM module for use with stacks, review the module's source code to ensure it does not contain `local-exec` provisioners. You can search for `local-exec` in the module's GitHub repository or check the module documentation for any known limitations.

## Best practices
{: #stacks-best-practices}

Follow these best practices to ensure successful deployment and management of your infrastructure with HCP Terraform stacks:

- **Use version control:** Always store your stack configuration in Git for version history and collaboration.
- **Commit Lock Files:** Always commit the `.terraform.lock.hcl` file to your repository after running `terraform stacks init` to ensure consistent provider versions.
- **Leverage variable sets:** Store sensitive credentials in HCP Terraform variable sets, not in your configuration files.
- **Tag resources:** Use consistent tagging strategies across deployments for cost tracking and resource management.
- **Test changes:** Use a development deployment to test changes before applying them to production deployments.
- **Monitor deployments:** Regularly review deployment status and outputs in HCP Terraform.
- **Use Terraform IBM modules:** Leverage pre-built, secure modules from the Terraform IBM Modules organization to ensure best practices.
- **Verify module compatibility:** Before using a Terraform IBM module with stacks, verify that it does not contain `local-exec` provisioners, as these are not supported in the stacks execution environment.
- **Implement orchestration checks:** Use `orchestrate` blocks to validate deployment states and dependencies.

## Example use cases
{: #stacks-use-cases}

HCP Terraform stacks with Terraform IBM modules can be used for various infrastructure deployment scenarios:

### Multi-region high availability

Deploy identical infrastructure across multiple regions for disaster recovery and high availability by defining multiple deployment blocks in your `deployments.tfdeploy.hcl` file, each targeting a different region with appropriate prefixes and tags.

### Environment separation

Deploy separate environments (dev, staging, production) with different configurations by creating deployment blocks for each environment. Each deployment can target the same or different regions and use environment-specific resource tags and naming prefixes.

## Next steps
{: #deploytim-hcp-stacks-next-steps}

- Explore the [sample-iac-solutions stacks example](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/stacks){: external} for a complete working example.
- Learn more about the [Terraform IBM Cloud Provider](https://github.com/IBM-Cloud/terraform-provider-ibm).
- Explore available [Terraform IBM Modules](https://github.com/terraform-ibm-modules).
- Review the [HCP Terraform stacks documentation](https://developer.hashicorp.com/terraform/language/stacks).
- Learn about [stack orchestration patterns](https://developer.hashicorp.com/terraform/language/stacks/deploy/orchestration).

## Related links
{: #stacks-related-links}

- [HCP Terraform stacks](https://developer.hashicorp.com/terraform/language/stacks)
- [Stack components](https://developer.hashicorp.com/terraform/language/stacks/components)
- [Stack deployments](https://developer.hashicorp.com/terraform/language/stacks/deploy)
- [Terraform IBM modules](https://github.com/terraform-ibm-modules)
- [Example stack configuration](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/stacks){: external}
