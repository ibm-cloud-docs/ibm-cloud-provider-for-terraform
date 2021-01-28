---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider plugin, terraform transit gateway resource, terraform transit gateway, transit gateway resource, transit gateway

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



# Transit Gateway resources
{: #tg-resource}

The {{site.data.keyword.cloud_notm}} [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started) provides to create,  manage gateways and connections and list available locations for gateways. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}.

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
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

