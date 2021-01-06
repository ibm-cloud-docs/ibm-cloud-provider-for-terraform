---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-06"

keywords:  terraform provider plugin, direct link gateway, terraform direct link gateway, terraform direct link gateway data sources

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


# Direct Link Gateway data sources
{: #dl-gateway-ds}

Use {{site.data.keyword.cloud_notm}} [Direct Link](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) to seamlessly connect your on-premises resources to your cloud resources. You can reference the output parameters for each resource in other resources or data sources by using [IBM Cloud Provider plug-in for Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}.
{: shordesc}

Before you start working with your data source, make sure to review the [required parameters](/docs/terraform?topic=terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your IBM Cloud Provider plug-in for Terraform configuration file. 
{: important}

## ibm_dl_gateway
{: #dl_gateway_ds}

Import the details of an existing {{site.data.keyword.cloud_notm}} infrastructure direct link gateway and its virtual connections.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dl-gw-dssample}

```
      data "ibm_dl_gateway" "test_dl_gateway_vc" {
			name = "mygateway"
		 }"
     
```
{: codeblock}

### Input parameters
{: #api-dl-gw-dsinput}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`name`|String|Required|The unique user-defined name for the gateway. |


### Output parameters
{: #dl-gw-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`bgp_asn`|String|Customer BGP ASN.|
|`created_at`|String|The date and time resource is created.|
|`crn`|String|The CRN of the gateway.|
|`global`|Boolean|Gateway with global routing as `true` can connect networks outside your associated region.|
|`id`|String|The unique identifier of the gateway.|
|`location_display_name`|String|Long name of the gateway location.|
|`location_name`|String|The location name of the gateway.|
|`metered`|String|Metered billing option. If set `true` gateway usage is billed per GB. Otherwise, flat rate is charged for the gateway.|
|`operational_status`|String|The gateway operational status|
|`resource_group`|String|The resource group identifier.|
|`speed_mbps`|String|The gateway speed in MBPS.|
|`type`|String|The gateway type.|
|`bgp_base_cidr`|String|The BGP base CIDR.|
|`bgp_cer_cidr`|String|The BGP customer edge router CIDR.|
|`bgp_ibm_asn`|String|The {{site.data.keyword.IBM_notm}} BGP ASN.|
|`bgp_ibm_cidr`|String|The {{site.data.keyword.IBM_notm}} BGP  CIDR.|
|`bgp_status`|String|The gateway BGP status.|
|`completion_notice_reject_reason`|String| The reason for completion notice rejection. Only included on a dedicated gateways type with a rejected completion notice.|
|`cross_connect_router`|String| The cross connect router. Only included on a dedicated gateways type. |
|`link_status` |String| The gateway link status. Only included on a dedicated gateways type.
|`port`|Integer|The port identifier.|
|`provider_api_managed`|Boolean|Indicates the gateway is created through a provider portal. If set `true`, gateway can only be changed. If set `false`, gateway is deleted through the corresponding provider portal.|
|`vlan`|String| The VLAN allocated for the gateway. Only set for connect gateways type created directly through the {{site.data.keyword.IBM_notm}} portal.|
|`virtual_connections`|String|List of the specified gateway's virtual connections.|
|`virtual_connections.created_at`|String|The creation date and time resource.|
|`virtual_connections.id`|String|The unique identifier of the virtual connection. For example, `ef4dcbtyu1a-fee4-41c7-9e11-9cd99e65c1f4`|
|`virtual_connections.name`|String|The unique user-defined name of the only virtual connection in the gateway.| 
|`virtual_connections.status`|String| The status of the virtual connection. Possible values are `pending`,`attached`,`approval_pending`,`rejected`,`expired`,`deleting`,`detached_by_network_pending`,`detached_by_network`.|
|`virtual_connections.type`|String|The virtual connection type. Possible values are `classic`,`vpc`.|
|`virtual_connections.network_account`|String|For virtual connections across two different {{site.data.keyword.cloud_notm}} accounts. Network_account indicates the account you own the target network. For example, `00aa14a2e0fb102c8995ebefhhhf8655556`
|`virtual_connections.network_id`|String| The unique identifier of the target network. For type `vpc`, virtual connections is the CRN of the target VPC. This field do not apply for type `classic` connections. For example, `crn:v1:bluemix:public:is:us-east:a/28e4d90ac7504be69447111122223333::vpc:aaa81ac8-5e96-42a0-a4b7-6c2e2dbb`|

## ibm_dl_gateways
{: #dl_gateways_ds}

Import the details of an existing {{site.data.keyword.cloud_notm}} infrastructure direct link gateways.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dl-gws-dssample}

```
data "ibm_dl_gateways" "ds_dlgateways" {
}
     
```
{: codeblock}

### Input parameters
{: #api-dl-gws-dsinput}

There is no input parameters that you need to specify for the data source. 
{: shortdesc}

### Output parameters
{: #dl-gws-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`gateways`|String|List of all the direct link gateways in the {{site.data.keyword.cloud_notm}} infrastructure.|
|`gateways.bgp_asn`|String|Customer BGP ASN.|
|`gateways.created_at`|String|The date and time resource is created.|
|`gateways.crn`|String|The CRN of the gateway.|
|`gateways.global`|Boolean|Gateway with global routing as `true` can connect networks outside your associated region.|
|`gateways.id`|String|The unique identifier of the gateway.|
|`gateways.location_display_name`|String|Long name of the gateway location.|
|`gateways.location_name`|String|The location name of the gateway.|
|`gateways.metered`|String|Metered billing option. If set `true` gateway usage is billed per GB. Otherwise, flat rate is charged for the gateway.|
|`gateways.name`|String| The unique user defined name of the gateway.|
|`gateways.operational_status`|String|The gateway operational status|
|`gateways.resource_group`|String|The resource group identifier.|
|`gateways.speed_mbps`|String|The gateway speed in MBPS.|
|`gateways.type`|String|The gateway type.|
|`gateways.bgp_base_cidr`|String|The BGP base CIDR.|
|`gateways.bgp_cer_cidr`|String|The BGP customer edge router CIDR.|
|`gateways.bgp_ibm_asn`|String|The {{site.data.keyword.IBM_notm}} BGP ASN.|
|`gateways.bgp_ibm_cidr`|String|The {{site.data.keyword.IBM_notm}} BGP  CIDR.|
|`gateways.bgp_status`|String|The gateway BGP status.|
|`gateways.completion_notice_reject_reason`|String| The reason for completion notice rejection. Only included on a dedicated gateways type with a rejected completion notice.|
|`gateways.cross_connect_router`|String| The cross connect router. Only included on a dedicated gateways type. |
|`gateways.link_status` |String| The gateway link status. Only included on a dedicated gateways type.
|`gateways.port`|Integer|The port identifier.|
|`gateways.provider_api_managed`|Boolean|Indicates the gateway is created through a provider portal. If set `true`, gateway can only be changed. If set `false`, gateway is deleted through the corresponding provider portal.|
|`gateways.vlan`|String| The VLAN allocated for the gateway. Only set for connect gateways type created directly through the {{site.data.keyword.IBM_notm}} portal.|

## ibm_dl_locations
{: #dl_loc_ds}

Import the details of valid locations for the specified direct link offering.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dl-loc-dssample}

```
  data "ibm_dl_locations" "test_dl_locations"{
		offering_type = "dedicated"
	 }
	 
```
{: codeblock}

### Input parameters
{: #dl-loc-dsinput}

Retrieve the input parameters that you need to specify for the data source. 
{: shortdesc}

| Input parameter | Data type |Required / optional | Description |
| ------------- |-------------| --------------|-------------- |
|`offering_type`| String | Required|The direct link offering type. Possible values are `dedicated`,`connect`.| 

### Output parameters
{: #dl-loc-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`locations`|String|List of all the direct link locations in the {{site.data.keyword.cloud_notm}} infrastructure.|
|`locations.billing_location`|String|The billing location.|
|`locations.building_colocation_owner`|String|The building co-location owner. Only present for dedicated offering type locations.|
|`locations.name`|String|The location short name.|
|`locations.display_name`|String|The location long name.|
|`locations.location_type`|String|The location type.|
|`locations.market`|String|The market location.|
|`locations.market_geography`|String|The location geography.|
|`locations.mzr`|Boolean|Is location a multi-zone region.|
|`locations.vpc_region`|String| The location VPC region.|

## ibm_dl_offering_speeds
{: #dl_offering_spd_ds}

Import the details of an existing {{site.data.keyword.cloud_notm}} infrastructure direct link offering speed options.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dl-off-spd-dssample}

```
  data "ibm_dl_offering_speeds" "ds_dlspeedoptions" {
    offering_type="dedicated"
  }
```
{: codeblock}

### Input parameters
{: #dl-off-spd-dsinput}

Retrieve the input parameters that you need to specify for the data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`offering_type`| String | Required|The direct link offering type. Possible values are `dedicated`,`connect`.| 

### Output parameters
{: #dl-off-spd-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`offering_speeds`|String|List of all the direct link offering speeds in the {{site.data.keyword.cloud_notm}} infrastructure.|
|`offering_speeds.link_speed`|String|The link speed in megabits per second.|

## ibm_dl_port
{: #dl_port_ds}

Import the details of an existing {{site.data.keyword.cloud_notm}} infrastructure direct link offering port.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dl-port-dssample}

```
  data "ibm_dl_port" "ds_dlport" {
      port_id = "dl_port_id"
   }
```
{: codeblock}

### Input parameters
{: #dl-port-dsinput}

Retrieve the input parameters that you need to specify for the data source. 
{: shortdesc}

| Input parameter | Data type |Required / optional | Description |
| ------------- |-------------| --------------|-------------- |
|`port_id`| String | Required|The unique ID for the direct link port.| 

### Output parameters
{: #dl-port-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`direct_link_count`|String|The count of the existing direct link gateways on the port.|
|`label`|String|The port label.|
|`location_display_name`|String|The port location long name.|
|`location_name`|String|The port location name.|
|`provider_name`|String|The port's provider name.|
|`supported_link_speeds`|String|The port supported speeds in megabits per second.|

## ibm_dl_ports
{: #dl_ports_ds}

Import the details of an existing {{site.data.keyword.cloud_notm}} infrastructure direct link  ports.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dl-ports-dssample}

```
data "ibm_dl_ports" "ds_dlports" {
}
```
{: codeblock}

### Input parameters
{: #dl-ports-dsinput}

There is no input parameters that you need to specify for the data source. 
{: shortdesc}

### Output parameters
{: #dl-ports-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`ports`|String|List of all the direct link ports.|
|`ports.direct_link_count`|String|Count of the existing direct link gateways in this port account.|
|`ports.label`|String|The port label.|
|`ports.location_display_name`|String|The port location long name.|
|`ports.location_name`|String|The port location name.|
|`ports.id`|String|The port identifier.|
|`ports.provider_name`|String|The port's provider name.|
|`ports.supported_link_speeds`|String|The port supported speeds in megabits per second.|

## ibm_dl_routers
{: #dl_routers_ds}

Import the details of an existing {{site.data.keyword.cloud_notm}} infrastructure direct link  location specific cross connect router information.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dl-routers-dssample}

```
data "ibm_dl_routers" "test_dl_routers" {
	offering_type = "dedicated"
	location_name = "dal09"
}
```
{: codeblock}

### Input parameters
{: #dl-routers-dsinput}

The input parameters that you need to specify for the data source. 
{: shortdesc}

| Input parameter | Data type |Required / optional | Description |
| ------------- |-------------| --------------|-------------- |
|`offering_type`|String|Required|The direct link offering type. Only `dedicated` is supported in this API.|
|`location_name`|String|Required|The name of the direct link location.|

### Output parameters
{: #dl-routers-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`cross_connect_routers`|String|List of all the cross connect router details.|
|`cross_connect_routers.router_name`|String|The name of the router.|
|`cross_connect_routers.total_connections`|String|Count of existing direct link dedicated gateways on this router account.|
