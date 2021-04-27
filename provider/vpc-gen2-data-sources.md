---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-27"

keywords: terraform provider plugin, terraform gen 2, terraform gen 2 compute

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



# VPC infrastructure data sources 
{: #vpc-gen2-data-sources}

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}.
{: note}


## `ibm_is_dedicated_host`
{: #dedicated-host-ds}

Retrieve the dedicated host data sources. For more information, about dedicated host in your {{site.data.keyword.cloud_notm}} VPC, see [Dedicated hosts](/docs/vpc?topic=vpc-creating-dedicated-hosts-instances).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dedicated-host-dssample}

The following example retrieves information about the dedicated host data sources.
{: shortdesc}

```
data "ibm_is_dedicated_host" "is_dedicated_host" {
	host_group = "1e09281b-f177-46fb-baf1-bc152b2e391a"
	name = "my-dedicated-host"
}
```
{: codeblock}

### Input parameters
{: #dedicated-host-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`host_group`|String|Required| The unique identifier of the dedicated host group.|
|`name`|String|Required| The unique name of this dedicated host.|
|`resource_group`|String|Optional| The unique identifier of the resource group.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dedicated-host-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`| String | The unique identifier of the dedicated host.|
|`available_memory`| String | The amount of memory in `GB` that is currently available for instances.|
|`available_vcpu`| String | The available `VCPU` for the dedicated host. Nested `available_vcpu` blocks have the following structure.|
|`available_vcpu.architecture`| String | The `VCPU` architecture.|
|`available_vcpu.count`| String | The number of `VCPUs` assigned.|
|`created_at`| String | The date and time that the dedicated host was created.|
|`crn`| String | The CRN for this dedicated host.|
|`host_group`| String | The unique identifier of the dedicated host group this dedicated host is in.|
|`href`| String | The URL for this dedicated host.|
|`instance_placement_enabled`| String | If set to `true`, instances can be placed on this dedicated host.|
|`instances`| String | Array of instances that are allocated to this dedicated host. Nested instances blocks have the following structure.|
|`instances.crn`| String | The CRN for this virtual server instance.|
|`instances.deleted`| String | If present, this property indicates the referenced resource has been deleted and provides supplementary information. Nested deleted blocks have the following structure.|
|`instances.more_info`| String | Link to documentation about deleted resources.
|`instances.href`| String | The URL for this virtual server instance.|
|`instances.id`| String | The unique identifier for this virtual server instance.
|`instances.name`| String | The user defined name for this virtual server instance (and default system hostname).|
|`lifecycle_state`| String | The lifecycle state of the dedicated host resource.|
|`memory`| String | The total amount of memory in `GB`` for this host.|
|`name`| String | The unique user defined name for this dedicated host. If unspecified, the name will be a hyphenated list of randomly-selected words.|
|`profile`| String | The profile this dedicated host uses. Nested profile blocks have the following structure.|
|`profile.href`| String | The URL for this dedicated host.|
|`profile.name`| String | The globally unique name for this dedicated host profile.|
|`provisionable`| String | Indicates whether this dedicated host is available for instance creation.|
|`resource_group`| String | The unique identifier of the resource group.|
|`resource_type`| String | The type of resource referenced.|
|`socket_count`| String | The total number of sockets for this host.|
|`state`| String | The administrative state of the dedicated host.|
|`supported_instance_profiles`| String | Array of instance profiles that can be used by instances placed on this dedicated host. Nested **supported_instance_profiles** blocks have the following structure.|
|`supported_instance_profiles.href`| String | The URL for this virtual server instance profile.|
|`supported_instance_profiles.name`| String | The globally unique name for this virtual server instance profile.|
|`vcpu`| String | The total `VCPU` of the dedicated host. Nested `VCPU` blocks have the following structure.|
|`vcpu.architecture`| String | The `VCPU` architecture.|
|`vcpu.count`| String | The number of `VCPUs` assigned.|
|`zone`| String | The globally unique name of the zone this dedicated host resides in.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_dedicated_hosts`
{: #dedicated-hosts-ds}

Retrieve the dedicated host collection. For more information, about dedicated host in your {{site.data.keyword.cloud_notm}} VPC, see [Dedicated hosts](/docs/vpc?topic=vpc-creating-dedicated-hosts-instances).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dedicated-hosts-dssample}

The following example retrieves information about the dedicated host data sources.
{: shortdesc}

```
data "ibm_is_dedicated_hosts" "is_dedicated_hosts" {
	host_group = "1e09281b-f177-46fb-baf1-bc152b2e391a"
}
```
{: codeblock}

### Input parameters
{: #dedicated-hosts-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`host_group`|String|Optional| The unique identifier of the dedicated host group.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dedicated-hosts-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`| String | The unique identifier of the dedicated host collection.|
|`dedicated_hosts`| String | Collection of dedicated hosts. Nested dedicated_hosts blocks have the following structure.|
|`dedicated_hosts.available_memory`| String | The amount of memory in GB that is currently available for instances.|
|`dedicated_hosts.available_vcpu`| String | The available `VCPU` for the dedicated host. Nested available_vcpu blocks have the following structure.|
|`dedicated_hosts.available_vcpu.architecture`| String | The `VCPU` architecture.|
|`dedicated_hosts.available_vcpu.count`| String | The number of `VCPUs` assigned.|
|`dedicated_hosts.created_at`| String | The date and time that the dedicated host was created.|
|`dedicated_hosts.crn`| String | The CRN for this dedicated host.|
|`dedicated_hosts.host_group`| String | The unique identifier of the dedicated host group this dedicated host is in.|
|`dedicated_hosts.href`| String | The URL for this dedicated host.|
|`dedicated_hosts.id`| String | The unique identifier for this dedicated host.|
|`dedicated_hosts.instance_placement_enabled`| String | If set to `true`, instances can be placed on this dedicated host.|
|`dedicated_hosts.instances`| String | Array of instances that are allocated to this dedicated host. Nested instances blocks have the following structure.|
|`dedicated_hosts.instances.crn`| String | The CRN for this virtual server instance.|
|`dedicated_hosts.instances.deleted`| String | If present, this property indicates the referenced resource has been deleted and provides some supplementary information. Nested deleted blocks have the following structure.|
|`dedicated_hosts.instances.deleted.more_info`| String | Link to documentation about deleted resources.|
|`dedicated_hosts.instances.href`| String | The URL for this virtual server instance.|
|`dedicated_hosts.instances.id`| String | The unique identifier for this virtual server instance.|
|`dedicated_hosts.instances.name`| String | The user-defined name for this virtual server instance (and default system hostname).|
|`dedicated_hosts.lifecycle_state`| String | The lifecycle state of the dedicated host resource.|
|`dedicated_hosts.memory`| String | The total amount of memory in GB for this host.|
|`dedicated_hosts.name`| String | The unique user defined name for this dedicated host. If unspecified, the name will be a hyphenated list of randomly-selected words.|
|`dedicated_hosts.profile`| String | The profile this dedicated host uses. Nested profile blocks have the following structure.|
|`dedicated_hosts.profile.href`| String | The URL for this dedicated host.|
|`dedicated_hosts.profile.name`| String | The globally unique name for this dedicated host profile.|
|`dedicated_hosts.provisionable`| String | Indicates whether this dedicated host is available for instance creation.|
|`dedicated_hosts.resource_group`| String | The resource group for this dedicated host. Nested resource group blocks have the following structure.|
|`dedicated_hosts.resource_group.href`| String | The URL for this resource group.|
|`dedicated_hosts.resource_group.id`| String | The unique identifier for this resource group.|
|`dedicated_hosts.resource_group.name`| String | The user defined name for this resource group.|
|`dedicated_hosts.resource_type`| String | The type of resource referenced.|
|`dedicated_hosts.socket_count`| String | The total number of sockets for this host.|
|`dedicated_hosts.state`| String | The administrative state of the dedicated host. The enumerated values for this property are expected to expand in the future. When processing this property, check for and log unknown values. Optionally, halt processing and surface the error, or bypass the dedicated host on which the unexpected property value was encountered.|
|`dedicated_hosts.supported_instance_profiles`| String | Array of instance profiles that can be used by instances placed on this dedicated host. Nested supported_instance_profiles blocks have the following structure.|
|`dedicated_hosts.supported_instance_profiles.href`| String | The URL for this virtual server instance profile.|
|`dedicated_hosts.supported_instance_profiles.name`| String | The globally unique name for this virtual server instance profile.
|`dedicated_hosts.vcpu`| String | The total `VCPU` of the dedicated host. Nested `VCPU` blocks have the following structure.|
|`dedicated_hosts.vcpu.architecture`| String | The `VCPU` architecture.|
|`dedicated_hosts.vcpu.count`| String | The number of `VCPUs` assigned.|
|`dedicated_hosts.zone`| String | The globally unique name of the zone this dedicated host resides in.|
|`total_count`| String | The total number of resources across all pages.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_dedicated_host_group`
{: #dedicated-host-grp-ds}

Retrieve the dedicated host group data sources. For more information, about dedicated host group in your {{site.data.keyword.cloud_notm}} VPC, see [Dedicated hosts groups](/docs/vpc?topic=vpc-creating-dedicated-hosts-instances).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dedicated-host-grp-dssample}

The following example retrieves information about the dedicated host data sources.
{: shortdesc}

```
data "ibm_is_dedicated_host_group" "is_dedicated_host_group" {
	name = "my-host-group"
}
```
{: codeblock}

### Input parameters
{: #dedicated-host-grp-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required| The unique user defined name of this dedicated host group.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dedicated-host-grp-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`| String | The unique identifier of the dedicated host group.|
|`class`| String | The dedicated host profile class for hosts in this group.|
|`created_at`| String | The date and time that the dedicated host group was created.|
|`crn`| String | The CRN for this dedicated host group.|
|`dedicated_hosts`| String | The dedicated hosts that are in this dedicated host group. Nested dedicated_hosts blocks have the following structure.|
|`dedicated_hosts.crn`| String | The CRN for this dedicated host.|
|`dedicated_hosts.deleted`| String | If present, this property indicates the referenced resource has been deleted and provides supplementary information. Nested deleted blocks have the following structure.|
|`dedicated_hosts.deleted.more_info`| String | Link to documentation about deleted resources.|
|`dedicated_hosts.href`| String | The URL for this dedicated host.|
|`dedicated_hosts.id`| String | The unique identifier for this dedicated host.|
|`dedicated_hosts.name`| String | The unique user-defined name for this dedicated host. If unspecified, the name will be a hyphenated list of randomly-selected words.|
|`dedicated_hosts.resource_type`| String | The type of resource referenced.|
|`family`| String | The dedicated host profile family for hosts in this group.|
|`href`| String | The URL for this dedicated host group.|
|`resource_group`| String | The unique identifier of the resource group for this dedicated host.|
|`resource_type`| String | The type of resource referenced.|
|`supported_instance_profiles`| String | Array of instance profiles that can be used by instances placed on this dedicated host group. Nested **supported_instance_profiles** blocks have the following structure.|
|`supported_instance_profiles.href`| String | The URL for this virtual server instance profile.|
|`supported_instance_profiles.name`| String | The unique name for this virtual server instance profile.|
|`zone`| String | The zone this dedicated host group resides in.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_dedicated_host_groups`
{: #dedicated-host-grps-ds}

Retrieve the dedicated host groups collection. For more information, about dedicated host groups in your {{site.data.keyword.cloud_notm}} VPC, see [Dedicated hosts groups](/docs/vpc?topic=vpc-creating-dedicated-hosts-instances).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dedicated-host-grps-dssample}

The following example retrieves information about the dedicated host data sources.
{: shortdesc}

```
data "ibm_is_dedicated_host_groups" "is_dedicated_host_groups" {
}
}
```
{: codeblock}

### Input parameters
{: #dedicated-host-grps-dsinput}

The input parameter is not supported for this data source.
{: shortdesc}

### Output parameters
{: #dedicated-host-grps-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`| String | The unique identifier of the dedicated host group collection.|
|`host_groups`| String | Collection of dedicated host groups. Nested groups blocks have the following structure.|
|`host_groups.class`| String | The dedicated host profile class for hosts in this group.|
|`host_groups.created_at`| String | The date and time that the dedicated host group was created.|
|`host_groups.crn`| String | The CRN for this dedicated host group.|
|`host_groups.dedicated_hosts`| String | The dedicated hosts that are in this dedicated host group. Nested dedicated_hosts blocks have the following structure.|
|`host_groups.dedicated_hosts.crn`| String | The CRN for this dedicated host.|
|`host_groups.dedicated_hosts.deleted`| String | If present, this property indicates the referenced resource has been deleted and provides supplementary information. Nested deleted blocks have the following structure.|
|`host_groups.dedicated_hosts.deleted.more_info`| String | Link to documentation about deleted resources.|
|`host_groups.dedicated_hosts.href`| String | The URL for this dedicated host.|
|`host_groups.dedicated_hosts.id`| String | The unique identifier for this dedicated host.|
|`host_groups.dedicated_hosts.name`| String | The unique user defined name for this dedicated host. If unspecified, the name will be a hyphenated list of randomly-selected words.|
|`host_groups.dedicated_hosts.resource_type`| String | The type of resource referenced.|
|`family`| String | The dedicated host profile family for hosts in this group.|
|`href`| String | The URL for this dedicated host group.|
|`id` | String | The unique identifier for this dedicated host group.
|`name`| String | The unique user defined name for this dedicated host group. If unspecified, the name will be a hyphenated list of randomly-selected words.
|`resource_group`| String | The unique identifier of the resource group for this dedicated host.|
|`resource_type`| String | The type of resource referenced.|
|`supported_instance_profiles`| String | Array of instance profiles that can be used by instances placed on this dedicated host group. Nested **supported_instance_profiles** blocks have the following structure.|
|`supported_instance_profiles.href`| String | The URL for this virtual server instance profile.|
|`supported_instance_profiles.name`| String | The unique name for this virtual server instance profile.|
|`zone`| String | The zone this dedicated host group resides in.|
|`total_count`| String | The total number of resources across all pages.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_is_dedicated_host_profile`
{: #dedicated-host-profile-ds}

Retrieve the dedicated host profile. For more information, about dedicated host groups in your {{site.data.keyword.cloud_notm}} VPC, see [Dedicated host profiles](/docs/vpc?topic=vpc-dh-profiles).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dedicated-host-profile-dssample}

The following example retrieves information about the dedicated host data sources.
{: shortdesc}

```
data "ibm_is_dedicated_host_profile" "is_dedicated_host_profile" {
	name = "dh2-56x464"
}
```
{: codeblock}

### Input parameters
{: #dedicated-host-profile-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required| The globally unique user defined name for this `VSI` profile.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dedicated-host-profile-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`| String | The unique identifier of the dedicated host profile.|
|`class`| String | The product class this dedicated host profile belongs to.|
|`family`| String | The product family this dedicated host profile belongs to.|
|`href`| String | The URL for this dedicated host.|
|`memory`| String | Nested memory blocks have the following structure.|
|`memory.type`| String | The type for this profile field.|
|`memory.value`| String | The value for this profile field.|
|`memory.default`| String | The default value for this profile field.|
|`memory.max`| String | The maximum value for this profile field.|
|`memory.min`| String | The minimum value for this profile field.|
|`memory.step`| String | The increment step value for this profile field.|
|`memory.values`| String | The permitted values for this profile field.|
|`socket_count` | String | Nested socket_count blocks have the following structure.|
|`socket_count.type`| String | The type for this profile field.|
|`socket_count.value`| String | The value for this profile field.|
|`socket_count.default`| String | The default value for this profile field.|
|`socket_count.max`| String | The maximum value for this profile field.|
|`socket_count.min`| String | The minimum value for this profile field.|
|`socket_count.step`| String | The increment step value for this profile field.|
|`socket_count.values`| String | The permitted values for this profile field.|
|`supported_instance_profiles`| String | Array of instance profiles that can be used by instances placed on dedicated hosts with this profile Nested `supported_instance_profiles` blocks have the following structure.|
|`supported_instance_profiles.href`| String | The URL for this virtual server instance profile.|
|`supported_instance_profiles.name`| String | The globally unique name for this virtual server instance profile.|
|`vcpu_architecture`| String | Nested `vcpu_architecture` blocks have the following structure.|
|`vcpu_architecture.type`| String | The type for this profile field.
|`vcpu_architecture.value`| String | The `VCPU` architecture for a dedicated host with this profile.|
|`vcpu_count` |String | Nested `vcpu_count` blocks have the following structure.|
|`vcpu_count.type`| String | The type for this profile field.|
|`vcpu_count.value`| String | The value for this profile field.|
|`vcpu_count.default`| String | The default value for this profile field.|
|`vcpu_count.max`| String | The maximum value for this profile field.|
|`vcpu_count.min`| String | The minimum value for this profile field.|
|`vcpu_count.step`| String | The increment step value for this profile field.|
|`vcpu_count.values`| String | The permitted values for this profile field.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_floating_ip`
{: #floating-ip-g2-ds}

Retrieve the information about `VPC` floating IP. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #floating-ip-g2-dssample}

The following example retrieves information about the `VPC` floating IP.
{: shortdesc}

```

 data "ibm_is_floating_ip" "test" {
      name   = "test-fp"
 }

