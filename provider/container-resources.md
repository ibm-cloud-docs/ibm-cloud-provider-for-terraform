---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-16" 

keywords: terraform provider plugin, terraform kubernetes service, terraform container service, terraform cluster, terraform worker nodes, terraform iks, terraform kubernetes, observability logging, observability monitoring

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



# Kubernetes Service resources
{: #container-resources}

Create, modify, or delete [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-iks-overview) resources. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_container_addons`
{: #container-addons}

Enable, update or disable a single add-on or a set of add-ons. For more information, see [Cluster addons](/docs/containers?topic=containers-api-at-iam#ks-cluster).
{: shortdesc}

### Sample Terraform code
{: #container-addon-sample}

```
resource "ibm_container_addons" "addons" {
  cluster = ibm_container_vpc_cluster.cluster.name
  addons {
    name    = "istio"
    version = "1.7"
  }
  addons {
    name    = "kube-terminal"
    version = "1.0.0"
  }
  addons {
    name    = "alb-oauth-proxy"
    version = "1.0.0"
  }
  addons {
    name    = "debug-tool"
    version = "2.0.0"
  }
  addons {
    name    = "knative"
    version = "0.17.0"
  }
  addons {
    name    = "static-route"
    version = "1.0.0"
  }
  addons {
    name    = "vpc-block-csi-driver"
    version = "2.0.3"
  }
  addons {
    name    = "cluster-autoscaler"
    version = "1.0.1"
  }
}

```
{: codeblock}

### Input parameters
{: #container-addons-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `addons` | Set | Required | Set of add-ons that needs to be enabled. |No|
| `addons.name` | String | Optional | The add-on name such as `istio`. Supported add-ons are `kube-terminal`, `alb-oauth-proxy`, `debug-tool`, `istio`, `knative`, `static-route`,`vpc-block-csi-driver`.| No |
| `addons.version`| String | Optional | The add-on version. Omit the version that you want to use as the default version.This is required when you want to update the add-on to specified version. |No|
| `cluster` | String | Required | The name or ID of the cluster. |No|
| `resource_group_id` | String | Optional | The ID of the resource group. You can retrieve the value from data source ibm_resource_group. If not provided defaults to default resource group.|Yes|

### Output parameters
{: #container-addons-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `addons` | String | The details of an enabled add-ons. |
| `addons.allowed_upgrade_versions` | String | The versions that the add-on is upgraded to.|
| `addons.deprecated` | String | Determines if the add-on version is deprecated.|
| `addons.health_state` | String | The health state of an add-on, such as critical or pending. |
| `addons.health_status` | String | The health status of an add-on, provides a description of the state in the form of error message.|
| `addons.min_kube_version` | String | The minimum Kubernetes version of the add-on. |
| `addons.min_ocp_version` | String | The minimum OpenShift version of the add-on. |
| `addons.supported_kube_range` | String | The supported Kubernetes version range of the add-on. |
| `addons.target_version`| String | The add-on target version. |
| `addons.vlan_spanning_required`| String | The VLAN spanning required for multi-zone clusters.|
| `id` | String | The Id of the add-ons. |


### Timeouts
{: #container-addon-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **Create** The enablement of the add-ons is considered `failed` if no response is received for 20 minutes.
* **Update** The enablement of the add-ons is considered `failed` if no response is received for 20 minutes.

## `ibm_container_alb`
{: #container-alb}

Enable or disable an Ingres application load balancer (ALB) that is set up in your cluster. ALBs are used to set up HTTP or HTTPS load-balancing for containerized apps that are deployed into an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster. 
{: shortdesc}

For more information, about Ingress ALBs, see [About Ingress ALBs](/docs/containers?topic=containers-ingress-about). 

### Sample Terraform code
{: #container-alb-sample}

```
resource ibm_container_alb alb {
  alb_id = "public-cr083d810e501d4c73b42184eab5a7ad56-alb"
  enable = true
}

```
{: codeblock}

### Input parameters
{: #container-alb-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | -------- |
| `alb_id` | String | Required | The unique identifier of the ALB. To retrieve the ID, run `ibmcloud ks alb ls`.  | Yes |
| `disable_deployment` | Boolean | Optional | If set to **true**, the default Ingress ALB in your cluster is disabled. If set to **false**, the default Ingress ALB is enabled in your cluster and configured with the IBM-provided Ingress subdomain. If you do not specify this option, you must specify the `enable` parameter. | Yes |
| `enable` | Boolean | Optional | If set to **true**, the default Ingress ALB in your cluster is enabled and configured with the IBM-provided Ingress subdomain. If set to **false**, the default Ingress ALB is disabled in your cluster. If you do not specify this option, you must specify the `disable_deployment` parameter.  | No |
| `region` | String | Optional | The region where the Ingress ALB is provisioned. | Yes |
| `user_ip` | String | Optional | For a private ALB only. The private ALB is deployed with an IP address from a user-provided private subnet. If no IP address is provided, the ALB is deployed with a random IP address from a private subnet in the {{site.data.keyword.cloud_notm}} account. | Yes |

### Output parameters
{: #container-alb-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `alb_type` | String | The type of the ALB. Supported values are `public` and `private`. |
| `cluster` | String | The name of the cluster where the ALB is provisioned. |
| `id` | String | The unique identifier of the ALB. | 
| `name` | String|The name of the ALB. |

### Timeouts
{: #container-alb-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **Create**: The enablement of the ALB is considered `failed` if no response is received for 5 minutes.  


## `ibm_container_alb_cert`
{: #container-alb-cert}

Create, update, or delete an SSL certificate that you store in {{site.data.keyword.cloudcerts_long_notm}} for an Ingress application load balancer (ALB). 
{: shortdesc}

### Sample Terraform code
{: #container-alb-cert-sample}

The following example adds an SSL certificate that is stored in {{site.data.keyword.cloudcerts_long_notm}} to an Ingress ALB that is set up in a cluster that is named `myCluster`. 

```
resource ibm_container_alb_cert cert {
  cert_crn    = "crn:v1:bluemix:public:cloudcerts:us-south:a/e9021a4dc47e3d:faadea8e-a7f4-408f-8b39-2175ed17ae62:certificate:3f2ab474fbbf9564582"
  secret_name = "test-sec"
  cluster_id     = "<cluster_ID>"
}

```
{: codeblock}

### Input parameters
{: #container-alb-cert-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Force new resource |
| ------------- |-------------| ----- | -------------- | ------ |
| `cert_crn` | String | Required | The CRN of the certificate that you uploaded to {{site.data.keyword.cloudcerts_long_notm}}.| No |
| `cluster_id` | String | Required | The ID of the cluster that hosts the Ingress ALB that you want to configure for SSL traffic. | Yes |
| `region` | String | Optional | The {{site.data.keyword.cloud_notm}} region where your SSL certificate is stored. | No |
| `secret_name` | String | Required | The name of the ALB certificate secret. | Yes |
|`namespace`|String| Optional| The namespace in which the secret is created. Default value is `ibm-cert-store`.|
|`persistence`|Bool | Optional | Persist the secret data in your cluster. If the secret is later deleted from the command line or OpenShift web console, the secret is automatically re-created in your cluster. |

### Output parameters
{: #container-alb-cert-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `cluster_crn` | String | The CRN of the cluster that hosts the Ingress ALB. |
| `cloud_cert_instance_id` | String | The {{site.data.keyword.cloudcerts_long_notm}} instance ID from which the certificate was downloaded. |
| `domain_name` | String | The domain name of the certificate. |
| `expires_on` | Date | The date the certificate expires. |
| `id` | String | The unique identifier of the certificate in the format `<cluster_name_id>/<secret_name>`. |
| `issuer_name` | String | The name of the issuer of the certificate. | 
|`status`|String| The Status of the secret. |

### Import
{: #container-alb-cert-import}

ibm_container_alb_cert can be imported by using cluster_id, secret_name.

**Example**

```
$ terraform import ibm_container_alb_cert.example 166179849c9a469581f28939874d0c82/mysecret
```

### Timeouts
{: #container-alb-cert-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **Create**: The creation of the SSL certificate is considered `failed` if no response is received for 10 minutes.
* **Delete**: The deletion of the SSL certificate is considered `failed` if no response is received for 10 minutes.
* **Update**: The update of the SSL certificate is considered `failed` if no response is received for 10 minutes. 

## `ibm_container_api_key_reset`
{: #container-api-key-reset}

Create, update, or delete Kubernetes API key. For more information, about Kubernetes API key, see [Assigning cluster access](/docs/containers?topic=containers-users#access-checklist).
{: shortdesc}

### Sample Terraform code
{: #container-api-key-reset-sample}

The following example reset Kubernetes API key.

```
resource "ibm_container_api_key_reset" "reset" {
    region ="us-east"
    resource_group_id = "766f3584b2c840ee96d856bc04551da8"
    reset_api_key=2

}

```
{: codeblock}

### Input parameters
{: #container-api-key-reset-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Force new resource |
| ------------- |-------------| ----- | -------------- | ------ |
| `region` | String | Required | The region in which API key has to be reset.| Yes |
| `resource_group_id` | String | Optional | The ID of the resource group. You can retrieve the value from data source `ibm_resource_group`. If not provided defaults to default resource group. | Yes |
| `reset_api_key` | Integer | Optional | Determines the API key need reset or not. This attribute is added to avoid the state dependencies. You need to increment the attribute to reset the API key on same `region` and `resource_group_id`. The default value is `1`.| No |

### Output parameters
{: #container-api-key-reset-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The resource ID. ID is a combination of `<region>/<resource_group_id>`.|

## `ibm_container_bind_service`
{: #container-bind}

Bind an {{site.data.keyword.cloud_notm}} service to an {{site.data.keyword.containerlong_notm}} cluster. Service binding is a quick way to create service credentials for an IBM Cloud service by using its public service endpoint and storing these credentials in a Kubernetes secret in your cluster. The Kubernetes secret is automatically encrypted in etcd to protect your data.

To bind a service to your cluster, you must provision an instance of the service first.
{: note}

For more information, about service binding, see [Adding services by using {{site.data.keyword.cloud_notm}} service binding](/docs/containers?topic=containers-service-binding). 

### Sample Terraform code
{: #container-bind-sample}

The following example binds a service with the name `myservice` to a cluster with the name `mycluster`. 

```
resource "ibm_container_bind_service" "bind_service" {
  cluster_name_id             = "mycluster"
  service_instance_name       = "myservice"
  namespace_id                = "default"
}
```
{: codeblock}

### Input parameters
{: #container-bind-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------ |
| `cluster_name_id` | String | Required | The name or ID of the cluster to which you want to bind an {{site.data.keyword.cloud_notm}} service. To find the cluster name or ID, run `ibmcloud ks cluster ls`.  | Yes |
| `key` | String | Optional | The name of existing service credentials that you want to use for the service. If you do not provide this option, service credentials are automatically created as part of the service binding process. | Yes |
| `namespace_id` | String | Required | The Kubernetes namespace where you want to create the Kubernetes secret that holds the service credentials of the service that you want to bind to the cluster. | Yes |
| `resource_group_id` | String | Optional | The ID of the resource group where your {{site.data.keyword.cloud_notm}} service is provisioned into. To list resource groups, run `ibmcloud resource groups`. | Yes |
| `role` | String | Optional | The IAM service access role that you want to use to create the service credentials for the {{site.data.keyword.cloud_notm}} service instance. If you specified existing service credentials in the `key` parameter, settings for the `role` parameter are ignored. | Yes |
| `service_instance_id` | String | Optional | The ID of the service that you want to bind to the cluster. If you specify this parameter, do not specify `service_instance_name` at the same time. | Yes |
| `service_instance_name` | String | Optional | The name of the service that you want to bind to the cluster. If you specify this parameter, do not specify `service_instance_id` at the same time. | Yes |
| `tags` | Array of string | Optional | A list of tags that you want to associate with the {{site.data.keyword.cloud_notm}} service instance that you bind to the cluster. </br>**NOTE**: `Tags` are managed locally and are not stored on the {{site.data.keyword.cloud_notm}} service endpoint. | No |

### Output parameters
{: #container-bind-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The unique identifier of the service bind resource in your cluster in the format `<cluster_name_ID>/<service_instance_name>` or `<service_instance_id>/<namespace_id>`. |
| `namespace_id` | String | The namespace in your cluster where the Kubernetes secret is located that holds the credentials to access your {{site.data.keyword.cloud_notm}} service instance. |
| `secret_name` | String | The name of the Kubernetes secret that holds the credentials to access your {{site.data.keyword.cloud_notm}} service instance. |

### Import
{: #container-bind-import}

ibm_container_bind_service can be imported by using cluster_name_id, service_instance_name or service_instance_id and namespace_id, eg

```
$ terraform import ibm_container_bind_service.example mycluster/myservice/default
```


## `ibm_container_cluster`
{: #container-cluster}

Create, update, or delete an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} single zone cluster. Every cluster is set up with a worker pools that is named `default` and that holds worker nodes with the same configuration, such as machine type, CPU, and memory.
{: shortdesc}

If you want to use this resource to update a cluster, make sure that you review the [version changelog](/docs/containers?topic=containers-changelog) for patch updates and the [version information and update information](/docs/containers?topic=containers-cs_versions) for major and minor changes. 
{: important}

If you want to create a VPC cluster, make sure to include the VPC infrastructure generation in the `provider` block of your Terraform configuration file. If you do not set this value, the generation is automatically set to 2. For more information, about how to configure the `provider` block, see [Overview of required input parameters for each resource category](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters). 
{: important}

You cannot create a free cluster in {{site.data.keyword.bpfull_notm}}.
{: important}

To create a worker pool or add worker nodes and zones to a worker pool, use the `ibm_container_worker_pool` and `ibm_container_worker_pool_zone` resources. 
{: tip}

For step-by-step instructions for how to create an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster, see [Creating single and multizone Kubernetes and OpenShift clusters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-tutorial-tf-clusters). 
{: tip}

### Sample Terraform code
{: #container-cluster-sample}

#### Classic {{site.data.keyword.containerlong_notm}} cluster

The following example creates a single zone {{site.data.keyword.containerlong_notm}} cluster that is named `mycluster` with one worker node in the default worker pool. 
{: shortdesc}

```
resource "ibm_container_cluster" "testacc_cluster" {
  name            = "test"
  datacenter      = "dal10"
  machine_type    = "free"
  hardware        = "shared"
  public_vlan_id  = "vlan"
  private_vlan_id = "vlan"
  subnet_id       = ["1154643"]

  default_pool_size = 1

  webhook {
    level = "Normal"
    type  = "slack"
    url   = "https://hooks.slack.com/services/yt7rebjhgh2r4rd44fjk"
  }
}
```
{: codeblock}

#### Creating Kubernetes cluster

Create the Kubernetes cluster with a default worker pool with 2 workers and one stand-alone worker as mentioned by worker number.
{: shortdesc}

```
resource "ibm_container_cluster" "testacc_cluster" {
  name            = "test"
  datacenter      = "dal10"
  machine_type    = "free"
  hardware        = "shared"
  public_vlan_id  = "<public_vlan_ID>"
  private_vlan_id = "<private_vlan_ID>"
  subnet_id       = ["1154643"]

  default_pool_size = 2
  worker_num        = 1
  webhook {
    level = "Normal"
    type  = "slack"
    url   = "https://hooks.slack.com/services/yt7rebjhgh2r4rd44fjk"
  }
}
```
{: codeblock}

#### Create a gateway enabled Kubernetes cluster

```
resource "ibm_container_cluster" "testacc_cluster" {
  name            = "testgate"
  gateway_enabled = true
  datacenter      = "dal10"
  machine_type    = "b3c.4x16"
  hardware        = "shared"
  private_vlan_id = "<private_vlan_ID>"
  private_service_endpoint = true
  no_subnet = false
}
```
{: codeblock}

#### Creating a KMS enabled Kubernetes cluster

```
resource "ibm_container_cluster" "cluster" {
  name              = "myContainerClsuter"
  datacenter        = "dal10"
  no_subnet         = false
  default_pool_size = 2
  hardware          = "shared"
  resource_group_id = data.ibm_resource_group.testacc_ds_resource_group.id
  machine_type      = "b2c.16x64"
  public_vlan_id    = "<public_vlan_ID>"
  private_vlan_id   = "<private_vlan_ID>"
  kms_config {
    instance_id = "12043812-757f-4e1e-8436-6af3245e6a69"
    crk_id = "0792853c-b9f9-4b35-9d9e-ffceab51d3c1"
    private_endpoint = false
  }
}
```
{: codeblock}

#### Creating an {{site.data.keyword.openshiftlong_notm}} Cluster 

Create the {{site.data.keyword.openshiftlong_notm}} cluster with default worker pool entitlement.
```
resource "ibm_container_cluster" "cluster" {
  name              = "test-openshift-cluster"
  datacenter        = "dal10"
  default_pool_size = 3
  machine_type      = "b3c.4x16"
  hardware          = "shared"
  kube_version      = "4.3_openshift"
  public_vlan_id    = "<public_vlan_ID>"
  private_vlan_id   = "<private_vlan_ID>"
  entitlement = "cloud_pak"
}
```
{: codeblock}

#### Classic {{site.data.keyword.openshiftlong_notm}} cluster
```
resource "ibm_container_cluster" "cluster" {
  name              = "mycluster"
  datacenter        = "dal10"
  default_pool_size = 3
  machine_type      = "b3c.4x16"
  hardware          = "shared"
  kube_version      = "3.11_openshift"
  public_vlan_id    = "<public_vlan_ID>"
  private_vlan_id   = "<private_vlane_ID>"
  lifecycle {
    ignore_changes = ["kube_version"]
  }
}
```
{: codeblock}

#### Classic {{site.data.keyword.openshiftlong_notm}} cluster with existing OpenShift license

If you purchased an {{site.data.keyword.cloud_notm}} Cloud Pak that includes an entitlement to run worker nodes that are installed with OpenShift Container Platform, you can create your cluster with that entitlement to avoid being charged twice for the {{site.data.keyword.openshiftshort}} license.

```
resource "ibm_container_cluster" "cluster" {
  name              = "test-openshift-cluster"
  datacenter        = "dal10"
  default_pool_size = 3
  machine_type      = "b3c.4x16"
  hardware          = "shared"
  kube_version      = "4.3_openshift"
  public_vlan_id    = "2863614"
  private_vlan_id   = "2863616"
  entitlement = "cloud_pak"
}
```
{: codeblock}

#### VPC Gen 1 {{site.data.keyword.containerlong_notm}} cluster
{: #gen1-cluster}

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
  flavor            = "bc1-2x8"
  worker_count      = 3
  resource_group_id = data.ibm_resource_group.resource_group.id

  zones {
    subnet_id = ibm_is_subnet.subnet1.id
    name      = "us-south-1"
  }
}

resource "ibm_container_vpc_worker_pool" "cluster_pool" {
  cluster           = ibm_container_
  .cluster.id
  worker_pool_name  = "mywp"
  flavor            = "bc1-4x16"
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
{: #gen2-cluster}

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
  flavor            = "bx2-4x16"
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
  flavor            = "bx2-2x8"
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

### Input parameters
{: #container-cluster-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `datacenter` | String | Required | The datacenter where you want to provision the worker nodes. The zone that you choose must be supported in the region where you want to create the cluster. To find supported zones, run `ibmcloud ks zones`. | Yes |
| `default_pool_size` | Integer | Optional | The number of worker nodes that you want to add to the default worker pool. | No |
| `disk_encryption` | Boolean | Optional | If set to **true**, the worker node disks are set up with an AES 256-bit encryption. If set to **false**, the disk encryption for the worker node is disabled. For more information, see [Encrypted disks for worker node](/docs/containers?topic=containers-security#workernodes).| Yes |
| `entitlement`|String|Optional|If you purchased an {{site.data.keyword.cloud_notm}} Cloud Pak that includes an entitlement to run worker nodes that are installed with OpenShift Container Platform, enter `entitlement` to create your cluster with that entitlement so that you are not charged twice for the {{site.data.keyword.openshiftshort}} license. Note that this option can be set only when you create the cluster. After the cluster is created, the cost for the {{site.data.keyword.openshiftshort}} license occurred and you cannot disable this charge. | No |
| `force_delete_storage`|Boolean|Optional|If set to `true`,force the removal of persistent storage associated with the cluster during cluster deletion. Default value is `false`. **NOTE** If `force_delete_storage` parameter is used after provisioning the cluster, then, you need to execute `terraform apply` before `terraform destroy` for `force_delete_storage` parameter to take effect. | No |
| `hardware` | String | Optional | The level of hardware isolation for your worker node. Use `dedicated` to have available physical resources dedicated to you only, or `shared` to allow physical resources to be shared with other IBM customers. This option is available for virtual machine worker node flavors only. | Yes |
| `gateway_enabled`|Boolean|Optional|Set to **true** if you want to automatically create a gateway-enabled cluster. If `gateway_enabled` is set to **true**, then `private_service_endpoint` must be set to **true** at the same time.| No |
| `kms_config`|String|Optional|Used to attach a Key Protect instance to a cluster. Nested `kms_config` block have `instance_id`, `crk_id`, `private_endpoint` structure.| No |
| `kms_config.instance_id`|String|Optional|The GUID of the Key Protect instance.| No |
| `kms_config.crk_id`|String|Optional|The ID of the customer root key (CRK).| No |
| `kms_config.private_endpoint`|Boolean|Optional|Set to `true` to configure the KMS private service endpoint. Default value is `false`.| No |
| `kube_version` | String | Optional | The Kubernetes or OpenShift version that you want to set up in your cluster. If the version is not specified, the default version in [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-cs_versions) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-openshift_versions#version_types) is used. For example, to specify Kubernetes version 1.16, enter `1.16`. For OpenShift clusters, you can specify version `3.11_openshift` or `4.3.1_openshift`.| No |
|`labels`| Map| Optional| Labels on all the workers in the default worker pool.|No|
| `machine_type` | String | Optional | The machine type for your worker node. The machine type determines the amount of memory, CPU, and disk space that is available to the worker node. For an overview of supported machine types, see [Planning your worker node setup](/docs/containers?topic=containers-planning_worker_nodes). | Yes |
| `name` | String | Required | The name of the cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name. | Yes |
| `no_subnet` | Boolean | Optional | If set to **true**, no portable subnet is created during cluster creation. The portable subnet is used to provide portable IP addresses for the Ingress subdomain and Kubernetes load balancer services. If set to **false**, a portable subnet is created by default. The default is **false**. | Yes |
| `patch_version` | String | Optional | Updates the worker nodes with the required patch version. The patch_version should be in the format:  `patch_version_fixpack_version`. For more information, about Kubernetes version information and update, see [Kubernetes version update](/docs/containers?topic=containers-cs_versions). **NOTE:** To update the patch or fix pack versions of the worker nodes, run the command `ibmcloud ks workers -c <cluster_name_or_id> --output json`. Fetch the required patch & fix pack versions from `kubeVersion.target` and set the `patch_version` parameter.|No|
| `public_service_endpoint` | Boolean | Optional | If set to **true**, your cluster is set up with a public service endpoint. You can use the public service endpoint to access the Kubernetes master from the public network. To use service endpoints, your account must be enabled for [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf). For more information, see [Worker-to-master and user-to-master communication: Service endpoints](/docs/containers?topic=containers-plan_clusters#workeruser-master). If set to **false**, the public service endpoint is disabled for your cluster.  | Yes |
| `public_vlan_id` | String | Optional | The ID of the public VLAN that you want to use for your worker nodes. You can retrieve the VLAN ID with the `ibmcloud ks vlans --zone <zone>` command. </br></br> * **Free clusters**: If you want to provision a free cluster, you do not need to enter a public VLAN ID. Your cluster is automatically connected to a public VLAN that is owned by IBM. </br> * **Standard clusters**: If you create a standard cluster and you have an existing public VLAN ID for the zone where you plan to set up worker nodes, you must enter the VLAN ID. To retrieve the ID, run `ibmcloud ks vlans --zone <zone>`. If you do not have an existing public VLAN ID, or you want to connect your cluster to a private VLAN only, do not specify this option. | Yes |
| `private_service_endpoint` | Boolean | Optional | If set to **true**, your cluster is set up with a private service endpoint. When the private service endpoint is enabled, communication between the Kubernetes and the worker nodes is established over the private network. If you enable the private service endpoint, you cannot disable it later. To use service endpoints, your account must be enabled for [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf). For more information, see [Worker-to-master and user-to-master communication: Service endpoints](/docs/containers?topic=containers-plan_clusters#workeruser-master). If set to **false**, the private service endpoint is disabled and all communication to the Kubernetes master must go through the public network. | Yes |
| `private_vlan_id` | String | Optional | The ID of the private VLAN that you want to use for your worker nodes. You can retrieve the VLAN ID with the `ibmcloud ks vlans --zone <zone>` command. </br></br> * **Free clusters**: If you want to provision a free cluster, you do not need to enter a private VLAN ID. Your cluster is automatically connected to a private VLAN that is owned by IBM. </br> * **Standard clusters**: If you create a standard cluster and you have an existing private VLAN ID for the zone where you plan to set up worker nodes, you must enter the VLAN ID. To retrieve the ID, run `ibmcloud ks vlans --zone <zone>`. If you do not have an existing private VLAN ID, do not specify this option. A private VLAN is created automatically for you. | Yes |
|`pod_subnet`| String | Optional| Specify a custom subnet CIDR to provide private IP addresses for pods. The subnet must be at least `/23` or more. For more information, refer to [Pod subnet](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#pod-subnet).|Yes|
| `resource_group_id` | String | Optional | The ID of the resource group where you want to provision your cluster. To retrieve the ID, use the  `ibm_resource_group` data source. If no value is provided, the cluster is automatically provisioned into the `default` resource group. | No |
| `subnet_id` | String | Optional | The ID of an existing subnet that you want to use for your worker nodes. To find existing subnets, run `ibmcloud ks subnets`.| No |
|`service_subnet`| String | Optional| Specify a custom subnet CIDR to provide private IP addresses for services. The subnet should be at least `/24` or more. For more information, refer to [Subnet service](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#service-subnet).|Yes|
| `tags` | Array of string | Optional | A list of tags that you want to add to your cluster. Tags can help find a cluster more quickly.  | No |
| `update_all_workers` | Boolean | Optional | If set to **true**, the Kubernetes version of the worker nodes is updated along with the Kubernetes version of the cluster that you specify in `kube_version`. | No |
| `webhook` | Array of objects | Optional | The webhook that you want to add to the cluster. For available options, see the [`webhook create` command](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli). | No |
| `webhook.level` | String | Optional| Notification level, such as `Normal` or `Warning`. | Yes |
| `webhook.type` | String | Optional | The Webhook type. Currently, supported value is `slack`.| Yes |
| `webhook.url` | String | Optional |The URL for the webhook.| Yes|
| `workers_info` | Array of objects | Optional | The worker nodes that you want to update. | No |
| `workers_info.id` | String | Optional | The ID of the worker node that you want to update. | No |
| `workers_info.version` | String | Optional | The Kubernetes version that you want to update your worker nodes to. | No |
| `worker_num`| Integer|Optional|The number of worker nodes in your cluster. This attribute creates a worker node that is not associated with a worker pool.| No |
| `wait_for_worker_update` | Boolean | Optional | Set to `true` to wait and update the Kubernetes version of worker nodes. **NOTE** Setting wait_for_worker_update to `false` is not recommended. Setting `false` results in upgrading all the worker nodes in the cluster at the same time causing the cluster downtime. | No |
|`wait_till`|String|Optional| The cluster creation happens in multi-stages. To avoid the longer wait times for resource execution.This argument in the resource will wait for the specified stage and complete the execution. The default stage value is `IngressReady`. The supported stages are  `MasterNodeReady` Resource waits till the master node is ready.  `OneWorkerNodeReady` Resource waits till one worker node is in to ready state.  `IngressReady` Resource waits till the ingress-host and ingress-secret are available.|No|

**Note**

1. For users on account to add tags to a resource, you need to assign the right access. For more information, about tags, see [Tags permission](/docs/account?topic=account-access).
2. `wait_till` is set only for the first time creation of the resource, further modification are not impacted.


### Output parameters
{: #container-cluster-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `albs` | List of objects | A list of Ingress application load balancers (ALBs) that are attached to the cluster. |
| `albs.id` | String | The unique identifier of the Ingress ALB. |
| `albs.name` | String | The name of the Ingress ALB. |
| `albs.alb_type` | String | The type of ALB. Supported values are `public` and `private`. 
| `albs.enable` | Boolean | Indicates if the ALB is enabled (**true**) or disabled (**false**) in the cluster. |
| `albs.state` | String | The state of the ALB. Supported values are `enabled` or `disabled`. | 
| `albs.num_of_instances`| Integer | The number of ALB replicas. | 
| `albs.alb_ip` | String | The virtual IP address that you want to use for your application load balancer (ALB). Currently supported only for private application load balancer (ALB).| 
| `albs.resize` | Boolean |  Indicate whether resizing should be done. | 
| `albs.disable_deployment` | Boolean |  Indicate whether to disable deployment only on disable application load balancer (ALB).|
| `crn` | String | The CRN of the cluster. |
| `id` | String | The unique identifier of the cluster. |
| `ingress_hostname` | String | The Ingress host name. |
| `ingress_secret` | String | The name of the Ingress secret. |
| `name` | String | The name of the cluster. |
| `public_service_endpoint_url` | String | The URL of the public service endpoint for your cluster. |
| `private_service_endpoint_url` | String | The URL of the private service endpoint for your cluster.|
| `server_url` | String | The server URL. | 
| `subnet_id` | String | The subnets attached to this cluster. | 
| `workers` | List of objects | A list of worker nodes that belong to the cluster. | 
| `workers.pool_name` | String | The name of the worker pool the worker node belongs to. |
| `worker_pools` | List of objects | A list of worker pools that exist in the cluster.|
| `worker_pools.machine_type` | String | The machine type that is used for the worker nodes in the worker pool. |
| `worker_pools.name` | String | The name of the worker pool. |
| `worker_pools.size_per_zone` | Integer | The number of worker nodes per zone. |
| `worker_pools.hardware` | String | The level of hardware isolation that is used for the worker node of the worker pool.|
| `worker_pools.id` | String | The ID of the worker pool. |
| `worker_pools.state` | String | The state of the worker pool. |
| `worker_pools.labels` | List of strings | A list of labels that are added to the worker pool. |
| `worker_pools.zones` | List of objects | A list of zones that are attached to the worker pool. |
| `worker_pools.zones.zone` | String | The name of the zone. |
| `worker_pools.zones.private_vlan` | String | The ID of the private VLAN that is used in that zone. |
| `worker_pools.zones.public_vlan` | String | The ID of the private VLAN that is used in that zone. |
| `worker_pools.zones.worker_count` | Integer | The number of worker nodes that are attached to the zone. |
| `workers_info` | List of objects | A list of worker nodes that belong to the cluster. |
| `workers_info.pool_name` | String | The name of the worker pool the worker node belongs to. |

### Timeouts
{: #container-cluster-timeout}

The following timeouts configuration are defined for `ibm_container_alb` resource.
{: shortdesc}

* **Create** The enablement of the feature is considered `failed` if no response is received for 90 minutes.
* **Delete** The delete of the feature is considered `failed` if no response is received for 45 minutes.
* **Update** The update of the feature is considered `failed` if no response is received for 45 minutes.

## `ibm_container_cluster_feature`
{: #container-cluster-feature}

Enable or disable a feature in your {{site.data.keyword.containerlong_notm}} cluster. 
{: shortdesc}

Supported features include: 
- Public service endpoint
- Private service endpoint

### Sample Terraform code
{: #container-cluster-feature-sample}

The following example enables the private service endpoint feature for a cluster that is named `mycluster`. 

```
resource ibm_container_cluster_feature feature {
  cluster                 = "mycluster"
  private_service_endpoint = "true"
}

```
{: codeblock}

### Input parameters
{: #container-cluster-feature-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `cluster` | String | Required | The name or ID of the cluster for which you want to enable or disabled a feature. To find the name or ID, use the `ibmcloud ks cluster ls` command. | Yes |
| `public_service_endpoint` | Boolean | Optional | Enable(**true**) or disable (**false**) the public service endpoint for your cluster. You can use the public service endpoint to access the Kubernetes master from the public network. To use service endpoints, your account must be enabled for [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf). For more information, see [Worker-to-master and user-to-master communication: Service endpoints](/docs/containers?topic=containers-plan_clusters#workeruser-master). | No |
| `private_service_endpoint` | Boolean | Optional | Enable (**true**) or disable (**false**) the private service endpoint for your cluster. When the private service endpoint is enabled, communication between the Kubernetes and the worker nodes is established over the private network. If you enable the private service endpoint, you cannot disable it later. To use service endpoints, your account must be enabled for [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf). For more information, see [Worker-to-master and user-to-master communication: Service endpoints](/docs/containers?topic=containers-plan_clusters#workeruser-master). | No |
| `refresh_api_servers` | Boolean | Optional | If set to **true**, the Kubernetes master of the cluster is refreshed to apply the changes of your feature. If set to **false**, no refresh of the Kubernetes master is performed. | No |
| `reload_workers` | Boolean | Optional|If set to **true**, your worker nodes are reloaded after the feature is enabled. If set to **false**, no reload of the worker nodes is performed. | No |
| `resource_group_id` | String | Optional | The ID of the resource group that your cluster belongs to. You can retrieve the resource group by using the `ibm_resource_group` data source. | No |

### Output parameters
{: #container-cluster-feature-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The ID of the cluster feature. | 
| `public_service_endpoint_url` | String | The URL to the public service endpoint of your cluster. | 
| `private_service_endpoint_url` | String | The URL to the private service endpoint of your cluster. | 


### Timeouts
{: #container-cluster-feature-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **create**: The enablement of the feature is considered `failed` if no response is received for 90 minutes.
* **update**: The update of the feature is considered `failed` if no response is received for 90 minutes. 


## `ibm_ob_logging`
{: #observability-logging}


Create, update, or delete a logging instance. This resource creates a logging configuration for your cluster to automatically collect pod logs and send them to {{site.data.keyword.loganalysislong_notm}. For more information, about Observability plug-in, see [managing  Observability logging commands](/docs/containers?topic=containers-observability_cli).
{: shortdesc}

### Sample Terraform code
{: #observability-logging-sample}

The following example enables you to create a logging configuration. 

```
data "ibm_resource_group" "testacc_ds_resource_group" {
  name = "Default"
}

resource "ibm_container_cluster" "testacc_cluster" {
  name              = "TestCluster"
  datacenter        = "dal10"
  resource_group_id = data.ibm_resource_group.testacc_ds_resource_group.id
  default_pool_size = 1
  wait_till         = "MasterNodeReady"
  hardware          = "shared"
  machine_type      = "%s"
  timeouts {
    create = "720m"
    update = "720m"
  }
}

resource "ibm_resource_instance" "instance" {
  name     = "TestLogging"
  service  = "logdna"
  plan     = "7-day"
  location = "us-south"
}

resource "ibm_resource_key" "resourceKey" {
  name                 = "TestKey"
  resource_instance_id = ibm_resource_instance.instance.id
  role                 = "Manager"
}

resource "ibm_ob_logging" "test2" {
  depends_on  = [ibm_resource_key.resourceKey]
  cluster     = ibm_container_cluster.testacc_cluster.id
  instance_id = ibm_resource_instance.instance.guid
}

```
{: codeblock}

### Input parameters
{: #observability-logging-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | 
| ------------- |-------------| ----- | -------------- | 
| `cluster` | String | Required | The name or ID of the cluster.|
| `instance_id` | String | Required |  The GUID of the monitoring instance.|
| `logdna_ingestion_key` | String | Optional | The LogDNA ingestion key that you want to use for your configuration.|
| `private_endpoint` | String | Optional | Add this option to connect to your logging service instance through the private service endpoint.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #observability-logging-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The ID of the cluster feature. | 
| `public_service_endpoint_url` | String | The URL to the public service endpoint of your cluster. | 
| `private_service_endpoint_url` | String | The URL to the private service endpoint of your cluster. | 
| `id` | String | The unique identifier of the logging instance attach to cluster. The ID is composed of `<cluster_name_id>/< logging_instance_id>`.|
| `instance_name` | String | Name of the logging instance.|
| `agent_key` | String | The {{site.data.keyword.at_full_notm}} agent key.|
| `agent_namespace` | String | The {{site.data.keyword.at_full_notm}} agent namespace.|
| `daemonset_name` | String | The name of the `daemon` set.|
| `namespace` | String | The name of namespace.|
| `crn` | String | The CRN of the {{site.data.keyword.at_full_notm}} instance attach.|
{: caption="Table. Available output parameters" caption-side="top"}

### Import
{: #observability-logging-import}

`ibm_ob_logging` can be imported by using `cluster_name_id`, `logging_instance_id`.

```
terraform import ibm_ob_logging.example mycluster/5c4f4d06e0dc402084922dea70850e3b-7cafe35
```
{: codeblock}

### Timeouts
{: #observability-logging-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **create**: The enablement of the feature is considered `failed` if no response is received for 10 minutes.
* **delete**: The delete of the feature is considered `failed` if no response is received for 10 minutes. 
* **update**: The update of the feature is considered `failed` if no response is received for 10 minutes. 



## `ibm_ob_monitoring`
{: #observability-monitoring}


Create, update, or delete a monitoring instance. This resource creates a monitoring configuration for your {{site.data.keyword.containerlong_notm}} cluster to automatically collect pod metrics, and send these metrics to your monitoring service instance. For more information, about Observability monitoring, see [setting up loggin with {{site.data.keyword.loganalysislong_notm}}](docs/containers?topic=containers-istio-health).
{: shortdesc}

### Sample Terraform code
{: #observability-monitoring-sample}

The following example enables you to create a monitoring configuration. 

```
data "ibm_resource_group" "testacc_ds_resource_group" {
  name = "Default"
}

resource "ibm_container_cluster" "testacc_cluster" {
  name              = "TestCluster"
  datacenter        = "dal10"
  resource_group_id = data.ibm_resource_group.testacc_ds_resource_group.id
  default_pool_size = 1
  wait_till         = "MasterNodeReady"
  hardware          = "shared"
  machine_type      = "%s"
  timeouts {
    create = "720m"
    update = "720m"
  }
}

resource "ibm_resource_instance" "instance" {
  name     = "TestMonitoring"
  service  = "sysdig-monitor"
  plan     = "graduated-tier"
  location = "us-south"
}

resource "ibm_resource_key" "resourceKey" {
  name                 = "TestKey"
  resource_instance_id = ibm_resource_instance.instance.id
  role                 = "Manager"
}

resource "ibm_ob_monitoring" "test2" {
  depends_on  = [ibm_resource_key.resourceKey]
  cluster     = ibm_container_cluster.testacc_cluster.id
  instance_id = ibm_resource_instance.instance.guid
}
```
{: codeblock}

### Input parameters
{: #observability-monitoring-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | 
| ------------- |-------------| ----- | -------------- | 
| `cluster` | String | Required | The name or ID of the cluster.|
| `instance_id` | String | Required |  The GUID of the monitoring instance.|
| `logdna_ingestion_key` | String | Optional | The LogDNA ingestion key that you want to use for your configuration.|
| `private_endpoint` | String | Optional | Add this option to connect to your logging service instance through the private service endpoint.|
| `sysdig_access_key` | String | Optional | The monitoring ingestion key that you want to use for your configuration.|
| `private_endpoint`| String | Optional |  Add this option to connect to your monitoring service instance through the private service endpoint.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #observability-monitoring-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The unique identifier of the logging instance attach to cluster. The ID is composed of `<cluster_name_id>/< logging_instance_id>`.|
| `instance_name` | String | The name of the logging instance.|
| `agent_key` | String | The {{site.data.keyword.at_full_notm}} agent key.|
| `agent_namespace` | String | The {{site.data.keyword.at_full_notm}} agent namespace.|
| `discovered_agent` | String | The name of the discovered agent.|
| `namespace` | String | The name of namespace.|
| `crn` | String | The CRN of the instance attach.|
{: caption="Table. Available output parameters" caption-side="top"}

### Import
{: #observability-monitoring-import}

`ibm_ob_monitoring` can be imported by using `cluster_name_id`, `monitoring_instance_id`.

```
terraform import ibm_ob_monitoring.example mycluster/5c4f4d06e0dc402084922dea70850e3b-7cafe35
```
{: codeblock}

### Timeouts
{: #observability-monitoring-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

* **create**: The enablement of the feature is considered `failed` if no response is received for 10 minutes.
* **delete**: The delete of the feature is considered `failed` if no response is received for 10 minutes. 
* **update**: The update of the feature is considered `failed` if no response is received for 10 minutes. 


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
|`disable_public_service_endpoint`|Boolean|Optional|Disable the public service endpoint to prevent public access to the Kubernetes master. Default value is 'false’.| No |
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
|`tags`|Array of string|Optional|A list of tags that you want to associate with your VPC cluster. **Note**: For users on account to add tags to a resource, they must be assigned the [appropriate permissions]/docs/account?topic=account-access). | No |
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

