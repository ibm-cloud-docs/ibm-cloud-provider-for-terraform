---

copyright:
  years: 2025
lastupdated: "2025-12-18"

keywords: Secure AI infrastructure, Terraform IBM Modules, TIM Modules, terraform-ibm-modules, Code Engine, COS, KMS, IaC, Infrastructure as Code, watsonx, AI

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Build Secure IBM Cloud Infrastructure with Terraform Modules for AI Applications
{: #secure-ai-infrastructure}
{: toc-content-type="tutorial"}
{: toc-services="terraform, terraform-ibm-modules, Code Engine, COS, KMS, Watsonx.ai"}
{: toc-completion-time="1h"}

This **IBM Cloud Terraform tutorial** shows how to compose and integrate reusable Terraform modules to build a secure, scalable **Infrastructure as Code** solution on IBM Cloud. You’ll provision, configure, and operate the Loan Risk AI Agents application while applying IaC best practices for automation, compliance, and observability.
{: shortdesc}

![Architectural diagram](images/IaC_diag.svg)
{: figure caption="Infrastructure as Code architecture composed of integrated IBM Cloud Terraform modules supporting the Loan Risk AI Agents application."}

The solution is built by **composing modular Terraform components**, each encapsulating a distinct IBM Cloud service. These modules are integrated through well-defined inputs and outputs to form a complete, secure, and repeatable **Infrastructure as Code deployment pattern**.

The application simulates a bank loan processing workflow where AI agents evaluate risk and determine interest rates. The source code is available at: https://github.com/IBM/ai-agent-for-loan-risk
{: note}

The deployment architecture uses these core components:

- **Application**: Built using LangGraph and TypeScript/Node.js
- **Compute**: IBM Cloud Code Engine - serverless platform for containerized workloads
- **AI Services**: watsonx.ai - foundation models for natural language processing
- **Storage**: Cloud Object Storage (COS) - unstructured data storage
- **Security**: Key Protect for encryption

## Before you begin
{: #tim-modules-ai-prereqs}

Before starting this tutorial, make sure you have the necessary tools, knowledge, and familiarity with IBM Cloud services. These prerequisites will help you follow along with provisioning infrastructure using Terraform modules and deploying the example Loan Risk AI Agents application.

* [Install the {{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started).
* [Install terraform CLI](https://developer.hashicorp.com/terraform/install).
* [Basic knowledge of Terraform syntax and workflows](https://developer.hashicorp.com/terraform/tutorials).
* [Understanding of IBM Cloud services](https://www.ibm.com/solutions/cloud).
* [IBM Cloud apikey](/docs/account?topic=account-userapikey&interface=ui) to access the IBM Cloud.
* [Familiar with the Loan Risk AI Agents application](https://github.com/IBM/ai-agent-for-loan-risk).

## Set up Terraform project structure for TIM-Based IaC
{: #tim-setup-project-structure}
{: step}

Before provisioning any resources, you need to set up a clean Terraform project structure. This ensures your infrastructure is modular, maintainable, and ready for TIM-based deployments.

### Create a new empty project folder
{: #tim-create-project-folder}
{: step}

Start by creating a dedicated folder for your Terraform project. This folder will contain all configuration files for your infrastructure deployment.

**In your terminal, run:**

```bash
mkdir my-terraform-project
cd my-terraform-project
```
{: pre}

### Create the necessary Terraform files
{: #tim-create-terraform-files}
{: step}

The project follows a standard Terraform layout, where each file serves a single purpose. This structure promotes clarity, reuse, and predictable behavior. Refer [this](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-understand-tim-structure) for more information.

```sh
.
├── main.tf            # Infrastructure components (modules & resources)
├── variables.tf       # Input variable definitions
├── outputs.tf         # Exported outputs
├── providers.tf       # Provider configuration
├── version.tf         # Terraform version constraints
└── terraform.tfvars   # Input values for deployment
```

You can create all the required files at once.

**In your terminal, run:**

```sh
touch main.tf variables.tf outputs.tf providers.tf version.tf terraform.tfvars
```
{: pre}

## Set up IBM Cloud provider
{: #tim-setup-ibmcloud-provider}
{: step}

Before you can provision any resources, Terraform needs to know **how to connect to IBM Cloud**. In this step, you will configure the IBM Cloud provider and specify required provider versions to ensure compatibility. This involves updating two files: `providers.tf` and `version.tf`.

### Configure the IBM Cloud and REST API providers
{: #secureai_configure-providers}
{: step}

The `providers.tf` file tells Terraform how to authenticate with IBM Cloud and interact with services. You also configure the REST API provider to allow API calls to external endpoints.

Add the following content to `providers.tf`:

```hcl
provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
  region           = var.region
}

provider "restapi" {
  uri                  = "https:"
  write_returns_object = true
  debug                = true
  headers = {
    Authorization = data.ibm_iam_auth_token.restapi.iam_access_token
    Content-Type  = "application/json"
  }
}
```
{: pre}

Make sure your IBM Cloud API key and region are defined as input variables in `variables.tf`.
{: note}

### Specify Terraform and provider versions
{: #secureai_terraform-version}
{: step}

The `version.tf` file ensures that Terraform uses the correct version and compatible provider versions for IBM Cloud and REST API.

Add the following content to `version.tf`:

```hcl
terraform {
  required_version = ">= 1.9.0"
  required_providers {
    ibm = {
      source  = "IBM-Cloud/ibm"
      version = ">= 1.80.4"
    }
    restapi = {
      source  = "Mastercard/restapi"
      version = ">= 1.19.1"
    }
  }
}
```
{: pre}

## Define input variables
{: #secureai_define-input-variables}
{: step}

To make your Terraform configuration **flexible and reusable**, you define input variables that allow you to manage sensitive information, environment-specific values, and configuration parameters outside of your main code. In this step, you will define the required variables `ibmcloud_api_key` and `prefix`, as well as the optional variables `watsonx_ai_api_key` and `region`, enabling different environments (dev, test, prod) to use the same Terraform code with different values.

Add the following content to `variables.tf`:

```hcl
variable "ibmcloud_api_key" {
  type        = string
  description = "The IBM Cloud API key."
  sensitive   = true
}

variable "watsonx_ai_api_key" {
  type        = string
  description = "The API key for IBM watsonx in the target account. If this key is not provided, the IBM Cloud API key will be used instead."
  sensitive   = true
  default     = null
}

variable "prefix" {
  type        = string
  description = "The prefix to be added to all resources name created by this solution."
}

variable "region" {
  type        = string
  description = "The IBM Cloud region to deploy resources in."
  default     = "us-south"
}
```
{: pre}

**Tip**: Required variables must be provided either via terraform.tfvars or environment variables. Optional variables can remain unset, in which case Terraform will use the default value.
{: note}


## Configure infrastructure components
{: #tim-configure-infra-components}
{: step}

In this step, you will build the **main Terraform configuration** that defines all the infrastructure components required to deploy the Loan Risk AI Agents application. The `main.tf` file orchestrates `resource groups`, `Code Engine project`, `secrets`, `builds`, `kms`, `cos` and the `application deployment`. All resources will use a **consistent naming prefix** (`${var.prefix}-`) to prevent naming conflicts and maintain uniformity across the deployment.

### Create a Resource Group (Foundation)
{: #secureai_create-resource-group}
{: step}

A **resource group** is a logical container for IBM Cloud resources used for organization, IAM access control, and lifecycle management.
This module typically acts as the **root dependency** for all other modules.

Add the following code to your `main.tf` file:

```hcl
module "resource_group" {
  source              = "terraform-ibm-modules/resource-group/ibm"
  version             = "1.4.0"
  resource_group_name = "${var.prefix}-resource-group"
}
```
{: pre}

For more information about this module, see the [terraform-ibm-resource-group documentation](https://github.com/terraform-ibm-modules/terraform-ibm-resource-group/blob/main/README.md).
{: note}

### Create a Code Engine Project
{: #tim-create-code-engine-project}
{: step}

Next, create a **Code Engine project** to host and manage the Loan Risk AI Agents sample application workloads in a serverless container environment. This project will serve as the deployment target for your containers.

Add the following code to your `main.tf` file:

```hcl
module "code_engine_project" {
  source            = "terraform-ibm-modules/code-engine/ibm//modules/project"
  version           = "4.5.1"
  name              = "${var.prefix}-ce-project"
  resource_group_id = module.resource_group.resource_group_id
}
```
{: pre}

For more information about this module, see the [terraform-ibm-code-engine-project documentation](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/project).
{: note}

### Create a Code Engine Secret
{: #tim-create-code-engine-secret}
{: step}

Create a **Code Engine secret** to grant access to the private container registry (`private.us.icr.io`), enabling the push of container images for the application. IBM Cloud Container Registry is the service that you can use to store and share your container images. This secret authenticates with the container registry during the build process.

Add the following code to your `main.tf` file:

```hcl
module "code_engine_secret" {
  source     = "terraform-ibm-modules/code-engine/ibm//modules/secret"
  version    = "4.5.1"
  name       = "${var.prefix}-registry-access-secret"
  project_id = module.code_engine_project.id
  format     = "registry"
  data = {
    "server"   = "private.us.icr.io",
    "username" = "iamapikey",
    "password" = var.ibmcloud_api_key,
  }
}
```
{: pre}

For more information about this module, see the [terraform-ibm-code-engine-secret documentation](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/secret).
{: note}

### Create a Container Registry namespace
{: #tim-create-container-registry-namespace}
{: step}

Create an **IBM Cloud Container Registry namespace**. This namespace organizes and stores the container images that will be used by the Code Engine project.

Add the following code to your `main.tf` file:

```hcl
module "namespace" {
  source            = "terraform-ibm-modules/container-registry/ibm"
  version           = "2.3.5"
  namespace_name    = "${var.prefix}-crn"
  resource_group_id = module.resource_group.resource_group_id
}
```
{: pre}

For more information about this module, see the [terraform-ibm-container-registry documentation](https://github.com/terraform-ibm-modules/terraform-ibm-container-registry/blob/main/README.md).
{: note}

### Create a Code Engine build to automatically build container image from source code
{: #tim-code-engine-build}
{: step}

This **Code Engine build** configuration builds a **container image from source code** hosted at [Loan Risk AI Agents repository](https://github.com/IBM/ai-agent-for-loan-risk) using the **Dockerfile** included in the repository. The build output is pushed to **IBM Cloud Container Registry** using the previously created **registry authentication secret**. The resulting **container image** serves as the **foundation for the AI application deployment**, enabling a **reproducible**, **automated**, and **build-from-source** workflow that integrates seamlessly with **Code Engine**

Key inputs:
- **source_url** – Git repository containing the AI application source code
- **strategy_type** – Uses the Dockerfile in the repository to build the image
- **output_secret** – References the secret created earlier for registry authentication
- **output_image** – Destination path in Container Registry for the built image

Add the following code to your `main.tf` file:

```hcl
locals {
  output_image = "private.us.icr.io/${module.namespace.namespace_name}/ai-agent-for-loan-risk"
}

module "code_engine_build" {
  source                     = "terraform-ibm-modules/code-engine/ibm//modules/build"
  version                    = "4.5.1"
  name                       = "${var.prefix}-ce-build"
  ibmcloud_api_key           = var.ibmcloud_api_key
  project_id                 = module.code_engine_project.id
  existing_resource_group_id = module.resource_group.resource_group_id
  source_url                 = "https://github.com/IBM/ai-agent-for-loan-risk"
  strategy_type              = "dockerfile"
  output_secret              = module.code_engine_secret.name
  output_image               = local.output_image
}
```
{: pre}

For more information about this module, see the [terraform-ibm-code-engine-build documentation](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/build).
{: note}

### Provision Key Protect and Customer-Managed Encryption Keys
{: #tim-key-protect}
{: step}

Create an **IBM Key Protect instance** and define a key ring with customer-managed encryption keys to secure Cloud Object Storage buckets and the watsonx.ai project.

Key inputs:
- **key_protect_instance_name** – Name of the Key Protect service instance
- **key_ring_name** – Logical container for organizing encryption keys
- **key_name** – Customer-managed root key used to encrypt COS and watsonx.ai resources
- **resource_group_id** – Resource group where the Key Protect instance is deployed
- **region** – Region where the Key Protect service is provisioned

Add the following code to your `main.tf` file:

```hcl
locals {
  key_ring_name = "${var.prefix}-cos-key-ring"
  key_name      = "${var.prefix}-cos-key"
}

module "key_protect_all_inclusive" {
  source                    = "terraform-ibm-modules/kms-all-inclusive/ibm"
  version                   = "5.5.5"
  key_protect_instance_name = "${var.prefix}-kp"
  resource_group_id         = module.resource_group.resource_group_id
  enable_metrics            = false
  region                    = var.region
  keys = [
    {
      key_ring_name = (local.key_ring_name)
      keys = [
        {
          key_name = (local.key_name)
        }
      ]
    }
  ]
  resource_tags = ["tutorial-tag"]
}
```
{: pre}

For more information about this module, see the [terraform-ibm-kms-all-inclusive documentation](https://github.com/terraform-ibm-modules/terraform-ibm-kms-all-inclusive/blob/main/README.md).
{: note}

### Create Cloud Object Storage with Key Protect Encryption
{: #tim-cos-key-protect}
{: step}

Provision a **Cloud Object Storage (COS)** instance and bucket, enabling encryption with customer-managed keys from the Key Protect service for secure storage of watsonx.ai project data.

Key inputs:
- **cos_instance_name**, **cos_plan**, **bucket_name** – COS instance and bucket configuration
- **kms_encryption_enabled** – Enable Key Protect encryption
- **existing_kms_instance_guid**, **kms_key_crn** – References to Key Protect keys
- **region**, **resource_group_id** – Deployment settings

Add the following code to your `main.tf` file:

```hcl
module "cos" {
  source  = "terraform-ibm-modules/cos/ibm"
  version = "10.7.2"
  resource_group_id = module.resource_group.resource_group_id
  region            = var.region
  cos_instance_name = "${var.prefix}-my-cos"
  cos_plan          = "standard"
  bucket_name       = "${var.prefix}-bucket"
  kms_encryption_enabled = true
  existing_kms_instance_guid = module.key_protect_all_inclusive.kms_guid
  kms_key_crn = module.key_protect_all_inclusive.keys["${local.key_ring_name}.${local.key_name}"].crn
}
```
{: pre}

For more information about this module, see the [terraform-ibm-cos documentation](https://github.com/terraform-ibm-modules/terraform-ibm-cos/blob/main/README.md).
{: note}

### Deploy watsonx.ai Project with COS Encryption
{: #tim-watsonx-ai-deployment}
{: step}

Create a **watsonx.ai project** with integrated **Cloud Object Storage (COS)** and **customer-managed encryption keys**. This project will securely store data for AI workloads and provide the project ID needed for deploying the Agentic AI agent.

**Key inputs:**
- **project_name** – Name of the watsonx.ai project
- **watsonx_ai_studio_plan** – Service plan for watsonx.ai Studio (e.g., `professional-v1`)
- **watsonx_ai_runtime_plan** – Service plan for runtime environments (e.g., `v2-professional`)
- **cos_instance_crn**, **cos_kms_key_crn**, **enable_cos_kms_encryption** – COS settings
- **resource_group_id**, **region** – Deployment settings

Add the following code to your `main.tf` file:

```hcl
data "ibm_iam_auth_token" "restapi" {
}

module "watsonx_ai" {
  source                    = "terraform-ibm-modules/watsonx-ai/ibm"
  version                   = "2.12.0"
  region                    = var.region
  resource_group_id         = module.resource_group.resource_group_id
  watsonx_ai_studio_plan    = "professional-v1"
  watsonx_ai_runtime_plan   = "v2-professional"
  project_name              = "${var.prefix}-wxai-project"
  enable_cos_kms_encryption = true
  cos_instance_crn          = module.cos.cos_instance_crn
  cos_kms_key_crn           = module.key_protect_all_inclusive.keys["${local.key_ring_name}.${local.key_name}"].crn
  skip_iam_authorization_policy = true
}
```
{: pre}

For more information about this module, see the [terraform-ibm-watsonx-ai documentation](https://github.com/terraform-ibm-modules/terraform-ibm-watsonx-ai/blob/main/README.md).
{: note}

### Create a Code Engine Application
{: #tim-code-engine-application}
{: step}

Deploy a **Code Engine application** to run the containerized Loan Risk AI Agents application as a scalable, serverless workload.

Key inputs:
- **image_reference** – Path to the container image built in the previous step
- **image_secret** – References the secret for registry access
- **run_env_variables** – Environment variables for watsonx integration

Add the following code to your `main.tf` file:

```hcl
module "code_engine_app" {
  depends_on      = [ module.code_engine_build ]
  source          = "terraform-ibm-modules/code-engine/ibm//modules/app"
  version         = "4.5.1"
  project_id      = module.code_engine_project.id
  name            = "${var.prefix}-ai-agent-for-loan-risk"
  image_reference = module.code_engine_build.output_image
  image_secret    = module.code_engine_secret.name
  run_env_variables = [{
    type  = "literal"
    name  = "WATSONX_AI_APIKEY"
    value = var.watsonx_ai_api_key != null ? var.watsonx_ai_api_key : var.ibmcloud_api_key  # Uses watsonx API key if provided, otherwise falls back to IBM Cloud API key for LLM inferencing
    },
    {
      type  = "literal"
      name  = "WATSONX_PROJECT_ID"
      value = module.watsonx_ai.watsonx_ai_project_id
    }
  ]
}
```
{: pre}

For more information about this module, see the [terraform-ibm-code-engine-application documentation](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/application).
{: note}

## Define outputs
{: #secureai_defineOutputs}
{: step}

Define output values to provide quick access to important resource information after deployment:

- **Resource Group ID** – For referencing in other services
- **Code Engine Project ID** – For managing workloads
- **Container Image URL** – For deployments
- **Application Route URL** – Public endpoint to access the application
- **watsonx.ai Project ID** – Required for AI agent integrations

Add the following content to `outputs.tf`:

```hcl
output "resource_group_id" {
 value       = module.resource_group.resource_group_id
 description = "The ID of the resource group."
}

output "ce_project_id" {
 value       = module.code_engine_project.id
 description = "The ID of the code engine project."
}

output "output_image" {
 value       = local.output_image
 description = "The URL of the container registry image"
}

output "app_url" {
 value       = module.code_engine_app.endpoint
 description = "The public endpoint to access the deployed loan application."
}

output "watsonx_ai_project_id" {
 value       = module.watsonx_ai.watsonx_ai_project_id
 description = "The ID of the created watsonx.ai project."
}
```
{: pre}

## Configure variables and deploy the infrastructure
{: #secureai_deploy-infrastructure}
{: step}

In this step, you will configure your environment-specific variables and deploy the complete infrastructure using Terraform. This includes initializing modules, previewing planned changes, and applying the configuration to provision resources in IBM Cloud.

For more details about TIM module deployments, see [Deploy TIM Module guide](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-deploy-tim-module) or learn more about deployment best practices.
{: note}

### Secure variables
{: #secureai_secure-variables}
{: step}

Create or update the `terraform.tfvars` file with your environment-specific values:

```hcl
ibmcloud_api_key             = "<your-IBM-cloud-api-key>"        # From IBM Cloud IAM
watsonx_ai_api_key           = "<your-watsonx-ai-api-key>"       # Optional
prefix                       = "<your-prefix>"                   # Define prefix to avoid naming conflicts
```
{: pre}

**Guidelines:**
1. Replace `<your-IBM-cloud-api-key>` with your actual IBM Cloud API key.
2. Replace `<your-prefix>` with a short, unique prefix for your resources.
3. Ensure this file is **not checked into source control** as it contains sensitive information.

### Deploy the infrastructure
{: #secureai_deployInfra}
{: step}

Open a terminal and run the following commands to deploy the infrastructure:

```bash
terraform init   # Initialize providers and modules
terraform plan   # Preview changes without applying
terraform apply  # Apply changes (type 'yes' when prompted)
```
{: pre}

This may take a few minutes. While waiting, you can explore the resources being created in the IBM Cloud console.
{: note}

Make sure you open these links in the target sandbox account:
- Code Engine Project section: https://cloud.ibm.com/containers/serverless/projects
  1. Click on your serverless project named `<your-initials>-ce-project`
  2. In the project dashboard, navigate to the **Image builds** section from the left-hand menu to view your build configuration
  3. Click on the build, then click **step-source-default** to see the logs of the AI app being built
  4. Once the build is done, navigate to the **Applications** section to view your application configuration. You should see the app starting to deploy, based on the docker image just built
  4. In the project dashboard, navigate to the **Secrets and configmaps** section to view your created secrets
- Resource Groups section: https://cloud.ibm.com/account/resource-groups


✅ **Success:** After the apply completes, your IBM Cloud resources will be successfully provisioned.
{: note}

**Access the deployed application**: Use the app_url output from terraform apply — it provides the public URL of the running Loan Risk AI Agents sample application. The app may take up to a minute to fully load after deployment..
{: note}

## Next steps — Verify and explore your deployment
{: #secureai-next-steps}
{: step}

After the Terraform apply completes, it’s important to verify that all resources have been correctly provisioned and are functioning as expected. This step guides you through exploring your IBM Cloud sandbox account to confirm deployment status.

### Explore Code Engine Project
{: #secureai-code-engine}
{: step}

Open the Code Engine Project section: [https://cloud.ibm.com/containers/serverless/projects](https://cloud.ibm.com/containers/serverless/projects)

1. Click on your serverless project named `<your-prefix>-ce-project`.
2. Navigate to the **Image builds** section to view your build configuration.
3. Click on the build, then **step-source-default** to see the logs of the AI app being built.
4. Once the build is complete, go to the **Applications** section to check that your app is starting.
5. Review the **Secrets and configmaps** section to confirm registry credentials and application secrets.

### Check Resource Groups
{: #secureai-resource-groups}
{: step}

Open the Resource Groups section: [https://cloud.ibm.com/account/resource-groups](https://cloud.ibm.com/account/resource-groups)

- Confirm that your resource group exists and that all associated resources are listed.

###  View all resources
{: #secureai-all-resources}
{: step}

Open the All Resources view: [https://cloud.ibm.com/resources](https://cloud.ibm.com/resources)

- Use your prefix in the search/filter to locate all deployed resources.
- Verify that each resource is provisioned according to your configuration.
