---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-14"

keywords: terraform quickstart, terraform getting started, terraform tutorial, virtual server for classic infrastructure

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an {{site.data.keyword.cloud_notm}} virtual server for classic infrastructure
{: #sample_infrastructure_config}

You can provision your virtual server for classic infrastructure by using the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on IBM Cloud. Similar to the [{{site.data.keyword.cloud_notm}} virtual server for VPC provision](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). that you provisioned. You need to create another configuration file with the specification for your virtual server instance. 
{: shortdesc}

Keep in mind that a virtual server is an {{site.data.keyword.cloud_notm}} classic infrastructure resource that incurs costs. Be sure to review the [available plans ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/gen1/infrastructure/provision/vs) before you proceed.
{: important}

## Prerequisities
{: pre}
https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#env-vars

1. Create a configuration file that is named `classic-vsi.tf` with the following content. Store this file in the folder that you created earlier.
 
    ```terraform
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

    For more information, about the `ibm_compute_vm_instance` resource description for the argument and its values, refer to [Argument reference](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/compute_vm_instance#argument-reference){: external}

2. Create a configuration file that is named `versions.tf` with the following content. Store this file in the folder that you created earlier.
   ```terraform
    terraform {
        required_version = ">=1.0.0, <2.0"
        required_providers {
            ibm = {
                source = "IBM-Cloud/ibm"
            }
        }
    }
    ```
    {: pre}

3. Initialize Terraform on IBM Cloud.

    ```sh
    terraform init
    ```
    {: pre}

4. Generate an Terraform on IBM Cloud execution plan. When you execute this command, Terraform on IBM Cloud validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in. 
  
    ```sh
    terraform plan
    ```
    {: pre}

5. Review the execution plan to verify the type of resource that is planned to be provisioned by Terraform on IBM Cloud.
6. Create your classic infrastructure virtual server. Confirm the creation by entering `yes` when prompted. 

    ```sh
    terraform apply
    ```
    {: pre} 

    **Example output:**

    ```text
      Creating...

       ibm_compute_vm_instance.vm1: Still creating... (40s elapsed)
       ibm_compute_vm_instance.vm1: Still creating... (50s elapsed)
       ibm_compute_vm_instance.vm1: Still creating... (1m0s elapsed)
       ibm_compute_vm_instance.vm1: Creation complete after 1m04s (ID: 62364997)
       
       Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
    ```
    {: screen}

7. List the classic infrastructure virtual server that is provisioned. 
   
    ```sh
    terraform show
    ```
    {: pre}

    **Example output:**

    ```text
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

8. Optional: Review your classic virtual server instance in the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/classic/devices).

9. Optional: Remove your classic infrastructure virtual server.

    ```sh
    terraform destroy
    ```
    {: pre}

**What's next?**

Explore other [{{site.data.keyword.cloud_notm}} resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider) that you can provision with Terraform on IBM Cloud.
