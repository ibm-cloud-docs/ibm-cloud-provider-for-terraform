---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-08"

keywords: terraform provider plugin, terraform provider cos, terraform resources cos, terraform resources object storage, create bucket with terraform

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



# Object Storage data sources
{: #object-storage-data-sources}

Review the data sources that you can use to retrieve information about your {{site.data.keyword.cos_full_notm}} instance. All data sources are imported as read-only information. You can reference the output parameters for each data source by using Terraform interpolation syntax. 
{: shortdesc}

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_cos_bucket`
{: #cos-bucket}

Retrieve information about an {{site.data.keyword.cos_full_notm}} bucket. 
{: shortdesc}

### Sample Terraform code
{: #cos-bucket-sample}

The following example shows how to retrieve information about your {{site.data.keyword.cos_full_notm}} service instance and the bucket. 
{: shortdesc}

```
data "ibm_resource_group" "cos_group" {
  name = "cos-resource-group"
}

data "ibm_resource_instance" "cos_instance" {
  name              = "cos-instance"
  resource_group_id = data.ibm_resource_group.cos_group.id
  service           = "cloud-object-storage"
}

data "ibm_cos_bucket" "standard-ams03" {
  bucket_name          = "a-standard-bucket-at-ams"
  resource_instance_id = data.ibm_resource_instance.cos_instance.id
  bucket_type          = "single_site_location"
  bucket_region        = "ams03"
}

output "bucket_private_endpoint" {
  value = data.ibm_cos_bucket.standard-ams03.s3_endpoint_private
}
```
{: codeblock}

### Input parameters
{: #cos-bucket-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `bucket_name` | String | Required | The name of the bucket. |
| `bucket_region` | String | Required | The region of the bucket. |
| `bucket_type` | String | Required | The type of the bucket. Supported values are `single_site_location`, `region_location`, and `cross_region_location`.  |
| `endpoint_type`|String | Optional| The type of the endpoint either public or private to be used for the buckets. Default value is `public`.|
| `resource_instance_id` | String | Required | The ID of the {{site.data.keyword.cos_full_notm}} service instance for which you want to create a bucket. |
| `storage_class`|String | Required | Storage class of the bucket. Supported values are `standard`, `vault`, `cold`, `flex`, `smart`.|



### Output parameters
{: #cos-bucket-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`allowed_ip`| String | List of `IPv4` or `IPv6` addresses in CIDR notation to be affected by firewall.|
|`activity_tracking`|List| Nested block wth the following structure.|
|`activity_tracking.read_data_events`|Array| Enables sending log data to Activity Tracker and LogDNA to provide visibility into an object read and write events.|
|`activity_tracking.write_data_events`|Bool| If set to `true`, all object write events (that is `uploads`) is sent to Activity Tracker.|
|`activity_tracking.activity_tracker_crn`|String| The first time activity_tracking is configured.|
|`archive_rule`|List|Nested block with the following structure.|
|`archive_rule.rule_id`|String| Unique identifier for the rule. Archive rules allow you to set a specific time frame after which objects transition to archive.|
|`archive_rule.enable`|Bool|Specifies archive rule status either `enable` or `disable` for a bucket.|
|`archive_rule.days`|String| Specifies the number of days when the specific rule action takes effect.|
|`archive_rule.type`|String| Specifies the storage class or archive type to which you want the object to transition. Supported values are `Glacier` or `Accelerated`.|
| `crn` | String | The CRN of the bucket. |
| `cross_region_location` | String | The location to create a cross-regional bucket. |
|`expire_rule`|List|Nested block with the following structure.|
|`expire_rule.rule_id`|String| Unique identifier for the rule. Expire rules allow you to set a specific time frame after which objects are deleted.|
|`expire_rule.enable`|Bool| Specifies expire rule status either `enable` or `disable` for a bucket.|
|`expire_rule.days`|String| Specifies the number of days when the specific rule action takes effect.|
|`expire_rule.prefix`|String| Specifies a prefix filter to apply to only a subset of objects with names that match the prefix.|
| `id` | String | The ID of the bucket. | 
| `key_protect` | String | The CRN of the {{site.data.keyword.keymanagementservicelong_notm}} instance where a root key is already provisioned. |
|`metrics_monitoring`|List |Nested block with the following structure|
|`metrics_monitoring.usage_metrics_enabled`|Bool| If set to `true`, all usage metrics (that is `bytes_used`) is sent to the monitoring service.
|`metrics_monitoring.metrics_monitoring_crn`|String|The first time `metrics_monitoring` is configured. The instance of {{site.data.keyword.cloud_notm}} monitoring that will receive the bucket metrics.|
| `region_location` | String | The location to create a regional bucket. |
| `resource_instance_id` | String | The ID of {site.data.keyword.cos_full_notm}} instance. | 
| `single_site_location` | String | The location to create a single site bucket. |
| `storage_class` | String | The storage class of the bucket. |
