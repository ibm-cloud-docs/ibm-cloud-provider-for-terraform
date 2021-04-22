---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-22"

keywords: Add resources, remove resources, iaas, softlayer, ibm cloud resources, ibm cloud services, Terraform on {{site.data.keyword.cloud_notm}}, provision resources

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




# Managing {{site.data.keyword.cloud_notm}} resources with Terraform on {{site.data.keyword.cloud_notm}}
{: #manage_resources}

Use the Terraform CLI to create, update, and delete platform and infrastructure services in {{site.data.keyword.cloud_notm}}. 
{: shortdesc}

## Provisioning IBM Cloud resources
{: #provision_resources}

To provision {{site.data.keyword.cloud_notm}} resources, you must describe the state of your resources that you want to achieve in a configuration file.  
{: shortdesc}

Terraform on {{site.data.keyword.cloud_notm}} configuration files are written by using the [HashiCorp Configuration Language (HCL) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.terraform.io/docs/language/syntax/configuration.html) or JSON syntax. When you create your configuration file, you must describe the type of resource that you want and the state that you want to achieve for your resource. Terraform on {{site.data.keyword.cloud_notm}} reads this configuration and creates an execution plan with the steps that were identified to achieve the specified state. If existing resources are found, Terraform on {{site.data.keyword.cloud_notm}} identifies the necessary steps to update them. 

Before you begin: 
- [Install the Terraform on {{site.data.keyword.cloud_notm}} command line and the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#setup_cli).
- [Configure the {{site.data.keyword.cloud_notm}} Provider plug-in to use your {{site.data.keyword.cloud_notm}} credentials](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#configure_provider). 

The following example shows how you can configure a virtual server in {{site.data.keyword.cloud_notm}} by using JSON syntax. A virtual server is an {{site.data.keyword.cloud_notm}} infrastructure resource that incurs costs. Be sure to review [available plans ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/infrastructure/virtual-server-group) before you proceed. 
{: important} 

Looking for other resource types? Find a complete list of supported resource types in the [{{site.data.keyword.cloud_notm}} Provider plug-in reference](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#configure_provider). 
{: tip}

1. Create a configuration file that is named `sample.tf` with the following content. Configuration file names must have the `.tf` extension to be found by Terraform on {{site.data.keyword.cloud_notm}}. Store this file in the same folder that you used to store your {{site.data.keyword.cloud_notm}} credentials.

   ```
   resource "ibm_compute_vm_instance" "vm1" {
    hostname = "vm1"
    domain = "example.com"
    os_reference_code = "DEBIAN_8_64"
    datacenter = "dal09"
    network_speed = 10
    hourly_billing = true
    private_network_only = false
    cores = 1
    memory = 1024
    disks = [25]
    local_disk = false
   }
   ```
   {: codeblock}
   
2. Initialize Terraform on {{site.data.keyword.cloud_notm}}. 

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

   Terraform on {{site.data.keyword.cloud_notm}} has been successfully initialized!

   You may now begin working with Terraform on {{site.data.keyword.cloud_notm}}. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform on {{site.data.keyword.cloud_notm}} commands should now work.

   If you ever set or change modules or backend configuration for Terraform on {{site.data.keyword.cloud_notm}}, rerun this command to reinitialize your working directory. If you forget, other commands detects it and remind you to do so if necessary.
   ```
   {: screen}
   
3. Generate an Terraform on {{site.data.keyword.cloud_notm}} execution plan. When you execute this command, Terraform on {{site.data.keyword.cloud_notm}} validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in.

   ```
   terraform plan
   ```
   {: pre}

   Example output:

   ```
   Refreshing Terraform on {{site.data.keyword.cloud_notm}} state in-memory prior to plan...
   The refreshed state be used to calculate this plan, but not be persisted to local or remote state storage.

   An execution plan has been generated and is shown here.
   Resource actions are indicated with the following symbols:
     + create

   Terraform on {{site.data.keyword.cloud_notm}} perform the following actions:

     + ibm_compute_vm_instance.vm1
         id:                           <computed>
         block_storage_ids.#:          <computed>
         cores:                        "1"
         datacenter:                   "dal09"
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
   **Note** You didn't specify an "-out" parameter to save this plan, so Terraform on {{site.data.keyword.cloud_notm}} can't guarantee that exactly these actions be performed if "terraform apply" is subsequently run.
   ```
   {: screen}
   
4. Review the execution plan to verify the steps that were identified by Terraform on {{site.data.keyword.cloud_notm}} to provision the virtual server.  

5. Create your infrastructure resources.  
   
   ```
   terraform apply
   ```
   {: pre} 
   
   Confirm the creation of infrastructure resources by entering **yes** when prompted. 
   
   Example output: 
   ```
   Creating...
     block_storage_ids.#:        "" => "<computed>"
     cores:                      "" => "1"
     datacenter:                 "" => "dal09"
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
   
   
## Updating IBM Cloud resources
{: #update_resources}

You can update your resources by changing your Terraform on {{site.data.keyword.cloud_notm}} configuration file and applying these changes in your environment. 
{: shortdesc}

1. List your {{site.data.keyword.cloud_notm}} resources. 
   
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
     datacenter = dal09
     dedicated_acct_host_only = false
     disks.# = 1
     disks.0 = 25
     domain = example.com
     file_storage_ids.# = 0
     hostname = vm1
     hourly_billing = true
     ip_address_id = 119153307
     ip_address_id_private = 119154963
     ipv4_address = 169.46.192.34
     ipv4_address_private = 10.173.135.134
     ipv6_enabled = false
     ipv6_static_enabled = false
     local_disk = false
     memory = 1024
     network_speed = 10
     notes = 
     os_reference_code = DEBIAN_8_64
     private_interface_id = 35066699
     private_network_only = false
     private_security_group_ids.# = 0
     private_subnet = 10.173.135.128/26
     private_subnet_id = 1304363
     private_vlan_id = 2433445
     public_bandwidth_unlimited = false
     public_interface_id = 35066701
     public_security_group_ids.# = 0
     public_subnet = 169.46.192.32/28
     public_subnet_id = 1810073
     public_vlan_id = 2433443
     secondary_ip_addresses.# = 0
     wait_time_minutes = 90
   ```
   {: screen}
   
2. Open your `sample.tf` configuration file and change a value. For example, you can change the **network_speed** to **100**. To find an overview of parameters that you can change, see the [{{site.data.keyword.cloud_notm}} resource reference](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#configure_provider).
   
3. Create an Terraform on {{site.data.keyword.cloud_notm}} execution plan.
 
   ```
   terraform plan
   ```
   {: pre}
   
   Example output: 

   ```
   Refreshing Terraform on {{site.data.keyword.cloud_notm}} state in-memory prior to plan...
   The refreshed state be used to calculate this plan, but not be persisted to local or remote state storage.

   ibm_compute_vm_instance.vm1: Refreshing state... (ID: 51404681)

   ---------------------------------------------------------------

   An execution plan has been generated and is shown here.
   Resource actions are indicated with the following symbols:
    ~ update in-place

   Terraform on {{site.data.keyword.cloud_notm}} performs the following actions:

    ~ ibm_compute_vm_instance.vm1
    network_speed: "10" => "100"

   Plan: 0 to add, 1 to change, 0 to destroy.
   ```
   {: screen}
   
4. Apply the changes to your {{site.data.keyword.cloud_notm}} resources.

   ```
   terraform apply
   ```
   {: pre}
   
5. Verify that your {{site.data.keyword.cloud_notm}} resources are updated.

   ```
   terraform show
   ```
   {: pre}

## Removing IBM Cloud resources 
{: #remove_resources}

You can use Terraform on {{site.data.keyword.cloud_notm}} to remove {{site.data.keyword.cloud_notm}} resources if you do not want them anymore. 
{: shortdesc}

1. Show the summary of steps that Terraform on {{site.data.keyword.cloud_notm}} identified to remove your {{site.data.keyword.cloud_notm}} resources. 

   ```
   terraform plan -destroy
   ```
   {: pre}
   
2. Verify the Terraform on {{site.data.keyword.cloud_notm}} execution plan. 

3. Remove your {{site.data.keyword.cloud_notm}} resources. 

   ```
   terraform destroy
   ```
   {: pre}
   
   Example output:

   ```
   ibm_compute_vm_instance.vm1: Refreshing state... (ID: 60948867)
   An execution plan has been generated and is shown here.
   Resource actions are indicated with the following symbols:
     - destroy

   Terraform on {{site.data.keyword.cloud_notm}} performs the following actions:

     - ibm_compute_vm_instance.vm1

   Plan: 0 to add, 0 to change, 1 to destroy.

   Do you really want to destroy?
     Terraform on {{site.data.keyword.cloud_notm}} destroys all your managed infrastructure, as shown above.
     There is no undo. Only 'yes' is accepted to confirm.

     Enter a value: yes

   ibm_compute_vm_instance.vm1: Destroying... (ID: 60948867)
   ibm_compute_vm_instance.vm1: Still destroying... (ID: 60948867, 10s elapsed)
   ibm_compute_vm_instance.vm1: Destruction complete after 14s
   Destroy complete! Resources: 1 destroyed.
   ```
   {: screen}
   
4. Verify that your {{site.data.keyword.cloud_notm}} resources are removed.
 
   ```
   terraform show
   ```
   {: pre}
   
