---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-18" 

keywords: terraform provider plugin, terraform resource group, terraform iam service, terraform resource management

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



# Resource management resources
{: #resource-mgmt-resources}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_resource_group`
{: #rg}

Create, update, or delete an IBM Cloud resource group. 
{: shortdesc}

### Sample Terraform code
{: #rg-sample}

```

resource "ibm_resource_group" "resourceGroup" {
  name     = "prod"
}

```
{: codeblock}

### Input parameters
{: #rg-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the resource group.|
|`quota_id`|String|Removed|The ID of the quota. You can refer to a quota by using the resource quota data source name.|
|`tags`|Array of string|Optional|Tags associated with the resource group instance. The tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #rg-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the new resource group.|
|`default`|Boolean|Specifies whether its default resource group or not.|
|`state`|String|State of the resource group.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #rg-import}

`ibm_resource_group` can be imported using resource group ID. The `ibm_resource_group.example` is the resource block name.

```
terraform import ibm_resource_group.example <resource_group_ID>
```
{: pre}



## `ibm_resource_instance`
{: #resource-instance}

Create, update, or delete an IAM-enabled service instance. 

### Sample Terraform code
{: #resource-instance-sample}

```
data "ibm_resource_group" "group" {
  name = "test"
}

resource "ibm_resource_instance" "resource_instance" {
  name              = "test"
  service           = "cloud-object-storage"
  plan              = "lite"
  location          = "global"
  resource_group_id = data.ibm_resource_group.group.id
  tags              = ["tag1", "tag2"]

  //User can increase timeouts
  timeouts {
    create = "15m"
    update = "15m"
    delete = "15m"
  }
}
```
{: codeblock}

### Input parameters
{: #resource-instance-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|Forces new resource|
|----|-----------|-----------|---------------------|------|
|`name`|String|Required|A descriptive name used to identify the resource instance.| No |
|`service`|String|Required|The name of the service offering. You can retrieve the value by installing the `catalogs-management` command line plug-in and running the `ibmcloud catalog service-marketplace` or `ibmcloud catalog search` command. For more information, about {{site.data.keyword.cloud_notm}} catalog service marketplace, refer [{{site.data.keyword.cloud_notm}} catalog service marketplace](/docs/cli?topic=cli-ibmcloud_catalog#ibmcloud_catalog_service_marketplace).| Yes |
|`plan`|String|Required|The name of the plan type supported by service. You can retrieve the value by running the `ibmcloud catalog service <servicename>` command.| No |
|`location`|String|Required|Target location or environment to create the resource instance.| Yes |
|`resource_group_id`|String|Optional|The ID of the resource group where you want to create the service. You can retrieve the value from data source `ibm_resource_group`. If not provided creates the service in default resource group.| Yes |
|`tags`|Array of string|Optional|Tags associated with the instance.| No |
|`parameters`|Map|Optional|Arbitrary parameters to create instance. The value must be a JSON object.| Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #resource-instance-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the new resource instance.|
|`guid`|String|The GUID of the resource instance.|
|`status`|String|The status of resource instance.|
|`extensions`|String|The extended metadata as a map associated with the resource instance.|
|`dashboard_url`|String|The dashboard URL of the new resource instance.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #resource-instance-timeout}

`ibm_resource_instance` provides the following timeouts:

|Name|Description|
|----|-----------|
|`create`|(Default 10 minutes) Used for Creating Instance.|
|`update`|(Default 10 minutes) Used for Updating Instance.|
|`delete`|(Default 10 minutes) Used for Deleting Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}



## `ibm_resource_key`
{: #resource-key}

Create, update, or delete service credentials for an IAM-enabled service. 
{: shortdesc}

By default, the `ibm_resource_key` resource creates service credentials that use the public service endpoint of a service. To create service credentials that use the private service endpoint instead, you must explicitly define that by using the `parameter` input parameter. Note that your service might not support private service endpoints yet. 
{: note}

### Sample Terraform code
{: #resource-key-sample}

#### Creating credentials for a resource without a service ID

```
data "ibm_resource_instance" "resource_instance" {
  name = "myobjectstorage"
}

resource "ibm_resource_key" "resourceKey" {
  name                 = "myobjectkey"
  role                 = "Viewer"
  resource_instance_id = data.ibm_resource_instance.resource_instance.id

  //User can increase timeouts
  timeouts {
    create = "15m"
    delete = "15m"
  }
}
```
{: codeblock}

The current `ibm_resource_key` resource does not support `service_id` argument. However, you can pass `service_id` as one of the parameter to create credentials for service ID.
{: note}

#### Creating credentials for a service ID

The `ibm_resource_instance` resource does not support creating service credentials for a service ID. However, you can pass in a service ID as an more parameter to create credentials for a service ID. 

```
data "ibm_resource_instance" "resource_instance" {
  name = "myobjectstorage"
}

resource "ibm_iam_service_id" "serviceID" {
  name        = "test"
  description = "New ServiceID"
}

resource "ibm_resource_key" "resourceKey" {
  name                 = "myobjectkey"
  role                 = "Viewer"
  resource_instance_id = data.ibm_resource_instance.resource_instance.id
  parameters = {
    serviceid_crn = ibm_iam_service_id.serviceID.crn
  }

  //User can increase timeouts
  timeouts {
    create = "15m"
    delete = "15m"
  }
}
```
{: codeblock}

#### Creating credentials that use the private service endpoint
{: #resource-key-sample-private}

The following example shows how you can create a Databases for etcd service instance with service credentials that use the private service endpoint. 
{: shortdesc}

```
data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_database" "database" {
  name              = "tfdb"
  plan              = "standard"
  location          = "us-south"
  resource_group_id = data.ibm_resource_group.group.id

  service = "databases-for-postgresql"
  version = 11

  service_endpoints            = "private"
  adminpassword                = "adminpassword"
  members_memory_allocation_mb = 3072
  members_disk_allocation_mb   = 61440

}

resource "ibm_resource_key" "resourceKey" {
  name                 = "tfkey"
  role                 = "Viewer"
  resource_instance_id = ibm_database.database.id
  
  parameters = {

     service-endpoints =  "private"
  
  }
}

```
{: codeblock}

#### Sample code by using HMAC
{: #sample-code-hmac}

```
data "ibm_resource_group" "group" {
    name ="Default"
}
resource "ibm_resource_instance" "resource_instance" {
  name              = "test-21"
  service           = "cloud-object-storage"
  plan              = "lite"
  location          = "global"
  resource_group_id = data.ibm_resource_group.group.id
  tags              = ["tag1", "tag2"]
  
  //User can increase timeouts
  timeouts {
    create = "15m"
    update = "15m"
    delete = "15m"
  }
}
resource "ibm_resource_key" "resourceKey" {
  name                 = "my-cos-bucket-xx-key"
  resource_instance_id = ibm_resource_instance.resource_instance.id
  parameters           = { "HMAC" = true }
  role                 = "Manager"
}
```
{: codeblock}


### Input parameters
{: #resource-key-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------|----------|
|`name`|String|Required| A descriptive name used to identify a resource key.| Yes |
|`role`|String|Required|The name of the user role. Valid roles are `Writer`, `Reader`, `Manager`, `Administrator`, `Operator`, `Viewer`, and `Editor`.| Yes |
|`parameters`|Map|Optional|Arbitrary parameters to pass to the resource in JSON format. If you want to create service credentials by using the private service endpoint, include the `service-endpoints =  "private"` parameter. | Yes |
|`resource_instance_id`|String|Optional|The ID of the resource instance associated with the resource key. **NOTE**: Conflicts with `resource_alias_id`.| Yes |
|`resource_alias_id`|String|Optional|The ID of the resource alias associated with the resource key. **NOTE**: Conflicts with `resource_instance_id`.| Yes |
|`tags`|Array of string|Optional|Tags associated with the resource key instance. Tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #resource-key-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the new resource key.|
|`credentials`|String|The credentials associated with the key.|
|`status`|String|Status of resource key.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #resource-key-timeout}

`ibm_resource_key` provides the following timeouts:

|Name|Description|
|----|-----------|
|`create`|(Default 10 minutes) Used for Creating Key.|
|`delete`|(Default 10 minutes) Used for Deleting Key.|
{: caption="Table. Available timeout configuration options" caption-side="top"}

