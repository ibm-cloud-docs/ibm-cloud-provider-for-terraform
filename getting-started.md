---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-03"

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
{:swift-ios: .ph data-hd-programlang='iOS Swift'}
{:swift-server: .ph data-hd-programlang='server-side Swift'}
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




# Getting started with Terraform
{: #getting-started}

{{site.data.keyword.cloud}} Provider plug-in for Terraform is an Open Source software enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} platform, classic infrastructure, and VPC infrastructure resources by using a high-level scripting language. You can use Terraform to automate your {{site.data.keyword.cloud_notm}} resource provisioning, rapidly build complex, multi-tier cloud environments, and enable Infrastructure as Code (IaC).  
{: shortdesc}

Looking for a managed Terraform solution? Try out [{{site.data.keyword.bplong_notm}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform CLI and {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud_notm}} catalog.
{: tip}

**How does it work?**</br>
Let's say you want to spin up multiple copies of your service that uses a cluster of virtual servers, a load balancer, and a database server on the {{site.data.keyword.cloud}}. You could learn how to create each resource, review the API or the commands that you need, and write a bash script to spin up these components. But it's easier, faster, and more orderly to specify the type of resource that you want and let Terraform do it all for you. 

The Terraform configuration files describe the resources that you need and how you want to configure them. Based on your configuration, Terraform creates an execution plan and describes the actions that need to be executed to get to the required state. You can review the execution plan, change it, or simply execute the plan. When you change your configuration, Terraform can determine what changed and create incremental execution plans that you can apply to your existing {{site.data.keyword.cloud_notm}} resources. 

**What do I need to get started?**</br>
To provision {{site.data.keyword.cloud_notm}} infrastructure and platform resources, you must have a [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/registration).  

**What do I provision as part of this tutorial?** </br>

In this getting started tutorial, you provision a [classic infrastructure virtual server](/docs/virtual-servers?topic=virtual-servers-about-public-virtual-servers) and a [VPC virtual server instance](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-getting-started). Both virtual server instances incur costs. Be sure to review the available plans for [classic infrastructure virtual servers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/infrastructure/virtual-server-group) and [VPC virtual server instances](https://cloud.ibm.com/vpc/provision/vs) before you proceed.

Sounds great? Get started by installing the [Terraform]() and the [{{site.data.keyword.cloud_notm}} Provider plug-in](). You can then configure the {{site.data.keyword.cloud_notm}} resources that you want and watch Terraform spin them up. 

**What credentials do I need?**</br>
The credentials that you need depend on the type of resource that you want to provision. For example, to provision classic infrastructure resources, you must provide your {{site.data.keyword.cloud_notm}} classic infrastructure user name and API key. To provision VPC infrastructure, you need an {{site.data.keyword.cloud_notm}} API key. For more information, about what credentials you need for a specific {{site.data.keyword.cloud_notm}} resource, see [Required input parameters for each resource category](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters).

**Where can I find an overview of available resources?**</br>
To find a full list of {{site.data.keyword.cloud_notm}} resources that you can provision with the {{site.data.keyword.cloud_notm}} Provider plug-in, see the [Index of  resources and data sources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-index-of-ibm-cloud-provider-plug-in-for-terraform-resources-and-data-sources) supported by the {{site.data.keyword.cloud}} Provider plug-in for Terraform.

1. Create a folder on your local machine for your first Terraform project and navigate into the folder. This folder is used to store all configuration files and variable definitions. 

   ```
   mkdir myproject && cd myproject
   ```
   {: pre}
      
2. [Create an {{site.data.keyword.cloud_notm}} API key](/docs/account?topic=account-userapikey#create_user_key) to provision the VPC virtual server instance. 

3. [Generate an SSH key](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-ssh-keys). The SSH key is required to provision the VPC virtual server instance and you can use the SSH key to access your instance via SSH. After you created your SSH key, make sure to [upload this SSH key to your {{site.data.keyword.cloud_notm}} account](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-managing-ssh-keys#managing-ssh-keys-with-ibm-cloud-console). 

4. [Retrieve your {{site.data.keyword.cloud_notm}} classic infrastructure user name and API key](/docs/account?topic=account-classic_keys). You use this user name and API key to provision the classic infrastructure virtual server in your {{site.data.keyword.cloud_notm}} account. 
        
6. Create a local Terraform variables file that is named `terraform.tfvars` to store your {{site.data.keyword.cloud_notm}} classic infrastructure credentials and the {{site.data.keyword.cloud_notm}} API key. Make sure to save this file in the folder that you created for your first Terraform project. Variables that are defined in the `terraform.tfvars` file are automatically loaded by Terraform when the {{site.data.keyword.cloud_notm}} Provider plug-in is initialized and you can reference them in every Terraform configuration file that you use. 

   Because the `terraform.tfvars` file contains confidential information, do not push this file to your version control system where you store the Terraform configuration files of the resources that you want to provision. This file is meant to be on your local system only. 
   {: important}
   
   ```
   ibmcloud_api_key = "<ibmcloud_api_key>"
   ssh_key = "<ssh_key_name>"
   iaas_classic_username = "<classic_infrastructure_username>"
   iaas_classic_api_key = "<classic_infrastructure_apikey>"
   ```
   {: codeblock}
   
   <table>
   <caption>Understanding the configuration file components</caption>
   <col style="width:30%">
	 <col style="width:70%">
   <thead>
     <th>Parameter</th>
     <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>ibmcloud_api_key</code></td>
   <td>Enter the {{site.data.keyword.cloud_notm}} API key that you retrieved earlier.</td>
   </tr>
   <tr>
   <td><code>ssh_key</code></td>
   <td>Enter the name of the SSH key that you chose when you uploaded the SSH key to your {{site.data.keyword.cloud_notm}} account.</td>
   </tr>
   <tr>
   <td><code>iaas_classic_username</code></td>
   <td>Enter the classic infrastructure user name that you retrieved earlier.  </td>
   </tr>
   <tr>
   <td><code>iaas_classic_api_key</code></td>
   <td>Enter the classic infrastructure API key that you retrieved earlier. </td>
   </tr>
   </tbody>
   </table>
   
7. Create an Terraform provider configuration file that is named `provider.tf`. Use this file to configure the {{site.data.keyword.cloud_notm}} Provider plug-in with the credentials from your `terraform.tfvars` file so that the plug-in can access and provision {{site.data.keyword.cloud_notm}} resources. To reference a variable from the `terraform.tfvars` file, use the syntax `var.<variable_name>`. 

    ```
     variable "ibmcloud_api_key" {}
     variable "iaas_classic_username" {}
     variable "iaas_classic_api_key" {}
 
     provider "ibm" {
       ibmcloud_api_key   = var.ibmcloud_api_key
       region             = "us-south"
       iaas_classic_username = var.iaas_classic_username
       iaas_classic_api_key  = var.iaas_classic_api_key
      }
    ```
    {: codeblock}
   
   <table>
   <caption>Understanding the configuration file components</caption>
   <col style="width:30%">
	 <col style="width:70%">
   <thead>
     <th>Parameter</th>
     <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>ibmcloud_api_key</code></td>
   <td>Reference the {{site.data.keyword.cloud_notm}} API key that you stored in your <code>terraform.tfvars</code> file. This API key is required to provision {{site.data.keyword.cloud_notm}} platform and VPC infrastructure resources. You can remove this credential if you want to provision classic infrastructure resources only.  </td>
   </tr>
   <tr>
   <td><code>region</code></td>
   <td>Specify the {{site.data.keyword.cloud_notm}} region where you want to provision your infrastructure resources. Run <code>ibmcloud is regions</code> to find supported regions.  </td>
   </tr>
   <tr>
   <td><code>iaas_classic_username</code></td>
   <td>Reference the classic infrastructure user name that you stored in your <code>terraform.tfvars</code> file. This user name is required to provision classic infrastructure resources. You can remove this credential if you want to provision {{site.data.keyword.cloud_notm}} platform or VPC infrastructure resources only. </td>
   </tr>
   <tr>
   <td><code>iaas_classic_api_key</code></td>
   <td>Reference the classic infrastructure API key that you stored in your <code>terraform.tfvars</code> file. This API key is required to provision classic infrastructure resources. You can remove this credential if you want to provision {{site.data.keyword.cloud_notm}} platform or VPC infrastructure resources only.   </td>
   </tr>
   </tbody>
   </table>
   
## Provisioning an {{site.data.keyword.cloud_notm}} Virtual Server for VPC
{: #sample_vpc_config}

Use {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform to provision a VPC, and set up networking for your VPC, and provision a Virtual Service for VPC in your {{site.data.keyword.cloud_notm}} account. 
{: shortdesc}

A VPC allows you to create your own space in {{site.data.keyword.cloud_notm}} so that you can run an isolated environment in the public cloud with custom network policies. The example in this topic provisions the following VPC infrastructure resources for you: 
- 1 VPC where you provision your VPC virtual server instance
- 1 security group and a rule for this security group to allow SSH connection to your virtual server instance
- 1 subnet to enable networking in your VPC
- 1 VPC virtual server instance 
- 1 floating IP address that you use to access your VPC virtual server instance over the public network

Keep in mind that a VPC virtual server instance is an {{site.data.keyword.cloud_notm}} VPC infrastructure resource that incurs costs. Be sure to review the [available plans ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/vpc/provision/vs) before you proceed.
{: important}

Before you begin: 
- [Install the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform](#install). 
- [Retrieve your {{site.data.keyword.cloud_notm}} credentials, upload an SSH key, and configure the {{site.data.keyword.cloud_notm}} Provider plug-in forTerraform provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#cloud_provider_config). 

To create a VPC and a virtual server instance: 

1. Make sure that you have the [required permissions](/docs/vpc-on-classic?topic=vpc-on-classic-managing-user-permissions-for-vpc-resources) to create and work with VPC infrastructure. 

2. In the same directory where you stored the `terraform.tfvars` and `provider.tf` files, create an Terraform configuration file and name it `vpc.tf`. The configuration file includes the following definition blocks: 
   - **locals**: Use this block to specify variables that you want to use multiple times throughout this configuration file. 
   - **resource**: Every resource block specifies the {{site.data.keyword.cloud_notm}} resource that you want to provision. To find more information about supported configurations for each resource, see the [{{site.data.keyword.cloud_notm}} Provider plug-in reference](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#configure_provider).
   - **data**: Use this block to retrieve information for an existing resource in your {{site.data.keyword.cloud_notm}} account. 
   - **output**: This block specifies commands that you want to run after your resources are provisioned. 
   
   Example configuration file: 
   
   ```
   variable "ssh_key" {
   }

   locals {
     BASENAME = "<name>"
     ZONE     = "us-south-1"
   }

   resource "ibm_is_vpc" "vpc" {
     name = "${local.BASENAME}-vpc"
   }

   resource "ibm_is_security_group" "sg1" {
     name = "${local.BASENAME}-sg1"
     vpc  = ibm_is_vpc.vpc.id
   }

   # allow all incoming network traffic on port 22
   resource "ibm_is_security_group_rule" "ingress_ssh_all" {
     group     = ibm_is_security_group.sg1.id
     direction = "inbound"
     remote    = "0.0.0.0/0"

     tcp {
       port_min = 22
       port_max = 22
     }
   }

   resource "ibm_is_subnet" "subnet1" {
     name                     = "${local.BASENAME}-subnet1"
     vpc                      = ibm_is_vpc.vpc.id
     zone                     = local.ZONE
     total_ipv4_address_count = 256
   }

   data "ibm_is_image" "ubuntu" {
     name = "ubuntu-18.04-amd64"
   }

   data "ibm_is_ssh_key" "ssh_key_id" {
     name = var.ssh_key
   }

   resource "ibm_is_instance" "vsi1" {
     name    = "${local.BASENAME}-vsi1"
     vpc     = ibm_is_vpc.vpc.id
     zone    = local.ZONE
     keys    = [data.ibm_is_ssh_key.ssh_key_id.id]
     image   = data.ibm_is_image.ubuntu.id
     profile = "cc1-2x4"

     primary_network_interface {
       subnet          = ibm_is_subnet.subnet1.id
       security_groups = [ibm_is_security_group.sg1.id]
     }
   }

   resource "ibm_is_floating_ip" "fip1" {
     name   = "${local.BASENAME}-fip1"
     target = ibm_is_instance.vsi1.primary_network_interface[0].id
   }

   output "sshcommand" {
     value = "ssh root@ibm_is_floating_ip.fip1.address"
   }
   ```
   {: codeblock}
    
   <table>
   <caption>Understanding the configuration file components</caption>
   <col style="width:30%">
	 <col style="width:70%">
   <thead>
     <th>Parameter</th>
     <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>locals.BASENAME</code></td>
   <td>Enter a name that you want to append to the name of all VPC infrastructure resources that you create with this configuration file. </td>
   </tr>
     <tr>
       <td><code>locals.ZONE</code></td>
       <td>Enter a supported VPC zone where you want to create your resources. To find available zones, run <code>ibmcloud is zones</code>.  </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_vpc.name</code></td>
       <td>Enter a name for your VPC. In this example, you use <code>locals.BASENAME</code> to create part of the name. For example, if your base name is `test`, the name of your VPC is set to `test-vpc`. Keep in mind that the name of your VPC must be unique within your {{site.data.keyword.cloud_notm}} account. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_security_group.name</code></td>
       <td>Enter a name for the security group that you create for your VPC. In this example, you use <code>locals.BASENAME</code> to create part of the name. For example, if your base name is `test`, the name of your security group is set to `test-sg1`.  </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_security_group.vpc</code></td>
       <td>Enter the ID of the VPC for which you want to create the security group. In this example, you reference the ID of the VPC that you create with the <code>ibm_is_vpc</code> resource in the same configuration file.  </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_security_group_rule.group</code></td>
       <td>Enter the ID of the security group for which you want to create a security group rule. In this example, you reference the ID of the security group that you create with the <code>ibm_is_security_group</code> resource in the same configuration file.  </td>
     </tr>
      <tr>
       <td><code>resource.ibm_is_security_group_rule.direction</code></td>
       <td>Specify if the security group rule is applied to incoming or outgoing network traffic. Choose <strong>inbound</strong> to specify a rule for incoming network traffic, and <strong>outbound</strong> to specify a rule for outgoing network traffic. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_security_group_rule.remote</code></td>
       <td>Enter the IP address range, for which the security group rule is applied. In this example, <code>0.0.0.0/0</code> allows network traffic from all IP addresses. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_security_group_rule.tcp</code></td>
       <td>Enter the TCP port range that you want to open in your security group rule. If you want to open up a single port, enter the same port number in <code>port_min</code> and <code>port_max</code>. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_subnet.name</code></td>
       <td>Enter a name for your subnet. In this example, you use <code>locals.BASENAME</code> to create part of the name. For example, if your base name is `test`, the name of your subnet is set to `test-subnet1`.  </td>
     </tr>
      <tr>
       <td><code>resource.ibm_is_subnet.vpc</code></td>
       <td>Enter the ID of the VPC for which you want to create the subnet. In this example, you reference the ID of the VPC that you create with the <code>ibm_is_vpc</code> resource in the same configuration file. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_subnet.zone</code></td>
       <td>Enter the zone in which you want to create the subnet. In this example, you use <code>locals.ZONE</code> as the name for your zone. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_subnet.</code></br><code>total_ipv4_address_count</code></td>
       <td>Enter the number of IPv4 IP addresses that you want to have in your subnet. </td>
     </tr>
     <tr>
       <td><code>data.ibm_is_image.name</code></td>
       <td>Enter the name of the Operating System that you want to install on your VPC virtual server instance. For supported image names, run <code>ibmcloud is images</code>. </td>
     </tr>
     <tr>
       <td><code>data.ibm_is_ssh_key.name</code></td>
       <td>Enter the name of the SSH key that you uploaded to your {{site.data.keyword.cloud_notm}} account.</td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.name</code></td>
       <td>Enter the name of the VPC virtual server instance that you want to create. In this example, you use <code>locals.BASENAME</code> to create part of the name. For example, if your base name is `test`, the name of your VPC virtual server instance is set to `test-vsi1`.  </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.vpc</code></td>
       <td>Enter the ID of the VPC in which you want to create the VPC virtual server instance. In this example, you reference the ID of the VPC that you create with the <code>ibm_is_vpc</code> resource in the same configuration file.  </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.zone</code></td>
       <td>Enter the zone in which you want to create the VPC virtual server instance. In this example, you use <code>locals.ZONE</code> as the name for your zone. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.keys</code></td>
       <td>Enter the UUID of the SSH key that you uploaded to your {{site.data.keyword.cloud_notm}} account. In this example, you retrieve the UUID from the <code>ibm_is_ssh_key</code> data source of this configuration file. Terraform uses the name of the SSH key that you define in your data source object to look up information about the SSH key in your {{site.data.keyword.cloud_notm}} account.</td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.image</code></td>
       <td>Enter the ID of the image that represents the Operating System that you want to install on your VPC virtual server instance. In this example, you retrieve the ID from the <code>ibm_is_image</code> data source of this configuration file. Terraform uses the name of the image that you define in your data source object to look up information about the image in the {{site.data.keyword.cloud_notm}} infrastructure portfolio. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.profile</code></td>
       <td>Enter the name of the profile that you want to use for your VPC virtual server instance. For supported profiles, run <code>ibmcloud is instance-profiles</code>. </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.</code></br><code>primary_network_interface.subnet</code></td>
       <td>Enter the ID of the subnet that you want to use for your VPC virtual server instance. In this example, you use the <code>ibm_is_subnet</code> resource in this configuration file to retrieve the ID of the subnet.   </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.</code></br><code><primary_network_interface.security_groups</code></td>
       <td>Enter the ID of the security group that you want to apply to your VPC virtual server instance. In this example, you use the <code>ibm_is_security_group</code> resource in this configuration file to retrieve the ID of the security group.   </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_floating_ip.name</code></td>
       <td>Enter a name for your floating IP resource. In this example, you use <code>locals.BASENAME</code> to create part of the name. For example, if your base name is `test`, the name of your floating IP resource is set to `test-fip1`.   </td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_floating_ip.target</code></td>
       <td>Enter the ID of the network interface where you want to allocate the floating IP addresses. In this example, you use the <code>ibm_is_instance</code> resource to retrieve the ID of the primary network interface.   </td>
     </tr>
     <tr>
       <td><code>output.ssh_command.value</code></td>
       <td>Build the SSH command that you need to run to connect to your VPC virtual server instance. In this example, you use the <code>ibm_is_floating_ip</code> resource to retrieve the floating IP address that is assigned to your VPC virtual server instance.  </td>
     </tr>
   </tbody>
   </table>

3. Initialize Terraform. 

   ```
   terraform init
   ```
   {: pre}
   
   Example output: 
   ```
   Initializing provider plugins...

   The following providers do not have any version constraints in configuration, so the latest version was installed.

   To prevent automatic upgrades to new major versions that may contain breaking changes, it is recommended to add version = "..." constraints to the corresponding provider blocks in configuration, with the constraint strings suggested.

   * provider.ibm: version = "~> 0.11"

   Terraform has been successfully initialized!

   You may now begin working with Terraform. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform commands should now work.

   If you ever set or change modules or backend configuration for Terraform, rerun this command to reinitialize your working directory. If you forget, other commands detect it and remind you to do so if necessary.
   ```
   {: screen}
   
4. Generate an Terraform execution plan. When you execute this command, Terraform validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in.

   ```
   terraform plan
   ```
   {: pre}

   Example output: 

   ```
   Refreshing Terraform state in-memory prior to plan...
   The refreshed state be used to calculate this plan, but not be
   persisted to local or remote state storage.

   An execution plan has been generated and is shown.
   Resource actions are indicated with the following symbols:
     + create

   Terraform performs the following actions:

     + ibm_is_floating_ip.fip1
         id:                                               <computed>
         address:                                          <computed>
         name:                                             "newvpc-fip1"
         status:                                           <computed>
         target:                                           "${ibm_is_instance.vsi1.primary_network_interface.0.id}"
         zone:                                             <computed>

     + ibm_is_instance.vsi1
         id:                                               <computed>
         boot_volume.#:                                    <computed>
         cpu.#:                                            <computed>
         generation:                                       "gc"
         gpu.#:                                            <computed>
         image:                                            "cfdaf1a0-5350-4350-fcbc-97173b510843"
         keys.#:                                           "1"
         keys.3772860677:                                  "<ssh_key_UUID>"
         memory:                                           <computed>
         name:                                             "newvpc-vsi2"
         primary_network_interface.#:                      "1"
         primary_network_interface.0.id:                   <computed>
         primary_network_interface.0.name:                 <computed>
         primary_network_interface.0.primary_ipv4_address: <computed>
         primary_network_interface.0.security_groups.#:    <computed>
         primary_network_interface.0.subnet:               "${ibm_is_subnet.subnet1.id}"
         profile:                                          "cc1-2x4"
         resource_group:                                   <computed>
         status:                                           <computed>
         vpc:                                              "${ibm_is_vpc.vpc.id}"
         zone:                                             "us-south-2"

     + ibm_is_security_group.sg1
         id:                                               <computed>
         name:                                             "newvpc-sg1"
         rules.#:                                          <computed>
         vpc:                                              "${ibm_is_vpc.vpc.id}"

     + ibm_is_security_group_rule.ingress_ssh_all
         id:                                               <computed>
         direction:                                        "ingress"
         group:                                            "${ibm_is_security_group.sg1.id}"
         ip_version:                                       "ipv4"
         remote:                                           "0.0.0.0/0"
         rule_id:                                          <computed>
         tcp.#:                                            "1"
         tcp.0.port_max:                                   "22"
         tcp.0.port_min:                                   "22"

     + ibm_is_subnet.subnet1
         id:                                               <computed>
         available_ipv4_address_count:                     <computed>
         ip_version:                                       "ipv4"
         ipv4_cidr_block:                                  <computed>
         ipv6_cidr_block:                                  <computed>
         name:                                             "newvpc-subnet1"
         network_acl:                                      <computed>
         status:                                           <computed>
         total_ipv4_address_count:                         "256"
         vpc:                                              "${ibm_is_vpc.vpc.id}"
         zone:                                             "us-south-2"

     + ibm_is_vpc.vpc
         id:                                               <computed>
         classic_access:                                   "false"
         default_network_acl:                              <computed>
         default_security_group:                           <computed>
         is_default:                                       "false"
         name:                                             "newvpc"
         resource_group:                                   <computed>
         status:                                           <computed>

   Plan: 6 to add, 0 to change, 0 to destroy.

   **Note** You didn't specify an "-out" parameter to save this plan, so Terraform can't guarantee that exactly these actions be performed if "terraform apply" is subsequently run.
   ```
   {: screen}
   
5. Create the VPC infrastructure resources. Confirm the creation by entering **yes** when prompted.

   ```
   terraform apply
   ```
   {: pre}
   
   Example output:

   ```
     ibm_is_vpc.vpc: Creating...
     classic_access:         "" => "false"
     default_network_acl:    "" => "<computed>"
     default_security_group: "" => "<computed>"
     is_default:             "" => "false"
     name:                   "" => "newvpc"
     resource_group:         "" => "<computed>"
     status:                 "" => "<computed>"
   ibm_is_vpc.vpc: Creation complete after 8s (ID: 7fe1b2d1-cad1-4058-b7fa-700527c86394)
   ibm_is_security_group.sg1: Creating...
     name:    "" => "newvpc-sg1"
     rules.#: "" => "<computed>"
     vpc:     "" => "<vpc_ID>"
   ibm_is_subnet.subnet1: Creating...
     available_ipv4_address_count: "" => "<computed>"
     ip_version:                   "" => "ipv4"
     ipv4_cidr_block:              "" => "<computed>"
     ipv6_cidr_block:              "" => "<computed>"
     name:                         "" => "newvpc-subnet1"
     network_acl:                  "" => "<computed>"
     status:                       "" => "<computed>"
     total_ipv4_address_count:     "" => "256"
     vpc:                          "" => "<vpc_ID>"
     zone:                         "" => "us-south-2"
   ibm_is_security_group.sg1: Creation complete after 4s (ID: <security_group_ID>)
   ibm_is_security_group_rule.ingress_ssh_all: Creating...
     direction:      "" => "ingress"
     group:          "" => "<security_group_ID>"
     ip_version:     "" => "ipv4"
     remote:         "" => "0.0.0.0/0"
     rule_id:        "" => "<computed>"
     tcp.#:          "" => "1"
     tcp.0.port_max: "" => "22"
     tcp.0.port_min: "" => "22"
   ibm_is_security_group_rule.ingress_ssh_all: Creation complete after 2s (ID: <security_group_rule_ID>)
   ibm_is_subnet.subnet1: Still creating... (10s elapsed)
   ibm_is_subnet.subnet1: Still creating... (20s elapsed)
   ibm_is_subnet.subnet1: Creation complete after 21s (ID: <subnet_ID>)
   ibm_is_instance.vsi1: Creating...
     boot_volume.#:                                         "" => "<computed>"
     cpu.#:                                                 "" => "<computed>"
     generation:                                            "" => "gc"
     gpu.#:                                                 "" => "<computed>"
     image:                                                 "" => "cfdaf1a0-5350-4350-fcbc-97173b510843"
     keys.#:                                                "" => "1"
     keys.3772860677:                                       "" => "<ssh_key_ID>"
     memory:                                                "" => "<computed>"
     name:                                                  "" => "newvpc-vsi2"
     primary_network_interface.#:                           "" => "1"
     primary_network_interface.0.id:                        "" => "<computed>"
     primary_network_interface.0.name:                      "" => "<computed>"
     primary_network_interface.0.primary_ipv4_address:      "" => "<computed>"
     primary_network_interface.0.security_groups.#:         "" => "1"
     primary_network_interface.0.security_groups.152758714: "" => "<security_group_ID>"
     primary_network_interface.0.subnet:                    "" => "<subnet_ID>"
     profile:                                               "" => "cc1-2x4"
     resource_group:                                        "" => "<computed>"
     status:                                                "" => "<computed>"
     vpc:                                                   "" => "<vpc_ID>"
     zone:                                                  "" => "us-south-2"
   ibm_is_instance.vsi1: Still creating... (10s elapsed)
   ibm_is_instance.vsi1: Still creating... (20s elapsed)
   ibm_is_instance.vsi1: Still creating... (30s elapsed)
   ibm_is_instance.vsi1: Still creating... (40s elapsed)
   ibm_is_instance.vsi1: Still creating... (50s elapsed)
   ibm_is_instance.vsi1: Still creating... (1m0s elapsed)
   ibm_is_instance.vsi1: Still creating... (1m10s elapsed)
   ibm_is_instance.vsi1: Still creating... (1m20s elapsed)
   ibm_is_instance.vsi1: Still creating... (1m30s elapsed)
   ibm_is_instance.vsi1: Still creating... (1m40s elapsed)
   ibm_is_instance.vsi1: Creation complete after 1m44s (ID: <vsi_ID>)
   ibm_is_floating_ip.fip1: Creating...
     address: "" => "<computed>"
     name:    "" => "newvpc-fip1"
     status:  "" => "<computed>"
     target:  "" => "<primary_subnet_ID>"
     zone:    "" => "<computed>"
   ibm_is_floating_ip.fip1: Still creating... (10s elapsed)
   ibm_is_floating_ip.fip1: Still creating... (20s elapsed)
   ibm_is_floating_ip.fip1: Creation complete after 24s (ID: <floating_ip_ID>)

   Apply complete! Resources: 6 added, 0 changed, 0 destroyed.

   Outputs:

   sshcommand = ssh root@169.61.123.231
   ```
   {: screen}
   
6. Log in to your VPC virtual server instance by using the `ssh` command that is listed at the end of your CLI output of the previous step.

   ```
   ssh root@169.61.123.231
   ```
   {: pre}
   
   Example output: 

   ```
   The authenticity of host '169.61.123.231 (169.61.123.231)' can't be established.
   ECDSA key fingerprint is SHA256:a1B0aaBCA12V3/AbC2AbcAA/a1Bab1CAAB1aABBabbC.
   Are you sure you want to continue connecting (yes/no)? yes
   Warning: Permanently added '169.61.123.231' (ECDSA) to the list of known hosts.
   Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-30-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/advantage

     System information as of Fri Jun 28 19:06:48 UTC 2019

     System load:  0.15              Processes:           105
     Usage of /:   0.9% of 98.06GB   Users logged in:     0
     Memory usage: 3%                IP address for eth0: 10.240.64.5
     Swap usage:   0%

     Get cloud support with Ubuntu Advantage Cloud Guest:
       http://www.ubuntu.com/business/services/cloud

   0 packages can be updated.
   0 updates are security updates.

   The programs included with the Ubuntu system are free software; the exact distribution terms for each program are described in the individual files in /usr/share/doc/*/copyright.

   Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.

   root@newvpc-vsi2:~# 
   ```
   {: screen}

7. Optional: If you don't want to work with your VPC infrastructure resources anymore, remove them.

   ```
   terraform destroy
   ```
   {: pre}

## Provisioning an {{site.data.keyword.cloud_notm}} Virtual Server for Classic Infrastructure
{: #sample_infrastructure_config}

You can provision your Virtual Server for Classic Infrastructure by using the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. Similar to the {{site.data.keyword.cloud_notm}} Virtual Server for VPC that you provisioned earlier, you create another configuration file with the specification for your virtual server instance. 
{: shortdesc}

Keep in mind that a virtual server is an {{site.data.keyword.cloud_notm}} classic infrastructure resource that incurs costs. Be sure to review the [available plans ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/infrastructure/virtual-server-group) before you proceed.
{: important}

1. Create a configuration file that is named `classic-vsi.tf` with the following content. Store this file in the folder that you created earlier.
 
   ```
   resource "ibm_compute_vm_instance" "vm1" {
   hostname             = "vm1"
   domain               = "example.com"
   os_reference_code    = "DEBIAN_8_64"
   datacenter           = "dal10"
   network_speed        = 10
   hourly_billing       = true
   private_network_only = false
   cores                = 1
   memory               = 1024
   disks                = [25]
   local_disk           = false
   }
   ```
   {: codeblock}
   
   <table>
   <caption>Understanding the configuration file components</caption>
   <col style="width:30%">
	 <col style="width:70%">
   <thead>
     <th>Parameter</th>
     <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>resource</code></td>
   <td>Required: The name of the {{site.data.keyword.cloud_notm}} resource that you want to provision. To provision a classic infrastructure virtual server instance, use <code>ibm_compute_vm_instance</code>. To find a list of other resources that you can provision, see the [{{site.data.keyword.cloud_notm}} Provider plug-in reference](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#configure_provider).  </td>
   </tr>
   <tr>
   <td><code>vm1</code></td>
   <td>Required: Enter a name for your classic infrastructure virtual server instance.  </td>
   </tr>
     <tr>
       <td><code>hostname</code></td>
       <td>Optional: Enter a host name for your classic infrastructure virtual server instance. This host name is used with the <code>domain</code> to create the full URL for your classic infrastructure virtual server instance.</td>
     </tr>
     <tr>
       <td><code>domain</code></td>
       <td>Optional: Enter the domain name that you want to assign to your classic infrastructure virtual server instance. This domain name is used with the <code>hostname</code> to create the full URL for your classic infrastructure virtual server instance.</td>
     </tr>
      <tr>
       <td><code>os_reference_code</code></td>
       <td>Optional: Enter the reference code of the operating system that you want to install on your classic infrastructure virtual server instance. To find available reference codes, log in to the [{{site.data.keyword.cloud_notm}} classic infrastructure API ![External link icon](../icons/launch-glyph.svg "External link icon")](https://api.softlayer.com/rest/v3/SoftLayer_Virtual_Guest_Block_Device_Template_Group/getVhdImportSoftwareDescriptions.json?objectMask=referenceCode).</td>
     </tr>
     <tr>
       <td><code>datacenter</code></td>
       <td>Required: Enter the location where you want to provision your classic infrastructure virtual server instance. For available locations, see the [{{site.data.keyword.cloud_notm}} classic infrastructure API ![External link icon](../icons/launch-glyph.svg "External link icon")](https://api.softlayer.com/rest/v3/SoftLayer_Location/getDatacenters.json?objectMask=name).</td>
     </tr>
     <tr>
       <td><code>network_speed</code></td>
       <td>Optional: Enter the network speed in Mbps for your classic infrastructure virtual server instance. Supported values are 10, 100, and 1000. If you do not specify this value, 100 Mbps is used by default. </td>
     </tr>
     <tr>
       <td><code>hourly_billing</code></td>
       <td>Optional: Specify how you want to get billed for your classic infrastructure virtual server instance. Enter <code>true</code> for hourly billing, and <code>false</code> for monthly billing. If you do not specify a billing type, hourly billing is used by default.</td>
     </tr>
      <tr>
       <td><code>private_network_only</code></td>
       <td>Optional: Decide if you want to connect your classic infrastructure virtual server instance to a private VLAN only. Enter <code>true</code> to connect it to a private VLAN only, and <code>false</code> to connect it to a public and a private VLAN. If you do not specify this option, your virtual server instance is automatically connected to a private and public VLAN by default. </td>
     </tr>
      <tr>
       <td><code>cores</code></td>
       <td>Optional: Enter the number of CPU cores that you want to allocate to your classic infrastructure virtual server instance.</td>
     </tr>
     <tr>
       <td><code>memory</code></td>
       <td>Optional: The amount of memory in megabytes that you want to allocate to your classic infrastructure virtual server instance.</td>
     </tr>
     <tr>
       <td><code>[disks]</code></td>
       <td>Optional: Enter the numeric disk sizes in gigabytes that you want to allocate to your classic infrastructure virtual server instance. To specify multiple disk sizes, separate each value with a comma {`,`). By default, the smallest disk size that is available for the type of virtual server is used.</td>
     </tr>
      <tr>
       <td><code>local_disks</code></td>
       <td>Optional: Specify the type of disk that you want to provision. Enter <code>true</code> to provision the disks on the host that the virtual server instance runs on, or <code>false</code> to provision SAN disks. If you do not specify this option, disks are provisioned on the host by default.</td>
     </tr>
   </tbody>
   </table>
   
2. Initialize Terraform.

    ```
    terraform init
    ```
    {: pre}
   
   Example output: 
   ```
   Initializing provider plugins...

   The following providers do not have any version constraints in configuration, so the latest version was installed.

   To prevent automatic upgrades to new major versions that may contain breaking changes, it is recommended to add version = "..." constraints to the corresponding provider blocks in configuration, with the constraint strings suggested.

   * provider.ibm: version = "~> 0.11"

   Terraform has been successfully initialized!

   You may now begin working with Terraform. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform commands should now work.

   If you ever set or change modules or backend configuration for Terraform, rerun this command to reinitialize your working directory. If you forget, other commands detects it and remind you to do so if necessary.
   ```
   {: screen}
   
3. Generate an Terraform execution plan. When you execute this command, Terraform validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in. 
  
   ```
   terraform plan
   ```
   {: pre}

   Example output:

   ```
   Refreshing Terraform state in-memory prior to plan...
   The refreshed state be used to calculate this plan, but not be persisted to local or remote state storage.

   An execution plan has been generated and is shown.
   Resource actions are indicated with the following symbols:
     + create

   Terraform performs the following actions:

     + ibm_compute_vm_instance.vm1
         id:                           <computed>
         block_storage_ids.#:          <computed>
         cores:                        "1"
         datacenter:                   "dal10"
         disks.#:                      "1"
         disks.0:                      "25"
         domain:                       "example.com"
         file_storage_ids.#:           <computed>
         hostname:                     "vm1"
         hourly_billing:               "true"
         ip_address_id:                <computed>
         ip_address_id_private:        <computed>
         ipv4_address:                 <computed>
         ipv4_address_private:         <computed>
         ipv6_address:                 <computed>
         ipv6_address_id:              <computed>
         ipv6_enabled:                 "false"
         ipv6_static_enabled:          "false"
         local_disk:                   "false"
         memory:                       "1024"
         network_speed:                "10"
         os_reference_code:            "DEBIAN_8_64"
         private_interface_id:         <computed>
         private_network_only:         "false"
         private_security_group_ids.#: <computed>
         private_subnet:               <computed>
         private_subnet_id:            <computed>
         private_vlan_id:              <computed>
         public_bandwidth_limited:     <computed>
         public_bandwidth_unlimited:   "false"
         public_interface_id:          <computed>
         public_ipv6_subnet:           <computed>
         public_ipv6_subnet_id:        <computed>
         public_security_group_ids.#:  <computed>
         public_subnet:                <computed>
         public_subnet_id:             <computed>
         public_vlan_id:               <computed>
         secondary_ip_addresses.#:     <computed>
         wait_time_minutes:            "90"

   Plan: 1 to add, 0 to change, 0 to destroy.
   ------------------------------------------------------------------------
   **Note** You didn't specify an "-out" parameter to save this plan, so Terraform can't guarantee that exactly these actions be performed if "terraform apply" is subsequently run.
   ```
   {: screen}
   
4. Review the execution plan to verify the type of resource that is planned to be provisioned by Terraform.

5. Create your classic infrastructure virtual server. Confirm the creation by entering **yes** when prompted. 

   ```
   terraform apply
   ```
   {: pre} 
   
   Example output:

   ```
   Creating...
     block_storage_ids.#:        "" => "<computed>"
     cores:                      "" => "1"
     datacenter:                 "" => "dal10"
     disks.#:                    "" => "1"
     disks.0:                    "" => "25"
     domain:                     "" => "example.com"
     file_storage_ids.#:         "" => "<computed>"
     hostname:                   "" => "vm1"
     hourly_billing:             "" => "true"
     ip_address_id:              "" => "<computed>"
     ip_address_id_private:      "" => "<computed>"
     ipv4_address:               "" => "<computed>"
     ipv4_address_private:       "" => "<computed>"
     ipv6_address:               "" => "<computed>"
     ipv6_address_id:            "" => "<computed>"
     ipv6_enabled:               "" => "false"
     local_disk:                 "" => "false"
     memory:                     "" => "1024"
     network_speed:              "" => "10"
     os_reference_code:          "" => "DEBIAN_8_64"
     private_network_only:       "" => "false"
     private_subnet:             "" => "<computed>"
     private_vlan_id:            "" => "<computed>"
     public_bandwidth_limited:   "" => "<computed>"
     public_bandwidth_unlimited: "" => "false"
     public_ipv6_subnet:         "" => "<computed>"
     public_subnet:              "" => "<computed>"
     public_vlan_id:             "" => "<computed>"
     secondary_ip_addresses.#:   "" => "<computed>"
     wait_time_minutes:          "" => "90"
   ibm_compute_vm_instance.vm1: Still creating... (10s elapsed)
   ibm_compute_vm_instance.vm1: Still creating... (20s elapsed)
   ibm_compute_vm_instance.vm1: Still creating... (30s elapsed)
   ibm_compute_vm_instance.vm1: Still creating... (40s elapsed)
   ibm_compute_vm_instance.vm1: Still creating... (50s elapsed)
   ibm_compute_vm_instance.vm1: Still creating... (1m0s elapsed)
   ibm_compute_vm_instance.vm1: Creation complete after 1m04s (ID: 62364997)
   
   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
   ```
   {: screen}
   
6. List the classic infrastructure virtual server that is provisioned. 
   
   ```
    terraform show
   ```
   {: pre}
   
   Example output: 
   ```
   ibm_compute_vm_instance.vm1:
     id = 62364997
     block_storage_ids.# = 0
     cores = 1
     datacenter = dal10
     dedicated_acct_host_only = false
     disks.# = 1
     disks.0 = 25
     domain = example.com
     file_storage_ids.# = 0
     hostname = vm1
     hourly_billing = true
     ip_address_id = 120354689
     ip_address_id_private = 120356235
     ipv4_address = 169.53.33.54
     ipv4_address_private = 10.120.45.183
     ipv6_enabled = false
     local_disk = false
     memory = 1024
     network_speed = 10
     notes = 
     os_reference_code = DEBIAN_8_64
     private_network_only = false
     private_subnet = 10.120.45.128/26
     private_vlan_id = 2451153
     public_bandwidth_unlimited = false
     public_subnet = 169.53.33.48/28
     public_vlan_id = 2451151
     secondary_ip_addresses.# = 0
     wait_time_minutes = 90
   ```
   {: screen}

7. Optional: Review your classic virtual server instance in the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/classic/devices). 

8. Optional: Remove your classic infrastructure virtual server. 

   ```
   terraform destroy
   ```
   {: pre}

**What's next?** </br>

[Explore other {{site.data.keyword.cloud_notm}} resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#configure_provider) that you can provision with Terraform. 
