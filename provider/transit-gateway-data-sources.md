---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-05"

keywords: terraform provider plugin, terraform transit gateway, terraform  transit gateways,  terraform transit gateway location, transit gateway locations, transit gateway, transit location

subcollection: terraform

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


# Transit Gateway data sources
{: #transit-gateway-ds}

The {{site.data.keyword.cloud_notm}} [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started) provides to create,  manage gateways and connections and list available locations for gateways. You can reference the output parameters for each resource in other resources or data sources by using [IBM Cloud Provider plug-in for Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}.

Before you start working with your data source, make sure to review the [required parameters](/docs/terraform?topic=terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your IBM Cloud Provider plug-in for Terraform configuration file. 
{: important}

## `ibm_tg_gateway`
{: #tg-gateway-ds}
 
Imports the information of an existing {{site.data.keyword.cloud_notm}} infrastructure transit gateway as a read only data source.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #tg-gateway-sample}

The following example shows the details of transit gateway data source. 
{: shortdesc}

```
resource "ibm_tg_gateway" "new_tg_gw"{
name="transit-gateway-1"
location="us-south"
global=true
resource_group="30951d2dff914dafb26455a88c0c0092"
} 

data "ibm_tg_gateway" "ds_tggateway" {
    name=ibm_tg_gateway.new_tg_gw.name
}
```

### Input parameters
{: #tg-gateway-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `name` | String | Required | The name of the gateway. |

### Output parameters
{: #tg-gateway-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `created_at` | String | The date and time resource is created.|
| `updated_at` | String | The date and time resource is last updated.|
| `crn` | String | The CRN of the gateway.|
| `global` | String | The gateways with global routing true to connect to the networks outside the associated region.|
| `location` | String | The gateway location.|
| `id` | String | The unique identifier of this gateway.|
| `status` | String | The gateway status.|
| `resource_group` | String | The resource group identifier.|
| `connections.name` | String | The user-defined name for the transit gateway connection.|
| `connections.network_type` | String | The type of network connected with the connection. Possible values are `classic` or `VPC`. |
| `connections.network_account_id` | String | The ID of the network connected account. This is used if the network is in a different account than the gateway. |
| `connections.network_id` | String | The ID of the network being connected with the connection. |
| `connections.id` | String | The unique identifier for the transit gateway connection to network either `VPC` or `classic`).|
| `connections.created_at` | String | The date and time the connection is created.|
| `connections.updated_at` | String | The date and time the connection is last updated.|
| `connections.status` | String | The current configuration state of the connection. Possible values are `attached`, `failed,` `pending`, `deleting`.|





## `ibm_tg_gateways`
{: #tg-gateways-ds}
 
Imports the information of an existing {{site.data.keyword.cloud_notm}} infrastructure transit gateway as a read only data source.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #tg-gateways-sample}

The following example shows the details of transit gateways data source. 
{: shortdesc}

```
data "ibm_tg_gateways" "ds_tggateways" {
}
```

### Input parameters
{: #tg-gateways-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

There is no input parameters for `ibm_tg_gateways`.

### Output parameters
{: #tg-gateways-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `transit_gateways` | String | List of all transit gateways.|
| `transit_gateways.created_at` | String | The date and time resource is created.|
| `transit_gateways.updated_at` | String | The date and time resource is last updated.|
| `transit_gateways.crn` | String | The CRN of the gateway.|
| `transit_gateways.global` | String | The gateways with global routing true to connect to the networks outside the associated region.|
| `transit_gateways.id` | String | The unique identifier of this gateway.|
| `transit_gateways.location` | String | The gateway location.|
| `transit_gateways.name` | String | The user-defined name for the transit gateway connection.|
| `transit_gateways.status` | String | The gateway status.|
| `transit_gateways.resource_group` | String | Resource group identifier.|






## `ibm_tg_location`
{: #tg-location-ds}
 
Imports the information of an existing {{site.data.keyword.cloud_notm}} infrastructure transit location as a read only data source.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #tg-location-sample}

The following example shows the details of transit location data source. 
{: shortdesc}

```
data "ibm_tg_location" "ds_tg_location" {
  name = "us-south"
}
```

### Input parameters
{: #tg-location-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `name` | String | Required | The name of the transit gateway location. |

### Output parameters
{: #tg-location-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `billing_location` | String | The geographical location of the location, used for billing purposes.|
| `name` | String | The name of the location.|
| `type` | String | The type of the location, determining a `multi-zone region`, a `single data center`, or a `point of presence`.|
| `local_connection_locations` | String | The set of network locations that are considered local for the transit gateway location.|
| `local_connection_locations.display_name` | String |The descriptive display name for the location.|
| `local_connection_locations.name` | String | The name of the location.|
| `local_connection_locations.type` | String | The type of the location, determining a `multi-zone region`, a `single data center`, or a `point of presence`.|





## `ibm_tg_locations`
{: #tg-locations-ds}
 
Imports the information of an existing {{site.data.keyword.cloud_notm}} infrastructure transit location as a read only data source.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #tg-locations-sample}

The following example shows the details of transit locations data source. 
{: shortdesc}

```
data "ibm_tg_locations" "ds_tg_locations" {
}
```

### Input parameters
{: #tg-locations-input}

There is no input parameters for `ibm_tg_locations`.

### Output parameters
{: #tg-locations-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `locations` | String | List of all locations that supports transit gateways.|
| `locations.billing_location` | String | The geographical location of the location, used for billing purposes.|
| `locations.name` | String | The name of the location.|
| `locations.type` | String | The type of the location, determining a `multi-zone region`, a `single data center`, or a `point of presence`.|





