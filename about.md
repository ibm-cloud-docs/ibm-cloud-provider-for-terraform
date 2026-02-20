---

copyright:
  years: 2017, 2025
lastupdated: "2025-05-27"

keywords: Terraform on IBM Cloud, Infrastructure as code, resources, what is Terraform on IBM Cloud, automation, automate, IaC

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# About Terraform on IBM Cloud
{: #about}

Infrastructure as Code (IaC) enables you to define, manage, and provision cloud resources — such as compute, network, and storage — using code instead of manual configuration through consoles or scripts. Terraform on IBM Cloud provides a powerful, automated approach to implement IaC. Using Terraform, you define your infrastructure using simple, declarative configuration files - while the platform takes care of deployment, updates, and lifecycle management, so you can focus on innovation.

## Two approaches to Terraform on IBM Cloud
{: #two-approaches}

IBM Cloud provides following two complementary approaches for implementing infrastructure as code with Terraform, each designed for different use cases and skill levels.

### 1. Terraform IBM Modules (TIM)
{: #approach-modules}

**Terraform IBM Modules** provide pre-built, open-source, enterprise-ready and secure-by-default building blocks that follow IBM Cloud best practices. They enable you to deploy robust architectures quickly while maintaining strong governance and reliability. This approach is ideal when you need:

- **Rapid deployment** - Get production-ready infrastructure quickly
- **Best practices built-in** - Security, compliance, and reliability by default
- **Composable architectures** - Combine modules to build complex solutions
- **Reduced maintenance** - Benefit from community updates and improvements
- **Consistency** - Standardize infrastructure across teams and projects

**Example use case:** Deploying a secure, multi-zone VPC with monitoring, logging, and encryption enabled using tested, validated modules.

**Get started:** [Working with Terraform IBM Modules](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about-tim)

### 2. IBM Cloud Provider Plug-in
{: #approach-provider}

The **IBM Cloud Provider Plug-in** gives you direct, fine-grained control over IBM Cloud resources using Terraform's native resource syntax. This approach is ideal when you need:

- **Maximum flexibility** - Define every aspect of your infrastructure
- **Custom configurations** - Build unique architectures not covered by pre-built modules
- **Learning Terraform** - Understand core Terraform concepts and IBM Cloud APIs
- **Granular control** - Manage individual resources with precise specifications

**Example use case:** Creating a custom VPC configuration with specific subnet layouts, security groups, and routing rules tailored to your organization's unique requirements.

**Get started:** [Learn more about the IBM Cloud Provider Plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about-ibm-cloud-provider-plugin)


### Which approach should you choose?
{: #choosing-approach}

The choice between Terraform IBM Modules and the IBM Cloud Provider Plug-in depends on your specific requirements, team expertise, and project goals. Use this guide to determine the best fit for your use case.

| Scenario | Recommended Approach |
|----------|---------------------|
| Learning Terraform and IBM Cloud | **Provider Plug-in** - Start with basics |
| Full control over Terraform resources | **Provider Plug-in** - Maximum flexibility |
| Deploying production workloads quickly | **Terraform IBM Modules** - Pre-validated solutions |
| Standardizing across teams | **Terraform IBM Modules** - Consistent patterns |
| Complex enterprise architectures | **Terraform IBM Modules** - Composable building blocks |
| Limited Terraform expertise | **Terraform IBM Modules** - Easier to learn |
| Specific compliance requirements | **Provider Plug-in** - Custom controls |

These approaches are not mutually exclusive. Many organizations use both - modules for common patterns and the provider plug-in for custom requirements.
{: tip}

## How does Terraform on IBM Cloud work?
{: #how-it-works}

[Terraform](https://developer.hashicorp.com/terraform){: external} enables you to specify your cloud infrastructure resources and services by using the high-level scripting HashiCorp Configuration Language (HCL). With HCL, you have one common language to declare the cloud resources that you want and the state that you want your resources to be in.

Let's say you want to spin up multiple copies of your cloud environment that uses a cluster of virtual servers, a load balancer, and a database server on {{site.data.keyword.cloud_notm}}. You could learn how to create each resource, review the API or the commands that you need, and write a bash script to spin up these components. But it's easier, faster, and more orderly to use one language to declare all your requirements, document them in a configuration file, and let Terraform on IBM Cloud do it all for you.

Based on your configuration, Terraform creates an execution plan and describes the actions that need to be executed to get to the required state. You can review the execution plan, change it, or simply execute the plan. When you change your configuration, Terraform on IBM Cloud can determine what changed and create incremental execution plans that you can apply to your existing {{site.data.keyword.cloud_notm}} resources.

## What are the benefits of using Terraform on IBM Cloud?
{: #abt-benefits}

Here are the key benefits of using Terraform to manage your IBM Cloud deployments.

|Benefit|Description|
|--|--|
|Codify your {{site.data.keyword.cloud_notm}} environment|Use a high-level scripting language to declare all the {{site.data.keyword.cloud_notm}} resources and services that you want. Instead of learning the API or command-line to work with a specific resource, you use  Terraform configuration files to specify the required state and resource configuration. Then, you use Terraform on IBM Cloud to rapidly build, configure, and replicate the resources in your cloud environments.|
|Automate cloud resource lifecycle|By using Terraform templates to build your cloud environment, you can orchestrate the provisioning, update, and deletion of your {{site.data.keyword.cloud_notm}} resources, and easily replicate your configuration across environments. |
|Enable Infrastructure as Code|By codifying your cloud environment, you can treat your Terraform templates the same way as you treat your app code. You can author your templates in any code editor, check them into a version control system such as GitHub, and let your team review and monitor updates before you apply these changes in your cloud environment. By applying these DevOps core practices, you can enable Infrastructure as Code (IaC) for your cloud environments.|
{: caption="Benefits" caption-side="top"}

## Key terms
{: #terms}

Learn about the key terms that are used in Terraform on IBM Cloud.

|Term|Description|
|--|--|
|{{site.data.keyword.cloud_notm}} Provider plug-in for Terraform|To support a multi-cloud approach, Terraform works with different cloud providers. A cloud provider is responsible for understanding the resources that you can provision, their API, and the methods to expose these resources in the cloud. To make this knowledge available to users, each cloud provider must provide a command-line plug-in for Terraform. The {{site.data.keyword.cloud_notm}} Provider plug-in is {{site.data.keyword.IBM_notm}}'s command-line plug-in for Terraform.|
|Data source|Data sources are Terraform objects that you can use to retrieve information about {{site.data.keyword.cloud_notm}} resources that you previously provisioned with Terraform on IBM Cloud. |
|Resource|Resources are Terraform objects that refer to IaaS, PaaS, or SaaS services that you can provision, update, or delete in {{site.data.keyword.cloud_notm}}. Typical examples include bare metal servers, virtual servers, auto scaling groups, load balancers, or non-infrastructure related services, such as Key Protect or Identity and Access Management (IAM) access policies. The resources that are supported in Terraform on IBM Cloud are defined by the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. |
|Terraform configuration file|A Terraform configuration file defines the {{site.data.keyword.cloud_notm}} resources that you want to create. You can configure one resource per file, or combine multiple resources in one file. Terraform configuration files can be written in HashiCorp Configuration Language (HCL) or JSON format, and are stored in a source code repository. For more information, about how to write configuration files, see [creating Terraform configurations](https://developer.hashicorp.com/terraform/language/syntax/configuration){: external}.|
|Terraform template|A Terraform template includes one or a set of Terraform configuration files that combined can be used to build a specific {{site.data.keyword.cloud_notm}} solution. For example, you might have a template that creates a multizone cluster in {{site.data.keyword.containerlong_notm}}. This cluster consists of multiple {{site.data.keyword.cloud_notm}} resources in different zones, such as classic infrastructure virtual servers and VLANs. Templates are designed and constructed for reuse by using variables so that you can share these templates with other teams in your organization.|
|Terraform execution plan|A Terraform execution plan is a summary of actions that Terraform on IBM Cloud must perform to provision, modify, or remove the {{site.data.keyword.cloud_notm}} resources of your template.|
 {: caption="Key terms" caption-side="top"}
