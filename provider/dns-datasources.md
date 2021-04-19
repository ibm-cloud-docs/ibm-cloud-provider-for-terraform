---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

keywords: terraform provider plugin, terraform dns service, terraform dns, terraform private dns

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



# DNS Services data sources 
{: #dns-data-sources}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

## `ibm_dns_glbs`
{: #dns-glbs-ds}

Retrieve the details of an existing {{site.data.keyword.cloud_notm}} infrastructure private DNS Global Load Balancers as a read-only data source. For more information, see [Working with global Load Balancers](/docs/dns-svcs?topic=dns-svcs-global-load-balancers).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-glbs-ds-sample}

```
data "ibm_dns_glbs" "test1" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
}
```
{: codeblock}

### Input parameters
{: #dns-glbs-ds-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`instance_id`|String|Required|The GUID of the private DNS service instance.|
|`zone_id`|String|Required|The ID of the private DNS zone.|

### Output parameters
{: #dns-glbs-ds-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`dns_glbs`|List|List of all private DNS Load balancers in the {{site.data.keyword.cloud_notm}} infrastructure.|
|`dns_glbs.name`|String|The name of the DNS Load balancers.|
|`dns_glbs.description`|String|The descriptive text of the DNS Load balancers.|
|`dns_glbs.ttl`|String| The time to live in second.|
|`dns_glbs.fallback_pool`|String|The pool ID to use when all other pools are detected as unhealthy.|
|`dns_glbs.default_pools`|String|TA list of pool IDs ordered by their failover priority.|
|`dns_glbs.az_pools`|List|Map availability zones to the pool ID's.|
|`dns_glbs.az_pools.availability_zone`|String|The availability zone.|
|`dns_glbs.az_pools.pools`|String|List of Load Balancer pools.|
|`created_on`|Timestamp|The date and time when the Load Balancer was created.|
|`modified_on`|Timestamp|The date and time when the Load Balancer was modified.|
|`glb_id`|String|The Load Balancer ID.|
|`health`|String|Healthy state of the Load Balancer. Possible values are `DOWN`, `UP`, or `DEGRADED`.|

## `ibm_dns_glb_monitors`
{: #dns-glb-monitors-ds}

Retrieve the details of an existing {{site.data.keyword.cloud_notm}} infrastructure private DNS Global Load Balancers monitors as a read-only data source. For more information, see [Viewing Global Load Balancer events](/docs/dns-svcs?topic=dns-svcs-health-check-events).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-glb-monitors-ds-sample}

```
data "ibm_dns_glb_monitors" "ds_pdns_glb_monitors" {
  instance_id = "resource_instance_guid"
}
```
{: codeblock}

### Input parameters
{: #dns-glb-monitors-ds-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`instance_id`|String|Required|The GUID of the private DNS service instance.|

### Output parameters
{: #dns-glb-monitors-ds-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`dns_glb_monitors`|List|List of all private DNS Load balancer monitors in the {{site.data.keyword.cloud_notm}} infrastructure.|
|`dns_glb_monitors.name`|String|The name of the DNS Load balancer monitor.|
|`dns_glb_monitors.description`|String|The descriptive text of the DNS Load balancer monitor.|
|`dns_glb_monitors.type`|String| The protocol to use for the health check. Currently supported protocols are `HTTP`, `HTTPS`, and `TCP`.|
|`dns_glb_monitors.port`|String| Port number to connect to for the health check. Required for TCP checks, HTTP, and HTTPS checks.|
|`dns_glb_monitors.interval`|String|The interval between each health check.|
|`dns_glb_monitors.retries`|String |The number of retries to attempt in case of a timeout before marking the origin as unhealthy.|
|`dns_glb_monitors.timeout`|String|The timeout (in seconds) before marking the health check as failed.|
|`dns_glb_monitors.method`|String|The method to use for the health check applicable to HTTP, HTTPS based checks, the default value is `GET`.|
|`dns_glb_monitors.path`|String|The endpoint path to health check against. This parameter is only valid for HTTP and HTTPS monitors.|
|`dns_glb_monitors.headers`|String|The HTTP request headers to send in the health check.|
|`dns_glb_monitors.headers.name`|String|The name of the HTTP request header.|
|`dns_glb_monitors.headers.value`|String|The value of the HTTP request header.|
|`dns_glb_monitors.allow_insecure`|String|Do not validate the certificate when monitor use HTTPS|
|`dns_glb_monitors.expected_codes`|String|The expected HTTP response code or code range of the health check.|
|`dns_glb_monitors.expected_body`|String|A case insensitive substring to look for in the response body.|
|`dns_glb_monitors.monitor_id`|String|The monitor ID.|

## `ibm_dns_glb_pools`
{: #dns-glb-pools-ds}

Retrieve the details of an existing {{site.data.keyword.cloud_notm}} infrastructure private DNS Global Load Balancers pools as a read-only data source. For more information, see [Viewing Global Load Balancer events](/docs/dns-svcs?topic=dns-svcs-health-check-events).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-glb-pools-ds-sample}

```
data "ibm_dns_glb_pools" "ds_pdns_glb_pools" {
  instance_id = "resource_instance_guid"
}
```
{: codeblock}

### Input parameters
{: #dns-glb-pools-ds-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`instance_id`|String|Required|The resource GUID of the private DNS service on which zones are created.|

### Output parameters
{: #dns-glb-pools-ds-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`dns_glb_pools`|List|List of all private DNS Load balancer pools in the {{site.data.keyword.cloud_notm}} infrastructure.|
|`dns_glb_pools.name`|String|The name of the DNS Load balancer pool.|
|`dns_glb_pools.description`|String|The descriptive text of the DNS Load balancer pool.|
|`dns_glb_pools.enable`|String| Whether the Load Balancer pool is enabled.|
|`dns_glb_pools.healthy_origins_threshold`|String| The minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls less than this number, the pool will be marked unhealthy and will failover to the next available pool.|
|`dns_glb_pools.origins`|List|The list of origins within the pool. Traffic directed to the pool is balanced across all currently healthy origins, provided the pool itself is healthy.|
|`dns_glb_pools.origins.name`|String|The name of the origin server.|
|`dns_glb_pools.origins.description`|String|The description of the origin server.|
|`dns_glb_pools.origins.address`|String|The address of the origin server. It can be a hostname or an IP address.|
|`dns_glb_pools.origins.enabled`|String|Whether the origin server is enabled.|
|`dns_glb_pools.origins.health`|String|Whether the health is `true` or `false`.|
|`dns_glb_pools.origins.health_failure_reason`|String|The reason for the health check failure.|
|`dns_glb_pools.monitor`|String|The ID of the Load Balancer monitor to be associated to this pool.|
|`dns_glb_pools.notification_channel`|String|The webhook URL as a notification channel.|
|`dns_glb_pools.healthcheck_region`|String|Health check region of VSIs. Allowable values are `us-south`,`us-east`, `eu-gb`, `eu-du`, `au-syd`, `jp-tok`.|
|`dns_glb_pools.healthcheck_subnets`|String|Health check subnet CRN of VSIs.|
|`dns_glb_pools.pool_id`|String|The pool ID.|
|`dns_glb_pools.created_on`|Timestamp|The time (created On) of the DNS Global Load Balancer pool|
|`dns_glb_pools.modified_on`|Timestamp|he time (modified On) of the DNS Global Load Balancer pool.|
|`dns_glb_pools.health`|String|The status of DNS GLB pool's health. Possible values are `DOWN`, `UP`, `DEGRADED`.|

## `ibm_dns_permitted_networks`
{: #dns-permitted-network}

Retrieve details about permitted networks for a zone that is associated with the private DNS service instance. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-permitted-network-sample}

```
data "ibm_resource_group" "rg" {
  name = "default"
}

resource "ibm_is_vpc" "test_pdns_vpc" {
  name           = "test-pdns-vpc"
  resource_group = data.ibm_resource_group.rg.id
}

resource "ibm_resource_instance" "test-pdns-instance" {
  name              = "test-pdns"
  resource_group_id = data.ibm_resource_group.rg.id
  location          = "global"
  service           = "dns-svcs"
  plan              = "standard-dns"
}

resource "ibm_dns_zone" "test-pdns-zone" {
  name        = "test.com"
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  description = "testdescription"
  label       = "testlabel-updated"
}

resource "ibm_dns_permitted_network" "test-pdns-permitted-network-nw" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  vpc_crn     = ibm_is_vpc.test_pdns_vpc.crn
}

data "ibm_dns_permitted_networks" "test" {
  instance_id = ibm_dns_permitted_network.test-pdns-permitted-network-nw.instance_id
  zone_id     = ibm_dns_permitted_network.test-pdns-permitted-network-nw.zone_id
}
```
{: codeblock}

### Input parameters
{: #dns-permitted-network-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`instance_id`|String|Required|The ID of the private DNS service instance where you created permitted networks.|
|`zone_id`|String|Required|The ID of the zone where you added the permitted networks.|


### Output parameters
{: #dns-permitted-network-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`permitted_networks`|List of permitted networks|A list of all permitted networks that were created for a zone in your private DNS instance. |
|`permitted_networks.created_on`|Timestamp|The date and time when the permitted network was created.|
|`permitted_networks.instance_id`|String|The ID of the private DNS service instance where you created permitted networks.
|`permitted_networks.modified_on`|Timestamp|The date and time when the permitted network was updated.|
|`permitted_networks.permitted_network`|List of VPCs|A list of VPC CRNs that are associated with the permitted network.| 
|`permitted_networks.permitted_network.vpc_crn`|String|The CRN of the VPC that the permitted network belongs to. | 
|`permitted_networks.permitted_network_id`|String|The ID of the permitted network.|
|`permitted_networks.state`|String|The state of the permitted network.| 
|`permitted_networks.type`|String|The type of the permitted network.|
|`permitted_networks.zone_id`|String|The ID of the zone where you added the permitted network.|

## `ibm_dns_resource_records`
{: #dns-record}

Retrieve details about existing IBM Cloud private domain name service records. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-record-template}

```
data "ibm_dns_resource_records" "ds_pdns_resource_records" {
  instance_id = "resource_instance_guid"
  zone_id = "resource_dns_resource_records_zone_id"
}
```
{: codeblock}

### Input parameters
{: #dns-record-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`instance_id`|String|Required|The ID of the private DNS service instance.|
|`zone_id`|String|Required|The ID of the zone that you added to the private DNS service instance.|

### Output parameters
{: #dns-record-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`dns_resource_records`|List of DNS records|A list of all private domain name service resource records. |
|`dns_resource_records.id`|String|The unique identifier of the private DNS resource record.|
|`dns_resource_records.name`|String|The name of a private DNS resource record.|
|`dns_resource_records.type`|String|The type of the private DNS resource record. Supported values are `A`, `AAAA`, `CNAME`, `PTR`, `TXT`, `MX`, and `SRV`.|
|`dns_resource_records.rdata`|String|The resource data of a private DNS resource record.
|`dns_resource_records.ttl`|Integer|The time-to-live value of the DNS resource record.|

## `ibm_dns_zones`
{: #dns-zones}

Retrieve details about a zone that you added to your private DNS service instance.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-zones-sample}

```
data "ibm_dns_zones" "ds_pdnszones" {
  instance_id = "resource_instance_guid"
}
```
{: codeblock}

### Input parameters
{: #dns-zones-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`instance_id`|String|Required|The ID of the private DNS service instance.|

### Output parameters
{: #dns-zones_output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`dns_zones`|List of zones|A List of zones that you added to your private DNS service instance.| 
|`dns_zones.zone_id`|String|The ID of the zone.|
|`dns_zones.instance_id`|String|The ID of the private DNS service instance where you added the zone.|
|`dns_zones.description`|String|The description of the zone.|
|`dns_zones.name`|String|The name of the zone.|
|`dns_zones.label`|String|The label of the zone.|
|`dns_zones.created_on`|Timestamp|The date and time when the zone was added to the private DNS service instance.|
|`dns_zones.modified_on`|Timestamp|The date and time when the zone was updated.|
|`dns_zones.state`|String|The state of the zone.|


