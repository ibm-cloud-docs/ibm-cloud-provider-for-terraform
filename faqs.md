---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-16"

keywords: terraform faqs, softlayer, iaas

subcollection: ibm-cloud-provider-for-terraform

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}


# FAQs
{: #faqs}

## How do I find the flavor and parameters to configure a virtual service instance in {{site.data.keyword.Bluemix_notm}}? 
{: #vsi_config}
{: faq}

The Terraform on IBM Cloud `ibm_compute_vm_instance` resource includes optional and mandatory configuration parameters. To find an overview of how you can configure your virtual server, use the {{site.data.keyword.Bluemix_notm}} CLI.  

1. Install the [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli). 

2. List supported configuration options for virtual servers in {{site.data.keyword.Bluemix_notm}}. The listed options include available data centers, machine flavors, CPU, memory, operating systems, local disk and SAN disk sizes, and network interface controllers (NIC). {{site.data.keyword.Bluemix_notm}} offers multiple virtual server offerings that each come with a specific configuration. The configuration of an offering is optimized for a specific workload need, such as high performance, or real-time analytics. For more information, see [Public Virtual Servers](/docs/virtual-servers?topic=virtual-servers-about-public-virtual-servers). 
    ```sh
    ibmcloud sl vs options
    ```
    {: pre}

## How long does it take for my resources to provision and delete?
{: #provisioning_times}
{: faq}

Most {{site.data.keyword.Bluemix_notm}} platform resources provision within a few seconds. Infrastructure resources, including Bare Metal servers, virtual servers, and {{site.data.keyword.Bluemix_notm}} Load Balancers can take longer. When you run the `terraform apply` or `terraform destroy` command, the command might take a few minutes to complete and you are not able to enter a different command during that time. The `terraform apply` command returns when your resources are fully provisioned, whereas the `terraform destroy` command might return before your resources are deleted from your {{site.data.keyword.Bluemix_notm}} platform or infrastructure portfolio. 

Use the `terraform apply` and `terraform destroy` times in the following table as a reference for when you can expect your commands to complete. 

If the Terraform on IBM Cloud operation does not complete due to a timeout, wait for the resource state change to complete and retry the operation. 
{: tip}

| Resource | terraform apply return time | terraform destroy return time |
| --- | --- | --- |
| {{site.data.keyword.Bluemix_notm}} platform resources | A few seconds | A few seconds |
| Virtual servers | A few seconds | A few seconds |
| {{site.data.keyword.Bluemix_notm}} Load Balancers |  A few seconds | Up to 30 minutes |
| Bare Metal servers | Up to a few hours | Up to a few hours |
{: caption="Overview of Terraform apply and destroy command completion times" caption-side="top"}

## How do I set up Terraform on IBM Cloud greater than v0.13.0 ?
{: #ibm-terraform-provider-v13}
{: faq}

For detailed steps, see how to [install the Terraform on IBM Cloud](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#tf_installation) and [install the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider).

## How can I resolve the error when provisioning a `ibm_container_alb_cert` resource with secret?
{: #provision-ibm-container-alb-cert}
{: faq}

    ```text
    stderr :
    Error: Error waiting for create resource alb cert (buvlsclf0qcur3hjcrng/ingress-tls-cert) : The resource alb cert buvlsclf0qcur3hjcrng/ingress-tls-cert does not exist anymore: Request failed with status code: 404, ServerErrorResponse: {"incidentID":"5f82fa1696ce299a-IAD","code":"E0024","description":"The specified Ingress secret name is not found for this cluster.","type":"ALBSecret","recoveryCLI":"To list the Ingress secrets for a cluster, run 'ibmcloud ks ingress secret ls -c \u003ccluster_name_or_ID\u003e'."}
    ```

You need to update the {{site.data.keyword.cloud_notm}} provider version to `version 1.16.1` or above to support [create secret](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_alb_cert){: external} feature in `ibm_container_alb_cert`. 

## How can I set or add multiple address prefixes to the configuration file when provisioning VPC?
{: #addressprefix}
{: faq}
{: support}

The `address_prefix_management` argument indicates a default address prefix should be created automatically or manually for each zone in the VPC. Supported values are **auto** and **manual**. The default value is **auto**. Most scenario covers default address prefixes set as optional without specifying during the creation of VPC through Terraform. 

If you require one or more address prefixes you should define as part of resource provisioning in the configuration file. To configure multiple address prefix with arguments define the code as stated in the code block. For more information, see [ibm_is_vpc_address_prefix data source](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_address_prefixes#attribute-reference){: external}.


    ```terraform
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

A access group policy is a way to organize your account having create, modify, or delete an IAM access groups, where user can grant permissions to members with appropriate privileges such as **Manager**, **Viewer** and **Administrator**. For more information, about [ibm_access_group_policy resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_access_group_policy){: external} and [iam_service_policy resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_policy){: external}. 

    ```terraform
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

The sample code block helps to configure the policy for all services in all resource group. But you have to enter all the roles in the list. 

    ```terraform
    resource "ibm_iam_user_policy" "policy" {
      ibm_id = "test@in.ibm.com"
      roles  = ["Viewer"]
    }
    ```
    {: codeblock}
    

## How can I configure a target resource to connect from different regions?
{: #target-regions-faq}
{: faq}
{: support}

You need to configure the different regions in the provider block by using `region` parameter, as shown in the code block.

    ```terraform
    // First code block
    provider "ibm" {
        ibmcloud_api_key   = xxxxxx
        region             = "eu-de"
    }
    ```
    {: codeblock}

    ```terraform
    // Second code block
    data "ibm_is_vpc" "vpc1" {
      name            = "aa-kubecf-a"
    }
    ```
    {: codeblock}


## How can I connect and retrieve information from multiple region at once in the same template?
{: #alias-parameter-faq}
{: faq}
{: support}

You can connect and retrieve information from a multiple regions by using `aliases` parameter as shown in the example code block. For more information, about configuring multiple provider block, see [Multiple provider configurations](https://www.terraform.io/language/providers/configuration#alias-multiple-provider-configurations).


    ```terraform
    provider "ibm" {
      ibmcloud_api_key = "${var.ibmcloud_api_key}"
      generation = 2
      region = "eu-de"
    }
    ```
    {: codeblock}

    ```terraform
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

You can configure only one region for a resource list to a group policy, as shown in the code block. For more information, about configuring resource block, see [Multiple provider configurations](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_policy#user-policy-using-service-with-region).

    ```terraform
    resource "ibm_iam_user_policy"  "policy" { 
    ibm_id = "test@in.ibm.com" 
    roles = ["Viewer"] 
    resources { 
      service = "kms" 
    } 
    } 
    ```
    {: codeblock}
    

## How can I create access group policies and add memo as an attribute to the policy?
{: #alias-attributes-gpolicy}
{: faq}
{: support}

Here is a code block that helps you to create access group policies and add memo as an attribute to the policy.

    ```terraform
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

## How do I create the Terraform resources of the same type in sequential order?
{: #alias-squential-terrreso}
{: faq}
{: support}

The sample code block helps to create the resources of the same type in a sequential order.

    ```terraform
    resource "ibm_is_vpc" "res_a" {
      name = "test1"
    }
    resource "ibm_is_vpc" "res_b" {
      name = "test2"
      depends_on = [ibm_is_vpc.res_a]
    }
    ```
    {: codeblock}

## How do I enable the User list visibility for the IAM in Terraform?
{: #alias-userlistvisibility-iam}
{: faq}
{: support}

Currently, {{site.data.keyword.bpshort}} do not support enabling `user list visibility`. For more information, about user list visibility, see [ibm_iam_account_settings](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings){: external}.

## Can I configure the `ibm_container_cluster` Terraform resource to control the IPs on the {{site.data.keyword.cos_full_notm}} bucket?
{: #alias-ibmcontainerclus-terraform}
{: faq}
{: support}

No, currently, the API does not support IPs on the {{site.data.keyword.cos_full_notm}} bucket. For more information, about the argument and attribute reference for the container cluster, see [ibm_container_cluster](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster){: external}.

## Can I retrieve a list of all the existing {{site.data.keyword.vsi_is_short}}s from all the regions by using Terraform?
{: #alias-retrievelist-terraform}
{: faq}
{: support}

Yes, but the VPC API’s are region specific so `ibm_is_vpcs` gives only one region VPC. If user requires one or more regions, you should define or use the `alias` during the resource provisioning, as shown in the code block.

    ```terraform
    provider "ibm" {
      region = "eu-de"
    }

    provider "ibm" {
      alias  = "dal"
      region = "us-south"
    }

    data ibm_is_vpcs eu-de{
    }
    data ibm_is_vpcs dal {
      provider = ibm.dal
    }

    output "vpcs" {
      value = concat(
        tolist(data.ibm_is_vpcs.eu-de.vpcs), 
        tolist(data.ibm_is_vpcs.dal.vpcs)
        )
    } 

    ```
    {: codeblock}
    

## How can I edit the flavor of an existing IKS worker pool without deleting or destroying an existing one by updating its machine_type?
{: #alias-flavoriks-machinetype}
{: faq}
{: support}

Updating the machine type in the Terraform file allows to built or provision new set of resource creating an entirely new worker pool. You can use the sample code block to update.

    ```terraform
    resource "ibm_container_cluster" "iks_cluster" {
        name                      = var.cluster_name
        datacenter                = var.datacenter
        machine_type              = var.machine_type
        hardware                  = var.hardware
        public_vlan_id            = var.public_vlan_id
        private_vlan_id           = var.private_vlan_id
        disk_encryption           = "true"

        kube_version              = var.kube_version

        default_pool_size         = var.pool_size

        public_service_endpoint   = "true"
        private_service_endpoint  = "true"
        update_all_workers        = var.update_all_workers
        wait_for_worker_update    = "true"

        resource_group_id         = var.resource_group.id
    } 

    ```
    {: codeblock}
    

## How can I secure a workspace by setting an environment variable?
{: #alias-squential-envvariable}
{: faq}
{: support}

Currently, the {{site.data.keyword.bplong_notm}} service team is working to enable secure environment variables and support for passing credentials for modules. It is planned in the future roadmap. However, here is a sample code block to secure a workspace.

    ```text
    Example input file get workspace:
      "env_values": [{
          "name": "GIT_ASKPASS",
          "value": "./git-askpass-helper.sh",
          "secure": false,
          "hidden": false
        },
        {
          "name": "GIT_PASSWORD",
          "value": "plain text token",
          "secure": false,
          "hidden": false
        }
      ]
    ```
    

## How can I create `ibm_function_trigger` with Terraform that connects to an Event Stream?
{: #alias-functional-trigger}
{: faq}
{: support}

The sample code block allows to create the resources of the same type in a sequential order. For more information, about creating a trigger that listens to an Event Streams instance block, see [Event Streams_trigger](/docs/openwhisk?topic=openwhisk-pkg_event_streams#eventstreams_trigger).

    ```terraform
    resource "ibm_function_trigger" "trigger" {
      name = "event - trigger"
      namespace = "ns01"
      user_defined_annotations = jsonencode([])
      user_defined_parameters = jsonencode([])
      feed {
        name = "/whisk.system/messaging / messageHubFeed"
        parameters = jsonencode([])
      }
    }
    ```
    {: codeblock}

## How do I associate a public gateway while creating multiple zones with a Subnet for each zone?
{: #alias-multiplezone-subnet}
{: faq}
{: support}


    ```text
    {
      
      "StatusCode": 400,
      "Headers": {
        
        "Cache-Control": ["max-age=0, no-cache, no-store, must-revalidate"],
        "Cf-Cache-Status": ["DYNAMIC"],
        "Cf-Ray": ["6ab6a5e86ac41b69-DEL"],
        "Connection": ["keep-alive"],
        "Content-Length": ["261"],
        "Content-Type": ["application/json; charset=utf-8"],
        "Date": ["Tue, 09 Nov 2021 11:19:47 GMT"],
        "Expect-Ct": ["max-age=604800, report-uri=\"https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct\""],
        "Expires": ["-1"],
        "Pragma": ["no-cache"],
        "Server": ["cloudflare"],
        "Strict-Transport-Security": ["max-age=31536000; includeSubDomains"],
        "Vary": ["Accept-Encoding"],
        "X-Content-Type-Options": ["nosniff"],
        "X-Request-Id": ["37b94c40-a4bf-4942-a0da-45dc5434d610"],
        "X-Xss-Protection": ["1; mode=block"]
      },
      "Result": {
        
        "errors": [{
          
          "code": "bad_field",
          "message": "Failed to attach public gateway of different zone to the subnet",
          "target": {
            
            "name": "public_gateway.id",
            "type": "field",
            "value": "r010-2df568da-f87e-468d-9696-27b05e126179"
          }
        }],
        "trace": "37b94c40-a4bf-4942-a0da-45dc5434d610"
      },
      "RawResult": null
    }
    ```

The Zones can have multiple subnets, but you need at least one subnet per zone for IP distribution. One subnet can be part of only one zone. Public gateway can be attached to one or more subnets (of the same zone). Each zone has only one public gateway.

## How can I resolve the unexpected HTTP status code 502 (502 Bad Gateway) null error when deploying an instance of IBM Cloud Database RabbitMQ by using Terraform?
{: #deploy-icdrabbitmq-faq}
{: faq}
{: support}

The sample Terraform configuration with the default memory and disk allocation size for RabbitMQ resource

```terraform
resource "ibm_database" "messages-for-rabbitmq" {
  name              = "rabbitmq"
  plan              = "standard"
  location          = "eu-de"
  service           = "messages-for-rabbitmq"
  resource_group_id = data.ibm_resource_group.resource_group.id
  adminpassword                = "password12"
  members_memory_allocation_mb = 2048
  members_disk_allocation_mb   = 1024
  
  service_endpoints = var.service_endpoints
}
```
{: codeblock}

You have to update the memory and disk allocation size in the Terraform configuration file as shown in the code block.

```terraform
members_memory_allocation_mb = 3072
members_disk_allocation_mb   = 3072
```
{: codeblock}

For more information, about configuring the memory and disk allocation for the database, see [{{site.data.keyword.cloud_notm}} Database instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database).

## How can I resolve cross-origin resource sharing (CORS) configuration issue while creating a cloudant instance?
{: #cos-instance-faq}
{: faq}
{: support}

You need to own `manager` role for configuring cross-origin resource sharing (CORS) configuration to successfully apply the plan. You can only create an {{site.data.keyword.cloudant_short_notm}} instance with the `writer` role. For more information, about {{site.data.keyword.cloudant_short_notm}} instance access, see [roles](/docs/Cloudant?topic=Cloudant-work-with-your-account#roles).

For example, to get the `resource-controller.instance.create` action you need Cloudant **Platform** editor or Administrator role. To configure the Cloudant instance feature such as `cloudantnosqldb.sapi.usercors` action you need the cloudant service manager role. For more information, about {{site.data.keyword.cloud_notm}} cloudant, see [ibm_cloudant](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cloudant) resource.

## Can I increase or decrease timeouts while deleting Terraform resource?
{: #timeouts-resource-faq}
{: faq}
{: support}

Yes, you can increase or decrease timeouts by using timeouts blocks within your resource block as shown in the example. For more information, about a resource having timeouts block, see [ibm_container_vpc_cluster](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_vpc_cluster#timeouts) timeouts.

```terraform
timeouts {
    create = "3h"
    update = "2h"
    delete = "1h"
  }

resource "ibm_container_cluster" "mycluster" {
  ...
  timeouts {
    delete = "60m" # something higher than the default of 45m
  }
}
```
{: codeblock}
