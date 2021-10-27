---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-27"

keywords: terraform templates, templates, sample terraform templates, private catalog

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# Sample Terraform templates for {{site.data.keyword.cloud_notm}}
{: #provider-template}

Explore the sample {{site.data.keyword.cloud}} Terraform templates, and try your templates by using {{site.data.keyword.bpshort}} workspace.

Deploy [Sample templates](#sample-templates) by using {{site.data.keyword.cloud_notm}} service. <br>
Browse [Code snippets](#code-snippets) by {{site.data.keyword.cloud_notm}} service.

## Sample templates
{: #sample-templates}

Following sample templates allows you to provision resource by using {{site.data.keyword.bpshort}} workspace. 

- [Kubernetes and {{site.data.keyword.openshiftshort}}](#kubnernetes-openshift)
- [VPC infrastructure](#vpc-templates)
- [Observability](#observability-templates)
- [Storage](#storage-templates)
- [Classic infrastructure service](#classic-infra-templates)
- [Account management and IAM](#account-mgt-iam)

## Onboard to {{site.data.keyword.cloud_notm}} private catalog
{: #provider-onboard}

You can click the **Onboard to {{site.data.keyword.cloud_notm}} catalog** button to automatically load the following sample Terraform templates into your catalog. In order to run the automation, click the **Create** button in **Create an action** page in the console.
{: shortdesc}

For more information, about how the Ansible based automation is configured to load the template to private catalogs? refer to [Onboard to IBM Catalog readme file](https://github.com/Cloud-Schematics/onboard-to-ibm-catalog/blob/main/README.md){: external}.
{: note}

<img src="images/onboardtoibmcatalog.png" usemap="#image-map2"><map name="image-map2"><area target="_blank" alt="bulk onboard Terraform templates into private catalog" title="onboard Terraform template to private catalog" href="https://cloud.ibm.com/schematics/actions/create?name=myprivatecatalogaction&url=https://github.com/Cloud-Schematics/onboard-to-ibm-catalog" coords="1,1,200,40" shape="rect"></map>

## Code snippets
{: #code-snippets}

The code snippets provides the templates that you can use to understand how to configure {{site.data.keyword.cloud_notm}} service. You can also use the snippets as a starting point for your custom templates.
{: shortdesc}

- [API Gateway](#api-gwy-snippet)
- [Certificate Manager](#cert-mgr-snippet)
- [Cloud Databases templates](#cloud-db-snippet)
- [Cloud Foundry](#cloud-foundry-snippet)
- [Direct Link](#dl-snippet)
- [DNS templates](#dns-snippet)
- [Event Streams](#event-stream-snippet)
- [Functions](#func-snippet)
- [Identity & Access (IAM)](#iam-snippet)
- [Internet templates ](#internet-snippet)
- [Key Management Service](#kms-snippet)
- [Kubernetes templates](#kubernetes-snippet)
- [Object Storage templates](#cos-snippet)
- [Power Systems templates](#power-sys-snippet)
- [Resource Management templates](#resource-mgt-snippet)
- [Schematics templates](#schematics-snippet)
- [Transit Gateway templates](#transit-gwy-snippet)
- [VPC infrastructure templates (Gen 2 compute)](#vpc-gen2-snippet)


## Templates
{: #sample}

### Kubernetes and {{site.data.keyword.openshiftshort}}
{: #kubnernetes-openshift}

In the **Workspace details** page, click **Next** button to view the **Create** button active to create {{site.data.keyword.bpshort}} workspace.
{: note}

|  Template | Description | Provision |
| ---- | ---- | --- |
| [Kubernetes cluster on VPC](https://github.com/Cloud-Schematics/multizone-iks-on-vpc-cluster) | Provision of a Kubernetes cluster on an existing VPC network, with private application load balancers.| <img usemap="#deploybutton_mapk01" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapk01" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multizone-iks-on-vpc-cluster&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [{{site.data.keyword.openshiftshort}} cluster on classic infrastructure](https://github.com/Cloud-Schematics/openshift-cluster) | Provision of a simple Red Hat OpenShift cluster on Classic infrastructure. | <img usemap="#deploybutton_mapk02" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapk02" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/openshift-cluster&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [{{site.data.keyword.openshiftshort}} cluster on Classic infrastrucutre for development environment](https://github.com/Cloud-Schematics/openshift-dev-cluster) | Provision of a Red Hat Openshift cluster on Classic infrastructure for a development team with {{site.data.keyword.cloud_notm}} operation, Red Hat CodeReady.| <img usemap="#deploybutton_mapk03" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapk03" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/openshift-dev-cluster&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Microservices with ingress on Kubernetes cluster](https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-ingress-app) | Deploy a sample app with ingress on your existing Kubernetes cluster on VPC.| <img usemap="#deploybutton_mapk04" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapk04" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-ingress-app&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Microservices with load balancer on Kubernetes cluster](https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-load-balancer-app) | Deploy a sample app with load balance on your existing Kubernetes cluster on VPC.| <img usemap="#deploybutton_mapk05" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapk05" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-load-balancer-app&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Secured {{site.data.keyword.openshiftlong_notm}} cluster on VPC](https://github.com/Cloud-Schematics/secure-openshift-cluster) | Provisioning secured {{site.data.keyword.openshiftlong_notm}} cluster with automation of forwarding observability capability by using VPC.| <img usemap="#deploybutton_mapk06" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapk06" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/secure-openshift-cluster&terraform_version=terraform_v1.0" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Kubernetes and {{site.data.keyword.openshiftshort}} Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}

Rolling - Separate subnet for running production workload and bastion worker.
Blue/Green - Fault Tolerance during deployments by maintaining two similar environments. Also isolation between the prod and pre-prod environment on the network level by using 2 subnets.

### VPC infrastructure
{: #vpc-templates}

|  Template | Description | Provision |
| ---- | ---- | --- |
| [Multiple VSIs on VPC with block storage volume and a load balancer](https://github.com/Cloud-Schematics/vpc-vsi-with-volumes-and-lb) | Provision multiple virtual servers each with a block storage volume on VPC, across a number of subnets, and connected with a single load balancer. | <img usemap="#deploybutton_mapvpc01" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc02" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/vpc-vsi-with-volumes-and-lb&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multiple VPC running on production workload with a bastion worker for Rolling deployment](https://github.com/Cloud-Schematics/vpc-bastion-rolling-deploy) | Provisioning VSIs on a VPC infrastructure to separate subnet for running production workload and a bastion worker for Rolling deployment. | <img usemap="#deploybutton_mapvpc02" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc02" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/vpc-bastion-rolling-deploy&terraform_version=terraform_v1.0" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multiple VPC to maintain the fault tolerance during Blue-Green deployment](https://github.com/Cloud-Schematics/vpc-bastion-bluegreen-deploy) | Provisioning VSIs on a VPC infrastructure for fault tolerance during deployments by maintaining two similar environments. Also isolation between the production and pre-production environment on the network level by using 2 subnets. | <img usemap="#deploybutton_mapvpc03" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc03" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/vpc-bastion-bluegreen-deploy&terraform_version=terraform_v1.0" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multi-tier VPC with bastion and VSIs](https://github.com/Cloud-Schematics/multitier-bastion-vpc-lamp) | Provision multi-tier infrastructure with VPC, SSH, Bastion host, front-end, and backend servers.| <img usemap="#deploybutton_mapvpc04" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc04" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multitier-bastion-vpc-lamp&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multi-zone VPC network](https://github.com/Cloud-Schematics/gcat-multizone-vpc) | Provision of a multi-zone infrastructure with VPC, in a single region up to 3 zones or more, ACL and public gateways.| <img usemap="#deploybutton_mapvpc05" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc05" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/gcat-multizone-vpc&terraform_version=terraform_v1.0" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multi-zone VPCs connecting using Transit Gateway](https://github.com/Cloud-Schematics/gcat-vpc-hub-spoke-cluster) | Provision of two multi-zone VPCs and connects them through the IBM Cloud Transit Gateway. Also, provision a `ROKS` cluster on the spoke VPC and bastion VSI on the OpenShift hub VPC.| <img usemap="#deploybutton_mapvpc06" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc06" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/gcat-vpc-hub-spoke-cluster&terraform_version=terraform_v1.0" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multi-tier landing zone with IAM and resource group access for a catalog offering](https://github.com/Cloud-Schematics/gcat-landing-zone-catalog) | Provision a resource group, a VPC in the resource group, IAM access groups, and invites users to those access groups. This module configures the environment using a JSON object stored in Cloud Object Storage to allow users to configure and update complex environments as part of a catalog offering.| <img usemap="#deploybutton_mapvpc07" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc07" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/gcat-landing-zone-catalog&terraform_version=terraform_v1.0" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multi-zone VPC with bastion using subnet](https://github.com/Cloud-Schematics/gcat-multizone-vpc-bastion-subnet) | Provision multi-zone VPC with a bastion subnet in one zone by reusing a multi-tier VPC template.| <img usemap="#deploybutton_mapvpc08" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapvpc08" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/gcat-multizone-vpc-bastion-subnet&terraform_version=terraform_v1.0" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="VPC Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


### Observability
{: #observability-templates}

|  Template | Description | Provision |
| ---- | ---- | --- |
| [Observability service instance](https://github.com/Cloud-Schematics/terraform-ibm-observability) | Provision an instance of all the Observability services on {{site.data.keyword.cloud_notm}} such as {{site.data.keyword.loganalysislong_notm}}, {{site.data.keyword.monitoringlong_notm}}, and {{site.data.keyword.cloudaccesstrailfull_notm}} in your account.| <img usemap="#deploybutton_mapcs13" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs13" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/terraform-ibm-observability&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Observability agents for Kubernetes cluster](https://github.com/Cloud-Schematics/iks-logging-and-monitoring) | Deploy logging and monitoring agents onto your existing {{site.data.keyword.containerlong_notm}} cluster on VPC. | <img usemap="#deploybutton_mapcs3" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs3" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-logging-and-monitoring&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Configure integrations for Log Analysis service](https://github.com/Cloud-Schematics/logdna-provider-example) | Configure the Log Analysis service instance in {{site.data.keyword.cloud_notm}} to integrate with `Slack`, `PagerDuty` and `Webhooks`. | <img usemap="#deploybutton_mapcs7" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs7" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/logdna-provider-example&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Configure alerts and dashboard for Monitoring services](https://github.com/Cloud-Schematics/sysdig-provider-example) | Configure the monitoring service instance in {{site.data.keyword.cloud_notm}} with alerts and dashboard. | <img usemap="#deploybutton_mapcs12" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs12" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/sysdig-provider-example&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Observability Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


### Storage
{: #storage-templates}

|  Template | Description | Provision |
| ---- | ---- | --- |
| [{{site.data.keyword.cos_full_notm}} bucket with encryption](https://github.com/Cloud-Schematics/kms-encrypted-cos-bucket) | Provision {{site.data.keyword.cos_full_notm}} with {{site.data.keyword.keymanagementservicelong_notm}} integration. | <img usemap="#deploybutton_mapcs6" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs6" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/kms-encrypted-cos-bucket&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Storage Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


### Account management and IAM
{: #account-mgt-iam}

|  Template | Description | Provision |
| ---- | ---- | --- |
| [Clone users to new account](https://github.com/Cloud-Schematics/add-all-users-to-new-account)| Clone all the IAM users from one {{site.data.keyword.cloud_notm}} account into another {{site.data.keyword.cloud_notm}} account. | <img usemap="#deploybutton_mapcs1" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs1" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/add-all-users-to-new-account&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Account management and IAM Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}

### Classic infrastructure service
{: #classic-infra-templates}

|  Template | Description | Provision |
| ---- | ---- | --- |
| [Autoscale the Classic VSIs](https://github.com/Cloud-Schematics/classic-vsi-autoscaling-solution) | Autoscale the classic VSIs using {{site.data.keyword.bpshort}}, {{site.data.keyword.openwhisk_short}}, and Sysdig. | <img usemap="#deploybutton_mapcs2" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs2" alt="This image leads to create a workspace."><area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/classic-vsi-autoscaling-solution&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Classic infrastructure templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


## Snippets
{: #tf_snippet}

### API Gateway templates
{: #api-gwy-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-api-gateway` | Create an <a href="/docs/api-gateway?topic=api-gateway-whatis_apigw">{{site.data.keyword.apigw_full_notm}}</a> service instance to set up an API for an {{site.data.keyword.cloud_ntom}} service of your choice. You can specify the API endpoint that you want to use to access your service, and define subscription keys so that developers can securely consume your API. <br><br> **Resources** <ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_api_gateway_endpoint**</li><li style="margin:0px; padding:0px">**ibm_api_gateway**</li><li style="margin:0px; padding:0px">**ibm_api_gateway_endpoint_subscription**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway)|

### Certificate Manager templates
{: #cert-mgr-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-certificate-manager-order` | Create an {{site.data.keyword.cis_full_notm}} instance with a domain, and use <a href="/docs/certificate-manager?topic=certificate-manager-about-certificate-manager">{{site.data.keyword.cloudcerts_long_notm}}</a> to generate a TLS certificate for this domain.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_cis**</li><li style="margin:0px; padding:0px">**ibm_cis_domain**</li><li style="margin:0px; padding:0px">**ibm_certificate_manager_order**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-certificate-manager/ibm-certificate-manager-order)|

### Cloud Foundry templates
{: #cloud-foundry-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-app` | Create and deploy a Cloud Foundry app in {{site.data.keyword.cloud_notm}}.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**null_resource**</li><li style="margin:0px; padding:0px">**ibm_app_route**</li><li style="margin:0px; padding:0px">**ibm_service_instance**</li><li style="margin:0px; padding:0px">**ibm_service_key**</li><li style="margin:0px; padding:0px">**ibm_app**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-app)|

### Direct Link templates
{: #dl-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-dl-gateway` | Create a speed and reliable direct link gateways, virtual connections, offering information, routers, and ports by using the resources.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_dl_gateway**</li><li style="margin:0px; padding:0px">**ibm_dl_virtual_connection**</li><li style="margin:0px; padding:0px">**ibm_is_vpc**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-direct-link)|

### Event Streams templates
{: #event-stream-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-event-streams` | Create a communication through an Event Streams instance, topic instance, or Kafka consumer application to connect an existing event stream instances and its topic instance by using {{site.data.keyword.bplong_notm}} workspace.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_event_streams_topic**</li><li style="margin:0px; padding:0px">**kafka_consumer_app**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-event-streams)|

### Functions templates
{: #func-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-function-cloudant-trigger` | Create a Cloudant NoSQL service instance and a Python app deployment that creates the **database demo** database in your service instance. Then, you create an action with {{site.data.keyword.cloud_notm}} functions that is triggered when you add or edit documents to your database.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**null_resource**</li><li style="margin:0px; padding:0px">**ibm_service_instance**</li><li style="margin:0px; padding:0px">**ibm_service_key**</li><li style="margin:0px; padding:0px">**ibm_app_route**</li><li style="margin:0px; padding:0px">**ibm_app**</li><li style="margin:0px; padding:0px">**ibm_function_package**</li><li style="margin:0px; padding:0px">**ibm_function_action**</li><li style="margin:0px; padding:0px">**ibm_function_trigger**</li><li style="margin:0px; padding:0px">**ibm_function_rule**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-function-cloudant-trigger)|

### Identity & Access (IAM) templates
{: #iam-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-iam-custom-role` | Create a custom role in IBM {{site.data.keyword.iamshort}} (IAM) for {{site.data.keyword.keymanagementservicelong_notm}}.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_iam_custom_role**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-custom-role)|
| `ibm-iam-policy` | Create an access policy in IBM {{site.data.keyword.iamshort}} (IAM) to grant permissions for a resource group to a user.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_iam_user_policy**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-policy)|
| `ibm-iam-policy` | Create an access group in {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} and assign this access group permission to a resource group. Then, you add users to your access group and assign these users access to {{site.data.keyword.containerlong_notm}}, classic {{site.data.keyword.cloud_notm}} infrastructure, and Cloud Foundry.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_iam_access_group**</li><li style="margin:0px; padding:0px">**ibm_iam_access_group_policy**</li><li style="margin:0px; padding:0px">**ibm_iam_user_invite**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-user-invite)|

### Key Management Service templates
{: #kms-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-key-management-service` | Create an {{site.data.keyword.cos_full_notm}} service instance with a bucket to store your data and provide a key management service resource for Hyper Protect Crypto Services and Key Protect service instance with a root key. This allow access between these services with an IBM {{site.data.keyword.iamshort}} policy.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_kms_key**</li><li style="margin:0px; padding:0px">**ibm_kp_key**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-kms)|

### Kubernetes templates
{: #kubernetes-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `vpc-classic-cluster` | Create an {{site.data.keyword.containerfull_notm}} cluster in a Virtual Private Cloud (VPC) for Generation 1 compute with worker nodes in a default worker pool that you spread across two zones. You can provision an {{site.data.keyword.cos_full_notm}} service, and bind this service to the cluster.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_is_vpc**</li><li style="margin:0px; padding:0px">**ibm_is_subnet**</li><li style="margin:0px; padding:0px">**ibm_container_vpc_cluster**</li><li style="margin:0px; padding:0px">**ibm_container_vpc_worker_pool**</li><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_container_bind_service**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster/vpc-classic-cluster)|
| `vpc-Gen2-cluster` | Create an {{site.data.keyword.containerfull_notm}} cluster in a Virtual Private Cloud (VPC) for Generation 2 compute with worker nodes in a default worker pool that you spread across two zones. Also, you provision an {{site.data.keyword.cos_full_notm}} service, and bind this service to the cluster.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_is_vpc**</li><li style="margin:0px; padding:0px">**ibm_is_subnet**</li><li style="margin:0px; padding:0px">**ibm_container_vpc_cluster**</li><li style="margin:0px; padding:0px">**ibm_container_vpc_worker_pool**</li><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_container_bind_service**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster/vpc-gen2-cluster)|
| `ibm-iks-classic-ROKS` | Create a Red Hat View GitHub repository on {{site.data.keyword.cloud_notm}} cluster that runs version 3.11 of the View GitHub repository Container Platform.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_container_cluster**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iks-classic-ROKS)|
| `ibm-cluster-update` | Cordon and drain your worker nodes to update the {{site.data.keyword.containerlong_notm}} cluster master and worker nodes to the latest version.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**null_resource**</li><li style="margin:0px; padding:0px">**ibm_container_cluster**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster-update)|
| `cluster-worker-pool-zone` | Create an {{site.data.keyword.containerlong_notm}} cluster with a default worker pool that is spread across two zones. Also, you create another worker pool and bind an {{site.data.keyword.cloud_notm}} service of your choice to the cluster.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_container_cluster**</li><li style="margin:0px; padding:0px">**ibm_container_worker_pool_zone_attachment**</li><li style="margin:0px; padding:0px">**ibm_container_worker_pool**</li><li style="margin:0px; padding:0px">**ibm_service_instance**</li><li style="margin:0px; padding:0px">**ibm_service_key**</li><li style="margin:0px; padding:0px">**ibm_container_bind_service**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster/cluster-worker-pool-zone)|
| `ibm-storage-cos` | Set up Helm in an {{site.data.keyword.containerlong_notm}} cluster to install the {{site.data.keyword.cos_full_notm}} Helm plug-in. Then, you create an {{site.data.keyword.cos_full_notm}} service instance where you can store data from the apps in your cluster. You also learn how to create a Kubernetes persistent volume claim (PVC) to create a bucket in your {{site.data.keyword.cos_full_notm}} instance. Also to deploy an app in the cluster that mounts your {{site.data.keyword.cos_full_notm}} bucket.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_container_bind_service**</li><li style="margin:0px; padding:0px">**kubernetes_secret**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-storage-cos)|
| `ibm-openshift-job` | Create and execute a secured shell script in an {{site.data.keyword.openshiftlong_notm}} cluster by using an Terraform on {{site.data.keyword.cloud_notm}} template. This template creates a Kubernetes configmap that includes a reference to a shell script. Then, you create a pod that mounts the configmap as a volume and executes the shell script.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**kubernetes_secret**</li><li style="margin:0px; padding:0px">**kubernetes_config_map**</li><li style="margin:0px; padding:0px">**kubernetes_job**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-openshift-job)|
| `portworx` | Set up Helm in an {{site.data.keyword.containerlong_notm}} software-defined storage (SDS) cluster to install Portworx as a storage solution. Make sure that this template requires an SDS cluster on Bare Metal worker nodes. After you installed Portworx, you can create persistent volume claims (PVC) to store data on local storage of your worker nodes. For more information, about Portworx and how to create an SDS cluster, see <a href="/docs/containers?topic=containers-portworx">Storing data on SDS with Portworx</a>.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**random_id**</li><li style="margin:0px; padding:0px">**kubernetes_secret**</li><li style="margin:0px; padding:0px">**helm_release**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/portworx)|
| `ibm-lbaas` | Create an {{site.data.keyword.loadbalancer_full}} for a classic virtual server instance. You configure the load balancer to manage incoming HTTPS and HTTP network traffic and set up health monitoring for your virtual server instance.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_compute_ssl_certificate**</li><li style="margin:0px; padding:0px">**ibm_compute_ssh_key**</li><li style="margin:0px; padding:0px">**ibm_compute_vm_instance**</li><li style="margin:0px; padding:0px">**ibm_lbaas**</li></li><li style="margin:0px; padding:0px">**ibm_lbaas_server_instance_attachment**</li><li style="margin:0px; padding:0px">**ibm_lbaas_health_monitor**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-lbaas)|
| `ibm-logdna-cluster-integration` | Create an {{site.data.keyword.cloud_notm}} cluster integration service to configure {{site.data.keyword.cloud_notm}} provider such as Helm, Kubernetes. Then, you can use a  resource role binding to fetch resource key, and agents to log through resource role binding.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**random_id**</li><li style="margin:0px; padding:0px">**kubernetes_role_binding**</li><li style="margin:0px; padding:0px">**helm_release**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-logdna-cluster-integration)|


### Transit Gateway templates
{: #transit-gwy-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-transit-gateway` | Create a transit gateways, list available connections, and locations for the gateways.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_tg_gateway**</li><li style="margin:0px; padding:0px">**ibm_tg_connection**</li><li style="margin:0px; padding:0px">**ibm_is_vpc**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-transit-gateway)|

### Cloud Databases templates
{: #cloud-db-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-database` | Create a classic virtual server instance and an {{site.data.keyword.cloud_notm}} database for PostgreSQL instance, and set up connectivity between the instances.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_compute_vm_instance**</li><li style="margin:0px; padding:0px">**ibm_resource_group**</li><li style="margin:0px; padding:0px">**ibm_database**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-database)|

### DNS templates
{: #dns-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-private-dns` | Create an {{site.data.keyword.vpc_short}} and an {{site.data.keyword.dns_full_notm}} instance, and add the VPC as a permitted network to the DNS service instance. Then, you create different types of DNS records.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_is_vpc**</li><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_dns_zone**</li><li style="margin:0px; padding:0px">**ibm_dns_resource_record**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-private-dns)|

### Internet templates 
{: #internet-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-cis` | Create an {{site.data.keyword.cis_full_notm}} instance and configure the instance with health check monitoring, origin pool, global load-balancing, DNS records, firewall, and limit the rate rules.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_cis**</li><li style="margin:0px; padding:0px">**ibm_cis_domain_settings**</li><li style="margin:0px; padding:0px">**ibm_cis_domain**</li><li style="margin:0px; padding:0px">**ibm_cis_edge_functions_action**</li><li style="margin:0px; padding:0px">**ibm_cis_edge_functions_trigger**</li><li style="margin:0px; padding:0px">**ibm_cis_healthcheck**</li><li style="margin:0px; padding:0px">**ibm_cis_origin_pool**</li><li style="margin:0px; padding:0px">**ibm_cis_global_load_balancer**</li><li style="margin:0px; padding:0px">**ibm_cis_dns_record**</li><li style="margin:0px; padding:0px">**ibm_cis_firewall**</li><li style="margin:0px; padding:0px">**ibm_cis_rate_limit**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cis)|

### Object Storage templates
{: #cos-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-cos-bucket` | Create an <a href="/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage">{{site.data.keyword.cos_full_notm}}</a> service instance in {{site.data.keyword.cloud_notm}} and your first bucket to persistently store data.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_group**</li><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_cos_bucket**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cos-bucket)|

### Power Systems templates
{: #power-sys-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-power` | Create an {{site.data.keyword.powerSys_notm}} instance with a public and a private network that mounts the system volumes. You can also create an SSH key to access the instance.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_pi_key**</li><li style="margin:0px; padding:0px">**ibm_pi_network**</li><li style="margin:0px; padding:0px">**ibm_pi_volume**</li><li style="margin:0px; padding:0px">**ibm_pi_instance**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-power)|

### Resource Management templates
{: #resource-mgt-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-resource-instance` | Create an {{site.data.keyword.cos_full_notm}} service instance with HMAC credentials, and configure custom timeouts for creating, updating, or deleting the instance.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm-resource-instance**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-resource-instance)|

### Schematics templates
{: #schematics-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-schematics` | Retrieve the Terraform on {{site.data.keyword.cloud_notm}} state file and output variables for a {{site.data.keyword.bpshort}} workspace by using a {{site.data.keyword.bpshort}} data source. For more information, about how to use the data source, see <a href="/docs/schematics?topic=schematics-remote-state">Managing cross-workspace state access with Terraform on {{site.data.keyword.cloud_notm}}</a>.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**N/A**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-schematics)|

### VPC infrastructure templates (Gen 2 compute)
{: #vpc-gen2-snippet}

| Name | Description and resources | Code |
| --- | --- | --- |
| `ibm-is-ng` | Create a Virtual Private Cloud (VPC) for Generation 2 compute, configure a VPC load balancer with custom routing rules. Then, add a virtual server instance to your VPC that you can access from the internet by using a public IP address. Then, create another VPC Gen 2 and configure it with a VPN gateway with custom IPSec and IKE networking rules. You also learn how to create VPC Gen 2 block storage volumes.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_is_vpc**</li><li style="margin:0px; padding:0px">**ibm_is_vpc_route**</li><li style="margin:0px; padding:0px">**ibm_is_subnet**</li><li style="margin:0px; padding:0px">**ibm_is_lb**</li><li style="margin:0px; padding:0px">**ibm_is_lb_listener**</li><li style="margin:0px; padding:0px">**ibm_is_lb_listener_policy**</li><li style="margin:0px; padding:0px">**ibm_is_lb_listener_policy_rule**</li><li style="margin:0px; padding:0px">**ibm_is_vpn_gateway**</li><li style="margin:0px; padding:0px">**ibm_is_vpn_gateway_connection**</li><li style="margin:0px; padding:0px">**ibm_is_ssh_key**</li><li style="margin:0px; padding:0px">**ibm_is_instance**</li><li style="margin:0px; padding:0px">**ibm_is_floating_ip**</li><li style="margin:0px; padding:0px">**ibm_is_security_group_rule**</li><li style="margin:0px; padding:0px">**ibm_is_ipsec_policy**</li><li style="margin:0px; padding:0px">**ibm_is_ike_policy**</li><li style="margin:0px; padding:0px">**ibm_is_volume**</li><li style="margin:0px; padding:0px">**ibm_is_public_gateway**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-is-ng)|
