---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-18" 

keywords: terraform provider plugin, terraform gen 2 resources, terraform generation 2, terraform generation 2 compute

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



# VPC infrastructure resources
{: #vpc-gen2-resources}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_is_flow_log`
{: #ibm_is_flow_log}

Create, update, delete and suspend the flow log resource.
{: shortdesc}

### Sample Terraform code
{: #ibm_is_flow-sample}

```
resource "ibm_is_instance" "testacc_instance" {
  name    = "testinstance"
  image   = "7eb4e35b-4257-56f8-d7da-326d85452591"
  profile = "b-2x8"

  primary_network_interface {
    port_speed = "1000"
    subnet     = "70be8eae-134c-436e-a86e-04849f84cb34"
  }

  vpc  = "01eda778-b822-43a2-816d-d30713df5e13"
  zone = "us-south-1"
  keys = ["eac87f33-0c00-4da7-aa66-dc2d972148bd"]
}


data "ibm_resource_group" "instance_group" {
  name = var.resource_group
}

resource "ibm_resource_instance" "instance1" {
  name              = "cos-instance"
  resource_group_id = data.ibm_resource_group.instance_group.id
  service           = "cloud-object-storage"
  plan              = "standard"
  location          = "global"
}

resource "ibm_cos_bucket" "bucket1" {
   bucket_name          = "us-south-bucket-vpc1"
   resource_instance_id = ibm_resource_instance.instance1.id
   region_location = var.region
   storage_class = "standard"
}

resource ibm_is_flow_log test_flowlog {
  depends_on = [ibm_cos_bucket.bucket1]
  name = "test-instance-flow-log"
  target = ibm_is_instance.testacc_instance.id
  active = true
  storage_bucket = ibm_cos_bucket.bucket1.bucket_name
}
```
{: codeblock}

### Input parameters
{: #ibm_is_flow-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}


| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `name` | String | Required | The unique user-defined name for the flow log collector.| No |
| `target` | String | Required | The ID of the target to collect flow logs. If the target is an instance, subnet, or VPC, flow logs is not collected for any network interfaces within the target that are more specific flow log collector. | Yes |
| `storage_bucket` | String | Required | The name of the {{site.data.keyword.cos_full_notm}} bucket where the collected flows will be logged. The bucket must exist and an IAM service authorization must grant {{site.data.keyword.cloud_notm}} flow logs resources of VPC infrastructure services writer access to the bucket. | Yes |
| `active` | String | Optional | Indicates whether the collector is active. If `false`, this collector is created in inactive mode. Default value is true. | No |
| `resource_group` | String | Optional | The resource group ID where the flow log is created. | Yes |
| `tags` | Array of Strings | Optional | The tags associated with the flow log. | No |

### Output parameters
{: #ibm-is-flow-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `created_at`| String| The date and time that the flow log collector created. |
| `crn` | String | The CRN of the flow log collector. |
| `href` | String | The URL of the flow log collector. |
| `id` | String | The unique identifier of the flow log collector. |
| `lifecycle_state` | String | The lifecycle state of the flow log collector. |
| `name`| String | The user-defined name of the flow log collector. |
| `vpc` | String | The VPC of the flow log collector that is associated. |

### Import
{: #ibm-is-flow-import}

`ibm_is_flow_log` can be imported by using VPC flow log ID.

**Example**

```
terraform import ibm_is_flow_log.example d7bec597-4726-451f-8a53-e62e6f19c32c
```

## `ibm_is_floating_ip`
{: #provider-floating-ip}

Create a floating IP address that you can associate with a {{site.data.keyword.vsi_is_short}} instance. You can use the floating IP address to access your instance from the public network, independent of whether the subnet is attached to a public gateway. For more information, see [About floatig IP](/docs/vpc?topic=vpc-creating-a-vpc-using-the-rest-apis#create-floating-ip-api-tutorial).
{: shortdesc}

 ### Sample Terraform code
{: #floating-ip-sample}

The following example shows how to create a {{site.data.keyword.vsi_is_short}} instance and associate a floating IP address to the primary network interface of the virtual server instance. 

```
resource "ibm_is_instance" "testacc_instance" {
  name    = "testinstance"
  image   = "7eb4e35b-4257-56f8-d7da-326d85452591"
  profile = "bx2-2x8"

  primary_network_interface {
    port_speed = "1000"
    subnet     = "70be8eae-134c-436e-a86e-04849f84cb34"
  }

  vpc  = "01eda778-b822-43a2-816d-d30713df5e13"
  zone = "us-south-1"
  keys = ["eac87f33-0c00-4da7-aa66-dc2d972148bd"]
}

resource "ibm_is_floating_ip" "testacc_floatingip" {
  name   = "testfip1"
  target = ibm_is_instance.testacc_instance.primary_network_interface.0.id
}
```
{: codeblock}

### Input parameters
{: #floating-ip-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `name` | String | Required | Enter a name for the floating IP address. | 
| `target` | String | Optional | Enter the ID of the network interface that you want to use to allocate the IP address. If you specify this option, do not specify `zone` at the same time. | 
| `zone` | String | Optional | Enter the name of the zone where you want to create the floating IP address. To list available zones, run `ibmcloud is zones`. If you specify this option, do not specify `target` at the same time. | 
| `resource_group`|String|Optional| The resource group ID where you want to create the floating IP.|
| `tags`|Array of strings|Optional|Enter any tags that you want to associate with your VPC. Tags might help you find your VPC more easily after it is created. Separate multiple tags with a comma (`,`). |

### Output parameters
{: #floating-ip-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `address` | String | The floating IP address that was created. | 
| `id` | String | The unique identifier of the floating IP address. | 
| `status` | String | The provisioning status of the floating IP address. |

### Timeouts
{: #floating-ip-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **create**: The creation of the floating IP address is considered `failed` if no response is received for 10 minutes. 
- **delete**: The deletion of the floating IP address is considered `failed` if no response is received for 10 minutes. 

### Import
{: #floating-ip-import}

The `ibm_is_floating_ip` can be imported by using floating IP ID.

**Example**
```
terraform import ibm_is_floating_ip.example d7bec597-4726-451f-8a63-e62e6f19c32c
```
{: pre}


## `ibm_is_ike_policy`
{: #provider-ike-policy}

Create, update, or cancel an Internet Key Exchange (IKE) policy. 
{: shortdesc}

IKE is an IPSec (Internet Protocol Security) standard protocol that is used to ensure secure communication over the VPC VPN service. For more information, see [Using VPC with your VPC](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-vpn-with-your-vpc). 

### Sample Terraform code
{: #ike-sample}

```
resource "ibm_is_ike_policy" "example" {
    name = "test"
    authentication_algorithm = "md5"
    encryption_algorithm = "triple_des"
    dh_group = 2
    ike_version = 1
}
```
{: codeblock}

### Input parameters
{: #ike-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}


| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `authentication_algorithm` | String | Required | Enter the algorithm that you want to use to authenticate `IPSec` peers. Available options are `md5`, `sha1`, or `sha256`. | No |
| `dh_group` | Integer | Required | Enter the Diffie-Hellman group that you want to use for the encryption key. Available options are `2`, `5`, or `14`. | No |
| `encryption_algorithm` | String | Required | Enter the algorithm that you want to use to encrypt data. Available options are: `triple_des`, `aes128`, or `aes256`. | No |
| `ike_version` | Integer | Optional | Enter the IKE protocol version that you want to use. Available options are `1`, or `2`. | No |
| `key_lifetime` | Integer | Optional | Enter the time in seconds that your encryption key can be used before it expires. You must enter a number between 300 and 86400. If you do not specify this option, 28800 seconds is used. | No | 
| `name` | String | Required | Enter a name for your IKE policy. |  No |
| `resource_group` | String | Optional | Enter the ID of the resource group where you want to create the IKE policy. To list available resource groups, run `ibmcloud resource groups`. If you do not specify a resource group, the IKE policy is created in the `default` resource group. | Yes |

### Output parameters
{: #ike-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `href`| String| The canonical URL that was assigned to your IKE policy. | 
| `id` | String | The unique identifier of the IKE policy that you created. |
| `negotiation_mode` | String | The negotiation mode that was set for your IKE policy. Only `main` is supported. | 
| `vpn_connections`| List | A collection of VPN connections that use the IKE policy. Every connection is listed with a VPC connection `name`, `id`, and `canonical URL`. |

### Import
{: #provider-ike-policy-import}

The `ibm_is_ike_policy` can be imported by using IKE Policy ID.

**Example**
```
terraform import ibm_is_ike_policy.example d7bec597-4726-451f-8a63-e62e6f19c32c
```
{: pre}

## `ibm_is_instance`
{: #provider-instance}

Create, update, or delete a {{site.data.keyword.vsi_is_short}} instance. 
{: shortdesc}

### Sample Terraform code
{: #instance-sample}

#### Example for creating an instance in a VPC

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
  public_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCKVmnMOlHKcZK8tpt3MP1lqOLAcqcJzhsvJcjscgVERRN7/9484SOBJ3HSKxxNG5JN8owAjy5f9yYwcUg+JaUVuytn5Pv3aeYROHGGg+5G346xaq3DAwX6Y5ykr2fvjObgncQBnuU5KHWCECO/4h8uWuwh/kfniXPVjFToc+gnkqA+3RKpAecZhFXwfalQ9mMuYGFxn+fwn8cYEApsJbsEmb0iJwPiZ5hjFC8wREuiTlhPHDgkBLOiycd20op2nXzDbHfCHInquEe/gYxEitALONxm0swBOwJZwlTDOB7C6y2dzlrtxr1L59m7pCkWI4EtTRLvleehBoj3u7jB4usR"
}

resource "ibm_is_instance" "testacc_instance" {
  name    = "testinstance"
  image   = "7eb4e35b-4257-56f8-d7da-326d85452591"
  profile = "bx2-2x8"

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

 //User can configure timeouts
  timeouts {
    create = "15m"
    update = "15m"
    delete = "15m"
  }
}
```
{: codeblock}

#### Example for creating an instance with custom security group rules
{: #custom-sec-group-rules}

The following example shows how you can create a virtual server instance with custom security group rules. Note that the security group, security group rules, and the virtual server instance must be created in a specific order to meet the dependencies of the individual resources. To force the creation in a specific order, you use the [`depends_on` parameter](https://www.terraform.io/docs/configuration/resources.html){: external}. If you do not provide this parameter, all resources are created at the same time which might lead to resource dependency errors during the provisioning of your virtual server, such as `The security group to attach to is not available`.

```
resource "ibm_is_vpc" "testacc_vpc" {
    name = "test"
}

resource "ibm_is_security_group" "testacc_security_group" {
    name = "test"
    vpc = ibm_is_vpc.testacc_vpc.id
}

resource "ibm_is_security_group_rule" "testacc_security_group_rule_all" {
    group = ibm_is_security_group.testacc_security_group.id
    direction = "inbound"
    remote = "127.0.0.1"
    depends_on = [ibm_is_security_group.testacc_security_group]
 }

 resource "ibm_is_security_group_rule" "testacc_security_group_rule_icmp" {
    group = ibm_is_security_group.testacc_security_group.id
    direction = "inbound"
    remote = "127.0.0.1"
    icmp {
        code = 20
        type = 30
    }
    depends_on = [ibm_is_security_group_rule.testacc_security_group_rule_all]

 }

 resource "ibm_is_security_group_rule" "testacc_security_group_rule_udp" {
    group = ibm_is_security_group.testacc_security_group.id
    direction = "inbound"
    remote = "127.0.0.1"
    udp {
        port_min = 805
        port_max = 807
    }
    depends_on = [ibm_is_security_group_rule.testacc_security_group_rule_icmp]
 }

 resource "ibm_is_security_group_rule" "testacc_security_group_rule_tcp" {
    group = ibm_is_security_group.testacc_security_group.id
    direction = "outbound"
    remote = "127.0.0.1"
    tcp {
        port_min = 8080
        port_max = 8080
    }
    depends_on = [ibm_is_security_group_rule.testacc_security_group_rule_udp]
 }

resource "ibm_is_instance" "testacc_instance" {
  name    = "testinstance"
  image   = "7eb4e35b-4257-56f8-d7da-326d85452591"
  profile = "b-2x8"

  primary_network_interface {
    subnet = ibm_is_subnet.testacc_subnet.id
    security_groups = [ibm_is_security_group.testacc_security_group.id]
  }

  vpc  = ibm_is_vpc.testacc_vpc.id
  zone = "us-south-1"
  keys = [ibm_is_ssh_key.testacc_sshkey.id]
  depends_on = [ibm_is_security_group_rule.testacc_security_group_rule_tcp]

  //User can configure timeouts
  timeouts {
    create = "15m"
    update = "15m"
    delete = "15m"
  }
}
```
{: codeblock}

### Input parameters
{: #instance-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
|`auto_delete_volume`|Bool|Optional|If set to `true`, automatically deletes the volumes that are attached to an instance. **Note** Setting this argument can bring some inconsistency in the volume resource, as the volumes is destroyed along with instances.|No|
|`boot_volume`|List|Optional|A list of boot volumes for an instance.| No |
|`boot_volume.name`|String|Optional|The name of the boot volume.| No |
|`boot_volume.encryption`|String|Optional|The type of encryption to use for the boot volume.| No |
|`force_recovery_time`|Integer|Optional|Define timeout (in minutes), to force the is_instance to recover from a perpetual "starting" state, during provisioning. And to force the is_instance to recover from a perpetual "stopping" state, during removal of user access. **Note** The force_recovery_time is used to retry multiple times until timeout.|No|
|`image`|String|Required|The ID of the virtual server image that you want to use. To list supported images, run `ibmcloud is images`.| No |
|`keys`|List|Required|A comma-separated list of SSH keys that you want to add to your instance.| No |
|`name`|String|Optional|The instance name.| No |
|`network_interfaces`|List|Optional|A list of more network interfaces that are set up for the instance.| Yes |
|`network_interfaces.name`|String|Optional|The name of the network interface.| No |
|`network_interface. primary_ipv4_address`|String|Optional|The IPV4 address of the interface.| Yes |
|`network_interfaces.subnet`|String|Required|The ID of the subnet.| No |
|`network_interfaces. security_groups`|List of strings|Optional|A comma separated list of security groups to add to the primary network interface.| No |
|`network_interfaces. allow_ip_spoofing`|Bool|Optional|Indicates whether IP spoofing is allowed on the interface. If `false`, IP spoofing is prevented on the interface. If `true`, IP spoofing is allowed on the interface.| No |
|`primary_network_interface`|List|Required|A nested block describes the primary network interface of this instance. Only one primary network interface can be specified for an instance.| No |
|`primary_network_interface. name`|String|Optional|The name of the network interface.| No |
|`primary_network_interface. primary_ipv4_address`|String|Optional|The IPV4 address of the interface.| Yes |
|`primary_network_interface. subnet`|String|Required|The ID of the subnet.| No |
|`primary_network_interface. security_groups`|List of strings|Optional|A comma separated list of security groups to add to the primary network interface.| No |
|`primary_network_interface. allow_ip_spoofing`|Bool|Optional|Indicates whether IP spoofing is allowed on the interface. If `false`, IP spoofing is prevented on the interface. If `true`, IP spoofing is allowed on the interface.| No |
|`profile`|String|Required|The name of the profile that you want to use for your instance. To list supported profiles, run `ibmcloud is instance-profiles`.| Yes |
|`resource_group`|String|Optional|The ID of the resource group where you want to create the instance.| Yes |
|`tags`|Array of strings|Optional|A list of tags that you want to add to your instance. Tags can help you find your instance more easily later.| No |
|`user_data`|String|Optional|User data to transfer to the instance.| No |
|`volumes`|List|Optional|A comma separated list of volume IDs to attach to the instance.| No |
|`vpc`|String|Required|The ID of the VPC where you want to create the instance.| Yes |
|`zone`|String|Required|The name of the VPC zone where you want to create the instance.| Yes |


### Output parameters
{: #instance-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the instance.|
|`memory`|Integer|The amount of memory that is allocated to the instance in gigabytes.|
|`status`|String|The status of the instance.|
|`vcpu`|List of virtual CPUs|A list of virtual CPUs that are allocated to the instance.|
|`vcpu.architecture`|String|The architecture of the CPU.|
|`vcpu.count`|Integer|The number of virtual CPUS that are assigned to the instance.|
|`gpu`|List of GPUs|A list of GPUs that are assigned to the instance.|
|`gpu.cores`|Integer|The number of cores of the GPU.|
|`gpu.count`|Integer|The count of the GPU.|
|`gpu.manufacture`|String|The manufacturer of the GPU.|
|`gpu.memory`|Integer|The amount of memory of the GPU in gigabytes.|
|`gpu.model`|String|The model of the GPU.|
|`primary_network_interface`|List of primary network interfaces|A list of primary network interfaces that are attached to the instance.|
|`primary_network_interface.id`|String|The ID of the primary network interface.|
|`primary_network_interface.name`|String|The name of the primary network interface.|
|`primary_network_interface.subnet`|String|The ID of the subnet that the primary network interface is attached to.
|`primary_network_interface.security_groups`|List of strings|A list of security groups that are used in the primary network interface.|
|`primary_network_interface.primary_ipv4_address`|String|The primary IPv4 address.|
|`primary_network_interface.allow_ip_spoofing`|String|Indicates whether IP spoofing is allowed on the interface.|
|`network_interfaces`|List of more network interfaces|A list of more network interfaces that are attached to the instance.|
|`network_interfaces.id`|String|The ID of the network interface.|
|`network_interfaces.name`|String|The name of the network interface.|
|`network_interfaces.subnet`|String|The ID of the subnet.|
|`network_interfaces.security_groups`|List of strings|A list of security groups that are used in the network interface.|
|`network_interfaces.primary_ipv4_address`|String|The primary IPv4 address.|
|`network_interface.allow_ip_spoofing`|String|Indicates whether IP spoofing is allowed on the interface.|
|`boot_volume`|List of boot volumes|A list of boot volumes that the instance uses.|
|`boot_volume.name`|String|The name of the boot volume.|
|`boot_volume.size`|Integer|The capacity of the volume in gigabytes.|
|`boot_volume.iops`|Integer|The number of input and output operations per second of the volume.|
|`boot_volume.profile`|String|The profile of the volume.|
|`boot_volume.encryption`|String|The type of encryption that is used for the boot volume.|
|`volume_attachments`|List of volume attachments|A list of volume attachments for the instance.|
|`volume_attachments.id`|String|The ID of the volume attachment.|
|`volume_attachments.name`|String|The name of the volume attachment.|
|`volume_attachments.volume_id`|String|The ID of the volume that is used in the volume attachment.|
|`volume_attachments.volume_name`|String|The name of the volume that is used in the volume attachment.|
|`volume_attachments.volume_crn`|String|The CRN of the volume that is used in the volume attachment.|

### Timeout
{: #instance-timeout}

The following timeouts are defined for the instance:

- **create**: The creation of the instance is considered failed when no response is received for 30 minutes.
- **update**: The update of the instance or the attachment of a volume to an instance is considered failed when no response is received for 30 minutes.
- **delete**: The deletion of the instance is considered failed when no response is received for 30 minutes.

### Import
{: #instance-import}

`ibm_is_instance` can be imported by using the instance ID

```
terraform import ibm_is_instance.example a1aaa111-1111-111a-1a11-a11a1a11a11a
```
{: pre}


## `ibm_is_instance_group`
{: #vpc-is-instance-grp}

Create, update, or delete an instance group on VPC.
{: shortdesc}

### Sample Terraform code
{: #vpc-is-instance-sample}

The following example creates an instance in a VPC generation 2 infrastructure

```
provider "ibm" {
  generation = 2
}

resource "ibm_is_vpc" "vpc2" {
  name = "vpc2test"
}

resource "ibm_is_subnet" "subnet2" {
  name            = "subnet2"
  vpc             = ibm_is_vpc.vpc2.id
  zone            = "us-south-2"
  ipv4_cidr_block = "10.240.64.0/28"
}

resource "ibm_is_ssh_key" "sshkey" {
  name       = "ssh1"
  public_key = "SSH KEY"
}

resource "ibm_is_instance_template" "instancetemplate1" {
  name    = "testtemplate"
  image   = "r006-14140f94-fcc4-11e9-96e7-a72723715315"
  profile = "bx2-8x32"

  primary_network_interface {
    subnet = ibm_is_subnet.subnet2.id
  }

  vpc  = ibm_is_vpc.vpc2.id
  zone = "us-south-2"
  keys = [ibm_is_ssh_key.sshkey.id]
}

resource "ibm_is_instance_group" "instance_group" {
  name              = "testgroup"
  instance_template = ibm_is_instance_template.instancetemplate1.id
  instance_count    = 2
  subnets           = [ibm_is_subnet.subnet2.id]

  //User can configure timeouts
  timeouts {
    create = "15m"
    delete = "15m"
    update = "10m"
  }
}
```
{: codeblock}


### Input parameters
{: #vpc-is-instance-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
|`name`|String|Required|The instance  group name.| No |
|`instance_template`|String|Required| The ID of the instance template to create the instance group.| Yes |
|`instance_count`|Integer|Optional|The number of instances to create in the instance group.| No |
|`resource_group`|String|Optional|The resource group ID.| No |
|`subnets`|List|Required|The list of subnet IDs used by the instances. | No |
|`application_port`|Integer|Optional|The instance group uses when scaling up instances to supply the port for the Load Balancer pool member. | No |
|`load_balancer`|String|Optional|The load Balancer ID.| No |
|`load_balancer_pool`|String|Optional|The load Balancer pool ID.| No |

### Output parameters
{: #instance-group-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of an instance group.|
|`managers`|String|List of managers associated with the instance group.|
|`vpc`|String|The VPC ID.|
|`status`|String|Status of an instance group.|

### Import
{: #instance-group-import}

`ibm_is_instance_group` can be imported by using the instance group ID.

```
terraform import ibm_is_instance_group.instance_group r006-14140f94-fcc4-11e9-96e7-a72723715315
```
{: pre}

### Timeouts
{: #is-instance-group-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **create**: The creation of the instance group is considered `failed` if no response is received for 15 minutes.
- **delete**: The deletion of the instance group is considered `failed` if no response is received for 15 minutes.
- **update**: The creation of the instance group is considered `failed` if no response is received for 10 minutes. 

## `ibm_is_instance_group_manager`
{: #vpc-is-instance-grp-manager}

Create, update, or delete an instance group manager on VPC of an instance group.
{: shortdesc}

### Sample Terraform code
{: #vpc-is-instance-grpmanager-sample}

The following example creates an instance group manager.

```
provider "ibm" {
  generation = 2
}

resource "ibm_is_vpc" "vpc2" {
  name = "vpc2test"
}

resource "ibm_is_subnet" "subnet2" {
  name            = "subnet2"
  vpc             = ibm_is_vpc.vpc2.id
  zone            = "us-south-2"
  ipv4_cidr_block = "10.240.64.0/28"
}

resource "ibm_is_ssh_key" "sshkey" {
  name       = "ssh1"
  public_key = "SSH_KEY"
}

resource "ibm_is_instance_template" "instancetemplate1" {
  name    = "testtemplate"
  image   = "r006-14140f94-fcc4-11e9-96e7-a72723715315"
  profile = "bx2-8x32"

  primary_network_interface {
    subnet = ibm_is_subnet.subnet2.id
  }

  vpc  = ibm_is_vpc.vpc2.id
  zone = "us-south-2"
  keys = [ibm_is_ssh_key.sshkey.id]
}

resource "ibm_is_instance_group" "instance_group" {
  name              = "testgroup"
  instance_template = ibm_is_instance_template.instancetemplate1.id
  instance_count    = 2
  subnets           = [ibm_is_subnet.subnet2.id]

  //User can configure timeouts
  timeouts {
    create = "15m"
    delete = "15m"
	update = "10m"
  }
}

resource "ibm_is_instance_group_manager" "instance_group_manager" {
  name                 = "testmanager"
  aggregation_window   = 120
  instance_group       = ibm_is_instance_group.instance_group.id
  cooldown             = 300
  manager_type         = "autoscale"
  enable_manager       = true
  max_membership_count = 2
  min_membership_count = 1
}
```
{: codeblock}


### Input parameters
{: #vpc-is-instance-grpmanager-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`name`|String|Optional|The name of the instance group manager.|
|`enable_manager`|Boolean|Optional| Enable or disable the instance group manager. Default value is `true`. |
|`instance_group`|String|Required|The instance group ID where instance group manager is created. |
|`manager_type`|String|Optional|The type of instance group manager. Default value is `autoscale`. |
|`aggregation_window`|Integer|Optional|The time window in seconds to aggregate metrics prior to evaluation. |
|`cooldown`|Integer|Optional|The duration of time in seconds to pause further scale actions after scaling has taken place. |
|`max_membership_count`|Integer|Required|The maximum number of members in a managed instance group. |
|`min_membership_count`|Integer|Optional|The minimum number of members in a managed instance group. Default value is `1`.|

### Output parameters
{: #instance-group-manager-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID in the combination of instance group ID and instance group manager ID.|
|`policies`|String|List of policies associated with the instance group manager.|
|`manager_id`|String|The ID of the instance group manager.|

### Import
{: #instance-group-manager-import}

`ibm_is_instance_group_manager` can be imported by using the instance group ID and instance group manager ID.

```
terraform import ibm_is_instance_group_manager.manager r006-eea6b0b7-babd-47a8-82c5-ad73d1e10bef/r006-160b9a68-58c8-4ec3-84b0-ad553ccb1e5a
```
{: pre}

## `ibm_is_instance_group_manager_policy`
{: #vpc-is-instance-grp-manager-policy}

Create, update, or delete a policy of an instance group manager.
{: shortdesc}

### Sample Terraform code
{: #vpc-is-instance-grpmanager-policy-sample}

The following example creates a policy for an instance group manager.

```
provider "ibm" {
  generation = 2
}

resource "ibm_is_vpc" "vpc2" {
  name = "vpc2test"
}

resource "ibm_is_subnet" "subnet2" {
  name            = "subnet2"
  vpc             = ibm_is_vpc.vpc2.id
  zone            = "us-south-2"
  ipv4_cidr_block = "10.240.64.0/28"
}

resource "ibm_is_ssh_key" "sshkey" {
  name       = "ssh1"
  public_key = "SSH_KEY"
}

resource "ibm_is_instance_template" "instancetemplate1" {
  name    = "testtemplate"
  image   = "r006-14140f94-fcc4-11e9-96e7-a72723715315"
  profile = "bx2-8x32"

  primary_network_interface {
    subnet = ibm_is_subnet.subnet2.id
  }

  vpc  = ibm_is_vpc.vpc2.id
  zone = "us-south-2"
  keys = [ibm_is_ssh_key.sshkey.id]
}

resource "ibm_is_instance_group" "instance_group" {
  name              = "testgroup"
  instance_template = ibm_is_instance_template.instancetemplate1.id
  instance_count    = 2
  subnets           = [ibm_is_subnet.subnet2.id]

  //User can configure timeouts
  timeouts {
    create = "15m"
    delete = "15m"
    update = "10m"
  }
}

resource "ibm_is_instance_group_manager" "instance_group_manager" {
  name                 = "testmanager"
  aggregation_window   = 120
  instance_group       = ibm_is_instance_group.instance_group.id
  cooldown             = 300
  manager_type         = "autoscale"
  enable_manager       = true
  max_membership_count = 2
  min_membership_count = 1
}

resource "ibm_is_instance_group_manager_policy" "cpuPolicy" {
  instance_group         = ibm_is_instance_group.instance_group.id
  instance_group_manager = ibm_is_instance_group_manager.instance_group_manager.manager_id
  metric_type            = "cpu"
  metric_value           = 70
  policy_type            = "target"
  name                   = "testpolicy"
}
```
{: codeblock}


### Input parameters
{: #vpc-is-instance-grpmanager-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`name`|String|Optional|The name of the policy.|
|`policy_type`|String|Required| The type of metric to evaluate. |
|`instance_group`|String|Required|The instance group ID. |
|`instance_group_manager`|String|Required|The instance group manager ID for policy creation. |
|`metric_type`|String|Required|The type of metric to evaluate. The possible values for metric types are `cpu`, `memory`, `network_in`, and `network_out`. |
|`metric_value`|Integer|Required|The metric value to evaluate. |

### Output parameters
{: #instance-group-manager-policy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID in the combination of instance group ID, instance group manager ID, and instance group manager policy ID.|
|`policy_id`|String|The policy ID. |

### Import
{: #instance-group-manager-policy-import}

`ibm_is_instance_group_manager_policy` can be imported by using instance group ID, instance group manager ID and instance group manager policy ID.

```
terraform import ibm_is_instance_group_manager_policy.policy r006-eea6b0b7-babd-47a8-82c5-ad73d1e10bef/r006-160b9a68-58c8-4ec3-84b0-ad553ccb1e5a/r006-94d99d1d-be65-4939-9006-1a1a767245b5
```
{: pre}


## `ibm_is_instance_template`
{: #vpc-is-instance-template}

Create, update, or delete an instance template on VPC.
{: shortdesc}

### Sample Terraform code
{: #vpc-is-instance-template-sample}

The following example creates an instance template in a VPC generation-2 infrastructure

```
provider "ibm" {
  generation = 2
}

resource "ibm_is_vpc" "vpc2" {
  name = "vpc2test"
}

resource "ibm_is_subnet" "subnet2" {
  name            = "subnet2"
  vpc             = ibm_is_vpc.vpc2.id
  zone            = "us-south-2"
  ipv4_cidr_block = "10.240.64.0/28"
}

resource "ibm_is_ssh_key" "sshkey" {
  name       = "ssh1"
  public_key = "SSH KEY"
}

resource "ibm_is_instance_template" "instancetemplate1" {
  name    = "testtemplate"
  image   = "r006-14140f94-fcc4-11e9-96e7-a72723715315"
  profile = "bx2-8x32"

  primary_network_interface {
    subnet = ibm_is_subnet.subnet2.id
  }

  vpc  = ibm_is_vpc.vpc2.id
  zone = "us-south-2"
  keys = [ibm_is_ssh_key.sshkey.id]

  boot_volume {
    name                             = "testbootvol"
    size                             = 16
    profile                          = "custom"
    delete_volume_on_instance_delete = true
  }
}
```
{: codeblock}

### Input parameters
{: #vpc-is-instance-template-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------ |
|`templates.id`|String|Required|The ID of the instance template. | No |
|`name`|String|Required|The name of the instance template. | No |
|`image`|String|Required|The ID of the image to create the template.| No |
|`profile`|String|Required|The number of instances created in the instance group. | No |
|`vpc`|String|Required|The VPC ID that the instance templates needs to be created.| No |
|`zone`|String|Required|The name of the zone. | No |
|`keys`|List|Required|List of SSH key IDs used to allow log in user to the instances. | No |
|`resource_group`|String|Optional|The resource group ID. | Yes |
|`primary_network_interfaces`|List| Required |A nested block describes the primary network interface for the template. | No |
|`primary_network_interfaces.subnet`|String|Required |The VPC subnet to assign to the interface. | Yes |
|`primary_network_interfaces.name`|String|Optional|The name of the interface. | No |
|`primary_network_interfaces.security_groups`|List | Optional|List of security groups of the subnet. | No |
|`primary_network_interfaces.primary_ipv4_address`|String|Optional|The IPv4 address assigned to the primary network interface. | No |
|`network_interfaces`|List|Optional|A nested block describes the network interfaces for the template. | No |
|`network_interfaces.subnet`|String|Required|The VPC subnet to assign to the interface. | Yes |
|`network_interfaces.name`|String| Optional |The name of the interface. | No |
|`network_interfaces.security_groups`|List|Optional|List of security groups of  the subnet. | No |
|`network_interfaces.primary_ipv4_address`|String|Optional|The IPv4 address assigned to the network interface. | No |
|`boot_volume`|List|Optional|A nested block describes the boot volume configuration for the template. | No |
|`boot_volume.encryption`|String|Optional|The encryption key CRN to encrypt the boot volume attached. | No |
|`boot_volume.name`|String|Optional|The name of the boot volume. | No |
|`boot_volume.size`|String|Optional|The boot volume size to configure in giga bytes. | No |
|`boot_volume.iops`|String|Optional|The IOPS for the boot volume. | No |
|`boot_volume.profile`|String|Optional|The profile for the boot volume configuration. | No |
|`boot_volume.delete_volume_on_instance_delete`|Boolean|Optional|You can configure to delete the boot volume based on instance deletion. | No |
|`volume_attachments`|List|Optional|A nested block describes the storage volume configuration for the template. | No |
|`volume_attachments.name`|String|Required|The name of the boot volume. | No |
|`volume_attachments.volume`|String|Required|The storage volume ID created in VPC. | No |
|`volume_attachments.delete_volume_on_instance_delete`|Boolean|Required|You can configure to delete the storage volume to delete based on instance deletion. | No |
|`user_data` | String|Optional|The user data provided for the instance. | No |
{: caption="Table 1. Available output parameters" caption-side="top"}

### Output parameters
{: #instance-template-output}

Review the output parameters that you can access after your resource is created.
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of an instance template.|

### Import
{: #instance-template-import}

`ibm_is_instance_template` can be imported by using instance template ID

```
terraform import ibm_is_instance_template.template r006-14140f94-fcc4-1349-96e7-a72734715115
```
{: pre}

## `ibm_is_ipsec_policy`
{: #provider-ipsec}

Create, update, or cancel an IPSec policy. 
{: shortdesc}

### Sample Terraform code
{: #ipsec-policy-sample}

```
resource "ibm_is_ipsec_policy" "example" {
    name = "test"
    authentication_algorithm = "md5"
    encryption_algorithm = "triple_des"
    pfs = "disabled"
}
```
{: codeblock}

### Input parameters
{: #ipsec-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ---------- |
| `authentication_algorithm` | String | Required | Enter the algorithm that you want to use to authenticate `IPSec` peers. Available options are `md5`, `sha1`, or `sha256`. | No |
| `encryption_algorithm` | String | Required | Enter the algorithm that you want to use to encrypt data. Available options are: `triple_des`, `aes128`, or `aes256`. |  No |
| `key_lifetime` | Integer | Optional | Enter the time in seconds that your encryption key can be used before it expires. You must enter a number between 300 and 86400. If you do not specify this option, 3600 seconds is used. | No |
| `name` | String | Required | Enter the name for your IPSec policy. | No |
| `pfs` | String | Required | Enter the Perfect Forward Secrecy protocol that you want to use during a session. Available options are `disabled`, `group_2`, `group_5`, and `group_14`. | No |
| `resource_group` | String | Optional | Enter the ID of the resource group where you want to create the IPSec policy. To list available resource groups, run `ibmcloud resource groups`. If you do not specify a resource group, the IPSec policy is created in the `default` resource group. |  Yes |

### Output parameters
{: #ike-policy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `encapsulation_mode` | String | The encapsulation mode that was set for your IPSec policy. Only `tunnel` is supported. |
| `id` | String | The unique identifier of the IPSec policy that you created. |
| `transform_protocol` | String | The transform protocol that is used in your IPSec policy. Only the `esp` protocol is supported that uses the triple DES (3DES) encryption algorithm to encrypt your data. |
| `vpn_connections`| List | A collection of VPN connections that use the IPSec policy. Every connection is listed with a VPC connection `name`, `id`, and `canonical URL`. | 


## `ibm_is_image`
{: #image}

Upload, update, or delete a custom virtual server instance image. For more information, about how to create a custom image, see the [VPC documentation](/docs/vpc?topic=vpc-managing-images).
{: shortdesc}

### Sample Terraform code
{: #image-sample}

```
resource "ibm_is_image" "test_is_images" {
 name                   = "test_image"
 href                   = "cos://us-south/buckettesttest/livecd.ubuntu-cpc.azure.vhd"
 operating_system       = "ubuntu-16-04-amd64"
 encrypted_data_key     = "eJxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx0="
 encryption_key         = "crn:v1:bluemix:public:kms:us-south:a/6xxxxxxxxxxxxxxx:xxxxxxx-xxxx-xxxx-xxxxxxx:key:dxxxxxx-fxxx-4xxx-9xxx-7xxxxxxxx"
}
```
{: codeblock}

### Input parameters
{: #image-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ----- |
|`encrypted_data_key`|String|Optional|A base64-encoded, encrypted representation of the key that was used to encrypt the data for this image.| Yes |
|`encryption_key`|String|Optional|The CRN of the Key Protect Root Key or Hyper Protect Crypto Service Root Key for this resource.| Yes |
|`href`|String|Required| The path of an image to be uploaded.| No |
|`name`|String|Required|The descriptive name used to identify an image.| No |
|`operating_system`|String|Required|Description of underlying OS of an image.| No |
|`resource_group`|String|Optional|The resource group ID for this image.| Yes |
|`tags`|Array of strings|Optional|A list of tags that you want to your image. Tags can help you find the image more easily later.| No |

### Output parameters
{: #image-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the image.|
|`architecture`|String|The processor architecture that this image is based on.|
|`crn`|String| The CRN for the image.|
|`file`|String| The file.|
|`format`|String| The format of an image.|
|`resourceGroup`|String| The resource group to which the image belongs to.|
|`status`|String| - The status of an image such as `corrupt`, or `available`.|
|`visibility`|String|The access scope of an image such as `private` or `public`.|
|`encryption`|String|The type of encryption used on the image.|

### Import
{: #image-import}

The `ibm_is_image` can be imported by using image ID.

**Example**

```
terraform import ibm_is_image.example d7bec597-4726-451f-8a63-e62e6f19c32c
```
{: pre}

## `ibm_is_lb`
{: #lb}

Create, update, or delete a VPC Load Balancer. For more information, see [Load Balancers for VPC](/docs/vpc?topic=vpc-nlb-vs-elb).
{: shortdesc}

### Sample Terraform code
{: #lb-sample}

An example to create an application load balancer:

```
resource "ibm_is_lb" "lb" {
  name    = "loadbalancer1"
  subnets = ["04813493-15d6-4150-9948-6cc646cb67f2"]
}
```
An example to create a network load balancer:

```
resource "ibm_is_lb" "lb" {
  name    = "loadbalancer1"
  subnets = ["04813493-15d6-4150-9948-6cc646cb67f2"]
  profile = "network-fixed"
}
```
{: codeblock}

### Input parameters
{: #lb-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`name`|String|Required|The name of the VPC load balancer.| No |
|`profile`|String|Required|The profile to use for this Load Balancer. Supported value is `network-fixed`.| Yes |
|`resource_group`|String|Optional| The resource group where the load balancer to be created.| Yes |
|`subnets`|Array|Required|List of the subnets IDs to connect to the load balancer.| No |
|`tags`|Array of strings|Optional|A list of tags that you want to add to your load balancer. Tags can help you find the load balancer more easily later. | No |
|`type`|String|Optional|The type of the load balancer. Default value `public`. Supported values `public` and `private`.| Yes |

### Output parameters
{: #lb-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`hostname`|String|The fully qualified domain name assigned to this load balancer.|
|`id`|String|The unique identifier of the load balancer.|
|`operating_status`|String|The operating status of this load balancer.|
|`public_ips`|String|The public IP addresses assigned to this load balancer.|
|`private_ips`|String|The private IP addresses assigned to this load balancer.|
|`status`|String|The status of the load balancer.|

### Import
{: #lb-import}

`ibm_is_lb` can be imported by using the load balancer ID. 

**Syntax**
```
terraform import ibm_is_lb.example <lb_ID>
```
{: pre}

**Example**
```
terraform import ibm_is_lb.example d7bec597-4726-451f-8a63-e62e6f19c32c
```

### Timeouts
{: #lb-timeout}

`ibm_is_lb` provides the following Timeouts. 

- **create** - (Default 10 minutes) Used for creating Instance.
- **delete** - (Default 10 minutes) Used for deleting Instance.

## `ibm_is_lb_listener`
{: #lb-listener}

Create, update, or delete a listener for a VPC load balancer. For more information, see [working with listeners](/docs/vpc?topic=vpc-nlb-listeners).

When provisioning the load balancer listener along with load balancer pool or pool member, use explicit dependencies on the resources or perform the Terraform apply with parallelism 1. 
{: note}

### Sample Terraform code
{: #lb-listener-sample}

```
resource "ibm_is_lb_listener" "testacc_lb_listener" {
  lb       = "8898e627-f61f-4ac8-be85-9db9d8bfd345"
  port     = "9080"
  protocol = "http"
  default_pool = "ibmcloud is load-balancer-pools <load_balancer_ID>"
}

resource "ibm_is_lb_pool" "webapptier-lb-pool" {
  lb                 = "8898e627-f61f-4ac8-be85-9db9d8bfd345"
  name               = "a-webapptier-lb-pool"
  protocol           = "http"
  algorithm          = "round_robin"
  health_delay       = "5"
  health_retries     = "2"
  health_timeout     = "2"
  health_type        = "http"
  health_monitor_url = "/"
  depends_on         = [ibm_is_lb_listener.testacc_lb_listener]
}

resource "ibm_is_lb_pool_member" "webapptier-lb-pool-member-zone1" {
  count          = "2"
  lb             = "8898e627-f61f-4ac8-be85-9db9d8bfd345"
  pool           = element(split("/", ibm_is_lb_pool.webapptier-lb-pool.id), 1)
  port           = "80"
  target_address = "192.168.0.1"
  depends_on     = [ibm_is_lb_listener.testacc_lb_listener]
}
```
{: codeblock}

### Input parameters
{: #lb-listener-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`lb`|String|Required|The load balancer unique identifier.| Yes |
|`port`|Integer|Required|The listener port number. Valid range 1 to 65535.| No |
|`protocol`|String|Required|The listener protocol. Enumeration type are `http`, `tcp`, and `https`. Network Load Balancer supports only `tcp` protocol.| No |
|`default_pool`|String|Optional| The load balancer pool unique identifier.| No |
|`certificate_instance`|String|Optional|The CRN of the certificate instance.| No |
|`connection_limit`|Integer|Optional|The connection limit of the listener. Valid range is 1 to 15000. Network Load Balancer do not support `connection_limit` argument.| No |

### Output parameters
{: #lb-listener-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the load balancer listener.|
|`status`|String|The status of load balancer listener.|

### Import
{: #lb-listener-import}

`ibm_is_lb_listener` can be imported by using the load balancer ID and listener ID.

```
terraform import ibm_is_lb_listener.example <loadbalancer_ID>/<listener_ID>
```
{: pre}

### Timeouts
{: #lb-listener-timeout}

`ibm_is_lb_listener` provides the following timeouts:

- **create** - (Default 10 minutes) Used for creating Instance.
- **update** - (Default 10 minutes) Used for updating Instance.
- **delete** - (Default 10 minutes) Used for deleting Instance.

## `ibm_is_lb_listener_policy`
{: #lb-listener-policy}

Create, update, or delete a load balancer listener policy.  
{: shortdesc}

### Sample Terraform code
{: #lb-listener-policy-sample}


#### Creating a load balancer listener policy for a `redirect` action
{: #redirect-sample}

```
resource "ibm_is_lb" "lb2"{
  name    = "mylb"
  subnets = ["<subnet_ID>"]
}

resource "ibm_is_lb_listener" "lb_listener2"{
  lb       = ibm_is_lb.lb2.id
  port     = "9086"
  protocol = "http"
}
resource "ibm_is_lb_listener_policy" "lb_listener_policy" {
  lb = ibm_is_lb.lb2.id
  listener = ibm_is_lb_listener.lb_listener2.listener_id
  action = "redirect"
  priority = 2
  name = "mylistener8"
  target_http_status_code = 302
  target_url = "https://www.redirect.com"
  rules{
      condition = "contains"
      type = "header"
      field = "1"
      value = "2"
  }
}
```
{: codeblock}

#### Creating a load balancer listener policy for a `forward` action
{: #forward-sample}

```
resource "ibm_is_lb" "lb2"{
  name    = "mylb"
  subnets = ["<subnet_ID>"]
}

resource "ibm_is_lb_listener" "lb_listener2"{
  lb       = ibm_is_lb.lb2.id
  port     = "9086"
  protocol = "http"
}
resource "ibm_is_lb_listener_policy" "lb_listener_policy" {
  lb = ibm_is_lb.lb2.id
  listener = ibm_is_lb_listener.lb_listener2.listener_id
  action = "forward"
  priority = 2
  name = "mylistener8"
  target_id = "r006-beafdff0-4fe0-4db4-8f0c-b0b4ad828712"
  rules{
      condition = "contains"
      type = "header"
      field = "1"
      value = "2"
  }
}
```
{: codeblock}

### Input parameters
{: #lb-listener-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ----- |
|`lb`|String|Required|The ID of the load balancer for which you want to create a load balancer listener policy.|  Yes |
|`listener`|String|Required|The ID of the load balancer listener.| Yes |
|`action`|String|Required|The action that you want to specify for your policy. Supported values are `forward`, `redirect`, and `reject`.| Yes |
|`priority`|Integer|Required|The priority of the load balancer policy. Low values indicate a high priority. The value must be between 1 and 10.| Yes |
|`name`|String|Optional|The name for the load balancer policy. Names must be unique within a load balancer listener.| No |
|`rules`|List of policy rules|Required|A list of rules that you want to apply to your load balancer policy. Note that rules can be created only. You cannot update the rules for a load balancer policy.| No |
|`rules.condition`|String|Required|The condition that you want to apply to your rule. Supported values are `contains`, `equals`, and `matches_regex`.| No |
|`rules.type`|String|Required|The data type where you want to apply the rule condition. Supported values are `header`, `hostname`,  and `path`| No |
|`rules.value`|Integer|Required|The value that must be found in the HTTP header, hostname or path to apply the load balancer listener rule. The value that you define can be between 1 and 128 characters long.| No |
|`rules.field`|Integer|Required|If you selected `header` as the data type where you want to apply the rule condition, enter the name of the HTTP header that you want to check. The name of the header can be between 1 and 128 characters long. | No |
|`target_id`|Integer|Optional|When `action` is set to **forward**, specify the ID of the load balancer pool that the load balancer forwards network traffic to. | No |
|`target_http_status_code`|Integer|Optional|When `action` is set to **redirect**, specify the HTTP response code that must be returned in the redirect response. Supported values are `301`, `302`, `303`, `307`, and `308`. | No | 
|`target_url`|Integer|Optional|When `action` is set to **redirect**, specify the URL that is used in the redirect response.|  No |

### Output parameters
{: #lb-listener-policy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the load balancer listener policy. The ID is composed of `<lb_ID>/<listener_ID>/<policy_ID>`. |
|`status`|String|The status of the load balancer listener policy.|
|`policy_id`|String|The ID of the load balancer listener policy.|

### Import
{: #lb-listener-policy-import}

The resource can be imported by using the ID. The ID is composed of `<lb_ID>/<listener_ID>/<policy_ID>`.

```
terraform import ibm_is_lb_listener_policy.example <lb_ID>/<listener_ID>/<policy_ID>
```
{: pre}

### Timeouts
{: #listener-policy-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **create**: The creation of the load balancer listener policy is considered `failed` if no response is received for 10 minutes. 
- **delete**: The deletion of the load balancer listener policy is considered `failed` if no response is received for 10 minutes.
- **update**: The creation of the load balancer listener policy is considered `failed` if no response is received for 10 minutes. 

## `ibm_is_lb_listener_policy_rule`
{: #lb-listener-policy-rule}

Create, update, or delete a VPC load balancer listener policy rule.
{: shortdesc}

### Sample Terraform code
{: #lb-listener-policy-rule-sample}

```
resource "ibm_is_lb" "lb2"{
  name    = "mylb"
  subnets = ["35860fed-c911-4936-8c94-f0d8577dbe5b"]
}

resource "ibm_is_lb_listener" "lb_listener2"{
  lb       = ibm_is_lb.lb2.id
  port     = "9086"
  protocol = "http"
}
resource "ibm_is_lb_listener_policy" "lb_listener_policy" {
  lb = ibm_is_lb.lb2.id
  listener = ibm_is_lb_listener.lb_listener2.listener_id
  action = "redirect"
  priority = 2
  name = "mylistener8"
  target_http_status_code = 302
  target_url = "https://www.redirect.com"
  rules{
      condition = "contains"
      type = "header"
      field = "1"
      value = "2"
  }
}

resource "ibm_is_lb_listener_policy_rule" "lb_listener_policy_rule" {
  lb        = ibm_is_lb.lb2.id
  listener  = ibm_is_lb_listener.lb_listener2.listener_id
  policy    = ibm_is_lb_listener_policy.lb_listener_policy.policy_id
  condition = "equals"
  type      = "header"
  field     = "MY-APP-HEADER"
  value     = "New-value"
}
```
{: codeblock}

### Input parameters
{: #lb-listener-policy-rule-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource | 
|----|-----------|-----------|---------------------| ------ |
|`lb`|String|Required|The ID of the load balancer for which you want to create a listener policy rule.| Yes |
|`listener`|String|Required|The ID of the load balancer listener for which you want to create a policy rule.|  Yes |
|`policy`|String|Required|The ID of the load balancer listener policy for which you want to create a policy rule.|  Yes |
|`condition`|String|Required|The condition that you want to apply to your rule. Supported values are `contains`, `equals`, and `matches_regex`.| No |
|`type`|String|Required|The object where you want to apply the rule. Supported values are `header`, `hostname`, and `path`.| No |
|`value`|String|Required|The value that must match the rule condition. The value can be between 1 and 128 characters long. |  No |
|`field`|String|Optional|If you set `type` to `header`, enter the HTTP header field where you want to apply the rule condition. | No |

### Output parameters
{: #lb-listener-policy-rule-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the load balancer listener policy rule. The ID is composed of ` <loadbalancer_ID>/<listener_ID>/<policy>ID>`. |
|`status`|String|The status of the load balancer listener.|
|`rule`|String|The ID of the rule|

### Import
{: #lb-listener-policy-rule-import}

You can import the rule by using the ID.

```
terraform import ibm_is_lb_listener_policy.example <loadbalancer_ID>/<listener_ID>/<policy>ID>
```
{: pre}

### Timeout
{: #lb-listener-policy-rule-timeout}

The following timeouts are configured for the resource: 

- **Create**: The creation of the resource is considered failed if no response is received for 10 minutes. 
- **Update**: The update of the resource is considered failed if no response is received for 10 minutes. 
- **Delete**: The deletion of the resource is considered failed if no response is received for 10 minutes. 


## `ibm_is_lb_pool`
{: #lb-pool}

Create, update, or delete a VPC load balancer pool.  For more information, see [working with pool](/docs/vpc?topic=vpc-nlb-pools).
{: shortdesc}

### Sample Terraform code to create a Load Balancer pool.
{: #lb-pool-sample}

```
resource "ibm_is_lb_pool" "testacc_pool" {
  name           = "test_pool"
  lb             = "addfd-gg4r4-12345"
  algorithm      = "round_robin"
  protocol       = "http"
  health_delay   = 60
  health_retries = 5
  health_timeout = 30
  health_type    = "http"
}
```
{: codeblock}

### Sample Terraform code to create a Load Balancer pool with HTTPS protocol.
{: #lb-pool-https-sample2}

```
resource "ibm_is_lb_pool" "testacc_pool" {
  name           = "test_pool"
  lb             = "addfd-gg4r4-12345"
  algorithm      = "round_robin"
  protocol       = "https"
  health_delay   = 60
  health_retries = 5
  health_timeout = 30
  health_type    = "https"
}
```
{: codeblock}

### Input parameters
{: #lb-pool-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}


|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------ |
|`name`|String|Required| The name of the pool.| No |
|`lb` |String|Required|The load balancer unique identifier.| Yes |
|`algorithm`|String|Required|The load-balancing algorithm. Supported values are `round_robin`, `weighted_round_robin`, or `least_connections`.| No |
|`protocol`|String|Required|The pool protocol. Enumeration type: `http`, `https`, `tcp` are supported.| No |
|`health_delay`|Integer|Required|The health check interval in seconds. Interval must be greater than `timeout` value.| No |
|`health_retries`|Integer|Required|The health check max retries.| No |
|`health_timeout`|Integer|Required|The health check timeout in seconds.| No |
|`health_type`|String|Required|The pool protocol. Enumeration type: `http`, `https`, `tcp` are supported.| No |
|`health_monitor_url`|String|Optional|The health check URL. This option is applicable only to the HTTP `health-type`.| No |
|`health_monitor_port`|Integer|Optional|The health check port number.|  No |
|`session_persistence_type`|String|Optional|The persistence session type.  Enumeration type: `source_ip`, `http_cookie`, and `app_cookie` are supported.| No |
|`session_persistence_cookie_name`|String|Optional|The session  cookie session name. This option is applicable only to `--session-persistence-type`.| No |

### Output parameters
{: #lb-pool-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the load balancer pool. The ID is composed of `<lb_id>/<pool_id>`.|
|`provisioning_status`|String| The status of load balancer pool.|

### Import
{: #lb-pool-import}

`ibm_is_lb_pool` can be imported by using the load balancer ID and pool ID. 

```
terraform import ibm_is_lb_pool.example <loadbalancer_ID>/<pool_ID>
```
{: pre}

### Timeouts
{: #lb-pool-timeout}

`ibm_is_lb_pool` provides the following timeouts:

- **create** - (Default 10 minutes) Used for creating Instance.
- **update** - (Default 10 minutes) Used for updating Instance.
- **delete** - (Default 10 minutes) Used for deleting Instance.

## `ibm_is_lb_pool_member`
{: #lb-pool-member}

Create, update, or delete a pool member for a VPC load balancer. 
{: shortdesc}

### Sample Terraform code
{: #lb-pool-member-sample}

In the following example, you can create a load balancer pool member for application load balancer:
```
resource "ibm_is_lb_pool_member" "testacc_lb_mem" {
  lb             = "daac2b08-fe8a-443b-9b06-1cef79922dce"
  pool           = "f087d3bd-3da8-452d-9ce4-c1010c9fec04"
  port           = 8080
  target_address = "127.0.0.1"
  weight         = 60
}
```
{: codeblock}

In the following example, you can create a load balancer pool member for network load balancer:

```
resource "ibm_is_lb_pool_member" "testacc_lb_mem" {
  lb             = "daac2b08-fe8a-443b-9b06-1cef79922dce"
  pool           = "f087d3bd-3da8-452d-9ce4-c1010c9fec04"
  port           = 8080
  target_id      = "54ad563a-0261-11e9-8317-bec54e704988"
  weight         = 60
}
```
{: codeblock}

### Input parameters
{: #lb-pool-member-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| --------- |
|`lb`|String|Required| The load balancer unique identifier.| Yes |
|`pool`|String|Required| The load balancer pool unique identifier.| Yes |
|`port`|Integer|Required| The port number of the application running in the server member.| No |
|`target_address`|String|Required|The IP address of the pool member.| No |
|`target_id`|String|Required|The unique identifier for the virtual server instance pool member. Required for network load balancer.|No|
|`weight`|Integer|Optional| Weight of the server member. This option takes effect only when the load-balancing algorithm of its belonging pool is `weighted_round_robin`.| No |

### Output parameters
{: #lb-pool-member-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the load balancer pool member.|
|`health`|String|Health of the server member in the pool.|
|`href`|String|The member’s canonical URL.|

### Import
{: #lb-pool-member-import}

`ibm_is_lb_pool_member` can be imported by using the load balancer ID, pool ID, pool member ID.

**Example**

```
terraform import ibm_is_lb_pool_member.example <loadbalancer_ID>/<pool_ID>/<pool_member_ID>
```
{: pre}

### Timeouts
{: #lb-pool-member-timeout}

`ibm_is_lb_pool_member` provides the following timeouts.

- **create** - (Default 10 minutes) Used for creating Instance.
- **update** - (Default 10 minutes) Used for updating Instance.
- **delete** - (Default 10 minutes) Used for deleting Instance.


## `ibm_is_network_acl`
{: #network-acl}

Create, update, or delete a network access control list (ACL). 
{: shortdesc}

### Sample Terraform code
{: #network-acl-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "vpctest"
}

resource "ibm_is_network_acl" "isExampleACL" {
  name = "is-example-acl"
  vpc  = ibm_is_vpc.testacc_vpc.id
  rules {
    name        = "outbound"
    action      = "allow"
    source      = "0.0.0.0/0"
    destination = "0.0.0.0/0"
    direction   = "outbound"
    icmp {
      code = 1
      type = 1
    }
  }
  rules {
    name        = "inbound"
    action      = "allow"
    source      = "0.0.0.0/0"
    destination = "0.0.0.0/0"
    direction   = "inbound"
    icmp {
      code = 1
      type = 1
    }
  }
}
```
{: codeblock}

### Input parameters
{: #network-acl-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------------ |
|`name`|String|Required|The name of the network ACL.| No |
|`vpc`|String|Optional|The VPC ID. This parameter is required if you want to create a network ACL for a Gen 2 VPC.| Yes |
|`resource_group`|String|Optional|The ID of the resource group where you want to create the network ACL. | Yes |
|`rules`|List of rules|Optional|A list of rules for a network ACL. The order in which the rules are added to the list determines the priority of the rules. For example, the first rule that you want to enforce must be specified as the first rule in this list. | No |
|`rules.name`|String|Required|The user-defined name for this rule.| No |
|`rules.action`|String|Required|`Allow` or `deny` matching network traffic. | No |
|`rules.source`|String|Required|The source IP address or CIDR block.| No |
|`rules.destination`|String|Required|The destination IP address or CIDR block.| No |
|`rules.direction`|String|Required|Indicates whether the traffic to be matched is `inbound` or `outbound`.| No |
|`rules.icmp`|List of protocol information|Optional|The protocol ICMP.| No |
|`rules.icmp.code`|Integer|Optional|The ICMP traffic code to allow. Valid values from 0 to 255. If unspecified, all codes are allowed. This can only be specified if type is also specified.| No |
|`rules.icmp.type`|Integer|Optional|The ICMP traffic type to allow. Valid values from 0 to 254. If unspecified, all types are allowed by this rule.| No |
|`rules.tcp`|List of protocol information|Optional|The TCP protocol.| No |
|`rules.tcp.port_max`|Integer|Optional|The highest port in the range of ports to be matched; if unspecified, 65535 is used.| No |
|`rules.tcp.port_min`|Integer|Optional|The lowest port in the range of ports to be matched; if unspecified, 1 is used.| No |
|`rules.tcp.source_port_max`|Integer|Optional|The highest port in the range of ports to be matched; if unspecified, 65535 is used.| No |
|`rules.tcp.source_port_min`|Integer|Optional|The lowest port in the range of ports to be matched; if unspecified, 1 is used.| No |
|`rules.udp`|List of protocol information|Optional|The UDP protocol.| No |
|`rules.udp.port_max`|Integer|Optional|The highest port in the range of ports to be matched; if unspecified, 65535 is used.| No |
|`rules.udp.port_min`|Integer|Optional|The lowest port in the range of ports to be matched; if unspecified, 1 is used.| No |
|`rules.udp.source_port_max`|Integer|Optional|The highest port in the range of ports to be matched; if unspecified, 65535 is used.| No |
|`rules.udp.source_port_min`|Integer|Optional|The lowest port in the range of ports to be matched; if unspecified, 1 is used.| No |

### Output parameters
{: #network-acl-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the network ACL.|
|`rules`|List of rules |The rules for a network ACL.| 
|`rules.id`|String|The rule ID.|
|`rules.ip_version`|String|The IP version of the rule.|
|`rules.subnets`|String|The subnets for the ACL rule.|

### Import
{: #network-acl-import}

The resource can be imported by using the network ACL ID. 

```
terraform import ibm_is_network_acl.example <network_acl_id>
```
{: pre}

## `ibm_is_public_gateway`
{: #provider-public-gateway}

Create, update, or delete a public gateway for a VPC subnet. 
{: shortdesc}

Public gateways enable a VPC subnet and all the instances that are connected to the subnet to connect to the internet. For more information, see [Use a Public Gateway for external connectivity of a subnet](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-about-networking-for-vpc#use-a-public-gateway). 

To attach a public gateway that you created to a subnet, use the `public_gateway` input parameter in the [`ibm_is_subnet` resource](#subnet).
{: note}

### Sample Terraform code
{: #public-gateway-sample}

The following example shows how you can create a public gateway for all the subnets that are located in a specific zone. 

```
resource "ibm_is_vpc" "testacc_vpc" {
    name = "test"
}

resource "ibm_is_public_gateway" "testacc_gateway" {
    name = "test_gateway"
    vpc = ibm_is_vpc.testacc_vpc.id
    zone = "us-south-1"

    //User can configure timeouts
    timeouts {
        create = "90m"
    }
}
```
{: codeblock}

### Input parameters
{: #public-gateway-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------ |
| `name` | String| Required | Enter a name for your public gateway. | No |
| `vpc` | String | Required | Enter the ID of the VPC, for which you want to create a public gateway. To list available VPCs, run `ibmcloud is vpcs`.  | Yes |
| `zone` | String | Required | Enter the zone where you want to create the public gateway. To list available zones, run `ibmcloud is zones`. | Yes |
| `tags`|Array of strings|Optional|Enter any tags that you want to associate with your VPC. Tags might help you find your VPC more easily after it is created. Separate multiple tags with a comma (`,`). | No |
| `resource_group`|String|Optional|Enter the ID of the resource group where you want to create the public gateway. To list available resource groups, run `ibmcloud resource groups`. If you do not specify a resource group, the public gateway is created in the `default` resource group. | Yes |
| `floating_ip` | List | Optional | A list of floating IP addresses that you want to assign to the public gateway. | No |
| `floating_ip.id`|String| Optional | The unique identifier of the floating IP address. If you specify this parameter, do not specify `floating_ip.address` at the same time. | No | 
| `floating_ip.address`|String| Optional | The floating IP address. If you specify this parameter, do not specify `floating_ip.id` at the same time.| No |


### Output parameters
{: #public-gateway-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `floating_ip` | List | A list of floating IP addresses that are assigned to the public gateway. |
| `floating_ip.id`|String| The unique identifier that was assigned to the floating IP address.|
| `floating_ip.address`|String|The IP address that was assigned to the public gateway.|
| `id` | String | The unique identifier that was assigned to your public gateway. |
| `status` | String | The provisioning status of your public gateway. |

### Timeouts
{: #public-gateway-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **create**: The creation of the public gateway is considered `failed` when no response is received for 10 minutes. 
- **delete**: The deletion of the public gateway is considered `failed` when no response is received for 10 minutes.

## `ibm_is_security_group`
{: #sec-group}

Create, update, or delete a security group for your VPC. 
{: shortdesc}

When you want to create a security group and security group rule for a virtual server instance in your VPC, you must create these resources in a specific order to avoid errors during the creation of your virtual server instance. For an example, see [Example for creating an instance with custom security group rules](#custom-sec-group-rules). 
{: note}


### Sample Terraform code
{: #sec-group-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
	name = "test"
}

resource "ibm_is_security_group" "testacc_security_group" {
	name = "test"
	vpc = ibm_is_vpc.testacc_vpc.id
}
```
{: codeblock}

### Input parameters
{: #sec-group-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`name`|String|Optional|The security group name.| No |
|`vpc`|String|Required|The VPC ID. | Yes |
|`resource_group`|String|Optional|The resource group ID where the security group to be created.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #sec-group-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the security group.|
|`rules`|List of objects|A nested block describes the rules of this security group. |
|`rules.direction`| String|The direction of the traffic either `inbound` or `outbound`.  |
|`rules.ip_version`|String|IP version either `ipv4` or `ipv6`.  |
|`rules.remote`|String|Security group id, an IP address, a CIDR block, or a single security group identifier.  |
|`rules.protocol`|String|The type of the protocol `all`, `icmp`, `tcp`, `udp`.   |
|`rules.type`|String|The ICMP traffic type to allow.  |
|`rules.code`|String|The ICMP traffic code to allow.  |
|`rules.port_max`|Integer|The TCP/UDP port range that includes the maximum bound. |
|`rules.port_min`|Integer|The TCP/UDP port range that includes the minimum bound. |
{: caption="Table 1. Available output parameters" caption-side="top"}


### Import
{: #sec-group-import}

`ibm_is_security_group` can be imported by using load balancer ID. 

```
terraform import ibm_is_security_group.example a1aaa111-1111-111a-1a11-a11a1a11a11a
```
{: pre}


## `ibm_is_security_group_rule`
{: #sec-group-rule}

Create, update, or delete a security group rule. 
{: shortdesc}

When you want to create a security group and security group rule for a virtual server instance in your VPC, you must create these resources in a specific order to avoid errors during the creation of your virtual server instance. For an example, see [Example for creating an instance with custom security group rules](#custom-sec-group-rules). 
{: note}

### Sample Terraform code
{: #sec-group-rule-sample}

In the following example, you create a different type of protocol rules `ALL`, `ICMP`, `UDP` and `TCP`.

```
resource "ibm_is_vpc" "testacc_vpc" {
	name = "test"
}

resource "ibm_is_security_group" "testacc_security_group" {
	name = "test"
	vpc = ibm_is_vpc.testacc_vpc.id
}

resource "ibm_is_security_group_rule" "testacc_security_group_rule_all" {
	group = ibm_is_security_group.testacc_security_group.id
	direction = "inbound"
	remote = "127.0.0.1"
 }
 
 resource "ibm_is_security_group_rule" "testacc_security_group_rule_icmp" {
	group = ibm_is_security_group.testacc_security_group.id
	direction = "inbound"
	remote = "127.0.0.1"
	icmp {
		code = 20
		type = 30
	}

 }

 resource "ibm_is_security_group_rule" "testacc_security_group_rule_udp" {
	group = ibm_is_security_group.testacc_security_group.id
	direction = "inbound"
	remote = "127.0.0.1"
	udp {
		port_min = 805
		port_max = 807
	}
 }

 resource "ibm_is_security_group_rule" "testacc_security_group_rule_tcp" {
	group = ibm_is_security_group.testacc_security_group.id
	direction = "outbound"
	remote = "127.0.0.1"
	tcp {
		port_min = 8080
		port_max = 8080
	}
 }
```
{: codeblock}

### Input parameters
{: #sec-group-rule-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| -------- |
|`group`|String|Required|The security group ID.| Yes |
|`direction`|String|Required|The direction of the traffic either `inbound` or `outbound`.| No |
|`remote`|String|Optional|Security group id, an IP address, a CIDR block, or a single security group identifier.| No |
|`ip_version`|String|Optional|The IP version either `IPv4` or `IPv6`. Default `IPv4`.| No |
|`icmp`|List of objects|Optional|A nested block describes the `icmp` protocol of this security group rule.  | No |
|`icmp.type`|Integer|Required|The ICMP traffic type to allow. Valid values from 0 to 254.  | No |
|`icmp.code`|Integer|Optional|The ICMP traffic code to allow. Valid values from 0 to 255.| No |
|`tcp`|List of objects|Optional|A nested block describes the `tcp` protocol of this security group rule.  | No |
|`tcp.port_min`|Integer|Required| The TCP port range that includes the minimum bound. Valid values are from 1 to 65535.  | No |
|`tcp.port_max`|Integer|Required| The TCP port range that includes the maximum bound. Valid values are from 1 to 65535.| No |
|`udp`|List of objects| Optional| A nested block describes the `udp` protocol of this security group rule.  | No |
|`udp.port_min`|Integer|Required|The UDP port range that includes minimum bound. Valid values are from 1 to 65535.  | No |
|`udp.port_max`|Integer|Required|The UDP port range that includes maximum bound. Valid values are from 1 to 65535. **NOTE**: If any of the `icmp` , `tcp` or `udp` is not specified it creates a rule with protocol `ALL`. | No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #sec-group-rule-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the security group rule. The ID is composed of `<security_group_id>/<security_group_rule_id>`.|
|`rule_id`|String|The unique identifier of the rule.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #sec-group-rule-import}

`ibm_is_security_group_rule` can be imported by using security group ID and security group rule ID.

```
terraform import ibm_is_security_group_rule.example d7bec597-4726-451f-8a63-e62e6f19c32c/cea6651a-bc0a-4438-9f8a-a0770bbf3ebb
```
{: pre}


## `ibm_is_security_group_network_interface_attachment`
{: #sec-group-netint}

Create, update, or delete a security group network interface attachment. 
{: shortdesc}


### Sample Terraform code
{: #sec-group-netint-sample}

```
resource "ibm_is_security_group_network_interface_attachment" "sgnic" {
  security_group    = "2d364f0a-a870-42c3-a554-000001352417"
  network_interface = "6d6128aa-badc-45c4-bb0e-7c2c1c47be55"
}
```
{: codeblock}

### Input parameters
{: #sec-group-netint-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------ |
|`security_group`|String|Required|The security group ID.|  Yes |
|`network_interface`|String|Required|The network interface ID. | Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #sec-group-netint-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the security group network interface. The ID is composed of `<security_group_id>/<network_interface_id>`.|
|`instance_network_interface`|String|The instance network interface ID.|
|`name`|String|The user-defined name for this network interface.|
|`port_speed`|Integer|The network interface port speed in Mbps.|
|`primary_ipv4_address`|String|The primary IPv4 address.|
|`primary_ipv6_address`|String|The primary IPv6 address in compressed notation as specified by RFC 5952.|
|`secondary_address`|Array|Collection secondary IP addresses.|
|`status`|String|The status of the volume.|
|`subnet`|String|The Subnet ID.|
|`type`|String|The type of this network interface as it relates to a instance.|
|`security_groups`|List of objects|A nested block describes the security groups of this network interface.|
|`security_groups.id`|String|The ID of this security group.	|
|`security_groups.crn`|String|The CRN of this security group.	|
|`security_groups.name`|String|The name of this security group.|
|`floating_ips`|List of objects|A nested block describes the floating IP's of this network interface. |
|`floating_ips.id`|String|The ID of this floating IP.  |
|`floating_ips.crn`|String|The CRN of this floating IP.  |
|`floating_ips.name`|String|The name of this floating IP.  |
|`floating_ips.address`|String|The globally unique IP address|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Import
{: #sec-group-netint-import}

`ibm_is_security_group_network_interface_attachment` can be imported using security group ID and network interface ID.

```
terraform import ibm_is_security_group_network_interface_attachment.example <security_group_ID>/<network_interface_ID>
```
## `ibm_is_ssh_key`
{: #ssh-key}

Create, update, or delete an SSH key. The SSH key is used to access a Gen 2 virtual server instance.
{: shortdesc}


### Sample Terraform code
{: #ssh-key-sample}

```
resource "ibm_is_ssh_key" "isExampleKey" {
	name = "test_key"
	public_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCKVmnMOlHKcZK8tpt3MP1lqOLAcqcJzhsvJcjscgVERRN7/9484SOBJ3HSKxxNG5JN8owAjy5f9yYwcUg+JaUVuytn5Pv3aeYROHGGg+5G346xaq3DAwX6Y5ykr2fvjObgncQBnuU5KHWCECO/4h8uWuwh/kfniXPVjFToc+gnkqA+3RKpAecZhFXwfalQ9mMuYGFxn+fwn8cYEApsJbsEmb0iJwPiZ5hjFC8wREuiTlhPHDgkBLOiycd20op2nXzDbHfCHInquEe/gYxEitALONxm0swBOwJZwlTDOB7C6y2dzlrtxr1L59m7pCkWI4EtTRLvleehBoj3u7jB4usR"
}
```
{: codeblock}

### Input parameters
{: #ssh-key-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| -------- |
|`name`|String|Required| The user-defined name for this key.| No |
|`public_key`|String|Required|The public SSH key.| Yes |
|`resource_group`|String|Optional|The resource group ID where the SSH is created.| Yes |
|`tags`|List of strings|A list of tags that you want to add to your SSH key. Tags can help you find the SSH key more easily later. | No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #ssh-key-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the SSH key.|
|`fingerprint`| String|The SHA256 fingerprint of the public key.|
|`length`|String|The length of this key.|
|`type`|String|The crypto system used by this key.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import

`ibm_is_ssh_key` can be imported by using the SSH key ID. 

```
terraform import ibm_is_ssh_key.example <ssh_key_ID>
```
{: pre}

## `ibm_is_subnet`
{: #subnet}

Create, update, or delete a subnet.
{: shortdesc}

### Sample Terraform code
{: #subnet-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "test"
}

resource "ibm_is_vpc_routing_table" "test_cr_route_table1" {
  name   = "test-cr-route-table1"
  vpc    = data.ibm_is_vpc.testacc_vpc.id
}


resource "ibm_is_subnet" "testacc_subnet" {
  name            = "test_subnet"
  vpc             = ibm_is_vpc.testacc_vpc.id
  zone            = "us-south-1"
  ipv4_cidr_block = "192.168.0.0/1"
  routing_table   = ibm_is_vpc_routing_table.test_cr_route_table1.routing_table  

  //User can configure timeouts
  timeouts {
    create = "90m"
    delete = "30m"
  }
}
```
{: codeblock}

### Input parameters
{: #subnet-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|Forces new resource |
|----|-----------|-----------|---------------------|-------|
|`ipv4_cidr_block`|String|Optional|The IPv4 range of the subnet.| Yes |
|`total_ipv4_address_count`|String|Optional|The total number of IPv4 addresses. Either `ipv4_cidr_block` or `total_pv4_address_count` input parameters must be provided in the resource.| Yes |
|`ip_version`|String|Optional|The IP Version. The default is `ipv4`.| Yes |
|`name`|String|Required| The name of the subnet.| No |
|`network_acl`|String|Optional|The ID of the network ACL for the subnet.| No |
|`public_gateway`|String|Optional|The ID of the public gateway for the subnet that you want to attach to the subnet. You create the public gateway with the [`ibm_is_public_gateway` resource](#provider-public-gateway).| No |
|`resource_group`|String|Optional|The ID of the resource group where you want to create the subnet.| Yes |
|`vpc`|String|Required|The VPC ID.| Yes |
|`zone`|String|Required|The subnet zone name.| Yes |
|`routing_table`|String|Optional| The routing table ID associated with the subnet.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #subnet-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the subnet.|
|`ipv6_cidr_block`|String|The IPv6 range of the subnet.|
|`status`|String|The status of the subnet.|
|`available_ipv4_address_count`|String|The total number of available IPv4 addresses.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #subnet-import}

The `ibm_is_subnet` can be imported by using the ID. 

**Syntax**

```
terraform import ibm_is_subnet.example <subnet_ID>
```
{: pre}

**Example**

```
terraform import ibm_is_subnet.example d7bec597-4726-451f-8a63-e62e6f19c32c
```
{: pre}

### Timeouts
{: #subnet-timeout}

`ibm_is_subnet` provides the following [Timeouts](https://www.terraform.io/docs/configuration/resources.html#timeouts) configuration options:

|Name|Description|
|----|-----------|
|`create`|(Default 10 minutes) Used for creating Instance.|
|`update`|(Default 10 minutes) Used for creating Instance.|
|`delete`|(Default 10 minutes) Used for deleting Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}

## `ibm_is_subnet_network_acl_attachment`
{: #subnet-network}

Create, update, or delete a subnet network ACL attachment resource.
{: shortdesc}

### Sample Terraform code
{: #subnet-network-sample}


```
resource "ibm_is_network_acl" "isExampleACL" {
  name = "is-example-acl"
  rules {
    name        = "outbound"
    action      = "allow"
    source      = "0.0.0.0/0"
    destination = "0.0.0.0/0"
    direction   = "outbound"
    icmp {
      code = 1
      type = 1
    }
  }
  rules {
    name        = "inbound"
    action      = "allow"
    source      = "0.0.0.0/0"
    destination = "0.0.0.0/0"
    direction   = "inbound"
    icmp {
      code = 1
      type = 1
    }
  }
}

resource "ibm_is_subnet" "testacc_subnet" {
  name            = "test_subnet"
  vpc             = ibm_is_vpc.testacc_vpc.id
  zone            = "us-south-1"
  ipv4_cidr_block = "192.168.0.0/1"

}

resource "ibm_is_subnet_network_acl_attachment" attach {
  subnet      = ibm_is_subnet.testacc_subnet.id
  network_acl = ibm_is_network_acl.isExampleACL.id
}
```
{: codeblock}

### Input parameters
{: #subnet-network-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|Forces new resource |
|----|-----------|-----------|---------------------|-------|
|`network_acl`|String|Optional|The network ACL identity.| No |
|`subnet`|String|Optional|The subnet identifier.| Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #subnet-network-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`created_at`|String|The creation date and time the network ACL.|
|`crn`|String|The CRN of this network ACL.|
|`href`|String|The URL of this network ACL.|
|`id`|String|The unique identifier of this network ACL.|
|`name`|String|The user-defined name of this network ACL.|
|`protocol`|List|The protocol list to enforce.|
|`protocol.icmp`|String|The protocol ICMP.|
|`protocol.icmp.code`|String|The ICMP traffic code to allow. If unspecified, all codes are allowed. This can only be specified if type is also specified. |
|`protocol.icmp.type`|String|The ICMP traffic type to allow. If unspecified, all types are allowed by this rule. |
|`protocol.tcp`|String|The TCP protocol.|
|`protocol.tcp.destination_port_max`|String|The inclusive maximum bound of TCP destination port range. |
|`protocol.tcp.destination_port_min`|String|The inclusive minimum bound of TCP destination port range. |
|`protocol.tcp.source_port_max`|String|The inclusive maximum bound of TCP source port range. |
|`protocol.tcp.source_port_min`|String|The inclusive minimum bound of TCP source port range. |
|`protocol.udp`|String|The UDP protocol.|
|`protocol.udp.destination_port_max`|String|The inclusive maximum bound of UDP destination port range. |
|`protocol.udp.destination_port_min`|String|The inclusive minimum bound of UDP destination port range. |
|`protocol.udp.source_port_max`|String|The inclusive maximum bound of UDP source port range. |
|`protocol.udp.source_port_min`|String|The inclusive minimum bound of UDP source port range. |
|`protocol.subnets`|String|The subnets to which this network ACL is attached.|
|`protocol.vpc`|String|The VPC to which this network ACL is a part of.|
|`resource_group`|String|The resource group of this network ACL.|
|`rules`|String|The ordered rules of this network ACL. If rules does not exist, all traffic will be denied. Nested rules blocks has the following structure.|
|`rules.action`|String|Specify to allow or deny matching traffic.|
|`rules.created_at`|String|The rule creation date and time.|
|`rules.source`|String|The source CIDR block. The CIDR block 0.0.0.0/0 applies to all addresses.|
|`rules.destination`|String|The destination CIDR block. The CIDR block 0.0.0.0/0 applies to all addresses.|
|`rules.href`|String|The URL of the Network ACL rule.|
|`rules.id`|String|The unique identifier of the Network ACL rule.|
|`rules.ip_version`|String|The IP version of the rule.|
|`rules.name`|String|The user-defined name of the rule.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #subnet-network-import}

`ibm_is_subnet_network_acl_attachment` can be imported by using the ID. 

**Syntax**
```
terraform import ibm_is_subnet_network_acl_attachment.example <subnet_network_acl_ID>
```
{: pre}

**Example**
```
terraform import ibm_is_subnet_network_acl_attachment.example d7bec597-4726-451f-8a63-e62e6f19c32c
```
{: pre}


## `ibm_is_virtual_endpoint_gateway`
{: #virtual-endpoint-gwy}

Create, update, or delete a VPC endpoint gateway by using virtual endpoint gateway resource. For more information, about the VPC endpoint gateway, see [Creating an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway).
{: shortdesc}

### Sample Terraform code
{: #virtual-endpoint-gwy-sample}

The following example creates a VPN gateway. 

```
resource "ibm_is_virtual_endpoint_gateway" "endpoint_gateway1" {

  name = "my-endpoint-gateway-1"
  target {
	name          = "ibm-dns-server2"
    resource_type = "provider_infrastructure_service"
  }
  vpc = ibm_is_vpc.testacc_vpc.id
  resource_group = data.ibm_resource_group.test_acc.id
}

resource "ibm_is_virtual_endpoint_gateway" "endpoint_gateway2" {
	name = "my-endpoint-gateway-1"
	target {
	  name          = "ibm-dns-server2"
	  resource_type = "provider_infrastructure_service"
	}
	vpc = ibm_is_vpc.testacc_vpc.id
	ips {
		subnet   = ibm_is_subnet.testacc_subnet.id
		name        = "test-reserved-ip1"
	}
	resource_group = data.ibm_resource_group.test_acc.id
}

resource "ibm_is_virtual_endpoint_gateway" "endpoint_gateway3" {
	name = "my-endpoint-gateway-1"
	target {
	  name          = "ibm-dns-server2"
	  resource_type = "provider_infrastructure_service"
	}
	vpc = ibm_is_vpc.testacc_vpc.id
	ips {
		id   = "0737-5ab3c18e-6f6c-4a69-8f48-20e3456647b5"
	}
	resource_group = data.ibm_resource_group.test_acc.id
}
```
{: codeblock}

### Input parameters
{: #virtual-endpoint-gwy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}


|Name|Data type|Required / optional|Description|Forces new resource|
|----|-----------|-----------|---------------------| ------- |
|`name`|String|Required|The endpoint gateway name.| Yes |
|`ips`|List|Optional|The endpoint gateway resource group.| No |
|`ips.id`|String|Optional|The endpoint gateway resource group IPs ID.| No |
|`ips.name`|String|Optional|The endpoint gateway resource group IPs name.| No |
|`ips.subnet`|String|Optional|The endpoint gateway resource group subnet ID.| No |
|`ips.resource_type`|String|Computed|The endpoint gateway resource group VPC resource type.| No |
|`resource_group`|String|Optional|The resource group ID.| Yes |
|`tags`|List of strings| Optional |A list of tags associated with the instance.| No |
|`target`|List|Required|The endpoint gateway target.| No |
|`target.crn`|String|Optional|The endpoint gateway target `CRN`. If CRN not specified, `name` must be specified.| Yes|
|`target.name`|String|Required|The endpoint gateway target name.| No |
|`target.resource_type`|String|Required|The endpoint gateway target resource type.| No |
|`vpc`|String|Required|The VPC ID.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #virtual-endpoint-gwy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the VPN gateway connection. The ID is composed of `<gateway_id>`.|
|`resource_type`|String|The endpoint gateway resource type.|
|`created_at`|String|The created date and time of the endpoint gateway.|
|`health_state`|String|The health state of the endpoint gateway.|
|`lifecycle_state`|String|The lifecycle state of the endpoint gateway.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #virtual-endpoint-gwy-import}

The `ibm_is_virtual_endpoint_gateway` can be imported by using virtual endpoint gateway ID.

**Example**
```
terraform import ibm_is_virtual_endpoint_gateway.example d7bec597-4726-451f-8a63-xxxxsdf345
```
{: pre}


## `ibm_is_virtual_endpoint_gateway_ip`
{: #virtual-endpoint-gwyip}

Create, update, or delete a VPC endpoint gateway IP by using virtual endpoint gateway resource. For more information, about the VPC endpoint gateways, see [About VPC gateways](/docs/vpc?topic=vpc-about-vpe).
{: shortdesc}


### Sample Terraform code
{: #virtual-endpoint-gwyip-sample}

The following example creates a VPN gateway IP.

```
resource "ibm_is_virtual_endpoint_gateway_ip" "virtual_endpoint_gateway_ip" {
	gateway = ibm_is_virtual_endpoint_gateway.endpoint_gateway.id
	reserved_ip = "0737-5ab3c18e-6f6c-4a69-8f48-20e3456647b5"
}

```
{: codeblock}

### Input parameters
{: #virtual-endpoint-gwyip-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|Forces new resource|
|----|-----------|-----------|---------------------| ------- |
|`gateway`|String|Required|The endpoint gateway ID.| Yes |
|`reserver_ip`|String|Required|The endpoint gateway IP ID.| Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #virtual-endpoint-gwyip-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the VPN gateway connection. The ID is composed of `<gateway_id>/<gateway_ip_id>`.|
|`name`|String|The endpoint gateway IP name.|
|`created_at`|String|The created date and time of the endpoint gateway IP.|
|`resource_type`|String|The endpoint gateway IP resource type.|
|`auto_delete`|String|The endpoint gateway IP auto delete.|
|`address`|String|The endpoint gateway IP address.|
|`target`|String|The endpoint gateway target details.|
|`target.id`|String|The IPs target ID.|
|`target.name`|String|The IPs target name.|
|`target.resource_type`|String|The endpoint gateway resource type.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #virtual-endpoint-gwyip-import}

The `ibm_is_virtual_endpoint_gateway_ip` can be imported using virtual endpoint gateway ID and gateway IP ID.

**Example**
```
terraform import ibm_is_virtual_endpoint_gateway_ip.example d7bec597-4726-451f-8a63-e62e6f19c32c/d7bec597-4726-451f-8a63-e62e6f19d35f

```
{: pre}

## `ibm_is_volume`
{: #volume}

Create, update, or delete a VPC block storage volume. For more information, about the VPC block storage volume, see [Getting started with VPC](/docs/vpc).
{: shortdesc}

### Sample Terraform code
{: #volume-sample}

The following example creates a volume with 10 IOPS. 

```
resource "ibm_is_volume" "testacc_volume" {
  name     = "test_volume"
  profile  = "10iops-tier"
  zone     = "us-south-1"
  iops     = 10000
  capacity = 100
}

```
{: codeblock}

The following example creates a custom volume. 

```
resource "ibm_is_volume" "testacc_volume" {
  name     = "test_volume"
  profile  = "custom"
  zone     = "us-south-1"
  iops     = 1000
  capacity = 200
}
```
{: codeblock}

### Input parameters
{: #volume-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}


|Name|Data type|Required / optional|Description|Forces new resource|
|----|-----------|-----------|---------------------| ------- |
|`name`|String|Required|The user-defined name for this volume.| No |
|`profile`|String|Required|The profile to use for this volume.| Yes |
|`zone`|String|Required|The location of the volume.| Yes |
|`iops`|Integer|Required for `custom` storage profiles only| The total input/ output operations per second (IOPS) for your storage. This value is required for `custom` storage profiles only. | Yes |
|`capacity`|Integer|Optional|(The capacity of the volume in gigabytes. This defaults to `100`.| Yes |
|`encryption_key`|String|Optional|The key to use for encrypting this volume.| Yes |
|`resource_group`|String|Optional|The resource group ID for this volume.| Yes |
|`resource_controller_url`|String|Optional|The URL of the IBM Cloud dashboard that can be used to explore and view details about this instance.| Yes |
|`tags`|List of strings| Optional |A list of tags that you want to add to your volume. Tags can help you find your volume more easily later.| No |

{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #volume-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the volume.|
|`status`|String|The status of volume.|
|`crn`|String|The CRN for the volume.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Timeouts
{: #volume-timeout}

`ibm_is_volume` provides the following timeouts:

|Name|Description|
|----|-----------|
|`create`|(Default 10 minutes) Used for Creating Instance.|
|`delete`|(Default 10 minutes) Used for Deleting Instance.|
{: caption="Table. Available timeout configuration options" caption-side="top"}

### Import
{: #volume-import}

The `ibm_is_volume` can be imported by using volume ID.

**Example**
```
terraform import ibm_is_volume.example d7bec597-4726-451f-8a63-e62e6f19c32c
```
{: pre}

## `ibm_is_vpc` 
{: #provider-vps}

Create, update, or delete a Virtual Private Cloud (VPC). VPCs allow you to create your own space in {{site.data.keyword.cloud_notm}} to run an isolated environment within the public cloud. VPC gives you the security of a private cloud, with the agility and ease of a public cloud.
{: shortdesc}

For more information, see [About Virtual Private Cloud](/docs/vpc-on-classic?topic=vpc-on-classic-about). 

### Sample Terraform code
{: #vpc-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
    name = "test"
}
```
{: codeblock}

### Input parameters
{: #vpc-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `classic_access` | Boolean | Optional | Specify if you want to create a VPC that can connect to classic infrastructure resources. Enter **true** to set up private network connectivity from your VPC to classic infrastructure resources that are created in the same {{site.data.keyword.cloud_notm}} account, and **false** to disable this access. If you choose to not set up this access, you cannot enable it after the VPC is created. Make sure to review the [prerequisites](/docs/vpc-on-classic-network?topic=vpc-on-classic-setting-up-access-to-your-classic-infrastructure-from-vpc#vpc-prerequisites) before you create a VPC with classic infrastructure access. Note that you can enable one VPC for classic infrastructure access per {{site.data.keyword.cloud_notm}} account only. | No |
|`address_prefix_management`|String|Optional|Indicates whether a default address prefix should be created automatically (`auto`) or manually (`manual`) for each zone in this VPC. Default value `auto`.| No |
|`default_network_acl`|String | Deprecated | The ID of the default network ACL.|No|
| `name` | String | Required | Enter a name for your VPC. |  No |
| `resource_group` | String | Optional | Enter the ID of the resource group where you want to create the VPC. To list available resource groups, run `ibmcloud resource groups`. If you do not specify a resource group, the VPC is created in the `default` resource group. |  Yes |
| `tags` | Array of Strings | Optional | Enter any tags that you want to associate with your VPC. Tags might help you find your VPC more easily after it is created. Separate multiple tags with a comma (`,`). |  No |


### Output parameters
{: #vpc-arguments}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`crn`|String|The CRN of the VPC.|
| `default_security_group` | String | The default security group ID of your VPC. | 
|`default_network_acl`| String| The unique ID of the VPC default network ACL.|
| `id` | String | The unique identifier of the VPC that you created. |
|`subnets`|List of subnets|A list of subnets that are attached to a VPC.|
|`subnets.name`|String|The name of the subnet.|
|`subnets.id`|String|The ID of the subnet.|
|`subnets.status`|String|The status of the subnet.|
|`subnets.zone`|String| The Zone of the subnet.|
|`subnets.total_ipv4_address_count`|String| Total IPv4 addresses under the subnet.|
|`subnets.available_ipv4_address_count`|String | Available IPv4 addresses available for the usage in the subnet.|
|`subnets.total_ipv4_address_count`|Integer|The total number of IPv4 addresses in the subnet.|
|`subnets.available_ipv4_address_count`|Integer|The number of IPv4 addresses in the subnet that are available for you to be used.|
| `status` | String | The provisioning status of your VPC. | 
| `cse_source_addresses`|List of Cloud Service Endpoints|A list of the cloud service endpoints that are associated with your VPC, including their source IP address and zone.|
|`cse_source_addresses.address`|String|The IP address of the cloud service endpoint.|
|`cse_source_addresses.zone_name`|String|The zone where the cloud service endpoint is located.|
|`security_group`|String|  A list of security groups attached to VPC. The nested security group block has the following structure:|
|`security_group.group_id`| String | The security group ID.|
|`security_group.group_name`| String | The name of the security group.|
|`security_group.rules`| String | Set of rules attached to a security group.|
|`security_group.rules.rule_id`| String | The rule ID. |
|`security_group.rules.direction`| String |  The direction of the traffic either inbound or outbound.|
|`security_group.rules.ip_version`| String |  ip version either ipv4 or IPv6.|
|`security_group.rules.remote`| String | Security group id, an IP address, a CIDR block, or a single security group identifier.|
|`security_group.rules.type`| String | The ICMP traffic type to allow.|
|`security_group.rules.code`| String | The ICMP traffic code to allow.|
|`security_group.rules.port_min`| String | The inclusive lower bound of TCP port range.|
|`security_group.rules.port_max`| String | The inclusive upper bound of TCP port range.|

### Timeouts
{: #vpc-timeout}

The following timeouts are defined for the resource: 

- **create**: The creation of the VPC is considered `failed` when no response is received for 10 minutes. 
- **delete**: The deletion of the VPC is considered `failed` when no response is received for 10 minutes. 


### Import
{: #vpc-import}

The `ibm_is_vpc` resource can be imported by using the VPC ID.

**Example**

```
terraform import ibm_is_vpc.example <vpc_ID>
```
{: pre}


## `ibm_is_vpc_address_prefix`
{: #address-prefix}

Create, update, or delete an IP address prefix. 
{: shortdesc}

### Sample Terraform code
{: #address-prefix-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "testvpc"
}

resource "ibm_is_vpc_address_prefix" "testacc_vpc_address_prefix" {
  name = "test"
  zone   = "us-south-1"
  vpc         = ibm_is_vpc.testacc_vpc.id
  cidr        = "10.240.0.0/24"
}

```
{: codeblock}

### Input parameters
{: #address-prefix-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|Forces new resource |
|----|-----------|-----------|---------------------|------|
|`name`|String|Required| The address prefix name.| No |
|`vpc`|String|Required|The VPC ID. | Yes |
|`zone`|String|Required|The name of the zone. | Yes |
|`cidr`|String|Required|The CIDR block for the address prefix. | Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #address-prefix-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the address prefix.|
|`has_subnets`|Boolean|Indicates whether subnets exist with addresses from this prefix.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Import
{: #address-prefix-import}

The resource can be imported by using the VPC ID and VPC address prefix ID.

```
terraform import ibm_is_vpc_address_prefix.example <vpc_ID>/<address_prefix_ID>
```
{: pre}

## `ibm_is_vpc_route`
{: #vpc-route}

Create, update, or delete a VPC route. For more information, about VPC routes, see [Setting up advanced routing in VPC](/docs/vpc?topic=vpc-about-custom-routes).
{: shortdesc}

### Sample Terraform code
{: #vpc-route-sample}

```
resource "ibm_is_vpc" "myvpc" {
  name = "myvpc"
}

resource "ibm_is_vpc_route" "myroute" {
  name        = "routetest"
  vpc         = ibm_is_vpc.myvpc.id
  zone        = "us-south-1"
  destination = "192.168.4.0/24"
  next_hop    = "10.0.0.4"
}
```
{: codeblock}

### Input parameters
{: #vpc-route-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|Forces new resource |
|----|-----------|-----------|---------------------| ------ |
|`name`|String|Required|The name of the route that you want to create.| No |
|`vpc`|String|Required|The ID of the VPC where you want to create the route. |  Yes |
|`zone`|String|Required|The name of the VPC zone where you want to create the route.| Yes |
|`destination`|String|Required|The destination IP address or CIDR that network traffic from your VPC must match to be routed to the `next_hop`.| Yes |
|`next_hop`|String|Required|The IP address where network traffic is sent next.| No |

### Output parameters
{: #vpc-route-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the VPC route. The ID is composed of `<vpc_id>/<vpc_route_id>`.|
|`status`|String|The status of the VPC route.|

### Import
{: #vpc-route-import}

The resource can be imported by using the VPC and route IDs. 

```
terraform import ibm_is_vpc_route.example <vpc_ID>/<vpc_route_ID>
```
{: pre}

### Timeouts
{: #vpc-route-timeout}

The resource is set up with the following timeouts: 

- **create**: The creation of the route is considered `failed` when no response is received for 10 minutes. 
- **delete**: The deletion of the route is considered `failed` when no response is received for 10 minutes. 


## `ibm_is_vpc_routing_table`
{: #vpc-routing-table}

This resource allows VPC routing tables to create, update, or delete. For more information, about VPC routes, see [routing tables for VPC](/docs/vpc?topic=vpc-list-routing-tables-for-vpc).
{: shortdesc}

### Sample Terraform code
{: #vpc-routing-table-sample}

```
resource "ibm_is_vpc" "testacc_vpc" {
  name = "testvpc"
}
resource "ibm_is_vpc_routing_table" "test_ibm_is_vpc_routing_table" {
	vpc = ibm_is_vpc.testacc_vpc.id
	name = "routTabletest"
	route_direct_link_ingress = true
	route_transit_gateway_ingress = false
        route_vpc_zone_ingress = false
}
```
{: codeblock}

### Input parameters
{: #vpc-routing-table-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------ |
|`name`|String|Optional|The routing table name.| No |
|`route_direct_link_ingress`|Boolean|Optional| If set to `true`, the routing table is used to route traffic that originates from Direct Link to the VPC. To succeed, the VPC must not already have a routing table with the property set to `true`. | No |
|`route_transit_gateway_ingress`|Boolean|Optional|If set to `true`, the routing table is used to route traffic that originates from Transit Gateway to the VPC. To succeed, the VPC must not already have a routing table with the property set to `true`.| No |
|`route_vpc_zone_ingress`|Boolean|Optional|If set to true, the routing table is used to route traffic that originates from subnets in other zones in the VPC. To succeed, the VPC must not already have a routing table with the property set to `true`.| No |
|`vpc`|String|Required|The VPC ID. |  Yes |

### Output parameters
{: #vpc-routing-table-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`href`|String| The routing table URL.|
|`id`|String|The routing table ID. The ID is composed of `<vpc_id>/<vpc_route_table_id>` of the VPC route. |
|`is_default`|String| Indicates the default routing table for this VPC.|
|`lifecycle_state`|String| The lifecycle state of the routing table.|
|`resource_type`|String| The resource type.|
|`routing_table`|String|The generated routing table ID.|
|`routes`|String|The routes for the routing table.|
|`routes.id`|String| The unique ID of the route.|
|`routes.name`| String| The user-defined name of the route.|
|`subnets`|String| The subnets to which routing table is attached.|
|`subnets.id`|String| The unique ID of the subnet.|
|`subnets.name`|String| The user-defined name of the subnet.|


### Import
{: #vpc-routing-table-import}

The `ibm_is_vpc_routing_table` can be imported by using VPC ID and VPC Route table ID.

**Example**

```
terraform import ibm_is_vpc_routing_table.example 56738c92-4631-4eb5-8938-8af9211a6ea4/fc2667e0-9e6f-4993-a0fd-cabab477c4d1
```
{: pre}


## `ibm_is_vpc_routing_table_route`
{: #vpc-routing-table-route}

This resource allows VPC routing tables to create, update, or delete. For more information, about VPC routes, see [about routing tables and routes](/docs/vpc?topic=vpc-about-custom-routes).
{: shortdesc}


### Sample Terraform code
{: #vpc-routing-table-route-sample}

```
resource "ibm_is_vpc_routing_table_route" "test_ibm_is_vpc_routing_table_route" {
  vpc = ""
  routing_table = ""
  zone = "us-south-1"
  name = "custom-route-2"
  destination = "192.168.4.0/24"
  action = "deliver"
  next_hop    = "10.0.0.4"
}
```
{: codeblock}

### Input parameters
{: #vpc-routing-table-route-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------ |
|`action`|String|Optional|The action to perform with a packet matching the route. The default value is `deliver`. The supported values are `delegate`, `deliver`, and `drop`| No |
|`destination`|String|Required| The destination of the route. |  Yes |
|`name`|String|Optional|The user-defined name of the route. If unspecified, the name will be a hyphenated list of randomly selected words. You need to provide unique name within the VPC routing table the route resides in.| No |
|`next_hop`|String|Required| The next hop of the route. |  Yes |
|`routing_table`|String|Required|The routing table ID.| No |
|`vpc`|String|Required| The VPC ID.| Yes |
|`zone`|String|Required| Name of the zone. |  Yes |

### Output parameters
{: #vpc-routing-table-route-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`href`|String| The routing table URL.|
|`id`|String|The routing table ID. The ID is composed of `<vpc_route_table_id>/<vpc_route_table_route_id>`. |
|`is_default`|String| Indicates the default routing table for this VPC.|
|`lifecycle_state`|String| The lifecycle state of the route.|
|`resource_type`|String| The resource type.|

### Import
{: #vpc-routing-table-route-import}

The `ibm_is_vpc_routing_table_route` can be imported by using VPC ID, VPC Route table ID, and VPC Route table Route ID.

**Example**

```
terraform import ibm_is_vpc_routing_table_route.example 56738c92-4631-4eb5-8938-8af9211a6ea4/4993-a0fd-cabab477c4d1-8af9211a6ea4/fc2667e0-9e6f-4993-a0fd-cabab477c4d1
```
{: pre}

## `ibm_is_vpn_gateway`
{: #vpn-gateway}

Create, update, or delete a VPC gateway. 
{: shortdesc}

### Sample Terraform code
{: #vpn-gateway-sample}

```
resource "ibm_is_vpn_gateway" "testacc_vpn_gateway" {
  name   = "test"
  subnet = "a1aa111a-a11a-1111-11aa-111a1aa1aaa1"
}
```
{: codeblock}

### Input parameters
{: #vpn-gateway-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------ |
|`name`|String|Required|The name of the VPN gateway.| No |
|`subnet`|String|Required|The unique identifier for this subnet.| Yes |
|`resource_group`|String|Optional| The resource group where the VPN gateway to be created.| Yes |
|`tags`|List of strings|Optional|A list of tags that you want to add to your VPN gateway. Tags can help you find your VPN gateway more easily later.| No |

### Output parameters
{: #vpn-gateway-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the VPN gateway.|
|`status`|String|The status of VPN gateway.|
|`public_ip_address`|String|The IP address assigned to this VPN gateway.|

### Import
{: #vpn-gateway-import}

`ibm_is_vpn_gateway` can be imported by using the VPN gateway ID. 

```
terraform import ibm_is_vpn_gateway.example <vpn_gateway_ID>
```
{: pre}

### Timeouts
{: #vpn-gateway-timeout}

The following timeouts are specified for this resource: 

- **create**: The creation of the VPN gateway is considered `failed` when no response is received for 10 minutes. 
- **delete**: The deletion of the VPN gateway is considered `failed` when no response is received for 10 minutes. 

## `ibm_is_vpn_gateway_connection`
{: #vpn-gateway-connection}

Create, update, or delete a VPN gateway connection. For more information, about VPN gateway, see [adding connections to a VPN gateway](/docs/vpc?topic=vpc-vpn-adding-connections).
{: shortdesc}

### Sample Terraform code
{: #vpn-gateway-connection-sample}

```
resource "ibm_is_vpn_gateway_connection" "VPNGatewayConnection" {
  name          = "test2"
  vpn_gateway   = ibm_is_vpn_gateway.testacc_VPNGateway2.id
  peer_address  = ibm_is_vpn_gateway.testacc_VPNGateway2.public_ip_address
  preshared_key = "VPNDemoPassword"
  local_cidrs = [ibm_is_subnet.testacc_subnet2.ipv4_cidr_block]
  peer_cidrs = [ibm_is_subnet.testacc_subnet1.ipv4_cidr_block]
}
```
{: codeblock}

### Input parameters
{: #vpn-gateway-connection-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|Forces new resource |
|----|-----------|-----------|---------------------|----------|
|`name`|String|Required|The name of the VPN gateway connection.| No |
|`vpn_gateway`|String|Required| The unique identifier of the VPN gateway.| Yes |
|`peer_address`|String|Required|The IP address of the peer VPN gateway.| No |
|`preshared_key`|String|Required| The preshared key.| Yes |
|`local_cidrs`|Array|Optional|List of local CIDRs for this resource.| Yes |
|`peer_cidrs`|Array|Optional|List of peer CIDRs for this resource.| Yes |
|`admin_state_up`|Boolean|Optional|The VPN gateway connection status. Default false. If set to false, the VPN gateway connection is shut down.| No |
|`action`|String|Optional| Dead peer detection actions. Supported values are `restart`, `clear`, `hold`, `none`. Default: `none`.| No |
|`interval`|Integer|Optional| Dead peer detection interval in seconds. Default 30.| No |
|`timeout`|Integer|Optional| Dead peer detection timeout in seconds. Default 120.| No |
|`ike_policy`|String|Optional|The ID of the IKE policy.| No |
|`ipsec_policy`|String|Optional| The ID of the IPSec policy.| No |

### Output parameters
{: #vpn-gateway-connection-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the VPN gateway connection. The ID is composed of `<vpn_gateway_id>/<vpn_gateway_connection_id>`.|
|`authentication_mode`|String|The authentication mode, only `psk` is supported now.|
|`created_at`| String | The date and time that VPN gateway connection was created.|
|`resource_type`| String | The resource type (vpn_gateway_connection). |
|`status`| String | The status of a VPN gateway connection either `down` or `up`.|
|`tunnels`| String | The VPN tunnel configuration for the VPN gateway connection (in static route mode).|
|`tunnels.address`| String | The IP address of the VPN gateway member in which the tunnel resides.|
|`tunnels.resource_type`| String | The status of the VPN tunnel.|
|`crn` |String| The `VPN Gateway info(ID)`.|
|`mode`| String |The mode of the `VPN gateway(policy,route)`.|


### Import
{: #vpn-gateway-connection-import}

`ibm_is_vpn_gateway_connection` can be imported by using the VPN gateway ID and the VPN gateway connection ID. 

**Syntax**

```
terraform import ibm_is_vpn_gateway_connection.example <vpn_gateway_ID>/<vpn_gateway_connection_ID>
```
{: pre}

**Example**

```
terraform import ibm_is_vpn_gateway_connection.example d7bec597-4726-451f-8a63-e62e6f19c32c/cea6651a-bc0a-4438-9t8a-a0770bbf3ebb
```
{: pre}


### Timeouts
{: #vpn-gateway-connection-timeout}

`ibm_is_vpn_gateway_connection` provides the following Timeouts:

- **delete** - (Default 10 minutes) Used for deleting Instance.




