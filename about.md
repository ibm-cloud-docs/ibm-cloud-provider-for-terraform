---

copyright:
  years: 2017, 2021
lastupdated: "2021-05-20"

keywords: Terraform on {{site.data.keyword.cloud_notm}}, configuration files, resources, what is Terraform on {{site.data.keyword.cloud_notm}}, automation, automate

subcollection: ibm-cloud-provider-for-terraform

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# About Terraform on {{site.data.keyword.cloud_notm}}
{: #about}

Terraform on {{site.data.keyword.cloud_notm}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} platform, classic infrastructure, and VPC infrastructure resources so that you can rapidly build complex, multi-tier cloud environments, and enable Infrastructure as Code (IaC).
{: shortdesc}

## How does Terraform on {{site.data.keyword.cloud_notm}} work? 
{: #how-it-works}

[Terraform](https://www.terraform.io/){: external} is an open source project that lets you specify your cloud infrastructure resources and services by using the high-level scripting HashiCorp Configuration Language (HCL). With HCL, you have one common language to declare the cloud resources that you want and the state that you want your resources to be in. 
 
Let's say you want to spin up multiple copies of your cloud environment that uses a cluster of virtual servers, a load balancer, and a database server on {{site.data.keyword.cloud_notm}}. You could learn how to create each resource, review the API or the commands that you need, and write a bash script to spin up these components. But it's easier, faster, and more orderly to use one language to declare all your requirements, document them in a configuration file, and let Terraform on {{site.data.keyword.cloud_notm}} do it all for you. 

### What is the {{site.data.keyword.cloud_notm}} Provider plug-in?
{: #provider-plugin-ov}

In order to abstract the APIs and complexity of the cloud resource provisioning and management process to the user, cloud providers create a plug-in for Terraform that contains the information for how to connect to the cloud provider and what APIs to call to work with a certain cloud resource. IBM's plug-in is called the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. The plug-in analyzes the resources that you specified and determines the order in which these resources must be provisioned, including any dependencies that must be considered. 

### How does Terraform on {{site.data.keyword.cloud_notm}} provision and manage cloud services?
{: #resource-lifecycle-ov}

To use Terraform on {{site.data.keyword.cloud_notm}}, you must create a Terraform configuration file that describes the {{site.data.keyword.cloud_notm}} resources that you need and how you want to configure them. Based on your configuration, Terraform creates an execution plan and describes the actions that need to be executed to get to the required state. You can review the execution plan, change it, or simply execute the plan. When you change your configuration, Terraform on {{site.data.keyword.cloud_notm}} can determine what changed and create incremental execution plans that you can apply to your existing {{site.data.keyword.cloud_notm}} resources. 



## What are the benefits of using Terraform on {{site.data.keyword.cloud_notm}}?

|Benefit|Description|
|--|--|
|Codify your {{site.data.keyword.cloud_notm}} environment|Use a high-level scripting language to declare all the {{site.data.keyword.cloud_notm}} resources and services that you want. Instead of learning the API or command-line to work with a specific resource, you use  Terraform configuration files to specify the required state and resource configuration. Then, you use Terraform on {{site.data.keyword.cloud_notm}} to rapidly build, configure, and replicate the resources in your cloud environments.|
|Automate cloud resource lifecycle|By using Terraform templates to build your cloud environment, you can orchestrate the provisioning, update, and deletion of your {{site.data.keyword.cloud_notm}} resources, and easily replicate your configuration across environments. |
|Enable Infrastructure as Code|By codifying your cloud environment, you can treat your Terraform templates the same way as you treat your app code. You can author your templates in any code editor, check them into a version control system such as GitHub, and let your team review and monitor updates before you apply these changes in your cloud environment. By applying these DevOps core practices, you can enable Infrastructure as Code (IaC) for your cloud environments.|

## Key terms
{: #terms}

Learn about the key terms that are used in Terraform on {{site.data.keyword.cloud_notm}}.

|Term|Description|
|--|--|
|{{site.data.keyword.cloud_notm}} Provider plug-in for Terraform|To support a multi-cloud approach, Terraform works with different cloud providers. A cloud provider is responsible for understanding the resources that you can provision, their API, and the methods to expose these resources in the cloud. To make this knowledge available to users, each cloud provider must provide a command-line plug-in for Terraform. The {{site.data.keyword.cloud_notm}} Provider plug-in is IBM's command-line plug-in for Terraform.|
|Data source|Data sources are Terraform objects that you can use to retrieve information about {{site.data.keyword.cloud_notm}} resources that you previously provisioned with Terraform on {{site.data.keyword.cloud_notm}}. |
|Resource|Resources are Terraform objects that refer to IaaS, PaaS, or SaaS services that you can provision, update, or delete in {{site.data.keyword.cloud_notm}}. Typical examples include bare metal servers, virtual servers, auto-scaling groups, load balancers, or non-infrastructure related services, such as Key Protect or Identity and Access Management (IAM) access policies. The resources that are supported in Terraform on {{site.data.keyword.cloud_notm}} are defined by the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. |
|Terraform configuration file|A Terraform configuration file defines the {{site.data.keyword.cloud_notm}} resources that you want to create. You can configure one resource per file, or combine multiple resources in one file. Terraform configuration files can be written in HashiCorp Configuration Language (HCL) or JSON format, and are stored in a source code repository. For more information, about how to write configuration files, see [creating Terraform configurations](https://www.terraform.io/docs/language/syntax/configuration.html){: external}.|
|Terraform template|A Terraform template includes one or a set of Terraform configuration files that combined can be used to build a specific {{site.data.keyword.cloud_notm}} solution. For example, you might have a template that creates a multizone cluster in {{site.data.keyword.containerlong_notm}}. This cluster consists of multiple {{site.data.keyword.cloud_notm}} resources in different zones, such as classic infrastructure virtual servers and VLANs. Templates are designed and constructed for reuse by using variables so that you can share these templates with other teams in your organization.|
|Terraform execution plan|A Terraform execution plan is a summary of actions that Terraform on {{site.data.keyword.cloud_notm}} must perform to provision, modify, or remove the {{site.data.keyword.cloud_notm}} resources of your template.|





