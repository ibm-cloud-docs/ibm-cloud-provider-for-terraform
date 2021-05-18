---

copyright:
  years: 2017, 2021
lastupdated: "2021-05-18"

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

In this tutorial, you use Terraform on {{site.data.keyword.cloud_notm}} to create an {{site.data.keyword.keymanagementservicelong}} instance. With {{site.data.keyword.keymanagementserviceshort}}, you can create encrypted keys that you can use to secure apps and services in 
{{site.data.keyword.cloud_notm}}. For more information, see the [{{site.data.keyword.keymanagementserviceshort}} documentation](/docs/key-protect?topic=key-protect-about).  

Before you begin, make sure that you have the permissions to create an [{{site.data.keyword.keymanagementservicelong}} instance](/docs/key-protect?topic=key-protect-manage-access). 



1. [Install the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli). 
2. [Create or retrieve an {{site.data.keyword.cloud_notm}} API key](/docs/account?topic=account-userapikey#create_user_key). The API key is used to authenticate with the {{site.data.keyword.cloud_notm}} platform and to determine your permissions for {{site.data.keyword.cloud_notm}} services.
3. In your Terraform installation directory, create a folder for your first Terraform on {{site.data.keyword.cloud_notm}} project and navigate into the folder. This folder is used to store all configuration files and variable definitions. 
   ```
   mkdir myproject && cd myproject
   ```
   {: pre}

4. Create a variables file that is named `terraform.tfvars` and specify the {{site.data.keyword.cloud_notm}} API key that you retrieved. Variables that are defined in the `terraform.tfvars` file are automatically loaded by Terraform when the {{site.data.keyword.cloud_notm}} Provider plug-in is initialized and you can reference them in every Terraform configuration file that you use. 

   Because the `terraform.tfvars` file contains confidential information, do not push this file to a version control system. This file is meant to be on your local system only. 
   {: important}
   
   ```
   ibmcloud_api_key = "<ibmcloud_api_key>"
   ```
   {: codeblock}
   
5. Create a provider configuration file that is named `provider.tf`. Use this file to configure the {{site.data.keyword.cloud_notm}} Provider plug-in with the {{site.data.keyword.cloud_notm}} API key from your `terraform.tfvars` file. The plug-in uses this key to access {{site.data.keyword.cloud_notm}} and to provision your {{site.data.keyword.keymanagementserviceshort}} instance. To access a variable value from the `terraform.tfvars` file, you must first declare the variable in the `provider.tf` file and then reference the variable by using the `var.<variable_name>` syntax . 

   ```
   variable "ibmcloud_api_key" {}
 
   provider "ibm" {
       ibmcloud_api_key   = var.ibmcloud_api_key
      }
   ```
   {: codeblock}

6. Create a Terraform configuration file that is named `main.tf`. In this file, you declare the {{site.data.keyword.keymanagementserviceshort}} instance that you want to provision. The following example creates a {{site.data.keyword.keymanagementserviceshort}} instance that is named `my_kp` in the `us-south` region. For other options that you can declare for this resource, see the [`ibm_resource_instance` documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/resource_instance){: external}. 
   
   ```
   resource "ibm_resource_instance" "kms_instance" {
     name     = "my_kp"
     service  = "kms"
     plan     = "tiered-pricing"
     location = "us-south"
   }
   ```
   {: codeblock}
   
7. Initialize the Terraform CLI. 
   ```
   terraform init
   ```
   {: pre}
   
8. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.keymanagementserviceshort}} instance in your account.
   ```
   terraform plan
   ```
   {: pre}
   
   Example output: 
   ```
   Terraform will perform the following actions:

   # ibm_resource_instance.kms_instance will be created
   + resource "ibm_resource_instance" "kms_instance" {
      + account_id              = (known after apply)
      + allow_cleanup           = (known after apply)
      + created_at              = (known after apply)
      + created_by              = (known after apply)
      + crn                     = (known after apply)
      + dashboard_url           = (known after apply)
      + deleted_at              = (known after apply)
      + deleted_by              = (known after apply)
      + extensions              = (known after apply)
      + guid                    = (known after apply)
      + id                      = (known after apply)
      + location                = "us-south"
      + locked                  = (known after apply)
      + name                    = "my_kp"
      + plan                    = "tiered-pricing"
      + plan_history            = (known after apply)
      + resource_aliases_url    = (known after apply)
      + resource_bindings_url   = (known after apply)
      + resource_controller_url = (known after apply)
      + resource_crn            = (known after apply)
      + resource_group_crn      = (known after apply)
      + resource_group_id       = (known after apply)
      + resource_group_name     = (known after apply)
      + resource_id             = (known after apply)
      + resource_keys_url       = (known after apply)
      + resource_name           = (known after apply)
      + resource_plan_id        = (known after apply)
      + resource_status         = (known after apply)
      + restored_at             = (known after apply)
      + restored_by             = (known after apply)
      + scheduled_reclaim_at    = (known after apply)
      + scheduled_reclaim_by    = (known after apply)
      + service                 = "kms"
      + service_endpoints       = (known after apply)
      + state                   = (known after apply)
      + status                  = (known after apply)
      + sub_type                = (known after apply)
      + tags                    = (known after apply)
      + target_crn              = (known after apply)
      + type                    = (known after apply)
      + update_at               = (known after apply)
      + update_by               = (known after apply)
    }

   Plan: 1 to add, 0 to change, 0 to destroy.
   ```
   {: screen}
   
9. Create the {{site.data.keyword.keymanagementserviceshort}} instance in {{site.data.keyword.cloud_notm}}.
   ```
   terraform apply
   ```
   {: pre}
   
   Example output: 
   ```
   ibm_resource_instance.kms_instance: Creating...
   ibm_resource_instance.kms_instance: Still creating... [10s elapsed]
   ibm_resource_instance.kms_instance: Still creating... [20s elapsed]
   ibm_resource_instance.kms_instance: Creation complete after 24s [id=crn:v1:bluemix:public:kms:us-   south:a/6ef045fd2b43266cfe8e6388dd2ec098:3ce1162f-baef-4fe7-beb3-a78d697cf981::]
   ```
   {: screen}
   
10. From the [{{site.data.keyword.cloud_notm}} resource dashboard](https://cloud.ibm.com/resources){: external}, find the {{site.data.keyword.keymanagementserviceshort}} instance that you created.

Congratulations! You used Terraform on {{site.data.keyword.cloud_notm}} to automatically provision your first resource in {{site.data.keyword.cloud_notm}}. 

## What's next? 
{: #whats-next}

- Explore the [`ibm_kp_key`](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-kms-resources#kp-key) resource to create your first key in your {{site.data.keyword.keymanagementserviceshort}} instance with Terraform on {{site.data.keyword.cloud_notm}}.
- Browse other [supported {{site.data.keyword.cloud_notm}} resources and data sources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-index-of-terraform-on-ibm-cloud-resources-and-data-sources) that you can use in Terraform on {{site.data.keyword.cloud_notm}}.
- Learn more about how to [configure the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) when you want to automate other {{site.data.keyword.cloud_notm}} resources. 
- Explore [sample Terraform templates](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-sample_terraformtemplates) that you can use to work with services in {{site.data.keyword.cloud_notm}}.


