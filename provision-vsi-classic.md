---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-16"

keywords: terraform quickstart, terraform getting started, terraform tutorial, virtual server for classic infrastructure

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an {{site.data.keyword.cloud_notm}} virtual server for classic infrastructure
{: #sample_infrastructure_config}
{: toc-content-type="tutorial"}
{: toc-services="containers, terraform, openshift"}
{: toc-completion-time="2h"}


You can provision your virtual server for classic infrastructure by using the {{site.data.keyword.cloud_notm}} Provider plug-in. Similar to the [{{site.data.keyword.cloud_notm}} virtual server for VPC provision](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started) that you provisioned. You need to create another configuration file with the specification for your virtual server instance. 
{: shortdesc}

Keep in mind that a virtual server is an {{site.data.keyword.cloud_notm}} classic infrastructure resource that incurs costs. Be sure to review the [available plans](https://cloud.ibm.com/gen1/infrastructure/provision/vs) before you proceed.
{: important}

## Objectives
{: #classic-tutorial-objective}

In this tutorial, you will:

- Learn how to configure a virtual server for classic infrastructure with `DEBIAN_8_64` Operating System by using {{site.data.keyword.cloud_notm}} Provider.
- Learn to configure the latest `Terraform version 1.0` and higher in `version.tf` file.
- Terraform commands to provision the resource.
- Destroy the configured virtual server for classic infrastructure.

## Prerequisities
{: #classic-tutorial-prereq}

1. Create your new folder in your local machine or [Git repository](/docs/sell?topic=sell-source-repo-setup) to configure the Terraform configuration files.
2. Setup the Terraform installation and configuration. For more information, see [installation and testing the configuration](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#tf_installation).
3. Setup the environment variable such as `IC_API_KEY`, `IAAS_CLASSIC_USERNAME`, and `IAAS_CLASS_API_KEY` on your local machine. For more information, about how to setup the environment variables? see [Using environment variable](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#env-vars).


## Audience
{: #classic-tutorial-audience}

This tutorial is intended for system administrators who want to learn how to create an virtual server for classic infrastructure with `DEBIAN_8_64` or `CENTOS_7_64` Operating System by using {{site.data.keyword.cloud_notm}} Provider.

## Configure the resource file
{: #classic-tutorial-resource}
{: step}

1. Create a configuration file that is named `classic-vsi.tf` with the following content. Store this file in your folder or Git repository that you created earlier.
 
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

## Configure Terraform and provider version
{: #classic-tutorial-version}
{: step}

Create a configuration file that is named `versions.tf` with the following content. Store this file in your folder or Git repository that you created earlier.
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

## Execute Terraform init
{: #classic-tutorial-init}
{: step}

Run the Terraform initialization command and observe the successful execution. 

```sh
 terraform init
```
{: pre}

## Generate Terrafom plan
{: #classic-tutorial-plan}
{: step}

Generate an Terraform on IBM Cloud execution plan. When you execute this command, Terraform on IBM Cloud validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in. 
  
```sh
 terraform plan
```
{: pre}

Review the execution plan to verify the type of resource that is planned to be provisioned by Terraform on IBM Cloud.

## Generate Terrafom apply
{: #classic-tutorial-apply}
{: step}

Create your classic infrastructure virtual server. Confirm the creation by entering `yes` when prompted. 

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

## Running Terrafom show
{: #classic-tutorial-show}
{: step}

List the classic infrastructure virtual server that is provisioned. 
   
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

Optional: Review your classic virtual server instance in the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/classic/devices) is created.

## Executing Terrafom destroy
{: #classic-tutorial-destroy}
{: step}

Optional: Remove your classic infrastructure virtual server.

```sh
 terraform destroy
```
{: pre}

**What's next?**

- Explore [Classic infrastrucutre services](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-template#classic-infra-templates) related templates that you can provision by using Terraform on IBM Cloud.

- Explore [{{site.data.keyword.cloud_notm}} VPC resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc){: external} that you can provision by using Terraform on IBM Cloud.
