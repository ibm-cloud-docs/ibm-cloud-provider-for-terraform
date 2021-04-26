---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-26"

keywords: terraform provider plugin, terraform satellite host, terraform satellite location

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



# Satellite resources
{: #satellite-resources}

With {{site.data.keyword.satellitelong_notm}}, you can bring your own infrastructure that is in your on-premises data center, in other cloud providers, or in edge environments to {{site.data.keyword.cloud_notm}} by creating a {{site.data.keyword.satelliteshort}} host and location.
{: shortdesc}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

## `ibm_satellite_host`
{: #satellite-host-resource}

Create, update, or delete [{{site.data.keyword.satellitelong_notm}} Host](/docs/satellite?topic=satellite-hosts). Assign a host to an {{site.data.keyword.satellitelong_notm}} location or cluster. Before you can assign hosts to clusters, first assign at least three hosts to the {{site.data.keyword.satelliteshort}} location, to run control plane operations. Then, when you have {{site.data.keyword.satelliteshort}} clusters, you can assign hosts as needed to provide compute resources for your workloads. You can assign hosts by specifying a host ID or by providing labels to match hosts to your request.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #satellite-host-sample}

Sample example to assign {{site.data.keyword.satelliteshort}} host to satellite control plane using {{site.data.keyword.vpc_short}}.
{: shortdesc}


```
resource "ibm_satellite_host" "assign_host" {
  count         = 3

  location      = "satellite-ibm"
  cluster       = "satellite-ibm"
  host_id       = element(var.host_vms, count.index)
  labels        = ["env:prod"]
  zone          = element(var.location_zones, count.index)
  host_provider = "ibm"
}
```
{: codeblock}

Sample example to assign {{site.data.keyword.satelliteshort}} control plane using AWS EC2.
{: shortdesc}


```
resource "ibm_satellite_host" "assign_host" {
  count         = 3

  location      = var.location
  host_id       = element(var.host_vms, count.index)
  labels        = ["env:prod"]
  zone          = element(var.location_zones, count.index)
  host_provider = "aws"
}
```
{: codeblock}

Sample example to assign {{site.data.keyword.satelliteshort}} host to {{site.data.keyword.openshiftshort}} {{site.data.keyword.satelliteshort}} cluster.
{: shortdesc}


```
resource "ibm_satellite_host" "assign_host" {
  count         = 3

  location      = var.location
  cluster       = var.satellite_cluster
  host_id       = element(var.host_vms, count.index)
  labels        = ["env:prod"]
  zone          = element(var.location_zones, count.index)
  host_provider = var.host_provider
}
```
{: codeblock}



### Input parameters
{: #satellite-host-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| 
|----|-----------|-----------|---------------------|
| `location`|String|Required| The name or ID of the {{site.data.keyword.satelliteshort}} location.|
| `cluster`|String|Optional|  The name or ID of a {{site.data.keyword.satelliteshort}} location or cluster to assign the host to.|
| `host_id`|String|Required|  The specific host ID to assign to a {{site.data.keyword.satelliteshort}}  location or cluster.|
| `labels`|Array of strings|Optional|  The key value pairs to label the host, such as `cpu=4` to describe the host capabilities.|
| `worker_pool`|String|Optional| The name or ID of the worker pool within the cluster to assign the host to.|
| `host_provider`|String|Optional| The name of host provider, such as `ibm`, `aws` or `azure`.|
{: caption="Table 1. Available input parameters" caption-side="top"}

### Output parameters
{: #satellite-host-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id`|String| The unique identifier of the location. The ID is combination of location and host_id delimited by `/`.|
| `host_state`|String| Health status of the host.|
| `zone`|String| The zone within the cluster to assign the host to.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #satellite-host-import}

`ibm_satellite_host` can be imported by using the location and host ID.

**Syntax**

```
terraform import ibm_satellite_host.host location/host_id
```
{: codeblock}

**Example**

```
terraform import ibm_satellite_host.host satellite-ibm/c0kinbr12312312
```
{: codeblock}


## `ibm_satellite_location`
{: #satellite-location-resource}

Create, update, or delete [{{site.data.keyword.satellitelong_notm}} Host](/docs/satellite?topic=satellite-locations). Set up an IBM Cloud™ Satellite location to represent a data center that you fill with your own infrastructure resources, and start running IBM Cloud services on your own infrastructure.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #satellite-location-sample}

Sample example to create {{site.data.keyword.satelliteshort}} location.
{: shortdesc}


```
resource "ibm_satellite_location" "create_location" {
  location      = var.location
  zones         = var.location_zones
  managed_from  = var.managed_from
}
```
{: codeblock}

Sample example to create {{site.data.keyword.satelliteshort}} location by using {{site.data.keyword.cos_full_notm}} bucket.
{: shortdesc}


```
resource "ibm_satellite_location" "create_location" {
  location      = var.location
  zones         = var.location_zones
  managed_from  = var.managed_from  

  cos_config {
    bucket  = var.cos_bucket
    region  = var.ibm_region
  }
}
```
{: codeblock}

### Input parameters
{: #satellite-location-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| 
|----|-----------|-----------|---------------------|
| `location`|String|Required| The name of the location to be created or pass existing location name.|
| `is_location_exist`| Bool | Optional | Determines the location has to be created or not.|
| `managed_from`|String|Required| The {{site.data.keyword.cloud_notm}} metro from which the {{site.data.keyword.satelliteshort}} location is managed. To list available multizone regions, run `ibmcloud ks locations`, such as `wdc04`, `wdc06`, or `lon04`.|
| `description` | String | Optional |  A description of the new Satellite location.|
| `logging_account_id` | String | Optional | The account ID for IBM Log Analysis with LogDNA log forwarding.|
| `cos_config` | List | Optional | The {{site.data.keyword.cos_full_notm}} bucket configuration details. Nested cos_config blocks have the following structure.|
| `cos_config.bucket`| String | Optional | The name of the {{site.data.keyword.cos_full_notm}} bucket that you want to use to back up the control plane data.|
| `cos_config.endpoint` | String | Optional | The {{site.data.keyword.cos_full_notm}} bucket endpoint.|
| `cos_config.region`| String | Optional | The name of a region, such as `us-south` or `eu-gb`.|
| `cos_credentials`| List | Optional | The {{site.data.keyword.cos_full_notm}} authorization keys. Nested `cos_credentials` blocks have the following structure.|
| `cos_credentials.access_key-id`| String | Required | The `HMAC` secret access key ID.|
| `cos_credentials.secret_access_key`| String | Optional | The `HMAC` secret access key.|
| `resource_group_id`| String | Optional | The ID of the resource group. You can retrieve the value from data source `ibm_resource_group`.|
| `zones`| Array of strings | Optional| The names for the host zones. For high availability, allocate your hosts across these three zones based on your infrastructure provider zones. For example, `us-east-1`, `us-east-2`, `us-east-3` .|
{: caption="Table 1. Available input parameters" caption-side="top"}

### Output parameters
{: #satellite-location-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id`|String| The unique identifier of the location. |
| `host_state`|String| Health status of the host.|
| `zone`|String| The zone within the cluster to assign the host to.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #satellite-location-import}

`ibm_satellite_location` can be imported by using the location ID or name.

**Syntax**

```
terraform import ibm_satellite_location.location location
```
{: codeblock}

**Example**

```
terraform import ibm_satellite_location.location satellite-location
```
{: codeblock}