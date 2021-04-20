---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-20"

keywords: terraform quickstart, terraform getting started, terraform tutorial

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



# Getting started with Terraform on {{site.data.keyword.cloud_notm}}
{: #getting-started}

Terraform on {{site.data.keyword.cloud_notm}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} platform, classic infrastructure, and VPC infrastructure resources so that you can rapidly build complex, multi-tier cloud environments, and enable Infrastructure as Code (IaC). 
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud_notm}} solution? Try out [{{site.data.keyword.bplong_notm}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud_notm}} catalog.
{: tip}

## How does it work?
{: #it-works}

Let's say you want to spin up multiple copies of your service that uses a cluster of virtual servers, a load balancer, and a database server on the {{site.data.keyword.cloud}}. You could learn how to create each resource, review the API or the commands that you need, and write a bash script to spin up these components. But it's easier, faster, and more orderly to specify the type of resource that you want and let Terraform on {{site.data.keyword.cloud_notm}} do it all for you. 

The Terraform on {{site.data.keyword.cloud_notm}} configuration files describe the resources that you need and how you want to configure them. Based on your configuration, Terraform on {{site.data.keyword.cloud_notm}} creates an execution plan and describes the actions that need to be executed to get to the required state. You can review the execution plan, change it, or simply execute the plan. When you change your configuration, Terraform on {{site.data.keyword.cloud_notm}} can determine what changed and create incremental execution plans that you can apply to your existing {{site.data.keyword.cloud_notm}} resources. 

## What do I need to get started?
{: #prerequisite}

To provision {{site.data.keyword.cloud_notm}} infrastructure and platform resources, you must have a [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/registration).  

## What do I provision as part of this tutorial?
{: #get-start-tut}

In this getting started tutorial, you provision a [classic infrastructure virtual server](/docs/virtual-servers?topic=virtual-servers-about-public-virtual-servers) and a [VPC virtual server instance](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-getting-started). 

Both virtual server instances incur costs. Be sure to review the available plans for [classic infrastructure virtual servers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/infrastructure/virtual-server-group) and [VPC virtual server instances](https://cloud.ibm.com/vpc/provision/vs) before you proceed.
{: note}

Sounds great? Get started by [installing the Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#tf_installation) and [installing the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider). You can then configure the {{site.data.keyword.cloud_notm}} resources that you want and watch Terraform on {{site.data.keyword.cloud_notm}} spin them up. 

## What credentials do I need?
{: #req-credentials}

The credentials that you need depend on the type of resource that you want to provision. For example: 
- To provision classic infrastructure resources, you must provide your {{site.data.keyword.cloud_notm}} classic infrastructure user name and API key. 
- To provision VPC infrastructure, you need an {{site.data.keyword.cloud_notm}} API key. 

For more information, about what credentials you need for a specific {{site.data.keyword.cloud_notm}} resource, see [Required input parameters for each resource category](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters).

## Where can I find an overview of available resources?
{: #resource-availablity}

To find a full list of {{site.data.keyword.cloud_notm}} resources that you can provision with the {{site.data.keyword.cloud_notm}} Provider plug-in, see the [Index of  resources and data sources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-index-of-terraform-resources-and-data-sources).

To configure the {{site.data.keyword.cloud_notm}} provider plug-in with all the required parameters for the resource or data source category that you want to provision, see [configuring {{site.data.keyword.cloud_notm}} provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#configure_provider).