```
{: codeblock}

### Input parameters
{: #floating-ip-g2-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the floating IP.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #floating-ip-g2-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`|String|The unique identifier of the floating IP.|
|`address`|String|The floating IP address that is created.|
|`status`|String|Provisioning status of the floating IP address.|
|`tags`|String|The tags associated with VPC.|
|`target`|String|The ID of the network interface used to allocate the floating IP address.|
|`zone`|String|The zone name where to create the floating IP address.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_flow_logs`
{: #ibm-is-flow-logs}

Import the details of an existing {{site.data.keyword.cloud_notm}} infrastructure flow logs as a read only data source.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ibm-is-flowlogs-sample}


```
data "ibm_is_flow_logs" "ds_flow_logs" {
}

```
{: codeblock}

### Input parameters
{: #ibm-is-flowlogs-dsinput}

There is no input parameters.
{: shortdesc}


### Output parameters
{: #ibm-is-flowlogs-dsoutput}

Review the output parameters that you can access after you retrieve your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `flow_log_collectors` | String | Lists all the flow logs in the {{site.data.keyword.cloud_notm}}. |
| `flow_log_collectors.active` | String | Indicates whether the collector is active. |
| `flow_log_collectors.created_at` | String | The date and time the flow log created. |
| `flow_log_collectors.crn` | String | The CRN of the flow log collector. |
| `flow_log_collectors.href` | String | The URL of the flow log collector. |
| `flow_log_collectors.id` | String | The unique identifier of the flow log collector. |
| `flow_log_collectors.lifecycle_state` | String | The lifecycle state of the flow log collector. |
| `flow_log_collectors.name` | String | The flow log collector name. |
| `flow_log_collectors.resource_group` | String | The resource group of the flow log. |
| `flow_log_collectors.storage_bucket` | String | The {{site.data.keyword.cos_full_notm}} bucket name where the flow logs are logged. |
| `flow_log_collectors.target` | String | The target ID that the flow log collector collects the flow logs. |
| `flow_log_collectors.vpc` | String | The VPC of the flow log collector that are associated. |

## `ibm_is_image`
{: #vpc-image}

Retrieve information about a virtual server image for Gen 2 compute. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-image-sample}

The following example retrieves information about the `centos-7.x-amd64` image. 
{: shortdesc}

```

