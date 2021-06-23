---

copyright:
  years: 2017, 2021
lastupdated: "2021-06-23"

keywords: terraform quickstart, terraform getting started, terraform tutorial, virtual server for vpc

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
{:terraform: .ph data-hd-interface='terraform'}
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



# Provisioning an {{site.data.keyword.cloud_notm}} virtual server for VPC
{: #sample_vpc_config}

Use {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on {{site.data.keyword.cloud_notm}} to provision a VPC, and set up networking for your VPC, and provision a virtual server for VPC in your {{site.data.keyword.cloud_notm}} account. 
{: shortdesc}

A VPC allows you to create your own space in {{site.data.keyword.cloud_notm}} so that you can run an isolated environment in the public cloud with custom network policies. The example in this topic provisions the following VPC infrastructure resources for you: 
- 1 VPC where you provision your VPC virtual server instance
- 1 security group and a rule for this security group to allow SSH connection to your virtual server instance
- 1 subnet to enable networking in your VPC
- 1 VPC virtual server instance 
- 1 floating IP address that you use to access your VPC virtual server instance over the public network

Keep in mind that a VPC virtual server instance is an {{site.data.keyword.cloud_notm}} VPC infrastructure resource that incurs costs. Be sure to review the [available plans](https://cloud.ibm.com/vpc/provision/vs) before you proceed.
{: important}

Before you begin: 
 - Install the [latest Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#tf_installation) and the latest [{{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider).
- [Retrieve your {{site.data.keyword.cloud_notm}} credentials, upload an SSH key, and configure the {{site.data.keyword.cloud_notm}} Provider plug-in forTerraform on {{site.data.keyword.cloud_notm}} provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider). 

To create a VPC and a VSI: 

1. Make sure that you have the [required permissions](/docs/vpc?topic=vpc-resource-authorizations-required-for-api-and-cli-calls) to create and work with VPC infrastructure. 

2. In the Terraform on {{site.data.keyword.cloud_notm}} directory create a `versions.tf` file to run the required Terraform on {{site.data.keyword.cloud_notm}} version. For `versions.tf`, refer to [sample versions tf file](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install-provider-v13).

   ```
   terraform {
    required_providers {
      ibm = {
         source = "IBM-Cloud/ibm"
         version = "1.26.2"
       }
     }
   }
   ```
   {: codeblock}

3. In the Terraform on {{site.data.keyword.cloud_notm}} directory create a Terraform on {{site.data.keyword.cloud_notm}} configuration file and name it `vpc.tf`. The configuration file includes the following definition blocks: 
   - **locals**: Use this block to specify variables that you want to use multiple times throughout this configuration file. 
   - **resource**: Every resource block specifies the {{site.data.keyword.cloud_notm}} resource that you want to provision. To find more information about supported configurations for each resource, see the [{{site.data.keyword.cloud_notm}} provider plug-in reference](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider).
   - **data**: Use this block to retrieve information for an existing resource in your {{site.data.keyword.cloud_notm}} account. 
   - **output**: This block specifies commands that you want to run after your resources are provisioned. 
   
   **Example configuration file:** 

   ```
    variable "ssh_key" {
    }

    locals {
      BASENAME = "gsmvpcv13test2"
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

    data "ibm_is_image" "centos" {
      name = "ibm-centos-7-6-minimal-amd64-1"
    }

    data "ibm_is_ssh_key" "ssh_key_id" {
      name = var.ssh_key
    }

    resource "ibm_is_instance" "vsi1" {
      name    = "${local.BASENAME}-vsi1"
      vpc     = ibm_is_vpc.vpc.id
      zone    = local.ZONE
      keys    = [data.ibm_is_ssh_key.ssh_key_id.id]
      image   = data.ibm_is_image.centos.id
      profile = "cx2-2x4"

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
       <td>Enter the UUID of the SSH key that you uploaded to your {{site.data.keyword.cloud_notm}} account. In this example, you retrieve the UUID from the <code>ibm_is_ssh_key</code> data source of this configuration file. Terraform on {{site.data.keyword.cloud_notm}} uses the name of the SSH key that you define in your data source object to look up information about the SSH key in your {{site.data.keyword.cloud_notm}} account.</td>
     </tr>
     <tr>
       <td><code>resource.ibm_is_instance.image</code></td>
       <td>Enter the ID of the image that represents the Operating System that you want to install on your VPC virtual server instance. In this example, you retrieve the ID from the <code>ibm_is_image</code> data source of this configuration file. Terraform on {{site.data.keyword.cloud_notm}} uses the name of the image that you define in your data source object to look up information about the image in the {{site.data.keyword.cloud_notm}} infrastructure portfolio. </td>
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

3. Initialize Terraform on {{site.data.keyword.cloud_notm}}. 

   ```
   terraform init
   ```
   {: pre}
   
   **Example output:**

   ```
    2021/06/22 16:47:27 [WARN] Log levels other than TRACE are currently unreliable, and are supported only for backward compatibility.
    Use TF_LOG=TRACE to see Terraform's internal logs.
    ----
    2021/06/22 16:47:27 [INFO] Terraform version: 0.13.5  
    2021/06/22 16:47:27 [INFO] Go runtime version: go1.14.7
    2021/06/22 16:47:27 [INFO] CLI args: []string{"/Users/geethasathyamurthy/terraform/terraform", "init"}
    2021/06/22 16:47:27 [DEBUG] Attempting to open CLI config file: /Users/geethasathyamurthy/.terraformrc
    2021/06/22 16:47:27 [DEBUG] File doesn't exist, but doesn't need to. Ignoring.
    2021/06/22 16:47:27 [DEBUG] ignoring non-existing provider search directory terraform.d/plugins
    2021/06/22 16:47:27 [DEBUG] ignoring non-existing provider search directory /Users/geethasathyamurthy/.terraform.d/plugins
    2021/06/22 16:47:27 [DEBUG] ignoring non-existing provider search directory /Users/geethasathyamurthy/Library/Application Support/io.terraform/plugins
    2021/06/22 16:47:27 [DEBUG] ignoring non-existing provider search directory /Library/Application Support/io.terraform/plugins
    2021/06/22 16:47:27 [INFO] CLI command args: []string{"init"}
    2021/06/22 16:47:27 [WARN] Log levels other than TRACE are currently unreliable, and are supported only for backward compatibility.
    Use TF_LOG=TRACE to see Terraform's internal logs.
    ----

    Initializing the backend...
    2021/06/22 16:47:27 [DEBUG] New state was assigned lineage "ec69aeac-0645-6299-244d-da5f238dcaad"
    2021/06/22 16:47:27 [DEBUG] checking for provisioner in "."
    2021/06/22 16:47:27 [DEBUG] checking for provisioner in "/Users/geethasathyamurthy/terraform"
    2021/06/22 16:47:27 [INFO] Failed to read plugin lock file .terraform/plugins/darwin_amd64/lock.json: open .terraform/plugins/darwin_amd64/lock.json: no such file or directory

    Initializing provider plugins...
    - Using previously-installed ibm-cloud/ibm v1.26.2

    Terraform has been successfully initialized!

    You may now begin working with Terraform. Try running "terraform plan" to see
    any changes that are required for your infrastructure. All Terraform commands
    should now work.

    If you ever set or change modules or backend configuration for Terraform,
    rerun this command to reinitialize your working directory. If you forget, other
    commands will detect it and remind you to do so if necessary.

   ```
   {: screen}
4. From your Terraform directory, export following `IC_API_Key` and `TF_LOG` variable to set your environment variable.
   
   **Example**

    - `export IC_API_KEY=VoeEd1231231234134123413`
    - `export TF_LOG=debug`
5. Generate an Terraform on {{site.data.keyword.cloud_notm}} execution plan. When you execute this command, Terraform on {{site.data.keyword.cloud_notm}} validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in.

   Your SSH key name need to be provide during terraform plan and terraform apply execution.
   {: note}

   ```
   terraform plan
   ```
   {: pre}

   **Example output:** 

   ```
    var.ssh_key
      Enter a value: <Provide your SSH key name>
    2021/06/22 16:48:53 [INFO] backend/local: plan operation completed

    An execution plan has been generated and is shown below.
    Resource actions are indicated with the following symbols:
      + create

    Terraform will perform the following actions:

      ibm_is_floating_ip.fip1 will be created
      + resource "ibm_is_floating_ip" "fip1" {
          + address                 = (known after apply)
          + id                      = (known after apply)
          + name                    = "gsmvpcv13test2-fip1"
          + resource_controller_url = (known after apply)
          + resource_crn            = (known after apply)
          + resource_group          = (known after apply)
          + resource_group_name     = (known after apply)
          + resource_name           = (known after apply)
          + resource_status         = (known after apply)
          + status                  = (known after apply)
          + tags                    = (known after apply)
          + target                  = (known after apply)
          + zone                    = (known after apply)
        }

      ibm_is_instance.vsi1 will be created
      + resource "ibm_is_instance" "vsi1" {
          + disks                   = (known after apply)
          + gpu                     = (known after apply)
          + id                      = (known after apply)
          + image                   = "r006-e0039ab2-fcc8-11e9-8a36-6ffb6501dd33"
          + keys                    = [
              + "r006-3f44b01f-5edc-434b-ba6b-f5de782759f7",
            ]
          + memory                  = (known after apply)
          + name                    = "gsmvpcv13test2-vsi1"
          + profile                 = "cx2-2x4"
          + resource_controller_url = (known after apply)
          + resource_crn            = (known after apply)
          + resource_group          = (known after apply)
          + resource_group_name     = (known after apply)
          + resource_name           = (known after apply)
          + resource_status         = (known after apply)
          + status                  = (known after apply)
          + tags                    = (known after apply)
          + vcpu                    = (known after apply)
          + volume_attachments      = (known after apply)
          + vpc                     = (known after apply)
          + wait_before_delete      = true
          + zone                    = "us-south-1"

          + boot_volume {
              + encryption = (known after apply)
              + iops       = (known after apply)
              + name       = (known after apply)
              + profile    = (known after apply)
              + size       = (known after apply)
            }

          + primary_network_interface {
              + allow_ip_spoofing    = false
              + id                   = (known after apply)
              + name                 = (known after apply)
              + primary_ipv4_address = (known after apply)
              + security_groups      = (known after apply)
              + subnet               = (known after apply)
            }
        }

      ibm_is_security_group.sg1 will be created
      + resource "ibm_is_security_group" "sg1" {
          + crn                     = (known after apply)
          + id                      = (known after apply)
          + name                    = "gsmvpcv13test2-sg1"
          + resource_controller_url = (known after apply)
          + resource_crn            = (known after apply)
          + resource_group          = (known after apply)
          + resource_group_name     = (known after apply)
          + resource_name           = (known after apply)
          + rules                   = (known after apply)
          + tags                    = (known after apply)
          + vpc                     = (known after apply)
        }

      ibm_is_security_group_rule.ingress_ssh_all will be created
      + resource "ibm_is_security_group_rule" "ingress_ssh_all" {
          + direction   = "inbound"
          + group       = (known after apply)
          + id          = (known after apply)
          + ip_version  = "ipv4"
          + protocol    = (known after apply)
          + related_crn = (known after apply)
          + remote      = "0.0.0.0/0"
          + rule_id     = (known after apply)

          + tcp {
              + port_max = 22
              + port_min = 22
            }
        }

      ibm_is_subnet.subnet1 will be created
      + resource "ibm_is_subnet" "subnet1" {
          + available_ipv4_address_count = (known after apply)
          + crn                          = (known after apply)
          + id                           = (known after apply)
          + ip_version                   = "ipv4"
          + ipv4_cidr_block              = (known after apply)
          + ipv6_cidr_block              = (known after apply)
          + name                         = "gsmvpcv13test2-subnet1"
          + network_acl                  = (known after apply)
          + resource_controller_url      = (known after apply)
          + resource_crn                 = (known after apply)
          + resource_group               = (known after apply)
          + resource_group_name          = (known after apply)
          + resource_name                = (known after apply)
          + resource_status              = (known after apply)
          + routing_table                = (known after apply)
          + status                       = (known after apply)
          + tags                         = (known after apply)
          + total_ipv4_address_count     = 256
          + vpc                          = (known after apply)
          + zone                         = "us-south-1"
        }

      ibm_is_vpc.vpc will be created
      + resource "ibm_is_vpc" "vpc" {
          + address_prefix_management   = "auto"
          + classic_access              = false
          + crn                         = (known after apply)
          + cse_source_addresses        = (known after apply)
          + default_network_acl         = (known after apply)
          + default_network_acl_name    = (known after apply)
          + default_routing_table       = (known after apply)
          + default_routing_table_name  = (known after apply)
          + default_security_group      = (known after apply)
          + default_security_group_name = (known after apply)
          + id                          = (known after apply)
          + name                        = "gsmvpcv13test2-vpc"
          + resource_controller_url     = (known after apply)
          + resource_crn                = (known after apply)
          + resource_group              = (known after apply)
          + resource_group_name         = (known after apply)
          + resource_name               = (known after apply)
          + resource_status             = (known after apply)
          + security_group              = (known after apply)
          + status                      = (known after apply)
          + subnets                     = (known after apply)
          + tags                        = (known after apply)
        }

    Plan: 6 to add, 0 to change, 0 to destroy.

    ------------------------------------------------------------------------

    **Note** You didn't specify an "-out" parameter to save this plan, so Terraform
    can't guarantee that exactly these actions will be performed if
    "terraform apply" is subsequently run.
   ```
   {: screen}
   
5. Create the VPC infrastructure resources. Confirm the creation by entering `yes` when prompted.

   ```
   terraform apply
   ```
   {: pre}
   
   **Example output:**

   ```
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # ibm_is_floating_ip.fip1 will be created
  + resource "ibm_is_floating_ip" "fip1" {
      + address                 = (known after apply)
      + id                      = (known after apply)
      + name                    = "gsmvpcv13test2-fip1"
      + resource_controller_url = (known after apply)
      + resource_crn            = (known after apply)
      + resource_group          = (known after apply)
2021/06/22 16:57:25 [DEBUG] command: asking for input: "Do you want to perform these actions?"
      + resource_group_name     = (known after apply)
      + resource_name           = (known after apply)
      + resource_status         = (known after apply)
      + status                  = (known after apply)
      + tags                    = (known after apply)
      + target                  = (known after apply)
      + zone                    = (known after apply)
    }

  # ibm_is_instance.vsi1 will be created
  + resource "ibm_is_instance" "vsi1" {
      + disks                   = (known after apply)
      + gpu                     = (known after apply)
      + id                      = (known after apply)
      + image                   = "r006-e0039ab2-fcc8-11e9-8a36-6ffb6501dd33"
      + keys                    = [
          + "r006-3f44b01f-5edc-434b-ba6b-f5de782759f7",
        ]
      + memory                  = (known after apply)
      + name                    = "gsmvpcv13test2-vsi1"
      + profile                 = "cx2-2x4"
      + resource_controller_url = (known after apply)
      + resource_crn            = (known after apply)
      + resource_group          = (known after apply)
      + resource_group_name     = (known after apply)
      + resource_name           = (known after apply)
      + resource_status         = (known after apply)
      + status                  = (known after apply)
      + tags                    = (known after apply)
      + vcpu                    = (known after apply)
      + volume_attachments      = (known after apply)
      + vpc                     = (known after apply)
      + wait_before_delete      = true
      + zone                    = "us-south-1"

      + boot_volume {
          + encryption = (known after apply)
          + iops       = (known after apply)
          + name       = (known after apply)
          + profile    = (known after apply)
          + size       = (known after apply)
        }

      + primary_network_interface {
          + allow_ip_spoofing    = false
          + id                   = (known after apply)
          + name                 = (known after apply)
          + primary_ipv4_address = (known after apply)
          + security_groups      = (known after apply)
          + subnet               = (known after apply)
        }
    }

  # ibm_is_security_group.sg1 will be created
  + resource "ibm_is_security_group" "sg1" {
      + crn                     = (known after apply)
      + id                      = (known after apply)
      + name                    = "gsmvpcv13test2-sg1"
      + resource_controller_url = (known after apply)
      + resource_crn            = (known after apply)
      + resource_group          = (known after apply)
      + resource_group_name     = (known after apply)
      + resource_name           = (known after apply)
      + rules                   = (known after apply)
      + tags                    = (known after apply)
      + vpc                     = (known after apply)
    }

  # ibm_is_security_group_rule.ingress_ssh_all will be created
  + resource "ibm_is_security_group_rule" "ingress_ssh_all" {
      + direction   = "inbound"
      + group       = (known after apply)
      + id          = (known after apply)
      + ip_version  = "ipv4"
      + protocol    = (known after apply)
      + related_crn = (known after apply)
      + remote      = "0.0.0.0/0"
      + rule_id     = (known after apply)

      + tcp {
          + port_max = 22
          + port_min = 22
        }
    }

  # ibm_is_subnet.subnet1 will be created
  + resource "ibm_is_subnet" "subnet1" {
      + available_ipv4_address_count = (known after apply)
      + crn                          = (known after apply)
      + id                           = (known after apply)
      + ip_version                   = "ipv4"
      + ipv4_cidr_block              = (known after apply)
      + ipv6_cidr_block              = (known after apply)
      + name                         = "gsmvpcv13test2-subnet1"
      + network_acl                  = (known after apply)
      + resource_controller_url      = (known after apply)
      + resource_crn                 = (known after apply)
      + resource_group               = (known after apply)
      + resource_group_name          = (known after apply)
      + resource_name                = (known after apply)
      + resource_status              = (known after apply)
      + routing_table                = (known after apply)
      + status                       = (known after apply)
      + tags                         = (known after apply)
      + total_ipv4_address_count     = 256
      + vpc                          = (known after apply)
      + zone                         = "us-south-1"
    }

  # ibm_is_vpc.vpc will be created
  + resource "ibm_is_vpc" "vpc" {
      + address_prefix_management   = "auto"
      + classic_access              = false
      + crn                         = (known after apply)
      + cse_source_addresses        = (known after apply)
      + default_network_acl         = (known after apply)
      + default_network_acl_name    = (known after apply)
      + default_routing_table       = (known after apply)
      + default_routing_table_name  = (known after apply)
      + default_security_group      = (known after apply)
      + default_security_group_name = (known after apply)
      + id                          = (known after apply)
      + name                        = "gsmvpcv13test2-vpc"
      + resource_controller_url     = (known after apply)
      + resource_crn                = (known after apply)
      + resource_group              = (known after apply)
      + resource_group_name         = (known after apply)
      + resource_name               = (known after apply)
      + resource_status             = (known after apply)
      + security_group              = (known after apply)
      + status                      = (known after apply)
      + subnets                     = (known after apply)
      + tags                        = (known after apply)
    }

   Apply complete! Resources: 6 added, 0 changed, 0 destroyed.

   Outputs:

   sshcommand = ssh root@ibm_is_floating_ip.fip1.address
   ```
   {: screen}
   
6. Log in to your VPC VSI by using the `ssh` command that is listed at the end of your command line output of the previous step.

   ```
   ssh root@52.118.150.55 
   ```
   {: pre}
   
   **Example output:**

   ```
    The authenticity of host '52.116.134.139 (52.116.134.139)' can't be established.
    ECDSA key fingerprint is SHA256:ZZRZY07mx3ccmnS5+Tip7eDDVSL7jlunPbANcrCeEYE.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added '52.116.134.139' (ECDSA) to the list of known hosts.

    -bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
    [root@gsmvpcv13test2-vsi1 ~]#
   ```
   {: screen}

7. Optional: If you don't want to work with your VPC infrastructure resources anymore, remove them.

   ```
   terraform destroy
   ```
   {: pre}

8. You can verify that VPC and VSI are created by accessing your IBM Cloud console. 
   - Click **Menu icon**  > **VPC Infrastructure** >  **VPCs** to view your VPC named `gsmvpcv13test2-vpc` is created 
   - Click **Menu icon** > **VPC Infrastructure** > **Virtual server instances** to view your VSI named `gsmvpcv13test2_vsi1` is created 


**What's next?**

Explore other [{{site.data.keyword.cloud_notm}} resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-index-of-terraform-on-ibm-cloud-resources-and-data-sources) that you can provision with Terraform on {{site.data.keyword.cloud_notm}}. 

