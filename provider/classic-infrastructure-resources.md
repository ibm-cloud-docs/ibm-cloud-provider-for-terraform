---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

keywords: terraform provider plugin, terraform classic infrastructure, terraform classic, terraform softlayer, terraform sl, terraform vsi, terraform Bare Metal server

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



# Classic infrastructure resources
{: #infrastructure-resources}

Review the Classic infrastructure resources that you can create, modify, or delete. You can reference the output parameters for each resource in other resources or data sources by using [Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}
 
## `ibm_cdn`
{: #cdn}

Create, or delete a CDN mapping. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cdn-sample}

```
resource "ibm_cdn" "test_cdn1" {
  host_name = "www.default.com"
  vendor_name = "akamai"
  origin_address = "111.111.111.5"
  origin_type = "HOST_SERVER"
}
```
{: codeblock}

### Input parameters
{: #cdn-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`host_name`|String|Required|The host name that is associated with the CDN domain mapping.| Yes |
|`cname`|String|Optional|The CNAME for your CDN. | Yes |
|`path`|String|Optional|The path for the CDN.| Yes |
|`vendor_name`|String|Required| Only `akamai` is supported for now.| Yes |
|`origin_type`|String|Required|The type of storage to use. Valid values are `HOST_SERVER` or `OBJECT_STORAGE`.| Yes |
|`origin_address`|String|Required|The IP address for the domain mapping.| No |
|`protocol`|String|Optional|The protocol to use. Default value is `HTTP`.| Yes |
|`http_port`|Integer|Optional|The port to be opened up. Default value is 80. This option can be set only if you use `HTTP` or `HTTPS` as the `protocol`. | No |
|`https_port`|Integer|Optional|The HTTPS port. Default value is 0. This option can be set only if you use `HTTP` or `HTTPS` as the `protocol`.| No |
|`bucket_name`|String|Required|If `origin_type` is set to `OBJECT_STORAGE`, you must provide the name of the bucket to use.| No |
|`certificate_type`|String|Conditional|The type of certificate to use. This value is required if `protocol` is set to `HTTPS`. Valid values are `SHARED_SAN_CERT` or `WILDCARD_CERT`.| Yes |
|`header`|String|Optional|The header for the CDN.| No |
|`respect_headers`|Boolean|Optional| If set to **true**, the TTL settings in the origin override CDN TTL settings.| No |
|`file_extension`|String|Optional|If `origin_type` is set to `OBJECT_STORAGE`, you can specify the file extensions that you want to cache. | No |
|`performance_configuration`|String|Optional|The performance configuration. Default is `General web delivery`.| No |
|`cache_key_query_rule`|String|Optional|The rule for caching keys. Valid values are `include-all` (includes all query arguments), `ignore-all` (ignores all query arguments), `ignore: space separated query-args` (ignores specific query arguments). Default value is `include-all`. | No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cdn-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique internal identifier of the CDN domain mapping.|
|`status`|String|The Status of the CDN domain mapping.|
{: caption="Table 1. Available output parameters" caption-side="top"}






## `ibm_compute_autoscale_group`
{: #autoscale-group}

Create, update, or delete autoscaling groups. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #autoscale-group-sample}

In the following example, you can create an auto scaling group that uses a Debian image. 
{: shortdesc}

```
resource "ibm_compute_autoscale_group" "test_scale_group" {
    name = "test_scale_group_name"
    regional_group = "as-sgp-central-1"
    minimum_member_count = 1
    maximum_member_count = 10
    cooldown = 30
    termination_policy = "CLOSEST_TO_NEXT_CHARGE"
    virtual_server_id = 267513
    port = 8080
    health_check {
      type = "HTTP"
    }
    virtual_guest_member_template {
      hostname = "test_virtual_guest_name"
      domain = "example.com"
      cores = 1
      memory = 1024
      network_speed = 100
      hourly_billing = true
      os_reference_code = "DEBIAN_8_64"

## Optional fields for virtual guest template ({{site.data.keyword.cloud_notm}} defaults apply):
      local_disk = false
      disks = [25]
      datacenter = "sng01"
      post_install_script_uri = ""
      ssh_key_ids = [383111]
      user_metadata = "#!/bin/bash ..."
    }

## Optional fields for scale_group:
    network_vlan_ids = [1234567, 7654321]
}
```
{: codeblock}

### Input parameters
{: #autoscale-group-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`name`|String|Required|The name of the autoscaling group.| No |
|`regional_group`|String|Required|The regional group for the autoscaling group.| Yes |
|`minimum_member_count`|Integer|Required|The minimum number of virtual guest members that are allowed in the autoscaling group.| No |
|`maximum_member_count`|Integer|Required|The maximum number of virtual guest members that are allowed in the autoscaling group.| No |
|`cooldown`|Integer|Required|The duration, expressed in seconds, that the autoscaling group waits before performing another scaling action.| No |
|`termination_policy`|String|Required|The termination policy for the autoscaling group.| No |
|`virtual_guest_member_template`|Array of string|Required|The template with which to create guest members. Only one template can be configured. You can find accepted values in the [`ibm_compute_vm_instance`](#vm) resource.| No |
|`network_vlan_ids`|Array|Optional|The collection of VLAN IDs for the autoscaling group. You can find accepted values in the [VLAN console](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want and notes the ID in the resulting URL. You can also refer to a VLAN name by using a data source.| No |
|`virtual_server_id`|Integer|Optional|The ID of a virtual server in a local load balancer. You can find the ID with the following URL `https://api.softlayer.com/rest/v3/SoftLayer_Network_Application_Delivery_Controller_LoadBalancer_VirtualIpAddress/<load_balancer_ID>/getObject?objectMask=virtualServers`. Replace `<load_balancer_ID>` with the ID of the target load balancer. **Note**: To view the load balancer ID. Log in to the [IBM Cloud Classic Infrastructure API](https://api.softlayer.com/rest/v3/SoftLayer_Hardware/getCreateObjectOptions.json) that uses your API key as the password. For more information, about creating classic infrastructure keys and locating your VPN username and password, refer [Managing classic infrastructure API keys](/docs/account?topic=account-classic_keys).| No |
|`port`|Integer|Optional|The port number in a local load balancer. For example, `8080`.| No |
|`health_check`|Map|Optional|The type of health check in a local load balancer. For example, `HTTP`. You can also use this value to specify custom HTTP methods.| No |
|`tags`|Array of string|Optional|A list of tags that you want to add to the autoscaling group. Tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #autoscale-group-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the autoscaling group.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_compute_autoscale_policy`
{: #autoscale-policy}

Create, update, or delete a policy for an autoscaling group.  
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #autoscale-policy-sample}

In the following example, you can create an autoscaling policy.
{: shortdesc}

```
resource "ibm_compute_autoscale_policy" "test_scale_policy" {
    name = "test_scale_policy_name"
    scale_type = "RELATIVE"
    scale_amount = 1
    cooldown = 30
    scale_group_id = ibm_compute_autoscale_group.sample-http-cluster.id
    triggers {
        type = "RESOURCE_USE"
        watches {
                    metric = "host.cpu.percent"
                    operator = ">"
                    value = "80"
                    period = 120
        }
    }
    triggers {
        type = "ONE_TIME"
        date = "2016-07-30T23:55:00-00:00"
    }
    triggers {
        type = "REPEATING"
        schedule = "0 1 ? * MON,WED *"
    }
}
```
{: codeblock}

### Input parameters
{: #autoscale-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the autoscaling policy.| No |
|`scale_type`|String|Required|The scale type for the autoscaling policy. Accepted values are `ABSOLUTE`, `RELATIVE`, and `PERCENT`.| No |
|`scale_amount`|Integer|Required|A count of the scaling actions to perform upon any trigger hit.| No |
|`cooldown`|Integer|Optional|The duration, expressed in seconds, that the policy waits after the last action date before performing another scaling action. If you do not provide a value, the `scale_group` cool down applies.| No |
|`scale_group_id`|Integer|Required| The ID of the autoscaling group that is associated with the policy.| Yes |
|`triggers`|Array of string|Optional| The triggers to check for this group.| No |
|`tags`|Array of string|Optional|The tags that you want to add to the autoscaling policy. Tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #autoscale-policy-output}
Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the autoscaling policy.|
{: caption="Table 1. Available output parameters" caption-side="top"}






## `ibm_compute_bare_metal`
{: #bm}

Provides a Bare Metal resource. This allows Bare Metal servers to be created, updated, and deleted. This resource supports both monthly Bare Metal servers and hourly Bare Metal servers. For more information, on Bare Metal severs, refer [IBM Cloud Bare Metal server page](https://www.ibm.com/cloud/bare-metal-servers).


### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #bm-sample}

#### Hourly Bare Metal server
When the `ibm_compute_bare_metal` resource definition has a `fixed_config_preset` attribute, Terraform on {{site.data.keyword.cloud_notm}} creates an hourly Bare Metal server. The monthly bare metal server resource provides options to configure process, memory, network, disk, and RAID. You can also assign VLANs and subnets for the target monthly bare metal server.  Hardware specifications are predefined in the `fixed_config_preset` attribute and cannot be modified. To configure the monthly bare metal server, you must provide more attributes such as `package_key_name`, `proecss_key_name`, `disk_key_names`, and `os_key_name`. The following example shows you how to create a new hourly Bare Metal server.
{: shortdesc}

##### Example of an hourly Bare Metal server
```
resource "ibm_compute_bare_metal" "hourly-bm1" {
    hostname = "hourly-bm1"
    domain = "example.com"
    os_reference_code = "UBUNTU_16_64"
    datacenter = "dal01"
    network_speed = 100 # Optional
    hourly_billing = true # Optional
    private_network_only = false # Optional
    fixed_config_preset = "S1270_8GB_2X1TBSATA_NORAID"

    user_metadata = "{\"value\":\"newvalue\"}" # Optional
    tags = [
      "collectd",
      "mesos-master"
    ]
    notes = "note test"
}
```
{: codeblock}

#### Monthly Bare Metal server
When the `fixed_config_preset` attribute is not configured, Terraform on {{site.data.keyword.cloud_notm}} creates a monthly Bare Metal server resource. The monthly Bare Metal server resource provides options to configure process, memory, network, disk, and RAID. You can also assign VLANs and subnets for the target monthly Bare Metal server. To configure the monthly Bare Metal server, you must provide more attributes such as `package_key_name`, `proecss_key_name`, `disk_key_names`, and `os_key_name`. The following example shows you how to create a new monthly Bare Metal server.

##### Example of a monthly Bare Metal server
```
resource "ibm_compute_bare_metal" "monthly_bm1" {


## Mandatory fields
    package_key_name = "DUAL_E52600_V4_12_DRIVES"
    process_key_name = "INTEL_INTEL_XEON_E52620_V4_2_10"
    memory = 64
    os_key_name = "OS_WINDOWS_2012_R2_FULL_DC_64_BIT_2"
    hostname = "cust-bm"
    domain = "ms.com"
    datacenter = "wdc04"
    network_speed = 100
    public_bandwidth = 500
    disk_key_names = [ "HARD_DRIVE_800GB_SSD", "HARD_DRIVE_800GB_SSD", "HARD_DRIVE_800GB_SSD" ]
    hourly_billing = false


## Optional fields
    private_network_only = false
    unbonded_network = true
    user_metadata = "{\"value\":\"newvalue\"}"
    public_vlan_id = 12345678
    private_vlan_id = 87654321
    public_subnet = "50.97.46.160/28"
    private_subnet = "10.56.109.128/26"
    tags = [
      "collectd",
      "mesos-master"
    ]
    redundant_power_supply = true
    storage_groups = {
       # RAID 5
       array_type_id = 3
       # Use three disks
       hard_drives = [ 0, 1, 2]
       array_size = 1600
       # Basic partition template for Windows
       partition_template_id = 17
    }
}
```
{: codeblock}

**Note**: Monthly Bare Metal servers do not support `immediate cancellation`. When Terraform on {{site.data.keyword.cloud_notm}} deletes the monthly Bare Metal server, the `anniversary date cancellation` option is used.

#### Create a Bare Metal server that uses quote ID
If you already have a quote ID for the Bare Metal server, you can create a new Bare Metal server with the quote ID. The following example shows you how to create a new Bare Metal server with a quote ID.

##### Example of a quote based ordering
```
resource "ibm_compute_bare_metal" "quote_test" {


## Mandatory fields
    hostname = "quote-bm-test"
    domain = "example.com"
    quote_id = 2209349


## Optional fields
    user_metadata = "{\"value\":\"newvalue\"}"
    public_vlan_id = 12345678
    private_vlan_id = 87654321
    public_subnet = "50.97.46.160/28"
    private_subnet = "10.56.109.128/26"
    tags = [
      "collectd",
      "mesos-master"
    ]  
}
```
{: codeblock}

### Input parameters
{: #bm-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

#### Input parameters for all Bare Metal server types

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`hostname`|String|Optional|The host name for the compute instance.| Yes |
|`domain`|String|Required|The domain for the computing instance.| Yes |
|`user_metadata`|String|Optional|(Arbitrary data to be made available to the compute instance.| Yes |
|`notes`|String|Optional|Notes to associate with the instance.| No |
|`ssh_key_ids`|Array of integers|Optional|The SSH key IDs to install on the compute instance when the instance is provisioned. **Note:** If you don't know the IDs for your SSH keys, you can reference your SSH keys by their labels.| Yes |
|`post_install_script_uri`|String|Optional|The URI of the script to be downloaded and executed after installation is complete.| Yes |
|`tags`|Array of string|Optional| Tags associated with this Bare Metal server. Permitted characters include A-Z, 0-9, whitespace, `_` (underscore), `-` (hyphen), `.` (period), and `:` (colon). All other characters are removed.| No |
|`file_storage_ids`|Array of integers|Optional|File storage to which this computing instance has access. File storage must be in the same data center as the Bare Metal server. If you use this argument to authorize, access to file storage, do not use the `allowed_hardware_ids` argument in the `ibm_storage_file` resource in order to prevent the same storage be added twice.| No |
|`block_storage_ids`|Array of integers|Optional|Block storage to which this computing instance has access. Block storage must be in the same data center as the Bare Metal server. If you use this argument to authorize, access to block storage, do not use the `allowed_hardware_ids` argument in the `ibm_storage_file` resource in order to prevent the same storage be added twice.#### Arguments common to hourly and monthly server|  No |


#### Input parameters common to hourly and monthly server

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`datacenter`|String|Required|The data center in which you want to provision the instance.|
|`gpu_key_name`|String|Optional|The key name for the primary Graphics Processing Unit (GPU). For example, `GPU_NVIDIA_GRID_K2`. Locate your package ID. See `package_key_name` attribute. To fetch the `PACKAGE_ID`, you need to access [Package ID](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/getAllObjects?objectFilter={%22type%22:{%22keyName%22:{%22operation%22:%22BARE_METAL_CPU%22}}}){: external} URL to view the `ID`. Once you have the ID, for example provide `PACKAGE_ID` as `142`, fetch its details by accessing the URL `https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/142/getItems?objectMask=mask[prices[id,categories[id,name,categoryCode],capacityRestrictionType,capacityRestrictionMinimum,capacityRestrictionMaximum,locationGroupId]]`. Select a `GPU` key name from the resulting available `GPU` key names where category code is `gpu0`. **Note**: To view the package ID. Log in to the [IBM Cloud Classic Infrastructure API](https://api.softlayer.com/rest/v3/SoftLayer_Hardware/getCreateObjectOptions.json) that uses your API key as the password. For more information, about creating classic infrastructure keys and locating your VPN username and password, refer [Managing classic infrastructure API keys](/docs/account?topic=account-classic_keys). |
|`gpu_secondary_key_name`|String|Optional|The key name for the secondary Graphics Processing Unit (GPU). For example, `GPU_NVIDIA_GRID_K2`. Key names can be fetched in the similar way as `gpu_key_name` and  category code is `gpu1`.|
|`hourly_billing`|Boolean|Required|The billing type for the instance. When set to `true`, the compute instance is billed on hourly usage. Otherwise, the instance is billed monthly. The default value is `true`.|
|`redundant_power_supply`|Boolean|Optional|When the value is `true`, more power supply is provided.|
|`redundant_network`|Boolean|Optional|When the value is `true`, two physical network interfaces are provided with a bonding configuration. The default value is `false`.|
|`unbonded_network`|Boolean|Optional|When the value is `true`, two physical network interfaces are provided without a bonding configuration. The default value is `false`.|
|`network_speed`|Integer|Optional|The connection speed, expressed in Mbps,  for the instance's network components. The default value is `100`.|
|`private_network_only`|Boolean|Optional|Specifies whether the instance has only access to the private network. When the value is `true`, a compute instance has only access to the private network. The default value is `false`.|
|`extended_hardware_testing`|Boolean|Optional|Enable the extended hardware testing while the Bare Metal server. The default value is `false`. **Note**: Enabling the `extended_hardware_testing` cause considerable delays in the deployment.|
|`ipv6_enabled`|Boolean|Optional|The primary public IPv6 address. The default value is `false`.|
|`ipv6_static_enabled`|Boolean|Optional|The public static IPv6 address block of `/64`. The default value is `false`.|
|`secondary_ip_count`|Integer|Optional|Specifies secondary public IPv4 addresses. Accepted values are `4` and `8`.|
|`image_template_id`|Integer|Optional|The image template ID you want to use to provision the computing instance. This is not the global identifier (UUID), but the image template group ID that should point to a valid global identifier. To retrieve the image template ID from the IBM Cloud infrastructure customer portal, navigate to **Devices > Manage > Images**, click the image that you want, and note the ID number in the resulting URL.       **NOTE**: Conflicts with `os_reference_code`. |

#### Input parameters for hourly Bare Metal servers


|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`fixed_config_preset`|String|Required|The configuration preset with which you want to provision the Bare Metal server. This preset governs the type of CPU, number of cores, amount of RAM, and number of hard disks that the Bare Metal server has. To see the available presets, log in to the [IBM Cloud Classic Infrastructure API](https://api.softlayer.com/rest/v3/SoftLayer_Hardware/getCreateObjectOptions.json) that uses your API key as the password. For more information, about creating classic infrastructure keys and locating your VPN username and password, refer [Managing classic infrastructure API keys](/docs/account?topic=account-classic_keys).  You can search for `fixedConfigurationPresets` to view the presets key names. **Note**: The `fixedConfigurationPresets` key names are displayed in the `JSON` or `txt` format.|
|`os_reference_code`|String|Optional|An operating system reference code that provisions the computing instance. To see available OS reference codes, log in to the [IBM Cloud Classic Infrastructure API](https://api.softlayer.com/rest/v3/SoftLayer_Virtual_Guest_Block_Device_Template_Group/getVhdImportSoftwareDescriptions.json?objectMask=referenceCode), that uses your API key as the password.         **NOTE**: Conflicts with `image_template_id`.  |
|`software_guard_extensions`|Boolean|Optional|The Software Guard Extensions product is added to a compatible server package, selecting `Intel SGX-enabled BIOS` and `hardware`. The default value is `false`.|

#### Input parameters for monthly Bare Metal servers

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`public_vlan_id`|Integer|Optional|The public VLAN to be used for the public network interface of the instance. You can find accepted values in the [VLAN networks](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want and notes the ID in the resulting URL.|
|`private_vlan_id`|Integer|Optional|The private VLAN to be used for the private network interface of the instance. You can find accepted values in the [VLAN networks](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want and notes the ID in the resulting URL.|
|`public_subnet`|String|Optional|The public subnet to be used for the public network interface of the instance. Accepted values are primary public networks. You can find accepted values in the [subnets Docs](https://cloud.ibm.com/classic/network/subnets).|
|`private_subnet`|String|Optional|The private subnet to be used for the private network interface of the instance. Accepted values are primary private networks. You can find accepted values in the [subnets Docs](https://cloud.ibm.com/classic/network/subnets).|
|`package_key_name`|String|Optional|The key name for the monthly Bare Metal server's package.Use this argument when you create a new monthly Bare Metal server. You can find available package key names in the {{site.data.keyword.cloud_notm}} API URL `https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/getAllObjects?objectFilter={"type":{"keyName":{"operation":"BARE_METAL_CPU"}}}`, that uses your API key as the password.|
|`process_key_name`|String|Optional| The key name for the monthly Bare Metal server's process. Use this argument when you create a new monthly Bare Metal server. To get a process key name, first find the package key name in the [{{site.data.keyword.cloud_notm}} API](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/getAllObjects?objectFilter={"type":{"keyName":{"operation":"BARE_METAL_CPU"}}}). To fetch the `PACKAGE_ID`, you need to access [Package ID](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/getAllObjects?objectFilter={%22type%22:{%22keyName%22:{%22operation%22:%22BARE_METAL_CPU%22}}}){: external} URL to view the `ID`. Once you have the ID, for example provide `PACKAGE_ID` as `142`. Then, replace <PACKAGE_ID> with your package key name in the following URL `https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/142/getItems?objectMask=mask[prices[id,categories[id,name,categoryCode],capacityRestrictionType,capacityRestrictionMinimum,capacityRestrictionMaximum,locationGroupId]]`. Select a process key name from the resulting available process key names. **Note**: To view the package ID. log in to the [IBM Cloud Classic Infrastructure API](https://api.softlayer.com/rest/v3/SoftLayer_Hardware/getCreateObjectOptions.json) that uses your API key as the password. For more information, about creating classic infrastructure keys and locating your VPN username and password, refer [Managing classic infrastructure API keys](/docs/account?topic=account-classic_keys).|
|`disk_key_names`|Array of string|Optional| The internal key names for the monthly Bare Metal server's disk. Use this argument when you create a new monthly Bare Metal server. To get disk key names, first find the package key name in the [{{site.data.keyword.cloud_notm}} API](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/getAllObjects?objectFilter={"type":{"keyName":{"operation":"BARE_METAL_CPU"}}}). Then, replace <PACKAGE_NAME> with your package key name in the following [URL](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/PACKAGE_NAME/getItems?objectMask=mask[prices[id,categories[id,name,categoryCode],capacityRestrictionType,capacityRestrictionMinimum,capacityRestrictionMaximum,locationGroupId]]). Select disk key names from the resulting available disk key names.|
|`os_key_name`|String|Optional| The operating system key name that you want to use to provision the computing instance. To get disk key names, first find the package key name in the [{{site.data.keyword.cloud_notm}} API](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/getAllObjects?objectFilter={"type":{"keyName":{"operation":"BARE_METAL_CPU"}}}). Then, replace <PACKAGE_NAME> with your package key name in the following [URL](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/<PACKAGE_NAME>/getItems?objectMask=mask[prices[id,categories[id,name,categoryCode],capacityRestrictionType,capacityRestrictionMinimum,capacityRestrictionMaximum,locationGroupId]]). Select an OS key name from the resulting available OS key names.|
|`public_bandwidth`|Integer|Optional| The amount of public network traffic, which is specified in gigabytes, allowed per month. The value can be greater than 0 when `private_network_only` is set to `false` and the server is a monthly based server.|
|`memory`|Integer|Optional| The amount of memory, which is specified in gigabytes, for the server.|
|`storage_groups`|List of objects|Optional| Configurations for RAID and partition.   |
|`storage_groups.array_type_id`|Integer|Required|The RAID type. You can retrieve the value from the [{{site.data.keyword.cloud_notm}} API](https://api.softlayer.com/rest/v3/SoftLayer_Configuration_Storage_Group_Array_Type/getAllObjects).    |
|`storage_groups.hard_drives`|Array of integers|Required|The index of hard disks for RAID configuration. The index starts at 0. For example, the array [0,1] is an index of two hard disks.    |
|`storage_groups.array_size`|Integer|Optional| The target RAID disk size, specific in gigabytes.    |
|`storage_groups.partition_template_id`|String|Optional| The partition template ID for the OS disk. Templates are different based on the target OS. To get the partition template ID, first find the OS ID in the [{{site.data.keyword.cloud_notm}} API](https://api.softlayer.com/rest/v3/SoftLayer_Hardware_Component_Partition_OperatingSystem/getAllObjects). Then, replace <OS_ID> with your OS ID in the following URL `https://api.softlayer.com/rest/v3/SoftLayer_Hardware_Component_Partition_OperatingSystem/<OS_ID>/getPartitionTemplates`. Select your template ID in resulting available partition template IDs.  |
|`software_guard_extensions`|Boolean|Optional| The Software Guard Extensions product is added to a compatible server package, selecting Intel SGX-enabled BIOS and hardware. The default value is `false`.|
|`restricted_network`|Boolean|Optional| The non-datacenter restricted port speed. The default value is `false`.|
|`tcp_monitoring`|Boolean|Optional| When the value is `false`, a ping monitoring service is provided. When the value is `true`, a ping monitoring service and a TCP monitoring service are provided.#### Arguments for quote-based Bare Metal servers|

#### Input parameters for quote-based Bare Metal servers

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`public_vlan_id`|Integer|Optional|The public VLAN to be used for the public network interface of the instance. You can find accepted values in the [VLAN network](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want and notes the ID in the resulting URL.|
|`private_vlan_id`|Integer|Optional|The private VLAN to be used for the private network interface of the instance. You can find accepted values in the [VLAN network](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want and notes the ID in the resulting URL.|
|`public_subnet`|String|Optional|The public subnet to be used for the public network interface of the instance. Accepted values are primary public networks. You can find accepted values in the [subnets Docs](https://cloud.ibm.com/classic/network/subnets).|
|`private_subnet`|String|Optional| The private subnet to be used for the private network interface of the instance. Accepted values are primary private networks. You can find accepted values in the [subnets Docs](https://cloud.ibm.com/classic/network/subnets).|
|`quote_id`|String|Optional|When you define `quote_id`, Terraform on {{site.data.keyword.cloud_notm}} uses specifications in the quote to create a Bare Metal server. You can find the quote ID in the [IBM Cloud infrastructure customer portal](https://cloud.ibm.com/classic) by navigating to **Account > Sales > Quotes**.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #bm-output}
Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the Bare Metal server.|
|`public_ipv4_address`|String|The public IPv4 address of the Bare Metal server.|
|`public_ipv4_address_id`|String|The unique identifier for the public IPv4 address of the Bare Metal server.|
|`private_ipv4_address`|String|The private IPv4 address of the Bare Metal server.|
|`private_ipv4_address_id`|String|The unique identifier for the private IPv4 address of the Bare Metal server.|
|`ipv6_address`|String|The public IPv6 address of the Bare Metal server instance provided when `ipv6_enabled` is set to `true`.|
|`ipv6_address_id`|String|The unique identifier for the public IPv6 address of the Bare Metal server.|
|`secondary_ip_addresses`|String|The public secondary IPv4 addresses of the Bare Metal server instance when `secondary_ip_count` is set to nonzero value.|
|`global_identifier`|String|The unique global identifier of the Bare Metal server.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_compute_dedicated_host`
{: #dedicated-host}

Provides a Dedicated Host resource. This allows dedicated host to be created, updated, and canceled.

For more information, refer to the [{{site.data.keyword.cloud_notm}} API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Virtual_DedicatedHost).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dedicated-host-sample}

In the following example, you can create a dedicated host:

```
resource "ibm_compute_dedicated_host" "dedicatedhost" {
  hostname        = "host"
  domain          = "example.com"
  router_hostname = "bcr01a.dal09"
  datacenter      = "dal09"
}

```
{: codeblock}

### Input parameters
{: #dedicated-host-input}

The following arguments are supported:

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------| -------| ---------- | ------- |
|`datacenter`| String | Required | The data center in which the dedicated host resides.| Yes |
|`hostname`| String | Required | The host name of dedicated host.| No |
|`domain`| String | Required | The domain of dedicated host.| Yes |
|`router_hostname`| String | Required | The hostname of the primary router associated with the dedicated host.| Yes |
|`hourly_billing`| Boolean | Optional | The billing type for the host. When set to `true`, the dedicated host is billed on hourly usage. Otherwise, the dedicated host is billed monthly. The default value is `true`.| Yes |
|`flavor`| String | Optional | The flavor of dedicated host. Default value `56_CORES_X_242_RAM_X_1_4_TB`. [Log in to the IBM-Cloud Infrastructure API to see available flavor types](https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/813/getItems.json). Use your API as the password to log in. Log in and find the key called `keyName`.| Yes |
|`wait_time_minutes`| Integer | Optional | The duration, expressed in minutes to wait for the dedicated host to become available before creation. The default value is `90`.| No |
|`tags`| Array of String | Optional | Tags associated with the dedicated host.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dedicated-host-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the dedicated host.|
|`cpu_count`|The capacity that the dedicated host's CPU allocation is restricted to.|
|`disk_capacity`|The capacity that the dedicated host's disk allocation is restricted to.|
|`memory_capacity`|The capacity that the dedicated host's memory allocation is restricted to.### Import `ibm_compute_dedicated_host` can be imported by using the ID. For example, ```$ terraform import ibm_compute_dedicated_host.dedicatedhost 238756```|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_compute_monitor`
{: #compute-monitor}

Create, update, or delete a monitor for your virtual server instance. With monitors, you can verify the health of your virtual server instance by sending ping requests to the instance and checking the responsiveness of your instance. For more information, see [Viewing and managing monitors](/docs/vpc?topic=vpc-managing-virtual-server-instances).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #compute-monitor-sample}

In the following example, you can create a monitor:

```
resource "ibm_compute_monitor" "test_monitor" {
    guest_id = ibm_compute_vm_instance.test_server.id
    ip_address = ibm_compute_vm_instance.test_server.id.ipv4_address
    query_type_id = 1
    response_action_id = 1
    wait_cycles = 5
    notified_users = [460547]
}
```
{: codeblock}

### Input parameters
{: #compute-monitor-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------- | -------- | ------- |
|`guest_id`| Integer | Required | The ID of the virtual guest that you want to monitor.| Yes |
|`ip_address`| String | Optional | The IP address that you want to monitor.| No |
|`query_type_id`| Integer | Required | The ID of the query type.| No |
|`response_action_id`| Integer | Required, | The ID of the response action to take if the monitor fails. Accepted values are `1` or `2`.| No |
|`wait_cycles`| Integer | Optional | The number of 5-minute cycles to wait before the response action is taken.| No |
|`notified_users`| Array of Integers | Optional | The list of user IDs that is notified.| No |
|`tags`| Array of Integers | Optional | Tags associated with the monitoring instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #compute-monitor-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the monitor.|
|`notified_users`|The list of user IDs that is notified.|
{: caption="Table 1. Available output parameters" caption-side="top"}





## `ibm_compute_placement_group`
{: #plmt-group}

Create, update, or delete a placement group for your virtual server instance. With placement groups, you can control the physical host your virtual server instance is deployed to. For more information, see [Placement groups](/docs/virtual-servers?topic=virtual-servers-placement-groups). 

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #plmt-group-sample}

```
resource "ibm_compute_placement_group" "test_placement_group" {
    name = "test"
    pod = "pod01"
    datacenter = "dal05"  
}
```
{: codeblock}

### Input parameters
{: #plmt-group-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ----|-----------| -----------| 
|`name`| String | Required | The descriptive that is used to identify a placement group.| No |
|`datacenter`| String | Required | The datacenter in which you want to provision the placement group.| Yes |
|`pod`| String | Required |  The data center pod where you want to create the placement group. To find the pod, run `ibmcloud sl placement-group create-options` and select one of the **Back-end Router IDs** for the data center where you want to create the placement group. | Yes |
|`rule`| String | Optional | The rule of the placement group. Default `SPREAD`. | Yes |
|`tags`| Array of Strings | Optional | Tags associated with the placement group.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #plmt-group-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the new placement group.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #plmt-group-timeouts}

The `timeouts` block allows you to specify [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) for certain actions:  

|Name|Description|
|----|-----------|
|`delete`|(Defaults to 10 mins) Used when you delete the placement group. There might be Virtual Guest resources on the placement group. The placement group delete request is issued once there are no Virtual Guests on the placement group.|
{: caption="Table. Available timeout configuration options" caption-side="top"}


## `ibm_compute_provisioning_hook`
{: #provision-hook}

Provides provisioning hooks that contains all the information that is needed to add a hook into a server or virtual provision and OS reload. This allows provisioning hooks to be created, updated, and deleted.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Provisioning_Hook).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #provision-hook-sample}

```
resource "ibm_compute_provisioning_hook" "test_provisioning_hook" {
    name = "test_provisioning_hook_name"
    uri  = "https://raw.githubusercontent.com/test/slvm/master/test-script.sh"
}
```
{: codeblock}

### Input parameters
{: #provision-hook-input}

The following arguments are supported:

|Name|Description|
|----|-----------|
|`name`|(Required, string) The descriptive name that is used to identify a provisioning hook.|
|`uri`|(Required, string) The endpoint from which the script is downloaded or downloaded and executed.|
|`tags`|(Optional, array of strings) Tags associated with the provisioning hook instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #provision-hook-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the new provisioning hook.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_compute_ssh_key`
{: #ssh-key}

Provide an SSH key resource. This allows SSH keys to be created, updated, and deleted.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Security_Ssh_Key).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ssh-key-sample}

```
resource "ibm_compute_ssh_key" "test_ssh_key" {
    label = "test_ssh_key_name"
    notes = "test_ssh_key_notes"
    public_key = "ssh-rsa <rsa_public_key>"
}
```
{: codeblock}

### Input parameters
{: #ssh-key-input}

The following arguments are supported:

|Name|Description|
|----|-----------|
|`label`|(Required, string) The descriptive name that is used to identify an SSH key.|
|`public_key`|(Required, string) The public SSH key.|
|`notes`|(Optional, string) Descriptive text about the SSH key.|
|`tags`|(Optional, array of strings) Tags associated with the SSH Key instance.   **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #ssh-key-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the new SSH key.|
|`fingerprint`|The sequence of bytes to authenticate or look up a longer SSH key.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_compute_ssl_certificate`
{: #ssl-compute-cert}

Provides an SSL certificate resource. This allows SSL certificates to be created, updated, and deleted.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer) security certificates Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Security_Certificate).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ssl-compute-cert-sample}

In the following example, you can use a certificate on file:

```
resource "ibm_compute_ssl_certificate" "test_cert" {
  certificate = file("cert.pem")
  private_key = file("key.pem")
}
```
{: codeblock}

You can also use an inline certificate:

```
resource "ibm_compute_ssl_certificate" "test_cert" {
    certificate = <<EOF
[......] # cert contents
-----END CERTIFICATE-----
    EOF

    private_key = <<EOF
-----BEGIN RSA PRIVATE KEY-----
[......] # cert contents
-----END RSA PRIVATE KEY-----
    EOF
}
```
{: codeblock}

### Input parameters
{: #ssl-compute-cert-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`certificate`| String | Required | The certificate provided publicly to clients requesting identity credentials.| Yes |
|`intermediate_certificate`| String | Optional | The certificate from the intermediate certificate authority, or chain certificate, that completes the chain of trust. Required when clients only trust the root certificate.| Yes |
|`private_key`| String | Required | The private key in the key/certificate pair.| Yes |
|`tags`| Array of Strings | Optional |  Tags associated with the security certificates instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #ssl-compute-cert-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`common_name`|The common name encoded within the certificate. This name is usually a domain name.|
|`create_date`|The date the certificate record was created.|
|`id`|The ID of the certificate record.|
|`key_size`|The size, expressed in number of bits, of the public key represented by the certificate.|
|`modify_date`|The date the certificate record was last modified.|
|`organization_name`|The organizational name encoded in the certificate.|
|`validity_begin`|The UTC timestamp representing the beginning of the certificate's validity.|
|`validity_days`|The number of days remaining in the validity period for the certificate.|
|`validity_end`|The UTC timestamp representing the end of the certificate's validity period.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_compute_user`
{: #compute-user}

Provides a SoftLayer user resource. This allows you to retrieve, create, update, and delete either SoftLayer or IBMId accounts.

### SoftLayer Account
If you use this resource to create SoftLayer local credentials, you need to define the `username` and `password` arguments.

To access the SoftLayer portal, the user can log in with the username and password.

To access the SoftLayer API, the user can log in with the username and API key. An `api_key` is generated by SoftLayer when the `has_api_key` flag is `true`.

If the {{site.data.keyword.cloud_notm}} API [`getBlueIdAuthenticationRequiredFlag`](https://api.softlayer.com/rest/v3/SoftLayer_Account/getBlueIdAuthenticationRequiredFlag) returns `false`, the account is a local account.

#### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #compute-user-sample}

The following example shows how to use this resource with SoftLayer accounts:

```
resource "ibm_compute_user" "joe" {
    address1     = "12345 Any Street"
    address2     = "Suite #99"
    city         = "Atlanta"
    company_name = "Comp Inc"
    country      = "US"
    email        = "joe@doe.com"
    first_name   = "Joe"
    has_api_key  = false
    last_name    = "Doe"
    username     = "testuser"
    password     = "Change3Me!"
    permissions  = [
        "ACCESS_ALL_GUEST",
        "ACCESS_ALL_HARDWARE",
        "SERVER_ADD",
        "SERVER_CANCEL",
        "RESET_PORTAL_PASSWORD"
    ]
    state        = "GA"
    timezone     = "EST"
}
```
{: codeblock}

### IBMId Account
You can use an IBMId instead of your SoftLayer credentials. An [IBMId](https://www.ibm.com/account/profile/us) is used as a consistent way to access IBM products. You can create an IBMId in advance.

If you use this resource for an IBMId account, the resource should not contain `username` and `password` arguments. The user name is generated by SoftLayer by combining the IBMId account number and the IBMId email address. The password is not used in an IBMId account.

To access the SoftLayer portal, the user can log in with the IBMId.

To access the SoftLayer API, the user can log in with the username generated by SoftLayer and the API key. An `api_key` is generated by SoftLayer when the `has_api_key` flag is `true`.

If the {{site.data.keyword.cloud_notm}} API [`getBlueIdAuthenticationRequiredFlag`](https://api.softlayer.com/rest/v3/SoftLayer_Account/getBlueIdAuthenticationRequiredFlag)
returns `true`, the account is an IBMId.

#### Example Usage

The following example shows how to use this resource with IBMId accounts:

```
resource "ibm_compute_user" "joe" {
    address1     = "12345 Any Street"
    address2     = "Suite #99"
    city         = "Atlanta"
    company_name = "Comp Inc"
    country      = "US"
    email        = "joe@doe.com"
    first_name   = "Joe"
    has_api_key  = false
    last_name    = "Doe"
    permissions  = [
        "ACCESS_ALL_GUEST",
        "ACCESS_ALL_HARDWARE",
        "SERVER_ADD",
        "SERVER_CANCEL",
        "RESET_PORTAL_PASSWORD"
    ]
    state        = "GA"
    timezone     = "EST"
}
```


**NOTE**: An [IBMId](https://www.ibm.com/account/profile/us) is used as a consistent way to access IBM products. You can create an IBMId in advance.

For more information, see the [SoftLayer API documentation](http://sldn.softlayer.com/reference/datatypes/SoftLayer_User_Customer).

### Input parameters
{: #compute-user-input}

The following arguments are supported:

|Name|Description|
|----|-----------|
|`address1`|(Required, string) The first line of the user's street address.|
|`address2`|(Optional, string) The second line of the user's street address.|
|`city`|(Required, string) The user's city.|
|`company_name`|(Required, string) The user's company.|
|`country`|(Required, string) The user's country.|
|`email`|(Required, string) The email address associated with the account.|
|`first_name`|(Required, string) The user's given name.|
|`has_api_key`|(Optional, boolean) When the value is `true`, a SoftLayer API key is created for the user. The key is returned in the `api_key` attribute. When the value is `false`, any existing SoftLayer API keys for the user are deleted. The default value is `false`.|
|`last_name`|(Required, string) The user's last name.|
|`username`|(Required for SoftLayer accounts, optional for IBMId accounts, string) A unique name to identify a user globally across all SoftLayer login. The username is also the user login. Once a username is created, it cannot be changed. You must define a username when the account is a SoftLayer account. The user name is generated by SoftLayer when the account is an IBMId account. For example, if an IBMId had an account number of `1234567` and an email address (IBMId) of `test@example.com`, then SoftLayer would generate `1234567_test@example.com` as the username. This argument is optional for an IBMId account.|
|`password`|(Required for SoftLayer accounts, string) The initial password for the user account. The password is hashed and encoded before it is stored in the Terraform on {{site.data.keyword.cloud_notm}} state file. For an IBMId account, the password argument is ignored. For a SoftLayer account, the password must conform to SoftLayer's password policies to avoid failures.  Valid passwords must meet the following rules: <ul><li>Be 8 to 20 characters in length.</li><li>Have a combination of uppercase and lowercase characters. </li><li>Contain at least one number. </li><li>Contain at least one of the following special characters: <code>_</code>, <code>-</code>, <code>&#124;</code>, <code>@</code>, <code>.</code>, <code>,</code>, <code>?</code>, <code>/</code>, <code>!</code>, <code>~</code>, <code>#</code>, <code>$</code>, <code>%</code>, <code>^</code>, <code>&</code>, <code>*</code>, <code>(</code>, <code>)</code>, <code>{</code>, <code>}</code>, <code>[</code>, <code>]</code>, <code>=</code>.|
|`permissions`|(Optional, string) Permissions assigned to this user. This is a set of zero or more string values. See the [{{site.data.keyword.cloud_notm}} API Documentation for user permissions](https://sldn.softlayer.com/reference/datatypes/SoftLayer_User_Customer_CustomerPermission_Permission).|
|`state`|(Required, string) The state of a user's street address.|
|`timezone`|(Required, string) The user's time zone as a short name value (e.g., "EST"). For accepted values, see the [{{site.data.keyword.cloud_notm}} API Documentation for time zones](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Locale_Timezone).|
|`user_status`|(Optional, string) The user's log in status. You can find accepted values in the [{{site.data.keyword.cloud_notm}} API Documentation for user status](http://sldn.softlayer.com/reference/datatypes/SoftLayer_User_Customer_Status). The default value is `ACTIVE`.|
|`tags`|(Optional, array of strings) Tags associated with the user account instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #compute-user-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`api_key`| The SoftLayer API key that is created for the user.|
|`id`| The unique SoftLayer identifier that is created for the user.|
|`ibm_id`| The username for IBMId accounts. This attribute is generated by SoftLayer when the IBMId is activated.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### More Notes

In SoftLayer, there is a delay when user logins are deleted from SoftLayer back-end systems. SoftLayer acknowledges delete requests and immediately updates the user status to `CANCEL_PENDING`. The actual deletion from the SoftLayer system processes at an unspecified time in the future. This delay might be significant, especially during your project's testing phase. You may receive an error if you create a user login, then delete it, and then create it again. This results in an error because the SoftLayer back-end has not completely processed the previous delete operation. If you want to create, delete, and re-create a user login, you must specify a new, globally-unique username in your subsequent requests.


## `ibm_compute_vm_instance`
{: #vm}

Provides a resource for VM instances. This allows VM instances to be created, updated, and deleted.

For more information, see the [IBM Cloud Classic Infrastructure API Docs](http://sldn.softlayer.com/reference/services/SoftLayer_Virtual_Guest).

**NOTE**: Update is not supported when the `bulk_vms` parameter is used.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vm-sample}

In the following example, you can create a VM instance by using a Debian image:

```
resource "ibm_compute_vm_instance" "twc_terraform_sample" {
    hostname = "twc-terraform-sample-name"
    domain = "bar.example.com"
    os_reference_code = "DEBIAN_8_64"
    datacenter = "wdc01"
    network_speed = 10
    hourly_billing = true
    private_network_only = false
    cores = 1
    memory = 1024
    disks = [25, 10, 20]
    user_metadata = "{\"value\":\"newvalue\"}"
    dedicated_acct_host_only = true
    local_disk = false
    public_vlan_id = 1391277
    private_vlan_id = 7721931
    private_security_group_ids = [576973]
}
```
{: codeblock}

In the following example, you can create a VM instance by using a block device template:

```
resource "ibm_compute_vm_instance" "terraform-sample-BDTGroup" {
   hostname = "terraform-sample-blockDeviceTemplateGroup"
   domain = "bar.example.com"
   datacenter = "ams01"
   public_network_speed = 10
   hourly_billing = false
   cores = 1
   memory = 1024
   local_disk = false
   image_id = 12345
   tags = [
     "collectd",
     "mesos-master"
   ]
   public_subnet = "50.97.46.160/28"
   private_subnet = "10.56.109.128/26"
}
```
{: codeblock}

In the following example, you can create a VM instance by using a flavor:

```
resource "ibm_compute_vm_instance" "terraform-sample-flavor" {
    hostname = "terraform-sample-flavor"
    domain = "bar.example.com"
    os_reference_code = "DEBIAN_8_64"
    datacenter = "dal06"
    network_speed = 10
    hourly_billing = true
    local_disk = false
    private_network_only = false
    flavor_key_name = "B1_2X8X25"
    user_metadata = "{\\\"value\\\":\\\"newvalue\\\"}"
    // provide disk 3, 4, 5 and so on
    disks = [10, 20, 30]
    tags = ["collectd"]
    // It should be false
    dedicated_acct_host_only = false
    ipv6_enabled = true
    secondary_ip_count = 4
    notes = "VM notes"
}
```
{: codeblock}

In the following example, you can create multiple virtual machines.

```
resource "ibm_compute_vm_instance" "terraform-bulk-vms" {
  bulk_vms = [{
    hostname = "vm1"

    domain = "bar.example.com"
  },
    {
      hostname = "vm2"

      domain = "bar.example.com"
    },
  ]

  os_reference_code    = "CENTOS_7_64"
  datacenter           = "dal09"
  network_speed        = 100
  hourly_billing       = true
  private_network_only = true
  cores                = 1
  memory               = 1024
  disks                = [25]
  local_disk           = false
}
```
{: codeblock}

In the following example, you can retry to create a VM instance by using a datacenter_choice. If VM fails to place order on first datacenter or VLANs it retries to place order on subsequent data centers and VLANs until place order is successful:

```
resource "ibm_compute_vm_instance" "terraform-retry" {
  hostname          = "vmretry"
  domain            = "example.com"
  network_speed     = 100
  hourly_billing    = true
  cores             = 1
  memory            = 1024
  local_disk        = false
  os_reference_code = "DEBIAN_7_64"
  disks             = [25]

  datacenter_choice = [
    {
      datacenter      = "dal09"
      public_vlan_id  = 123245
      private_vlan_id = 123255
    },
    {
      datacenter = "wdc54"
    },
    {
      datacenter      = "dal09"
      public_vlan_id  = 153345
      private_vlan_id = 123255
    },
    {
      datacenter = "dal06"
    },
    {
      datacenter      = "dal09"
      public_vlan_id  = 123245
      private_vlan_id = 123255
    },
    {
      datacenter      = "dal09"
      public_vlan_id  = 1232454
      private_vlan_id = 1234567
    },
  ]
}

```
{: codeblock}

In the following example, you create a VM instance by using a quote ID: 
```
resource "ibm_compute_vm_instance" "vm1" {
  # Mandatory fields
  hostname             = "terraformquote"
  domain               = "IBM.cloud"
  quote_id             = "2877000"

  # Optional fields
  os_reference_code    = "DEBIAN_9_64"
  datacenter           = "dal06"
  network_speed        = 100
  hourly_billing       = false
  private_network_only = false
  flavor_key_name      = "B1_2X8X100"
  local_disk           = true
}
```
{: codeblock}


### Input parameters
{: #vm-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`hostname`|String|Optional|The hostname for the computing instance. If you set this option, do not specify `bulk_vms` at the same time. | No |
|`domain`|String|Optional|The domain for the computing instance. If you set this option, do not specify `bulk_vms` at the same time.| No |
|`bulk_vms`|List of objects|Optional|List of hostname and domain of the computing instance. The minimum number of vm's to be defined is 2.   | Yes |
|`bulk_vms.hostname`|String|Required|The hostname for the computing instance.    |
|`bulk_vms.domain`|String|Required| The domain for the computing instance. If you set this option, do not specify `hostname` and `domain` at the same time.| Yes |
|`cores`|Integer|Optional|The number of CPU cores that you want to allocate. If you set this option, do not specify `flavor_key_name` at the same time.| No |
|`memory`|Integer|Optional|The amount of memory, expressed in megabytes, that you want to allocate. If you set this option, do not specify `flavor_key_name` at the same time.| No |
|`flavor_key_name`|String|Optional|The flavor key name that you want to use to provision the instance. To see available key name, log in to the [IBM Cloud Classic Infrastructure API](https://api.softlayer.com/rest/v3/SoftLayer_Virtual_Guest/getCreateObjectOptions.json), that uses your API key as the password. If you set this option, do not specify `cores` and `memory` at the same time.| No |
|`datacenter`|String|Optional|The data center in which you want to provision the instance. **NOTE**: If `dedicated_host_name` or `dedicated_host_id`    is provided then the datacenter should be same as the dedicated host datacenter.     If `placement_group_name` or `placement_group_id`    is provided then the datacenter should be same as the placement group datacenter.    Conflicts with `datacenter_choice`. | Yes |
|`hourly_billing`|Boolean|Optional| The billing type for the instance. When set to `true`, the computing instance is billed on hourly usage. Otherwise, the instance is billed monthly. The default value is `true`.| Yes |
|`local_disk`|Boolean|Optional|The disk type for the instance. When set to `true`, the disks for the computing instance are provisioned on the host that the instance runs. Otherwise, SAN disks are provisioned. The default value is `true`.| Yes |
|`dedicated_acct_host_only`|Boolean|Optional| Specifies whether the instance must only run on hosts with instances from the same account. The default value is `false`. If VM is provisioned by using `flavorKeyName`, value should be set to `false`.        **NOTE**: Conflicts with `dedicated_host_name`, `dedicated_host_id`, `placement_group_name` and `placement_group_id`.| Yes |
|`dedicated_host_id`|Integer|Optional|Specifies [dedicated host](/docs/virtual-servers?topic=virtual-servers-dedicated-virtual-servers) for the instance by its ID. **NOTE**: Conflicts with `dedicated_acct_host_only`, `dedicated_host_name`, `placement_group_name` and `placement_group_id`.| Yes |
|`dedicated_host_name`|String|Optional|Specifies [dedicated host](/docs/virtual-servers?topic=virtual-servers-dedicated-virtual-servers) for the instance by its name. **NOTE**: Conflicts with `dedicated_acct_host_only`, `dedicated_host_id`, `placement_group_name` and `placement_group_id`.| Yes |
|`placement_group_id`|Integer|Optional|Specifies [placement group](/docs/virtual-servers?topic=virtual-servers-dedicated-virtual-servers) for the instance by its ID. **NOTE**: Conflicts with `dedicated_acct_host_only`, `dedicated_host_name`, `dedicated_host_id` and `placement_group_name`.| Yes |
|`placement_group_name`|String|Optional|Specifies [placement group](/docs/virtual-servers?topic=virtual-servers-dedicated-virtual-servers) for the instance by its name.        **NOTE**: Conflicts with `dedicated_acct_host_only`, `dedicated_host_id`, `dedicated_host_name` and `placement_group_id`| Yes |
|`transient`|Boolean|Optional|Specifies whether to provision a transient virtual server. The default value is `false`. Transient instances cannot be upgraded or downgraded. Transient instances cannot use local storage.       **NOTE**: Conflicts with `dedicated_acct_host_only`, `dedicated_host_id`, `dedicated_host_name`, `cores`, `memory`, `public_bandwidth_limited` and `public_bandwidth_unlimited`| Yes |
|`os_reference_code`|String|Optional|The operating system reference code that is used to provision the computing instance. To see available OS reference codes, log in to the [IBM Cloud Classic Infrastructure API](https://api.softlayer.com/rest/v3/SoftLayer_Virtual_Guest_Block_Device_Template_Group/getVhdImportSoftwareDescriptions.json?objectMask=referenceCode), that uses your API key as the password.       **NOTE**: Conflicts with `image_id`.| Yes |
|`image_id`|Integer|Optional| The image template ID that you want to use to provision the computing instance. This is not the global identifier (UUID), but the image template group ID that should point to a valid global identifier. To retrieve the image template ID from the IBM Cloud infrastructure customer portal, navigate to **Devices > Manage > Images**, click the image that you want, and note the ID number in the resulting URL. **NOTE**: Conflicts with `os_reference_code`. | Yes |
|`network_speed`|Integer|Optional|The connection speed (in Mbps) for the instance's network components. The default value is `100`| No |
|`private_network_only`|Boolean|Optional|When set to `true`, a compute instance has only access to the private network. The default value is `false`.| Yes |
|`private_security_group_ids`|Array of integers|Optional| The IDs of security groups to apply on the private interface. This attribute can't be updated. You can use this parameter to add a security group to your virtual server instance when you create it. If you want to add or remove security groups later, you must use the `ibm_network_interface_sg_attachment` resource. If you use this attribute in addition to `ibm_network_interface_sg_attachment` resource you might experience errors. So use one of these consistently for a particular virtual server instance.| Yes |
|`public_vlan_id`|Integer|Optional| The public VLAN ID for the public network interface of the instance. Accepted values are in the [VLAN doc](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want and notes the ID number in the browser URL. You can also refer to a VLAN name by using a data source. **NOTE**: Conflicts with `datacenter_choice`.| Yes |
|`private_vlan_id`|Integer|Optional|The private VLAN ID for the private network interface of the instance. You can find accepted values in the [VLAN doc](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want to use and note the ID number in the browser URL. You can also refer to a VLAN name by using a data source. **NOTE**: Conflicts with `datacenter_choice`.| Yes |
|`public_security_group_ids`|Array of integers|Optional|The IDs of security groups to apply on the public interface. This attribute can't be updated. You can use this parameter to add a security group to your virtual server instance when you create it. If you want to add or remove security groups later, you must use the `ibm_network_interface_sg_attachment` resource. If you use this attribute in addition to `ibm_network_interface_sg_attachment` resource, you might experience errors. So use one of these consistently for a particular virtual server instance.| Yes |
|`public_subnet`|String|Optional| The public subnet for the public network interface of the instance. Accepted values are primary public networks. You can find accepted values in the [subnets doc](https://cloud.ibm.com/classic/network/subnets).| Yes |
|`private_subnet`|String|Optional| The private subnet for the private network interface of the instance. Accepted values are primary private networks. You can find accepted values in the [subnets doc](https://cloud.ibm.com/classic/network/subnets).| Yes |
|`disks`|Array of integers|Optional| The numeric disk sizes in GBs for the instance's block device and disk image settings. The default value is the smallest available capacity for the primary disk. If you specify an image template, the template provides the disk capacity. If you specify the `flavorKeyName`, first disk is provided by the flavor.| No |
|`user_metadata`|String|Optional|Arbitrary data to be made available to the computing instance.| Yes |
|`notes`|String|Optional| Descriptive text of up to 1000 characters about the VM instance.| No |
|`ssh_key_ids`|Array of integers|Optional| The SSH key IDs to install on the computing instance when the instance provisions.      **NOTE** If you don't know the ID(s) for your SSH keys, you can reference your SSH keys by their labels.| No |
|`file_storage_ids`|Array of integers|Optional| File storage to which this computing instance has access. File storage must be in the same data center as the Bare Metal server. If you use this argument to authorize, access to file storage, then do not use the `allowed_virtual_guest_ids` argument in the `ibm_storage_file` resource in order to prevent the same storage be added twice.| No |
|`block_storage_ids`|Array of integers|Optional| File storage to which this computing instance has access. File storage must be in the same data center as the Bare Metal server. If you use this argument to authorize, access to file storage, then do not use the `allowed_virtual_guest_ids` argument in the `ibm_storage_block` resource in order to prevent the same storage be added twice.| No |
|`post_install_script_uri`|String|Optional| The URI of the script to be downloaded and executed after installation is complete.| Yes |
|`tags`|Array of string|Optional| Tags associated with the VM instance. Permitted characters include: A-Z, 0-9, whitespace, `_` (underscore), `-` (hyphen), `.` (period), and `:` (colon). All other characters are removed.| No |
|`ipv6_enabled`|Boolean|Optional|The primary public IPv6 address. The default value is `false`.| Yes |
|`ipv6_static_enabled`|Boolean|Optional|The public static IPv6 address block of `/64`. The default value is `false`.| No |
|`secondary_ip_count`|Integer|Optional| Specifies secondary public IPv4 addresses. Accepted values are `4` and `8`.|  Yes |
|`wait_time_minutes`|Integer|Optional| The duration, expressed in minutes, to wait for the VM instance to become available before declaring it as created. It is also the same amount of time waited for no active transactions before proceeding with an update or deletion. The default value is `90`.| No |
|`wait_time_minutes`|Integer |Deprecated| Use Timeouts block to wait for the VM instance to become available, or while waiting for non active transactions before proceeding with an update or deletion. The default value is `90`.| No |
|`public_bandwidth_limited`|Integer|Optional| Allowed public network traffic in GB per month. It can be greater than 0 when the server is a monthly based server. Defaults to the smallest available capacity for the public bandwidth are used.       **NOTE**: Conflicts with `private_network_only` and `public_bandwidth_unlimited`.| Yes |
|`public_bandwidth_unlimited`|Boolean|Optional|  Allowed unlimited public network traffic in GB per month for a monthly based server. The `network_speed` should be 100 Mbps. Default value is `false`.       **NOTE**: Conflicts with `private_network_only` and `public_bandwidth_limited`.| Yes |
|`evault`|Integer|Optional|Allowed `Evault` in GB per month for monthly based servers.| Yes |
|`datacenter_choice`|List of objects|Optional|A nested block to describe datacenter choice options to retry on different data centers and VLANs. Nested `datacenter_choice` blocks must have the following structure:    | No |
|`datacenter_choice.datacenter`|String|Required|The datacenter in which you want to provision the instance.    | No |
|`datacenter_choice.public_vlan_id`|String|Optional|The public VLAN ID for the public network interface of the instance. Accepted values are in the [VLAN doc](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want to use and note the ID number in the browser URL. You can also refer to a VLAN name by using a data source.    | No |
|`datacenter_choice.private_vlan_id`|String|Optional|The private VLAN ID for the private network interface of the instance. You can find accepted values in the [VLAN doc](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want to use and note the ID number in the browser URL. You can also refer to a VLAN name by using a data source.  **NOTE**: Conflicts with `datacenter`, `private_vlan_id`, `public_vlan_id`, `placement_group_name` and `placement_group_id`.| Yes |
|`quote_id`|String|Optional|When you define the `quote_id`, Terraform uses the specification in the quote to create a virtual server. You can find the quote ID in the IBM Cloud portal.|Yes|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vm-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the VM instance.|
|`ipv4_address`|String|The public IPv4 address of the VM instance.|
|`ip_address_id_private`|String|The unique identifier for the private IPv4 address that is assigned to the VM instance.|
|`ipv4_address_private`|String|The private IPv4 address of the VM instance.|
|`ip_address_id`|String|The unique identifier for the public IPv4 address that is assigned to the VM instance.|
|`ipv6_address`|String|The public IPv6 address of the VM instance provided when `ipv6_enabled` is set to `true`.|
|`ipv6_address_id`|String|The unique identifier for the public IPv6 address assigned to the VM instance provided when `ipv6_enabled` is set to `true`.|
|`private_subnet_id`|String|The unique identifier of the subnet `ipv4_address_private` belongs to.|
|`public_ipv6_subnet`|String|The public IPv6 subnet provided when `ipv6_enabled` is set to `true`.|
|`public_ipv6_subnet_id`|String|The unique identifier of the subnet `ipv6_address` belongs to.|
|`public_subnet_id`|String|The unique identifier of the subnet `ipv4_address` belongs to.|
|`secondary_ip_addresses`|String|The public secondary IPv4 addresses of the VM instance.|
|`public_interface_id`|String|The ID of the primary public interface.|
|`private_interface_id`|String|The ID of the primary private interface.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_dns_domain`
{: #dns-domain}

Provides a single DNS domain managed on IBM Cloud Classic Infrastructure (SoftLayer). Domains contain general information about the domain name, such as the name and serial number.

Individual records, such as `A`, `AAAA`, `CTYPE`, and `MX` records, are stored in the domain's associated resource records by using the `ibm_dns_record` resource.


### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-domain-sample}

```
resource "ibm_dns_domain" "dns-domain-test" {
    name = "dns-domain-test.com"
    target = "127.0.0.10"
}
```
{: codeblock}

### Input parameters
{: #dns-domain-input}

The following arguments are supported:

|Name|Data type| Required / optional|Description|Forces new resource|
|----|-----------|-------|--------|--------|
|`name`| String | Required | The name of the domain. For example, "example.com". When the domain is created, proper `NS` and `SOA` records are created automatically for the domain.| Yes |
|`target`| String | Optional | The primary target IP address to which the domain resolves. When the domain is created, an `A` record with a host value of `@` and a data-target value of the IP address are provided and associated with the new domain.| No |
|`tags`| Array of Strings | Optional | Tags associated with the DNS domain instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dns-domain-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique internal identifier of the domain record.|
|`serial`|A unique number denoting the latest revision of the domain.|
|`update_date`|The date that the domain record was last updated.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_dns_domain_registration_nameservers`
{: #dns-register}

Configures the (custom) name servers associated with a DNS domain registration managed by the IBM Cloud DNS Registration Service. The default IBM Cloud name servers specified when the domain was initially registered are replaced with the values passed when this resource is created. 

This resource is typically used in conjunction with {{site.data.keyword.cis_full_notm}} to enable DNS services for the domain to be managed via {{site.data.keyword.cis_full_notm}}. All further configuration of the domain is then performed by using the Cloud Internet Services resource instances. To transfer management control, the IBM Cloud DNS domain registration is updated with the Internet Services specific name servers. This step is required before the domain in Cloud Internet Services becomes active and start serving web traffic. Using interpolation syntax, the computed name servers of the CIS resource are passed into this resource. 


### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-register-sample}

```
resource "ibm_dns_domain_registration_nameservers" "dnstestdomain" {
    dns_registration_id = data.ibm_dns_domain_registration.dnstestdomain.id
    name_servers = ibm_cis_domain.dnstestdomain.name_servers
}
data "ibm_dns_domain_registration" "dnstestdomain" {
    name = "dnstestdomain.com"
}
resource "ibm_cis_domain" "dnstestdomain" {
   
}
```
{: codeblock}

Or 

```
resource "ibm_dns_domain_registration_nameservers" "dns-domain-test" {
    dns_registration_id = data.ibm_dns_domain_registration.dns-domain-test.id
    name_servers = ["ns006.name.ibm.cloud.com", "ns017.name.ibm.cloud.com"] 
}
data "ibm_dns_domain_registration" "dns-domain-test" {
    name = "test-domain.com"
}
```


### Input parameters
{: #dns-register-input}

The following arguments are supported:

|Name|Description|
|----|-----------|
|`dns_registration_id`|(Required, string) The unique ID of the domain's registration. This is exported by the ibm_dns_domain_registration data source. |
|`name_servers`|(Required, Array of string) Example for an array of name servers returned from configuration of a domain on an instance of {{site.data.keyword.cis_full_notm}}. This is of the format: ["ns006.name.cloud.ibm.com", "ns017.name.cloud.ibm.com"]|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dns-register-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique internal identifier of the domain registration record.|
|`name_servers`|The new name servers pointing to the new DNS management service provider|
|`original_name_servers`|The original name servers configured at the time of domain registration.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_dns_secondary`
{: #dns-second}

The `ibm_dns_secondary` resource represents a single secondary DNS zone managed on SoftLayer. Each record created within the secondary DNS service defines which zone is transferred, what server it is transferred from, and the frequency that zone transfers occur at. Zone transfers are performed automatically based on the transfer frequency set on the secondary DNS record.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-second-sample}

```
resource "ibm_dns_secondary" "dns-secondary-test" {
    zone_name = "dns-secondary-test.com"
    master_ip_address = "127.0.0.10"
    transfer_frequency = 10
}
```
{: codeblock}

### Input parameters
{: #dns-second-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource
|----|-----------| ------ | ----- | ----------|
|`zone_name`| String | Required | The name of the zone that is transferred.| Yes |
|`transfer_frequency`| Integer | Required | Signifies how often a secondary DNS zone should be transferred in minutes.| No |
|`master_ip_address`| String | Required |  The IP address of the master name server where a secondary DNS zone is transferred from.| No |
|`tags`| Array of Strings | Optional | Tags associated with the DNS secondary instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dns-second-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|A secondary zone's internal identifier.|
|`status_id`|The status of a secondary DNS record.|
|`status_text`|The textual representation of a secondary DNS zone's status.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_dns_reverse_record`
{: #dns-rev-rec}

Provides a single DNS reverse record managed on IBM Cloud Classic Infrastructure (SoftLayer). Record contains general information about the reverse record, such as the hostname, IP address and time to leave.

The IBM Cloud Classic Infrastructure (SoftLayer) object  [SoftLayer_Dns_Domain_ResourceRecord](https://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord) is used for most create-retrieve-update-delete (`CRUD`) operations.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-rev-rec-sample}
```
resource "ibm_dns_reverse_record" "testreverserecord" {
    ipaddress="123.123.123.123"
    hostname="www.example.com"
    ttl=900
}

```
{: codeblock}

### Input parameters
{: #dns-rev-rec-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`ipaddress`| String | Required | The IP address or a hostname of a domain's resource record.| Yes |
|`hostname`| String | Required | The host defined by a reverse record.| No |
|`ttl`|Integer| Optional| The time to live (TTL) duration, expressed in seconds, of a resource record. Default value is 604800 seconds.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dns-rev-rec-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of reverse dns record.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_dns_record`
{: #dns-record}

Provides a single-resource record entry in `ibm_dns_domain`. Each resource record contains a `host` and a `data` property to define the name and target data of a resource.

The IBM Cloud Classic Infrastructure (SoftLayer) object  [SoftLayer_Dns_Domain_ResourceRecord](https://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord) is used for most create-retrieve-update-delete (`CRUD`) operations. The IBM Cloud Classic Infrastructure (SoftLayer) object [SoftLayer_Dns_Domain_ResourceRecord_SrvType](https://sldn.softlayer.com/reference/services/SoftLayer_Dns_Domain_ResourceRecord_SrvType) is used for service record types (`SRV`).

The SOA and NS records are automatically created by IBM Cloud Classic Infrastructure (SoftLayer) when the domain is created, you don't need to create those manually.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #dns-record-sample}

#### `A` Record

Review the [IBM Cloud Classic Infrastructure Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_AType) to properly implement the `A` record.

```
resource "ibm_dns_domain" "main" {
    name = "main.example.com"
}

resource "ibm_dns_record" "www" {
    data = "123.123.123.123"
    domain_id = ibm_dns_domain.main.id
    host = "www.example.com"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "a"
}
```
{: codeblock}

#### `AAAA` Record

Review the [IBM Cloud Classic Infrastructure Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_AaaaType) to properly implement the `AAAA` record.

```
resource "ibm_dns_record" "aaaa" {
    data = "fe80:0000:0000:0000:0202:b3ff:fe1e:8329"
    domain_id = ibm_dns_domain.main.id
    host = "www.example.com"
    responsible_person = "user@softlayer.com"
    ttl = 1000
    type = "aaaa"
}
```
{: codeblock}

#### `CNAME` Record

Review the [IBM Cloud Classic Infrastructure Docs] to properly implement the `CNAME` record.

```
resource "ibm_dns_record" "cname" {
    data = "real-host.example.com."
    domain_id = ibm_dns_domain.main.id
    host = "alias.example.com"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "cname"
}
```
{: codeblock}

#### `NS` Record

Review the [IBM Cloud Classic Infrastructure Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_NsType) to properly implement the `NS` record.

```
resource "ibm_dns_record" "recordNS" {
    data = "ns.example.com."
    domain_id = ibm_dns_domain.main.id
    host = "example.com"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "ns"
}
```
{: codeblock}

#### `MX` Record

Review the [IBM Cloud Classic Infrastructure Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_MxType) to properly implement the `MX` record.

```
resource "sibm_dns_record" "recordMX-1" {
    data = "mail-1"
    domain_id = ibm_dns_domain.main.id
    host = "@"
    mx_priority = "10"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "mx"
}
```
{: codeblock}

#### `SOA` Record

Review the [IBM Cloud Classic Infrastructure Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_SoaType) to properly implement the `SOA` record.

```
resource "ibm_dns_record" "recordSOA" {
    data = "ns1.example.com. abuse.example.com. 2018101002 7200 600 1728000 43200"
    domain_id = ibm_dns_domain.main.id
    host = "example.com"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "soa"
}
```
{: codeblock}

#### `SPF` Record

Review the [IBM Cloud Classic Infrastructure Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_SpfType) to properly implement the `SPF` record.

```
resource "ibm_dns_record" "recordSPF" {
    data = "v=spf1 mx:mail.example.org ~all"
    domain_id = ibm_dns_domain.main.id
    host = "mail-1"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "spf"
}
```
{: codeblock}

#### `TXT` Record

Review the [IBM Cloud Classic Infrastructure Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_TxtType/) to properly implement the `TXT` record.

```
resource "ibm_dns_record" "recordTXT" {
    data = "host"
    domain_id = ibm_dns_domain.main.id
    host = "A SPF test host"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "txt"
}
```
{: codeblock}

#### `SRV` Record

Review the [IBM Cloud Classic Infrastructure  Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_SrvType) to properly implement the `SRV` record.

```
resource "ibm_dns_record" "recordSRV" {
    data = "ns1.example.org"
    domain_id = ibm_dns_domain.main.id
    host = "hosta-srv.com"
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "srv"
    port = 8080
    priority = 3
    protocol = "_tcp"
    weight = 3
    service = "_mail"
}
```
{: codeblock}

#### `PTR` Record

Review the [IBM Cloud Classic Infrastructure  Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Dns_Domain_ResourceRecord_PtrType/) to properly implement the `PTR` record.

```
resource "ibm_dns_record" "recordPTR" {
    data = "ptr.example.com"
    domain_id = ibm_dns_domain.main.id

## The host is the last octet of IP address in the range of the subnet
    host = "45"  
    responsible_person = "user@softlayer.com"
    ttl = 900
    type = "ptr"
}
```
{: codeblock}

### Input parameters
{: #dns-record-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`data`| String | Required | The IP address or a hostname of a domain's resource record. Fully qualified host and domain name data must end with the `.` character.| No |
|`domain_id`| Integer | Required | The ID for the domain associated with the resource record.| Yes |
|`expire`| Integer | Optional | The duration, expressed in seconds, that a secondary name server (or servers) holds a zone before it is no longer considered authoritative.| No |
|`host`| String | Required |The host defined by a resource record. The `@` symbol denotes a wildcard.| No |
|`minimum_ttl`|Integer| Optional | The duration, expressed in seconds, that a domain's resource records are valid. This is also known as a minimum time to live (TTL), and can be overridden by an individual resource record's TTL.|
|`mx_priority`| Integer | Optional | The priority of the mail exchanger that delivers mail for a domain. This is useful in cases where a domain has more than one mail exchanger. A lower number denotes a higher priority, and mail attempt to deliver through the highest priority exchanger before moving to lower priority exchanger. The default value is `0`.| No |
|`refresh`|Integer|Optional| The duration, expressed in seconds, that a secondary name server waits to check the domain's primary name server for a new copy of a DNS zone. If a zone file has changed, the secondary DNS server updates its copy of the zone to match the primary DNS server's zone.| No |
|`responsible_person`| String | Required | The email address of the person responsible for a domain. Replace the `@` symbol in the address with a `.`. For example, root@example.org would be expressed as `root.example.org.`.| No |
|`retry`| Integer | Optional | The duration, expressed in seconds, that the domain's primary name server (or servers) waits before attempting to refresh the domain's zone with the secondary name server. A failed attempt to refresh by a secondary name server triggers the retry action.| No |
|`ttl`|Integer | Required |The time to live (TTL) duration, expressed in seconds, of a resource record. A name server uses TTL to determine how long to cache a resource record. An SOA record's TTL value defines the domain's overall TTL.| No |
|`type`| String | Required |The type of domain resource record. Accepted values are as follows: `a` for address records, `aaaa` for address records, `cname` for canonical name records, `mx` for mail exchanger records, `ptr` for pointer records in reverse domains, `spf` for sender policy framework records, `srv` for service records. | Yes |
|`txt`| String | Optional | Used for text records.| No |
|`service`| String | Required |`SRV` records only. The symbolic name of the service.| No |
|`protocol`| String | Required |`SRV` records only. The protocol of the service that you want to use, such as `TCP` or `UDP`.| No |
|`port`| Integer | Required |`SRV` records only. The TCP or UDP port on which the service be found.| No |
|`priority`| Integer | Required | `SRV` records only. The priority of the target host. The lowest numerical value is given the highest priority. The default value is `0`.| No |
|`weight`| Integer | Required | `SRV` records only. A relative weight for records that have the same priority. The default value is `0`.| No |
|`tags`| Array of Strings | Optional | Tags associated with the DNS domain record instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #dns-record-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The internal identifier of the domain resource record.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_firewall`
{: #firewall}

Provides a firewall in IBM. One firewall protects one public VLAN and provides in-bound network packet filtering.

You can order or find firewalls in the IBM Cloud infrastructure customer portal by navigating to **Network > IP Management > VLANs** and clicking the **Gateway/Firewall** column.

For an overview of supported firewalls, see [Exploring firewalls](/docs/hardware-firewall-dedicated?topic=fortigate-10g-exploring-firewalls).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #firewall-sample}

```
resource "ibm_firewall" "testfw" {
  firewall_type = "HARDWARE_FIREWALL_DEDICATED"
  ha_enabled = false
  public_vlan_id = 12345678
  tags = [
     "collectd",
     "mesos-master"
   ]
}
```
{: codeblock}

### Input parameters
{: #firewall-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`firewall_type`| String | Optional | Specifies the type of firewall to create. Valid options are HARDWARE_FIREWALL_DEDICATED or FORTIGATE_SECURITY_APPLIANCE. Defaults to HARDWARE_FIREWALL_DEDICATED| Yes |
|`ha_enabled`|Boolean| Required | Specifies whether the local load balancer needs to be HA-enabled.| Yes |
|`public_vlan_id`|Integer | Required | The target public VLAN ID that you want the firewall to protect. You can find accepted values [here](https://cloud.ibm.com/classic/network/vlans). Click the VLAN that you want to use and note the ID number in the resulting URL. You can also refer to a VLAN name by using a data source.| Yes |
|`tags`|Array of Strings | Optional | Set tags on the firewall. Permitted characters include: A-Z, 0-9, whitespace, `_` (underscore), `-` (hyphen), `.` (period), and `:` (colon). All other characters are removed.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: firewall-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the VLAN.|
|`location`|The location/datacenter of the created firewall device.|
|`primary_ip:`|The public gateway IP address.|
|`username:`|The username that is used to log in into the device, in case of Forti Gate Appliances.|
|`password:`|The password that is used to log in into the device, in case of Forti Gate Appliances.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_multivlan_firewall`
{: #multivlan-firewall}

Create a firewall with multiple VLANs.

For more information, see the [IBM Cloud (SoftLayer) multi VLAN firewall Request Docs](https://sldn.softlayer.com/reference/datatypes/SoftLayer_Container_Product_Order_Network_Protection_Firewall_Dedicated/).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #multivlan-firewall-sample}

In the following example, you can create a firewall with multiple VLANs:

```
resource "ibm_multi_vlan_firewall" "firewall_first" {
	datacenter = "dal13"
	pod = "pod01"
	name = "Checkdelete1"
	firewall_type = "FortiGate Security Appliance"
	addon_configuration = ["FortiGate Security Appliance - Web Filtering Add-on (High Availability)","FortiGate Security Appliance - NGFW Add-on (High Availability)","FortiGate Security Appliance - AV Add-on (High Availability)"]
	}
```
{: codeblock}


### Input parameters
{: #multivlan-firewall-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`datacenter`| String | Required | The data center in which the firewall appliance resides.| Yes |
|`pod`| String | Required | The pod in which the firewall resides| Yes |
|`name`| String | Required | The name of the firewall device| Yes |
|`firewall_type`| String | Required | The type of the firewall device. Supported values include `FortiGate Security Appliance` and `FortiGate Firewall Appliance HA Option`.| Yes |
|`addon_configuration`| List | Required |) The list of add-ons that are allowed. Allowed values are `FortiGate Security Appliance) - Web Filtering Add-on (High Availability)`,`FortiGate Security Appliance - NGFW Add-on (High Availability)`,`FortiGate Security Appliance - AV Add-on (High Availability)` or `FortiGate Security Appliance - Web Filtering Add-on`, `FortiGate Security Appliance - NGFW Add-on`,`FortiGate Security Appliance - AV Add-on`.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #multivlan-firewall-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the multi VLAN firewall|
|`public_vlan_id`|The ID of the Public VLAN for accessing this gateway|
|`private_vlan_id`|The ID of the Private VLAN for accessing this gateway|
|`public_ip`|The public gateway IP address.|
|`public_ipv6`|The public gateway IPv6 address.|
|`private_ip`|The private gateway IP address.|
|`username`|The username that is used to log in into the device.|
|`password`|The password that is used to log in into the device.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_firewall_policy`
{: #firewall-policy}

Provides rules for firewall resources in IBM. One rule resource is allowed per firewall. However, a rule resource can contain multiple firewall rules within it.

**NOTE**: The target VLAN should have at least one subnet for rule configuration. To express any IP addresses externally, configure `src_ip_address` as `0.0.0.0` and `src_ip_cidr` as `0`. To express API IP addresses internally, configure `dst_ip_address` as `any` and `src_ip_cidr` as `32`.

When a rules resource is created, it cannot be deleted. IBM does not allow entire rule deletion.

Firewalls should have at least one rule. If Terraform on {{site.data.keyword.cloud_notm}} destroys the rules resources, _permit from any to any with `TCP`, `UDP`, `ICMP`, `GRE`, `PPTP`, `ESP`, and `HA_` rule to be configured.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #firewall-policy-sample}

```
resource "ibm_firewall" "demofw" {
  ha_enabled = false
  public_vlan_id = 1234567
}

resource "ibm_firewall_policy" "rules" {
 firewall_id = ibm_firewall.demofw.id
 rules {
      "action" = "permit"
      "src_ip_address"= "10.1.1.0"
      "src_ip_cidr"= 24
      "dst_ip_address"= "any"
      "dst_ip_cidr"= 32
      "dst_port_range_start"= 80
      "dst_port_range_end"= 80
      "notes"= "Permit from 10.1.1.0"
      "protocol"= "udp"
 }
 rules {
       "action" = "deny"
       "src_ip_address"= "10.1.1.0"
       "src_ip_cidr"= 24
       "dst_ip_address"= "any"
       "dst_ip_cidr"= 32
       "dst_port_range_start"= 81
       "dst_port_range_end"= 81
       "notes"= "Permit from 10.1.1.0"
       "protocol"= "udp"
  }
}
```
{: codeblock}

### Input parameters
{: #firewall-policy-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`firewall_id`| Integer | Required | The device ID for the target hardware firewall.| Yes |
|`rules`|Array | Required | The firewall rules. At least one rule is required.| No |
|`rules.action`| String | Required | Specifies whether traffic is allowed when rules are matched. Accepted values are `permit` or `deny`.| No |
|`rules.src_ip_address`| String | Required | Specifies either a specific IP address or the network address for a specific subnet.| No |
|`rules.src_ip_cidr`| String | Required |Specifies the standard CIDR notation for the selected source. `32` implements the rule for a single IP while, for example, `24` implements the rule for 256 IP's.| No |
|`rules.dst_ip_address`| String | Required | Accepted values are `any`, a specific IP address, or the network address for a specific subnet.| No |
|`rules.dst_ip_cidr`| String | Required | Specifies the standard CIDR notation for the selected destination.| No |
|`rules.dst_port_range_start`| String | Optional | The start of the range of ports for TCP and UDP. Accepted values are `1`-`65535`.| No |
|`rules.dst_port_range_end`| String | Optional |The end of the range of ports for TCP and UDP. Accepted values are `1`-`65535`.| No |
|`rules.notes`| Strings | Optional | Descriptive text about the rule.| No |
|`rules.protocol`| String | Required | The protocol for the rule. Accepted values are `tcp`,`udp`,`icmp`,`gre`,`pptp`,`ah`, or `esp`.| No |
|`tags`| Array of Strings | Optional | Tags associated with the firewall policy instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}




## `ibm_hardware_firewall_shared`
{: #shared-fw}

Provides a firewall in IBM. One firewall protects one public VLAN and provides in-bound network packet filtering. 



For more information, about how to configure a firewall, see the [docs](/docs/hardware-firewall-shared?topic=hardware-firewall-shared-about-hardware-firewall-shared-).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #shared-fw-sample}

```
resource "ibm_hardware_firewall_shared" "test_firewall" {
    firewall_type="100MBPS_HARDWARE_FIREWALL"
    hardware_instance_id="12345678"
}
```
{: codeblock}

### Input parameters
{: #shared-fw-input}

The following arguments are supported:

|Name|Description|
|----|-----------|
|`firewall_type`|(Required, string) Specifies whether it needs to be of particular speed. Firewall type is in between <br> [10MBPS_HARDWARE_FIREWALL, <br>20MBPS_HARDWARE_FIREWALL, <br>100MBPS_HARDWARE_FIREWALL, <br>1000MBPS_HARDWARE_FIREWALL].|
|`virtual_instance_id`|(Optional, string) Specifies the ID of particular guest on which firewall shared is to be deployed. **NOTE**: This is conflicting parameter with hardware_instance_id.|
|`hardware_instance_id`|(Optional, string) Specifies the ID of particular guest on which firewall shared is to be deployed. **NOTE**: This is conflicting parameter with virtual_instance_id.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #shared-fw-output}

The following attributes are exported:

 |Name|Description|
|----|-----------|
|`id`|The unique identifier of the hardware firewall.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_ipsec_vpn`
{: #ipsec-vpn}

Create, update, or delete an IPSec VPN resource.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ipsec-vpn-sample}

The following example creates an IPSec VPN resource. 
{: shortdesc}

```
resource "ibm_ipsec_vpn" "ipsec" {
    datacenter = "tok02"
    Customer_Peer_IP = "192.168.32.2"
    phase_one = [{Authentication="SHA1",Encryption="3DES",Diffie-Hellman-Group=12,Keylife=131}]
    phase_two = [{Authentication="SHA1",Encryption="3DES",Diffie-Hellman-Group=12,Keylife=133}]
    remote_subnet = [{Remote_ip_adress = "10.0.0.0",Remote_IP_CIDR = 22}]
    }
 ```
 {: codeblock}
 
### Input parameters
{: #ipsec-vpn-input}
 
Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`datacenter`|String|Required|The data center in which the IPSec VPN resides.|
|`phase_one`|Map|Optional|The key-value parameters for phase One negotiation.|
|`phase_two`|Map|Optional|The key-value parameters for phase Two negotiation.|
|`address_translation`|Map|Optional|The key-value parameters for creating an address translation.|
|`Preshared_Key`|String|Optional|A key used so that peers authenticate each other. This key is hashed by using the phase one encryption and phase one authentication.|
|`Customer_Peer_IP`|String|Optional|The remote end of a network tunnel. This end of the network tunnel resides on an outside network and be sending and receiving the IPSec packets.
|`internal_subnet_id`|Map|Optional|The ID of the network device on which the VPN configurations have to be applied. When a private subnet is associated, the network tunnel will allow the customer (remote) network to access the private subnet.|
|`remote_subnet_id`|Map|Optional|The ID of the customer owned device on which the network configuration has to be applied. When a remote subnet is associated, a network tunnel allows the customer (remote) network to communicate with the private and service subnets on the SoftLayer network which are on the other end of this network tunnel.
|`remote_subnet`|Map|Optional|The key-value parameters for creating a customer subnet.|
|`service_subnet_id`|String|Optional|The ID of the service subnet which is to be associated to the network tunnel. When a service subnet is associated, a network tunnel allows the customer (remote) network to communicate with the private and service subnets on the SoftLayer network which are on the other end of this network tunnel. Service subnets provide access to SoftLayer services such as the customer management portal and the SoftLayer API.|

### Output parameters
{: #ipsec-vpn-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The computed ID of the IPSec VPN device that is created. |
|`name`|String|The computed name of the IPSec VPN device that is created.|
|`internal_peer_ip_address`|String|The local end of a network tunnel. This end of the network tunnel resides on the SoftLayer networks and allows access to remote end of the tunnel to subnets on SoftLayer networks.|
 

## `ibm_lb`
{: #lb}

Provides a resource for local load balancers. This allows local load balancers to be created, updated, and deleted.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #lb-sample}

In the following example, you can create a local load balancer:

```
resource "ibm_lb" "test_lb_local" {
  connections = 1500
  datacenter  = "tok02"
  ha_enabled  = false
  dedicated   = false

  //User can increase timeouts
  timeouts {
    create = "45m"
  }
}
```
{: codeblock}

### Input parameters
{: #lb-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`connections`|Integer | Required |The number of connections for the local load balancer. Only incremental upgrade is supported. For downgrade, please open the SoftLayer support ticket.| No |
|`datacenter`| String | Required | The data center for the local load balancer.| Yes |
|`ha_enabled`|Boolean|Required|Specifies whether the local load balancer must be HA-enabled.| Yes |
|`security_certificate_id`| Integer | Optional | The ID of the security certificate associated with the local load balancer.| Yes |
|`dedicated`|Boolean|Optional| Specifies whether the local load balancer must be dedicated. The default value is `false`.| No |
|`ssl_offload`|Boolean|Optional| Specifies the local load balancer SSL offload. If `true` start SSL acceleration on all SSL virtual services. (those with a type of HTTPS) This action should be taken only after configuring an SSL certificate for the virtual IP. If `false` stop SSL acceleration on all SSL virtual services (those with a type of HTTPS). The default value is `false`.| No |
|`tags`|Array of Strings|Optional|Tags associated with the local load balancer instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #lb-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the local load balancer.|
|`hostname`|The host name of the local load balancer.|
|`ip_address`|The IP address of the local load balancer.|
|`subnet_id`|The unique identifier of the subnet associated with the local load balancer.|
|`ssl_enabled`|The status of whether the local load balancer provides SSL capability.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #lb-timeout}

ibm_subnet provides the following [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) configuration options:

|Name|Description|
|----|-----------|
|`create`|(Default 30 minutes) Used for Creating Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}


## `ibm_lbaas`
{: #lbaas}

Provides a resource for a load balancer as a service. This allows a load balancer as a service to be created, updated, and deleted. Currently, only one subnet is supported.

Cloud load balancer creation takes 5 to 10 minutes. Destroy can take up to 30 minutes. Cloud Load Balancer does not support customization of acceptable response codes. Only the range 2xx is considered healthy. Redirects in the range 3xx are considered unhealthy. 
 
### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #lbaas-sample}

```

resource "ibm_lbaas" "lbaas" {
  name        = "terraformLB"
  description = "delete this"
  subnets     = [1511875]

  protocols = [{
    frontend_protocol     = "HTTPS"
    frontend_port         = 443
    backend_protocol      = "HTTP"
    backend_port          = 80
    load_balancing_method = "round_robin"
    tls_certificate_id    = 11670
  },
    {
      frontend_protocol     = "HTTP"
      frontend_port         = 80
      backend_protocol      = "HTTP"
      backend_port          = 80
      load_balancing_method = "round_robin"
    },
  ]
}

```
{: codeblock}

### Input parameters
{: #lbaas-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`name`| String | Required | The load balancer's name.| Yes |
|`description`| String | Optional | A description of the load balancer.| No |
|`type`| String | Optional | Specify whether this load balancer is a public or internal facing load balancer. Accepted values are `PUBLIC` or `PRIVATE`. The default is 'PUBLIC'.| Yes |
|`subnets`| Array | Required | The subnet where the load balancer will be provisioned. Only one subnet is supported.| Yes |
|`protocols`| Array | Optional | A nested block describes the protocols that are assigned to load balancer.   | Yes |
|`protocols.frontend_protocol`| String | Required | The front-end protocol. Accepted values are 'TCP', 'HTTP', and 'HTTPS'.  |  No |
|`protocols.frontend_port`| Integer | Required |The front-end protocol port number. The port number must be in the range of 1-65535.  | No |
|`protocols.backend_protocol`| String | Required | The back-end protocol. Accepted values are 'TCP', 'HTTP', and 'HTTPS'.  | No |
|`protocols.backend_port`| Integer | Required |The back-end protocol port number. The port number must be in the range of 1-65535.  | No |
|`protocols.load_balancing_method`| String | Optional | The load-balancing algorithm. Accepted values are 'round_robin', 'weighted_round_robin', and 'least_connection'. The default is 'round_robin'.  | No |
|`protocols.session_stickiness`| String | Optional | The SOURCE_IP for session stickiness.  | No |
|`protocols.max_conn`| Integer | Optional | The maximum number of connections the listener can accept. The number must be 1-64000.  | No |
|`protocols.tls_certificate_id`| Integer | Optional | The ID of the SSL/TLS certificate used for a protocol. This ID should be specified when `front-end protocol` has a value of `HTTPS`.| No |
|`session_stickiness`| String | Optional | The `SOURCE_IP` or `HTTP_COOKIE` for session stickiness.|No|
|`ssl_ciphers`| List | Optional |The comma-separated list of SSL Ciphers. You can find list of supported ciphers [SSL_offload](/docs/loadbalancer-service?topic=loadbalancer-service-ssl-offload-with-ibm-cloud-load-balancer).| No |
|`use_system_public_ip_pool`| Boolean | Optional | Applicable for public load balancer only. It specifies whether the public IP addresses are allocated from system public IP pool or public subnet from the account order of the load balancer. The default value is `true`.| No |
|`wait_time_minutes`| Integer | Required | The duration, expressed in minutes, to wait for the LBaaS instance to become available before declaring it as created. It is also the same amount of time waited for deletion to finish. The default value is `90`.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #lbaas-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the created policy.|
|`datacenter`|The datacenter where the load balancer is provisioned. This is based on the subnet chosen while creating load-balancer.|
|`status`|Specifies the operation status of the load balancer as `online` or `offline`.|
|`vip`|The virtual IP address of the load balancer.|
|`protocol_id`|The UUID of a load balancer protocol.|
|`health_monitors`|A nested block describes the health_monitors assigned to the load balancer. Nested `health_monitors` blocks have the following structure:  |
|`health_monitors.protocol`|The back-end protocol.  |
|`health_monitors.port`|The back-end port.  |
|`health_monitors.interval`|Interval in seconds to perform   |
|`health_monitors.max_retries`|Maximum retries  |
|`health_monitors.timeout`|Health check methods timeout in   |
|`health_monitors.url_path`|If monitor is "HTTP", it specifies the URL path.|
|`health_monitors.monitor_id`|Health Monitor UUID|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_lbaas_health_monitor`
{: #health-monitor}

Provides a resource for the health monitors of IBM LBaaS. This allows you to update a health monitor configuration of the load balancer. Health monitors are created and deleted by the creation and deletion of LBaaS protocols.
 
### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #health-monitor-sample}

```

resource "ibm_lbaas" "lbaas" {
  name        = "terraformLB"
  description = "delete this"
  subnets     = [1511875]

  protocols = [{
    frontend_protocol     = "HTTPS"
    frontend_port         = 443
    backend_protocol      = "HTTP"
    backend_port          = 80
    load_balancing_method = "round_robin"
    tls_certificate_id    = 11670
  },
    {
      frontend_protocol     = "HTTP"
      frontend_port         = 80
      backend_protocol      = "HTTP"
      backend_port          = 80
      load_balancing_method = "round_robin"
    },
  ]
}

resource "ibm_lbaas_health_monitor" "lbaas_hm" {
  protocol = ibm_lbaas.lbaas.health_monitors.0.protocol
  port = ibm_lbaas.lbaas.health_monitors.0.port
  timeout = 3
  interval = 5
  max_retries = 6
  url_path = "/"
  lbaas_id = ibm_lbaas.lbaas.id
  monitor_id = ibm_lbaas.lbaas.health_monitors.0.monitor_id
}

```
{: codeblock}

### Input parameters
{: #health-monitor-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`monitor_id`| String | Required | Health Monitor unique identifier. The monitor ID can be imported from either the `ibm_lbaas` resource or datasource. For example, `ibm_lbaas.lbaas.health_monitors.X.monitor_id` or `data.ibm_lbaas.lbaas.health_monitors.X.monitor_id`| Yes |
|`lbaas_id`| String | Required | LBaaS unique identifier| Yes |
|`protocol`| String | Required | The back-end protocol| No |
|`port`| Integer | Required | The back-end port| No |
|`interval`| Integer | Optional | Interval in seconds to perform | No |
|`max_retries`|Integer | Optional | Maximum retries| No |
|`timeout`| Integer | Optional | Health check methods timeout in | No |
|`url_path`| String | Optional | If monitor is "HTTP", it specifies the URL path.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #health-monitor-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the LBaaS health monitor resource. The ID is composed of `<lbaas_id>/<monitor_id>`.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #health-monitor-import}

`ibm_lbaas_health_monitor` can be imported by using LBaaS ID and monitor ID.

```
terraform import ibm_lbaas_health_monitor.example 988-454f-45vf-454542/d343f-f44r-wer3-fe
```
{: pre}





## `ibm_lbaas_server_instance_attachment`
{: #instance-attachment}

Provides a resource for attaching the server instance to IBM Cloud Load Balancer. This allows attach, detach, and update server instances as LoadBalancer members to IBM Cloud Load Balancer. A `depends_on` statement is required for the associated load balancer to ensure that attach and detach occur after and before load balancer creation and deletion. If you do not specify the `depends_on` parameter, intermittent attach failures will occur on creation and load balancer deletion will fail. Typically when apply or destroy is rerun the operation will be successful. 


 
### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #instance-attachment-sample}

```

resource "ibm_compute_vm_instance" "vm_instances" {
  count = "2"
  ....
}

resource "ibm_lbaas" "lbaas" {
  name        = "terraformLB"
  description = "delete this"
  subnets     = [1511875]

  protocols = [{
    frontend_protocol     = "HTTPS"
    frontend_port         = 443
    backend_protocol      = "HTTP"
    backend_port          = 80
    load_balancing_method = "round_robin"
    tls_certificate_id    = 11670
  },
    {
      frontend_protocol     = "HTTP"
      frontend_port         = 80
      backend_protocol      = "HTTP"
      backend_port          = 80
      load_balancing_method = "round_robin"
    },
  ]
}

resource "ibm_lbaas_server_instance_attachment" "lbaas_member" {
  count				 = 2
  private_ip_address = element(ibm_compute_vm_instance.vm_instances.*.ipv4_address_private,count.index)
  weight             = 40
  lbaas_id           = ibm_lbaas.lbaas.id
  depends_on         = ["ibm_lbaas.lbaas.id"]
}

```
{: codeblock}

### Input parameters
{: #instance-attachment-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`private_ip_address`| String | Required | The private IP address of a load balancer member.| Yes |
|`weight`| Integer | Optional | The weight of a load balancer member.| No |
|`lbaas_id`| String | Required |The UUID of a load balancer.| Yes |
|`depends_on`| String | Required |The UUID of a load balancer | No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #instance-attachment-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`uuid`|The unique identifier of the load balancer member.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_lb_service`
{: #lb-service}

Provides a resource for local load balancer services. This allows local load balancer services to be created, updated, and deleted.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_Application_Delivery_Controller_LoadBalancer_Service).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #lb-service-sample}

In the following example, you can create a local load balancer service:

```
resource "ibm_lb_service" "test_lb_local_service" {
    port = 80
    enabled = true
    service_group_id = ibm_lb_service_group.test_service_group.service_group_id
    weight = 1
    health_check_type = "DNS"
    ip_address_id = ibm_compute_vm_instance.test_server.ip_address_id
}

```
{: codeblock}

### Input parameters
{: #lb-service-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`service_group_id`| Integer | Required |  The ID of the local load balancer service group.| Yes |
|`ip_address_id`| Integer | Required | The ID of the virtual server.| Yes |
|`port`| Integer | Required | The port for the local load balancer service.| No |
|`enabled`| Integer | Required | Specifies whether you want to enable the load balancer service. The default value is `false`.| No |
|`health_check_type`| String | Required | The health check type for the load balancer service.| No |
|`weight`| Integer | Required | The weight for the load balancer service.| No |
|`tags`| Array of Strings | Optional | Tags associated with the local load balancer service instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}




## `ibm_lb_service_group`
{: #service-group}

Provides a resource for local load balancer service groups. This allows local load balancer service groups to be created, updated, and deleted.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_Application_Delivery_Controller_LoadBalancer_Service_Group).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #service-group-sample}

In the following example, you can create a local load balancer service group:

```
resource "ibm_lb_service_group" "test_service_group" {
    port = 82
    routing_method = "CONSISTENT_HASH_IP"
    routing_type = "HTTP"
    load_balancer_id = "ibm_lb.test_lb_local.id
    allocation = 100
}
```
{: codeblock}

### Input parameters
{: #service-group-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`load_balancer_id`| Integer | Required | The ID of the local load balancer.| Yes |
|`allocation`| Integer | Required | The connection allocation for the load balancer service group.| No |
|`port`| Integer | Required | The port for the local load balancer service group.| No |
|`routing_method`| String | Required | The routing method for the load balancer group. For example, `CONSISTENT_HASH_IP`.| No |
|`routing_type`| String | Required |The routing type for the group.| No |
|`timeout`| Integer | Optional |The timeout value for connections from remote clients to the load balancer. Timeout values are only valid for HTTP service groups. | No |
|`tags`| Array of Strings | Optional | Tags associated with the local load balancer service group instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #service-group-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`virtual_server_id`|The unique identifier of the virtual server.|
|`service_group_id`|The unique identifier of the load balancer service group.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_lb_vpx`
{: #lb-vpx}

Provides a resource for VPX load balancers. This allows VPX load balancers to be created, updated, and deleted.  

**NOTE**: IBM VPX load balancers consist of `Citrix NetscalerVPX` devices (virtual), which are currently priced on a per-month basis. Use caution when creating the resource because the cost for an entire month is incurred immediately upon creation. For more information, about pricing, see the [network appliance Docs](https://www.ibm.com/cloud/network-appliances). In the Citrix log, click **See more pricing** for a current price matrix.

You can also use the following REST URL to get a listing of VPX choices along with version numbers, speed, and plan type:

```
https://<userName>:<apiKey>@api.softlayer.com/rest/v3/SoftLayer_Product_Package/192/getItems.json?objectMask=id;capacity;description;units;keyName;prices.id;prices.categories.id;prices.categories.name
```

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #lb-vpx-sample}

Review the [IBM Cloud Classic Infrastructure  Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_Application_Delivery_Controller) for more information.

```
resource "ibm_lb_vpx" "test_vpx" {
    datacenter = "dal06"
    speed = 10
    version = "10.1"
    plan = "Standard"
    ip_count = 2
    public_vlan_id = 1251234
    private_vlan_id = 1540786
    public_subnet = "23.246.226.248/29"
    private_subnet = "10.107.180.0/26"
}
```
{: codeblock}

### Input parameters
{: #lb-vpx-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`datacenter`| String | Required |The data center in which you want to provision the VPX load balancer. You can find accepted values in the [data center Docs](https://www.ibm.com/cloud/load-balancer).| Yes |
|`speed`|Integer | Required | The speed, expressed in Mbps. Accepted values are `10`, `200`, and `1000`.| Yes |
|`version`| String | Required | The VPX load balancer version. Accepted values are `10.1`, `10.5`, `11.0`, `11.1` and `12.1`.| Yes |
|`plan`| String | Required |The VPX load balancer plan. Accepted values are `Standard` and `Platinum`.| Yes |
|`ip_count`| Integer | Required | The number of static public IP addresses assigned to the VPX load balancer. Accepted values are `1`,`2`, `4`, `8`, and `16`.| Yes |
|`public_vlan_id`|Integer | Optional | The public VLAN ID that is used for the public network interface of the VPX load balancer. You can find accepted values in the [VLAN network](https://cloud.ibm.com/classic/network/vlans) by clicking the VLAN that you want to use and noting the ID in the resulting URL. You can also refer to a VLAN name by using a data source.| Yes |
|`private_vlan_id`|Integer | Optional | The private VLAN ID that is used for the private network interface of the VPX load balancer. You can find accepted values in the [VLAN network](https://cloud.ibm.com/classic/network/vlans) by clicking the VLAN that you want to use and noting the ID in the resulting URL. You can also refer to a VLAN name by using a data source.| Yes |
|`public_subnet`|String | Optional| The public subnet that is used for the public network interface of the VPX load balancer. Accepted values are primary public networks. You can find accepted values in the [subnet Docs](https://cloud.ibm.com/classic/network/subnets).| Yes |
|`private_subnet`|String | Optional | Public subnet that is used for the private network interface of the VPX load balancer. Accepted values are primary private networks. You can find accepted values in the [subnet Docs](https://cloud.ibm.com/classic/network/subnets).| Yes |
|`tags`|Array of string | Optional | Tags associated with the VPX load balancer instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #lb-vpx-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The internal identifier of a VPX load balancer|
|`name`|The internal name of a VPX load balancer.|
|`vip_pool`|A list of virtual IP addresses for the VPX load balancer.|
|`management_ip_address`|The private address of the VPX UI.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_lb_vpx_ha`
{: #lb-vpx-ha}

Configure a high availability (HA) pair with two `NetscalerVPX` devices. The two `NetscalerVPXs` must be version 10.5 and located in the same subnet. A primary `NetscalerVPX` provides load-balancing services in active mode, and a secondary `NetscalerVPX` provides load-balancing services when the primary `NetscalerVPX` fails. For more information, refer to the  [Citrix support Documentation  ](https://support.citrix.com/article/CTX116748){: external} and the [Knowledge layer Netscaler Docs](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-setting-up-citrix-netscaler-vpx-for-high-availability-ha-).

**NOTE**: This resource only supports Netscaler VPX 10.5. The [NITRO API](https://docs.citrix.com/en-us/netscaler/11/nitro-api.html) is used to configure HA. Terraform on {{site.data.keyword.cloud_notm}} can only access the NITRO API in the IBM Cloud Classic Infrastructure (SoftLayer) private network, so connect to the private network when running Terraform on {{site.data.keyword.cloud_notm}}. You can also use the [SSL VPN](https://www.ibm.com/cloud/vpn-access){: external} to access a private network connection.

The two `NetscalerVPXs` use the same password in HA mode. When you create this resource, Terraform on {{site.data.keyword.cloud_notm}} changes the password of the secondary Netscaler VPX to the password of the primary Netscaler VPX. When you destroy this resource, Terraform on {{site.data.keyword.cloud_notm}} restores the original password of the secondary Netscaler VPX.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #lb-vpx-ha-sample}

```

## Create a primary Netscaler VPX
resource "ibm_lb_vpx" "test_pri" {
    datacenter = "lon02"
    speed = 10
    version = "10.5"
    plan = "Standard"
    ip_count = 2
}


## Create a secondary Netscaler VPX in the same subnets
resource "ibm_lb_vpx" "test_sec" {
    datacenter = "lon02"
    speed = 10
    version = "10.5"
    plan = "Standard"
    ip_count = 2
    public_vlan_id = ibm_lb_vpx.test_pri.public_vlan_id
    private_vlan_id = ibm_lb_vpx.test_pri.private_vlan_id
    public_subnet = ibm_lb_vpx.test_pri.public_subnet
    private_subnet = ibm_lb_vpx.test_pri.private_subnet


## Configure high availability with the primary and secondary `NetscalerVPXs`
resource "ibm_lb_vpx_ha" "test_ha" {
    primary_id = ibm_lb_vpx.test_pri.id
    secondary_id = ibm_lb_vpx.test_sec.id
    stay_secondary = false
}
```
{: codeblock}

### Input parameters
{: #lb-vpx-ha-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`primary_id`| String | Required | The ID of the primary Netscaler VPX.| Yes |
|`secondary_id`| String | Required | The ID of the secondary Netscaler VPX.| Yes |
|`stay_secondary`|Boolean | Optional | Specifies whether the secondary Netscaler VPX will  take over the service. Set this argument to `true` to prevent the secondary Netscaler VPX from taking over the service even if the primary Netscaler VPX fails. For more information, see the [Citrix Netscaler Docs](https://docs.citrix.com/en-us/netscaler/10-5/ns-system-wrapper-10-con/ns-nw-ha-intro-wrppr-con/ns-nw-ha-frcng-scndry-nd-sty-scndry-tsk.html) and the [Citrix support documentation  ](https://support.citrix.com/article/CTX116748). The default value is `false`.| No |
|`tags`|Array of string | Optional | Tags associated with the high availability Netscaler VPX pair instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #lb-vpx-ha-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the high availability Netscaler VPX pair.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_lb_vpx_service`
{: #vpx-svc}

Provides a resource for VPX load balancer services. This allows VPX load balancer services to be created, updated, and deleted. For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_LoadBalancer_Service).  

**NOTE**: If you use Netscaler VPX 10.5, Terraform on {{site.data.keyword.cloud_notm}} uses Netscaler's [NITRO REST API](https://docs.citrix.com/en-us/netscaler/11/nitro-api.html) to manage the resource.  Terraform on {{site.data.keyword.cloud_notm}} can only access the NITRO API in the IBM Cloud Classic Infrastructure (SoftLayer) private network, so connect to the private network when running Terraform on {{site.data.keyword.cloud_notm}}. You can also use the [SSL VPN](https://www.ibm.com/cloud/vpn-access){: external} to access a private network connection.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vpx-svc-sample}

In the following example, you can create a VPX load balancer:

```
resource "ibm_lb_vpx_service" "test_service" {
  name = "test_load_balancer_service"
  vip_id = ibm_lb_vpx_vip.testacc_vip.id
  destination_ip_address = ibm_compute_vm_instance.test_server.ipv4_address
  destination_port = 80
  weight = 55
  connection_limit = 5000
  health_check = "HTTP"
  usip = "NO"
}
```
{: codeblock}

### Input parameters
{: #vpx-svc-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`name`| String | Required |The ID of the VPX load balancer service.| Yes |
|`vip_id`| String | Required |The ID of the VPX load balancer virtual IP address to which the service is assigned.| Yes |
|`destination_ip_address`| String | Required | The IP address of the server to which traffic directs. If you use Netscaler VPX 10.1, you must indicate a public IP address in an IBM Cloud Classic Infrastructure (SoftLayer) account. If you use Netscaler VPX 10.5, you can use any IP address.| Yes |
|`destination_port`| Integer | Required |The destination port of the server to which traffic directs.| No |
|`weight`| Integer | Required | The percentage of the total connection limit allocated to the load balancer between all your services. See the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_LoadBalancer_Service) for details.       **NOTE**: If you use Netscaler VPX 10.5, the weight value is ignored.| No |
|`connection_limit`| Integer | Required |The connection limit for this service. Acceptable values are `0`-`4294967294`. See the [Citrix Netscaler Docs](https://docs.citrix.com/en-us/netscaler/11/reference/netscaler-command-reference/basic/service.html) for details.| No |
|`health_check`| String | Required |The health check type. See the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_LoadBalancer_Service) for details.| No |
|`usip`| String | Optional | Whether the service reports the source IP of the client to the service being load balanced. Acceptable values are `YES` or `NO`. The default value is `NO`. See the [Citrix Netscaler Docs](https://developer-docs.citrix.com/projects/netscaler-nitro-api/en/11.0/configuration/basic/service/service) for more information.       **NOTE**: This argument is only available for VPX 10.5.| No |
|`tags`| Array of string | Optional | Tags associated with the VPX load balancer service instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vpx-svc-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the VPX load balancer service.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_lb_vpx_vip`
{: #lb-vpx-vip}

Provides a resource for VPX load balancer virtual IP addresses. This allows VPX load balancer virtual IP addresses to be created, updated, and deleted.  

**NOTE**: If you use Netscaler VPX 10.5, Terraform on {{site.data.keyword.cloud_notm}} uses Netscaler's [NITRO REST API](https://docs.citrix.com/en-us/netscaler/11/nitro-api.html) to manage the resource.  Terraform on {{site.data.keyword.cloud_notm}} can only access the NITRO API in the IBM Cloud Classic Infrastructure (SoftLayer) private network, so connect to the private network when running Terraform on {{site.data.keyword.cloud_notm}}. You can also use the [SSL VPN](https://www.ibm.com/cloud/vpn-access){: external} to access a private network connection.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #lb-vpx-vip-sample}

The following example configuration supports Netscaler VPX 10.1 and 10.5:

```
resource "ibm_lb_vpx_vip" "testacc_vip" {
    name = "test_load_balancer_vip"
    nad_controller_id = 1234567
    load_balancing_method = "lc"
    source_port = 80
    virtual_ip_address = "211.233.12.12"
    type = "HTTP"
}
```
{: codeblock}

The following example configuration supports only Netscaler VPX 10.5. More options for the `load_balancing_method` and `persistence` arguments are shown. A private IP address can be used for the `virtual_ip_address` argument.

```
resource "ibm_lb_vpx_vip" "testacc_vip" {
    name = "test_load_balancer_vip"
    nad_controller_id = "1234567"
    load_balancing_method = "DESTINATIONIPHASH"
    persistence = "SOURCEIP"
    source_port = 80
    virtual_ip_address = "10.10.2.2"
    type = "HTTP"
}
```
{: codeblock}

Netscaler VPX 10.5 also supports SSL offload. If you set the `type` argument to `SSL` and configure the `security_certificate_id` argument, then the `virtual_ip_address` argument provides the `HTTPS` protocol. The following example shows an SSL-offload configuration:

```

## Create a Netscaler VPX 10.5
resource "ibm_lb_vpx" "test" {
    datacenter = "lon02"
    speed = 10
    version = "10.5"
    plan = "Standard"
    ip_count = 2
}

resource "ibm_lb_vpx_vip" "test_vip1" {
    name = "test_vip1"
    nad_controller_id = ibm_lb_vpx.test.id
    load_balancing_method = "rr"
    source_port = 443

## SSL type provides SSL offload
    type = "SSL"
    virtual_ip_address = ibm_lb_vpx.test.vip_pool[0]

## Use a security certificate in the SoftLayer portal
    security_certificate_id = 80347
}

resource "ibm_lb_vpx_service" "testacc_service1" {
  name = "test_load_balancer_service1"
  vip_id = ibm_lb_vpx_vip.test_vip1.id

## 10.6.218.166 should provides HTTP service with port 80
  destination_ip_address = "10.66.218.166"
  destination_port = 80
  weight = 100
  connection_limit = 4294967294
  health_check = "ICMP"
}
```
{: codeblock}

### Input parameters
{: #lb-vpx-vip-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description| Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`name`| String | Required |The ID of the VPX load balancer virtual IP address.| Yes |
|`nad_controller_id`| Integer | Required | The ID of the VPX load balancer that the virtual IP address is assigned to.| Yes |
|`load_balancing_method`| String | Required | See the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_LoadBalancer_VirtualIpAddress) for available methods. If you use Netscaler VPX 10.5, see the [Citrix Docs](https://docs.citrix.com/en-us/netscaler/10-5/ns-tmg-wrapper-10-con/ns-lb-wrapper-con-10/ns-lb-customizing-lbalgorithms-wrapper-con.html) for more methods that you can use.| No |
|`persistence`| String | Optional |Applies to Netscaler VPX 10.5 only. See the available persistence types in the [Citrix Docs](https://docs.citrix.com/en-us/netscaler/10-5/ns-tmg-wrapper-10-con/ns-lb-wrapper-con-10/ns-lb-persistence-wrapper-con/ns-lb-persistence-about-con.html).  | No |
|`virtual_ip_address`| String | Required |The public IP address for the VPX load balancer virtual IP.| No |
|`source_port`|Integer | Required | The source port for the VPX load balancer virtual IP address.| No |
|`type`| String | Required | The connection type for the VPX load balancer virtual IP address. Accepted values are `HTTP`, `FTP`, `TCP`, `UDP`, `DNS`, and `SSL`. If you set the type to `SSL`, then `security_certificate_id` provides certification for SSL offload services.| Yes |
|`security_certificate_id`| Integer | Optional | Applies to Netscaler VPX 10.5 only. The ID of a security certificate that you want to use. This argument provides security certification for SSL offload services. For more information, see the  [ibm_compute_ssl_certificate resource](#ssl-compute-cert).| Yes |
|`tags`| Array of string | Optional | Tags associated with the VPX load balancer virtual IP instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #lb-vpx-vip-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the VPX load balancer virtual IP.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_network_gateway`
{: #network-gateway}

Provides a resource for an IBM Cloud network gateway appliance. This resource allows a network gateway to be created, updated, and deleted.  

A network gateway can be created in stand-alone mode and HA mode with both members, with either the same or different configurations.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/services/SoftLayer_Network_Gateway).

For more information, about getting started, see the [IBM Virtual Router Appliance Docs](/docs/gateway-appliance?topic=gateway-appliance-getting-started).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #network-gateway-sample}

#### Stand-alone configuration

```
resource "ibm_network_gateway" "gateway" {
  name = "my-gateway"

  members = [{
    hostname             = "host-name"
    domain               = "ibm.com"
    datacenter           = "ams01"
    network_speed        = 100
    private_network_only = false
    tcp_monitoring       = true
    process_key_name     = "INTEL_SINGLE_XEON_1270_3_50"
    os_key_name          = "OS_VYATTA_5600_5_X_UP_TO_1GBPS_SUBSCRIPTION_EDITION_64_BIT"
    redundant_network    = false
    disk_key_names       = ["HARD_DRIVE_2_00TB_SATA_II"]
    public_bandwidth     = 20000
    memory               = 8
    tags                 = ["gateway tags 1", "terraform test tags 1"]
    notes                = "gateway notes 1"
    ipv6_enabled         = true
  },
  ]
}
```
{: codeblock}

#### HA configuration

```
resource "ibm_network_gateway" "gateway" {
  name = "my-ha-gateway"

  members = [{
    hostname             = "host-name-1"
    domain               = "ibm.com"
    datacenter           = "ams01"
    network_speed        = 100
    private_network_only = false
    tcp_monitoring       = true
    process_key_name     = "INTEL_SINGLE_XEON_1270_3_50"
    os_key_name          = "OS_VYATTA_5600_5_X_UP_TO_1GBPS_SUBSCRIPTION_EDITION_64_BIT"
    redundant_network    = false
    disk_key_names       = ["HARD_DRIVE_2_00TB_SATA_II"]
    public_bandwidth     = 20000
    memory               = 8
    tags                 = ["gateway tags", "terraform test tags 1"]
    notes                = "gateway notes"
    ipv6_enabled         = true
  },
    {
      hostname             = "host-name-2"
      domain               = "ibm.com"
      datacenter           = "ams01"
      network_speed        = 100
      private_network_only = false
      tcp_monitoring       = true
      process_key_name     = "INTEL_SINGLE_XEON_1270_3_50"
      os_key_name          = "OS_VYATTA_5600_5_X_UP_TO_1GBPS_SUBSCRIPTION_EDITION_64_BIT"
      redundant_network    = false
      disk_key_names       = ["HARD_DRIVE_2_00TB_SATA_II"]
      public_bandwidth     = 20000
      memory               = 8
      tags                 = ["gateway tags 1", "terraform test tags 1"]
      notes                = "my ha mode gateway"
      ipv6_enabled         = true
    },
  ]
}
```
{: codeblock}


### Input parameters
{: #network-gateway-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`name`| String | Required | The name of the gateway.| No |
|`ssh_key_ids`| List | Optional | The SSH key IDs to install on the gateway when the gateway gets created.| Yes |
|`post_install_script_uri`| String | Optional | The URI of the script to be downloaded and executed after the gateway installation is complete. Default value is `nil`. | Yes |
|`members`| List | Required | A nested block describes the hardware members of this network gateway. | No |
|`members.hostname`| String | Optional | Hostname of the member.  | Yes |
|`members.domain`| String | Required |The domain of the member  | Yes |
|`members.notes`|String | Optional | Descriptive text of up to 1000 characters about the member.  | Yes |
|`members.datacenter`| String | Required | The data center in which you want to provision the member.  | Yes |
|`members.network_speed`| Integer | Optional |The connection speed (in Mbps) for the member network components. Default value is `100`.  | Yes |
|`members.redundant_power_supply`| Boolean | Optional | When the value is `true`, more power supply is provided. Default value is `false`  | Yes |
|`members.tcp_monitoring`| Boolean | Optional |Whether to enable TCP monitoring for the member. Default value is `false`.  | Yes |
|`members.process_key_name`| String | Optional | The process key name for the member. Default value is  `INTEL_SINGLE_XEON_1270_3_40_2`. Refer to the same attribute on the `ibm_compute_bare_metal` resource.  | Yes |
|`members.package_key_name`| String | Optional | The key name for the network gateway package. You can find available package key names in the SoftLayer API URL `https://api.softlayer.com/rest/v3/SoftLayer_Product_Package/getAllObjects?objectFilter={"type":{"keyName":{"operation":"BARE_METAL_GATEWAY"}}}` that uses your API key as the password. Default value is `NETWORK_GATEWAY_APPLIANCE`. The default value will allow order Single processor multi-core Servers. Use `2U_NETWORK_GATEWAY_APPLIANCE_1O_GBPS` for ordering Dual processor multi-core Servers.  | Yes |
|`members.os_key_name`| String | Optional | The os key name for member. Default value is  `OS_VYATTA_5600_5_X_UP_TO_1GBPS_SUBSCRIPTION_EDITION_64_BIT`. Refer to the same attribute on the `ibm_compute_bare_metal` resource.  | Yes |
|`members.redundant_network`| Boolean | Optional | When the value is `true`, two physical network interfaces are provided with a bonding configuration. Default value is `false`.   | Yes |
|`members.unbonded_network`| Boolean | Optional |  When the value is `true`, two physical network interfaces are provided without a bonding configuration. Default value is `false`.   | Yes |
|`members.tags`| Set | Optional | Tags associated with the VM instance. Permitted characters include: A-Z, 0-9, whitespace, `_` (underscore), `-` (hyphen), `.` (period), and `:` (colon). All other characters are removed.  | Yes |
|`members.public_bandwidth`| Integer | Optional | Allowed public network traffic (in GB) per month. Default value is `20000`.  | Yes |
|`members.memory`| Integer | Required | The amount of memory, expressed in megabytes, that you want to allocate.  | Yes |
|`members.storage_groups`| List | Optional | A nested block describes the storage group for the member of the network gateway. Nested `storage_groups` blocks have the following structure:      | Yes |
|`members.storage_groups.array_type_id`| Integer | Required | The ID of the array type.      | No |
|`members.storage_groups.hard_drives`| List | Required |The list of hard disk associated with the gateway member.      | No |
|`members.storage_groups.array_size`| Integer | Optional | The size of the array.      | No |
|`members.storage_groups.partition_template_id`| Integer | Optional | The partition template ID for the member.  | No |
|`members.ssh_key_ids`| List | Optional |  The SSH key IDs to install on the member.  | Yes |
|`members.post_install_script_uri`| String | Optional | The URI of the script to be downloaded and executed on the member. Default value is `nil`.  | Yes |
|`members.user_metadata`| String | Optional | Arbitrary data to be made available to the member.  | Yes |
|`members.disk_key_names`| List | Optional |  Provide the disk key name. Refer to the same attribute in the `ibm_compute_bare_metal` resource.  | Yes |
|`members.public_vlan_id`| Integer | Optional | ID of the public VLAN.  | Yes |
|`members.private_vlan_id`| Integer | Optional |  ID of the private VLAN.       **NOTE**: If there are two members in this gateway, then both should have same value for `public_vlan_id` and `private_vlan_id`. | Yes |
|`members.ipv6_enabled`| Boolean | Optional | Whether to enable IPv6. Default value is `true`.  | Yes |
|`members.private_network_only`| Boolean | Optional |  Whether to enable a private network only. Default value is `false`.| Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #network-gateway-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the network gateway.|
|`public_ipv4_address`|The public IP address of the network gateway.|
|`private_ipv4_address`|The private IP address of the network gateway.|
|`private_ip_address_id`|The private IP address ID of the network gateway.|
|`private_vlan_id`|The private VLAN ID of the network gateway.|
|`public_ip_address_id`|The public IP address ID of the network gateway.|
|`public_ipv6_address_id`|The public IPv6 address ID for the network gateway.|
|`public_vlan_id`|The public VLAN ID for the network gateway.|
|`status`|Status of the network gateway.|
|`associated_vlans`|A nested block describes the associated VLANs for the member of the network gateway. Nested `associated_vlans` blocks export the following attributes:  |
|`vlan_id`|The VLAN ID.  |
|`network_vlan_id`|The ID of the VLAN that is associated.  |
|`bypass`| Indicates if the VLAN is in bypass or routed mode.|
|`members`|A nested block describes the hardware members of this network gateway. Nested `members` blocks export the following attributes:  |
|`member_id`| ID of the member.  |
|`public_ipv4_address`|Public IPv4 address associated with the member.  |
|`private_ipv4_address`|Private IPv4 address associated with the member.  |
|`ipv6_address`| IPv6 address associated with the member.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_network_gateway_vlan_association`
{: #network-vlan-associate}

Provide a resource to associate a VLAN with a network gateway. The VLANs can be disassociated or updated later to be bypassed or routed.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/services/SoftLayer_Network_Gateway_Vlan).

For more information, about getting started, see the [IBM Virtual Router Appliance Docs](/docs/gateway-appliance?topic=gateway-appliance-getting-started).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #network-vlan-associate-sample}

```
resource "ibm_network_gateway" "gateway" {
  name = "gateway"

  members = [{
    hostname             = "my-virtual-router"
    domain               = "terraformuat1.ibm.com"
    datacenter           = "ams01"
    network_speed        = 100
    private_network_only = false
    tcp_monitoring       = true
    process_key_name     = "INTEL_SINGLE_XEON_1270_3_40_2"
    os_key_name          = "OS_VYATTA_5600_5_X_UP_TO_1GBPS_SUBSCRIPTION_EDITION_64_BIT"
    redundant_network    = false
    disk_key_names       = ["HARD_DRIVE_2_00TB_SATA_II"]
    public_bandwidth     = 20000
    memory               = 4
    ipv6_enabled         = true
  },
  ]
}

resource "ibm_network_gateway_vlan_association" "gateway_vlan_association" {
  gateway_id      = ibm_network_gateway.gateway.id
  network_vlan_id = 645086
}

```
{: codeblock}

### Input parameters
{: #network-vlan-associate-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`gateway_id`| Integer | Required | The ID of the network gateway.| Yes |
|`network_vlan_id`| Integer | Required | The ID of the network VLAN to associate with the network gateway.| Yes |
|`bypass`| Boolean | Optional |Indicates if the VLAN should be in bypass or routed mode. Default value is `true`. |  No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #network-vlan-associate-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the gateway/VLAN association.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_network_interface_sg_attachment`
{: #network-sg-attachment}

Provide a resource to attach security group to a network interface. This allows attachments to be created and deleted.

For more information, see the [IBM Cloud Classic Infrastructure  (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Virtual_Network_SecurityGroup_NetworkComponentBinding).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #network-sg-attachment-sample}

```
data "ibm_security_group" "allowssh" {
  name = "allow_ssh"
}

resource "ibm_compute_vm_instance" "vsi"{
   ....
}
resource "ibm_network_interface_sg_attachment" "sg1" {
    security_group_id = data.ibm_security_group.allowssh.id
    network_interface_id = ibm_compute_vm_instance.vsi.public_interface_id
    //User can increase timeouts 
    timeouts {
      create = "15m"
    }
}
```
{: codeblock}

### Input parameters
{: #network-sg-attachment-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource
|----|-----------| ------ | ----- | ----------|
|`security_group_id`| Integer | Required | The ID of the security group.| Yes |
|`network_interface_id`| Integer | Required | The ID of the network interface to which the security group must be applied.| Yes |
|`soft_reboot`| Boolean | Optional | Default `true`. If set to **true** and a reboot is required to apply the security group attachment for the virtual server instance, then a soft reboot is performed. If set to **false**, no reboot is performed. **Note**: A reboot is always required the first time a security group is applied to a network interface of a virtual server instance that was never rebooted before. | Yes |
{: caption="Table. Available input parameters" caption-side="top"}


### Timeouts
{: #network-sg-attachment-timeouts}

ibm_network_interface_sg_attachment provides the following [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) configuration options:

|Name|Description|
|----|-----------|
|`create`|(Default 15 minutes) Used for Creating Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}




## `ibm_network_public_ip`
{: #public-ip}

Provides a public IP resource to route between servers. This allows public IP's to be created, updated, and deleted. Public IP's are not restricted to routing within the same data center.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/services/SoftLayer_Network_Subnet_IpAddress_Global).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #public-ip-sample}

```
resource "ibm_network_public_ip" "test_public_ip " {
    routes_to = "119.81.82.163"
    notes     = "public ip notes"
}
```
{: codeblock}

### Input parameters
{: #public-ip-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description |
|----|-----------| ------ | ----- |
|`routes_to`| String | Required | The destination IP address that the public IP routes traffic through. The destination IP address can be a public IP address of IBM resources in the same account, such as a public IP address of a VM or public virtual IP addresses of `NetscalerVPXs`.|
|`notes`| String | Optional | Descriptive text to associate with the public IP instance.|
|`tags`| Array of string | Optional | Tags associated with the public IP instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #public-ip-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the public IP.|
|`ip_address`|The address of the public IP.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #public-ip-timeout}

ibm_network_public_ip provides the following [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) configuration options:

|Name|Description|
|----|-----------|
|`create`|(Default 30 minutes) Used for Creating Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}




## `ibm_network_vlan`
{: #vlan}

Provides a VLAN resource. This allows public and private VLANs to be created, updated, and canceled.

If you have a default SoftLayer account, you do not have permission to create a VLAN by using the SoftLayer API. If you want to create a VLAN with Terraform on {{site.data.keyword.cloud_notm}}, you must get the required permissions in advance. Contact a SoftLayer sales person or open a ticket.

You can manage existing VLANs with Terraform on {{site.data.keyword.cloud_notm}} by using the `terraform import` command. The command requires the VLAN IDs, which you can find in the [IBM Cloud infrastructure customer portal](https://cloud.ibm.com/classic/network/vlans). After the VLAN IDs are imported into SoftLayer, the IDs provide useful information such as subnets and child resource counts. When you run the `terraform destroy` command, the billing item for the VLAN is deleted. The VLAN remains in SoftLayer until you delete remaining resources on the VLAN, such as virtual guests, secondary subnets, and firewalls.

For more information, refer to the [{{site.data.keyword.cloud_notm}} API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_Vlan).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vlan-sample}

In the following example, you can create a VLAN:

```
resource "ibm_network_vlan" "test_vlan" {
   name = "test_vlan"
   datacenter = "dal06"
   type = "PUBLIC"
   router_hostname = "fcr01a.dal06"
   tags = [
     "collectd",
     "mesos-master"
   ]
}

```
{: codeblock}

### Input parameters
{: #vlan-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`datacenter`| String | Required |The data center in which the VLAN resides.| Yes |
|`type`| String | Required | The type of VLAN. Accepted values are `PRIVATE` and `PUBLIC`.| Yes |
|`subnet_size`| Integer | Required | The size of the primary subnet for the VLAN. Accepted values are `8`, `16`, `32`, and `64`. This field has been removed.| Yes |
|`name`| String | Optional | The name of the VLAN. Maximum length of 20 characters.| No |
|`router_hostname`| String | Optional | The hostname of the primary router associated with the VLAN.| Yes |
|`tags`| Array of string | Optional |  Tags associated with the VLAN. Permitted characters include: A-Z, 0-9, whitespace, `_` (underscore), `-` (hyphen), `.` (period), and `:` (colon). All other characters are removed. | No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vlan-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the VLAN.|
|`vlan_number`|The VLAN number as recorded within the SoftLayer network. This attribute is configured directly on SoftLayer's networking equipment.|
|`softlayer_managed`|SoftLayer manages the VLAN. If SoftLayer creates the VLAN automatically when SoftLayer creates other resources, this attribute is set to `true`. If a user creates the VLAN by using the SoftLayer API, portal, or ticket, this attribute is set to `false`.|
|`child_resource_count`|A count of the resources, such as virtual servers and other network components, that are connected to the VLAN.|
|`subnets`|The collection of subnets associated with the VLAN.    |
|`subnets.subnet`|The subnet for the VLAN.    |
|`subnets.subnet-type`|A subnet can be one of several types. `PRIMARY, ADDITIONAL_PRIMARY, SECONDARY, ROUTED_TO_VLAN, SECONDARY_ON_VLAN, STORAGE_NETWORK, and STATIC_IP_ROUTED`. A `PRIMARY` subnet is the primary network that is bound to a VLAN within the SoftLayer network. An `ADDITIONAL_PRIMARY` subnet is bound to a network VLAN to augment the pool of available primary IP addresses that might be assigned to a server. A `SECONDARY` subnet is any of the secondary subnets bound to a VLAN interface. A `ROUTED_TO_VLAN` subnet is a portable subnet that can be routed to any server on a VLAN. A `SECONDARY_ON_VLAN` subnet also doesn't exist as a VLAN interface, but is routed directly to a VLAN instead of a single IP address by SoftLayer's.    |
|`subnets.subnet-size`|The size of the subnet for the VLAN.    |
|`subnets.gateway`|A subnet gateway address.    |
|`subnets.cidr`|A subnet Classless Inter-Domain Routing prefix. The number in the range of 0 - 32 signifying the number of bits in a subnet mask. |
{: caption="Table 1. Available output parameters" caption-side="top"}

### Timeouts
{: #vlan-timeout}

The `timeouts` block allows you to specify [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) for certain actions:

- **create**: (Defaults to 10 mins) Used when creating the VLAN.
- **delete**: (Defaults to 10 mins) Used when deleting the VLAN. There might be some resources (like Virtual Guests) on the VLAN. The VLAN delete request is issued once there are no Virtual Guests on the VLAN.


## `ibm_network_vlan_spanning`
{: #vlan-spanning}

This resource configures the VLAN spanning attribute for an IaaS account. By default VLAN spanning on the private network is disabled (off) and servers provisioned on separate private VLANs will not be able to communicate with each other over the private network. When enabled, the private network VLAN spanning service allows all private network VLANs to communicate with one another and hence all servers in the account to communicate with each other. Future servers will be added as they are provisioned. VLAN spanning enables servers to communicate across VLANs in the same data center and across data centers. 

VLAN Spanning must be enabled to use Security Groups containing servers provisioned over multiple VLANs or across multiple data centers and regions. Note VLAN Spanning does not implement network security or firewalls and must be used with Security Groups or Virtual Router Appliances (Vyatta or Juniper) to provide network isolation. 

VRF at an IaaS account level can be used as an alternative to VLAN Spanning and is required if DirectLink is used.  



### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #vlan-spanning-sample}

```
resource "ibm_network_vlan_spanning" "spanning" {
   "vlan_spanning" = "on"
}`
```
{: codeblock}


### Input parameters
{: #vlan-spanning-input}

The following arguments are supported:

|Name|Description|
|----|-----------|
|`vlan_spanning`|(Required, string) Indicate if you want to enable VLAN spanning (`on`) or disable VLAN spanning (`off`). |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #vlan-spanning-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the VLAN spanning resource.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_object_storage_account`
{: #os-account}

Retrieve the account name for an existing Object Storage instance within your IBM account. If no Object Storage instance exists, you can use this resource to order an Object Storage instance and to store the account name.

Do not use this resource for managing the lifecycle of an Object Storage instance in IBM. For lifecycle management, see the [Swift API](https://docs.openstack.org/api-ref/object-store/) or [Swift resources](https://github.com/TheWeatherCompany/terraform-provider-swift).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #os-account-sample}

```
resource "ibm_object_storage_account" "foo" {
}
```
{: codeblock}

### Input parameters
{: #os-account-input}

|Name|Description|
|----|-----------|
|`tags`|(Optional, array of strings) Tags associated with the {{site.data.keyword.cos_full_notm}} account instance. **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.


### Output parameters
{: #os-account-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The Object Storage account name, which you can use with Swift resources.|
{: caption="Table. Available input parameters" caption-side="top"}

## `ibm_security_group`
{: #sec-group}

Provides a networking security group resource that controls access to the public and private interfaces of a virtual server instance. This resource allows security groups to be created, updated, and deleted. To create rules for the security group, use the `security_group_rule` resource.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_SecurityGroup).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #sec-group-sample}

```
resource "ibm_security_group" "sg1" {
    name = "sg1"
    description = "allow my app traffic"
}
```
{: codeblock}

### Input parameters
{: #sec-group-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`name`| String | Required | The descriptive name that is used to identify the security group.| Yes |
|`description`| String | Optional | More details to describe the security group.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #sec-group-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the security group.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_security_group_rule`
{: #sec-group-rule}

Provide a rule for a security group. You can set the IP range to manage incoming (ingress) and outgoing (egress) traffic to a virtual server instance. This resource allows rules for security groups to be created, updated, and deleted. To create the security group, use the `security_group` resource.

For more information, see the [IBM Cloud Classic Infrastructure (SoftLayer)  API Docs](http://sldn.softlayer.com/reference/datatypes/SoftLayer_Network_SecurityGroup_Rule).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #sec-group-rule-sample}

```
resource "ibm_security_group_rule" "allow_port_8080" {
    direction = "ingress"
    ether_type = "IPv4"
    port_range_min = 8080
    port_range_max = 8080
    protocol = "tcp"
    security_group_id = 123456
}
```
{: codeblock}

### Input parameters
{: #sec-group-rule-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`direction`| String | Required | The direction of traffic. Accepted values: `ingress` or `egress`.| No |
|`ether_type`| String | Optional | The IP version. Accepted values  (case-sensitive): `IPv4` or `IPv6`. Default value is `IPv4`.| No |
|`port_range_min`| Integer | Optional | The start of the port range for allowed traffic.| No |
|`port_range_max`| Integer | Optional | The end of the port range for allowed traffic.| No |
|`protocol`| String | Optional |  The IP protocol type. Accepted values (case-sensitive): `icmp`,`tcp`, or `udp`.| No |
|`remote_group_id`| Integer | Optional | The ID of the remote security group allowed as part of the rule.       **NOTE**: Conflicts with `remote_ip`.| No |
|`remote_ip`| String | Optional |  The CIDR or IP address for allowed connections.       **NOTE**: Conflicts with `remote_group_id`.| No |
|`security_group_id`| Integer | Required | The ID of the security group this rule belongs to.| Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #sec-group-rule-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the security group rule.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_storage_block`
{: #storage-block}

Provides a block storage resource. This allows iSCSI-based Endurance and Performance block storage to be created, updated, and deleted. For more information, about Block storage, see [Learn about Block Storage](/docs/BlockStorage?topic=BlockStorage-getting-started). 

Block storage can be accessed and mounted through a Multipath Input/Output Internet Small Computer System Interface (iSCSI) connection.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #storage-block-sample}

In the following example, you can create 20G of Endurance block storage with 10G snapshot capacity and 0.25 IOPS/GB.

```
resource "ibm_storage_block" "test1" {
        type = "Endurance"
        datacenter = "dal05"
        capacity = 20
        iops = 0.25
        os_format_type = "Linux"

        # Optional fields
        allowed_virtual_guest_ids = [ 27699397 ]
        allowed_ip_addresses = ["10.40.98.193", "10.40.98.200"]
        snapshot_capacity = 10
        hourly_billing = true
}
```
{: codeblock}

In the following example, you can create 20G of Performance block storage and 100 IOPS.

```
resource "ibm_storage_block" "test2" {
        type = "Performance"
        datacenter = "dal05"
        capacity = 20
        iops = 100
        os_format_type = "Linux"

        # Optional fields
        allowed_virtual_guest_ids = [ 27699397 ]
        allowed_ip_addresses = ["10.40.98.193", "10.40.98.200"]
        hourly_billing = true
}
```
{: codeblock}


### Input parameters
{: #storage-block-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`type`| String | Required | The type of the storage. Accepted values are `Endurance` and `Performance`.| Yes |
|`datacenter`| String | Required |The data center where you want to provision the block storage instance.| Yes |
|`capacity`| Integer | Required | The amount of storage capacity that you want to allocate, specified in gigabytes.|
|`iops`| Float | Required | The IOPS value for the storage. For supported values.| No |
|`os_format_type`| String | Required | The OS type used to format the storage space. This OS type must match the OS type that connects to the LUN. [Log in to the IBM Cloud Classic Infrastructure API to see available OS format types](https://api.softlayer.com/rest/v3/SoftLayer_Network_Storage_Iscsi_OS_Type/getAllObjects/). Use your API as the password to log in. Log in and find the key called `name`.| Yes |
|`snapshot_capacity`| Integer | Optional | The amount of snapshot capacity to allocate, specified in gigabytes.| Yes |
|`allowed_virtual_guest_ids`| Array of integers | Optional | The virtual guests that you want to give access to this instance. Virtual guests must be in the same data center as the block storage. You can also use this field to import the list of virtual guests that have access to this storage from the `block_storage_ids` argument in the `ibm_compute_vm_instance` resource.| No |
|`allowed_hardware_ids`| Array of integers | Optional | The Bare Metal servers that you want to give access to this instance. Bare Metal servers must be in the same data center as the block storage. You can also use this field to import the list of Bare Metal servers that have access to this storage from the `block_storage_ids` argument in the `ibm_compute_bare_metal` resource.| No |
|`allowed_ip_addresses`| Array of string | Optional | The IP addresses that you want to give access to this instance. IP addresses must be in the same data center as the block storage.| No |
|`notes`| Strings | Optional |  A descriptive note that you want to associate with the block storage.| No |
|`tags`| Array of string | Optional | Tags associated with the storage block instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
|`hourly_billing`| Boolean | Optional | Set true to enable hourly billing. Default value is **false**   **NOTE**: `Hourly billing` is only available in updated data centers with improved capabilities. Refer to the link to get the updated list of data centers. See [Data Center locations](/docs/FileStorage?topic=FileStorage-selectDC)| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #storage-block-output}

The following attributes are exported:

|Name|Data type |Description|
|----|-----------| -------- |
|`id`|String |The unique identifier of the storage.|
|`hostname`|String|The fully qualified domain name of the storage.|
|`allowed_virtual_guest_info`|String|Deprecated please use `allowed_host_info` instead.|
|`allowed_hardware_info`|String|Deprecated please use `allowed_host_info` instead.|
|`allowed_host_info`|String|The user name, password, and host IQN of the hosts with access to the storage.|
|`lunid` | String| The `LUN` ID of the storage device. |
|`volumename`|String|The name of the storage volume.|
{: caption="Table 1. Available output parameters" caption-side="top"}



## `ibm_storage_evault`
{: #storage-evault}

Provides an EVault  storage resource. This allows [IBM Cloud Backup](/docs/Backup?topic=Backup-getting-started) storage to be created, updated, and deleted.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #storage-evault-sample}

In the following example, you can create 20G of EVault storage.

```
resource "ibm_storage_evault" "test" {
  datacenter          = "dal05"
  capacity            = "20"
  virtual_instance_id = "62870765"
}
```
{: codeblock}

### Input parameters
{: #storage-evault-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`datacenter`| String | Required |The data center where you want to provision the EVault  storage instance.| Yes |
|`capacity`| Integer | Required | The amount of storage capacity that you want to allocate, specified in gigabytes.| No |
|`virtual_instance_id`| Integer | Optional | The ID of the virtual instance.     **NOTE**: Conflicts with `hardware_instance_id`.| Yes |
|`hardware_instance_id`| Integer | Optional | The ID of the hardware instance.     **NOTE**: Conflicts with `virtual_instance_id`.| Yes |
|`tags`| Array of string | Optional | Tags associated with the storage EVault instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #storage-evault-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the EVault.|
|`username`|The username of the EVault.|
|`password`|The password of the EVault.|
|`service_resource_name`|The name of an EVault storage network resource.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #storage-evault-timeout}

ibm_storage_evault provides the following [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) configuration options:

|Name|Description|
|----|-----------|
|`create`|(Default 10 minutes) Used for Creating Instance.|
|`update`|(Default 10 minutes) Used for Updating Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}




## `ibm_storage_file`
{: #storage-file}

ibm_storage_file resource provides a file storage resource. This allows NFS-based Endurance and Performance [file storage](/docs/FileStorage?topic=FileStorage-getting-started) to be created, updated, and deleted.

File storage is mounted by using the NFS protocol. For example, a file storage resource with the `hostname` argument set to `nfsdal0501a.service.softlayer.com` and the `volumename` argument set to ` IBM01SV278685_7` has the mount point `nfsdal0501a.service.softlayer.com:\IBM01SV278685_7`.

See [Mounting File Storage](/docs/FileStorage?topic=FileStorage-mountingLinux) for NFS configuration.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #storage-file-sample}

In the following example, you can create 20G of Endurance file storage with a 10G snapshot capacity and 0.25 IOPS/GB.

```
resource "ibm_storage_file" "fs_endurance" {
  type       = "Endurance"
  datacenter = "dal06"
  capacity   = 20
  iops       = 0.25

  # Optional fields
  allowed_virtual_guest_ids = ["28961689"]
  allowed_subnets           = ["10.146.139.64/26"]
  allowed_ip_addresses      = ["10.146.139.84"]
  snapshot_capacity         = 10
  hourly_billing            = true

  # Optional fields for snapshot
  snapshot_schedule = [
    {
      schedule_type   = "WEEKLY"
      retention_count = 20
      minute          = 2
      hour            = 13
      day_of_week     = "SUNDAY"
      enable          = true
    },
    {
      schedule_type   = "HOURLY"
      retention_count = 20
      minute          = 2
      enable          = true
    }
  ]
}

```
{: codeblock}

In the following example, you can create 20G of Performance file storage with 100 IOPS.

```
resource "ibm_storage_file" "fs_performance" {
        type = "Performance"
        datacenter = "dal06"
        capacity = 20
        iops = 100
        # Optional fields
        allowed_virtual_guest_ids = [ "28961689" ]
        allowed_subnets = [ "10.146.139.64/26" ]
        allowed_ip_addresses = [ "10.146.139.84" ]
        hourly_billing = true
}
```

### Input parameters
{: #storage-file-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`type`| String | Required | The type of the storage. Accepted values are `Endurance` and `Performance`| Yes |
|`datacenter`| String | Required |The data center where you want to provision the file storage instance.| Yes |
|`capacity`| Integer | Required |The amount of storage capacity that you want to allocate, expressed in gigabytes.| No |
|`iops`| Float | Required | The IOPS value for the storage instance. For supported values, see [Provisioning](/docs/FileStorage?topic=FileStorage-getting-started#provconsiderations). | No |
|`snapshot_capacity`| Integer | Optional | The amount of snapshot capacity that you want to allocate, expressed in gigabytes.| Yes |
|`allowed_virtual_guest_ids`| Array of integers | Optional | The virtual guests that you want to give access to this instance. Virtual guests must be in the same data center as the block storage. You can also use this field to import the list of virtual guests that have access to this storage from the `block_storage_ids` argument in the `ibm_compute_vm_instance` resource.| No |
|`allowed_hardware_ids`| Array of integers | Optional | The Bare Metal servers that you want to give access to this instance. Bare Metal servers must be in the same data center as the block storage. You can also use this field to import the list of Bare Metal servers that have access to this storage from the `block_storage_ids` argument in the `ibm_compute_bare_metal` resource.| No |
|`allowed_subnets`| Array of integers | Optional | The subnets that you want to give access to this instance. Subnets must be in the same data center as the block storage.| No |
|`allowed_ip_addresses`| Array of string | Optional | The IP addresses that you want to allow. IP addresses must be in the same data center as the block storage. | No |
|`snapshot_schedule`| Array | Optional | Applies only to Endurance storage. Specifies the parameters required for a snapshot schedule.    | No |
|`snapshot_schedule.schedule_type`| String | Optional | The snapshot schedule type. Accepted values are `HOURLY`, `WEEKLY`, and `DAILY`.    | No |
|`snapshot_schedule.retention_count`| Integer | Optional | The retention count for a snapshot schedule. Required for all types of `schedule_type`.    | No |
|`snapshot_schedule.minute`| Integer | Optional | The minute for a snapshot schedule. Required for all types of `schedule_type`. |  No |
|`snapshot_schedule.hour`| Integer | Optional | The hour for a snapshot schedule. Required if `schedule_type` is set to `DAILY` or `WEEKLY`.    | No |
|`snapshot_schedule.day_of_week`| String | Optional | The day of the week for a snapshot schedule. Required if the `schedule_type` is set to `WEEKLY`.    | No |
|`snapshot_schedule.enable`| Boolean | Optional | Whether to disable an existing snapshot schedule.| No |
|`notes`| String | Optional |  Descriptive text to associate with the file storage.  | No |
|`tags`| Arrays of Strings | Optional |  Tags associated with the file storage instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.  | No |
|`hourly_billing`| Boolean | Optional |  Set true to enable hourly billing. Default is false.   **NOTE**: `Hourly billing` is only available in updated data centers with improved capabilities. Refer to the [link](/docs/FileStorage?topic=FileStorage-selectDC) to get the updated list of data centers.| Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #storage-file-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the storage volume.|
|`hostname`|The fully qualified domain name of the storage.|
|`volumename`|The name of the storage volume.|
|`mountpoint`|The network mount address of the storage.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_subnet`
{: #subnet}

This resource provides portable and static subnets that consist of either IPv4 and IPv6 addresses. Users are able to create 
public portable subnets, private portable subnets, and public static subnets with an IPv4 option, and public portable subnets and public static subnets with an IPv6 option. 
 
The portable IPv4 subnet is created as a secondary subnet on a VLAN. IP addresses in the portable subnet can be assigned as secondary IP 
addresses for IBM resources in the VLAN. Because each portable subnet has a default gateway IP address, network IP address, and broadcast IP address, the number of usable IP addresses is `capacity` - 3. A `capacity` of 4 means that the number of usable IP addresses is 1; a `capacity` of 8 means that the number of usable IP addresses is 5. For example, consider a portable subnet of `10.0.0.0/30` that has `10.0.0.1` as a default gateway IP address, `10.0.0.0` as a network IP address, and `10.0.0.3` as a broadcast IP address. Only `10.0.0.2` can be assigned to IBM resources as a secondary IP address. 

The static IPv4 subnet provides secondary IP addresses for primary IP addresses. It provides secondary IP addresses for IBM resources such as virtual servers, Bare Metal servers, and `NetscalerVPXs`. Consider a virtual server that requires secondary IP addresses. Users can create a static subnet on the public IP address of the virtual server. Unlike the portable subnet, the number of usable IP addresses for the static subnet is the same as the value of `capacity`. For example, when a static subnet of `10.0.0.0/30` has a `capacity` of 4, then four IP addresses (10.0.0.0 - 10.0.0.3) can be used as secondary IP addresses. 

Both the public portable IPv6 subnet and the public static IP only accept `64` as a value for the `capacity` attribute. They provide 2^64 IP addresses. For more detail, refer to [IPv6 address](/docs/subnets?topic=subnets-about-subnets-and-ips).

### Sample Terraform on {{site.data.keyword.cloud_notm}} code of portable subnet
{: #subnet-sample}
The following example creates a private portable subnet which has one available IPv4 address:

```
resource "ibm_subnet" "portable_subnet" {
  type = "Portable"
  private = true
  ip_version = 4
  capacity = 4
  vlan_id = 1234567
  notes = "portable_subnet"
  //User can increase timeouts 
  timeouts {
    create = "45m"
  }
}
```
{: codeblock}

Users can use Terraform on {{site.data.keyword.cloud_notm}} built-in functions to get IP addresses from `portable subnet`. The following example returns the first usable IP address of the portable subnet `test`.:

```
resource "ibm_subnet" "test" {
  type = "Portable"
  private = true
  ip_version = 4
  capacity = 4
  vlan_id = 1234567
}


## Use a built-in function cidrhost with index 1.
output "first_ip_address" {
  value = cidrhost(ibm_subnet.test.subnet_cidr,1)
}

```
{: codeblock}

### Example Usage of static subnet
The following example creates a public static subnet which has four available IPv4 addresses:

```
resource "ibm_subnet" "static_subnet" {
  type = "Static"
  private = false
  ip_version = 4
  capacity = 4
  endpoint_ip="151.1.1.1"
  notes = "static_subnet_updated"
}
```
{: codeblock}

Users can use Terraform on {{site.data.keyword.cloud_notm}} built-in functions to get IP addresses from `subnet`. The following example returns the first usable IP address in the static subnet `test`:

```
resource "ibm_subnet" "test" {
  type = "Static"
  private = false
  ip_version = 4
  capacity = 4
  endpoint_ip="159.8.181.82"
}


## Use a built-in function cidrhost with index 0.
output "first_ip_address" {
  value = cidrhost(ibm_subnet.test.subnet_cidr,0)
}

```
{: codeblock}

### Input parameters
{: #subnet-input}

The following arguments are supported:

|Name| Data type | Required / optional | Description | Forces new resource |
|----|-----------| ------ | ----- | ----------|
|`private`| Boolean | Optional |Specifies whether the network is public or private.| Yes |
|`type`| String | Required |The type of the subnet. Accepted values are `portable` and `static`.| Yes |
|`ip_version`| Integer | Optional | The IP version of the subnet. Accepted values are 4 and 6.| Yes |
|`capacity`| Integer | Required | The size of the subnet. <ul><li>Accepted values for a public portable IPv4 subnet are 4, 8, 16, and 32. </li><li> Accepted values for a private portable IPv4 subnet are 4, 8, 16, 32, and 64. </li><li>Accepted values for a public static IPv4 subnet are 1, 2, 4, 8, 16, and 32. </li><li>Accepted value for a public portable IPv6 subnet is 64. A /64 block is created and 2^64 IP addresses are provided. </li><li>Accepted value for a public static IPv6 subnet is 64. A /64 block is created and 2^64 IP addresses are provided.</li></ul>| Yes |
|`vlan_id`| Integer | Optional | The VLAN ID for portable subnet. You can configure both public and private VLAN ID. You can find accepted values in the [SoftLayer VLAN documentation](https://cloud.ibm.com/classic/network/vlans) by clicking the VLAN that you want and noting the ID in the resulting URL. You can also refer to a VLAN name by using a data source.| Yes |
|`endpoint_ip`| String | Optional | The target primary IP address for a static subnet. Only public IP addresses of virtual servers, Bare Metal servers, and `NetscalerVPXs` can be configured as an `endpoint_ip`. The `static subnet` will be created on the VLAN where the `endpoint_ip` is located.| Yes |
|`notes`| String | Optional | Descriptive text or comments about the subnet.| No |
|`tags`| Array of Strings | Optional |  Tags associated with the subnet instance.     **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #subnet-output}

The following attributes are exported:

|Name|Description|
|----|-----------|
|`id`|The unique identifier of the subnet.|
|`subnet_cidr`|The IP address / CIDR format (ex. 10.10.10.10/28), which you can use to get an available IP address in `subnet`.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #subnet-timeout}

ibm_subnet provides the following [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) configuration options:

|Name|Description|
|----|-----------|
|`create`|(Default 30 minutes) Used for Creating Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}




## `ibm_ssl_certificate`
{: #ssl-cert}

Provides an SSL certificate resource. This allows SSL certificates to be requested, and delete request for SSL certificates.

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #ssl-cert-sample}

In the following example, you can use a certificate on file:

```
resource "ibm_ssl_certificate" "my_ssllllll" {
  	certificate_signing_request= "-----BEGIN CERTIFICATE REQUEST-----\nCERTIFICATE CONTENT\n-----END CERTIFICATE REQUEST-----"
	organization_information = {
		org_address {
			org_address_line1= "abc"
			org_address_line2= "xyz"
			org_city="pune"
			org_country_code= "IN"
			org_state="MH"
			org_postal_code= "411045"
		}
		org_organization_name= "GSLAB"
		org_phone_number= "8657072955"
		org_fax_number = ""
	}	
	technical_contact_same_as_org_address_flag = "false"
	technical_contact {
		tech_address {
			tech_address_line1= "fcb"
			tech_address_line2= "pqr"
			tech_city="pune"
			tech_country_code= "IN"
			tech_state="MH"
			tech_postal_code= "411045"
		}
		tech_organization_name= "IBM"
		tech_phone_number= "8657072955"
		tech_fax_number = ""
		tech_first_name = "qwerty"
		tech_last_name = "ytrewq"
		tech_email_address = "abc@gmail.com"
		tech_title= "SSL CERT"
	}
	billing_contact {
		billing_address {
			billing_address_line1= "plk"
			billing_address_line2= "PLO"
			billing_city="PUNE"
			billing_country_code= "IN"
			billing_state="MH"
			billing_postal_code= "411045"
		}
		billing_organization_name= "IBM"
		billing_phone_number= "8657072955"
		billing_fax_number = ""
		billing_first_name = "ERTYU"
		billing_last_name = "SDFGHJK"
		billing_email_address = "kjjj@gsd.com"
		billing_title= "PFGHJK"
	}
	administrative_contact {
		admin_address {
			admin_address_line1= "fghds"
			admin_address_line2= "twyu"
			admin_city="pune"
			admin_country_code= "IN"
			admin_state="MH"
			admin_postal_code= "411045"
		}
		admin_organization_name = "GSLAB"
		admin_phone_number = "8657072955"
		admin_fax_number = ""
		admin_first_name = "DFGHJ"
		admin_last_name = "dfghjkl"
		admin_email_address = "fghjk@gshhds.com"
		admin_title= "POIUYGHJK"
	}	
	administrative_contact_same_as_technical_flag = "false"
	billing_contact_same_as_technical_flag = "false"	
	billing_address_same_as_organization_flag = "false"
	administrative_address_same_as_organization_flag = "false"
	ssl_type="SSL_CERTIFICATE_QUICKSSL_PREMIUM_2_YEAR"
	renewal_flag= true
	server_count= 1
	server_type= "apache2"
	validity_months= 24
	order_approver_email_address= "admin@pune.in"	
}
```
{: codeblock}


### Input parameters
{: #ssl-cert-input}

The following arguments are supported:

|Name|Description|
|----|-----------|
|`certificateSigningRequest`|(Required, string) The Certificate Signing Request which is specially formatted encrypted message sent from a Secure Sockets Layer (SSL) digital certificate applicant to a certificate authority.|
|`sslType`|(Required, string) The SSL certificate type.|
|`serverType`|(Required, string) The server type for which we are requesting SSL certificate.|
|`serverCount`|(Required, string) The number of servers with provided server type.|
|`validityMonths`|(Required, integer) The validity of SSL certificate in months it should be multiple of 12.|
|`orderApproverEmailAddress`|(Required, string) The email of approver to approve SSL certificate request.|
|`organization_information`| (Required, set) Organization information from issuer belongs to.	|
|`organization_information.org_address`|(Required, string) Organization address of the issuer.		|
|`organization_information.org_address.org_addressLine1`|(Required, string) The address of organization who is requesting for SSL certificate.		|
|`organization_information.org_address.org_addressLine2`|(optional, string) The address of organization who is requesting for SSL certificate.		|
|`organization_information.org_address.org_city`|(Required, string) The city of organization which is requesting for SSL certificate.		|
|`organization_information.org_address.org_postalCode`|(Required, integer) The postal code for the city of organization.		|
|`organization_information.org_address.org_state`|(Required, string) The two letter state code of organization who is requesting for SSL certificate. Allowed value for country which doesn't have states is `OT`.		|
|`organization_information.org_address.org_countryCode`|(Required, string) The two letter country code of organization.	|
|`organization_information.org_organizationName`|(Required, string) Name of organization.	|
|`organization_information.org_phone_number`|(Required, string) Phone number of organization	|
|`organization_information.org_fax_number`|(Optional, string) Fax number for organization|
|`technical_contact`|(Required, set) Technical contact details of issuer.	|
|`technical_contact.tech_address`|(Optional, set) Technical address details		|
|`technical_contact.tech_address.tech_addressLine1`|(Required, string) The address for technical contact.		|
|`technical_contact.tech_address.tech_addressLine2`|(Optional, string) The address for technical contact.		|
|`technical_contact.tech_address.tech_city`|(Required, string) The city for technical contact.		|
|`technical_contact.tech_address.tech_postalCode`|(Required, integer) The postal code for technical contact.		|
|`technical_contact.tech_address.tech_state`|(Required, string) The two letter state code of technical contact. Allowed value for country which doesn't have states is `OT`.		|
|`technical_contact.tech_address.tech_countryCode`|(Required, string) The two letter country code for technical contact.	|
|`technical_contact.tech_organizationName`|(Required, string) Name of organization for technical contact.	|
|`technical_contact.tech_firstName`|(Required, string) The first name for technical contact.	|
|`technical_contact.tech_lastName`|(Required, string) The last name for technical contact.	|
|`technical_contact.tech_title`|(Required, string) The title for technical contact.	|
|`technical_contact.tech_emailAddress` |(Required, string) email address for technical contact.	|
|`technical_contact.tech_phone_number`| (Required, string) phone number for technical detail.	|
|`technical_contact.tech_fax_number`|(Optional, string) Fax number for technical detail.|
|`administrative_contact`|(Optional, set) Administrator contact details.	|
|`administrative_contact.admin_address`|(Optional, set) Administrator address details.		|
|`administrative_contact.admin_address.admin_addressLine1`|(Optional, string) The address for administrative contact.|
|`administrative_contact.admin_address.admin_addressLine2`|(optional, string) The address for administrative contact.		|
|`administrative_contact.admin_address.admin_city`|(Optional, string) The city for administrative contact.		|
|`administrative_contact.admin_address.admin_postalCode`|(Optional, integer) The postal code for administrative contact.		|
|`administrative_contact.admin_address.admin_state`|(Optional, string) The two letter state code of administrative contact. Allowed value for country which doesn't have states is `OT`.		|
|`administrative_contact.admin_address.admin_countryCode`|(Optional, string) The two letter country code for administrative contact.	|
|`administrative_contact.admin_organizationName`|(Optional, string) Name of organization for administrative contact.	|
|`administrative_contact.admin_firstName`|(Optional, string) The first name for administrative contact.	|
|`administrative_contact.admin_lastName`|(Optional, string) The last name for administrative contact.	|
|`administrative_contact.admin_title`|(Optional, string) The title for administrative contact.	|
|`administrative_contact.admin_emailAddress` |(Optional, string) email address for administrative contact.	|
|`administrative_contact.admin_phone_number`|(Optional, string) Phone number of administrator.	|
|`administrative_contact.admin_fax_number`|(Optional, string) Fax number for administrator.|
|`billing_contact`|(Optional, set) Billing Contact details.	|
|`billing_contact.billing_address`|(Optional, set) Billing address details.		|
|`billing_contact.billing_address.billing_addressLine1`|(Optional, string) The address for billing contact.		|
|`billing_contact.billing_address,billing_addressLine2`|(optional, string) The address for billing contact.		|
|`billing_contact.billing_address.billing_city`|(Optional, string) The city for billing contact.		|
|`billing_contact.billing_address.billing_postalCode`|(Optional, integer) The postal code for billing contact.		|
|`billing_contact.billing_address.billing_state`|(Optional, string) The two letter state code of billing contact. Allowed value for country which doesn't have states is `OT`.		|
|`billing_contact.billing_address.billing_countryCode`|(Optional, string) The two letter country code for billing contact.	|
|`billing_contact.billing_organizationName`|(Optional, string) Name of organization for billing contact.	|
|`billing_contact.billing_firstName`|(Optional, string) The first name for billing contact.	|
|`billing_contact.billing_lastName`|(Optional, string) The last name for billing contact.	|
|`billing_contact.billing_title`|(Optional, string) The title for billing contact.	|
|`billing_contact.billing_emailAddress`|(Optional, string) email address for billing contact.	|
|`billing_contact.billing_phone_number`|(Optional, string) Phone number for billing contact.	|
|`billing_contact.billing_fax_number`|(Optional, string) Fax number for billing contact.|
|`technicalContactSameAsOrgAddressFlag` |(Optional, bool) If your organization address and technical contact address are the same make this flag as true and skip technical contact address details.|
|`administrativeContactSameAsTechnicalFlag` |(Required, bool)- If your technical contact details and administrative contact details are the same then make this as true and skip details of administrative contact.|
|`billingContactSameAsTechnicalFlag` |(Required, bool)- If your technical contact details and billing contact details are the same then make this as true and skip details of billing contact. |
|`administrativeAddressSameAsOrganizationFlag` |(Required, bool) - If administrative address is same as organization address then make this flag as true and skip address details.|
|`billingAddressSameAsOrganizationFlag` |(Required, bool) - If billing address is same as organization address then make this flag as true and skip address details. |
