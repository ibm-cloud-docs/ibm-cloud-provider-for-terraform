---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider plugin, terraform power resources, terraform power systems resources, terraform power

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



# Power Systems data sources
{: #power-data-sources}

Review the data sources that you can use to retrieve information about the [Provisioning a virtual server](/docs/hp-virtual-servers?topic=hp-virtual-servers-provision). All data sources are imported as read-only information. You can reference the output parameters for each data source by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

To find supported input parameter values, you can use the Power Systems CLI plug-in in {{site.data.keyword.cloud_notm}}. To install the plug-in, run `ibmcloud plugin install pi`. 
{: tip}

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_pi_image`
{: #power-image}

Retrieve the details of an image that you can use in your Power Systems Virtual Server instance. The image represents the version of the operation system that is installed in your Power Systems Virtual Server instance.
{: shortdesc}

### Sample Terraform code
{: #power-image-sample}

The following example shows how to retrieve information about the `7200-03-03` image ID. 
{: shortdesc}

```
data "ibm_pi_image" "ds_image" {
  pi_image_name        = "7200-03-03"
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameters
{: #power-image-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The cloud instance ID associated with the account. | 
| `pi_image_name` | String | Required | The ID of the image. To find supported images, run the `ibmcloud pi images` command. |

### Output parameters
{: #power-image-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `architecture` | String | The CPU architecture that the image is designed for. | 
| `id` | String | The unique identifier of the image. |
| `operatingsystem` | String | The operating system that is installed with the image. |
| `size` | String | The size of the image in megabytes. |
| `state` | String | The state for this image. | 





## `ibm_pi_images`
{: #power-images}

Retrieve a list of supported images that you can use in your Power Systems Virtual Server instance. The image represents the version of the operation system that is installed in your Power Systems Virtual Server instance.
{: shortdesc}

### Sample Terraform code
{: #power-images-sample}

The following example retrieves all images for a cloud instance ID. 
{: shortdesc}

```
data "ibm_pi_images" "ds_images" {
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameter
{: #power-images-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The cloud instance ID that is associated with the account. | 

### Output parameters
{: #power-images-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `image_info` | List of images | A list of all supported images. | 
| `image_info.href` | String | The hyper link of an image. | 
| `image_info.id` | String | The unique identifier of an image. | 
| `image_info.name`| String | The name of an image. |
| `image_info.state` | String | The state of an image. |






## `ibm_pi_instance`
{: #power-instance}

Retrieve information about a Power Systems Virtual Server instance. 
{: shortdesc}

### Sample Terraform code
{: #power-instance-sample}

The following example shows how to retrieve information about an instance that is named `myinstance`. 

```
data "ibm_pi_instance" "ds_instance" {
  pi_instance_name     = "myinstance"
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameters
{: #power-instance-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The service instance associated with the account. |
| `pi_instance_name` | String | Required | The name of the instance. |


### Output parameters
{: #power-instance-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `addresses` | List of objects | The address associated with this instance. |
| `addresses.ip`|String|The IP address of the instance.|
| `addresses.macaddress`|String| The MAC address of the instance. |
| `addresses.network_id`|String|The network ID of the instance. |
| `addresses.network_name`|String|The network name of the instance. |
| `addresses.type`|String| The type of the network. |
| `addresses.externalip`|String| The external IP address of the instance.|
|`health_status`|String|The health of the instance.|
| `id` | String | The unique identifier of the instance. |
| `state` | String | The state of the instance.|
| `memory`|String|The amount of memory that is allocated to the instance.|
| `min_processors`|Integer|The minimum number of processors that must be allocated to the instance.| 
| `max_processors`|Integer|The maximum number of processors that can be allocated to the instance without shutting down or rebooting the `LPAR`.|
| `max_virtual_cores` | Integer | The maximum value that you increase without a reboot. |
| `min_memory`|Integer|The minimum amount of memory that must be allocated to the instance.|
| `max_memory`|Integer|The maximum amount of memory that can be allocated to the instance without shutting down or rebooting the `LPAR`.|
| `min_virtual_cores` | Integer |The minimum cores assigned to an instance.|
|`processors`|String|The number of processors that are allocated to the instance.|
|`proctype`|String|The procurement type of the instance. Supported values are `shared` and `dedicated`. |
|`status`|String|The status of the instance.|
| `virtual_cores_assigned` | Integer | The virtual cores that are assigned to the instance. |
|`volumes`|List of strings|The list of volume IDs that are attached to the instance. |






## `ibm_pi_instance_ip`
{: #power-instance-ip}

Retrieve information about a Power Systems Virtual Server instance IP address. 
{: shortdesc}

### Sample Terraform code
{: #power-instance-ip-sample}

The following example shows how to retrieve information about an instance IP for an instance that is named `myinstance`. 

```
data "ibm_pi_instance" "ds_instance" {
  pi_instance_name     = "myinstance"
  pi_network_name = "APP"
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameters
{: #power-instance-ip-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The service instance associated with the account. |
| `pi_instance_name` | String | Required | The name of the instance. |
| `pi_network_name`|String|Required| The subnet that the instance belongs to. 


### Output parameters
{: #power-instance-ip-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `ip`|String| The IP address that is attached to this instance from the subnet.|
|`id`|String|The unique identifier of the network.|
|`macaddress`|String|The MAC address of the network that is attached to this instance.|
|`external_ip`|String|The external IP of the network that is attached to this instance.|
|`type`|String| The type of the network that is attached to this instance.|
|`ipoctet`|String|The IP octet of the network that is attached to this instance.|





## `ibm_pi_key`
{: #power-ssh-key}

Retrieve information about the SSH key that is used for your Power Systems Virtual Server instance. The SSH key is used to access the instance after it is created.
{: shortdesc}

### Sample Terraform code
{: #power-ssh-key-sample}

```
data "ibm_pi_key" "ds_instance" {
  pi_key_name          = "terraform-test-key"
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameters
{: #power-ssh-key-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The service instance associated with the account. |
| `pi_key_name` | String | Required | The name of the key.|


### Output parameters
{: #power-ssh-key-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `creation_date` | Timestamp | The timestamp when the SSH key was created. |
| `id` | String | The unique identifier of the SSH key. |
| `sshkey` | String | The public SSH key value. |





## `ibm_pi_network`
{: #power-network}

Retrieve information about the network that your Power Systems Virtual Server instance is connected to. 
{: shortdesc}

### Sample Terraform code
{: #power-network-sample}

The following example retrieves information about a network that is named `mynetwork`.

```
data "ibm_pi_network" "ds_network" {
  pi_network_name = "APP"
  pi_cloud_instance_id = "49fba6c9-23f8-40bc-9899-aca322ee7d5b"
}
```
{: codeblock}

### Input parameters
{: #power-network-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The service instance associated with the account. |
| `pi_network_name` | String | Required | The name of the network.|


### Output parameters
{: #power-network-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `available_ip_count` | Float | The total number of IP addresses that you have in your network. |
| `gateway` | String | The network gateway that is attached to your network. |
| `id` | String | The ID of the network. |
| `used_ip_count` | Float | The number of used IP addresses. |
| `used_ip_percent` | Float | The percentage of IP addresses used. |
| `vlan_id` | String | The VLAN ID that the network is connected to. |
| `type`|String|The type of network.|
|`cidr`|String|The CIDR of the network.|





## `ibm_pi_public_network`
{: #power-public-network}

Retrieve the details about a public network that is used for your Power Systems Virtual Server instance. 
{: shortdesc}

### Sample Terraform code
{: #power-public-network-sample}

```
data "ibm_pi_public_network" "ds_public_network" {
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameters
{: #power-public-network-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The service instance associated with the account. |

### Output parameters
{: #power-public-network-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `name` | String | The name of the network. |
| `id` | String | The ID of the network. |
| `type` | String | The type of VLAN that the network is connected to. |
| `vlan_id` | String | The ID of the VLAN that the network is connected to. |





## `ibm_pi_tenant`
{: #power-tenant}

Retrieve information about the tenants that are configured for your Power Systems Virtual Server instance. 
{: shortdesc}

### Sample Terraform code
{: #power-tenant-sample}

The following example retrieves all tenants for the Power Systems Virtual Server instance with the ID `11aaa1a1-11a1-11aa-1111-aaa111aa1a1a`. 

```
data "ibm_pi_tenant" "ds_tenant" {
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameters
{: #power-tenant-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The ID of the Power Systems Virtual Server instance for which you want to retrieve tenants. |

### Output parameters
{: #power-tenant-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `creation_date` | Timestamp | The timestamp when the tenant was created. |
| `enabled` | Boolean | If set to **true**, the tenant is enabled for the Power Systems Virtual Server instance ID. If set to **false**, the tenant is not enabled for the instance.|
| `id`|String| The ID of the tenant.|
| `tenantname` | String|  The name of the tenant. |
| `cloudinstances` | List of instances | A list with the regions and Power Systems Virtual Server instance IDs that the tenant owns. |
| `cloudinstances.cloud_instance_id`|String|The unique identifier of the cloud instance.|
| `cloudinstances.region`|String|The region of the cloud instance.|





## `ibm_pi_volume`
{: #power-volume}

Retrieves information about a persistent storage volume that is mounted to a Power Systems Virtual Server instance. 
{: shortdesc}

### Sample Terraform code
{: #power-volume-sample}

The following example retrieves information about the `volume_1` volume that is mounted to the Power Systems Virtual Server instance with the ID `11aaa1a1-11a1-11aa-1111-aaa111aa1a1a`. 

```
data "ibm_pi_volume" "ds_volume" {
  pi_volume_name       = "volume_1"
  pi_cloud_instance_id = "`11aaa1a1-11a1-11aa-1111-aaa111aa1a1a`"
}
```
{: codeblock}

### Input parameters
{: #power-volume-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The ID of the Power Systems Virtual Server instance for which you want to retrieve volume details. |
| `pi_volume_name` | String | Required | The name of the volume for which you want to retrieve detailed information. |

### Output parameters
{: #power-volume-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `bootable` | Boolean | If set to **true**, the Power Systems Virtual Server instance can boot from this volume. If set to **false**, this volume is not used during the boot process of the instance. |
| `id` | String | The unique identifier of the volume. |
| `size` | Integer | The size of the volume in gigabytes. |
| `state` | String | The state of the volume. |
| `type` | String | The disk type that is used for the volume. |
| `wwn` | String | The world wide name of the volume. |





## `ibm_pi_instance_volumes`
{: #power-instance-volumes}

Retrieves information about a persistent storage volume that is mounted to a Power Systems Virtual Server instance. 
{: shortdesc}

### Sample Terraform code
{: #power-instance-volumes-sample}

The following example retrieves information about the `volume_1` volume that is mounted to the Power Systems Virtual Server instance with the ID `11aaa1a1-11a1-11aa-1111-aaa111aa1a1a`. 

```
data "ibm_pi_instance_volumes" "ds_volumes" {
  pi_instance_name     = "volume_1"
  pi_cloud_instance_id = "11aaa1a1-11a1-11aa-1111-aaa111aa1a1a"
}
```
{: codeblock}

### Input parameters
{: #power-instance-volumes-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The ID of the Power Systems Virtual Server instance for which you want to retrieve volume details. |
| `pi_volume_name` | String | Required | The name of the volume for which you want to retrieve detailed information. |

### Output parameters
{: #power-instance-volumes-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `boot_volume_id` | String | The unique identifier of the boot volume.|
| `instance_volumes` | List of volumes | List of volumes attached to instance. |
| `instance_volumes.id` | String | The unique identifier of the volume. |
| `instance_volumes.name` | String | The name of the volume. |
| `instance_volumes.shareable` | Boolean | If set to **true**, the volume can be shared across multiple Power Systems Virtual Server instances. If set to **false**, the volume can be mounted to one instance only. |
| `instance_volumes.size` | Integer | The size of this volume in gigabytes. |
| `instance_volumes.state` | String | The state of the volume. |
| `instance_volumes.type` | String | The disk type that is used for this volume. |
|`instance_volumes.bootable`|Boolean|Indicates if the volume is bootable (**true**) or not (**false**). |
|`instance_volumes.href`|String|The hyper link of the volume. |

