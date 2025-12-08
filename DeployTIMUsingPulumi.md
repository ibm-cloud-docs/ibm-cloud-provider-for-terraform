---

copyright:
  years: 2017, 2025
lastupdated: "2025-12-08"

keywords: Terraform on IBM Cloud, pulumi, ibmcloud, automate, automation, iaas, paas, infrastructure-as-code, multi-service, multi-zone, terraform-ibm-modules, pulumi and ibmcloud, terraform

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: pulumi, ibm-cloud-services
account-plan:
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}

# Use your favorite programming language with Terraform IBM Modules and Pulumi
{: #UseLangWithTIM}
{: #pulumi-with-terraform-ibm-modules}
{: toc-content-type="tutorial"}
{: toc-services="vpc"}
{: toc-completion-time="30m"}

Learn how to use [Pulumi](https://www.pulumi.com/docs/iac/get-started/) with the [Terraform IBM Cloud Provider](https://github.com/IBM-Cloud/terraform-provider-ibm) and IBM-supported [Terraform IBM Modules](https://github.com/terraform-ibm-modules) to define and manage your IBM Cloud infrastructure using the programming language of your choice.
{: shortdesc}

Pulumi enables developers to write Infrastructure as Code (IaC) using familiar languages such as Python, Go, TypeScript, or C#. With Pulumi, you can leverage existing Terraform providers and modules to manage IBM Cloud resources efficiently and consistently.

## Objectives
{: #UseTIMobjectives}

- Use Pulumi with the Terraform IBM Cloud provider.
- Import and use Terraform IBM Modules within Pulumi.
- Deploy and manage IBM Cloud infrastructure using your preferred language (Python, Go, TypeScript, or C#).
- Understand interoperability between Terraform modules and Pulumi stacks.

## Audience
{: #UseTIMaudience}

This tutorial is intended for developers, DevOps engineers, and SREs familiar with Terraform who want to adopt Pulumi for multi-language infrastructure management while continuing to use existing IBM Cloud Terraform modules.

## Prerequisites
{: #UseTIMprereqs}

Before you begin, ensure that you have the following:

- An {{site.data.keyword.cloud_notm}} account with permissions to create and manage infrastructure.
- [Pulumi CLI](https://www.pulumi.com/docs/get-started/install/) installed.
- [Terraform IBM Cloud Provider](https://github.com/IBM-Cloud/terraform-provider-ibm) or IBM Terraform modules available locally or through GitHub.
- [IBM Cloud CLI](/docs/cli?topic=cli-getting-started) and [Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) (optional, for validation).
- Access to API key credentials for your IBM Cloud account.

## Set up your environment
{: #UseTIMlesson1-setup}
{: step}

1. Install Pulumi for your operating system.

   ```bash
   curl -fsSL https://get.pulumi.com | sh
   ```
   {: pre}

2. Verify your installation.

   ```bash
   pulumi version
   ```
   {: pre}

3. Log in to Pulumi (you can use the Pulumi Service or a local backend).

   ```bash
   pulumi login
   ```
   {: pre}

4. Create a new project.

   ```bash
   pulumi new python
   ```
   {: pre}

   You can replace `python` with `typescript`, `go`, or `csharp` based on your preferred language.
   {: tip}

## Configure the IBM Cloud provider
{: #UseTIMlesson2-provider}
{: step}

Pulumi uses Terraform providers through the [Pulumi Terraform Bridge](https://www.pulumi.com/docs/using-pulumi/adopting/from-terraform/#terraform-bridge).

To configure the IBM Cloud provider:

1. Add the Pulumi Terraform provider dependency for IBM Cloud in your `requirements.txt` (Python example).

   ```bash
   pulumi_terraform==0.8.1
   ```
   {: pre}

2. Define IBM Cloud credentials using environment variables.

   ```bash
   export IC_API_KEY=<your_ibmcloud_api_key>
   export IC_REGION=us-south
   ```
   {: pre}

3. Initialize the provider in your Pulumi program.

   ```python
   import os
   import pulumi
   from pulumi_terraform import Provider

   ibm_provider = Provider("ibm", {"ibmcloud_api_key": os.getenv("IC_API_KEY")})
   ```

## Use Terraform IBM Modules in Pulumi
{: #UseTIMlesson3-ibm-modules}
{: step}

Before proceeding, you should be aware of below concepts -

**Stack** - A Stack is an isolated instance of your Pulumi program, typically representing an environment (dev, staging, prod).

**Project** - A Project is a single Pulumi program containing your infrastructure definitions.

**Configuration** - Stack-specific settings that can be changed without modifying code.

**State** - Pulumi maintains state to track current infrastructure and manage updates.

The [IBM Provider](https://www.pulumi.com/registry/packages/ibm/) must be installed as a local Package by following the [instructions for Any Terraform Provider](https://www.pulumi.com/registry/packages/terraform-provider/)

You can [reuse existing Terraform IBM modules](https://www.pulumi.com/docs/iac/guides/building-extending/using-existing-tools/use-terraform-module/#adding-a-terraform-module-to-your-pulumi-project) directly in Pulumi.

Example (Python):


Pulumi automatically provisions the underlying Terraform module using the IBM Cloud provider.

## Deploy your Pulumi stack
{: #UseTIMlesson4-deploy}
{: step}

1. Preview your changes.

   ```bash
   pulumi preview
   ```
   {: pre}

2. Deploy your stack.

   ```bash
   pulumi up
   ```
   {: pre}

   Review the proposed changes and confirm with `yes` to apply.

3. To destroy your stack.

   ```bash
   pulumi down
   ```
   {: pre}

4. Manage your stack history.

   ```bash
   pulumi stack history
   ```
   {: pre}

## Advanced usage
{: #UseTIMlesson5-advanced}
{: step}

- **Mix Pulumi and Terraform:**
  Use Pulumi for orchestration and logic, and Terraform modules for reusable infrastructure blueprints.

- **Multi-language support:**
  Write reusable Pulumi components that abstract Terraform modules, making them available in Python, TypeScript, Go, or C#.

- **CI/CD integration:**
  Integrate Pulumi with IBM Cloud Continuous Delivery or GitHub Actions for automated deployments.

- **State management:**
  Store Pulumi state in IBM Cloud Object Storage or the Pulumi Service for collaborative management.

## Clean up resources
{: #UseTIMlesson6-cleanup}
{: step}

When you complete this tutorial, remove the deployed resources to avoid unnecessary charges.

```bash
pulumi down
```
{: pre}

## Next steps
{: #UseTIMnext-steps}

- Learn more about the [Terraform IBM Cloud Provider](https://github.com/IBM-Cloud/terraform-provider-ibm)
- Explore available [Terraform IBM Modules](https://github.com/terraform-ibm-modules)
- Review the [Pulumi Terraform Bridge documentation](https://www.pulumi.com/docs/using-pulumi/adopting/from-terraform/)
- Check some examples provided [here](https://github.ibm.com/GoldenEye/pulumi-ibmcloud)

## Related links
{: #UseTIMrelated-links}

- [Pulumi Documentation](https://www.pulumi.com/docs/)
- [IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started)
- [IBM Cloud Provider for Terraform GitHub Repository](https://github.com/IBM-Cloud/terraform-provider-ibm)
