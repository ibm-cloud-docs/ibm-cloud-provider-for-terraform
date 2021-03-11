---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-11" 

keywords: terraform provider plugin, terraform container registry, container registry, container registry namespaces 

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



# Container Registry resources
{: #container-registry}


## `ibm_cr_namespace`
{: #cr-namespace}

Create, update, or delete a container registry namespace. For more information, about container registry, see [About IBM Cloud Container Registry](/docs/Registry?topic=Registry-registry_overview).
{: shortdesc}

### Sample Terraform code
{: #cr-namespace-sample}

The following example shows how to configure an `ALB`.
{: shortdesc}

```
resource "ibm_cr_namespace" "test" {
  name              = "test123"
  resource_group_id = "c34128405d5742549538xxx1237"
}
```
{: codeblock}

```
data "ibm_resource_group" "rg" {
  name = "default"
}
resource "ibm_cr_namespace" "rg_namespace" {
  name              = "testaasd2312"
  resource_group_id = data.ibm_resource_group.rg.id
}
```
{: codeblock}

### Input parameter
{: #cr-namespace-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `name` | String | Required | The name of the namespaces to create. | Yes |
| `resource_group_id` | String | Optional | The ID of the resource group to which the namespace is assigned. If not provided, default resource group ID will be assigned. | Yes |

### Output parameters
{: #cr-namespace-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The name of the namespace.| 
| `crn` | String | The `CRN` of the namespace.|
| `created_on` | String | The created time of the namespace.|
| `updated_on` | String | The updated time of the namespace.|

### Import
{: #cr-namespace-import}

The `ibm_cr_namespace` resource can be imported by using the ID. The ID is formed from the name (namespace name) `ID=name`.

**Syntax**

```
terraform import ibm_cr_namespace.test <name of the namespace>
```

**Example**

```
terraform import ibm_cr_namespace.test namespace-name
```

## `ibm_container_worker_pool`
{: #container-pool}

Create, update, or delete a worker pool.
{: shortdesc}

### Sample Terraform code
{: #container-pool-sample}

The following example creates the worker pool `mypool` for the cluster that is named `mycluster`. 
{: shortdesc}

#### Create a worker pool
```
resource "ibm_container_worker_pool" "testacc_workerpool" {
  worker_pool_name = "mypool"
  machine_type     = "u2c.2x4"
  cluster          = "mycluster"
  size_per_zone    = 1
  hardware         = "shared"
  disk_encryption  = "true"
  region           = "eu-de"

  labels {
    "test" = "test-pool"
  }

  //User can increase timeouts 
    timeouts {
      update = "180m"
    }
}
```
{: codeblock}

#### Create a worker pool with an existing OpenShift license
```
resource "ibm_container_worker_pool" "test_pool" {
  worker_pool_name = "test_openshift_wpool"
  machine_type     = "b3c.4x16"
  cluster          = "openshift_cluster_example"
  size_per_zone    = 3
  hardware         = "shared"
  disk_encryption  = "true"
  entitlement = "cloud_pak"

  labels = {
    "test" = "oc-pool"
  }
}
```
{: codeblock}

### Input parameter
{: #container-feature-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `cluster` | String | Required | The name or ID of the cluster where you want to enable or disable the feature. | Yes |
| `disk_encryption` | Boolean | Optional|If set to **true**, the worker node disks are set up with an AES 256-bit encryption. If set to **false**, the disk encryption for the worker node is disabled. For more information, see [Encrypted disks](/docs/containers?topic=containers-security).| Yes |
| `entitlement`|String|Optional|If you purchased an {{site.data.keyword.cloud_notm}} Cloud Pak that includes an entitlement to run worker nodes that are installed with OpenShift Container Platform, enter `entitlement` to create your worker pool with that entitlement so that you are not charged twice for the {{site.data.keyword.openshiftshort}} license. ** Note ** that this option can be set only when you create the worker pool. After the worker pool is created, the cost for the {{site.data.keyword.openshiftshort}} license automates when you add worker nodes to your worker pool. | No |
| `hardware` | String | Optional | The level of hardware isolation for your worker node. Use `dedicated` to have available physical resources dedicated to you only, or `shared` to allow physical resources to be shared with other IBM customers. This option is available for virtual machine worker node flavors only. | Yes |
| `labels` | Map | Optional | A list of labels that you want to add to your worker pool. The labels can help you find the worker pool more easily later. |  Yes |
| `machine_type` | String | Required | The machine type for your worker node. The machine type determines the amount of memory, CPU, and disk space that is available to the worker node. For an overview of supported machine types, see [Planning your worker node setup](/docs/containers?topic=containers-planning_worker_nodes). | Yes |
| `name` | String | Required | The name of the worker pool. | Yes |
| `resource_group_id` | String | Optional | The ID of the resource group where your cluster is provisioned into. To list resource groups, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. | Yes |
| `size_per_zone` | Integer | Required | The number of worker nodes per zone that you want to add to the worker pool. | No |

 
### Output parameters
{: #container-feature-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The unique identifier of the worker pool in the format `<cluster_name_id>/<worker_pool_id>`.| 
| `state` | String | The state of the worker pool. |
| `zones` | List | A list of zones that are attached to the worker pool. | 
| `zones.zone` | String | The name of the zone. | 
| `zones.private_vlan` | String | The ID of the private VLAN that is used in the zone. | 
| `zones.public_vlan` | String | The ID of the public VLAN that is used in the zone. | 
| `zones.worker_count` | Integer | The number of worker nodes that are attached to the zone.  | 

### Import
{: #container-feature-import}

ibm_container_worker_pool can be imported by using cluster_name_id, worker_pool_id eg

```
$ terraform import ibm_container_worker_pool.example mycluster/5c4f4d06e0dc402084922dea70850e3b-7cafe35
```

### Timeouts
{: #container-feature-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **Update**: The update of the worker pool is considered `failed` if no response is received for 90 minutes. 

## `ibm_container_worker_pool_zone_attachment`
{: #container-pool-zone}

Create, update, or delete a zone from a worker pool. 
{: shortdesc}

### Sample Terraform code
{: #container-pool-zone-sample}

The following example adds zone dal12 to a worker pool that is named `mypool` in the `mycluster` cluster. 
{: shortdesc}

```
resource "ibm_container_worker_pool" "test_pool" {
  worker_pool_name = "mypool"
  machine_type     = "u2c.2x4"
  cluster          = "mycluster"
  size_per_zone    = 2
  hardware         = "shared"
  disk_encryption  = "true"
  labels {
    "test" = "test-pool"

    "test1" = "test-pool1"
  }
}
resource "ibm_container_worker_pool_zone_attachment" "test_zone" {
  cluster         = "mycluster"
  worker_pool     = element(split("/",ibm_container_worker_pool.test_pool.id),1)
  zone            = "dal12"
  private_vlan_id = "2320267"
  public_vlan_id  = "2320265"

  //User can increase timeouts
  timeouts {
      create = "90m"
      update = "3h"
      delete = "30m"
    }
}

```
{: codeblock}

### Input parameter
{: #container-pool-zone-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | -------| 
| `cluster`| String | Required | The name or ID of the cluster that the worker pool belongs to. | Yes |
| `private_vlan_id` | String | Optional | The ID of the private VLAN that you want to use for the zone. To find available zones, run `ibmcloud ks vlans <zone>`. If you do not have a private VLAN for that zone, do not specify this option. A private VLAN is automatically created for you. |  No |
| `public_vlan_id` | String | Optional | The ID of the public VLAN that you want to use for the zone. To find available zones, run `ibmcloud ks vlans <zone>`.  If you do not have a public VLAN for that zone, do not specify this option. A public VLAN is automatically created for you.| No |
| `resource_group_id` | String | Optional | The ID of the resource group where your cluster is provisioned into. To list resource groups, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. | Yes |
|`wait_till_albs`|Boolean|Optional|When you add a zone to a worker pool, worker nodes are provisioned in that zone with the configuration that you defined in your worker pool. This process and enabling the ALBs on those worker nodes can take a few minutes to complete. To avoid long wait times when you run your Terraform code, you can specify the stage when you want Terraform to mark the zone attachment complete. Set to **true** to wait until all worker nodes are successfully provisioned in the zone that you added to your worker pool and all ALBs are available and healthy. If you want the worker node creation and ALB enablement to continue in the background, set this option to **false**. | No |
| `worker_pool` | String | Required | The name or ID of the worker pool to which you want to add a zone. | Yes |
| `zone` | String | Required | The name of the zone that you want to attach to the worker pool. To list available zones, run `ibmcloud ks zones`. | Yes |

### Output parameters
{: #container-pool-zone-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The unique identifier of the worker pool zone attachment in the format `<cluster_name_id>/< worker_pool_name_id>/<zone>`| 
| `worker_count` | Integer | The number of worker nodes that are attached to this zone.|

### Import
{: #container-pool-zone-import}

ibm_container_worker_pool_zone_attachment can be imported using cluster_name_id, worker_pool_name_id and zone, eg

```
terraform import ibm_container_worker_pool_zone_attachment.example mycluster/5c4f4d06e0dc402084922dea70850e3b-7cafe35/dal10
```

### Timeouts
{: #container-pool-zone-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **create**: The attachment of the zone is considered `failed` if no response is received for 90 minutes. 
* **update**: The update of the zone is considered `failed` if no response is received for 90 minutes. 
* **delete**: The detachment of the zone is considered `failed` if no response is received for 90 minutes. 

## `ibm_container_vpc_alb`
{: #vpc-alb}

Enable or disable an Application Load Balancer (ALB) for a VPC cluster. 
{: shortdesc}

### Sample Terraform code
{: #vpc-alb-sample}

The following example adds zone dal12 to a worker pool that is named `mypool` in the `mycluster` cluster. 
{: shortdesc}

```
resource "ibm_container_vpc_alb" "alb" {
  alb_id = "public-cr083d810e501d4c73b42184eab5a7ad56-alb"
  enable = true
}
```
{: codeblock}

### Import parameter
{: #vpc-alb-import}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
|`alb_id`|String|Required|The unique identifier of the application load balancer. | Yes |
|`enable`|Boolean|Optional|If set to **true**, the ALB in your cluster is enabled. If you set this option, do not specify `disable_deployment` at the same time.| No |
|`disable_deployment`|Boolean|Optional|Disable the ALB deployment only. If provided, the ALB deployment is deleted but the IBM-provided Ingress subdomain remains. If you set this option, do not specify `enable` at the same time. | No |

### Output parameter
{: #vpc-alb-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
|`alb_type`|String|The ALB type.|
|`cluster`|String| The name of the cluster.|
|`name`|String|The name of the ALB.|
|`id`|String|The ALB ID.|
|`load_balancer_hostname`|String|The host name of the ALB.|
|`resize`|Boolean|Resize of the ALB.|
|`state`|String|ALB state.|
|`status`|String| The status of ALB.|
|`zone`|String| The name of the zone.|


### Timeout
{: #vpc-alb-timeout}

The following timeouts are defined for this resource.

- **Create** The enablement or disablement of the ALB is considered failed when no response is received for 5 minutes. 
- **Update** The update of the ALB is considered failed when no response is received for 5 minutes. 


## `ibm_container_vpc_cluster`
{: #vpc-cluster}

Create, update, or delete a VPC cluster. 
{: shortdesc}

To create a VPC cluster, make sure to include the VPC infrastructure generation in the `provider` block of your Terraform configuration file. If you do not set this value, the generation is automatically set to 2. For more information, about how to configure the `provider` block, see [Overview of required input parameters for each resource category](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters). 
{: important}

You cannot create a free cluster in {{site.data.keyword.bpfull_notm}}.
{: important}

If you want to delete a VPC cluster and their associated load balancer. The following order is followed by the resource.
1. Invokes the cluster deletion.
2. Waits for the cluster deletion to complete.
3. Verifies for the load balancer that is associated with the cluster and waits for the associated load balancer to delete successfully.
{: important}

### Sample Terraform code
{: #vpc-cluster-sample}


#### VPC Gen 1 {{site.data.keyword.containerlong_notm}} cluster
{: #vpc-gen1}

The following example creates a VPC Gen 1 cluster that is spread across two zones.
{: shortdesc}

```
provider "ibm" {
  generation = 2
}

resource "ibm_is_vpc" "vpc1" {
  name = "myvpc"
}

resource "ibm_is_subnet" "subnet1" {
  name                     = "mysubnet1"
  vpc                      = ibm_is_vpc.vpc1.id
  zone                     = "us_south-1"
  total_ipv4_address_count = 256
}

resource "ibm_is_subnet" "subnet2" {
  name                     = "mysubnet2"
  vpc                      = ibm_is_vpc.vpc1.id
  zone                     = "us-south-2"
  total_ipv4_address_count = 256
}

data "ibm_resource_group" "resource_group" {
  name = var.resource_group
}

resource "ibm_container_vpc_cluster" "cluster" {
  name              = "mycluster"
  vpc_id            = ibm_is_vpc.vpc1.id
  flavor            = "bc1.2x8"
  worker_count      = 3
  resource_group_id = data.ibm_resource_group.resource_group.id

  zones {
    subnet_id = ibm_is_subnet.subnet1.id
    name      = "us-south-1"
  }
}

resource "ibm_container_vpc_worker_pool" "cluster_pool" {
  cluster           = ibm_container_vpc_cluster.cluster.id
  worker_pool_name  = "mywp"
  flavor            = "bc1.4x16"
  vpc_id            = ibm_is_vpc.vpc1.id
  worker_count      = 3
  resource_group_id = data.ibm_resource_group.resource_group.id
  zones {
    name      = "us-south-2"
    subnet_id = ibm_is_subnet.subnet2.id
  }
}
```
{: codeblock}

#### VPC Gen 2 {{site.data.keyword.containerlong_notm}} cluster
{: #vpc-gen2}

The following example creates a VPC Gen 2 cluster that is spread across two zones.
{: shortdesc}

```
provider "ibm" {
  generation = 2
}

resource "ibm_is_vpc" "vpc1" {
  name = "myvpc"
}

resource "ibm_is_subnet" "subnet1" {
  name                     = "mysubnet1"
  vpc                      = ibm_is_vpc.vpc1.id
  zone                     = "us_south-1"
  total_ipv4_address_count = 256
}

resource "ibm_is_subnet" "subnet2" {
  name                     = "mysubnet2"
  vpc                      = ibm_is_vpc.vpc1.id
  zone                     = "us-south-2"
  total_ipv4_address_count = 256
}

data "ibm_resource_group" "resource_group" {
  name = var.resource_group
}

resource "ibm_container_vpc_cluster" "cluster" {
  name              = "mycluster"
  vpc_id            = ibm_is_vpc.vpc1.id
  flavor            = "bx2.4x16"
  worker_count      = 3
  resource_group_id = data.ibm_resource_group.resource_group.id
  kube_version      = 1.17.5

  zones {
    subnet_id = ibm_is_subnet.subnet1.id
    name      = "us-south-1"
  }
}

resource "ibm_container_vpc_worker_pool" "cluster_pool" {
  cluster           = ibm_container_vpc_cluster.cluster.id
  worker_pool_name  = "mywp"
  flavor            = "bx2.2x8"
  vpc_id            = ibm_is_vpc.vpc1.id
  worker_count      = 3
  resource_group_id = data.ibm_resource_group.resource_group.id
  zones {
    name      = "us-south-2"
    subnet_id = ibm_is_subnet.subnet2.id
  }
}
```
{: codeblock}

#### VPC Gen 2 {{site.data.keyword.openshiftlong_notm}} cluster with existing OpenShift entitlement
{: #gen2-openshift}

```
provider "ibm" {
  generation = 2
}

resource "ibm_resource_instance" "cos_instance" {
  name     = "my_cos_instance"
  service  = "cloud-object-storage"
  plan     = "standard"
  location = "global"
}

resource "ibm_container_vpc_cluster" "cluster" {
  name              = "my_vpc_cluster"
  vpc_id            = "r006-abb7c7ea-aadf-41bd-94c5-b8521736fadf"
  kube_version 	    = "4.3_openshift"
	flavor            = "bx2.16x64"
  worker_count      = "2"
  entitlement       = "cloud_pak"
  cos_instance_crn  = ibm_resource_instance.cos_instance.id
  resource_group_id = "${data.ibm_resource_group.resource_group.id}"
  zones {
         subnet_id = "0717-0c0899ce-48ac-4eb6-892d-4e2e1ff8c9478"
         name = "us-south-1"
      }
  }
```
{: codeblock}



#### Creating a KMS enables Kubernetes cluster
{: #kms-enables-kubernetes}

```
resource "ibm_container_vpc_cluster" "cluster" {
  name              = "cluster2"
  vpc_id            = "${ibm_is_vpc.vpc1.id}"
  flavor            = "bx2.2x8"
  worker_count      = "1"
  wait_till         = "OneWorkerNodeReady"
  resource_group_id = "${data.ibm_resource_group.resource_group.id}"
  zones {
    subnet_id = "${ibm_is_subnet.subnet1.id}"
    name      = "us-south-1"
  }

  kms_config {
      instance_id = "12043812-757f-4e1e-8436-6af3245e6a69"
      crk_id = "0792853c-b9f9-4b35-9d9e-ffceab51d3c1"
      private_endpoint = false
  }
}
```
{: codeblock}


### Input parameters
{: #vpc-cluster-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
|`cos_instance_crn`|String|Optional|Required for OpenShift clusters only. The standard {{site.data.keyword.cos_full_notm}} instance CRN to back up the internal registry in your OpenShift on VPC Gen 2 cluster.| No |
|`disable_public_service_endpoint`|Boolean|Optional|Disable the public service endpoint to prevent public access to the Kubernetes master. Default value is 'true’.| No |
|`entitlement`|String|Optional|The {{site.data.keyword.openshiftshort}} cluster entitlement avoids the OCP license charges incurred. Use Cloud Pak with OCP Licence entitlement to create the {{site.data.keyword.openshiftshort}} cluster. **NOTE** <ul><li> It is set only the first time creation of the cluster, further modifications are not impacted. </li></ul> <ul><li> Set this argument to `cloud_pak` only if you use the cluster with a Cloud Pak that has an {{site.data.keyword.openshiftshort}} entitlement.</li></ul>| No |
| `force_delete_storage`|Boolean|Optional|If set to `true`,force the removal of persistent storage associated with the cluster during cluster deletion. Default value is `false`. **NOTE** If `force_delete_storage` parameter is used after provisioning the cluster, then, you need to execute `terraform apply` before `terraform destroy` for `force_delete_storage` parameter to take effect. | No |
|`flavor`|String|Required|The flavor of the VPC worker node that you want to use. | Yes |
|`name`|String|Required|The name of the cluster.| Yes |
|`kms_config`|String|Optional|Use to attach a Key Protect instance to a cluster. Nested `kms_config` block has an `instance_id`, `crk_id`, `private_endpoint`.| No |
|`kms_config.instance_id`|String|Optional|The GUID of the Key Protect instance.| No |
|`kms_config.crk_id`|String|Optional|The ID of the customer root key (CRK).| No |
|`kms_config.private_endpoint`|Boolean|Optional|Set `true` to configure the KMS private service endpoint. Default value is `false`.| No |
|`kube_version`|String|Optional| Specify the Kubernetes version, including the major.minor version. If you do not include this flag, the default version is used. To see available versions, run `ibmcloud ks versions`.| No |
| `patch_version` | String | Optional | Updates the worker nodes with the required patch version. The patch_version should be in the format:  `patch_version_fixpack_version`. For more information, about Kubernetes version information and update, see [Kubernetes version update](/docs/containers?topic=containers-cs_versions). **NOTE:** To update the patch or fix pack versions of the worker nodes, run the command `ibmcloud ks workers -c <cluster_name_or_id> --output json`. Fetch the required patch & fix pack versions from `kubeVersion.target` and set the `patch_version` parameter.|No|
|`pod_subnet`|String|Optional|Specify a custom subnet CIDR to provide private IP addresses for pods. The subnet must have a CIDR of at least `/23` or larger. For more information, see the [documentation](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_subnets). Default value is `172.30.0.0/16`.| Yes |
|`service_subnet`|String|Optional|Specify a custom subnet CIDR to provide private IP addresses for services. The subnet must be at least ’/24’ or larger. For more information, see the [documentation](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_messages). Default value is `172.21.0.0/16`.| Yes |
| `wait_for_worker_update` | Boolean | Optional | Set to `true` to wait and update the Kubernetes  version of worker nodes. **NOTE** Setting wait_for_worker_update to `false` is not recommended. Setting `false` results in upgrading all the worker nodes in the cluster at the same time causing the cluster downtime. | No |
|`wait_till`|String|Optional|The creation of a cluster can take a few minutes (for virtual servers) or even hours (for Bare Metal servers) to complete. To avoid long wait times when you run your Terraform code, you can specify the stage when you want Terraform to mark the cluster resource creation as completed. Depending on what stage you choose, the cluster creation might not be fully completed and continues to run in the background. However, your Terraform code can continue to run without waiting for the cluster to be fully created. Supported stages are: <ul><li><strong>`MasterNodeReady`</strong>: Terraform marks the creation of your cluster complete when the cluster master is in a <code>ready</code> state.</li><li><strong>`OneWorkerNodeReady`</strong>: Terraform marks the creation of your cluster complete when the master and at least one worker node are in a <code>ready</code> state.</li><li><strong>`IngressReady`</strong>: Terraform marks the creation of your cluster complete when the cluster master and all worker nodes are in a <code>ready</code> state, and the Ingress subdomain is fully set up.</li></ul> If you do not specify this option, <code>`IngressReady`</code> is used by default. You can set this option only when the cluster is created. If this option is set during a cluster update or deletion, the parameter is ignored by the Terraform provider. | No |
|`worker_count`|Integer|Optional| The number of worker nodes per zone in the default worker pool. Default value `1`.| Yes |
|`worker_labels`|Map|Optional| Labels on all the workers in the default worker pool.| No |
|`resource_group_id`|String|Optional|The ID of the resource group. You can retrieve the value by running `ibmcloud resource groups` or by using the `ibm_resource_group` data source. If no value is provided, the `default` resource group is used. | Yes |
|`tags`|Array of strings|Optional|A list of tags that you want to associate with your VPC cluster. **Note**: For users on account to add tags to a resource, they must be assigned the [appropriate permissions]/docs/account?topic=account-access). | No |
|`update_all_workers`|Boolean|Optional| Set to true, if you want to update workers Kubernetes version with the cluster kube_version.| No |
|`vpc_id`|String|Required|The ID of the VPC that you want to use for your cluster. To list available VPCs, run `ibmcloud is vpcs`. | Yes |
|`zones`|List|Required|A nested block describes the zones of this VPC cluster. | No |
|`zones.subnet_id`|String|Required|The VPC subnet to assign the cluster.| Yes |
|`zones.name`|String|Required|The name of the zone| Yes |

**Note**

1. For users on account to add tags to a resource, you need to assign the right access. For more information, about tags, see [Tags permission](/docs/account?topic=account-access).
2. `wait_till` is set only for the first time creation of the resource, further modification are not impacted.

### Output parameters
{: #vpc-cluster-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
|`id`|String|The ID of the VPC cluster. |
|`crn`|String|The CRN of the VPC cluster. |
|`ingress_hostname`|String|The hostname that was assigned to your Ingress subdomain.|
|`ingress_secret`|String|The name of the Ingress secret that was created for you and that the Ingress subdomain uses.|
|`master_status`|String|The status of the Kubernetes master. |
|`master_url`|String|The URL of the Kubernetes master. |
|`private_service_endpoint_url`|String|The private service endpoint URL.|
|`public_service_endpoint_url`|String| The public service endpoint URL.|
|`state`|String|The state of the VPC cluster. |
|`albs`|List of objects|A list of Application Load Balancers (ALBs) that are attached to the cluster. | 
|`albs.id`|String|The ID of the ALB. |
|`albs.name`|String|The name of the ALB.| 
|`albs.alb_type`|String|The ALB type. Valid values are `public` or `private`. |
|`albs.enable`|Boolean|Enable (true) or disable (false) the ALB. |
|`albs.state`|String| The status of the ALB. Valid values are `enabled` or `disabled`.|
|`albs.resize`|Boolean|Indicates whether resizing should be done.|
|`albs.disable_deployment`|Boolean|Indicate whether to disable the deployment of the ALB. |
|`albs.load_balancer_hostname`|String|The host name of the ALB.|

### Import
{: #vpc-cluster-import}

The VPC cluster can be imported by using the cluster ID. 

```
terraform import ibm_container_vpc_cluster.cluster aaaaaaaaa1a1a1a1aaa1a
```
{: pre}

## `ibm_container_vpc_worker_pool`
{: #vpc-worker-pool}

Create or delete a worker pool for a VPC cluster. 
{: shortdesc}

### Sample Terraform code
{: #vpc-worker-pool-sample}

```
resource "ibm_container_vpc_worker_pool" "test_pool" {
  cluster          = "my_vpc_cluster"
  worker_pool_name = "my_vpc_pool"
  flavor           = "c2.2x4"
  vpc_id           = "1111111a-1a11-1aa1-1111-11aa1aa1aa11"
  worker_count     = "1"

  zones {
    name      = "us-south-1"
    subnet_id = "111aaa1a-aaa1-1a11-1111-11111a11111a"
  }
}
```
{: codeblock}

### Input parameter
{: #vpc-worker-pool-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------------ |
|`worker_pool_name`|String|Required|The name of the worker pool.| Yes |
|`cluster`|String|Required|The name or ID of the cluster.| Yes |
|`vpc_id`|String|Required|The ID of the VPC.| Yes |
|`worker_count`|Integer|Required| The number of worker nodes per zone in the worker pool.| No |
|`flavor`|String|Required|The flavor of the worker node.| Yes |
|`zones`|List|Required|A nested block describes the zones of this worker pool. | No |
|`zones.subnet_id`|String|Required|The subnet that you want to use for your worker pool.| No |
|`zones.name`|String|Required|The name of the zone.| No |
|`labels`|Map|Optional|A list of labels that you want to add to all the worker nodes in the worker pool.| No |
|`resource_group_id`|String|Optional| The ID of the resource group. To retrieve the ID, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. If no value is provided, the `default` resource group is used. | Yes |
|`entitlement`| String | Optional | The {{site.data.keyword.openshiftshort}} cluster entitlement avoids incurred OCP license charges and use cloud pak with OCP license entitlement to add the {{site.data.keyword.openshiftshort}} cluster worker pool. **Note** <ul><li> It is set as one time creation of the worker pool. There is no impacts on any modification.</li><li> Set the argument to `entitlement` only when you use cluster with a cloud pak that has an {{site.data.keyword.openshiftshort}} entitlement </li></ul>| No |

### Output parameter
{: #vpc-worker-pool-output}


Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
|`id`|String| The unique identifier of the worker pool. The ID is composed of `<cluster_name_id>/<worker_pool_id>`.|

### Timeout
{: #vpc-worker-pool-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **Create** The creation of the worker pool is considered failed when no response is received for 90 minutes. 
- **Delete** The deletion of the worker pool is considered failed when no response is received for 90 minutes. 

### Import
{: #vpc-worker-pool-import}

The worker pool can be imported by using the cluster name or ID, and the ID of the worker pool. 

```
terraform import ibm_container_vpc_worker_pool.example <cluster_name_or_ID>/<worker_pool_ID>
```

