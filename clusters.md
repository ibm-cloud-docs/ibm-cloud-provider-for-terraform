---

copyright:
  years: 2017, 2025
lastupdated: "2025-12-09"

keywords: terraform create kubernetes cluster, terraform create openshift cluster, terraform kubernetes cluster, terraform openshift cluster, schematics create kubernetes cluster, schematics create openshift cluster, schematics kubernetes cluster, schematics openshift cluster, terraform iks cluster, terraform roks cluster, schematics iks cluster, schematics roks cluster, terraform multizone cluster, schematics multizone cluster, terraform remove default worker pool, schematics remove default worker pool

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: containers, terraform, openshift
account-plan:
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}


# Creating single and multizone Kubernetes and OpenShift clusters
{: #tutorial-tf-clusters}
{: toc-content-type="tutorial"}
{: toc-services="containers, terraform, openshift"}
{: toc-completion-time="2h"}

Use this tutorial to create single and multizone clusters with [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-getting-started) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-getting-started), and deploy your own set of compute hosts in the public cloud where you can run and manage highly available containerized apps.

In this tutorial, you create a standard classic {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster with the following configuration:

- The cluster is created in the `us-south` region.
- The cluster is created with the default worker pool.
- All worker nodes are connected to a private and public VLAN. These public and private VLANs assign public and private IP addresses to the worker nodes.
- All worker nodes are created with a virtual worker node flavor on shared hardware. If you want to use a different worker node flavor, see the [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-add-workers-vpc) or [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-add-workers-vpc) documentation.
- To allow access to your cluster from the internet and run public-facing app workloads in your cluster, the cluster is set up with both a public and a private service endpoint. For more information, about how network traffic flows when a public and a private service endpoint is enabled, see Worker-to-master and user-to-master communication: Service endpoints in [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-strategy) and [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-clusters).

Keep in mind that creating a cluster incurs costs. Make sure to review [What am I charged for when I use {{site.data.keyword.containerlong_notm}}?](/docs/containers?topic=containers-faqs#charges) or [What am I charged for when I use {{site.data.keyword.openshiftlong_notm}}?](/docs/openshift?topic=openshift-faqs#charges) before you proceed.
{: note}

## Objectives
{: #cluster-tutorial-objectives}

In this tutorial, you will:
- Learn how to create a single zone {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster with Terraform on IBM Cloud.
- Convert your single zone cluster into a multizone cluster for higher availability.
- Add a new worker pool to the cluster.
- Remove the default worker pool that is automatically set up during cluster creation.

## Audience
{: #cluster-tutorial-audience}

This tutorial is intended for system administrators that want to learn how to create an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster and spread this cluster across zones.

## Prerequisites
{: #cluster-tutorial-prereq}

- If you do not have one, create an [IBM Cloud Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration){: external}.
- Install the [{{site.data.keyword.cloud_notm}} command line and the {{site.data.keyword.containerlong_notm}} command line plug-in](/docs/cli?topic=cli-getting-started).
- Follow the [instructions](/docs/containers?topic=containers-clusters#cluster_prepare) to make sure that you are assigned the required permissions in Identity and Access Management (IAM) to create clusters and that your account is enabled for Virtual Routing and Forwarding (VRF).

## Prepare your Terraform on IBM Cloud environment
{: #prepare-tf}
{: step}

1. [Install the Terraform on IBM Cloud command line and the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli).
2. If you do not have one, [create an {{site.data.keyword.cloud_notm}} API key](/docs/account?topic=account-userapikey&interface=ui).
3. Create an Terraform on IBM Cloud project directory. The directory will hold all your Terraform on IBM Cloud configuration files that you create as part of this tutorial. The directory in this tutorial is named `tf-cluster`, but you can use any name for the directory.

    ``` sh
    mkdir tf-cluster && cd tf-cluster
    ```
    {: pre}

4. In your project directory, create a `terraform.tfvars` file and add the {{site.data.keyword.cloud_notm}} API key that you created earlier. The `terraform.tfvars` file is an Terraform on IBM Cloud variables file that you store on your local machine. When you initialize the Terraform on IBM Cloud CLI, all variables that are defined in this file are automatically loaded into Terraform on IBM Cloud and you can reference them in every Terraform on IBM Cloud configuration file in the same project directory.

    ```terraform
    ibmcloud_api_key = "<ibmcloud_api_key>"
    ```
    {: codeblock}

    The `terraform.tfvars` file includes credentials to authenticate with the {{site.data.keyword.cloud_notm}} platform. Keep the file on your local machine only and do not share these credentials with an unauthorized person.
    {: important}

5. In the same project directory, create a `provider.tf` file and configure IBM as your Terraform on IBM Cloud provider. To authenticate with {{site.data.keyword.cloud_notm}}, you must pass in your {{site.data.keyword.cloud_notm}} API key by using Terraform on IBM Cloud interpolation syntax.

    The providers file is used to configure your endpoint URLs, cloud regions, or other settings before Terraform can use them, so that Terraform can install and use them in the [provider configuration](https://developer.hashicorp.com/terraform/language/providers/configuration){: external} file that is named `provider.tf`.
    {: note}

    ```terraform
    terraform {
    required_version = ">=1.0.0, <2.0"
    required_providers {
        ibm = {
        source = "IBM-Cloud/ibm"
        }
    }
    }
    ```
    {: codeblock}

Great! Now that you completed your Terraform on IBM Cloud setup, you can go ahead and add the code to create your {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster.

## Create a single zone cluster
{: #create-cluster}
{: step}

Create a classic {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster by using Terraform on IBM Cloud.
{: shortdesc}

1. Create an Terraform on IBM Cloud configuration file for your single zone cluster. The following example creates a single zone cluster in the `dal10` zone with a default worker pool that consists of 3 worker nodes that are connected to a private and public VLAN in `dal10`.

    Example for an {{site.data.keyword.containerlong_notm}} cluster

    ```terraform
    data ibm_resource_group "resource_group" {
        name = "default"
    }
    resource ibm_container_cluster "tfcluster" {
    name            = "tfclusterdoc"
    datacenter      = "dal10"
    machine_type    = "b3c.4x16"
    hardware        = "shared"
    public_vlan_id  = "2234945"
    private_vlan_id = "2234947"

    kube_version = "1.21.9"

    default_pool_size = 3

    public_service_endpoint  = "true"
    private_service_endpoint = "true"

    resource_group_id = data.ibm_resource_group.resource_group.id
    }
    ```
    {: codeblock}

    For more information, about the description of `ibm_container_cluster` argument reference such as `public_vlan_id`, `private_vlan_id`, `kube_version` values, refer to [registry documentation of `ibm_container_cluster`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference){: external}.
    {: note}

    Example for an {{site.data.keyword.openshiftlong_notm}} cluster

    ```terraform
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

    For more information, about the description of `ibm_container_cluster` argument reference such as `public_vlan_id`, `private_vlan_id`, `kube_version` values, refer to [registry documentation of `ibm_container_cluster`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference){: external}.
    {: note}

2. Initialize the Terraform on IBM Cloud CLI.

    ```sh
    terraform init
    ```
    {: pre}

3. Create an Terraform on IBM Cloud execution plan. When you execute this command, Terraform on IBM Cloud validates the syntax of your configuration file and resource definitions against the specifications of the {{site.data.keyword.cloud_notm}} Provider plug-in.

    ```sh
    terraform plan
    ```
    {: pre}

    Example output:

    ```text
    Refreshing Terraform on IBM Cloud state in-memory prior to plan...

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

4. Review the Terraform on IBM Cloud execution plan to verify that your cluster set up is correct.
5. Create your single zone cluster. Note that the creation of your cluster takes a few minutes to complete.

    ```sh
    terraform apply
    ```
    {: pre}

    Example output:

    ```text
    ...
    ibm_container_cluster.tfcluster: Creating...
    ibm_container_cluster.tfcluster: Still creating... [10s elapsed]
    ...
    ibm_container_cluster.tfcluster: Creation complete after 20m27s [id=bpugrqtd0ejuoqvinshg]

    Apply complete! Resources: 1 added, 0 changed, 1 destroyed.
    ```
    {: screen}

6. Optional: Review your cluster from the command-line.

    Example for {{site.data.keyword.containerlong_notm}}

    ```sh
    ibmcloud ks cluster get --cluster tfcluster
    ```
    {: pre}

    Example for {{site.data.keyword.openshiftlong_notm}}

    ```sh
    ibmcloud oc cluster get --cluster tfcluster
    ```
    {: pre}


You have now completed the tutorial! You created your single zone {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster.

## Convert your single zone cluster into a multizone cluster
{: #multizone}
{: step}

Add zones to the default worker pool in your cluster that you created in `step 1`. By adding zones, the same number of worker nodes that you created in `step 2` are spread across these zones converting your single zone cluster into a multizone cluster.
{: shortdesc}

1. Open your Terraform on IBM Cloud configuration file and add the following content to your configuration. For each zone that you want to add, you must add a separate `ibm_container_worker_pool_zone_attachment` resource.

    ```terraform
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

    For more information, about the description of `ibm_container_worker_pool_zone_attachment` argument reference such as `public_vlan_id`, `private_vlan_id` values, refer to [registry documentation of `ibm_container_worker_pool_zone_attachment`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_worker_pool_zone_attachment#argument-reference){: external}.
    {: note}

2. Create an Terraform on IBM Cloud execution plan and review the action Terraform on IBM Cloud is about to perform.

    ```sh
    terraform plan
    ```
    {: pre}

    Example output:

    ```text
    data.ibm_resource_group.resource_group: Refreshing state...
    ibm_container_cluster.tfcluster: Refreshing state... [id=aaaaaaa1aaaaaaaaaaa]

    ------------------------------------------------------------------------

    An execution plan has been generated and is shown.
    Resource actions are indicated with the following symbols:
        + create

    Terraform on IBM Cloud will perform the following actions:

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

    ```sh
    terraform apply
    ```
    {: pre}

    Example output:

    ```text
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

4. Optional: Review the worker nodes in your cluster from the command-line.

    Example for {{site.data.keyword.containerlong_notm}}

    ```sh
    ibmcloud ks workers --cluster tfcluster
    ```
    {: pre}

    Example for {{site.data.keyword.openshiftlong_notm}}

    ```sh
    ibmcloud oc workers --cluster tfcluster
    ```
    {: pre}

You successfully converted your single zone cluster into a multizone cluster.

## Add a worker pool to your cluster
{: #workerpool-add}
{: step}

Create another worker pool in your cluster and add zones to the worker pool to add more worker nodes to your cluster.
{: shortdesc}

Adding a worker pool only does not create any worker nodes. To create worker nodes, you must use the `ibm_container_worker_pool_zone_attachement` resource to add zones to your worker pool.
{: note}

1. Open your existing Terraform on IBM Cloud configuration file and add the following content to your configuration. The `ibm_container_worker_pool` resource creates a worker pool in your cluster with a size of two worker nodes per zone that you want. To start creating the worker nodes in each zone, you must add an `ibm_container_worker_pool_zone_attachment` resource for every zone where you want to create worker nodes.

    ```terraform
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

    For more information, about the description of `ibm_container_worker_pool_zone_attachment` argument reference such as `public_vlan_id`, `private_vlan_id` values, refer to [registry documentation of `ibm_container_worker_pool_zone_attachment`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_worker_pool_zone_attachment#argument-reference){: external}.
    {: note}

     For more information, about the description of `ibm_container_worker_pool` argument reference, refer to [registry documentation of `ibm_container_worker_pool`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_worker_pool#argument-reference){: external}.
    {: note}

2. Create an Terraform on IBM Cloud execution plan and review the actions that Terraform on IBM Cloud is about to perform.

    ```sh
    terraform plan
    ```
    {: pre}

    Example output

    ```text
    ...
    Plan: 4 to add, 0 to change, 0 to destroy.
    ```
    {: screen}

3. Create the worker pool in your cluster and spread worker nodes across the zones that you defined. Note that the creation of worker nodes might take a few minutes to complete.

    ```sh
    terraform apply
    ```
    {: pre}

    Example output

    ```text
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

4. Optional: Review the worker nodes in your cluster from the command-line.

    Example for {{site.data.keyword.containerlong_notm}}

    ```sh
    ibmcloud ks workers --cluster tfcluster --show-pools
    ```
    {: pre}

    Example for {{site.data.keyword.openshiftlong_notm}}

    ```sh
    ibmcloud oc workers --cluster tfcluster --show-pools
    ```
    {: pre}

## Remove the default worker pool from your cluster
{: #rm-default-wp}
{: step}

You can remove the default worker pool from your cluster.
{: shortdesc}

The default worker pool is automatically created when the cluster is created. Because you do not explicitly specify the default worker pool in your configuration file, you cannot remove this worker pool by removing the `ibm_container_worker_pool` resource from your file. Instead, you use the `local-exec` Terraform on IBM Cloud provisioner to run an {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} command against your cluster to remove the default worker pool.

1. Open your Terraform on IBM Cloud configuration and add the following content. To run a command against your cluster, you embed the `local-exec` provisioner in an Terraform on IBM Cloud [`null_resource`](https://registry.terraform.io/providers/hashicorp/null/latest/docs/resources/resource){: external}.

    Example for an {{site.data.keyword.containerlong_notm}} cluster

    ```terraform
    resource "null_resource" "delete-default-worker-pool" {
        provisioner "local-exec" {
        command = "ibmcloud ks worker-pool rm --cluster ${ibm_container_cluster.tfcluster.id} --worker-pool ${ibm_container_cluster.tfcluster.worker_pools.0.id}"
        }
    }
    ```
    {: codeblock}

    Example for an {{site.data.keyword.openshiftlong_notm}} cluster

    ```text
    resource "null_resource" "delete-default-worker-pool" {
        provisioner "local-exec" {
        command = "ibmcloud oc worker-pool rm --cluster ${ibm_container_cluster.tfcluster.id} --worker-pool ${ibm_container_cluster.tfcluster.worker_pools.0.id}"
        }
    }
    ```
    {: codeblock}

2. Initialize the Terraform on IBM Cloud command-line.

    ```sh
    terraform init
    ```
    {: pre}

3. Create an Terraform on IBM Cloud execution plan and review the actions that Terraform on IBM Cloud is about to perform.

    ```sh
    terraform plan
    ```
    {: pre}

    Example output

    ```text
    ...
    Plan: 1 to add, 0 to change, 0 to destroy.
    ```
    {: screen}

4. Remove the default worker pool from your cluster. Note that although the command completes within a few seconds, the deletion of your default worker pool and all associated worker nodes continues in the background and takes a few minutes to complete.

    ```sh
    terraform apply
    ```
    {: pre}

    Example output:

    ```text
    ...
    null_resource.delete-worker-pool: Creating...
    null_resource.delete-worker-pool: Provisioning with 'local-exec'...
    null_resource.delete-worker-pool (local-exec): Executing: ["/bin/sh" "-c" "ibmcloud ks worker-pool rm --cluster <cluster_ID> --worker-pool <worker_pool_ID>"]
    null_resource.delete-worker-pool (local-exec): OK
    null_resource.delete-worker-pool: Creation complete after 3s [id=2958122372197562274]

    Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
    ```
    {: screen}

5. Optional: Review the worker nodes in your cluster from the command-line.

    Example for {{site.data.keyword.containerlong_notm}}

    ```sh
    ibmcloud ks workers --cluster tfcluster --show-pools
    ```
    {: pre}

    Example for {{site.data.keyword.openshiftlong_notm}}

    ```sh
    ibmcloud oc workers --cluster tfcluster --show-pools
    ```
    {: pre}

6. Remove the `ibm_container_worker_pool_zone_attachment` resources that you added for the default worker pool from your Terraform on IBM Cloud configuration file. This step is important so that these resources are not added to your cluster again when you run the next `terraform apply` command. To remove these resources, you can remove the code from your file or use `#` to comment out each line. The following lines must be removed.

    ```terraform
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

    For more information, about the description of `ibm_container_worker_pool_zone_attachment` argument reference such as `public_vlan_id`, `private_vlan_id` values, refer to [registry documentation of `ibm_container_worker_pool_zone_attachment`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_worker_pool_zone_attachment#argument-reference){: external}.
    {: note}

7. Update the Terraform on IBM Cloud state file. When you run this command, Terraform on IBM Cloud automatically verifies that all the resources in the state file exist in {{site.data.keyword.cloud_notm}}. Missing resources are removed from the state file.

    ```sh
    terraform refresh
    ```
    {: pre}

## What's next?
{: #multizone-whatsnext}

Great job! You successfully created a multizone {{site.data.keyword.containerlong_notm}} or {{site.data.keyword.openshiftlong_notm}} cluster, added a worker pool, and removed the default worker pool from your cluster. Explore the learning paths for administrators in [{{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-learning-path-admin) and [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-learning-path-admin) to learn how you can further protect your cluster, add persistent storage, set up integrations, add logging and monitoring capabilities, and more.
