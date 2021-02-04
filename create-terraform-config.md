---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-04"

keywords: terraform template guidelines, terraform config file guidelines, sample terraform files, terraform provider, terraform variables, terraform input variables, terraform template

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



# Creating Terraform templates
{: #create-tf-config}

Learn how to create Terraform templates that are well-structured, reusable, and comprehensive.
{: shortdesc}

An Terraform template consists of one or more Terraform configuration files that declare the state that you want to achieve for your {{site.data.keyword.cloud_notm}} resources. To successfully work with your resources, you must [configure IBM as your cloud provider](#configure-provider) and [add resources to your Terraform configuration file](#configure-resources). Optionally, you can use [input variables](#configure-variables) to customize your resources.

You can write your Terraform configuration file by using HashiCorp Configuration Language (HCL) or JSON syntax. For more information, see [Configuration language](https://www.terraform.io/docs/configuration/index.html){: external}.  


## Configuring the `provider` block 
{: #configure-provider}
{: help}
{: support}

Specify the cloud provider that you want to use in the `provider` block of your Terraform configuration file. The `provider` block includes all the input variables that the {{site.data.keyword.cloud_notm}} Provider plug-in for the Terraform to provision your resources.
{: shortdesc}

**Do I need to provide the {{site.data.keyword.cloud_notm}} API key?** </br>
The {{site.data.keyword.cloud_notm}} API key is essential to authenticate with the {{site.data.keyword.cloud_notm}} platform, receive the IAM token and IAM refresh token that {{site.data.keyword.bpshort}} requires to work with the resource's API, and to determine the permissions that you were granted. When you use native Terraform, you must provide the {{site.data.keyword.cloud_notm}} API key at all times. In {{site.data.keyword.bpshort}}, the API key is automatically retrieved for all IAM-enabled resources, including {{site.data.keyword.containerlong_notm}} clusters, and VPC infrastructure resources. However, the API key is not retrieved for Cloud Foundry and classic infrastructure resources and must be provided in the `provider` block. 

**Can I specify a different {{site.data.keyword.cloud_notm}} API key in the `provider` block?** </br>
If you want to use a different API key than the one that is associated with your {{site.data.keyword.cloud_notm}} account, you can provide this API key in the `provider` block. If an API key is configured in the `provider` block, this key takes precedence over the API key that is stored in {{site.data.keyword.cloud_notm}}.  

**Can I provide an API key for a service ID?** </br>
You can provide an API key for a service ID for all IAM-enabled services, including VPC infrastructure resources. You cannot use a service ID for classic infrastructure or Cloud Foundry resources. 

To configure the `provider` block: 

1. Choose how you want to configure the `provider` block. 
   - **Option 1: Create a separate `provider.tf` file.** The information in this file is loaded by Terraform and {{site.data.keyword.bplong_notm}}, and applied to all Terraform configuration files that exist in the same GitHub directory or tape archive file (`.tar`). This approach is useful if you split out your infrastructure code across multiple files. 
   - **Option 2: Add a `provider` block to your Terraform configuration file.** You might choose this option if you prefer to specify the provider alongside with your variables and resources in one Terraform configuration file. 

2. Review what [credentials and information you must provide in the `provider` block to work with your resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters). {{site.data.keyword.bpshort}} automatically retrieves your {{site.data.keyword.cloud_notm}} API key so that you do not need to specify this information in your `provider` block. 
   
3. Create a `provider.tf` file or add the following code to your Terraform configuration file. For a full list of supported parameters that you can set in the `provider` block, see the [{{site.data.keyword.cloud_notm}} provider reference](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#provider-parameter-ov).

   Example for VPC infrastructure resources: 
   ```
   provider "ibm" {
     generation = 2
     region = "<region_name>"
   }
   ```
   {: codeblock}
   
   Example for classic infrastructure resources: 
   ```
   variable "iaas_classic_username" {
      type = "string"
   }
   variable "iaas_classic_api_key" {
      type = "string"
   }

   provider "ibm" {
     region = "<region_name>"
     iaas_classic_username = var.iaas_classic_username
     iaas_classic_api_key  = var.iaas_classic_api_key
   }
   ```
   {: codeblock}
   
   Example for all {{site.data.keyword.containerlong_notm}} resources:
   ```
   provider "ibm" {
   }
   ```
   {: codeblock}
   
   Example for all other resources:
   ```
   provider "ibm" {
     region = "<region_name>"
   }
   ```
   {: codeblock}

## Adding {{site.data.keyword.cloud_notm}} resources to the `resource` block
{: #configure-resources}

Use `resource` blocks to define the {{site.data.keyword.cloud_notm}} resources that you want to manage with {{site.data.keyword.bplong_notm}}. 
{: shortdesc}

To support a multi-cloud approach, Terraform works with multiple cloud providers. A cloud provider is responsible for understanding the resources that you can provision, their API, and the methods to expose these resources in the cloud. To make this knowledge available to users, every supported cloud provider must provide a command line plug-in for Terraform that users can use to work with the resources. To find an overview of the resources that you can provision in {{site.data.keyword.cloud_notm}}, see the [Terraform reference](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-index-of-ibm-cloud-provider-plug-in-for-terraform-resources-and-data-sources). 

Example infrastructure code for provisioning a VPC: 
```
resource ibm_is_vpc "vpc" {
  name = "myvpc"
}
```
{: codeblock}



### Referencing resources in other resource blocks
{: #reference-resource-info}

Review the options that you have to reference existing resources in other resource blocks of your Terraform configuration file. 
{: shortdesc}

The {{site.data.keyword.cloud_notm}} Provider plug-in reference includes two types of objects, data sources and resources. You can use both objects to reference resources in other resource blocks.  

- **Resources**: To create a resource, you use the resource definition in the {{site.data.keyword.cloud_notm}} Provider plug-in reference. A resource definition includes the syntax for configuring your {{site.data.keyword.cloud_notm}} resources and an **Attributes reference** that shows the properties that you can reference as input parameters in other resource blocks. For example, when you create a VPC, the ID of the VPC is made available after the creation. You can use the ID as an input parameter when you create a subnet for your VPC. Use this option if you combine multiple resources in one Terraform configuration file.  </br>

  Example infrastructure code: 
  ```
  resource ibm_is_vpc "vpc" {
    name = "myvpc"
  }

  resource ibm_is_security_group "sg1" {
    name = "mysecuritygroup"
    vpc  = ibm_is_vpc.vpc.id
  }
  ```
  {: codeblock}

- **Data sources**: You can also use the data sources from the {{site.data.keyword.cloud_notm}} Provider plug-in reference to retrieve information about an existing {{site.data.keyword.cloud_notm}} resource. Review the **Argument reference** section in the {{site.data.keyword.cloud_notm}} Provider plug-in reference to see what input parameters you must provide to retrieve an existing resource. Then, review the **Attributes reference** section to find an overview of parameters that are made available to you and that you can reference in your `resource` blocks. Use this option if you want to access the details of a resource that is configured in another Terraform configuration file. 
  
  Example infrastructure code: 
  ```
  data ibm_is_image "ubuntu" {
    name = "ubuntu-18.04-amd64"
  }
  
  resource ibm_is_instance "vsi1" {
    name    = "$mysi"
    vpc     = ibm_is_vpc.vpc.id
    zone    = "us-south1"
    keys    = [data.ibm_is_ssh_key.ssh_key_id.id]
    image   = data.ibm_is_image.ubuntu.id
    profile = "cc1-2x4"

    primary_network_interface {
      subnet          = ibm_is_subnet.subnet1.id
      security_groups = [ibm_is_security_group.sg1.id]
    }
  }
  ```
  {: codeblock}


## Using `variable` blocks to customize resources
{: #configure-variables}

You can use `variable` blocks to templatize your infrastructure code. For example, instead of creating multiple Terraform configuration files for a resource that you want to deploy in multiple data centers, simply reuse the same configuration and use an input variable to define the data center. 
{: shortdesc}

**Where do I store my variable declarations?** </br>
You can decide to declare your variables within the same Terraform configuration file where you specify the resources that you want to provision, or to create a separate `variables.tf` file that includes all your variable declarations. When you create a workspace, {{site.data.keyword.bplong_notm}} automatically parses through your Terraform configuration files to find variable declarations. 

**What information do I need to include in my variable declaration?** </br>
When you declare an input variable, you must provide a name for your variable and the data type, such as `string` or `integer`, that the variable uses. You can optionally add a description and a default value for your variable. When input variables are imported into {{site.data.keyword.bpshort}} and a default value is specified, you can choose to overwrite the default value. 

**Is there a character limit for input variables?** </br>
Yes. If you define input variables in your Terraform configuration file, keep in mind that the value that you enter for these variables can be up to 2049 characters. If your input variable requires a value that exceeds this limit, the value is truncated after 2049 characters. 

Example variable declaration without a Default value is 
```
variable "datacenter" {
  type        = "string"
  description = "The data center that you want to deploy your Kubernetes cluster in."
}
```
{: codeblock}

Example variable declaration with a Default value is 
```
variable "datacenter" {
  type        = "string"
  description = "The data center that you want to deploy your Kubernetes cluster in."
  default = "dal10"
}
```
{: codeblock}

### Referencing variables
{: #reference-variables}

You can reference the value of the variable in other blocks of your Terraform configuration files by using the `"${var.<variable_name>}"` syntax. 

Example for referencing a `datacenter` variable: 

```
resource ibm_container_cluster "test_cluster" {
  name         = "test"
  datacenter   = var.datacenter
}
```
{: codeblock}

For more information, about variable configurations, see the [Terraform documentation](https://www.terraform.io/docs/configuration/variables.html){: external}.



## Storing your Terraform templates
{: #store-template}

Your Terraform configuration files contain infrastructure code that you must treat as regular code. To support collaboration, source and version control, store your files in a GitHub or GitLab repository. With version control, you can revert to previous versions, audit changes, and share code with multiple teams. If you do not want to store your files in GitHub, you have the option to provide your template by uploading a [tape archive file (`.tar`)](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-upload) from your local machine instead. 
{: shortdesc}

Cloning GitHub repository in {{site.data.keyword.bplong_notm}} is allowed only to the listed extension files. The blocked extension files having more than 500 KB in size, and any invalid image is considered as vulnerable files while cloning.
-	Allowed extension: `.tf` `.tfvars` `.md` `.yaml` `.sh` `.txt` `.yml` `.html` `.tf` `.json` `.gitignore` `license` `.js` `.pub` `.service` `_rsa`
-	Blocked extension: `.php5` `.pht` `.phtml` `.shtml` `.asa` `.cer` `.asax` `.swf` `.xap` `.tfstate` `.tfstate.backup`
-	Allowed image extension: `.tif` `.tiff` `.gif` `.png` `.bmp` `.jpg` `.jpeg` 


The directory structure of the Terraform template in the GitHub repository looks like listed in the table with the last updated time.

| File | Description |
|----|-----|
| README.md | Create README.md |
| main.tf | Create main.tf |
| output.tf | Create output.tf |
| provider.tf | Create provider.tf |
| variables.tf | Create variables.tf |

