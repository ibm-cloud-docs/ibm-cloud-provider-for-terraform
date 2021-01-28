---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider plugin, terraform cloud databases, terraform databases, terraform postgres, terraform mysql, terraform compose

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



# {{site.data.keyword.databases-for}} data sources 
{: #databases-data-sources}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_database`
{: #database}

Create a read-only copy of an existing {{site.data.keyword.cloud_notm}} database service. 
{: shortdesc}

Configuration of an {{site.data.keyword.databases-for}} `data_source` requires that the `region` parameter is set for the IBM provider in the `provider.tf`. The region must be the same as the `location` that the {{site.data.keyword.databases-for}} instance is deployed into. If not specified, `us-south` is used by default. A `terraform refresh` of the `data_source` fails if the region and the location differ.
{: note}

### Sample Terraform code
{: #database-sample}

The following example creates a read-only copy of the `mydatabase` instance in `us-east`.  
{: shortdesc}

```
data "ibm_database" "database" {
  name = "mydatabase"
  location = "us-east"
}
```

### Input parameters
{: #database-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`name`|String|Required|The name of the {{site.data.keyword.databases-for}} instance. IBM Cloud does not enforce that service names are unique and it is possible that duplicate service names exist. The first located service instance is used by Terraform. The name must not include spaces.|
| `resource_group_id`| String | Optional | The ID of the resource group where the {{site.data.keyword.databases-for}} instance is deployed into. The default is `default`. |
|`location` | String | Optional | The location where the {{site.data.keyword.databases-for}} instance is deployed into. |
|`service` | String | Optional| The service type of the instance. To retrieve this value, run `ibmcloud catalog service-marketplace` or `ibmcloud catalog search`.  |
{: caption="Table. Available input parameters" caption-side="top"}


### Output parameters
{: #database-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id`|String|The CRN of the {{site.data.keyword.databases-for}} instance.  |
|`guid`|String|The unique identifier of the {{site.data.keyword.databases-for}} instance.|
|`plan`|String| The service plan of the {{site.data.keyword.databases-for}} instance.|
|`location`|String| The location where the {{site.data.keyword.databases-for}} instance is deployed into. |
|`status`|String| The status of the {{site.data.keyword.databases-for}} instance. |
|`status`|String| The status of resource instance.|
|`adminuser`|String| The user ID of the default administration user for the database, such as `admin` or `root`. |
|`version`|String|The database version.|
|`platform_options.key_protect_key_id`| String | The CRN of key protect key. |
|`platform_options.disk_encryption_key_crn`| String | The CRN of disk encryption key. |
|`platform_options.backup_encryption_key_crn`| String | The CRN of backup encryption key. |
|`connectionstrings` |List| List of connection strings by userid for the database. For information about how to use connection strings, see the [documentation](/docs/databases-for-postgresql?topic=databases-for-postgresql-connection-strings). The results are returned in pairs of the userid and string: `connectionstrings.1.name = admin connectionstrings.1.string = postgres://admin:$PASSWORD@12345aa1-1111-1111-a1aa-a1aaa11aa1a1.a1a1a111a1a11a1a111a111a1a111a111.databases.appdomain.cloud:32554/ibmclouddb?sslmode=verify-full`|
|`cert_file_path`|String| The absolute path to certificate PEM file.|
|`auto_scaling`|List|Configure rules to allow your database to automatically increase its resources. Single block of autoscaling is allowed at once.|
|`auto_scaling.cpu`|List|Autoscaling CPU.|
|`auto_scaling.cpu.rate_increase_percent`|Integer|Auto scaling rate in increase percent.|
|`auto_scaling.cpu.rate_limit_count_per_member`|Integer|Auto scaling rate limit in count per number.|
|`auto_scaling.cpu.rate_period_seconds`|Integer|Auto scaling rate in period seconds.|
|`auto_scaling.cpu.rate_units`|String|Auto scaling rate in units.|
|`auto_scaling.disk`|List|Disk auto scaling.|
|`auto_scaling.disk.capacity_enabled`|Boolean|Auto scaling scalar enables or disables the scalar capacity.|
|`auto_scaling.disk.free_space_less_than_percent`|Integer|Auto scaling scalar capacity free space less than percent.|
|`auto_scaling.disk.io_above_percent`|Integer|Auto scaling scalar I/O utilization above percent.|
|`auto_scaling.disk.io_enabled`|Boolean|Auto scaling scalar I/O utilization enabled.|
|`auto_scaling.disk.io_over_period`|Boolean|Auto scaling scalar I/O utilization over period.|
|`auto_scaling.disk.rate_increase_percent`|Integer|Auto scaling rate increase percent.|
|`auto_scaling.disk.rate_limit_mb_per_member`|Integer|Auto scaling rate limit in megabytes per member.|
|`auto_scaling.disk.rate_period_seconds`|Integer|Auto scaling rate period in seconds.|
|`auto_scaling.disk.rate_units`|String|Auto scaling rate in units.|
|`auto_scaling.memory`|List|Memory Auto Scaling.|
|`auto_scaling.io_above_percent`|Integer|Auto scaling scalar I/O utilization above percent.|
|`auto_scaling.memory.io_enabled`|Boolean|Auto scaling scalar I/O utilization enabled.|
|`auto_scaling.memory.io_over_period`|String|Auto scaling scalar I/O utilization over period.|
|`auto_scaling.memory.rate_increase_percent`|Integer|Auto scaling rate in increase percent.|
|`auto_scaling.memory.rate_limit_mb_per_member`|Integer|Auto scaling rate limit in megabytes per member.|
|`auto_scaling.memory.rate_period_seconds`|Integer|Auto scaling rate period in seconds.|
|`auto_scaling.memory.rate_units`|String|Auto scaling rate in units.|
|`whitelist`|List| A list of allowed IP addresses or ranges.|
{: caption="Table 1. Available output parameters" caption-side="top"}

The provider only exports the admin user ID and associated connection string. It does not export any user IDs that are configured for the instance in addition. 
{: note}
