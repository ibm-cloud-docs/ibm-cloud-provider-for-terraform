---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-26"

keywords: terraform faqs, softlayer, iaas

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}



# FAQs
{: #faqs}

## How do I find the flavor and parameters to configure a virtual service instance in {{site.data.keyword.Bluemix_notm}}? 
{: #vsi_config}
{: faq}

The Terraform on {{site.data.keyword.cloud_notm}} `ibm_compute_vm_instance` resource includes optional and mandatory configuration parameters. To find an overview of how you can configure your virtual server, use the {{site.data.keyword.Bluemix_notm}} CLI.  

1. Install the [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli). 

2. List supported configuration options for virtual servers in {{site.data.keyword.Bluemix_notm}}. The listed options include available data centers, machine flavors, cpu, memory, operating systems, local disk and SAN disk sizes, and network interface controllers (nic). {{site.data.keyword.Bluemix_notm}} offers multiple virtual server offerings that each come with a specific configuration. The configuration of an offering is optimized for a specific workload need, such as high performance, or real-time analytics. For more information, see [Public Virtual Servers](/docs/virtual-servers?topic=virtual-servers-about-public-virtual-servers). 
    ```
    ibmcloud sl vs options
    ```
    {: pre}


## How long does it take for my resources to provision and delete?
{: #provisioning_times}
{: faq}

Most {{site.data.keyword.Bluemix_notm}} platform resources provision within a few seconds. Infrastructure resources, including Bare Metal servers, virtual servers, and {{site.data.keyword.Bluemix_notm}} Load Balancers can take longer. When you run the `terraform apply` or `terraform destroy` command, the command might take a few minutes to complete and you are not able to enter a different command during that time. The `terraform apply` command returns when your resources are fully provisioned, whereas the `terraform destroy` command might return before your resources are deleted from your {{site.data.keyword.Bluemix_notm}} platform or infrastructure portfolio. 

Use the `terraform apply` and `terraform destroy` times in the following table as a reference for when you can expect your commands to complete. 

If the Terraform on {{site.data.keyword.cloud_notm}} operation does not complete due to a timeout, wait for the resource state change to complete and retry the operation. 
{: tip}

<table>
<caption>Overview of `terraform apply` and `terraform destroy` command completion times</caption>
<thead>
<th>Resource</th>
<th><code>terraform apply</code> return time</th>
<th><code>terraform destroy</code> return time</th>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} platform resources</td>
<td>A few seconds</td>
<td>A few seconds</td>
</tr>
<tr>
<td>Virtual servers</td>
<td>A few minutes</td>
<td>A few seconds</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Load Balancers</td>
<td>A few minutes</td>
<td>Up to 30 minutes</td>
</tr>
<tr>
<td>Bare Metal servers</td>
<td>Up to a few hours</td>
<td>Up to a few hours</td>
</tr>
</tbody>
</table>

## How do I set up Terraform on {{site.data.keyword.cloud_notm}} greater than v0.13.0 ?
{: #ibm-terraform-provider-v13}
{: faq}

For detailed steps, see how to [install the Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#tf_installation) and [install the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider).

## Why I am getting an issue when trying to provision an `ibm_container_alb_cert`?
{: #provision-ibm-container-alb-cert}
{: faq}

If you are using the resource `ibm_container_alb_cert` to create a secret and fails with a following error

**Error**

```
stderr : 
Error: Error waiting for create resource alb cert (buvlsclf0qcur3hjcrng/ingress-tls-cert) : The resource alb cert buvlsclf0qcur3hjcrng/ingress-tls-cert does not exist anymore: Request failed with status code: 404, ServerErrorResponse: {"incidentID":"5f82fa1696ce299a-IAD","code":"E0024","description":"The specified Ingress secret name is not found for this cluster.","type":"ALBSecret","recoveryCLI":"To list the Ingress secrets for a cluster, run 'ibmcloud ks ingress secret ls -c \u003ccluster_name_or_ID\u003e'."}
```
{: screen}

**Solution**

You need to update the Terraform on {{site.data.keyword.cloud_notm}} provider to use `version 1.16.1` and above.

## How do you set or add multiple address prefixes to the configuration file when provisioning VPC?
{: #addressprefix}
{: faq}
{: support}

The `address_prefix_management` argument indicates a default address prefix should be created automatically or manually for each zone in the VPC. Supported values are **auto** and **manual**. The default value is **auto**.

Most scenario covers default address prefixes set as optional without specifying during the creation of VPC through Terraform. 

**Solution**

If user requires one or more address prefixes you should define as part of resource provisioning in the configuration file. To configure multiple address prefix with arguments define the code as stated in the example. For more information, see [ibm_is_vpc_address_prefix data source](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_address_prefixes#attribute-reference){: external}.

**Example**

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "testvpc"
}

resource "ibm_is_vpc_address_prefix" "testacc_vpc_address_prefix" {
  name = "test"
  zone = "us-south-1"
  vpc  = ibm_is_vpc.testacc_vpc.id
  cidr = "10.240.0.0/24"
}

resource "ibm_is_vpc_address_prefix" "testacc_vpc_address_prefix2" {
  name = "test2"
  zone = "us-south-1"
  vpc  = ibm_is_vpc.testacc_vpc.id
  cidr = "10.240.0.0/24"
}
```
{: codeblock}

## How do I define a policy which has all resource groups?
{: #policy-faq}
{: faq}
{: support}

**Solution**

A access group policy is a way to organize your account having create, modify, or delete an IAM access groups, where user can grant permissions to members with appropriate privileges such as **Manager**, **Viewer** and **Administrator**. For more information, about [ibm_access_group_policy resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_access_group_policy) and [iam_service_policy resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_policy). 

**Sample code**

```
resource "ibm_iam_access_group" "accgrp" {
  name = "rg"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles           = ["Manager", "Viewer", "Administrator"]
]

  resources {
    resource_type = "resource-group"
  }
}
```
{: codeblock}

## How do I configure policy for all services in all the resource groups for an user?
{: #user-policy-faq}
{: faq}
{: support}

**Solution**

View the sample code to configure the policy for all services in all resource group. But you have to enter all the roles in the list. 

**Sample code**

```
resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@in.ibm.com"
  roles  = ["Viewer"]
}
```
{: codeblock}


## How to configure a target resource to connect from different regions?
{: #target-regions-faq}
{: faq}
{: support}

You need to configure the different regions in the provider block by using `region` parameter, as shown in the example.

**Example**

```
// First code block
provider "ibm" {
    ibmcloud_api_key   = xxxxxx
    region             = "eu-de"
}
```

```
// Second code block
data "ibm_is_vpc" "vpc1" {
  name            = "aa-kubecf-a"
}
```


## How can a user connect and retrieve information from multiple region at once in the same template?
{: #alias-parameter-faq}
{: faq}
{: support}

**Solution**

You can connect and retrieve information from a multiple regions by using `aliases` parameter as shown in the example code block. For more information, about configuring multiple provider block, see [Multiple provider configurations](https://www.terraform.io/docs/language/providers/configuration.html#alias-multiple-provider-configurations).

**Example**

```
provider "ibm" {
  ibmcloud_api_key = "${var.ibmcloud_api_key}"
  generation = 2
  region = "eu-de"
}
```
{: codeblock}

**Example to configure an `aliases` to connect and retrieve information from multiple regions**

```
provider "ibm" {
  ibmcloud_api_key = "${var.ibmcloud_api_key}"
  region = "eu-de"
}

provider "ibm" {
  ibmcloud_api_key = "${var.ibmcloud_api_key}"
  alias  = "eu-gb-alias"
  region = "eu-gb"
}
```
{: codeblock}

## How do I assign multiple resources to a group policy?
{: #alias-resource-gpolicy}
{: faq}
{: support}

**Solution**

You can configure only one region for a resource list to a group policy, as shown in the example. For more information, about configuring resource block, see [Multiple provider configurations](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_policy#user-policy-using-service-with-region).

**Example**

```
resource "ibm_iam_user_policy"  "policy" { 
 ibm_id = "test@in.ibm.com" 
 roles = ["Viewer"] 
 resources { 
  service = "kms" 
 } 
} 
```
{: codeblock}

## How can a user create access group polices and add memo as an attribute to the policy?
{: #alias-attributes-gpolicy}
{: faq}
{: support}

**Solution**

You can create access group policies and add memo as an attribute to the policy as shown in the example code block.

**Example**

```
resource "ibm_iam_access_group_policy" "policy" {
	access_group_id = ibm_iam_access_group.grp.id
	roles = ["Viewer"]
	resources {
		resource_type = "resource-group"
		resource = "resource-id"
	}
}

or

data "ibm_resource_group" "group" {
	name = "default"
}
resource "ibm_iam_access_group_policy" "policy" {
	access_group_id = ibm_iam_access_group.accgrp.id
	roles = ["Viewer"]
	resources {
		resource_type = "resource-group"
		resource = data.ibm_resource_group.group.id
	}
}
```
{: codeblock}

## How do I create the resources of the same type in sequential order during the Terraform resource creation?
{: #alias-squential-terrreso}
{: faq}
{: support}

**Solution**

The sample code block helps to create the resources of the same type in a sequential order.

**Sample**

```
resource "ibm_is_vpc" "res_a" {
  name = "test1"
}
resource "ibm_is_vpc" "res_b" {
  name = "test2"
  depends_on = [ibm_is_vpc.res_a]
}
```
{: codeblock}