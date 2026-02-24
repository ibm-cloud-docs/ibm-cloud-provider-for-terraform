---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-20"

keywords: Terraform IBM Modules, Deploy a Terraform IBM Module, terraform module deployment

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Deploy a Terraform IBM Module using Terraform CLI
{: #deploy-tim-module}
{: toc-content-type="tutorial"}
{: toc-services="cos"}


In this tutorial, you will learn how to deploy a terraform-ibm-module (TIM) module using Terraform CLI. It will cover how variables are defined and passed, which CLI commands drive the process, and demonstrate the workflow with IBM Cloud Object Storage (COS) as an example.


## Objectives
{: #deploy-tim-module-objectives}

By the end of this tutorial, you will learn to deploy and manage resources on IBM Cloud by using a Terraform IBM Module.

While this tutorial uses the [Cloud Object Storage module](https://github.com/terraform-ibm-modules/terraform-ibm-cos) as an example, you can apply these techniques to any Terraform IBM Module.

## Prerequisites
{: #deploy-tim-module-prerequisites}

Before you get started, make sure you have:

- [Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) installed.
- [IBM Cloud apikey](/docs/account?topic=account-userapikey&interface=ui) to access the IBM Cloud.


## Analyze the code
{: #deploy-tim-module-lesson1-code}
{: step}

The Terraform IBM module provides reusable infrastructure code for IBM Cloud resources. You can find the Cloud Object Storage module code in the [terraform-ibm-cos repository](https://github.com/terraform-ibm-modules/terraform-ibm-cos){: external}.

The repository contains:
1. **Module source code**: The core Terraform configuration files
2. **Examples directory**: Reference implementations showing different use cases
3. **Documentation**: Variable definitions, outputs, and usage guidelines
 
See [Understanding the Terraform IBM Module Structure](/docs/ibm-cloud-provider-for-terraform/ibm-cloud-provider-for-terraform-understand-tim-structure) for more details.

## Create your configuration
{: #deploy-tim-module-lesson2-configuration}
{: step}

To deploy infrastructure using this module, you need to write your own Terraform configuration that references the module. Follow these steps:

### Review the examples

Explore the `examples/` directory to understand how the module can be used. Each example is a complete, runnable Terraform configuration. It demonstrates:

- Module configuration with specific parameters
- Required variable values
- Integration patterns with other resources

### Write your code

Create a new Terraform project directory and write your own Terraform configuration file that invokes this module. For guidance, refer to the [usage section](https://github.com/terraform-ibm-modules/terraform-ibm-cos/?tab=readme-ov-file#terraform-ibm-cos){: external}.


## Define variables
{: #deploy-tim-module-lesson3-configure}
{: step}

Once you have written your Terraform configuration, the next step is to set up your variables. The input variables are declared in `variables.tf`. You can [set input variables](https://developer.hashicorp.com/terraform/language/values/variables#manage-variables-in-hcp-terraform){: external} by setting environment variables, passing them as command-line arguments, defining them directly in variables.tf or specifying them in `terraform.tfvars`.


This tutorial uses the `terraform.tfvars` file to provide values for the input variables. Create a new file named `terraform.tfvars` and add variables as shown below.

```hcl
ibmcloud_api_key = "<your-api-key>"
prefix = "tf-demo" # you can choose a prefix of your choice
region = "us-south"
...
```

Review the input variables in your code and update `terraform.tfvars` to override any default values that don't align with your requirements.

Never commit this file if it contains your `ibmcloud_api_key`, as it exposes sensitive credentials. You can also set the value safely by using a `TF_VAR_ibmcloud_api_key` environment variable instead.
{: note}

## Initialize Terraform
{: #deploy-tim-module-lesson4-init}
{: step}

The `terraform init` command initializes Terraform in the working directory. It reads the backend configuration from your files to download and install the required provider plugins and the modules.

```bash
terraform init
```

## Generate execution plan
{: #deploy-tim-module-lesson5-plan}
{: step}

The `terraform plan` command generates an execution plan that provides a preview of the changes Terraform intends to make to your infrastructure based on your configuration files, allowing you to review and verify the proposed changes. To generate this execution plan, run the following command:

```bash
terraform plan
```

Review the output of the plan and make any necessary changes to your configuration files before proceeding to the next step.

## Deploy the resources
{: #deploy-tim-module-lesson6-deploy}
{: step}

The `terraform apply` command deploys the resources specified in your configuration files to your IBM Cloud account. To deploy these resources, run the following command:

```bash
terraform apply
```

Approve the deployment when prompted, by typing `yes`. Alternatively, you may use `terraform apply -auto-approve` to automatically approve the changes.

If you confirm, Terraform starts provisioning all resources defined in the execution plan. This step may take some time depending on the configuration.

You can also save the execution plan in a file called `tfplan` by using `terraform plan -out=tfplan`  and then run `terraform apply tfplan` to execute the infrastructure changes specified in the saved plan file.
{: tip}

## Verify the deployed resources
{: #deploy-tim-module-lesson7-verify}
{: step}

After Terraform completes applying the configuration, verify that the resources have been successfully created in your IBM Cloud account. To verify if the resources are deployed properly,

- Go to the [IBM Cloud dashboard](https://cloud.ibm.com/).
- Navigate to **Resource List** in the left panel.
- Check under the appropriate category (**Storage** in this case), or you can search for the prefix used for the deployment.

The infrastructure has been deployed successfully, and the resources are now visible on the dashboard. You’re all set to start using them.

## Clean-up the resources
{: #deploy-tim-module-lesson8-destroy}
{: step}

When the resources deployed are no longer needed, you can clean up your environment by removing everything Terraform created. Cleaning up is important to avoid unnecessary charges for cloud resources and keeps your IBM Cloud account organized. Even small resources, like storage buckets, can accumulate costs over time. To delete the resources, run the following command:

```bash
terraform destroy
```

This displays a summary of the resources that will be removed. If you confirm, Terraform proceeds to delete all resources managed by the module.


## Next steps
{: #deploy-tim-module-next-steps}

You have now completed the deployment of a Terraform module - Cloud Object Storage. You can now explore other [modules](https://registry.terraform.io/search/modules?q=terraform-ibm-modules){: external} to deploy more resources in your IBM Cloud account according to your business needs.
