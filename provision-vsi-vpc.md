---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-07"

keywords: terraform quickstart, terraform getting started, terraform tutorial, virtual server for vpc

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services:  terraform, vpc
account-plan: lite
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}


# Provisioning an {{site.data.keyword.cloud_notm}} virtual server for VPC
{: #sample_vpc_config}
{: toc-content-type="tutorial"}
{: toc-services="terraform, vpc"}
{: toc-completion-time="2h"}

Use {{site.data.keyword.cloud_notm}} Provider plug-in to provision a VPC, and set up networking for your VPC, and provision a virtual server for VPC in your {{site.data.keyword.cloud_notm}} account. A VPC allows you to create your own space in {{site.data.keyword.cloud_notm}} so that you can run an isolated environment in the public cloud with custom network policies.
{: shortdesc}

## Objectives
{: #vpc-tutorial-objective}

In this tutorial, you will learn to provisions:

- 1 VPC where you provision your VPC virtual server instance
- 1 security group and a rule for this security group to allow SSH connection to your virtual server instance
- 1 subnet to enable networking in your VPC
- 1 VPC virtual server instance
- 1 floating IP address that you use to access your VPC virtual server instance over the public network

Keep in mind that a VPC virtual server instance is an {{site.data.keyword.cloud_notm}} VPC infrastructure resource that incurs costs. Be sure to review the [available plans](https://cloud.ibm.com/vpc/provision/vs) before you proceed.
{: important}

## Audience
{: #vpc-tutorial-audience}

This tutorial is intended for system administrators who want to learn how to provision an {{site.data.keyword.cloud_notm}} virtual server for a VPC by using {{site.data.keyword.cloud_notm}} Provider.
{: shortdesc}

## Prerequisites
{: #vpc-tutorial-prereq}

- Install the [latest Terraform on IBM Cloud](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#tf_installation) and the latest [{{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on IBM Cloud](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider).
- Retrieve your {{site.data.keyword.cloud_notm}} credentials, [upload an SSH key](/docs/ssh-keys?topic=ssh-keys-about-ssh-keys), and [configure the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference).

## Create the Terraform configuration files
{: #vpc-tutorial-create}
{: step}

1. Make sure that you have the [required permissions](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources) to create and work with VPC infrastructure.

2. In the Terraform directory, create a configuration file names `versions.tf` file as specified in the code block. For more information, about `versions.tf`, refer to [sample Terraform version file](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#tf_installation_step).

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
    {: codeblock}

3. From your Terraform directory, export `IC_API_KEY` variable to set environment variable in your local machine. For more information, about how to setup the environment variables? see [Using environment variable](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#env-vars).

    Example

    `export IC_API_KEY="<provide your IBM Cloud API Key>"`

4. In the Terraform directory, create a Terraform configuration file and name it `vpc.tf`. The configuration file includes the following definition blocks:

    ```terraform
    variable "ssh_key" {
    }

    locals {
        BASENAME = "vpctestexample"
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

    resource "ibm_is_floating_ip" "fip1" {
        name   = "${local.BASENAME}-fip1"
        target = ibm_is_instance.vsi1.primary_network_interface[0].id
        }

        output "sshcommand" {
        value = "ssh root@${ibm_is_floating_ip.fip1.address}"
        }
     }
    ```
    {: codeblock}

    For more information, about the description of the resource argument, refer to [registry documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external}. The table specifies the registry link of each resources and data sources.

    | Resource name | Registry documentation link |
    | --- | --- |
    | `ibm_is_vpc` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc#argument-reference) |
    | `ibm_is_security_group` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_security_group#argument-reference) |
    | `ibm_is_security_group_rule` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_security_group_rule#argument-reference) |
    | `ibm_is_instance` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference) |
    | `ibm_is_floating_ip` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_floating_ip#argument-reference) |
    | `ibm_is_subnet` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_subnet#argument-reference) |
    {: caption="Registry link of the resources" caption-side="top"}

    | Data Sources name | Registry documentation link |
    | --- | --- |
    | `ibm_is_ssh_key` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_ssh_key#argument-reference) |
    | `ibm_is_image` | [Docs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_image#argument-reference) |
    {: caption="Registry link of the data sources" caption-side="top"}

## Initializing Terraform
{: #vpc-tutorial-init}
{: step}

Run the Terraform initialization command and observe the successful execution.

```sh
terraform init
```
{: pre}

Example output

```text
2021/06/22 16:47:27 [WARN] Log levels other than TRACE are currently unreliable, and are supported only for backward compatibility.
Use TF_LOG=TRACE to see Terraform's internal logs.
----
2021/06/22 16:47:27 [INFO] Terraform version: 0.13.5
2021/06/22 16:47:27 [INFO] Go runtime version: go1.14.7
terraform/plugins/darwin_amd64/lock.json: no such file or directory

Initializing provider plugins...
- Using previously-installed ibm-cloud/ibm v1.26.2

Terraform has been successfully initialized!
...
If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```
{: screen}

## Generating Terraform plan
{: #vpc-tutorial-plan}
{: step}

Generate an Terraform on IBM Cloud execution plan. When you execute this command, Terraform on IBM Cloud validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in.

Your SSH key name need to be provide during `terraform plan` and `terraform apply` execution.
{: note}

```sh
terraform plan
```
{: pre}

Example output

```text
var.ssh_key
    Enter a value: <Provide your SSH key name>
2021/06/22 16:48:53 [INFO] backend/local: plan operation completed

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
    + create

Terraform will perform the following actions:

    ibm_is_floating_ip.fip1 will be created
    + resource "ibm_is_floating_ip" "fip1" {
        ...
    }

    ibm_is_instance.vsi1 will be created
    + resource "ibm_is_instance" "vsi1" {
        ...
        }
    }

    ibm_is_security_group.sg1 will be created
    + resource "ibm_is_security_group" "sg1" {
        ...
    }

    ibm_is_security_group_rule.ingress_ssh_all will be created
    + resource "ibm_is_security_group_rule" "ingress_ssh_all" {
        ...
    }

    ibm_is_subnet.subnet1 will be created
    + resource "ibm_is_subnet" "subnet1" {
        ...
    }

    ibm_is_vpc.vpc will be created
    + resource "ibm_is_vpc" "vpc" {
        ...
    }

Plan: 6 to add, 0 to change, 0 to destroy.

------------------------------------------------------------------------

You didn't specify an "-out" parameter to save this plan, so Terraform
can't guarantee that exactly these actions will be performed if
"terraform apply" is subsequently run.
```
{: screen}

## Executing Terraform apply
{: #vpc-tutorial-apply}
{: step}

Create the VPC infrastructure resources. Confirm the creation by entering `yes` when prompted.

```sh
terraform apply
```
{: pre}

Observe the [`terraform.tfstate`](https://developer.hashicorp.com/terraform/language/state/purpose){: external} file that is created in your directory. Terraform state file maps your resources to your configuration and keep track of the metadata. Also improves performance for the large infrastructures.

Example output

```text
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
    + create

Terraform will perform the following actions:

ibm_is_floating_ip.fip1 will be created
+ resource "ibm_is_floating_ip" "fip1" {
    ...
}

ibm_is_instance.vsi1 will be created
+ resource "ibm_is_instance" "vsi1" {
    ...
    }
}

ibm_is_vpc.vpc will be created
+ resource "ibm_is_vpc" "vpc" {
    + address_prefix_management   = "auto"
...
}

Apply complete! Resources: 6 added, 0 changed, 0 destroyed.

Outputs:

sshcommand = ssh root@ibm_is_floating_ip.fip1.address
```
{: screen}

## Analyzing the provisioned resource
{: #vpc-tutorial-analyze}
{: step}

1. Log in to your VPC VSI by using the `ssh` command that is listed at the end of your command-line output of the previous step.

    ```sh
    ssh root@52.118.150.55
    ```
    {: pre}

    Example output

    ```text
    The authenticity of host '52.116.134.139 (52.116.134.139)' can't be established.
    ECDSA key fingerprint is SHA256:ZZRZY07mx3ccmnS5+Tip7eDDVSL7jlunPbANcrCeEYE.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added '52.116.134.139' (ECDSA) to the list of known hosts.

    -bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
    [root@vpctestexample-vsi1 ~]#
    ```
    {: screen}

2. You can verify that VPC and VSI are created by accessing your [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com).
    - Click **Navigation Menu** icon > **VPC Infrastructure** > **VPCs** to view VPC named `vpctestexample` is created
    - Click **Navigation Menu** icon > **VPC Infrastructure** > **Virtual server instances** to view VSI named `vsi1` is created

## Executing Terraform destroy
{: #vpc-tutorial-destroy}
{: step}

Optional: If you don't want to work with your VPC infrastructure resources anymore, remove them.

```sh
terraform destroy
```
{: pre}

## What's next?
{: #vpc-tutorial-whatsnext}

Explore other [{{site.data.keyword.cloud_notm}} resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/) that you can provision by using Terraform on IBM Cloud.
