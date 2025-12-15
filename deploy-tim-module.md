---

copyright:
  years: 2025, 2025
lastupdated: "2025-12-15"

keywords: Terraform IBM Modules, Deploy a Terraform IBM Module, terraform module deployment

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Deploy a Terraform IBM Module using Terraform CLI
{: #deploy-tim-module}
{: toc-content-type="tutorial"}
{: toc-services="vpc"}


In this tutorial, you will learn how to deploy a terraform-ibm-module (TIM) module using Terraform CLI. It will cover how variables are defined and passed, which CLI commands drive the process, and demonstrate the workflow with IBM Cloud Object Storage (COS) as an example.


## Objectives
{: #deploy-tim-module-objectives}

By the end of this tutorial, you will be able to:
- Configure and manage variables in modules using `terraform.tfvars`.
- Use Terraform CLI commands to deploy and manage resources.

While this tutorial uses the [Cloud Object Storage module](https://github.com/terraform-ibm-modules/terraform-ibm-cos) as an example, the skills gained here will be transferable to all Terraform modules.

## Prerequisites
{: #deploy-tim-module-prerequisites}

Before you begin, ensure you have the following:
- [Git CLI](https://git-scm.com/install/) installed
- [Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- [IBM Cloud apikey](/docs/account?topic=account-userapikey&interface=ui) to access the IBM Cloud.

## Clone the repository
{: #deploy-tim-module-lesson1-clone}
{: step}

Start by cloning the GitHub repository containing the Terraform module.

You can use `git clone` command as follows:

```bash
git clone https://github.com/terraform-ibm-modules/terraform-ibm-cos.git
```

## Understand the code
{: #deploy-tim-module-lesson2-code}
{: step}

In the root of the cloned project, there exists a folder called `examples`. The `examples` directory contains working demonstrations of how to use the module. Each example is a complete, runnable Terraform configuration.
This tutorial uses the `basic` example. Navigate to this example directory as follows:

```bash
cd terraform-ibm-cos/examples/basic
```
This example provisions the following resources:
- A new resource group (if an existing one is not provided)
- An IBM Cloud Object Storage instance
- Two buckets in the newly provisioned Object Storage instance

## Configure the variables
{: #deploy-tim-module-lesson3-configure}
{: step}

Create a new file named `terraform.tfvars` in the basic folder. This file is used to provide values for the input variables in the `variables.tf` file.

In the `basic` example, the module defines various input variables in `variables.tf`. Some variables such as `ibmcloud_api_key`, `prefix` and `region`, don't have default values, making them required. Terraform needs the values for the required variables. Defining them in `terraform.tfvars` enables automatic loading. The `prefix` variable is a string added to the beginning of resource names to keep them organized and easily identifiable.

Add these required variables in the file:

```hcl
ibmcloud_api_key = "<your-api-key>"
prefix = "tf-demo" # you can choose a prefix of your choice
region = "us-south"
```

Review the `variables.tf` file and update `terraform.tfvars` to override any default values do not meet your requirements.

## Initialize Terraform
{: #deploy-tim-module-lesson4-init}
{: step}

Initialize Terraform in the working directory (`examples/basic`) using the following command:

```bash
terraform init
```

This command downloads and installs plugins for the required providers as specified in `providers.tf`.

## Generate execution plan
{: #deploy-tim-module-lesson5-plan}
{: step}

Run the following command:

```bash
terraform plan
```

This command displays the execution plan, which provides a preview of the changes Terraform intends to make to your infrastructure based on your configuration files, allowing you to review and verify the proposed changes.

For this basic example, the command output shows that:
- A new resource group called `<your-prefix>-resource-group` will be created
- A Cloud Object Storage instance will be created
- Two buckets will be created in the chosen region

## Deploy the resources
{: #deploy-tim-module-lesson6-deploy}
{: step}

Run the following command to begin the deployment:

```bash
terraform apply
```

Approve the deployment when prompted, by typing `yes`. Alternatively, you may use `terraform apply -auto-approve` to automatically approve the changes.
Once confirmed, Terraform will begin provisioning all resources defined in the execution plan. This step make take some time depending on the configuration.

## Verify the deployed resources
{: #deploy-tim-module-lesson7-verify}
{: step}

After Terraform completes applying the configuration, verify that the resources have been successfully created in your IBM Cloud account. To verify the resources:

- Go to the [IBM Cloud dashboard](https://cloud.ibm.com/).
- Navigate to **Resource List** in the left panel.
- Check under the appropriate category (**Storage** in this case), or you can search for the prefix that was used for the deployment.

The module has been deployed successfully, and you can now see the resources on the dashboard. You’re all set to start using them.

## Clean-up the resources
{: #deploy-tim-module-lesson8-destroy}
{: step}


When the resources deployed are no longer needed, you can clean up your environment by removing everything Terraform created. Use the following command to perform this step:

```bash
terraform destroy
```

This will show a summary of the resources that will be removed. Once you confirm, Terraform will initiate delete requests for all resources managed by the module.

Cleaning up is important to avoid unnecessary charges for cloud resources and keeps your IBM Cloud account organized. Even small resources, like storage buckets, can accumulate costs over time.

## What you learned
{: #deploy-tim-module-learnings}

By completing this tutorial, you have:

- Learned how to provide values for input variables using the `terraform.tfvars` file.
- Practiced using essential Terraform CLI commands such as `init`, `plan` and `apply` to provision cloud resources using a [terraform-ibm-module](https://github.com/terraform-ibm-modules).

Although this tutorial used the Cloud Object Storage module as an example, these learnings apply to any Terraform IBM module, providing a reusable pattern you can apply across your infrastructure projects.
