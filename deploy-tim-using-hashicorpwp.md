---

copyright:
  years: 2025, 2025
lastupdated: "2025-12-15"

keywords: no-code, ibmcloud, infrastructure-as-code, terraform-ibm-modules, no-code and ibmcloud, terraform, hcp, waypoint, hashicorp

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: terraform, hcp, waypoint
account-plan: 
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}

# Deploy Terraform IBM Modules using HashiCorp Cloud Platform (HCP) Waypoint
{: #DeployTIMUsingHashiCorpWP}
{: toc-content-type="tutorial"}
{: toc-services="terraform, hcp, waypoint"}
{: toc-completion-time="1h"}

A step-by-step guide to use IBM-supported [Terraform IBM Modules](https://registry.terraform.io/namespaces/terraform-ibm-modules){: external} to deploy and manage your infrastructure with HCP Waypoint.
{: shortdesc}

This tutorial walks you through publishing Terraform IBM Modules to the HCP Terraform Registry and explicitly enabling them for No-Code provisioning. It also shows how to wrap the published module in a Waypoint Template. This method simplifies complex infrastructure-as-code into an easy, form-driven experience, allowing developers to deploy approved infrastructure patterns independently while preserving governance and standardization.

## Objectives 
{: #objectives}

In this tutorial, you will:

- Adjust Terraform IBM Modules: Configure a [Terraform IBM Module](https://github.com/terraform-ibm-modules){: external} for use in the registry by updating source references and validating the module structure.

- Publish to the HCP Registry: Set up Version Control System(VCS) connections and versioning to publish the module to the HCP Terraform Registry with No-Code provisioning enabled.

- Create a Waypoint Template: Build a reusable Waypoint template that consumes the No-Code module and defines the necessary input variables.

- Provision Infrastructure: Developers use these standardized templates to deploy their applications without needing to manage the underlying infrastructure.

## Audience
{: #audience}

This tutorial is designed for Platform Engineers who create standardized 'golden paths' that allow Application Developers to self-serve infrastructure without needing to write any code.

## Prerequisites
{: #prerequisites}

1. An HCP account with HCP Waypoint enabled. Refer to [HCP Account](https://developer.hashicorp.com/hcp/docs/hcp/create-account){: external} for information about creating an account.
2. If you do not have one, create an {{site.data.keyword.cloud_notm}} [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration). 
3. Make sure that you have an existing {{site.data.keyword.redhat_notm}} account that has an [active OpenShift subscription](https://access.redhat.com/products/red-hat-openshift-container-platform){: external}. 


## No-Code Terraform Module
{: #no_code_module}
{: step}

This step explains how Platform Engineers prepare and publish a Terraform module to the HCP Registry, enabling self-service, no-code infrastructure provisioning.

### Create a Root Module from an Existing Example

Instead of designing a new module from scratch, use an existing example configuration to create a standalone root module suitable for No-Code provisioning.

1.  Fork or copy the repository

    On GitHub, fork the [`terraform-ibm-base-ocp-vpc`](https://github.com/terraform-ibm-modules/terraform-ibm-base-ocp-vpc) repo (or clone it directly if you're working internally).

2.  Clone your fork or repo locally (or in a GitHub Codespace/Workspace):

    ```bash
    git clone https://github.com/terraform-ibm-modules/terraform-ibm-base-ocp-vpc.git
    cd terraform-ibm-base-ocp-vpc/examples/basic
    ```
    {: pre}

3.  Update the example to consume the module from the Terraform Registry

    In the example’s `main.tf`, **remove the local module source line** and **uncomment/use the registry-based source lines**. This converts the example into a consumer of the published module:

    ```hcl
    # Remove the local source reference line
    # source = "../../"

    # Uncomment the following lines to consume the module from the registry
    source  = "terraform-ibm-modules/base-ocp-vpc/ibm"
    version = "X.Y.Z" # Replace X.Y.Z with the specific released version you want to pin
    ```
    {: pre}

4.  Modify the example configuration to your needs

    Adjust variables, provider configuration, resource group, region, or any other inputs in the example files under `examples/basic` so they reflect your use case.

5.  Commit and push your changes:


    ```bash
    git add .
    git commit -m "Update example to use registry module and customize configuration"
    git push origin main
    ```
    {: pre}

    *(Or push to a feature branch, depending on your workflow.)*

6.  Your module is now ready for publishing and consumption.

### Publish a No-Code Terraform Module
Start by publishing your Terraform IBM module as a **No-Code Module** in the HCP Terraform Registry. This allows developers to provision infrastructure without writing Terraform themselves.

1.  Go to the **Registry** section in your HCP Terraform environment and open the **Modules** tab.
2.  Click **Publish**, then choose **Module**.
3.  Connect to VCS: On the Add Module screen, select **GitHub App** (or your preferred VCS).
4.  Select Repository:
    * Choose your **Organization** and the repository containing the Terraform IBM module.
    * Set **Module Publishing Type** to **Branch**.
    * Enter the **Branch Name** (e.g., `main`) and the **Module Version** (e.g., `1.0.0`).
    * Provide a **Source Directory** if the module isn’t at the repo root.
    * Click **Next**.
5.  Finalize:
    * Enter a **Module Name** (e.g., `openshift`).
    * Specify the **Provider Name** `ibm`.
    * Enable **No-code provisioning** by selecting **Add Module to no-code provision allowlist**.
    * Click **Publish Module**.
6.  After a brief build period, the module’s detail page will show it is fully **No-Code enabled**.


## Build a Waypoint Template
{: #waypoint_template}
{: step}

After publishing your no-code module, create a Waypoint Template that uses it. This template serves as the self-service interface for developers to deploy infrastructure.
{: shortdesc}

1.  Open the **Waypoint** section in your HCP environment.
2.  From the **Default project** (or your chosen project), click **Create template**.
3.  Choose Terraform Module:
    * Set the **Template name** (e.g., `openshift`).
    * Add a **Summary** (e.g., `Creates a basic OpenShift cluster in a VPC`).
    * Select the **No-Code Module** you published (`openshift (ibm) – Version 1.0.0`).
    * Choose the **HCP Terraform Project** (`Default Project`).
    * Set the required **Input Variables** (e.g., `prefix`, `region`) and optionally allow developers to enter values when creating applications.
    * Click **Next**.
4.  Define Template Metadata:
    * Add a detailed **Description** (e.g., pulled from the module’s README).
    * Provide **Developer Instructions**.
    * Add **Labels** (e.g., `waypoint-test`).
    * Under **Advanced settings**, verify the **Execution mode** (e.g., **Agent**).
    * Click **Publish**.
5.  Your new template will appear in the Waypoint **Templates** list.


## Provision an Application via Waypoint
{: #waypoint_application}
{: step}

Developers can now use your template to deploy their infrastructure through Waypoint.
{: shortdesc}

1.  In Waypoint, open **Applications** and click **+ Create an application**.
2.  Select Template:
    * Choose the template you created (`openshift`).
    * Click **Next**.
3.  Configure the Application:
    * Enter an **Application Name** (e.g., `sample-app`).
    * Provide the required **Input variables** (`prefix: sample-app`, `region: au-syd`).
    * Click **Create application**.
4.  Provisioning:
    * Waypoint creates the application and triggers a run in the linked HCP Terraform workspace.
    * You’ll be taken to the run overview as it moves through **Plan** and **Apply**, deploying the IBM resources defined in your module.
5.  Once the apply completes, the infrastructure is fully deployed and the application status shows **Running**.


## Next steps
{: #next-steps}

- Learn more about the [Terraform IBM Cloud Provider](https://github.com/IBM-Cloud/terraform-provider-ibm).
- Explore available [Terraform IBM Modules](https://github.com/terraform-ibm-modules).
- [Use an add-on to deploy supporting infrastructure](https://developer.hashicorp.com/hcp/docs/waypoint/addon-use).
- Learn more about the [Agents](https://developer.hashicorp.com/hcp/docs/waypoint/concepts/agents).

## Related links
{: #related-links}

- [HCP Waypoint](https://developer.hashicorp.com/hcp/docs/waypoint)
- [Templates](https://developer.hashicorp.com/hcp/docs/waypoint/concepts/templates)
- [Add-ons](https://developer.hashicorp.com/hcp/docs/waypoint/concepts/add-ons)
