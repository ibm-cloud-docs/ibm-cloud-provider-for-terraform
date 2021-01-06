---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-06"

keywords: terraform provider plugin, terraform power resources, terraform power systems resources, terraform power

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


# Power Systems resources
{: #power-vsi}

Review the [Power Systems resources](/docs/power-iaas?topic=power-iaas-about-virtual-server) that you can create. You can reference the output parameters for each resource in other resources or data sources by using [IBM Cloud Provider plug-in for Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

To find supported input parameter values, you can use the Power Systems CLI plug-in in {{site.data.keyword.cloud_notm}}. To install the plug-in, run `ibmcloud plugin install pi`. 
{: tip}

If you want to create, update, or delete Power System resources in a multizone-capable region, you must specify the `zone` in the `provider` block of your IBM Cloud Provider plug-in for Terraform configuration file. For more information, see the [`provider` block configuration](/docs/terraform?topic=terraform-provider-reference).
{: important}

## `ibm_pi_image`
{: #power-image}

Create, update, or delete for a Power Systems Virtual Server image. 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #power-image-sample}

```
resource "ibm_pi_image" "testacc_image  "{
  pi_image_name       = "7200-03-02"
  pi_image_id         = [ "image ID obtained from the datasource"]
  pi_cloud_instance_id = "<value of the cloud_instance_id>"
}
```

### Input parameters
{: #power-image-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`pi_image_name`|String|Required|The name of the image. |
|`pi_image_id`|String|Required|The ID of the image. | 
|`pi_cloud_instance_id`|String|Required|The cloud_instance_id for this account.|

### Output parameters
{: #power-image-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The unique identifier of the image.|
|`image_id`|String|The unique identifier of the image.|

### Timeouts
{: #power-image-timeout}

The following timeouts are defined for this resource: 

- **Create** The creation of the image is considered failed if no response is received for 60 minutes. 
- **Delete** The deletion of the image is considered failed if no response is received for 60 minutes. 


## `ibm_pi_instance`
{: #power-instance}

Create or update a [Power Systems Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #power-instance-sample}

The following example creates a Power Systems Virtual Server instance. 
{: shortdesc}

```
resource "ibm_pi_instance" "test-instance" {
    pi_memory             = "4"
    pi_processors         = "2"
    pi_instance_name      = "test-vm"
    pi_proc_type          = "shared"
    pi_image_id           = "${data.ibm_pi_image.powerimages.id}'
    pi_network_ids        = [data.ibm_pi_public_network.dsnetwork.id]
    pi_key_pair_name      = ibm_pi_key.key.key_id
    pi_sys_type           = "s922"
    pi_cloud_instance_id  = "11a1111a-aaaa-1aa1-a111-11aaa1aaa11"
    pi_pin_policy         = "none"
    pi_health_status      = "WARNING"
}
```

### Input parameters
{: #power-instance-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The cloud instance ID of your account. |
| `pi_image_id` | String | Required | The ID of the image that you want to use for your Power Systems Virtual Server instance. The image determines the operating system that is installed in your instance. To list available images, run the `ibmcloud pi images` command. |
| `pi_instance_name` | String | Required | The name of the Power Systems Virtual Server instance. | 
| `pi_key_pair_name` | String | Required| The name of the SSH key that you want to use to access your Power Systems Virtual Server instance. The SSH key must be uploaded to {{site.data.keyword.cloud_notm}}. |
| `pi_memory` | Float | Required | The amount of memory that you want to assign to your instance in gigabytes. |
| `pi_network_ids` | String | Required | The list of network IDs that you want to assign to the instance. | 
| `pi_pin_policy` | String | Optional | Select the pinning policy for your Power Systems Virtual Server instance. Supported values are `soft`, `hard`, and `none`. You can choose to soft pin (`soft`) or hard pin (`hard`) a virtual server to the physical host where it runs. When you soft pin an instance for high availability, the instance automatically migrates back to the original host once the host is back to its operating state. If the instance has a licensing restriction with the host, the hard pin option restricts the movement of the instance during remote restart, automated remote restart, DRO, and live partition migration. The default pinning policy is `none`.| 
| `pi_processors` | Float | Required | The number of vCPUs to assign to the VM (as visible within the guest operating system). | 
| `pi_proc_type` | String | Required | The type of processor mode in which the VM will run (shared/dedicated). |
| `pi_replicants` | Float | Optional | The number of instances that you want to provision with the same configuration. If this parameter is not set,  `1` is used by default. |
| `pi_replication_policy` | String | Optional | The replication policy that you want to use. If this parameter is not set, `none` is used by default. | 
| `pi_replication_scheme` | String | Optional | The replication scheme that you want to set (prefix/suffix). |
| `pi_sys_type` | String | Required | The type of system on which to create the VM (s922/e880/any). | 
| `pi_user_data` | String | Optional | The base64-encoded form of the user data (cloud-init) to pass to the instance during creation. | 
| `pi_virtual_cores_assigned` | Integer | Optional | Specify the number of virtual cores to be assigned. |
| `pi_volume_ids` | String | Required | The list of volume IDs that you want to attach to the instance during creation. |

### Output parameters
{: #power-instance-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `addresses` | Map of strings | A list of addresses that are assigned to the instance. |
| `addresses.ip`|String| The IP address of the instance.|
| `addresses.macaddress`|String|The MAC address of the instance.|
| `addresses.networkid`|String| The network ID of the instance.|
| `addresses.network_name`|String|The network name of the instance.|
| `addresses.type`|String|The type of network.|
| `addresses.externalip`|String|The external IP address of the instance.|
| `id`|String|The unique identifier of the instance. The ID is composed of `<power_instance_id>/<instance_id>`.|
| `instance_id` | String | The unique identifier of the instance. | 
| `pin_policy` |String|The pinning policy of the instance. |
| `progress` | Float | Specifies the overall progress of the instance deployment process in percentage. |
| `status` | String | The status of the instance. |
| `health_status`|String|The health status of the VM.|
| `migratable`|Boolean|Indicates the VM is migrated or not.|
| `max_processors`| Integer| The maximum number of processors that can be allocated to the instance with shutting down or rebooting the `LPAR`.|
| `max_virtual_cores` | Integer | The maximum number of virtual cores. |
| `min_processors` | Float | The minimum number of processors that the instance can have. | 
| `min_memory` |Integer| The minimum memory that was allocated to the instance.|
| `max_memory`|Integer|The maximum amount of memory that can be allocated to the instance without shut down or reboot the `LPAR`.|
| `min_virtual_cores` | Integer |The minimum number of virtual cores. |


### Timeouts
{: #power-instance-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **create** - The creation of the instance is considered failed if no response is received for 60 minutes. 
* **delete** - The deletion of the instance is considered failed if no response is received for 60 minutes. 

### Import
{: #power-instance-import}

The resource can be imported by using the ID that is composed of `<power_instance_id>/<instance_id>`.

```
terraform import ibm_pi_instance.example <power_instance_id>/<instance_id>
```
{: pre}

**Example**
```
terraform import ibm_pi_instance.example d7bec597-4726-451f-8453-e62e6f19c32c/cea6651a-bc0a-4438-9f8a-a0770456f3ebb
```






## `ibm_pi_key`
{: #ssh-key}

Create, update, or delete an SSH key for your Power Systems Virtual Server instance. The SSH key is used to access the instance after it is created.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #ssh-key-sample}

The following example creates an SSH key that is named `mykey`. 
{: shortdesc}

```
resource "ibm_pi_key" "testacc_sshkey" {
  pi_key_name          = "mykey"
  pi_ssh_key           = "ssh-rsa <value>"
  pi_cloud_instance_id = "<value of the cloud_instance_id>"
}
```

### Input parameters
{: #ssh-key-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The cloud instance ID for this account. | 
| `pi_key_name` | Integer | Required | The name of the SSH key that you uploaded to {{site.data.keyword.cloud_notm}}. 
| `pi_ssh_key` | String | Required | The value of the public SSH key. | 
| `pi_creation_date`|String|Optional|The date when the SSH key was created.|

### Output parameters
{: #ssh-key-output} 

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The unique identifier of the key. The ID is composed of `<power_instance_id>/<key_name>`.|
|`key_id`|String|The unique identifier of the key.|

### Timeouts
{: #ssh-key-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **create** - The creation of the SSH key is considered failed if no response is received for 60 minutes. 
* **delete** - The deletion of the SSH key is considered failed if no response is received for 60 minutes. 

### Import
{: #ssh-key-import}

The resource can be imported by using the ID that is composed of `<power_instance_id>/<key_name>`.

```
terraform import ibm_pi_key.example <power_instance_id>/<key_name>
```
{: pre}






## `ibm_pi_network`
{: #power-network}

Create, update, or delete a network connection for your Power Systems Virtual Server instance. 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #power-network-sample}

The following example creates a network connection for your Power Systems Virtual Server instance.
{: shortdesc}

```
resource "ibm_pi_network" "power_networks" {
  count                = 1
  pi_network_name      = "power-network"
  pi_cloud_instance_id = "<value of the cloud_instance_id>"
  pi_network_type      = "vlan"
  pi_cidr              = "<Network in CIDR notation (192.168.0.0/24)>"
  pi_dns               = [<"DNS Servers">]
}
```

### Input parameters 
{: #power-network-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The cloud instance ID for this account. |
| `pi_network_name` | String | Required | The name of the network. |
| `pi_network_type` | String | Required | The type of network that you want to create, such as `pub-vlan` or `vlan`. |
| `pi_dns`|List of strings|Optional|List of DNS entries for the network. Required for `vlan` network type.|
| `pi_cidr` | String | Optional | The network CIDR. Required for `vlan` network type. |

### Output parameters
{: #power-network-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id`|String|The unique identifier of the network. The ID is composed of `<power_instance_id>/<network_id>`.
| `networkid` | String | The unique identifier of the network. |
| `vlanid` | Integer | The ID of the VLAN that your network is attached to. | 

### Timeouts
{: #power-network-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **create**: The creation of the network is considered `failed` if no response is received for 60 minutes. 
- **delete**: The deletion of the network is considered `failed` if no response is received for 60 minutes. 

### Import
{: #power-network-import}

The resource can be imported by using the ID that is composed of `<power_instance_id>/<network_id>`.

```
terraform import ibm_pi_network.example <power_instance_id>/<network_id>
```
{: pre}






## `ibm_pi_network_port`
{: #pi-networkport}

Creates or updates network port in the Power Virtual Server Cloud. For more information, see [about Power Systems](/docs/power-iaas?topic=power-iaas-about-virtual-server).
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #pi-network-sample}

```
resource "ibm_pi_network_port" "test-network-port" {
    pi_network_name             = "Zone1-CFN"
    pi_cloud_instance_id  = "51e1879c-bcbe-4ee1-a008-49cdba0eaf60"
    pi_network_port_description         = "IP Reserved for Oracle RAC "
}
```

### Input parameters
{: #pi-network-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`pi_instance_name`|String|Required|The name of the VM. |
|`pi_cloud_instance_id`|String|Required|The cloud_instance_id of the account. | 
|`pi_network_port_description`|String|Optional|The description for the Network Port.|

### Output parameters
{: #pi-network-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The unique identifier of the instance. The ID is composed of <power_network_port_id>/<id>.|
|`ipaddress`|String|The unique identifier of the instance.|
|`macaddress`|String|The MAC address of the port.|
|`status`|String|The status of the port.|
|`portid`|String|The ID of the port.|
|`public_ip`|String| The public IP associated with the port. |

### Timeouts
{: #pi-network-timeout}

The following timeouts are defined for this resource:

- **Create** The creation of the network port is considered failed if no response is received for 60 minutes.
- **Delete** The deletion of the network port is considered failed if no response is received for 60 minutes.

### Import
{: #pi-network-import}

`ibm_pi_network_port` can be imported by using `power_instance_id` and `port_id`.

**Example**

```
terraform import ibm_pi_network_port.example d7bec597-4726-451f-8a63-e62e6f19c32c/cea6651a-bc0a-4438-9f8a-a0770bbf3ebb
```
## `ibm_pi_snapshot`
{: #pi-snapshot}

Creates, updates, deletes, and manages snapshots in the Power Virtual Server Cloud.
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #pi-snapshot-sample}

```
resource "ibm_pi_snapshot" "testacc_snapshot"{
  pi_instance_name       = test-instance
  pi_snapshot_name       = test-snapshot
  pi_volume_ids       = ["volumeid1","volumeid2"]
  description  = "Testing snapshot for instance"
  pi_cloud_instance_id = "<value of the cloud_instance_id>"
}
```

### Input parameters
{: #pi-snapshot-input}

Review the input parameters that you can specify for your resource.
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`pi_instance_name`|String|Required|The name of the instance you want to take a snapshot of. |
|`pi_snapshot_name`|String|Required|The unique name of the snapshot. |
|`description`|String|Optional|The description for the snapshot.|
|`pi_volume_ids`|String|Optional|The volume ID, if none provided then all volumes of the instance will be part of the snapshot.|
|`pi_cloud_instance_id`|String|Required|The cloud instance ID for this account.|


### Output parameters
{: #pi-snapshot-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The unique identifier of the snapshot. The ID is composed of <power_instance_id>/<pi_snap_shot_id>.|
|`volume_snapshots`|String|A map of the source and target volumes.|

### Timeouts
{: #pi-snapshot-timeout}

The following timeouts are defined for this resource:

- **Create** The creation of the snapshot is considered failed, if no response is received for 60 minutes.
- **Delete** The deletion of the snapshot is considered failed, if no response is received for 60 minutes.
- **Update** The update of the snapshot is considered failed, if no response is received for 60 minutes.

### Import
{: #pi-snapshot-import}

`ibm_pi_snapshot` can be imported by using `power_instance_id` and `pi_snap_shot_id`.

**Example**

```
terraform import ibm_pi_snapshot.example d7bec597-4726-451f-8a63-e62e6f19c32c/cea6651a-bc0a-4438-9f8a-a0770bbf3ebb
```

## `ibm_pi_volume`
{: #power-volume}

Create, update, or delete a volume to attach it to a Power Systems Virtual Server instance. 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #power-volume-sample}

The following example creates a 20 GB volume. 
{: shortdesc}

```
resource "ibm_pi_volume" "testacc_volume"{
  pi_volume_size       = 20
  pi_volume_name       = test-volume
  pi_volume_type       = ssd
  pi_volume_shareable  = true
  pi_cloud_instance_id = "<value of the cloud_instance_id>"
}
```

### Input parameters 
{: #power-volume-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `pi_cloud_instance_id` | String | Required | The cloud instance ID for this account. |
| `pi_volume_name` | String | Required |  The name of the volume. |
| `pi_volume_shareable` | Boolean | Required | If set to **true**, the volume can be shared across Power Systems Virtual Server instances. If set to **false**, you can attach it only to one instance. | 
| `pi_volume_size` | Integer | Required | The size of the volume in gigabytes. | 
| `pi_volume_type` | String | Required | The type of volume that you want to create. Supported values are `ssd`, `standard`, `tier1`, and `tier3`. |

### Output parameters
{: #power-volume-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the volume. The ID is composed of `<power_instance_id>/<volume_id>`.| 
| `status` | String | The status of the volume. | 
| `volume_id`|String|The unique identifier of the volume. |
| `wwn` | String | The world wide name of the volume. |

### Timeouts
{: #power-volume-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **create**: The creation of the volume is considered `failed` if no response is received for 60 minutes. 
- **delete**: The deletion of the volume is considered `failed` if no response is received for 60 minutes. 

### Import
{: #power-volume-import}

The resource can be imported by using the ID that is composed of `<power_instance_id>/<volume_id>`.

```
terraform import ibm_pi_volume.example <power_instance_id>/<volume_id>
```
{: pre}
