---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-06"

keywords: terraform provider plugin, terraform dns, terraform vpc dns, terraform private dns

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


# DNS Services resources
{: #dns-resources}

Review the IBM Cloud DNS service resources that you can create, modify, or delete. You can reference the output parameters for each resource in other resources or data sources by using [IBM Cloud Provider plug-in for Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

For more information, about IBM Cloud DNS service, see [About DNS services](/docs/dns-svcs?topic=dns-svcs-about-dns-services).

Before you start working with your resource, make sure to review the [required parameters](/docs/terraform?topic=terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your IBM Cloud Provider plug-in for Terraform configuration file. 
{: important}


## `ibm_dns_glb`
{: #dns-glb}

Provides a private DNS Global Load Balancer resource. This allows DNS Global Load Balancer to create, update, and delete. For more information, see [Working with global Load Balancers](/docs/dns-svcs?topic=dns-svcs-global-load-balancers). 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dns-glb-sample}

```
resource "ibm_dns_glb" "test_pdns_glb" {
  depends_on    = [ibm_dns_glb_pool.test_pdns_glb_pool]
  name          = "testglb"
  instance_id   = ibm_resource_instance.test_pdns_instance.guid
  zone_id       = ibm_dns_zone.test_pdns_glb_zone.zone_id
  description   = "new glb"
  ttl           = 120
  fallback_pool = ibm_dns_glb_pool.test_pdns_glb_pool.pool_id
  default_pools = [ibm_dns_glb_pool.test_pdns_glb_pool.pool_id]
  az_pools {
    availability_zone = "us-south-1"
    pools             = [ibm_dns_glb_pool.test_pdns_glb_pool.pool_id]
  }
}
```
{: codeblock}

### Input parameters
{: #dns-glb-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
| `az_pools` | Set | Optional | Map availability zones to pool ID's.| No |
|`az_pools.availability_zone`|String|Required | Availability of the zone. | No |
|`az_pools.pools`|List of String|Required |List of Load Balancer pools.| No |
|`default_pools`|list of Strings|Required |TA list of pool IDs ordered by their failover priority.| No |
|`description`|String|Optional| Descriptive text of the Load Balancer.| No |
|`fallback_pool`|Integer|Required |The pool ID to use when all other pools are detected as unhealthy.| No |
|`instance_id`|String|Required|The GUID of the private DNS.| Yes |
|`name`|String|Required|The name of the Load Balancer.| No |
|`ttl`|Integer|Optional|The time to live (TTL) in seconds.| No |
|`zone_id`|String|Required|The ID of the private DNS Zone.| Yes |

### Output parameters
{: #dns-glb-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`created_on`|Timestamp|The time when the Load Balancer was created.| 
|`glb_id`|String|The Load Balancer ID.| 
|`health`|String|Healthy state of the Load Balancer. Possible values are `DOWN`, `UP`, or `DEGRADED`.| 
|`id`|String|The unique identifier of the DNS record. The ID is composed of `<instance_id>/<zone_id>/<glb_id>`.|
|`modified_on`|Timestamp|The time when the Load Balancer was modified.|

### Import
{: #dns-glb-import}

The `ibm_dns_glb` can be imported by using private DNS instance ID, zone ID, and global Load Balancer ID.

**Example**

```
terraform import ibm_dns_glb.example 6ffda12064634723b079acdb018ef308/5ffda12064634723b079acdb018ef308/435da12064634723b079acdb018ef308
```
{: pre}





## `ibm_dns_glb_monitor`
{: #dns-glb-monitor}

Provides a private DNS Global Load Balancer monitor resource. This allows DNS Global Load Balancer monitor to create, update, and delete. For more information, see [Viewing Global Load Balancer events](/docs/dns-svcs?topic=dns-svcs-health-check-events). 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dns-glb-monitor-sample}

```
resource "ibm_dns_glb_monitor" "test-pdns-monitor" {
  depends_on     = [ibm_dns_zone.test-pdns-zone]
  name           = "test-pdns-glb-monitor"
  instance_id    = ibm_resource_instance.test-pdns-instance.guid
  description    = "test monitor description"
  interval       = 63
  retries        = 3
  timeout        = 8
  port           = 8080
  type           = "HTTP"
  expected_codes = "200"
  path           = "/health"
  method         = "GET"
  expected_body  = "alive"
  headers {
    name  = "headerName"
    value = ["example", "abc"]
  }
}
```
{: codeblock}

### Input parameters
{: #dns-glb-monitor-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
| `expected_body` | String | Optional | A case-insensitive sub-string to look in the response body. If the string is not found, the origin will be marked as unhealthy. This parameter is only valid for HTTP and HTTPS monitors.| No |
|`expected_codes`|String|Optional | The expected HTTP response code or code range of the health check. This parameter is only valid for HTTP and HTTPS monitors. Allowable values are `200, 201, 202, 203, 204,205, 206, 207, 208, 226, xx`. | No |
|`allow_insecure`|String|Optional | Do not validate the certificate when monitor use HTTPS. This parameter is currently only valid for HTTPS monitors.| No |
|`description`|String|Optional| Descriptive text of the Load Balancer monitor.| No |
|`headers`|Set|Optional |The HTTP request headers to send in the health check. It is recommended you set a host header by default. The `User-Agent` header cannot be overridden. This parameter is only valid for HTTP and HTTPS monitors.| No |
|`headers.name`|String|Required|The name of the HTTP request header.| No |
|`headers.value`|list of Strings|Required |The value of HTTP request header.| No |
|`interval`|Integer|Optional | The interval between each health check.| No |
|`instance_id`|String|Required|The GUID of the private DNS.| Yes |
|`method`|String|Optional | The method to use for the health check applicable to HTTP or HTTPS based checks, the default value is `GET`.| No |
|`name`|String|Required|The name of the Load Balancer monitor.| No |
|`path`|String|Optional | The endpoint path to health check against. This parameter is only valid for HTTP and HTTPS monitors.| No |
|`port`|Integer|Optional | The port number to connect to for the health check. Required for TCP checks. HTTP and HTTPS checks should only define the port when using a non-standard port. For example, HTTP  default is `80`, and HTTPS default is `443`).| No |
|`retries`|Integer|Optional | The number of retries to attempt in case of a timeout before marking the origin as unhealthy.| No |
|`timeout`|Integer|Optional | The timeout (in seconds) before marking the health check as failed.| No |
|`type`|String|Optional|The protocol to use for the health check. Currently supported protocols are `HTTP`,`HTTPS` and `TCP`. Default Value is `HTTP` | Yes |

### Output parameters
{: #dns-glb-monitor-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`created_on`|Timestamp|The time (created On) of the DNS Global Load Balancer monitor.| 
|`id`|String|The unique ID of the private DNS Monitor. The ID is composed of `<instance_id>/<glb_monitor_id>`.| 
|`modified_on`|Timestamp|The time (modified On) of the DNS Global Load Balancer monitor.|
|`monitor_id`| The monitor ID.|

### Import
{: #dns-glb-monitor-import}

The `ibm_dns_glb_monitor` can be imported by using private DNS instance ID, and GLB Monitor ID.

**Example**

```
terraform import ibm_dns_glb_monitor.example 6ffda12064634723b079acdb018ef308/435da12064634723b079acdb018ef308
```
{: pre}






## `ibm_dns_glb_pool`
{: #dns-glb-pool}

Provides a private DNS Global Load Balancer pool resource. This allows DNS Global Load Balancer pool to  create, update, and delete. For more information, see [Viewing Global Load Balancer events](/docs/dns-svcs?topic=dns-svcs-health-check-events#health-check-event-properties)
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dns-glb-pool-sample}

```
resource "ibm_dns_glb_pool" "test-pdns-pool-nw" {
  depends_on                = [ibm_dns_zone.test-pdns-glb-pool-zone]
  name                      = "testpool"
  instance_id               = ibm_resource_instance.test-pdns-glb-pool-instance.guid
  description               = "New test pool"
  enabled                   = true
  healthy_origins_threshold = 1
  origins {
    name        = "example-1"
    address     = "www.google.com"
    enabled     = true
    description = "origin pool"
  }
  monitor              = ibm_dns_glb_monitor.test-pdns-glb-monitor.monitor_id
  notification_channel = "https://mywebsite.com/dns/webhook"
  healthcheck_region   = "us-south"
  healthcheck_subnets  = [ibm_is_subnet.test-pdns-glb-subnet.resource_crn]
}
```
{: codeblock}

### Input parameters
{: #dns-glb-pool-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}


|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
| `instance_id` | String | Required | The GUID of the private DNS on which zone has to be created.| Yes |
|`name`|String|Required | The name of the origin server. | No |
|`enabled`|Bool|Optional | Whether the origin server is enabled.| No |
|`description`|String|Optional| Descriptive text of the origin server.| No |
|`healthy_origins_threshold`|Integer|Optional |The minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls below this number, the pool will be marked unhealthy and will failover to the next available pool.| No |
|`origins`|Set|Required|The list of origins within this pool. Traffic directed at this pool is balanced across all currently healthy origins, provided the pool itself is healthy.| No |
|`origins.address`|String|Required | The address of the origin server. It can be a hostname or an IP address. | No |
|`origins.name`|String|Required | The name of the origin server. | No |
|`origins.description`|String|Optional| Descriptive text of the origin server.| No |
|`origins.enabled`|Bool|Optional | Whether the origin server is enabled.| No |
|`address`|String|Required |The address of the origin server. It can be a hostname or an IP address.| No |
|`monitor`|String|Optional | The ID of the Load Balancer monitor to be associated to this pool. | No |
|`notification_channel`|String|Optional|The webhook URL as a notification channel.| No |
|`healthcheck_region`|String|Optional | Health check region of VSIs. Allowable values are `us-south`,`us-east`, `eu-gb`, `eu-du`, `au-syd`, `jp-tok`.| No |
|`healthcheck_subnets`|List|Optional|The health check subnet CRN of VSIs. | No |

### Output parameters
{: #dns-glb-pool-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`created_on`|Timestamp|The time (created On) of the DNS Global Load Balancer pool.| 
|`id`|String|The unique ID of the private DNS zone. The ID is composed of `<instance_id>/<glb_pool_id>`.| 
|`pool_id`| The pool ID.|
|`modified_on`|Timestamp|The time (modified On) of the DNS Global Load Balancer pool.|
|`health`| The status of DNS GLB pool's health. Possible values are `DOWN`, `UP`, `DEGRADED`.|
|`origins.health`| Whether the health is `ture` or `false`. |
|`origins.health_failure_reason`| The reason for health check failure.|

### Import
{: #dns-glb-pool-import}

The `ibm_dns_glb_pool` can be imported by using private DNS instance ID, GLB pool ID.

**Example**

```
terraform import ibm_dns_glb_pool.example 6ffda12064634723b079acdb018ef308/435da12064634723b079acdb018ef308
```
{: pre}





 
## `ibm_dns_permitted_network`
{: #dns-permitted-network}

Create or delete a DNS permitted network. For more information, see [Managing permitted networks](/docs/dns-svcs?topic=dns-svcs-managing-permitted-networks).
{: shortdesc}

You can add a VPC as a permitted network to a DNS entry only. 
{: note}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dns-permitted-network-sample}

```
resource "ibm_dns_permitted_network" "test-pdns-permitted-network-nw" {
    instance_id = ibm_resource_instance.test-pdns-instance.guid
    zone_id = ibm_dns_zone.test-pdns-zone.zone_id
    vpc_crn = ibm_is_vpc.test_pdns_vpc.crn
    type = "vpc"
}
```

### Input parameters
{: #dns-permitted-network-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`instance_id`|String|Required|The ID of the IBM Cloud DNS service instance where you want to add a permitted network.|
|`zone_id`|String|Required|The ID of the private DNS zone where you want to add the permitted network.|
|`vpc_crn`|String|Required|The CRN of the VPC that you want to add as a permitted network.|
|`type`|String|Required|The type of permitted network that you want to add. Supported values are `vpc`.|

### Output parameters
{: #dns-permitted-network-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the DNS private network. The ID is composed of `<instance_ID>/<zone_ID>/<permitted_network_ID>`. |
|`created_on`|Timestamp|The time when the permitted network was added to the DNS.|
|`modified_on`|Timestamp|The time when the permitted network was modified.|

## `ibm_dns_resource_record`
{: #dns-record}

Create, update, or delete a DNS record. For more information, see [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records). 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dns-record-sample}

```
resource "ibm_dns_resource_record" "test-pdns-resource-record-a" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  type        = "A"
  name        = "testA"
  rdata       = "1.2.3.4"
  ttl         = 3600
}

resource "ibm_dns_resource_record" "test-pdns-resource-record-aaaa" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  type        = "AAAA"
  name        = "testAAAA"
  rdata       = "2001:0db8:0012:0001:3c5e:7354:0000:5db5"
}

resource "ibm_dns_resource_record" "test-pdns-resource-record-cname" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  type        = "CNAME"
  name        = "testCNAME"
  rdata       = "test.com"
}

resource "ibm_dns_resource_record" "test-pdns-resource-record-ptr" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  type        = "PTR"
  name        = "1.2.3.4"
  rdata       = "testA.test.com"
}

resource "ibm_dns_resource_record" "test-pdns-resource-record-mx" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  type        = "MX"
  name        = "testMX"
  rdata       = "mailserver.test.com"
  preference  = 10
}

resource "ibm_dns_resource_record" "test-pdns-resource-record-srv" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  type        = "SRV"
  name        = "testSRV"
  rdata       = "tester.com"
  priority    = 100
  weight      = 100
  port        = 8000
  service     = "_sip"
  protocol    = "udp"
}

resource "ibm_dns_resource_record" "test-pdns-resource-record-txt" {
  instance_id = ibm_resource_instance.test-pdns-instance.guid
  zone_id     = ibm_dns_zone.test-pdns-zone.zone_id
  type        = "TXT"
  name        = "testTXT"
  rdata       = "textinformation"
  ttl         = 900
}
```
{: codeblock}

### Input parameters
{: #dns-record-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`instance_id`|String|Required|The ID of the IBM Cloud DNS service instance where you want to create the DNS record.|
|`zone_id`|String|Required|The ID of the DNS zone where you want to create a DNS record.|
|`type`|String|Required|The type of DNS record that you want to create. Supported values are `A`, `AAAA`, `CNAME`, `PTR`, `TXT`, `MX`, and `SRV`.|
|`name`|String|Required|The name of the DNS record.| 
|`rdata`|String|Required|The resource data of a DNS resource record.
|`ttl`|Integer|Optional|The time to live (TTL) in minutes that the resolved DNS record is cached before the associated IP address must be retrieved again. The minimum TTL must be 1 minute and can be 12 hours at a maximum. If no value is specified, 15 minutes is used by default. To find the default TTL values for each record type, see [Adding DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records#adding-dns-records).|
|`preference`|Integer|Required for `MX` records|If you create an `MX` record, enter the preference of the record.|
|`priority`|Integer|Required for `SRV` records|If you create an `SRV` record, enter the priority of the record.|
|`weight`|Integer|Required for `SRV` records|If you create an `SRV` record, enter the weight of the record. The weight is considered when multiple records with the same priority exist. A higher value is associated with a higher weight and a higher chance of being considered among records with the same priority.|
|`port`|Integer|Required for `SRV` records|If you create an `SRV` record, enter the TCP or UDP port of the target server. |
|`service`|String|Required for `SRV` records|If you create an `SRV` record, enter the name of the service that you want. The name must start with an underscore (`_`).|
|`protocol`|String|Required for `SRV` records|If you create an `SRV` record, enter the name of the protocol that you want. |

### Output parameters
{: #dns-record-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the DNS record. The ID is composed of `<instance_id>/<zone_id>/<dns_record_id>`.|
|`zone_id`|String|The ID of the zone where the DNS record was created.| 
|`resource_record_id`|String|The ID of the DNS record.| 
|`created_on`|Timestamp|The time when the DNS record was created.| 
|`modified_on`|Timestamp|The time when the DNS record was modified.|

### Import
{: #dns-record-import}

The resource can be imported by using the DNS record ID, zone ID and resource record ID. 

```
terraform import ibm_dns_resource_record.example <instance_id>/<zone_id>/<dns_record_id>
```
{: pre}





## `ibm_dns_zone`
{: #dns-zone}

Create, update, or delete a DNS zone. For more information, see [Managing DNS zones](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones).
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #dns-zone-sample}

```
resource "ibm_dns_zone" "pdns-1-zone" {
    name = "test.com"
    instance_id = p-dns-instance-id
    description = "testdescription"
    label = "testlabel"
}
```
{: codeblock}

### Input parameters
{: #dns-zone-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the DNS zone that you want to create.| 
|`instance_id`|String|Required|The ID of the IBM Cloud DNS service instance where you want to create a DNS zone.|
|`description`|String|Optional|The description of the DNS zone.|
|`label`|String|Optional|The label of the DNS zone.| 

### Output parameters
{: #dns-zone-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the DNS zone. The ID is composed of `<instance_id>/<zone_id>`.|
|`zone_id`|String|The ID of the zone that is associated with the DNS zone. |
|`created_on`|Timestamp|The time when the DNS zone was created.| 
|`modified_on`|Timestamp|The time when the DNS zone was updated.| 
|`state`|String|The state of the DNS zone.|




