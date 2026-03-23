---

copyright:
  years: 2025, 2026
lastupdated: "2026-03-23"

keywords: no-code, ibmcloud, infrastructure-as-code, terraform-ibm-modules, no-code and ibmcloud, terraform, hcp, waypoint, hashicorp

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: terraform, hcp, waypoint
account-plan:
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}

# Deploy Terraform IBM Modules using HashiCorp Cloud Platform (HCP) Waypoint
{: #deploy-tim-using-hcp-waypoint}
{: toc-content-type="tutorial"}
{: toc-services="terraform, hcp, waypoint"}
{: toc-completion-time="1h"}

A step-by-step guide to use IBM-supported [Terraform IBM Modules](https://registry.terraform.io/namespaces/terraform-ibm-modules){: external} to deploy and manage your infrastructure with HCP Waypoint.
{: shortdesc}

This tutorial shows you how to create infrastructure using secure [Terraform IBM Modules](https://github.com/terraform-ibm-modules){: external}, publish them to the [HCP Terraform Registry](https://registry.terraform.io/browse/modules){: external}, and enable them for No-Code provisioning. You also learn how to wrap the published module in a [Waypoint](https://www.hashicorp.com/products/waypoint){: external} template. This approach transforms complex infrastructure-as-code into a simple, form-driven experience. Developers can deploy approved infrastructure patterns independently while maintaining governance and security standards. Terraform IBM Modules ensure your infrastructure follows IBM Cloud best practices from the start.

The process involves three key steps: First, you create a configuration that composes Terraform IBM Modules. Next, you publish this configuration as a no-code module to the HCP Registry. Finally, you build a Waypoint template that enables developers to provision infrastructure through a simple form interface without writing code.

## Objectives
{: #waypoint_objectives}

In this tutorial, you learn to:

- **Prepare a no-code module:** Build a configuration that composes [Terraform IBM Modules](https://github.com/terraform-ibm-modules){: external} to define your infrastructure following IBM Cloud best practices and security standards.

- **Publish the no-code module:** Set up Version Control System (VCS) connections and versioning to publish the module to the HCP Terraform Registry with no-code provisioning enabled.

- **Build a Waypoint template:** Create a reusable Waypoint template that consumes the no-code module and defines the necessary input variables.

- **Provision infrastructure:** Enable developers to use the template to deploy infrastructure through a simple form interface without writing code.

## Audience
{: #waypoint-audience}

This tutorial is designed for platform engineers who create standardized templates or `golden paths` that allow application developers to self-serve infrastructure without writing code.

## Prerequisites
{: #waypoint-prerequisites}

Before you begin this tutorial, complete the following prerequisites:

1. An HCP account with HCP Waypoint enabled. For information about creating an account, see [HCP Account](https://developer.hashicorp.com/hcp/docs/hcp/create-account){: external}.
1. If you don't have one, create an {{site.data.keyword.cloud_notm}} [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration).


## Prepare a no-code module
{: #waypoint-no_code_module}
{: step}

This step explains how platform engineers prepare and publish a Terraform module to the HCP Registry, enabling self-service, no-code infrastructure provisioning.

### Create a configuration using Terraform IBM Modules
{: #waypoint-configure-a-root-module}
{: step}

Create a Terraform configuration that consumes Terraform IBM Modules and defines the infrastructure pattern for no-code provisioning. This configuration will be published to enable form-based deployment.

To create a configuration using Terraform IBM Modules, follow these steps:

1. **Create a Terraform configuration** that composes one or more [Terraform IBM Modules (TIM)](https://github.com/terraform-ibm-modules){: external} to define your infrastructure pattern. Your configuration acts as a wrapper that calls the underlying TIM modules with specific configurations tailored to your organization's requirements.

  * **Select appropriate Terraform IBM Modules** from the [Terraform IBM Modules GitHub organization](https://github.com/terraform-ibm-modules){: external} or the public [Terraform Registry](https://registry.terraform.io/namespaces/terraform-ibm-modules){: external}. These modules cover various IBM Cloud services including VPC, OpenShift, databases, security services, and more. Each module is designed with security and best practices in mind, ensuring your infrastructure follows IBM Cloud standards.

  * **Configure module inputs** by defining variables that expose the necessary parameters for your infrastructure pattern. This allows developers to customize deployments while maintaining the underlying secure architecture defined by the TIM modules.

1. **Store your configuration in version control** (such as GitHub, GitLab, or Bitbucket) to enable versioning, collaboration, and integration with HCP Terraform. Ensure your repository follows Terraform module structure conventions with proper documentation.

   For comprehensive examples of using Terraform IBM Modules, refer to the [Sample IaC Solutions](https://github.com/terraform-ibm-modules/sample-iac-solutions){: external}. These examples demonstrate end-to-end infrastructure patterns, such as deploying containerized applications on OpenShift within a secure landing zone architecture that includes VPC networking, security groups, observability services, and key management. Each example shows how multiple TIM modules work together to create production-ready infrastructure following IBM Cloud best practices. {: tip}

Your configuration is now ready to be published to the HCP Terraform Registry, where it can be enabled for no-code provisioning and consumed through Waypoint templates.

### Publish a no-code module
{: #waypoint_publish-a-code}
{: step}

To publish your configuration as a **no-code module** in the HCP Terraform Registry, follow these steps:

1. Go to the **Registry** section in your HCP Terraform environment and open the **Modules** tab.
2. Click **Publish**, then choose **Module**.
3. Connect to VCS: On the Add Module screen, select **GitHub App** (or your preferred VCS).
4. Select Repository:
    * Choose your **Organization** and the repository containing the Terraform IBM module.
    * Set **Module Publishing Type** to **Branch**.
    * Enter the **Branch Name** (for example, `main`) and the **Module Version** (for example, `1.0.0`).
    * Provide a **Source Directory** if the module isn’t at the repo root.
    * Click **Next**.
5. Finalize:
    * Enter a **Module Name** (for example, `my-infrastructure`).
    * Specify the **Provider Name** `ibm`.
    * Enable **No-code provisioning** by selecting **Add Module to no-code provision allowlist**.
    * Click **Publish Module**.
6. After a brief build period, the module’s detail page will show it is fully **no-code ready module**.


## Build a Waypoint template
{: #waypoint_template}
{: step}

After publishing your no-code module, create a Waypoint template that uses it. This template serves as the self-service interface for developers to deploy infrastructure.


1. Open the **Waypoint** section in your HCP environment.
2. From the **Default project** (or your chosen project), click **Create template**.
3. Choose Terraform Module:
    * Set the **Template name** (for example, `my-infrastructure`).
    * Add a **Summary** (for example, `Creates infrastructure using Terraform IBM Modules`).
    * Select the **No-Code Module** you published (`my-infrastructure (ibm) – Version 1.0.0`).
    * Choose the **HCP Terraform Project** (`Default Project`).
    * Set the required **Input Variables** (for example, `prefix`, `region`) and optionally allow developers to enter values when creating applications.
    * Click **Next**.
4. Define Template Metadata:
    * Add a detailed **Description** (for example, pulled from the module's README).
    * Provide **Developer Instructions**.
    * Add **Labels** (for example, `waypoint-test`).
    * Under **Advanced settings**, verify the **Execution mode** (for example, **Agent**).
    * Click **Publish**.
5. Your new template will appear in the Waypoint **Templates** list.


## Provision an application infrastructure via Waypoint
{: #waypoint_application}
{: step}

With the Waypoint template in place, application developers can now self-serve infrastructure without writing any Terraform code. They simply complete a form with their application requirements, and Waypoint handles the provisioning automatically using your pre-approved infrastructure pattern.

1. In Waypoint, open **Applications** and click **+ Create an application**.
2. Select template:
    * Choose the template you created (`my-infrastructure`).
    * Click **Next**.
3. Configure the application:
    * Enter an **Application Name** (for example, `sample-app`).
    * Provide the required **Input variables** (`prefix: sample-app`, `region: au-syd`).
    * Click **Create application**.
4. Provisioning:
    * Waypoint creates the application and triggers a run in the linked HCP Terraform workspace.
    * You’ll be taken to the run overview as it moves through **Plan** and **Apply**, deploying the IBM resources defined in your module.
5. Once the apply completes, the infrastructure is fully deployed and the application status shows **Running**.


## Next steps
{: #deploytim-hcpwp-next-steps}
{: step}

- Learn more about the [Terraform IBM Cloud Provider](https://github.com/IBM-Cloud/terraform-provider-ibm).
- Explore available [Terraform IBM Modules](https://github.com/terraform-ibm-modules).
- [Use an add-on to deploy supporting infrastructure](https://developer.hashicorp.com/hcp/docs/waypoint/addon-use).
- Learn more about the [Agents](https://developer.hashicorp.com/hcp/docs/waypoint/concepts/agents).

## Related links
{: #waypointrelated-links}

- [HCP Waypoint](https://developer.hashicorp.com/hcp/docs/waypoint)
- [Templates](https://developer.hashicorp.com/hcp/docs/waypoint/concepts/templates)
- [Add-ons](https://developer.hashicorp.com/hcp/docs/waypoint/concepts/add-ons)