data "ibm_is_image" "ds_image" {
    name = "centos-7.x-amd64"
}

```
{: codeblock}

### Input parameters
{: #vpc-image-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the image.|
|`visibility`|String|Optional|The visibility of the image. Accepted values are `public` or `private`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-image-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`architecture`|String|The architecture of the image.|
|`checksum`| String| The `SHA256` checksum of the image.|
|`crn`|String|The CRN for this image.|
|`id`|String|The unique identifier of the image.|
|`os`|String|The name of the operating system.|
|`status`|String|The status of this image.|
|`encryption`|String|The type of encryption used of the image.|
|`encryption_key`| String|The CRN of the Key Protect or Hyper Protect Crypto Service root key for this resource.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_images`
{: #vpc-images}

Retrieve information about Gen 2 virtual server images. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-images-sample}

```

data "ibm_is_images" "ds_images" {
}

```
{: codeblock}

### Input parameters
{ #vpc-images-input}

No input parameters are required for this data source.
{: shortdesc}

### Output parameters
{ #vpc-images-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`images`|List of objects|List of all supported images.  |
|`images.architecture`|String|The architecture for this image.  |
|`images.crn`|String|The CRN for this image.  |
|`images.checksum`| String | The `SHA256` checksum of the image.|
|`images.encryption`|String|The type of encryption used of the image.|
|`images.encryption_key`| String|The CRN of the Key Protect or Hyper Protect Crypto Service root key for this resource.|
|`images.id`|String|The unique identifier for this image.  |
|`images.os`|String|The name of the operating system.  |
|`images.name`|String|The name for this image.  |
|`images.status`|String|The status of this image.  |
|`images.visibility`|String|The visibility of the image public or private.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_is_instance`
{: #instance}

Retrieve the details for a Gen 2 {{site.data.keyword.vsi_is_short}} instance.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #instance-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "testvpc"
}

resource "ibm_is_subnet" "testacc_subnet" {
  name            = "testsubnet"
  vpc             = ibm_is_vpc.testacc_vpc.id
  zone            = "us-south-1"
  ipv4_cidr_block = "10.240.0.0/24"
}

resource "ibm_is_ssh_key" "testacc_sshkey" {
  name       = "testssh"
  public_key = file("~/.ssh/id_rsa.pub")
}

resource "ibm_is_instance" "testacc_instance" {
  name    = "testinstance"
  image   = "a7a0626c-f97e-4180-afbe-0331ec62f32a"
  profile = "bc1-2x8"

  primary_network_interface {
    subnet = ibm_is_subnet.testacc_subnet.id
  }

  network_interfaces {
    name   = "eth1"
    subnet = ibm_is_subnet.testacc_subnet.id
  }

  vpc  = ibm_is_vpc.testacc_vpc.id
  zone = "us-south-1"
  keys = [ibm_is_ssh_key.testacc_sshkey.id]
}

data "ibm_is_instance" "ds_instance" {
  name        = "${ibm_is_instance.testacc_instance.name}"
  private_key = file("~/.ssh/id_rsa")
  passphrase  = ""
}
```
{: codeblock}

### Input parameters
{: #instance-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`name`|String|Required|The name of the {{site.data.keyword.vsi_is_short}} instance that you want to retrieve. |
|`private_key`|String|Optional|The private key of an SSH key that you want to add to your {{site.data.keyword.vsi_is_short}} instance during creation in PEM format. It is used to decrypt the default password of the Windows administrator for the virtual server instance if the image is used of type `windows`.|
|`passphrase`|String|Optional|The passphrase that you used when you created your SSH key. If you did not enter a passphrase when you created the SSH key, do not provide this input parameter.|

### Output parameters
{: #instance-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID that was assigned to the {{site.data.keyword.vsi_is_short}} instance.|
|`memory`|Integer|The amount of memory that was allocated to the instance.|
|`status`|String|The status of the instance.|
|`image`|String|The ID of the virtual server image that is used in the instance.|
|`zone`|String|The zone where the instance was created.|
|`vpc`|String|The ID of the VPC that the instance belongs to.|
|`resource_group`|String|The name of the resource group where the instance was created.|
|`vcpu`|Object|A list of virtual CPUs that were allocated to the instance.|
|`vcpu.architecture`|String|The architecture of the virtual CPU. |
|`vcpu.count`|Integer|The number of virtual CPUs that are allocated to the instance.|
|`gpu`|Object|A list of graphics processing units that are allocated to the instance.|
|`gpu.cores`|Integer|The number of cores that are assigned to the GPU.|
|`gpu.count`|Integer|The number of GPUs that are allocated to the instance.|
|`gpu.manufacture`|String|The manufacturer of the GPU.|
|`gpu.memory`|Integer|The amount of memory that was allocated to the GPU.|
|`gpu.model`|String|The model of the GPU.| 
|`primary_network_interface`|Object|A list of primary network interfaces that were created for the instance.| 
|`primary_network_interface.id`|String|The ID of the primary network interface.|
|`primary_network_interface.name`|String|The name of the primary network interface.|
|`primary_network_interface.subnet`|String|The ID of the subnet that is used in the primary network interface.|
|`primary_network_interface.security_groups`|List|A list of security groups that were created for the interface.|
|`primary_network_interface.primary_ipv4_address`|String|The IPv4 address range that the subnet uses.|
|`network_interfaces`|Object|A list of more network interfaces that the instance uses.|
|`network_interfaces.id`|String|The ID of the more network interface.|
|`network_interfaces.name`|String|The name of the more network interface.|
|`network_interfaces.subnet`|String|The ID of the subnet that is used in the more network interface.|
|`network_interfaces.security_groups`|List|A list of security groups that were created for the interface.|
|`network_interfaces.primary_ipv4_address`|String|The IPv4 address range that the subnet uses.|
|`boot_volume`|Object|A list of boot volumes that were created for the instance.|
|`boot_volume.id`|String|The ID of the boot volume attachment.|
|`boot_volume.name`|String|The name of the boot volume.|
|`boot_volume.device`|String|The name of the device that is associated with the boot volume.|
|`boot_volume.volume_id`|String|The ID of the volume that is associated with the boot volume attachment.|
|`boot_volume.volume_crn`|String|The CRN of the volume that is associated with the boot volume attachment.|
|`volume_attachments`|Object|A list of volume attachments that were created for the instance.| 
|`volume_attachments.id`|String|The ID of the volume attachment.|
|`volume_attachments.name`|String|The name of the volume attachment.|
|`volume_attachments.volume_id`|String|The ID of the volume that is associated with the volume attachment.|
|`volume_attachments.volume_name`|String|The name of the volume that is associated with the volume attachment.|
|`volume_attachments.crn`|String|The CRN of the volume that is associated with the volume attachment.|
|`resource_controller_url`|String|The URL of the {{site.data.keyword.cloud_notm}} dashboard that you can use to see details for your instance.| 
|`password`|String|The password that you can use to access your instance.|
|`keys`|Object|A list of SSH keys that were added to the instance during creation.|
|`keys.id`|String|The ID of the SSH key.|
|`keys.name`|String|The name of the SSH key that you entered when you uploaded the key to {{site.data.keyword.cloud_notm}}.|


## `ibm_is_instances`
{: #instances}

Retrieve the details for all Gen 2 {{site.data.keyword.vsi_is_short}} instances in your account.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #instances-sample}

```
data "ibm_is_instances" "ds_instances" {
}

data "ibm_is_instances" "ds_instances1" {
  vpc_name = "testacc_vpc"
}
```
{: codeblock}

### Input parameters
{: #instances-input}

The input parameters that you need to specify for the data source. 
{: shortdesc}

| Input parameter | Data type |Required / optional | Description |
| ------------- |-------------| --------------|-------------- |
|`vpc_name`|String|Optional|The name of the VPC to filter the instances attached.|
|`vpc`|String|Optional|The VPC ID to filter the instances attached.|

### Output parameters
{: #instances-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`instances`|Object|A list of {{site.data.keyword.vsi_is_short}} instances that exist in your account.|
|`instances.id`|String|The ID that was assigned to the {{site.data.keyword.vsi_is_short}} instance.|
|`instances.memory`|Integer|The amount of memory that was allocated to the instance.|
|`instances.status`|String|The status of the instance.|
|`instances.image`|String|The ID of the virtual server image that is used in the instance.|
|`instances.zone`|String|The zone where the instance was created.|
|`instances.vpc`|String|The ID of the VPC that the instance belongs to.|
|`instances.resource_group`|String|The name of the resource group where the instance was created.|
|`instances.vcpu`|Object|A list of virtual CPUs that were allocated to the instance.|
|`instances.vcpu.architecture`|String|The architecture of the virtual CPU. |
|`instances.vcpu.count`|Integer|The number of virtual CPUs that are allocated to the instance.|
|`instances.primary_network_interface`|Object|A list of primary network interfaces that were created for the instance.| 
|`instances.primary_network_interface.id`|String|The ID of the primary network interface.|
|`instances.primary_network_interface.name`|String|The name of the primary network interface.|
|`instances.primary_network_interface.subnet`|String|The ID of the subnet that is used in the primary network interface.|
|`instances.primary_network_interface.security_groups`|List|A list of security groups that were created for the interface.|
|`instances.primary_network_interface.primary_ipv4_address`|String|The IPv4 address range that the subnet uses.|
|`instances.network_interfaces`|Object|A list of more network interfaces that the instance uses.|
|`instances.network_interfaces.id`|String|The ID of the more network interface.|
|`instances.network_interfaces.name`|String|The name of the more network interface.|
|`instances.network_interfaces.subnet`|String|The ID of the subnet that is used in the more network interface.|
|`instances.network_interfaces.security_groups`|List|A list of security groups that were created for the interface.|
|`instances.network_interfaces.primary_ipv4_address`|String|The IPv4 address range that the subnet uses.|
|`instances.boot_volume`|Object|A list of boot volumes that were created for the instance.|
|`instances.boot_volume.id`|String|The ID of the boot volume attachment.|
|`instances.boot_volume.name`|String|The name of the boot volume.|
|`instances.boot_volume.device`|String|The name of the device that is associated with the boot volume.|
|`instances.boot_volume.volume_id`|String|The ID of the volume that is associated with the boot volume attachment.|
|`instances.boot_volume.volume_crn`|String|The CRN of the volume that is associated with the boot volume attachment.|
|`instances.volume_attachments`|Object|A list of volume attachments that were created for the instance.| 
|`instances.volume_attachments.id`|String|The ID of the volume attachment.|
|`instances.volume_attachments.name`|String|The name of the volume attachment.|
|`instances.volume_attachments.volume_id`|String|The ID of the volume that is associated with the volume attachment.|
|`instances.volume_attachments.volume_name`|String|The name of the volume that is associated with the volume attachment.|
|`instances.volume_attachments.crn`|String|The CRN of the volume that is associated with the volume attachment.|


## `ibm_is_instance_group`
{: #instance-group}

Retrieve the details for all Gen 2 {{site.data.keyword.vsi_is_short}} instance group in your account.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #instance-group-sample}

```
data "ibm_is_instance_group" "instance_group_data" {
	name =  ibm_is_instance_group.instance_group.name
}
```
{: codeblock}

### Input parameters
{: #instance-group-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of an instance group.|


### Output parameters
{: #instance-group-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|Object|The ID of an instance group. |
| `managers` | String | List of managers associated with the instance group.|
| `vpc` | String | The VPC ID. |
| `status` | String | The status of an instance group. |
| `instance_template` | String |The ID of an instance template to create an instance group. |
| `instance_count` | String | The number of instances created in an instance group. |
| `resource_group`| String | The resource group ID. |
| `subnets`| String | The list of subnet IDs used by an instances. |
| `application_port` | String | Scales an instances to supply the port for the Load Balancer pool member. |
| `load_balancer_pool` | String | The Load Balancer pool ID.|


## `ibm_is_instance_group_managers`
{: #instance-group-managers}

Retrieve all the instance group managers information of an instance group.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #instance-group-managers-sample}

In the following example, you can retrieve a list of instance group managers information.

```
data "ibm_is_instance_group_managers" "instance_group_managers" {
    instance_group = "r006-76740f94-fcc4-11e9-96e7-a77723715315"
}
```
{: codeblock}

### Input parameters
{: #instance-group-managers-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`instance_group`|String|Required|The instance group ID where the instance group manager is created.|

### Output parameters
{: #instance-group-managers-dsoutput}

Review the output parameters that you can access after you retrieved your data source.
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `instance_group_managers` | List of string | Nested block with list of instance manager properties. |
|`instance_group_managers.id`|Object|This ID is the combination of instance group ID, and instance group manager ID. |
|`instance_group_managers.manager_type`|String| The type of an instance group manager. |
|`instance_group_managers.aggregation_window`|String|The time window in seconds to aggregate metrics prior to evaluation. |
|`instance_group_managers.manager_id`|String|The instance group manager ID. |
|`instance_group_managers.policies`|String|List of policies associated with the instance group manager. |
|`instance_group_managers.cooldown`|The duration of time in seconds to pause further scale actions after scaling has taken place. |
|`instance_group_managers.max_membership_count`|String|The maximum number of members in a managed instance group. |
|`instance_group_managers.min_membership_count`|String|The minimum number of members in a managed instance group. |

## `ibm_is_instance_group_manager_policy`
{: #instance-group-managerpolicy}

Retrieve the policy information of an instance group manager.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #instance-group-manager-policy-sample}

In the following example, you can retrieve a policy information of an instance group manager.

```
data "ibm_is_instance_group_manager_policy" "instance_group_manager_policy" {
  instance_group = "r006-76770f94-f7654-11e9-96e7-a77724435315"
  instance_group_manager = "r006-76770f94-f8764-11e9-96e7-a77726534315"
	name = "testpolicy
}
```
{: codeblock}

### Input parameters
{: #instance-group-manager-policy-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the policy.|
|`instance_group`|String|Required|The instance group ID.|
|`instance_group_manager`|String|Required|The instance group manager ID|


### Output parameters
{: #instance-group-manager-policy-dsoutput}

Review the output parameters that you can access after you retrieved your data source.
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|Object|This ID is the combination of instance group ID, instance group manager ID and instance group manager policy ID. |
| `policy_type` | String | The type of metric to evaluate. |
| `metric_type` | String | The type of metric to evaluate. The possible values are `cpu`, `memory`, `network_in` and `network_out`. |
| `metric_value` | String |The metric value to evaluate. |
| `policy_id` | String | The policy ID. |

## `ibm_is_instance_group_manager_policies`
{: #instance-group-managerpolicies}

Retrieve the details for all Gen 2 {{site.data.keyword.vsi_is_short}} instance group manager policies in your account.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #instance-group-manager-sample}

In the following example, you can retrieve a policy information of an instance group manager.

```
data "ibm_is_instance_group_manager_policy" "instance_group_manager_policy" {
  instance_group = "r006-76770f94-f7654-11e9-96e7-a77724435315"
  instance_group_manager = "r006-76770f94-f8764-11e9-96e7-a77726534315"
}
```
{: codeblock}

### Input parameters
{: #instance-group-manager-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`instance_group`|String|Required|The instance group ID.|
|`instance_group_manager`|String|Required|The instance group manager ID|


### Output parameters
{: #instance-group-manager-dsoutput}

Review the output parameters that you can access after you retrieved your data source.
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|Object|This ID is the combination of instance group ID, instance group manager ID and instance group manager policy ID. |
| `name` | String | The policy name.|
| `policy_type` | String | The type of metric to evaluate. |
| `metric_type` | String | The type of metric to evaluate. The possible values are `cpu`, `memory`, `network_in` and `network_out`. |
| `metric_value` | String |The metric value to evaluate. |
| `policy_id` | String | The policy ID. |

## `ibm_is_instance_profile`
{: #vpc-instance-profile}

Retrieve information about a virtual server instance profile. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-instance-profile-sample}

The following example retrieves information about the `bx2-2x8` instance profile. 
{: shortdesc}

```

data "ibm_is_instance_profile" "profile" {
	name = "b-2x8"
}

```
{: codeblock}

### Input parameters
{: #vpc-instance-profile-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name for this virtual server instance profile.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-instance-profile-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`family`|String|The family of the virtual server instance profile.|
|`architecture`|String|The default Operating System architecture for an instance of the profile.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_is_instance_profiles`
{: #vpc-instance-profiles}

Retrieve information about supported virtual server instance profiles. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-instance-profiles-sample}

```
data "ibm_is_instance_profiles" "ds_instance_profiles" {
}

```
{: codeblock}

### Input parameters
{: #vpc-instance-profiles-input}

This data source does not support any input parameters.
{: shortdesc}

### Output parameters
{: #vpc-instance-profiles-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`profiles`|List of objects|List of all server instance profiles in the region.  |
|`profiles.name`|String|The name for this virtual server instance profile.  |
|`profiles.family`|String|The family of the virtual server instance profile.|
|`profiles.architecture`|String|The default Operating System architecture for an instance of the profile.|
{: caption="Table 1. Available output parameters" caption-side="top"}





## `ibm_is_public_gateway`
{: #public-gwy-g2}

Retrieve the details for a public gateway data source.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #public-gwy-g2-sample}

The following example shows how you can retrieve information about the `us-south` region. 
{: shortdesc}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "test"
}

resource "ibm_is_public_gateway" "testacc_gateway" {
  name = "test-gateway"
  vpc  = ibm_is_vpc.testacc_vpc.id
  zone = "us-south-1"
}

data "ibm_is_public_gateway" "testacc_dspgw"{
  name = ibm_is_public_gateway.testacc_public_gateway.name
}
```
{: codeblock}

### Input parameters
{: #public-gwy-g2-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `name` | String | Required | The name of the gateway. |
| `resource_group` | String | Optional | The resource group ID of the public gateway. **Note** This parameter is supported only for VPC Gen 2 infrastructure. |

### Output parameters
{: #public-gwy-g2-dsoutput}

Review the output parameters that you can access after you retrieve your data source.
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `is` | String | The ID of the public gateway. |
| `status` | String | The status of the gateway. |
| `vpc` | String | The VPC ID of the gateway. |
| `zone` | String | The public gateway zone name. |
| `floating_ip` | String | Lists the nested block describes the floating IP of the gateway.  with **id** and **address**. |
| `floating_ip.id` | String | The ID of the floating IP that is bound to the public gateway. |
| `floating_ip.address` | String | The IP address of the floating IP that is bound to the public gateway. |





## `ibm_is_lb`
{: #ibm-is-lb}

Import the details of an existing IBM VPC Load Balancer as a read only data source.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ibm-is-lb-sample}

The following example shows how you can retrieve information about the `us-south` region. 
{: shortdesc}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "testvpc"
}

resource "ibm_is_subnet" "testacc_subnet" {
  name            = "testsubnet"
  vpc             = ibm_is_vpc.testacc_vpc.id
  zone            = "us-south-1"
  ipv4_cidr_block = "10.240.0.0/24"
}

resource "ibm_is_lb" "testacc_lb" {
  name    = "testlb"
  subnets = [ibm_is_subnet.testacc_subnet.id]
}

data "ibm_is_lb" "ds_lb" {
  name = ibm_is_lb.testacc_lb.name
}
```
{: codeblock}

### Input parameters
{: #ibm-is-lb-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `name` | String | Required | The name of the load balancer. | 


### Output parameters
{: #ibm-is-lb-dsoutput}

Review the output parameters that you can access after you retrieve your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `hostname` | String | Fully qualified domain name assigned to this load balancer.|
| `id` | String | The ID of the load balancer. |
| `listeners` | String | The ID of the listeners attached to this load balancer. |
| `logging`| Boolean| Enable (`true`) or disable (`false`) datapath logging for this load balancer. If unspecified, datapath logging is disabled. This option is supported only for application load balancers. |
| `operating_status` | String | The operating status of this load balancer.|
| `pools` | String | List all the Pools attached to this load balancer. |
| `pools.algorithm` | String | The load balancing algorithm. |
| `pools.created_at` | String |The date and time pool was created. |
| `pools.href` | String | The pool's canonical URL. |
| `pools.id` | String | The unique identifier for this load balancer pool. |
| `pools.name` | String | The user-defined name for this load balancer pool. |
| `pools.protocol` | String | The protocol used for this load balancer pool. |
| `pools.provisioning_status` | String | The provisioning status of this pool. |
| `pools.health_monitor` | String | The health monitor of this pool. |
| `pools.health_monitor.delay` | String | The health check interval in seconds. Interval must be greater than timeout value. |
| `pools.health_monitor.max_retries` | String | The health check max retries. |
| `pools.health_monitor.timeout` | String | The health check timeout in seconds. |
| `pools.health_monitor.type` | String | The protocol type of this load balancer pool health monitor. |
| `pools.health_monitor.url_path` | String | The health monitor of this pool. |
| `pools.health_monitor` | String | The health check URL. This is applicable only to HTTP type of health monitor. |
| `pools.instance_group` | String | The instance group that is managing this pool. |
| `pools.instance_group.crn` | String | The CRN for this instance group. |
| `pools.instance_group.href` | String |  The URL for this instance group. |
| `pools.instance_group.id` | String | The unique identifier for this instance group. |
| `pools.instance_group.name` | String | The user-defined name for this instance group. |
| `pools.members` | String | The backend server members of the pool. |
| `pools.members.href` | String | The canonical URL of the member. |
| `pools.members.id` | String | The unique identifier for this load balancer pool member. |
| `pools.session_persistence` | String | The session persistence of this pool. |
| `pools.session_persistence.type` | String | The session persistence type. |
| `public_ips` | String | The public IP addresses assigned to this load balancer.|
| `private_ips` | String | The private IP addresses assigned to this load balancer.|
| `resource_group` | String | The resource group where the load balancer is created. |
| `security_groups`| List| A list of security groups that are used with this load balancer. This option is supported only for application load balancers.|
| `security_groups_supported`|Boolean|Indicates if this load balancer supports security groups.|
| `subnets` | String | The ID of the subnets to provision this load balancer. |
| `status` | String | The status of load balancer.|
| `tags` | String | The tags associated with the load balancer. |
| `type` | String | The type of the load balancer. |





## `ibm_is_lbs`
{: #ibm-is-lbs}

Import the details of an existing IBM VPC Load Balancers as a read only data source.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ibm-is-lbs-sample}

The following example shows how you can declare the data. 
{: shortdesc}

```
data "ibm_is_lbs" "ds_lbs" {
 }
```
{: codeblock}

### Input parameters
{: #ibm-is-lbs-dsinput}

There is no input parameters for bim-is-lbs data source. 
{: shortdesc}


### Output parameters
{: #ibm-is-lbs-dsoutput}

Review the output parameters that you can access after you retrieve your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`load_balancers`|String|The Collection of load balancers.|
|`loadbalancers.id`|String|The unique identifier of the load balancer.|
|`loadbalancers.created_at`|String|The date and time this load balancer was created.|
|`loadbalancers.crn`|String|The load balancer's CRN.|
|`loadbalancers.name`|String|Name of the load balancer.|
|`loadbalancers.subnets`|String|The subnets this load balancer is part of.|
|`loadbalancers.subnets.crn`|String|The CRN for the subnet.|
|`loadbalancers.subnets.id`|String|The unique identifier for this subnet.|
|`loadbalancers.subnets.href`|String|The URL for this subnet.|
|`loadbalancers.subnets.name`|String|The user-defined name for this subnet.|
|`loadbalancers.hostname`|String|The Fully qualified domain name assigned to this load balancer.|
|`loadbalancers.listeners`|String|The listeners of this load balancer.|
|`loadbalancers.listeners.id`|String|The unique identifier for this load balancer listener.|
|`loadbalancers.listeners.href`|String|The listener's canonical URL.|
|`loadbalancers.operating_status`|String|The operating status of this load balancer.|
|`loadbalancers.pools`|String|The pools of this load balancer.|
|`loadbalancers.pools.href`|String|The pool's canonical URL.|
|`loadbalancers.pools.id`|String|The unique identifier for this load balancer pool.|
|`loadbalancers.pools.name`|String|The user-defined name for this load balancer pool.|
|`loadbalancers.profile`|String|The profile to use for this load balancer.|
|`loadbalancers.profile.family`|String|The product family this load balancer profile belongs to.|
|`loadbalancers.profile.href`|String|The URL for this load balancer profile.|
|`loadbalancers.profile.name`|String|The name for this load balancer profile.|
|`loadbalancers.private_ips`|String|The private IP addresses assigned to this load balancer.|
|`loadbalancers.provisioning_status`|String|The provisioning status of this load balancer. Possible values are: **active**, **create_pending**, **delete_pending**, **failed**, **maintenance_pending**, **update_pending**|
|`loadbalancers.public_ips`|String|The public IP addresses assigned to this load balancer.|
|`loadbalancers.resource_group`|String|The resource group where the load balancer is created.|
|`loadbalancers.status`|String|The status of the load balancers.|
|`loadbalancers.type`|String|The type of the load balancer.|
|`loadbalancers.tags`|String|Tags associated with the load balancer.|





## `ibm_is_lb_profiles`
{: #ibm-is-lb-profiles}

Retrieve information of an existing {{site.data.keyword.cloud_notm}} Infrastructure load balancer profiles.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ibm-is-lb-profiles-sample}

```

data "ibm_is_lb_profiles" "ds_lb_profiles" {
}

```
{: codeblock}

### Input parameters
{: #ibm-is-lb-profiles-input}

There is no input parameters that you can specify for your data source. 
{: shortdesc}

### Output parameters
{: #ibm-is-lb-profiles-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`lb_profiles`|String|List of all load balancer profiles in the IBM Cloud Infrastructure.|
|`lb_profiles.family`|String|The product family this load balancer profile belongs to.|
|`lb_profiles.href`|String|The URL for this load balancer profile.|
|`lb_profiles.name`|String|The name for this load balancer profile.|





## `ibm_is_region`
{: #vpc-region}

Retrieve information about a VPC Gen 2 Compute region. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-region-sample}

```

data "ibm_is_region" "ds_region" {
    name = "us-south"
}

```
{: codeblock}

### Input parameters
{: #vpc-region-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the region.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-region-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`status`|String|The status of the region.|
|`endpoint`|String|The endpoint of the region.|
{: caption="Table 1. Available output parameters" caption-side="top"}





## `ibm_is_security_group`
{: #sec-group-datasource}

Import the details of a security group as a read-only data source. You can reference the output parameters for each data source by using [Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}


### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #sec-group-sample}

The following example allows to create a different types of protocol rules `ALL`, `ICMP`, `UDP`, `TCP` and read the security group.
{: shortdesc}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "test"
}

resource "ibm_is_security_group" "testacc_security_group" {
  name = "test"
  vpc  = ibm_is_vpc.testacc_vpc.id
}

resource "ibm_is_security_group_rule" "testacc_security_group_rule_all" {
  group     = ibm_is_security_group.testacc_security_group.id
  direction = "inbound"
  remote    = "127.0.0.1"
}

resource "ibm_is_security_group_rule" "testacc_security_group_rule_icmp" {
  group     = ibm_is_security_group.testacc_security_group.id
  direction = "inbound"
  remote    = "127.0.0.1"
  icmp {
    code = 20
    type = 30
  }
}

resource "ibm_is_security_group_rule" "testacc_security_group_rule_udp" {
  group     = ibm_is_security_group.testacc_security_group.id
  direction = "inbound"
  remote    = "127.0.0.1"
  udp {
    port_min = 805
    port_max = 807
  }
}

resource "ibm_is_security_group_rule" "testacc_security_group_rule_tcp" {
  group     = ibm_is_security_group.testacc_security_group.id
  direction = "egress"
  remote    = "127.0.0.1"
  tcp {
    port_min = 8080
    port_max = 8080
  }
}

data "ibm_is_security_group" "sg1_rule" {
  name = ibm_is_security_group.testacc_security_group.name
}
```
{: codeblock}

### Input parameters
{: #sec-group-ds-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------| 
|`name`|String|Required|The name of the security group.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #sec-group-ds-output}

Review the output parameters that are exported. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the security group.|
|`rules`|List of objects|Rules associated with security group. Each rule has following attributes. |
|`rules.rule_id`| String|ID of the rule.  |
|`rules.direction`|String|Direction of traffic to enforce, either inbound or outbound. |
|`rules.ip_version`|String|IP version: IPv4 or IPv6.  |
|`rules.protocol`|String|The type of the protocol `all`, `icmp`, `tcp`, `udp`.   |
|`rules.type`|String|The traffic type to allow.  |
|`rules.code`|String|The traffic code to allow.  |
|`rules.port_max`|Integer|The TCP/UDP port range that includes the maximum bound. |
|`rules.port_min`|Integer|The TCP/UDP port range that includes the minimum bound. |
|`rules.remote`|Integer| Security group ID, an IP address, a CIDR block, or a single security group identifier. |
{: caption="Table 1. Available output parameters" caption-side="top"}





## `ibm_is_ssh_key`
{: #vpc-ssh-key}

Retrieve information about a VPC Gen 2 SSH key. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-ssh-key-sample}

```

data "ibm_is_ssh_key" "ds_key" {
    name = "test"
}

```
{: codeblock}

### Input parameters
{: #vpc-ssh-key-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the SSH key.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-ssh-key-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`|String|The ID of the SSH key.|
|`fingerprint`| String| The SHA256 fingerprint of the public key.|
|`length`|String|The length of the SSH key.|
|`type`|String|The crypto system that is used by this key.|
|`public_key`|String|The public SSH key value.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_is_subnet`
{: #vpc-subnet}

Retrieve information about a VPC Gen 2 compute subnet. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-subnet-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
	name = "test"
}

resource "ibm_is_subnet" "testacc_subnet" {
	name = "test_subnet"
	vpc = ibm_is_vpc.testacc_vpc.id
	zone = "us-south-1"
	ipv4_cidr_block = "192.168.0.0/1"
}
data "ibm_is_subnet" "ds_subnet" {
	identifier = ibm_is_subnet.testacc_subnet.id
}

```
{: codeblock}

### Input parameters
{: #vpc-subnet-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`identifier`|String|Required|The ID of the subnet is optional when the name is provided.|
|`name`|String|Optional|The name of the subnet is required when the identifier is not provided.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-subnet-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`ipv4_cidr_block`| String|The IPv4 range of the subnet.|
|`ipv6_cidr_block`|String|The IPv6 range of the subnet.|
|`total_ipv4_address_count`|Integer|The total number of IPv4 addresses.|
|`ip_version`|String|The IP version.|
|`name`|String|The name of the subnet.|
|`network_acl`|String|The ID of the network ACL for the subnet.|
|`public_gateway`|String|The ID of the public gateway for the subnet.|
|`status`|String|The status of the subnet.|
|`tags` |String| Tags associated for the instance.|
|`vpc`|String|The ID of the VPC that the subnet belongs to.|
|`zone`|String|The subnet zone name.|
|`available_ipv4_address_count`|Integer|The total number of available IPv4 addresses.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_is_subnets`
{: #vpc-subnets}

Retrieve information about all existing VPC subnets in an IBM Cloud account. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-subnets-sample}

```
data "ibm_is_subnets" "ds_subnets" {
}
```
{: codeblock}

### Input parameters
{: #vpc-subnets-input}

This resource does not support any input parameters.

### Output parameters
{: #vpc-subnets-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`subnets`|List|A list of subnets in the IBM Cloud account.|
|`subnets.name`|String|The name of the subnet.|
|`subnets.id`|String|The ID of the subnet.|
|`subnets.ipv4_cidr_block`|String|The IPv4 CIDR block of this subnet.|
|`subnets.ipv6_cidr_block`|String|The IPv6 CIDR block of this subnet.|
|`subnets.status`|String|The status of the subnet.|
|`subnets.crn`|String|The CRN of the subnet.|
|`subnets.available_ipv4_address_count`|Integer|The number of IPv4 addresses that are available in the subnet.|
|`subnets.total_ipv4_address_count`|Integer|The total number of IPv4 addresses in the subnet.|
|`subnets.network_acl`|String|The access control list (ACL) that is attached to the subnet.|
|`subnets.public_gateway`|Boolean|If set to **true**, a public gateway is attached to the subnet. If set to **false**, no public gateway for this subnet exists.|
|`subnets.resource_group`|String|The resource group that the subnet belongs to.|
|`subnets.vpc`|String|The ID of the VPC that this subnet belongs to.|
|`subnets.zone`|String|The zone where the subnet was created.|


## `ibm_is_subnet_reserved_ip`
{: #vpc-subnet-reserved-ipds}

Retrieve information about a reserved IP in a subnet. For more information, about associated reserved IP subnet, see [reserved IP subnet](/docs/vpc?topic=vpc-troubleshoot-reserved-ip).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #pc-subnet-reserved-ip-dssample}

```
data "ibm_is_subnet_reserved_ip" "data_reserved_ip" {
  subnet = ibm_is_subnet.test_subnet.id
  reserved_ip = ibm_is_subnet_reserved_ip.resource_res_ip.reserved_ip
}

```
{: codeblock}

### Input parameters
{: #pc-subnet-reserved-ip-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`subnet`| String | Required | The ID for the subnet.|
|`reserved_ip`| String | Required | The ID for the reserved IP.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #pc-subnet-reserved-ip-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`auto_delete`| String | The auto_delete boolean for reserved IP.|
|`created_at`| String | The creation timestamp for the reserved IP.|
|`href`| String | The unique reference for the reserved IP.|
|`id`| String | The ID for the reserved IP.|
|`name`| String | The name for the reserved IP.|
|`owner`| String | The owner of the reserved IP.|
|`reserved_ip`| String | The ID for the reserved IP.|
|`resource_type`| String | The resource type.|
|`subnet`| String | The ID for the subnet for the reserved IP.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_subnet_reserved_ips`
{: #vpc-subnet-reserved-ipsds}

Retrieve information about a reserved IP in a subnet. For more information, about associated reserved IP subnet, see [reserved IP subnet](/docs/vpc?topic=vpc-troubleshoot-reserved-ip).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #pc-subnet-reserved-ips-dssample}

```
data "ibm_is_subnet_reserved_ips" "data_reserved_ips" {
  subnet = ibm_is_subnet.test_subnet.id
}

```
{: codeblock}

### Input parameters
{: #pc-subnet-reserved-ips-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`subnet`| String | Required | The ID for the subnet.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #pc-subnet-reserved-ips-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`| String | The ID for the all the reserved ID in current timestamp format.|
|`limit`| String | The number of reserved IPs to list.|
|`reserved_ips`| String | The collection of all the reserved IPs in the subnet.|
|`reserved_ips.address`| String | The IP bound for the reserved IP.|
|`reserved_ips.auto_delete`| String | If reserved IP shall be deleted automatically.|
|`reserved_ips.created_at`| String | The date and time that the reserved IP was created.|
|`reserved_ips.href`| String | The URL for this reserved IP.|
|`reserved_ips.reserved_ip`| String | The unique identifier for this reserved IP.|
|`reserved_ips.name`| String | The user defined or system provided name for this reserved IP.|
|`reserved_ips.owner`| String | The owner of a reserved IP, defining whether it is managed by the user or the provider.|
|`reserved_ips.resource_type`| String | The resource type.|
|`sort`| String | The keyword on which all the reserved IPs are sorted.|
|`subnet`| String | The ID for the subnet for the reserved IP.|
|`total_count`| String | The number of reserved IP in the subnet.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_instance_templates`
{: #vpc-instance-templates}

Retrieve information about all the instance template in an account. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-instance-templates-sample}

The following example, you can fetch information of list of the instance templates VPC gen-2 infrastructure.
{: shortdesc}

```
data "ibm_is_instance_templates" "instancetemplates" {	   
}
```
{: codeblock}

### Input parameters
{: #vpc-instance-templates-input}

This data source does not support any input parameters.
{: shortdesc}

### Output parameters
{: #vpc-instance-templates-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`templates`|List of objects|List of templates.  |
|`templates.id`|String|The ID of the instance template. |
|`templates.name`|String|The name of the instance template. |
|`templates.image`|String|The ID of the image to create the template.|
|`templates.profile`|String|The number of instances created in the instance group. |
|`templates.vpc`|String|The VPC ID that the instance templates needs to be created.|
|`templates.zone`|String|The name of the zone. |
|`templates.keys`|String|List of SSH key IDs used to allow log in user to the instances. |
|`templates.resource_group`|String|The resource group ID. |
|`templates.primary_network_interfaces`|String|A nested block describes the primary network interface for the template. |
|`templates.primary_network_interfaces.subnet`|String|The VPC subnet to assign to the interface. |
|`templates.primary_network_interfaces.name`|String|The name of the interface. |
|`templates.primary_network_interfaces.security_groups`|String|List of security groups of the subnet. |
|`templates.primary_network_interfaces.primary_ipv4_address`|String|The IPv4 address assigned to the primary network interface. |
|`templates.network_interfaces`|String|A nested block describes the network interfaces for the template. |
|`templates.network_interfaces.subnet`|String|The VPC subnet to assign to the interface. |
|`templates.network_interfaces.name`|String|The name of the interface. |
|`templates.network_interfaces.security_groups`|String|List of security groups of  the subnet. |
|`templates.network_interfaces.primary_ipv4_address`|String|The IPv4 address assigned to the network interface. |
|`templates.boot_volume`|String|A nested block describes the boot volume configuration for the template. |
|`templates.boot_volume.encryption`|String|The encryption key CRN such as HPCS, Key Protect, etc., is provided to encrypt the boot volume attached.  |
|`templates.boot_volume.name`|String|The name of the boot volume. |
|`templates.boot_volume.size`|String|The boot volume size to configure in giga bytes. |
|`templates.boot_volume.iops`|String|The IOPS for the boot volume. |
|`templates.boot_volume.profile`|String|The profile for the boot volume configuration. |
|`templates.boot_volume.delete_volume_on_instance_delete`|String|You can configure to delete the boot volume based on instance deletion. |
|`templates.volume_attachments`|String|A nested block describes the storage volume configuration for the template. |
|`templates.volume_attachments.name`|String|The name of the boot volume. |
|`templates.volume_attachments.volume`|String|The storage volume ID created in VPC. |
|`templates.volume_attachments.delete_volume_on_instance_delete`|Boolean|You can configure to delete the storage volume to delete based on instance deletion. |
|`templates.user_data` | String|The user data provided for the instance. |
{: caption="Table 1. Available output parameters" caption-side="top"}





## `ibm_is_virtual_endpoint_gateway`
{: #vpc-endpoint-gwyds}

Create, update, or delete a VPC endpoint gateway by using virtual endpoint gateway resource. For more information, about the VPC endpoint gateway, see [Creating an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-endpoint-gwyds-sample}

```
data "ibm_is_virtual_endpoint_gateway" "data_test" {    
    name = ibm_is_virtual_endpoint_gateway.endpoint_gateway.name
}

```
{: codeblock}

### Input parameters
{: #vpc-endpoint-gwyds-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The endpoint gateway name.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-endpoint-gwyds-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`created_at`|String|The created date and time of the endpoint gateway.|
|`health_state`|String|Endpoint gateway health state. `ok: Healthy`, `degraded: Suffering from compromised performance, capacity, or connectivity`, `faulted: Completely unreachable, inoperative, or entirely incapacitated`, `inapplicable: The health state does not apply because of the current lifecycle state`. A resource with a lifecycle state of failed or deleting will have a health state of inapplicable. A pending resource may have this state.|
|`lifecycle_state`|String|The endpoint gateway lifecycle state, supported values are `deleted`, `deleting`, `failed`, `pending`, `stable`, `updating`, `waiting`, `suspended`.|
|`ips`|String|The unique identifier for the reserved IP.|
|`ips.id`|String|The collection of reserved IPs bound to an endpoint gateway.|
|`ips.name`|String|The user defined or system provided name of the resource IP.|
|`ips.resource_type`|String|The endpoint gateway IP resource type.|
|`resource_group`|String| The unique identifier for the resource group.|
|`target`|String| The endpoint gateway target.|
|`target.name`|String|The target name.|
|`target.resource_type`|String|The resource type of the subnet reserved IP.|
|`vpc`|String|The VPC ID.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_virtual_endpoint_gateway_ips`
{: #vpc-endpoint-gwy-ipsds}

Create, update, or delete a VPC endpoint gateway IPs by using virtual endpoint gateway ips resource. For more information, about the VPC endpoint gateways, see [About VPC gateways](/docs/vpc?topic=vpc-about-vpe).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-endpoint-gwy-ipsds-sample}

```
data "ibm_is_virtual_endpoint_gateway_ips" "data_test1" {
  gateway     = ibm_is_virtual_endpoint_gateway.endpoint_gateway.id
}
```
{: codeblock}

### Input parameters
{: #vpc-endpoint-gwy-ipsds-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`gateway`|String|Required|The endpoint gateway ID.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-endpoint-gwy-ipsds-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`address`|String|The endpoint gateway IP address.|
|`auto_delete`|String|The endpoint gateway IP auto delete.|
|`created_at`|String|The created date and time of the endpoint gateway IP.|
|`id`|String|The endpoint gateway reserved IP ID.|
|`name`|String|The endpoint gateway IP name.|
|`reserved_ip`|String|The endpoint gateway reserved IP ID.|
|`resource_type`|String|The endpoint gateway IP resource type.|
|`target`|String|The endpoint gateway target details.|
|`target.id`|String|The IPs target ID.|
|`target.name`|String|The IPs target name.|
|`target.resource_type`|String|The endpoint gateway resource type.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_virtual_endpoint_gateways`
{: #vpc-endpoint-gwysds}

Create, update, or delete a VPC endpoint gateways by using virtual endpoint gateways resource. For more information, about the VPC endpoint gateway, see [Creating an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-endpoint-gwysds-sample}

```
data "ibm_is_virtual_endpoint_gateways" "data_test" {

}
```
{: codeblock}

### Input parameters
{: #vpc-endpoint-gwysds-input}

The input parameters is not support for the data source. 
{: shortdesc}

### Output parameters
{: #vpc-endpoint-gwysds-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`created_at`|String|The created date and time of the endpoint gateway.|
|`health_state`|String|Endpoint gateway health state. `ok: Healthy`, `degraded: Suffering from compromised performance, capacity, or connectivity`, `faulted: Completely unreachable, inoperative, or entirely incapacitated`, `inapplicable: The health state does not apply because of the current lifecycle state`. A resource with a lifecycle state of failed or deleting will have a health state of inapplicable. A pending resource may have this state.|
|`lifecycle_state`|String|The endpoint gateway lifecycle state, supported values are `deleted`, `deleting`, `failed`, `pending`, `stable`, `updating`, `waiting`, `suspended`.|
|`id`|String| The endpoint gateway ID.|
|`ips`|String|The collection of reserved IPs bound to an endpoint gateway.|
|`ips.id`|String|The unique identifier for the reserved IP.|
|`ips.name`|String|The user defined or system provided name of the resource IP.|
|`ips.resource_type`|String|The endpoint gateway IP resource type or the subnet reserved IP.|
|`name`|String| The endpoint gateway name.|
|`resource_group`|String| The unique identifier for the resource group.|
|`target`|String| The endpoint gateway target services.|
|`target.name`|String|The endpoint gateway target name.|
|`target.resource_type`|String|The endpoint gateway target resource type.|
|`vpc`|String|The VPC ID.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_vpc`
{: #vpc}

Retrieve information about a Gen 2 compute VPC. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
    name = "test"
}

data "ibm_is_vpc" "ds_vpc" {
    name = "test"
}

```
{: codeblock}

### Input parameters
{: #vpc-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the VPC.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`classic_access`|Boolean|Indicates whether this VPC is connected to Classic Infrastructure.|
|`crn`|String|The CRN of the VPC.|
| `cse_source_addresses`|List of Cloud Service Endpoints|A list of the cloud service endpoints that are associated with your VPC, including their source IP address and zone.|
|`cse_source_addresses.address`|String|The IP address of the cloud service endpoint.|
|`cse_source_addresses.zone_name`|String|The zone where the cloud service endpoint is located.|
|`default_network_acl`|String| The ID of the default network ACL.|
|`default_security_group`| String | The unique identifier of the VPC default security group.|
|`default_routing_table`| String | The unique identifier of the VPC default routing table.|
|`resource_group`|String|The resource group ID where the VPC created.|
|`subnets`|List of subnets|A list of subnets that are attached to a VPC.|
|`subnets.name`|String|The name of the subnet.|
|`subnets.id`|String|The ID of the subnet.|
|`subnets.zone`|String|The zone that the subnet belongs to.|
|`subnets.status`|String|The status of the subnet.|
|`subnets.total_ipv4_address_count`|Integer|The total number of IPv4 addresses in the subnet.|
|`subnets.available_ipv4_address_count`|Integer|The number of IPv4 addresses in the subnet that are available for you to be used.|
|`status`|String|The status of the VPC.|
|`tags`|Array|Tags associated with the instance.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_volume_profile`
{: #volume-profile-ds}

Retrieve information of an existing {{site.data.keyword.cloud_notm}} VSI. For more information, about the volume concepts, see [expandable volume concepts for VPC](/docs/vpc?topic=vpc-expanding-block-storage-volumes#expandable-volume-concepts).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #volume-profile-dssample}

```
data "ibm_is_volume_profile" "volprofile"{
  name = "general-purpose"
}

```
{: codeblock}

### Input parameters
{: #volume-profile-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name for the virtual server volume profile.|
{: caption="Available input parameters" caption-side="top"}

### Output parameters
{: #volume-profile-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`href`|String| The family of the virtual server volume profile.|
{: caption="Available output parameters" caption-side="top"}

## `ibm_is_volume_profiles`
{: #volume-profiles-ds}

Retrieve information of an existing {{site.data.keyword.cloud_notm}} VSI. For more information, about the volumes and profiles, see [profiles](/docs/vpc?topic=vpc-block-storage-profiles).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #volume-profiles-dssample}

```
data "ibm_is_volume_profiles" "volprofiles"{
}

```
{: codeblock}

### Input parameters
{: #volume-profiles-dsinput}

This data source do not support input parameters. 
{: shortdesc}


### Output parameters
{: #volume-profiles-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`profiles`|String| Lists all server volume profiles in the region.|
|`profiles.name`|String| The name of the virtual server volume profile.|
|`profiles.family`|String| The family of the virtual server volume profile.|
{: caption="Available output parameters" caption-side="top"}

## `ibm_is_vpc_default_routing_table`
{: #vpc-default-routing-tableds}

Retrieve information of an existing {{site.data.keyword.cloud_notm}} infrastructure VPC default routing table. For more information, see [routing tables for VPC](/docs/vpc?topic=vpc-list-routing-tables-for-vpc).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-default-routing-table-dssample}

```
resource "ibm_is_vpc" "test_vpc" {
  name = "test-vpc"
}

data "ibm_is_vpc_default_routing_table" "ds_default_routing_table" {
	vpc = ibm_is_vpc.test_vpc.id
}

```
{: codeblock}

### Input parameters
{: #vpc-default-routing-table-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`vpc`|String|Required|The ID of the VPC.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-default-routing-table-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`created_at`|Timestamp| The date and time that the default routing table was created.|
|`href`|String| The routing table URL.|
|`id`|String| The unique ID for the default routing table. |
|`is_default`|String| Indicates the default routing table for this VPC.|
|`name`|String| The name for the default routing table.|
|`lifecycle_state`|String| The lifecycle state of the routing table.|
|`resource_type`|String| The resource type.|
|`route_direct_link_ingress`|Boolean| Indicates the routing table is used to route traffic that originates from Direct Link to the VPC.|
|`route_transit_gateway_ingress`|Boolean|Indicates the routing table is used to route traffic that originates from Transit Gateway to the VPC.|
|`route_vpc_zone_ingress`|Boolean|Indicates the routing table is used to route traffic that originates from subnets in other zones in the VPC. |
|`routes`|String|The routes for the default routing table.|
|`routes.id`|String| The unique ID of the route.|
|`routes.name`| String| The name of the route.|
|`subnets`|String| The subnets to which routing table is attached.|
|`subnets.id`|String| The unique ID of the subnet.|
|`subnets.name`|String| The name of the subnet.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_vpc_routing_table_routes`
{: #vpc-routing-tableds}

Retrieve information of an existing {{site.data.keyword.cloud_notm}} infrastructure VPC default routing table. For more information, see [routing tables for VPC](/docs/vpc?topic=vpc-list-routing-tables-for-vpc).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-routing-table-dssample}

```
resource "ibm_is_vpc" "test_vpc" {
  name = "test-vpc"
}

resource "ibm_is_vpc_routing_table" "test_routing_table" {
  name   = "test-routing-table"
  vpc    = ibm_is_vpc.test_vpc.id
}


data "ibm_is_vpc_routing_table_routes" "ds_routing_table_routes" {
	vpc = ibm_is_vpc.test_vpc.id
	routing_table = ibm_is_vpc_routing_tables.test_routing_table.routing_table
}
```
{: codeblock}

### Input parameters
{: #vpc-routing-table-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`vpc`|String|Required|The ID of the VPC.|
|`routing_table`|String|Required|The ID of the routing table.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-routing-table-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`routing_table_routes`|List| List of all the routing table in a VPC.|
|`routing_table_routes.name`|String| The name for the default routing table.|
|`routing_table_routes.route_id`|String| The unique ID for the route.|
|`routing_table_routes.lifecycle_state`|String| The lifecycle state of the route.|
|`routing_table_routes.href`|String| The routing table URL.|
|`routing_table_routes.created_at`|Timestamp| The date and time that the route was created.|
|`routing_table_routes.action`|String| The action to perform with a packet matching the route.|
|`routing_table_routes.destination`|String| The destination of the route.|
|`routing_table_routes.next_hop`|String| The next hop address of the route. |
|`routing_table_routes.zone`|String| The zone name of the route. |
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_vpc_routing_tables`
{: #vpc-routing-tablesds}

Retrieve information of an existing {{site.data.keyword.cloud_notm}} infrastructure VPC default routing tables. For more information, see [routing tables for VPC](/docs/vpc?topic=vpc-list-routing-tables-for-vpc).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-routing-tables-dssample}

```
resource "ibm_is_vpc" "test_vpc" {
  name = "test-vpc"
}

data "ibm_is_vpc_routing_tables" "ds_routing_tables" {
	vpc = ibm_is_vpc.test_vpc.id
}
```
{: codeblock}

### Input parameters
{: #vpc-routing-tables-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`vpc`|String|Required|The ID of the VPC.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-routing-tables-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`routing_tables`|List| List of all the routing tables in a VPC.|
|`routing_tables.name`|String| The name for the default routing tables.|
|`routing_tables.route_table`|String| The unique ID for the routing table.|
|`routing_tables.lifecycle_state`|String| The lifecycle state of the routing table.|
|`routing_tables.href`|String| The routing table URL.|
|`routing_tables.resource_type`|String| The type of resource referenced.|
|`routing_tables.created_at`|Timestamp| The date and time the routing table was created.|
|`routing_tables.is_default`|String| Indicates whether the default routing table.|
|`routing_tables.route_direct_link_ingress`|String| Indicates if the routing table is used to route traffic that originates from Direct Link to the VPC.|
|`routing_tables.route_transit_gateway_ingress`|String| Indicates if the routing table is used to route traffic that originates from Transit Gateway to the VPC.|
|`routing_tables.route_vpc_zone_ingress`|String| Indicates if the routing table is used to route traffic that originates from subnets in other zones of the VPC.|
|`routes`|String|The routes for the routing table.|
|`routes.id`|String| The unique ID of the route.|
|`routes.name`| String| The user-defined name of the route.|
|`subnets`|String| The subnets to which routing table is attached.|
|`subnets.id`|String| The unique ID of the subnet.|
|`subnets.name`|String| The user-defined name of the subnet.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_vpn_gateways`
{: #vpc-gateways-ds}

Retrieve information of an existing VPN gateways. For more information, see [use a VPC/VPN gateway for secure and private on-premises access](/docs/vpc-on-classic?topic=solution-tutorials-vpc-site2site-vpn).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-gateways-dssample}

```
data "ibm_is_vpn_gateways" "ds_vpn_gateways" {
  
}
```
{: codeblock}

### Input parameters
{: #vpc-gateways-dsinput}

This resource do not support the input parameters.
{: shortdesc}


### Output parameters
{: #vpc-gateways-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`|String| The ID of the VPN gateway.|
|`name`| String |The VPN gateway instance name.|
|`created_at`|timestamp| The date and time the VPN gateway was created.|
|`crn`|String| The VPN gateway's CRN.|
|`members`|String|The nested collection of the VPN gateway members.|
|`members.address`|String| The public IP address assigned to the VPN gateway member.|
|`members.private_address` |String | The private IP address assigned to the VPN gateway member.|
|`members.role`| String | The high availability role assigned to the VPN gateway member.|
|`members.status`|String| The status of the VPN gateway member.|
|`resource_type`|String| The resource type, supported value is `vpn_gateway`.|
|`status`|String|The status of the VPN gateway, support values are `available`, `deleting`, `failed`, `pending`).|
|`subnet`|String| The VPN gateway subnet information.|
|`resource_group`|String| The resource group ID.|
|`mode`|String|The VPN gateway mode, supported values are `policy` and `route`.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_vpn_gateway_connections`
{: #vpc-gateways-connection-ds}

Retrieve information of an existing VPN gateway connections. For more information, see [adding connections to a VPN gateway](/docs/vpc?topic=vpc-vpn-adding-connections).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-gateways-connection-dssample}

```
data "ibm_is_vpn_gateway_connections" "ds_vpn_gateway_connections" {
  vpn_gateway = ibm_is_vpn_gateway.testacc_vpnGateway.id
}
```
{: codeblock}

### Input parameters
{: #vpc-gateways-connection-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`status`|String|Optional|Filters the collection to VPN gateway connections with the specified status.|
|`vpn_gateway`|String|Required| The VPN gateway ID.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-gateways-connection-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`|String| The ID of the VPN gateway connection.|
|`name`| String |The VPN gateway connection name.|
|`created_at`|timestamp| The date and time the VPN gateway connection was created.|
|`admin_state_up`|String| The VPN gateway connection admin state. Default value is `true`.|
|`authentication_mode`|String|The authentication mode.|
|`ike_policy`|String| The VPN gateway connection IKE Policy.|
|`interval`| String | Interval for dead peer detection.|
|`ipsec_policy`|String| The IP security policy VPN gateway connection.|
|`local_cidrs`|String| The VPN gateway connection local CIDRs.|
|`mode`|String|The mode of the VPN gateway.|
|`peer_address`|String| The VPN gateway connection peer address.|
|`peer_cidrs`|String| The VPN gateway connection peer CIDRs.|
|`resource_type`|String|The resource type.|
|`timeout`|String|Timeout for dead peer detection.|
|`action`|String|Action detection for dead peer detection action.|
|`tunnels`|String|The VPN tunnel configuration for the VPN gateway connection (in static route mode).|
|`tunnels.address`|String|The IP address of the VPN gateway member in which the tunnel resides.|
|`tunnels.status`|String|The status of the VPN tunnel.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_is_zone`
{: #vpc-zone}

Retrieve information about a Gen 2 compute zone. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-zone-sample}

```

data "ibm_is_zone" "ds_zone" {
    name = "us-south-1"
    region = "us-south"
}

```
{: codeblock}

### Input parameters
{: #vpc-zone-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the zone.|
|`region`|String|Required| The name of the region.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-zone-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`status`|String|The status of the zone.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_is_zones`
{: #vpc-zones}

Retrieves information about Gen 2 compute zones. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpc-zones-sample}

```

data "ibm_is_zones" "ds_zones" {
    region = "us-south"
}

```
{: codeblock}

### Input parameters
{: #vpc-zones-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`region`|String|Required|The name of the region.|
|`status`|String|Optional|Filter the list by status of zones.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpc-zones-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`zones`|String|The list of zones in an {{site.data.keyword.cloud_notm}} region.  For example, `us-south-1`,`us-south-2`.|
{: caption="Table 1. Available output parameters" caption-side="top"}




