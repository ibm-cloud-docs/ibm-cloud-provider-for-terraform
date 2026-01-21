---

copyright:
  years: 2025, 2026
lastupdated: "2026-01-21"

keywords: pulumi, ibmcloud, automation, infrastructure-as-code, terraform-ibm-modules, pulumi and ibmcloud, terraform

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: pulumi, ibm-cloud-services
account-plan:
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}

# Use your favorite programming language with Terraform IBM Modules and Pulumi
{: #pulumi-with-tim}
{: toc-content-type="tutorial"}
{: toc-completion-time="30m"}

Learn how to use [Pulumi](https://www.pulumi.com/docs/get-started/){: external} with the [Terraform IBM Modules](https://github.com/terraform-ibm-modules){: external} to define and manage your {{site.data.keyword.cloud_notm}} infrastructure using the programming language of your choice.
{: shortdesc}

### Pulumi Overview
{: #pulumi-overview}

Pulumi enables developers to write Infrastructure as Code (IaC) using familiar languages such as Python, Go, TypeScript, or C#. With Pulumi, you can leverage existing Terraform providers and modules to manage {{site.data.keyword.cloud_notm}} resources efficiently and consistently.

The following **[Pulumi concepts](https://www.pulumi.com/docs/iac/concepts/)**{: external} will be used in the steps below.

- **[Stack](https://www.pulumi.com/docs/iac/concepts/stacks/)**{: external} - A Stack is an isolated instance of your Pulumi program, typically representing an environment (dev, staging, prod).
- **[Project](https://www.pulumi.com/docs/iac/concepts/projects/)**{: external} - A Project is a single Pulumi program containing your infrastructure definitions.
- **[Configuration](https://www.pulumi.com/docs/iac/concepts/config/)**{: external} - Stack-specific settings that can be changed without modifying code.
- **[State](https://www.pulumi.com/docs/iac/concepts/state-and-backends/)**{: external} - Pulumi maintains state to track current infrastructure and manage updates.

## Objectives
{: #pulumi-with-tim-objectives}

- Use Pulumi with the {{site.data.keyword.cloud_notm}} provider plug-in for Terraform.
- Integrate [Terraform IBM Modules](https://registry.terraform.io/namespaces/terraform-ibm-modules){: external} in Pulumi.
- Deploy and manage {{site.data.keyword.cloud_notm}} infrastructure in Python.

## Audience
{: #pulumi-with-tim-audience}

This tutorial is for developers, DevOps engineers, and SREs familiar with Terraform who want to adopt Pulumi for multi-language infrastructure management while leveraging existing [Terraform IBM Modules](https://github.com/terraform-ibm-modules).

## Prerequisites
{: #pulumi-with-tim-prereqs}

Before you begin, ensure that you have the following:

- An {{site.data.keyword.cloud_notm}} account with permissions to create and manage infrastructure, and access to API key credentials.
- [Pulumi CLI](https://www.pulumi.com/docs/get-started/download-install/){: external} installed.

## Set up Pulumi environment
{: #pulumi-with-tim-setup}
{: step}

Follow the below instructions to setup the environment:

1.  Install Pulumi on your local machine, if it is not already installed.

    ```bash
    curl -fsSL https://get.pulumi.com | sh
    ```
    {: pre}

2.  Verify your installation.

    ```bash
    pulumi version
    ```
    {: pre}

3.  Log in to Pulumi by either creating a Pulumi account or using local-only mode. In this tutorial, local-only mode is used.

    ```bash
    pulumi login --local
    ```
    {: pre}

4.  Create a new project.

   - Create new Pulumi project and follow the instructions to provide `Project name`, `Project description`, `Stack name`, `Passphrase` and `toolchain` (package manager) of your choice from the options provided.

      ```bash
      mkdir test-pulumi
      cd test-pulumi
      pulumi new python
      ```
      {: pre}

      **Please note:**

   - If you want to create a new stack, that can be done using `pulumi stack init <stack-name>`.
   - If the directory is not empty, the command to create new project may result in error, to avoid that you can use the `--force` flag i.e. `pulumi new python --force`.

      You can replace `python` with `typescript`, `go`, or `csharp` based on your preferred language or the minimal program template which are provided with Pulumi.
      {: tip}

   - This should set up the virtual environment, generate the necessary files (`__main__.py`,`YAML` configuration files, and `requirements.txt`), and install the dependencies listed in `requirements.txt`.

## Configure Terraform IBM Modules in Pulumi
{: #configure-tim-module-in-pulumi}
{: step}

Configure your Pulumi project by adding IBM Provider package and Terraform IBM Modules.

1. Install dependencies

   - Run this command to add the IBM provider package to the Project

      ```bash
      pulumi package add terraform-provider ibm-cloud/ibm
      ```
      {: pre}

   - Add Terraform IBM Modules as a SDK in your Pulumi project

      Using the below packages, you can provision {{site.data.keyword.cloud_notm}} resources - a Resource Group and a Watson Discovery service instance.

      ```bash
      pulumi package add terraform-module terraform-ibm-modules/resource-group/ibm 1.4.6 ibm_rg_module
      pulumi package add terraform-module terraform-ibm-modules/watsonx-discovery/ibm 1.11.1 wx_discovery
      ```
      {: pre}

   - Copy the below code in the `__main__.py` file

      ```py
        # Imports
        import pulumi
        import pulumi_ibm_rg_module as rgmod
        import pulumi_wx_discovery as wxd_mod

        # Pulumi configuration
        config = pulumi.Config()
        PREFIX = config.get("prefix") or "pulumi-demo"
        EXISTING_RESOURCE_GROUP = "Default" # Change this to None if new resource group should be created.

        def create_resource_group():
        """Create or reference an existing IBM Cloud resource group."""
        if EXISTING_RESOURCE_GROUP:
            return rgmod.Module(
                    "resource_group", existing_resource_group_name=EXISTING_RESOURCE_GROUP
            )
        return rgmod.Module("resource_group", resource_group_name=f"{PREFIX}-resource-group")

        def create_watson_discovery(rg):
        """Provision a Watson Discovery instance."""
        return wxd_mod.Module(
            "wxd-test",
            resource_group_id=rg.resource_group_id,
            watson_discovery_name=f"{PREFIX}-wxd-test",
        )

        def main():
        """Main method to provision resources."""

        rg = create_resource_group()
        watson_discovery = create_watson_discovery(rg)

        # Export Outputs
        pulumi.export("watson_discovery_id", watson_discovery.id)
        pulumi.export("watson_discovery_dashboard", watson_discovery.dashboard_url)


        if __name__ == "__main__":
        main()
      ```

2. Update Pulumi stack config

    You can now add configuration like `prefix`, `resource group` by using the command - `pulumi config set <attribute> <attribute-value>`

      ```bash
      pulumi config set prefix pulumi-demo # Replace with prefix of your choice.
      ```
      {: pre}

      The configuration will be added as part of the `Pulumi.<your-stack-name>.yaml` file.

3. Set {{site.data.keyword.cloud_notm}} credentials using environment variables

      ```bash
      export IBMCLOUD_API_KEY=<your_ibmcloud_api_key>
      ```
      {: pre}

## Deploy your Pulumi stack
{: #deploy-tim-with-pulumi}
{: step}

1. Preview your changes

   ```bash
   pulumi preview
   ```
   {: pre}

2. Deploy your stack

   ```bash
   pulumi up
   ```
   {: pre}

   Review the proposed changes and confirm with `yes` to apply.

3. Validation

   After running a Pulumi deployment, you should verify that the {{site.data.keyword.cloud_notm}} resources have been provisioned correctly. If the deployment is successful, Pulumi will display the resource creation summary in the terminal. The resources created can then be validated as suggested below:

      **(a) Verify via {{site.data.keyword.cloud_notm}} Console**

      - Log in to the {{site.data.keyword.cloud_notm}} Console.
      - Navigate to the relevant service (Resource Group , Watson) and confirm the resources are listed.
      - Cross‑check resource names and configurations against your Pulumi stack.

      **(b) Use {{site.data.keyword.cloud_notm}} CLI**

      - Run {{site.data.keyword.cloud_notm}} CLI commands to verify the provisioned resources after logging in to the {{site.data.keyword.cloud_notm}} CLI. This can help confirm that the resources exist and match the expected configuration.

## Clean up resources
{: #pulumi-with-tim-cleanup}
{: step}

When the resources deployed are no longer needed, you can clean up your environment and remove the deployed resources to avoid unnecessary charges.

```bash
pulumi down
```
{: pre}

With the above command, the resources in the stack are deleted, but the stack’s history and configuration remain. You can remove the stack entirely by running below command.

```bash
pulumi stack rm <stack-name>
```
{: pre}

## Additional Examples
{: #example-tim-with-pulumi}

Now that you have learned how to deploy a Terraform IBM Module using Pulumi, you can explore additional modules such as `Key Protect` and `Object Storage` by following the same steps outlined above.

The related module code is provided [here](https://github.com/terraform-ibm-modules/sample-iac-solutions/blob/main/pulumi/__main__.py). You can use these [examples](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/pulumi/terraform_ibm_modules) and [instructions](https://github.com/terraform-ibm-modules/sample-iac-solutions/blob/main/pulumi/README.md) directly to deploy the modules.

## Next steps
{: #pulumi-with-tim-next-steps}

- [Learn more](https://www.pulumi.com/docs/iac/guides/building-extending/using-existing-tools/use-terraform-module/#adding-a-terraform-module-to-your-pulumi-project){: external} about integrating existing Terraform modules directly in Pulumi.
- [Pulumi Terraform provider](https://pypi.org/project/pulumi-terraform/6.0.1/){: external}
- Explore [Terraform IBM Modules](https://registry.terraform.io/modules/terraform-ibm-modules/){: external}
