---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform create kubernetes cluster, terraform create openshift cluster, terraform kubernetes cluster, terraform openshift cluster, schematics create kubernetes cluster, schematics create openshift cluster, schematics kubernetes cluster, schematics openshift cluster, terraform iks cluster, terraform roks cluster, schematics iks cluster, schematics roks cluster, terraform multizone cluster, schematics multizone cluster, terraform remove default worker pool, schematics remove default worker pool 

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: containers, terraform, openshift
account-plan: 
completion-time: 2h

---

{[METADATA_ATTRIBUTES]}



# Creating single and multizone Kubernetes and OpenShift clusters
{: #tutorial-tf-clusters}
{: toc-content-type="tutorial"}
{: toc-services="containers, terraform, openshift"}
{: toc-completion-time="2h"}

Use this tutorial to create single and multizone clusters with [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-iks-overview) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-roks-overview), and deploy your own set of compute hosts in the public cloud where you can run and manage highly available containerized apps.

In this tutorial, you create a standard classic {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster with the following configuration:

- The cluster is created in the `us-south` region. 
- The cluster is created with the default worker pool.
- All worker nodes are connected to a private and public VLAN. These public and private VLANs assign public and private IP addresses to the worker nodes.
- All worker nodes are created with a virtual worker node flavor on shared hardware. If you want to use a different worker node flavor, see the [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-planning_worker_nodes) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-planning_worker_nodes) documentation.
- To allow access to your cluster from the internet and run public-facing app workloads in your cluster, the cluster is set up with both a public and a private service endpoint. For more information, about how network traffic flows when a public and a private service endpoint is enabled, see Worker-to-master and user-to-master communication: Service endpoints in [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-plan_clusters#workeruser-master) and [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-plan_clusters#workeruser-master). 

Keep in mind that creating a cluster incurs costs. Make sure to review [What am I charged for when I use {{site.data.keyword.containerlong_notm}}?](/docs/containers?topic=containers-faqs#charges) or [What am I charged for when I use {{site.data.keyword.openshiftlong_notm}}?](/docs/openshift?topic=openshift-faqs#charges) before you proceed.
{: note}

## Objectives
{: #cluster-tutorial-objectives}

In this tutorial, you will:
- Learn how to create a single zone {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster with Terraform.
- Convert your single zone cluster into a multizone cluster for higher availability.
- Add a new worker pool to the cluster.
- Remove the default worker pool that is automatically set up during cluster creation.

## Audience
{: #cluster-tutorial-audience}

This tutorial is intended for system administrators that want to learn how to create an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster and spread this cluster across zones.

## Prerequisites

- If you do not have one, create an [IBM Cloud Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration){: external}. 
- Install the [{{site.data.keyword.cloud_notm}} CLI and the {{site.data.keyword.containerlong_notm}} CLI plug-in](/docs/cli?topic=cli-getting-started).
- Follow the [instructions](/docs/containers?topic=containers-clusters#cluster_prepare) to make sure that you are assigned the required permissions in Identity and Access Management (IAM) to create clusters and that your account is enabled for Virtual Routing and Forwarding (VRF). 

## Lesson 1: Prepare your Terraform environment
{: #prepare-tf}

1. [Install the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_cli).
2. If you do not have one, [create an {{site.data.keyword.cloud_notm}} API key](/docs/account?topic=account-userapikey#create_user_key).
3. Create an Terraform project directory. The directory will hold all your Terraform configuration files that you create as part of this tutorial. The directory in this tutorial is named `tf-cluster`, but you can use any name for the directory.

   ``` 
   mkdir tf-cluster && cd tf-cluster
   ```
   {: pre}

4. In your project directory, create a `terraform.tfvars` file and add the {{site.data.keyword.cloud_notm}} API key that you created earlier. The `terraform.tfvars` file is an Terraform variables file that you store on your local machine. When you initialize the Terraform CLI, all variables that are defined in this file are automatically loaded into Terraform and you can reference them in every Terraform configuration file in the same project directory.

   ```
   ibmcloud_api_key = "<ibmcloud_api_key>"
   ```
   {: codeblock}
   
   The `terraform.tfvars` file includes credentials to authenticate with the {{site.data.keyword.cloud_notm}} platform. Keep the file on your local machine only and do not share these credentials with an unauthorized person.
   {: important}
   
5. In the same project directory, create a `provider.tf` file and configure IBM as your Terraform provider. To authenticate with {{site.data.keyword.cloud_notm}}, you must pass in your {{site.data.keyword.cloud_notm}} API key by using Terraform interpolation syntax.

   ```
   variable "ibmcloud_api_key" {}

   provider "ibm" {
     ibmcloud_api_key    = var.ibmcloud_api_key
   }
   ```
   {: codeblock}
   
Great! Now that you completed your Terraform setup, you can go ahead and add the code to create your {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster.


## Lesson 2: Create a single zone cluster
{: #create-cluster}

Create a classic {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster by using Terraform. 
{: shortdesc}
   
1. Create an Terraform configuration file for your single zone cluster. The following example creates a single zone cluster in the `dal10` zone with a default worker pool that consists of 3 worker nodes that are connected to a private and public VLAN in `dal10`.

   **Example for an {{site.data.keyword.containerlong_notm}} cluster**: 

   ```
   data ibm_resource_group "resource_group" {
     name = "default"
   }

   resource ibm_container_cluster "tfcluster" {
       name            = "tfcluster"
       datacenter      = "dal10"
       machine_type    = "b3c.4x16"
       hardware        = "shared"
       public_vlan_id  = "<public_vlan_ID_dal10>"
       private_vlan_id = "<private_vlan_ID_dal10>"

       kube_version = "1.17"

       default_pool_size = 3
         
       public_service_endpoint  = "true"
       private_service_endpoint = "true"

       resource_group_id = data.ibm_resource_group.resource_group.id
   }
   ```
   {: codeblock}
   
   **Example for an {{site.data.keyword.openshiftlong_notm}} cluster**:

   ```
   data "ibm_resource_group" "resource_group" {
     name = "default"
   }

   resource "ibm_container_cluster" "tfcluster" {
       name            = "tfcluster"
       datacenter      = "dal10"
       machine_type    = "b3c.4x16"
       hardware        = "shared"
       public_vlan_id  = "<public_vlan_ID_dal10>"
       private_vlan_id = "<private_vlan_ID_dal10>"

       kube_version = "3.11_openshift"

       default_pool_size = 3
         
       public_service_endpoint  = "true"
       private_service_endpoint = "true"

       resource_group_id = data.ibm_resource_group.resource_group.id
   }
   ```
   {: codeblock}
   
   <table>
   <caption>Understanding the configuration file</caption>
   <col style="width:30%">
	 <col style="width:70%">
   <thead>
     <th>Parameter</th>
     <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>data.ibm_resource_group.name</code></td>
   <td>Enter the name of the resource group where you want to create your cluster. The example in this tutorial uses the <code>default</code> resource group, but you can enter any other resource group in your account. To list available resource groups, run <code>ibmcloud resource groups</code>. The name of the resource group is used to retrieve the ID of the resource group that is required in <code>resource.ibm_container_cluster</code>. </td>
   </tr>
   <tr>
   <td><code>resource.ibm_container_cluster.name</code></td>
   <td>Enter a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name. </td>
   </tr>
   <tr>
   <td><code>resource.ibm_container_cluster.datacenter</code></td>
   <td>Enter the zone where you want to create your cluster. To convert your single zone cluster to a multizone cluster later, you must choose one of the multizone metro locations. The example in this tutorial uses <code>dal10</code> as one of the zones in the <code>us-south</code> metro location, but you can use a different multizone metro location as well. To list available zones, run <code>ibmcloud ks zones</code>.</td>
   </tr>
   <tr>
   <td><code>resource.ibm_container_cluster.machine_type</code></td>
   <td>Enter the flavor for your worker nodes that you want to add to your cluster. All worker nodes that you define here are automatically added to the default worker pool in your cluster. The example in this tutorial uses a virtual machine worker node. To list other supported flavors in your zone, run <code>ibmcloud ks flavors --zone &lt;zone&gt;</code>. For an overview of supported flavors and how they are provisioned, see the [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-planning_worker_nodes) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-planning_worker_nodes) documentation. </td>
   </tr>
    <tr>
   <td><code>resource.ibm_container_cluster.hardware</code></td>
     <td>Decide if you want to provision your virtual worker nodes on <code>shared</code> or <code>dedicated</code> hardware.  Shared hardware can be used for virtual worker nodes only. Bare Metal machines are always dedicated to you. For more information, about shared and dedicated hardware, see the [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-planning_worker_nodes#vm) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-planning_worker_nodes#vm) documentation.  </td>
   </tr>
    <tr>
   <td><code>resource.ibm_container_cluster.public_vlan_id</code></td>
     <td>Enter the ID of an existing public VLAN that you have in the zone where you want to create the cluster. If you do not have a public VLAN in that zone yet, remove this parameter from your configuration file. A public VLAN is automatically created for you. To list available VLANs in a zone, run <code>ibmcloud ks vlan ls --zone &lt;zone&gt;</code>. </td>
   </tr>
    <tr>
   <td><code>resource.ibm_container_cluster.private_vlan_id</code></td>
     <td>Enter the ID of an existing private VLAN that you have in the zone where you want to create the cluster. If you do not have a private VLAN in that zone yet, remove this parameter from your configuration file. A private VLAN is automatically created for you. To list available VLANs in a zone, run <code>ibmcloud ks vlan ls --zone &lt;zone&gt;</code>. </td>
   </tr>
    <tr>
   <td><code>resource.ibm_container_cluster.kube_version</code></td>
     <td>Enter the Kubernetes or OpenShift version that you want to install in your cluster. If the version is not specified, the default version in [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-cs_versions) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-openshift_versions#version_types) is used. </td>
   </tr>
    <tr>
   <td><code>resource.ibm_container_cluster.default_pool_size</code></td>
     <td>Enter the number of worker nodes that you want to create in the default worker pool. For a highly available setup, enter at least 3 worker nodes. </td>
   </tr>
    <tr>
      <td><code>resource.ibm_container_cluster.public_service_endpoint</code></br><code>resource.ibm_container_cluster.private_service_endpoint</code></td>
     <td>Enter <strong>true</strong> to enable the public and private service endpoint for your cluster. For more information, about how network traffic flows when the public and private service endpoints are enabled, see the [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-plan_clusters#workeruser-master) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-plan_clusters#workeruser-master) documentation.   </td>
   </tr> 
   <tr>
   <td><code>resource.ibm_container_cluster.resource_group_id</code></td>
     <td>Retrieve the ID of the resource group where you want to create your cluster from the <code>ibm_resource_group</code> data source that you defined in your configuration file.  </td>
   </tr> 
   </tbody>
   </table>
   
2. Initialize the Terraform CLI.

   ```
   terraform init
   ```
   {: pre}
   
3. Create an Terraform execution plan. When you execute this command, Terraform validates the syntax of your configuration file and resource definitions against the specifications of the {{site.data.keyword.cloud_notm}} Provider plug-in.

   ```
   terraform plan
   ```
   {: pre}
   
   Example output:

   ```
   Refreshing Terraform state in-memory prior to plan...
   The refreshed state will be used to calculate this plan, but will not be
   persisted to local or remote state storage.

   data.ibm_resource_group.resource_group: Refreshing state...

   ------------------------------------------------------------------------

   An execution plan has been generated and is shown.
   Resource actions are indicated with the following symbols:
     + create

   Terraform will perform the following actions:

     # ibm_container_cluster.tfcluster will be created
     + resource "ibm_container_cluster" "tfcluster" {
         + albs                         = (known after apply)
         + crn                          = (known after apply)
         + datacenter                   = "dal10"
         + default_pool_size            = 3
         + disk_encryption              = true
         + gateway_enabled              = false
      ....

   Plan: 1 to add, 0 to change, 0 to destroy.
   ```
   {: screen}
   
4. Review the Terraform execution plan to verify that your cluster setup is correct.
5. Create your single zone cluster. Note that the creation of your cluster takes a few minutes to complete.

   ```
   terraform apply
   ```
   {: pre}
   
   Example output: 

   ```
   ...
   ibm_container_cluster.tfcluster: Creating...
   ibm_container_cluster.tfcluster: Still creating... [10s elapsed]
   ibm_container_cluster.tfcluster: Still creating... [20s elapsed]
   ibm_container_cluster.tfcluster: Still creating... [30s elapsed]
   ....
   ibm_container_cluster.tfcluster: Still creating... [20m21s elapsed]
   ibm_container_cluster.tfcluster: Creation complete after 20m27s [id=bpugrqtd0ejuoqvinshg]

   Apply complete! Resources: 1 added, 0 changed, 1 destroyed.
   ```
   {: screen}
   
6. Optional: Review your cluster from the CLI. 

   **Example for {{site.data.keyword.containerlong_notm}}:**</br>

   ```
   ibmcloud ks cluster get --cluster tfcluster
   ```
   {: pre}
   
   **Example for {{site.data.keyword.openshiftlong_notm}}:**</br>

   ```
   ibmcloud oc cluster get --cluster tfcluster
   ```
   {: pre}
   
</br>
   
You have now completed the tutorial! You created your single zone {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster. 
 
## Lesson 3: Convert your single zone cluster into a multizone cluster
{: #multizone}
 
Add zones to the default worker pool in your cluster that you created in lesson 1. By adding zones, the same number of worker nodes that you created in lesson 2 are spread across these zones converting your single zone cluster into a multizone cluster. 
{: shortdesc}

1. Open your Terraform configuration file and add the following content to your configuration. For each zone that you want to add, you must add a separate `ibm_container_worker_pool_zone_attachment` resource.

   ```
   resource "ibm_container_worker_pool_zone_attachment" "dal12" {
    cluster         = ibm_container_cluster.tfcluster.id
    worker_pool     = ibm_container_cluster.tfcluster.worker_pools.0.id
    zone            = "dal12"
    private_vlan_id = "<private_vlan_ID_dal12>"
    public_vlan_id  = "<public_vlan_ID_dal12>"
    resource_group_id = data.ibm_resource_group.resource_group.id
   }
   
   resource "ibm_container_worker_pool_zone_attachment" "dal13" {
    cluster         = ibm_container_cluster.tfcluster.id
    worker_pool     = ibm_container_cluster.tfcluster.worker_pools.0.id
    zone            = "dal13"
    private_vlan_id = "<private_vlan_ID_dal13>"
    public_vlan_id  = "<public_vlan_ID_dal13>"
    resource_group_id = data.ibm_resource_group.resource_group.id
   }
   ```
   {: codeblock}
   
   <table>
   <caption>Understanding the configuration file</caption>
   <col style="width:30%">
	 <col style="width:70%">
   <thead>
     <th>Parameter</th>
     <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>resource.ibm_container_worker_pool_zone_attachment.cluster</code></td>
   <td>Enter the name or ID of the cluster where you want to add zones. The example in this tutorial references the cluster that you created in lesson 3. Terraform automatically retrieves the ID of the cluster. </td>
   </tr>
     <tr>
   <td><code>resource.ibm_container_worker_pool_zone_attachment.worker_pool</code></td>
   <td>Enter the ID of the worker pool where you want to add the zone. The example in this tutorial retrieves the list of worker pools of the cluster and gets the ID of the default worker pool. The default worker pool represents position 0 in the list of worker pools. </td>
   </tr>
    <tr>
   <td><code>resource.ibm_container_worker_pool_zone_attachment.zone</code></td>
   <td>Enter the zone that you want to add to the cluster. The zone must be in the same multizone metro location that you chose when you created the cluster. To list available zones, run <code>ibmcloud ks zones</code>. </td>
   </tr>
   <tr>
   <td><code>resource.ibm_container_worker_pool_zone_attachment.private_vlan_id</code></td>
   <td>Enter the ID of an existing private VLAN that you have in the zone that you want to add to the cluster. If you do not have a private VLAN in that zone yet, remove this parameter from your configuration file. A private VLAN is automatically created for you. To list available VLANs in a zone, run <code>ibmcloud ks vlan ls --zone &lt;zone&gt;</code>. </td>
   </tr>
     <tr>
   <td><code>resource.ibm_container_worker_pool_zone_attachment.public_vlan_id</code></td>
   <td>Enter the ID of an existing public VLAN that you have in the zone that you want to add to the cluster. If you do not have a public VLAN in that zone yet, remove this parameter from your configuration file. A public VLAN is automatically created for you. To list available VLANs in a zone, run <code>ibmcloud ks vlan ls --zone &lt;zone&gt;</code>. </td>
   </tr>
  </tbody>
  </table>
  
2. Create an Terraform execution plan and review the action Terraform is about to perform.

   ```
   terraform plan
   ```
   {: pre}
   
   Example output:

   ```
   data.ibm_resource_group.resource_group: Refreshing state...
   ibm_container_cluster.tfcluster: Refreshing state... [id=aaaaaaa1aaaaaaaaaaa]

   ------------------------------------------------------------------------

   An execution plan has been generated and is shown.
   Resource actions are indicated with the following symbols:
     + create

   Terraform will perform the following actions:

     # ibm_container_worker_pool_zone_attachment.dal12 will be created
     + resource "ibm_container_worker_pool_zone_attachment" "dal12" {
         + cluster         = "aaaaaaa1aaaaaaaaaaa"
         + id              = (known after apply)
         + private_vlan_id = "123456"
         + public_vlan_id  = "654321"
         + region          = (known after apply)
         + worker_count    = (known after apply)
         + worker_pool     = "bpugrqtd0ejuoqvinshg-6a55017"
         + zone            = "dal12"
       }
   ...
   Plan: 2 to add, 0 to change, 0 to destroy.
   ```
   {: screen}

3. Add the zones to your cluster. When you add the zones to the cluster, new worker nodes are created in these zones which might take a few minutes to complete.
   
   ```
   terraform apply
   ```
   {: pre}
   
   Example output: 

   ```
   ...
   ibm_container_worker_pool_zone_attachment.dal12: Still creating... [28m20s elapsed]
   ibm_container_worker_pool_zone_attachment.dal12: Still creating... [28m30s elapsed]
   ibm_container_worker_pool_zone_attachment.dal12: Still creating... [28m40s elapsed]
   ibm_container_worker_pool_zone_attachment.dal12: Creation complete after 28m48s 
   ...
   ibm_container_worker_pool_zone_attachment.dal13: Still creating... [28m20s elapsed]
   ibm_container_worker_pool_zone_attachment.dal13: Still creating... [28m30s elapsed]
   ibm_container_worker_pool_zone_attachment.dal13: Still creating... [28m40s elapsed]
   ibm_container_worker_pool_zone_attachment.dal13: Creation complete after 28m48s 

   Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
   ```
   {: screen}
   
4. Optional: Review the worker nodes in your cluster from the CLI. 
 
   **Example for {{site.data.keyword.containerlong_notm}}:**
   ```
   ibmcloud ks workers --cluster tfcluster
   ```
   {: pre}
   
   **Example for {{site.data.keyword.openshiftlong_notm}}:**
   ```
   ibmcloud oc workers --cluster tfcluster
   ```
   {: pre}
   
</br>
You successfully converted your single zone cluster into a multizone cluster. 
 
## Lesson 4: Add a worker pool to your cluster
{: #workerpool-add}

Create another worker pool in your cluster and add zones to the worker pool to add more worker nodes to your cluster. 
{: shortdesc}

Adding a worker pool only does not create any worker nodes. To create worker nodes, you must use the `ibm_container_worker_pool_zone_attachement` resource to add zones to your worker pool. 
{: note}

1. Open your existing Terraform configuration file and add the following content to your configuration. The `ibm_container_worker_pool` resource creates a worker pool in your cluster with a size of two worker nodes per zone that you want. To start creating the worker nodes in each zone, you must add an `ibm_container_worker_pool_zone_attachment` resource for every zone where you want to create worker nodes. 

   ```
   resource "ibm_container_worker_pool" "workerpool" {
     worker_pool_name = "tf-workerpool"
     machine_type     = "u3c.2x4"
     cluster          = ibm_container_cluster.tfcluster.id
     size_per_zone    = 2
     hardware         = "shared"

     resource_group_id = data.ibm_resource_group.resource_group.id
   }
   
   resource "ibm_container_worker_pool_zone_attachment" "tfwp-dal10" {
    cluster         = ibm_container_cluster.tfcluster.id
    worker_pool     = element(split("/",ibm_container_worker_pool.workerpool.id),1)
    zone            = "dal10"
    private_vlan_id = "<private_vlan_ID_dal10>"
    public_vlan_id  = "<public_vlan_ID_dal10>"
    resource_group_id = data.ibm_resource_group.resource_group.id
   }
   
   resource "ibm_container_worker_pool_zone_attachment" "tfwp-dal12" {
    cluster         = ibm_container_cluster.tfcluster.id
    worker_pool     = element(split("/",ibm_container_worker_pool.workerpool.id),1)
    zone            = "dal12"
    private_vlan_id = "<private_vlan_ID_dal12>"
    public_vlan_id  = "<public_vlan_ID_dal12>"
    resource_group_id = data.ibm_resource_group.resource_group.id
   }
   
   resource "ibm_container_worker_pool_zone_attachment" "tfwp-dal13" {
    cluster         = ibm_container_cluster.tfcluster.id
    worker_pool     = element(split("/",ibm_container_worker_pool.workerpool.id),1)
    zone            = "dal13"
    private_vlan_id = "<private_vlan_ID_dal13>"
    public_vlan_id  = "<public_vlan_ID_dal13>"
    resource_group_id = data.ibm_resource_group.resource_group.id
   }   
   ```
   {: codeblock}
   
   <table>
   <caption>Understanding the configuration file</caption>
   <col style="width:30%">
	 <col style="width:70%">
   <thead>
     <th>Parameter</th>
     <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>resource.ibm_container_worker_pool.worker_pool_name</code></td>
   <td>Enter a name for your worker pool. </td>
   </tr>
     <tr>
   <td><code>resource.ibm_container_worker_pool.machine_type</code></td>
   <td>Enter the flavor for your worker nodes in your worker pool. The example in this tutorial uses a virtual machine worker node. To list other supported flavors in your zone, run <code>ibmcloud ks flavors --zone &lt;zone&gt;</code>. For an overview of supported flavors and how they are provisioned, see the [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-planning_worker_nodes) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-planning_worker_nodes) documentation.  </td>
   </tr>
     <tr>
   <td><code>resource.ibm_container_worker_pool.cluster</code></td>
   <td>Enter the name or ID of the cluster where you want to create the worker pool. The example in this tutorial references the cluster that you created in lesson 3. Terraform automatically retrieves the ID of the cluster. </td>
   </tr>
     <tr>
   <td><code>resource.ibm_container_worker_pool.size_per_zone</code></td>
   <td>Enter the number of worker nodes that you want to create when a zone is added to the worker pool. </td>
   </tr>
      <tr>
   <td><code>resource.ibm_container_worker_pool.hardware</code></td>
   <td>Decide if you want to provision your virtual worker nodes on <code>shared</code> or <code>dedicated</code> hardware.  Shared hardware can be used for virtual worker nodes only. Bare Metal machines are always dedicated to you. For more information, about shared and dedicated hardware, see the [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-planning_worker_nodes#vm) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-planning_worker_nodes#vm) documentation.</td>
   </tr>
   <tr>
   <td><code>resource.ibm_container_worker_pool.resource_group_id</code></td>
     <td>Retrieve the ID of the resource group where you want to create your worker pool from the <code>ibm_resource_group</code> data source that you defined in your configuration file. The resource group of the worker pool and the cluster must match. </td>
   </tr>   
      <tr>
   <td><code>data.ibm_container_worker_pool_zone_attachment.worker_pool</code></td>
   <td>Enter the ID of the new worker pool where you want to add the zone. The ID is returned as a concatenated string in the format <code>&lt;cluster_name_id&gt;/&lt;worker_pool_id&gt;</code>. To receive the worker pool ID, you must split the string after the <code>/</code>, put both strings into a list, and use the Terraform <code>element</code> function to retrieve the worker pool ID. </td>
   </tr>
   </tbody>
   </table>
   
2. Create an Terraform execution plan and review the actions that Terraform is about to perform.

   ```
   terraform plan
   ```
   {: pre}
   
   Example output: 
   ```
   ...
   Plan: 4 to add, 0 to change, 0 to destroy.
   ```
   {: screen}
   
3. Create the worker pool in your cluster and spread worker nodes across the zones that you defined. Note that the creation of worker nodes might take a few minutes to complete.

   ```
   terraform apply
   ```
   {: pre}
   
   Example output:

   ```
   ...
   ibm_container_worker_pool.workerpool: Creating...
   ibm_container_worker_pool.workerpool: Creation complete after 6s [id=aaaaaaaaa1eaaaaaaaaa/aaaaaaaaa1eaaaaaaa-aa1aa11]
   ibm_container_worker_pool_zone_attachment.test-dal10: Creating...
   ibm_container_worker_pool_zone_attachment.test-dal10: Still creating... [10s elapsed]
   ibm_container_worker_pool_zone_attachment.test-dal10: Still creating... [20s elapsed]
   ...
   Apply complete! Resources: 4 added, 0 changed, 0 destroyed.
   ```
   {: screen}
   
4. Optional: Review the worker nodes in your cluster from the CLI. 
   
   **Example for {{site.data.keyword.containerlong_notm}}:**

   ```
   ibmcloud ks workers --cluster tfcluster --show-pools
   ```
   {: pre}
   
   **Example for {{site.data.keyword.openshiftlong_notm}}:**

   ```
   ibmcloud oc workers --cluster tfcluster --show-pools
   ```
   {: pre}
 
## Lesson 5: Remove the default worker pool from your cluster
{: #rm-default-wp}

You can remove the default worker pool from your cluster. 
{: shortdesc}

The default worker pool is automatically created when the cluster is created. Because you do not explicitly specify the default worker pool in your configuration file, you cannot remove this worker pool by removing the `ibm_container_worker_pool` resource from your file. Instead, you use the `local-exec` Terraform provisioner to run an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} command against your cluster to remove the default worker pool. 

1. Open your Terraform configuration and add the following content. To run a command against your cluster, you embed the `local-exec` provisioner in an Terraform [`null_resource`](https://registry.terraform.io/providers/hashicorp/null/latest/docs/resources/resource){: external}. 
   
   **Example for an {{site.data.keyword.containerlong_notm}} cluster:**

   ```
   resource "null_resource" "delete-default-worker-pool" {
     provisioner "local-exec" {
       command = "ibmcloud ks worker-pool rm --cluster ${ibm_container_cluster.tfcluster.id} --worker-pool ${ibm_container_cluster.tfcluster.worker_pools.0.id}"
     }
   }
   ```
   {: codeblock}
    
   **Example for an {{site.data.keyword.openshiftlong_notm}} cluster:**

   ```
   resource "null_resource" "delete-default-worker-pool" {
     provisioner "local-exec" {
       command = "ibmcloud oc worker-pool rm --cluster ${ibm_container_cluster.tfcluster.id} --worker-pool ${ibm_container_cluster.tfcluster.worker_pools.0.id}"
     }
   }
   ```
   {: codeblock}
    
2. Initialize the Terraform CLI. 

    ```
    terraform init
    ```
    {: pre}
   
3. Create an Terraform execution plan and review the actions that Terraform is about to perform.

   ```
    terraform plan
   ```
   {: pre}
   
   Example output: 

   ```
   ...
   Plan: 1 to add, 0 to change, 0 to destroy.
   ```
   {: screen}
   
4. Remove the default worker pool from your cluster. Note that although the command completes within a few seconds, the deletion of your default worker pool and all associated worker nodes continues in the background and takes a few minutes to complete. 

   ```
    terraform apply
   ```
   {: pre}
   
   Example output:

   ```
   ...
   null_resource.delete-worker-pool: Creating...
   null_resource.delete-worker-pool: Provisioning with 'local-exec'...
   null_resource.delete-worker-pool (local-exec): Executing: ["/bin/sh" "-c" "ibmcloud ks worker-pool rm --cluster <cluster_ID> --worker-pool <worker_pool_ID>"]
   null_resource.delete-worker-pool (local-exec): OK
   null_resource.delete-worker-pool: Creation complete after 3s [id=2958122372197562274]

   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
   ```
   {: screen}
   
5. Optional: Review the worker nodes in your cluster from the CLI. 
   
   **Example for {{site.data.keyword.containerlong_notm}}:**

   ```
    ibmcloud ks workers --cluster tfcluster --show-pools
   ```
   {: pre}
   
   **Example for {{site.data.keyword.openshiftlong_notm}}:**

   ```
    ibmcloud oc workers --cluster tfcluster --show-pools
   ```
   {: pre}
   
6. Remove the `ibm_container_worker_pool_zone_attachment` resources that you added for the default worker pool from your Terraform configuration file. This step is important so that these resources are not added to your cluster again when you run the next `terraform apply` command. To remove these resources, you can remove the code from your file or use `#` to comment out each line. The following lines must be removed.

   ```
   resource "ibm_container_worker_pool_zone_attachment" "dal12" {
    cluster         = ibm_container_cluster.tfcluster.id
    worker_pool     = ibm_container_cluster.tfcluster.worker_pools.0.id
    zone            = "dal12"
    private_vlan_id = "<private_vlan_ID_dal12>"
    public_vlan_id  = "<public_vlan_ID_dal12>"
    resource_group_id = data.ibm_resource_group.resource_group.id
   } 

   resource "ibm_container_worker_pool_zone_attachment" "dal13" {
    cluster         = ibm_container_cluster.tfcluster.id
    worker_pool     = ibm_container_cluster.tfcluster.worker_pools.0.id
    zone            = "dal13"
    private_vlan_id = "<private_vlan_ID_dal13>"
    public_vlan_id  = "<public_vlan_ID_dal13>"
    resource_group_id = data.ibm_resource_group.resource_group.id
   }
   ```
   {: codeblock}

7. Update the Terraform statefile. When you run this command, Terraform automatically verifies that all of the resources in the statefile exist in {{site.data.keyword.cloud_notm}}. Missing resources are removed from the statefile.

   ```
    terraform refresh
   ```
   {: pre}
   
</br>

**What's next?**</br>

Great job! You successfully created a multizone {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster, added a worker pool, and removed the default worker pool from your cluster. Explore the learning paths for administrators in [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-learning-path-admin) and [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-learning-path-admin) to learn how you can further protect your cluster, add persistent storage, set up integrations, add logging and monitoring capabilities, and more. 
