---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-22"

keywords: terraform provider plugin, terraform transit gateway resource, terraform transit gateway, transit gateway resource, transit gateway

subcollection: ibm-cloud-provider-for-terraform

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:step: data-tutorial-type='step'}


# Transit Gateway resources
{: #tg-resource}

The {{site.data.keyword.cloud_notm}} [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started) provides to create,  manage gateways and connections and list available locations for gateways. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}.

Before you start working with your resource, make sure to review the [required parameters](/docs/terraform?topic=terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_tg_connection`
{: #tg-connection}

Create, update and delete for the transit gateway's connection resource. 
{: shortdesc}

### Sample Terraform code
{: #tg-connection-sample}

The following example shows how to create, update and delete a transit gateway connection by using a transit gateway resource.

```
resource "ibm_tg_connection" "test_ibm_tg_connection"{
  gateway = ibm_tg_gateway.test_tg_gateway.id
  network_type = "vpc"
  name= "myconnection"
  network_id = ibm_is_vpc.test_tg_vpc.resource_crn
}

```
{: codeblock}

### Input parameters
{: #tg-connection-rinput}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `gateway` | String | Required | Enter the transit gateway identifier. | Yes |
| `name` | String| Optional | Enter a name. If unentered, the default name is provided based on the network type, such as `vpc` for network type VPC and `classic` for network type classic. | No|
| `network_account_id` | String | Optional | The ID of the network connected account. This is used if the network is in a different account than the gateway. | Yes |
| `network_type` | String | Required | Enter the network type. Allowed values are `classic` and `vpc`. | Yes |
| `network_id` |  String | Optional | Enter the ID of the network being connected through this connection. This parameter is required for network type `vpc`, the CRN of the VPC to be connected. This field is required to be unspecified for network type `classic`. For example, `crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b` | Yes |

### Output parameters
{: #tg-connection-r-output}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the gateway ID or connection ID resource.|
| `connection_id` | String | The unique identifier for transit gateway connection to network. |
| `created_at` | String |The date and time the connection was created. | 
| `updated_at` | String | Last updated date and time of the connection. |
| `status` | String | The configuration status of the connection, such as **attached**, **failed**, **pending**, **deleting**. |

The resource do not wait for the available status, if you are provisioning the cross account gateway or connection. You need to complete the manual approval process for provisioning.
{: note}

### Import
{: #connection-r-import}

`ibm_tg_connection` can be imported by using transit gateway ID and connection ID.

**Example**
```
terraform import ibm_tg_connection.example 5ffda12064634723b079acdb018ef308/cea6651a-bd0a-4438-9f8a-a0770bbf3ebb
```
{: pre}

## `ibm_tg_gateway`
{: #tg-gateway-resource}

Create, update and delete for the transit gateway resource. 
{: shortdesc}

### Sample Terraform code
{: #tg-gatewy-sample}

The following example shows how to create, update and delete a transit gateway by using a transit gateway resource.

```
resource "ibm_tg_gateway" "new_tg_gw"{
  name="transit-gateway-1"
  location="us-south"
  global=true
  resource_group="30951d2dff914dafb26455a88c0c0092"
}

```
{: codeblock}

### Input parameters
{: #tg-gateway-r-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `name` | String | Required | The unique user-defined name for the gateway. For example, `myGateway` | No |
| `location` | Integer| Optional | The location of the transit gateway. For example, `us-south` | Yes |
| `global` | Boolean | Required | The gateways with global routing (true) to connect to the networks outside their associated region. | No |
| `resource_group` |  String | Optional | The resource group ID where the transit gateway to be created. | Yes |

### Output parameters
{: #tg-gateway-r-output}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the gateway ID or connection ID resource.|
| `crn` | String | The CRN of the gateway.|
| `created_at` | String | The date and time the connection is created. | 
| `updated_at` | String | The date and time the connection is last updated. |
| `status` | String | The configuration status of the connection, such as **Available**, **pending**. |

### Import
{: #gateway-import}

`ibm_tg_gateway` can be imported by using transit gateway ID and connection ID.

**Example**
```
terraform import ibm_tg_gateway.example 5ffda12064634723b079acdb018ef308
```
{: pre}

