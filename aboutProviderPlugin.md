---

copyright:
  years: 2017, 2025
lastupdated: "2025-11-21"

keywords: Terraform on IBM Cloud, configuration files, resources, what is Terraform on IBM Cloud, automation, automate

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.terraform-provider_full}}
{: #about}

{{site.data.keyword.terraform-provider_full_notm}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} platform, classic infrastructure, and VPC infrastructure resources so that you can rapidly build complex, multitiered cloud environments, and enable Infrastructure as Code (IaC).
{: shortdesc}

## How does Terraform on IBM Cloud work?
{: #how-it-works}

[Terraform](https://developer.hashicorp.com/terraform){: external} is an open source project that lets you specify your cloud infrastructure resources and services by using the high-level scripting HashiCorp Configuration Language (HCL). With HCL, you have one common language to declare the cloud resources that you want and the state that you want your resources to be in.

Let's say you want to spin up multiple copies of your cloud environment that uses a cluster of virtual servers, a load balancer, and a database server on {{site.data.keyword.cloud_notm}}. You could learn how to create each resource, review the API or the commands that you need, and write a bash script to spin up these components. But it's easier, faster, and more orderly to use one language to declare all your requirements, document them in a configuration file, and let Terraform on IBM Cloud do it all for you.

### What is the {{site.data.keyword.cloud_notm}} Provider plug-in?
{: #provider-plugin-ov}

To abstract the APIs and complexity of the cloud resource provisioning and management process to the user, cloud providers create a plug-in for Terraform that contains the information for how to connect to the cloud provider and what APIs to call to work with a certain cloud resource. IBM's plug-in is called the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. The plug-in analyzes the resources that you specified and determines the order in which these resources must be provisioned, including any dependencies that must be considered.

### How does Terraform on IBM Cloud provision and manage cloud services?
{: #resource-lifecycle-ov}

To use Terraform on IBM Cloud, you must create a Terraform configuration file that describes the {{site.data.keyword.cloud_notm}} resources that you need and how you want to configure them. Based on your configuration, Terraform creates an execution plan and describes the actions that need to be executed to get to the required state. You can review the execution plan, change it, or simply execute the plan. When you change your configuration, Terraform on IBM Cloud can determine what changed and create incremental execution plans that you can apply to your existing {{site.data.keyword.cloud_notm}} resources.

The following points specifies how Terraform on IBM Cloud provisions your services in {{site.data.keyword.cloud_notm}}.

1. You declare the {{site.data.keyword.cloud_notm}} resources that you want in a Terraform configuration file by using HashiCorp Configuration Language (HCL). Store this configuration file in a source code repository that is version-controlled and that allows teams to collaborate, such as GitHub or GitLab.
2. Configure the {{site.data.keyword.cloud_notm}} Provider plug-in.
3. Create a Terraform execution plan that summarizes all the actions that Terraform needs to run to create, update, or delete the {{site.data.keyword.cloud_notm}} resources in your Terraform template.
4. Apply the Terraform configuration file in {{site.data.keyword.cloud_notm}}.

## What are the benefits of using Terraform on IBM Cloud?
{: #abt-benefits}

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
