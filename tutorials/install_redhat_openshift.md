---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-22"

keywords: Terraform on IBM Cloud, ansible, red hat, openshift, automate, automation, iaas

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
services: terraform, openshift
account-plan: 
completion-time: 3h

---

{{site.data.keyword.attribute-definition-list}}


# Using Terraform on IBM Cloud to manage your own Red Hat OpenShift Container Platform on IBM Cloud classic infrastructure
{: #redhat}
{: toc-content-type="tutorial"}
{: toc-services="terraform, openshift"}
{: toc-completion-time="3h"}

Use this tutorial to create your own highly available Red Hat® OpenShift Container Platform 3.11 environment on IBM® Cloud classic infrastructure by using Terraform on IBM Cloud. 
{: shortdesc}

Instead of manually installing Red Hat® OpenShift Container Platform on {{site.data.keyword.cloud_notm}} classic infrastructure, check out [Red Hat OpenShift on {{site.data.keyword.cloud_notm}}](/docs/openshift?topic=openshift-openshift_tutorial). This offering lets you create an {{site.data.keyword.containerlong_notm}} cluster with worker nodes that come installed with the OpenShift Container Platform software. You get all the advantages of managed {{site.data.keyword.containerlong_notm}} for your cluster infrastructure environment, while the OpenShift tooling and catalog that runs on Red Hat Enterprise Linux for your app deployments.
{: tip}

[Red Hat® OpenShift Container Platform ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.redhat.com/en/technologies/cloud-computing/openshift/container-platform){: external} is built around a core of containers, with orchestration and management provided by Kubernetes, on a foundation of Atomic Host and Red Hat® Enterprise Linux. OpenShift Origin is the community distribution of Kubernetes that is optimized for continuous app development and multi-tenant deployment. The community project provides developer and operations-centric tools that are based on Kubernetes to enable rapid app development, deployment, scaling, and long-term app lifecycle maintenance. 

This tutorial shows how you can set up OpenShift Container Platform 3.11 on {{site.data.keyword.cloud_notm}} classic infrastructure with Terraform on IBM Cloud to try out the high availability capabilities of native Kubernetes and {{site.data.keyword.cloud_notm}}. Review the following image to find an architectural overview of the classic infrastructure components that are needed for the Red Hat OpenShift Container Platform to work properly.

<img src="../images/infra-diagram.png" alt="Infrastructure components for the Red Hat® OpenShift Container Platform on {{site.data.keyword.cloud_notm}}" width="800" style="width: 800px; border-style: none"/>

When you complete this tutorial, the following classic infrastructure components are provisioned for you: 
- 1 OpenShift Container Platform master node 
- 1 OpenShift Container Platform infrastructure node
- 1 OpenShift Container Platform application node
- 1 OpenShift Container Platform Bastion node
- 3 or more GlusterFS storage nodes if you decide to set up your cluster with GlusterFS
- Native {{site.data.keyword.cloud_notm}} classic infrastructure services, such as VLANs and security groups

## Objectives 
{: #objectives}

In this tutorial, you set up Red Hat OpenShift Container Platform version 3.11 on {{site.data.keyword.cloud_notm}} classic infrastructure and deploy your first `nginx` app in the OpenShift cluster. In particular, you will: 

- Set up your environment and all the software that you need for your Red Hat OpenShift Container Platform installation, such as Terraform on IBM Cloud, {{site.data.keyword.cloud_notm}} Provider plug-in, and the Terraform on IBM Cloud OpenShift project. 
- Retrieve {{site.data.keyword.cloud_notm}} credentials, configure the {{site.data.keyword.cloud_notm}} Provider plug-in, and define your Red Hat OpenShift Container Platform classic infrastructure components.
- Provision {{site.data.keyword.cloud_notm}} classic infrastructure for your Red Hat OpenShift Container Platform components by using Terraform on IBM Cloud. 
- Install Red Hat OpenShift Container Platform on {{site.data.keyword.cloud_notm}} classic infrastructure. 
- Deploy the `nginx` app in your OpenShift cluster and expose this app to the public. 

## Audience
{: #audience}

This tutorial is intended for network administrators who want to deploy Red Hat OpenShift Container Platform on {{site.data.keyword.cloud_notm}} classic infrastructure. 

## Prerequisites
{: #prerequisites}

- If you do not have one, create an {{site.data.keyword.cloud_notm}} [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration). 
- Make sure that you have an existing {{site.data.keyword.redhat_notm}} account that has an [active OpenShift subscription](https://access.redhat.com/products/red-hat-openshift-container-platform){: external}. 
- Install [Docker and the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). 

## Lesson 1: Configure your environment
{: #configure_environment}

In this tutorial, you provision {{site.data.keyword.cloud_notm}} classic infrastructure for the Red Hat OpenShift Container Platform by using Terraform on IBM Cloud. Before you can start the classic infrastructure provisioning process, you must ensure that you set up Terraform on IBM Cloud, the {{site.data.keyword.cloud_notm}} Provider plug-in, and the Terraform on IBM Cloud OpenShift project. 
{: shortdesc}

1. Create a Docker container that installs Terraform on IBM Cloud and the {{site.data.keyword.cloud_notm}} Provider plug-in. To execute Terraform on IBM Cloud commands, you must be logged in to the container. 
    You can also [install Terraform on IBM Cloud and the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#setup_cli) on your local machine to run Terraform on IBM Cloud commands without a Docker container. 
    {: tip}

    1. Download the latest version of the Docker image for Terraform on IBM Cloud to your local machine. 
        ```sh
        docker pull ibmterraform/terraform-provider-ibm-docker
        ```
        {: pre}

        Example output: 
        ```text
        Using default tag: latest
        latest: Pulling from ibmterraform/terraform-provider-ibm-docker
        911c6d0c7995: Pull complete 
        fed331e93a76: Pull complete 
        82a1ea1a0cd7: Pull complete 
        a4b4f00ab356: Pull complete 
        78858415d97d: Pull complete 
        515c9be5f236: Pull complete 
        94021f117e26: Pull complete 
        a50b454f6bba: Pull complete 
        dd63d43987e3: Pull complete 
        a098dba94337: Pull complete  
        Digest: sha256:df316f5ed26cbec1bc1ad7a6f6d2c978f767408080a4a4db954c94c91e8271e5
        Status: Downloaded newer image for ibmterraform/terraform-provider-ibm-docker:latest
        ```
        {: screen}

    2. Create a container from your image and log in to your container. When the container is created, Terraform on IBM Cloud and the {{site.data.keyword.cloud_notm}} Provider plug-in are automatically installed and you are automatically logged in to the container. The working directory is set to `/go/bin`. 
        ```sh
        docker run -it ibmterraform/terraform-provider-ibm-docker:latest
        ```
        {: pre}

2. From within your container, set up the IBM Terraform on IBM Cloud OpenShift Project.
    1. Install OpenSSH inside the container that you created in the previous step. 
        ```sh
        apk add --no-cache openssh
        ```
        {: pre}

        Example output: 
        ```text
        fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/main/x86_64/APKINDEX.tar.gz
        fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/community/x86_64/APKINDEX.tar.gz
        (1/6) Installing openssh-keygen (7.5_p1-r9)
        (2/6) Installing openssh-client (7.5_p1-r9)
        (3/6) Installing openssh-sftp-server (7.5_p1-r9)
        (4/6) Installing openssh-server-common (7.5_p1-r9)
        (5/6) Installing openssh-server (7.5_p1-r9)
        (6/6) Installing openssh (7.5_p1-r9)
        Executing busybox-1.27.2-r11.trigger
        OK: 326 MiB in 50 packages
        ```
        {: screen}

    2. Download the Terraform on IBM Cloud configuration files to deploy the Red Hat OpenShift Container Platform. 
        ```sh
        git clone https://github.com/IBM-Cloud/terraform-ibm-openshift.git
        ```
        {: pre}

        Example output: 
        ```text
        Cloning into 'terraform-ibm-openshift'...
        remote: Enumerating objects: 375, done.
        remote: Total 375 (delta 0), reused 0 (delta 0), pack-reused 375
        Receiving objects: 100% (375/375), 681.75 KiB | 1.22 MiB/s, done.
        Resolving deltas: 100% (190/190), done.
        ```
        {: screen}

    3. Navigate into the installation directory. 
        ```sh
        cd terraform-ibm-openshift
        ```
        {: pre}

3. Generate an SSH key. The SSH key is used to access {{site.data.keyword.cloud_notm}} classic infrastructure resources during provisioning.  
    1. Create an SSH key inside the container that you created earlier. Enter the email address that you want to associate with your SSH key. Make sure to accept the default file name, file location, and missing passphrase by pressing **Enter**.
        ```sh
        ssh-keygen -t rsa -b 4096 -C "<email_address>"
        ```
        {: pre}

        Example output: 
        ```text
        Generating public/private RSA key pair.
        Enter file in which to save the key (/root/.ssh/id_rsa): 
        Created directory '/root/.ssh'.
        Enter passphrase (empty for no passphrase): 
        Enter same passphrase again: 
        Your identification has been saved in /root/.ssh/id_rsa.
        Your public key has been saved in /root/.ssh/id_rsa.pub.
        The key fingerprint is:
        SHA256:67LDt8zjbPoX+uKFGrVs2CrsyNk1izzBOkDf8tBb3Xc myemail@example.com
        The key's randomart image is:
        +---[RSA 4096]----+
        |                 |
        |                 |
        |                 |
        | .               |
        |. ..o   S .      |
        |.  +oo * =.. . E |
        | . o+oB B.... .  |
        | .o=+=+%*..      |
        |  +o=o*@X*.      |
        +----[SHA256]-----+
        ```
        {: screen}

    2. Verify that the SSH key is created successfully. The creation is successful if you can see one **id_rsa** and one **id_rsa.pub** file. 
        ```sh
        cd /root/.ssh && ls
        ```
        {: pre}

        Example output: 
        ```text
        id_rsa      id_rsa.pub
        ```
        {: screen}

4. Navigate back to your OpenShift installation directory. 
    ```sh
    cd /go/bin/terraform-ibm-openshift
    ```
    {: pre}

5. Open the Terraform on IBM Cloud `variables.tf` file and review the default values that are set in the file. The `variables.tf` file specifies all information that you want to pass on to Terraform on IBM Cloud during the provisioning of your infrastructure resources. You can change the default values, but do not add sensitive data, such as your infrastructure user name and API key, to this file. The `variables.tf` file is usually stored under version control and shared across users. 
    ```sh
    vi variables.tf
    ```
    {: pre}

    <table>
    <thead>
    <th>Variable</th>
    <th>Description</th>
    <th>Default value</th>
    </thead>
    <tbody>
    <tr>
    <td><code>app_count</code></td>
    <td>Enter the number of app nodes that you want to create. App nodes are used to run your app pods.</td>
    <td>1</td>
    </tr>
    <tr>
    <td><code>bastion_flavor</code></td>
    <td>Enter the flavor that you want to use for your Bastion virtual machine. The Bastion host is the only ingress point for SSH in the OpenShift cluster from external entities. When you connect to the OpenShift Container Platform infrastructure, the Bastion host forwards the request to the infrastructure or app server. For more information, see <a href="https://access.redhat.com/documentation/en-us/reference_architectures/2018/html/deploying_and_managing_openshift_3.9_on_google_cloud_platform/components_and_considerations#bastion_instance">Bastion instance</a> <img src="../icons/launch-glyph.svg" alt="External link icon">. </td>
    <td>B1_4X16X100</td>
    </tr>
    <tr>
    <td><code>datacenter</code></td>
    <td>Enter the zone where you want to provision your {{site.data.keyword.cloud_notm}} classic infrastructure. To find existing zones, run <code>ibmcloud ks zones</code>. </td>
    <td>dal12</td>
    </tr>
    <tr>
    <td><code>ibm_sl_api_key</code></td>
    <td>The {{site.data.keyword.cloud_notm}} classic infrastructure API key to access classic infrastructure resources. Do not enter this information in this file. Instead, you are prompted to enter this information when you create the classic infrastructure resources. To retrieve your API key, see <a href="/docs/account?topic=account-classic_keys">Managing classic infrastructure API keys</a>.</td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>ibm_sl_username</code></td>
    <td>The {{site.data.keyword.cloud_notm}} classic infrastructure user name to access classic infrastructure resources. Do not enter this information in this file. Instead, you are prompted to enter this information when you create the classic infrastructure resources. To retrieve your user name, see <a href="/docs/account?topic=account-classic_keys">Managing classic infrastructure API keys</a>.</td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>infra_count</code></td>
    <td>Enter the number of infrastructure nodes that you want to create. Infrastructure nodes are used to run infrastructure-related pods, such as router or registry pods. </td>
    <td>1</td>
    </tr>
    <tr>
    <td><code>master_count</code></td>
    <td>Enter the number of master nodes that you want to create. The master runs the API server, controller manager server, and etcd database instance.</td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>pool_id</code></td>
    <td>The Red Hat pool ID that is linked to the subscription that you set up with Red Hat. Do not enter this information here. Instead, follow the steps in <a href="#deploy_openshift">Lesson 3</a> to retrieve your pool ID and provide the pool ID during the OpenShift installation. </td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>rhn_password</code></td>
    <td>The <a href="https://access.redhat.com/solutions/253273">Red Hat Network password</a> <img src="../icons/launch-glyph.svg" alt="External link icon"> to access the OpenShift project. You can enter this information here or provide it as part of your OpenShift deployment in <a href="#provision_infrastructure">Lesson 2</a>.  </td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>rhn_username</code></td>
    <td>The <a href="https://access.redhat.com/solutions/253273">Red Hat Network user name with OpenShift subscription</a> <img src="../icons/launch-glyph.svg" alt="External link icon"> to access the OpenShift project. You can enter this information here or provide it as part of your OpenShift deployment in <a href="#provision_infrastructure">Lesson 2</a>.  </td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>private_vlanid</code></td>
    <td>Enter the VLAN ID of your existing private VLAN that you want to use. To find existing VLAN IDs, run <code>ibmcloud sl vlan list</code> and review the <strong>ID</strong> column. </td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>public_vlanid</code></td>
    <td>Enter the VLAN ID of your existing public VLAN that you want to use. To find existing VLAN IDs, run <code>ibmcloud sl vlan list</code> and review the <strong>ID</strong> column. </td>
    <td>n/a</td>
    </tr>
    <tr>
    <td><code>ssh_label</code></td>
    <td>Enter a label to assign to your SSH key. </td>
    <td>ssh_key_openshift</td>
    </tr>
    <tr>
    <td><code>ssh_private_key</code></td>
    <td>Enter the path to the SSH private key that you created earlier. </td>
    <td><code>~/.ssh/id_rsa</code></td>
    </tr>
    <tr>
    <td><code>ssh_public_key</code></td>
    <td>Enter the path to the SSH public key that you created earlier. </td>
    <td><code>~/.ssh/id_rsa.pub</code></td>
    </tr>
    <tr>
    <td><code>storage_count</code></td>
    <td>Decide whether you want to configure your OpenShift cluster with GlusterFS. Enter 0 to configure your OpenShift cluster without GlusterFS, and 3 or more to set up your OpenShift cluster with GlusterFS. </td>
    <td>0</td>
    </tr>
    <tr>
    <td><code>storage_flavor</code></td>
    <td>If you configure your OpenShift cluster with GlusterFS, enter the flavor that you want to use for your storage virtual machine. Each storage node mounts three block storage devices that host the Red Hat Gluster Storage. You can use the combination of compute capacity and local Gluster storage to run a hyper-converged deployment where your apps are placed on the same node as the app's persistent storage. </td>
    <td>B1_4X16X100</td>
    </tr>   
    <tr>
    <td><code>subnet_size</code></td>
    <td>Enter the number of subnets that you want to be able to create with your public and private VLAN. This value is required only if you decide to create a new private and public VLAN pair. </td>
    <td>64</td>
    </tr>
    <tr>
    <td><code>vlan_count</code></td>
    <td>Enter <code>1</code> to automatically create a new private and public VLAN, or <code>0</code> if you want to use existing VLANs. To find existing VLANs, run <code>ibmcloud sl vlan list</code>. The zone where your existing VLAN routers are provisioned is included in the <strong>primary_router</strong> column of your command line output. </td>
    <td>1</td>
    </tr>
    <tr>
    <td><code>vm_domain</code></td>
    <td>Enter the domain name that you want to use for your virtual machine nodes. </td>
    <td><code>ibm.com</code></td>
    </tr>
    </tbody>
    </table>

## Lesson 2: Provision the IBM Cloud classic infrastructure for your Red Hat OpenShift cluster 
{: #provision_infrastructure}

Now that you prepared your environment, you can go ahead and provision {{site.data.keyword.cloud_notm}} classic infrastructure resources by using Terraform on IBM Cloud. 
{: shortdesc}

Before you begin, make sure that you are logged in to the container that you created in the previous lesson. 

1. [Retrieve your {{site.data.keyword.cloud_notm}} classic infrastructure user name and API key](/docs/account?topic=account-classic_keys).

2. From the OpenShift installation directory `/go/bin/terraform-ibm-openshift` inside your container, create the {{site.data.keyword.cloud_notm}} classic infrastructure components for your Red Hat OpenShift cluster. When you run the command, Terraform on IBM Cloud evaluates what components must be provisioned and presents an execution plan. You must confirm that you want to provision the classic infrastructure resources by entering **yes**. During the provisioning, Terraform on IBM Cloud creates another execution plan that you must approve to continue. When prompted, enter the classic infrastructure user name and API key that you retrieved earlier. The provisioning of your resources takes about 40 minutes.  
    ```sh
    make rhn_username=<rhn_username> rhn_password=<rhn_password> infrastructure
    ```
    {: pre}

    Example output: 
    ```text
    ...

    Apply complete! Resources: 63 added, 0 changed, 0 destroyed.
    ```
    {: screen}

    The following resources are created for you. 

    **Nodes**: 

    <table>
    <thead>
    <th>Resource</th>
    <th>Flavor</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td>Master node</td>
    <td>B1_4X16X100</td>
    <td>Three disks that are arranged as SAN with a total capacity of 100 GB <ul><li>Disk 1: 50 GB</li><li>Disk 2: 25 GB</li><li>Disk 3: 25 GB</li></ul></td>
    </tr>
    <tr>
    <td>Infrastructure node</td>
    <td>B1_2X4X100</td>
    <td>Three disks that are arranged as SAN with a total capacity of 100 GB <ul><li>Disk 1: 50 GB</li><li>Disk 2: 25 GB</li><li>Disk 3: 25 GB</li></ul></td>
    </tr>
    <tr>
    <td>App nodes</td>
    <td>B1_2X4X100</td>
    <td>Three disks that are arranged as SAN with a total capacity of 100 GB <ul><li>Disk 1: 50 GB</li><li>Disk 2: 25 GB</li><li>Disk 3: 25 GB</li></ul></td> 
    </tr>
    <tr>
    <td>Bastion node</td>
    <td>B1_2X2X100</td>
    <td>Two disks with the following capacity: <ul><li>Disk 1: 100 GB</li><li>Disk 2: 50 GB</li></ul></td>
    </tr>
    <tr>
    <td>Storage nodes</td>
    <td>B1_4X16X100</td>
    <td>Two disks with the following capacity: <ul><li>Disk 1: 100 GB</li><li>Disk 2: 50 GB </li><ul>
    </tbody>
    </table>

    <strong>Security groups</strong>: 

    The default security groups that are created assume the following setup: 
    - All outbound traffic from all nodes to the internet is allowed. 
    - The Bastion server is the only node that allows inbound SSH access. 
    - The Bastion server is connected to both the public and the private VLAN.
    - All OpenShift nodes (master, infrastructure, and app nodes) are connected to a private VLAN only. 
    </br>

    <table>
    <thead>
    <th>Group</th>
    <th>VLAN</th>
    <th>Inbound/ outbound</th>
    <th>Port</th>
    <th>From</th>
    <th>To</th>
    </thead>
    <tbody>
    <tr>
    <td><code>ose_bastion_sq</code></td>
    <td>Public</td>
    <td>Inbound</td>
    <td>22/ TCP</td>
    <td>Internet gateway</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_bastion_sq</code></td>
    <td>Private</td>
    <td>Outbound</td>
    <td>All</td>
    <td>-</td>
    <td>All</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>443/ TCP</td>
    <td>Internet gateway</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>80/ TCP</td>
    <td>Internet gateway</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>22/ TCP</td>
    <td>ose_bastion_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>443/ TCP</td>
    <td>ose_master_sg & ose_node_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>8053/ TCP</td>
    <td>ose_node_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>8053/ UDP</td>
    <td>ose_node_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Outbound</td>
    <td>All</td>
    <td>-</td>
    <td>All</td>
    </tr>
    <tr>
    <td><code>ose_master_sg (for etcd)</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>2379/ TCP</td>
    <td>ose_master_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_master_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>2380/ TCP</td>
    <td>ose_master_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_node_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>443/ TCP</td>
    <td>ose_bastion_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_node_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>22/ TCP</td>
    <td>ose_bastion_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_node_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>10250/ TCP</td>
    <td>ose_master_sg & ose_node_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_node_sg</code></td>
    <td>Private</td>
    <td>Inbound</td>
    <td>4789/ TCP</td>
    <td>ose_node_sg</td>
    <td>-</td>
    </tr>
    <tr>
    <td><code>ose_node_sg</code></td>
    <td>Private</td>
    <td>Outbound</td>
    <td>All</td>
    <td>-</td>
    <td>All</td>
    </tr>
    </tbody>
    </table>

3. Validate your deployment.  
    ```sh
    terraform show
    ```
    {: pre}


## Lesson 3: Deploy Red Hat OpenShift Container Platform on your classic infrastructure
{: #deploy_openshift}

Deploy Red Hat OpenShift Container Platform on the {{site.data.keyword.cloud_notm}} classic infrastructure resources that you created earlier.
{: shortdesc}

During the deployment the following cluster components are set up and configured: 
- 1 OpenShift Container Platform master node
- 3 OpenShift Container Platform infrastructure nodes
- 2 OpenShift Container Platform application nodes
- 1 OpenShift Container Platform Bastion node

For more information, about Red Hat OpenShift Container Platform components, see the [Architecture Overview ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.9/architecture/index.html).

1. Retrieve the pool ID for your Red Hat account. 
    1. From the OpenShift installation directory `/go/bin/terraform-ibm-openshift` inside your container, log in to your Bastion node by using a secure shell. 
        ```sh
        ssh root@$(terraform output bastion_public_ip)
        ```
        {: pre}

    2. Enter **yes** to all security questions to proceed. You are now logged in to your Bastion node. 

        Example output: 
        ```text
        root@bastion-ose-1a2b3c1234 #
        ```
        {: screen}

    3. Remove any previous registration of the Bastion node. 
        ```sh
        subscription-manager unregister
        ```
        {: pre}

    4. Import the `gpg` public key for Red Hat by using the Red Hat Package Manager. 
        ```sh
        rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
        ```
        {: pre}

    5. Register your Bastion node with the Red Hat Network. Enter the user name and password for your Red Hat account. 
        ```sh
        subscription-manager register --serverurl subscription.rhsm.redhat.com:443/subscription --baseurl cdn.redhat.com --username <redhat_username> --password <redhat_password>

        ```
        {: pre}

    6. Find your OpenShift **Pool ID**. For example, the pool ID in the following example is `1a2345bcd6789098765abcde43219bc3`.
        ```sh
        subscription-manager list --available --matches '*OpenShift Container Platform*'

        ```
        {: pre}

        Example output: 
        ```text
        +-------------------------------------------+
        Available Subscriptions
        +-------------------------------------------+
        Subscription Name:   30 Day Self-Supported Red Hat OpenShift Container Platform, 2-Core Evaluation
        Provides:            Red Hat Ansible Engine
        Red Hat Software Collections (for RHEL Server for IBM Power LE)
        Red Hat OpenShift Enterprise Infrastructure
        Red Hat JBoss Core Services
        Red Hat Enterprise Linux Fast Data path
        Red Hat OpenShift Container Platform for Power
        JBoss Enterprise Application Platform
                                    :
        Red Hat OpenShift Container Platform Client Tools for Power
        Red Hat Enterprise Linux Fast Datapath (for RHEL Server for IBM Power LE)
        Red Hat OpenShift Enterprise JBoss EAP add-on
        Red Hat OpenShift Container Platform
        Red Hat Gluster Storage Management Console (for RHEL Server)
        Red Hat OpenShift Enterprise JBoss A-MQ add-on
        Red Hat Enterprise Linux for Power, little endian Beta
        Red Hat OpenShift Enterprise Client Tools
                                    :
        Red Hat OpenShift Enterprise Application Node
                                    :
        Red Hat OpenShift Service Mesh
                                    :
        Red Hat OpenShift Enterprise JBoss FUSE add-on
        SKU:                 SER0419
        Contract:            123456789
        Pool ID:             1a2345bcd6789098765abcde43219bc3
        Provides Management: Yes
        Available:           10
        Suggested:           1
        Service Level:       Self-Support
        Service Type:        L1-L3
        Subscription Type:   Stackable
        Starts:              12/03/2018
        Ends:                01/02/2019
        System Type:         Physical
        ```
        {: screen}

    7. Exit the secure shell to return to your OpenShift installation directory inside your container. 
        ```sh
        exit
        ```
        {: pre}

        Example output: 
        ```text
        logout
        Connection to 169.47.XXX.XX closed.
        /go/bin/terraform-ibm-openshift #
        ```
        {: screen}

2. Finish setting up and registering the nodes with the Red Hat Network. 
      ```sh
      make rhn_username=<rhn_username> rhn_password=<rhn_password> pool_id=<pool_ID> rhn_register
      ```
     {: pre}

    When you create the nodes, the following software and Red Hat subscriptions are automatically downloaded and installed on the nodes for you: 

    **Software packages:**

    <table>
    <thead>
    <th>Software</th>
    <th>Version</th>
    </thead>
    <tbody>
    <tr>
    <td>Red Hat® Enterprise Linux 7.4 x86_64</td>
    <td>kernel-3.11.0.x</td>
    </tr>
    <tr>
    <td>Atomic-OpenShift (<code>master/clients/node/sdn-ovs/utils</code>)</td>
    <td>3.11.x.x</td>
    </tr>
    <tr>
    <td>Docker</td>
    <td>1.12.x</td>
    </tr>
    <tr>
    <td>Ansible</td>
    <td>2.3.2.x</td>
    </tr>
    </tbody>
    </table>

    **Red Hat subscription channels and `rpm` packages:**

    <table>
    <thead>
    <th>Channel</th>
    <th>Repository Name</th>
    </thead>
    <tbody>
    <tr>
    <td>Red Hat® Enterprise Linux 7 Server (RPMs)</td>
    <td><code>rhel-7-server-rpms</code></td>
    </tr>
    <tr>
    <td>Red Hat® OpenShift Enterprise 3.11 (RPMs)</td>
    <td><code>rhel-7-server-ose-3.11-rpms</code></td>
    </tr>
    <tr>
    <td>Red Hat® Enterprise Linux 7 Server - Extras (RPMs)</td>
    <td><code>rhel-7-server-extras-rpms</code></td>
    </tr>
    <tr>
    <td>Red Hat® Enterprise Linux 7 Server - Fast Datapath (RPMs)</td>
    <td><code>rhel-7-fast-datapath-rpms</code></td>
    </tr>
    </tbody>
    </table>

2. Prepare the master, infrastructure, and application nodes for the OpenShift installation.   
    ```sh
    make openshift
    ```
    {: pre}

    If the installation fails with the error `module.post_install.null_resource.post_install: error executing "/tmp/terraform_1700732344.sh": wait: remote command exited without exit status or exit signal`, go to the [{{site.data.keyword.cloud_notm}} classic infrastructure console](https://cloud.ibm.com/classic), and click **Devices** > **Device List**. Then, find the affected virtual server and from the actions menu, perform a soft reboot. 
    {: tip}

    Example output: 
    ```text
    Outputs:

    app_hostname = [
    IBM-OCP-93735f7b3d-app-0
    ]
    app_private_ip = [
        10.72.12.13
    ]
    app_public_ip = [
        158.123.12.126
    ]
    bastion_hostname = IBM-OCP-93735f7b3d-bastion
    bastion_private_ip = 10.72.12.14
    bastion_public_ip = 158.123.12.125
    infra_hostname = [
        IBM-OCP-12345a1a2b-infra-0
    ]
    infra_private_ip = [
        10.72.12.13
    ]
    infra_public_ip = [
        158.123.12.123
    ]
    master_hostname = [
        IBM-OCP-12345a1a2b-master-0
    ]
    master_private_ip = [
        10.72.12.12
    ]
    master_public_ip = [
        158.123.12.124
    ]
    ```
    {: screen}

3. Note the **master_hostname** and **master_public_ip** that was assigned to your master node. 
    To show all your resources with the assigned host names and IP addresses, run `terraform show`. 
    {: tip}

4. Exit your container. 
    ```sh
    exit
    ```
    {: pre}

4. On your local machine, add the master node as a host to your local `/etc/hosts` file. 
    1. Open the `/etc/hosts` file. 
        ```sh
        sudo vi /etc/hosts
        ```
        {: pre}

    2. Insert the following line to the end of your file. 
        ```sh
        <master_public_ip> <master_hostname>
        ```
        {: codeblock}

5. Open the OpenShift console.
    ```sh
    open https://$(terraform output master_public_ip):8443/console
    ```
    {: pre}

6. Set up users and authentication for your OpenShift cluster. The OpenShift Container Platform master includes a built-in `OAuth` server. By default, this `OAuth` server is set up to deny all authentication. To let developers and administrators authenticate with the cluster, follow the steps in [Configuring access and authentication ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/configuring_authentication.html#install-config-configuring-authentication) to set up access for your cluster. 

7. Configure your Docker registry. During the creation of your cluster, an internal, integrated Docker registry is automatically set up for you. You can use the registry to build container images from your source code, deploy them, and manage their lifecycle. For more information, see [Registry Overview ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html#install-config-registry-overview). 

8. Configure your cluster router to enable incoming non-SSH network traffic for your cluster. For more information, see [Router Overview ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/router/index.html#install-config-router-overview). 

## Lesson 4: Deploy an app in your Red Hat OpenShift cluster
{: #deploy_app}

With your OpenShift cluster up and running, you can now deploy your first app in the cluster. 
{: shortdesc}

1. Log in to the master node. 
    ```sh
    ssh -t -A root@$(terraform output master_public_ip)
    ```
    {: pre}

2. Log in to the OpenShift client. Enter **admin** as your user name and **test123** as your password, or use any other user name and password that you set up earlier. 
    ```sh
    oc login https://$(terraform output master_public_ip):8443
    ```
    {: pre} 

3. Create a project directory where you can store all your app files and configurations. 
    ```sh
    oc new-project <project_name>
    ```
    {: pre}

4. Deploy the app. In this example, `nginx` is deployed to your cluster.
    ```sh
    oc new-app --name=nginx --docker-image=bitnami/nginx
    ```
    {: pre}

5. Create a service for your `nginx` app to expose your app inside the cluster. 
    ```sh
    oc expose svc/nginx
    ```
    {: pre}

6. Edit your service and change the service type to **NodePort**. 
    ```sh
    oc edit svc/nginx
    ```
    {: pre}

7. Access your `nginx` app from the internet.  
    1. Get the public route that was assigned to your `nginx` app. You can find the route in the **HOST/PORT** column of your command line output. 
        ```sh
        oc get routes
        ```
        {: pre} 

        Example output: 
        ```text
        NAME            HOST/PORT                                      PATH      SERVICES        PORT      TERMINATION   WILDCARD
        nginx-example   nginx-example-new.apps.158.123.12.123.xip.io             nginx-example   all                   None
        ```
        {: screen}

    2. In your preferred web browser, open your app by using the public route. 
        ```text
        http://nginx-example-new.apps.158.176.91.200.xip.io
        ```
        {: codeblock}

</br>

**What's next?**</br>
Great! You successfully installed Red Hat OpenShift Container Platform on {{site.data.keyword.cloud_notm}} classic infrastructure and deployed your first app to your OpenShift cluster. Now you can try out one of the following features:  

- [Explore other features in Red Hat OpenShift Container Platform ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/welcome/index.html). 
- Remove your OpenShift cluster by running the `make destroy` command. 



