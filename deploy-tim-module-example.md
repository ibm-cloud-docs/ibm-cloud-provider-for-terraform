---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-24"

keywords: Terraform IBM Modules, Deploy a Terraform IBM Module, terraform module deployment, TIM example, deploy TIM example

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Deploy a VPC using an example
{: #deploy-tim-module-example}
{: toc-content-type="how-to"}
{: toc-services="vpc"}

This tutorial walks you through the process of deploying an example provided within a Terraform module. By working with an existing example, you can quickly understand the module’s core capabilities, explore how it integrates with other modules, and observe its behavior in a real deployment.

This helps you build a understanding of the Terraform module to enable you to create your own customized configuration.

## Objectives
{: #deploy-tim-module-example-objectives}

By the end of this exercise, you will learn to:
- Set variable values using a .tfvars file
- Deploy and manage the deployed resources

While this tutorial uses the [VPC module](https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone-vpc) as an example, the steps will be same for all other Terraform IBM modules.

## Before you begin
{: #deploy-tim-module-example-prerequisites}

Before you begin, ensure you have the following:
- [Git CLI](https://git-scm.com/install/) installed.
- [Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli).
- [IBM Cloud apikey](/docs/account?topic=account-userapikey&interface=ui) to access the IBM Cloud.

## Steps
{: #deploy-tim-module-example-steps}

Proceed with the following steps to deploy the example from the TIM module.


### Clone the repository
{: #deploy-tim-module-example-clone}
{: step}

Clone the repository using the `git clone` command.

```bash
git clone https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone-vpc.git
```

This tutorial uses the `basic` example deployment for simplicity and clarity. Navigate to the example directory.

```bash
cd terraform-ibm-landing-zone-vpc/examples/basic
```

This example provisions the following resources:
- A new resource group (if an existing resource group isn't provided)
- An IBM Virtual Private Cloud (VPC) with publicly exposed subnet and custom security group rules.


### Define the variables
{: #deploy-tim-module-example-cli-variables}
{: step}

Create a new file named `terraform.tfvars` in the basic folder. Open the file in a text editor. Add these required variables in the file:

```hcl
ibmcloud_api_key = "<your-api-key>"
prefix = "tf-demo" # you can choose a prefix of your choice
region = "us-south"
```

Never commit this file if it contains your `ibmcloud_api_key`, as it exposes sensitive credentials. You can also set the value safely by using a `TF_VAR_ibmcloud_api_key` environment variable instead.
{: note}

### Initialize Terraform
{: #deploy-tim-module-example-cli-init}
{: step}

The `terraform init` command initializes Terraform in the working directory (`examples/basic`). It reads the backend configuration from your files to download and install the required provider plugins and the modules. To initialize Terraform, run the following command:

```bash
terraform init
```

### Generate execution plan
{: #deploy-tim-module-example-cli-plan}
{: step}

The `terraform plan` command generates and displays the execution plan for you to review and verify the proposed changes. To view this execution plan, run the following command,

```bash
terraform plan
```

### Deploy the resources
{: #deploy-tim-module-example-cli-deploy}
{: step}

Run the following command to begin the deployment:

```bash
terraform apply
```

Approve the deployment when prompted, by typing `yes`. Alternatively, you may use `terraform apply -auto-approve` to automatically approve the changes.
Once confirmed, Terraform will begin provisioning all resources defined in the execution plan. This step make take some time depending on the configuration.

### Verify the deployed resources
{: #deploy-tim-module-example-cli-verify}
{: step}

To verify the resources:

- Go to the [IBM Cloud dashboard](https://cloud.ibm.com/).
- Navigate to **Resource List** in the left panel.
- Check under the appropriate category (**Virtual Private Cloud** in this case), or you can search for the prefix that was used for the deployment.

You’re all set to start the deployed infrastructure.

### Clean-up the resources
{: #deploy-tim-module-example-cli-destroy}
{: step}


When the resources deployed are no longer needed, you can clean up your environment by removing everything Terraform created. Use the following command to perform this step:

```bash
terraform destroy
```

This displays a summary of the resources that will be removed. If you confirm, Terraform proceeds to delete all resources managed by the module.

## Conclusion
{: #deploy-tim-module-example-conclusion}

Congratulations! You have successfully deployed the IBM Cloud VPC using the example.

You’re now ready to use the example code as a foundation for building your own configuration, complete with your own customizations. To learn more, refer to the [tutorial](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-deploy-tim-module) provided.
