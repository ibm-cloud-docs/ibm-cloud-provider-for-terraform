---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-13"

keywords: terraform templates, templates, sample terraform templates, private catalog

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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


# Sample Terraform templates for {{site.data.keyword.cloud_notm}}
{: #provider-template}

Explore the sample {{site.data.keyword.cloud}} Terraform templates, onboard the templates to your private catalogs, and try your templates by using {{site.data.keyword.bpshort}} workspace.

Deploy [Sample templates](#sample-templates) by using IBM Cloud service. <br>
Browse [Code snippets](#code-snippets) by IBM Cloud service.

## Onboard to IBM Cloud private catalog
{: #provider-onboard}

Click the **Onboard to IBM Cloud catalog** button to automatically load the following sample Terraform templates into your catalog. In order to run this automation, press the **Create** button in **Create an action** page in the console.
{: shortdesc}

For more information, about how the Ansible based automation is configured to load the template to private catalogs? refer to [Onboard to IBM Catalog readme file](https://github.com/Cloud-Schematics/onboard-to-ibm-catalog/blob/main/README.md).
{: note}

<img src="images/onboardtoibmcatalog.png" usemap="#image-map2"><map name="image-map2"><area target="_blank" alt="bulk onboard Terraform templates into private catalog" title="onboard Terraform template to private catalog" href="https://cloud.ibm.com/schematics/actions/create?name=demo-catalogs&url=https://github.com/Cloud-Schematics/onboard-to-ibm-catalog" coords="1,1,200,40" shape="rect"></map>

## Sample templates
{: #sample-templates}

Following are the lsit of sample templates that allows you to provision resource by using {{site.data.keyword.bpshort}} workspace. 

- [Kubernetes and OpenShift](#kubnernetes-openshift)
- [VPC infrastructure](#vpc-templates)
- [Observability](observability-templates)
- [Storage](#storage-templates)
- [Classic infrastructure service](#classic-infra-templates)
- [Account management and IAM](#account-mgt-iam)

## Code snippets
{: #code-snippets}

The code snippets provides the templates that you can use to understand how to configure IBM Cloud service. You can also use the snippets as a starting point for your custom templates.
{: shortdesc}

[API Gateway](#api-gwy-snippet)
[Certificate Manager](#cert-mgr-snippet)
[Cloud Foundry](#cloud-foundry-snippet)
[Direct Link](#dl-snippet)

## Templates
{: #sample}

### Kubernetes and OpenShift
{: #kubnernetes-openshift}

In the **Workspace details** page, click **Next** button to view the **Create** button active to create {{site.data.keyword.bpshort}} workspace.
{: note}

|  Template | Description | Provision |
| ---- | ---- | --- |
| [Kubernetes cluster on VPC](https://github.com/Cloud-Schematics/multizone-iks-on-vpc-cluster) | Provision of a Kubernetes cluster on an existing VPC network, with private application load balancers.| <img usemap="#deploybutton_mapcs10" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs10" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multizone-iks-on-vpc-cluster&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [{{site.data.keyword.openshiftshort}} cluster on classic infrastructure](https://github.com/Cloud-Schematics/openshift-cluster) | Provision of a simple Red Hat OpenShift cluster on Classic infrastructure. | <img usemap="#deploybutton_mapcs11" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs11" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/openshift-cluster&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [{{site.data.keyword.openshiftshort}} cluster on Classic infrastrucutre for development environment](https://github.com/Cloud-Schematics/openshift-dev-cluster) | Provision of a Red Hat Openshift cluster on Classic infrastructure for a development team with IBM Cloud Operation, Red Hat CodeReady.| <img usemap="#deploybutton_mapcs11" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs11" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/openshift-dev-cluster&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Microservices with ingress on Kubernetes cluster](https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-ingress-app) | Deploy a sample app with ingress on your existing Kubernetes cluster on VPC.| <img usemap="#deploybutton_mapcs4" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs4" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-ingress-app&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Microservices with load balancer on Kubernetes cluster](https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-load-balancer-app) | Deploy a sample app with load balance on your existing Kubernetes cluster on VPC.| <img usemap="#deploybutton_mapcs5" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs5" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-load-balancer-app&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Kubernetes and OpenShift Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


### VPC infrastructure
{: #vpc-templates}

|  Repository link | Description | Link to provision |
| ---- | ---- | --- |
| [Multiple VSIs on VPC with block storage volume and a load balancer](https://github.com/Cloud-Schematics/vpc-vsi-with-volumes-and-lb) | Provision multiple virtual servers each with a block storage volume on VPC, across a number of subnets, and connected with a single load balancer. | <img usemap="#deploybutton_mapcs14" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs14" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/vpc-vsi-with-volumes-and-lb&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multi-tier VPC with bastion and VSIs](https://github.com/Cloud-Schematics/multitier-bastion-vpc-lamp) | Provision multi-tier infrastructure with VPC, SSH, Bastion host, front-end, and backend servers.| <img usemap="#deploybutton_mapcs8" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs8" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multitier-bastion-vpc-lamp&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multi-tier VPC network](https://github.com/Cloud-Schematics/multitier-vpc-network) | Provision of a multi-tier infrastructure with VPC, in a single region up to 3 zones, ACL and public gateways.| <img usemap="#deploybutton_mapcs9" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs9" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multitier-vpc-network&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="VPC Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


### Observability
{: #observability-templates}

|  Repository link | Description | Link to provision |
| ---- | ---- | --- |
| [Observability service instance](https://github.com/Cloud-Schematics/terraform-ibm-observability) | Provision an instance of all the Observability services on IBM Cloud such as IBM Cloud Log Analysis, IBM Cloud Monitoring, and IBM Cloud Activity Tracker in your account.| <img usemap="#deploybutton_mapcs13" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs13" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/terraform-ibm-observability&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Observability agents for Kubernetes cluster](https://github.com/Cloud-Schematics/iks-logging-and-monitoring) | Deploy logging and monitoring agents onto your existing {{site.data.keyword.containerlong_notm}} cluster on VPC. | <img usemap="#deploybutton_mapcs3" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs3" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-logging-and-monitoring&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Configure integrations for Log Analysis service](https://github.com/Cloud-Schematics/logdna-provider-example) | Configure the Log Analysis service instance in IBM Cloud to integrate with `Slack`, `PagerDuty` and `Webhooks`. | <img usemap="#deploybutton_mapcs7" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs7" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/logdna-provider-example&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Configure alerts and dashboard for Monitoring services](https://github.com/Cloud-Schematics/sysdig-provider-example) | Configure the monitoring service instance in IBM Cloud with alerts and dashboard. | <img usemap="#deploybutton_mapcs12" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs12" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/sysdig-provider-example&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Observability Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


### Storage
{: #storage-templates}

|  Repository link | Description | Link to provision |
| ---- | ---- | --- |
| [IBM Cloud Object Storage bucket with encryption](https://github.com/Cloud-Schematics/kms-encrypted-cos-bucket) | Provision IBM Cloud Object Storage with IBM Key Protect integration. | <img usemap="#deploybutton_mapcs6" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs6" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/kms-encrypted-cos-bucket&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Storage Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


### Account management and IAM
{: #account-mgt-iam}

|  Repository link | Description | Link to provision |
| ---- | ---- | --- |
| [Clone users to new account](https://github.com/Cloud-Schematics/add-all-users-to-new-account)| Clone all the IAM users from one IBM Cloud account into another IBM Cloud account. | <img usemap="#deploybutton_mapcs1" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs1" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/add-all-users-to-new-account&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Account management and IAM Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}

### Classic infrastructure service
{: #classic-infra-templates}

|  Repository link | Description | Link to provision |
| ---- | ---- | --- |
| [Autoscale the Classic VSIs](https://github.com/Cloud-Schematics/classic-vsi-autoscaling-solution) | Autoscale the classic VSIs using {{site.data.keyword.bpshort}}, {{site.data.keyword.openwhisk_short}}, and Sysdig. | <img usemap="#deploybutton_mapcs2" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs2" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/classic-vsi-autoscaling-solution&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Classic infrastructure templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}


## Snippets
{: #tf_snippet}

### API Gateway templates
{: #api-gwy-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-api-gateway` | Create an <a href="/docs/api-gateway?topic=api-gateway-whatis_apigw">IBM Cloud API Gateway</a> service instance to set up an API for an IBM Cloud service of your choice. You can specify the API endpoint that you want to use to access your service, and define subscription keys so that developers can securely consume your API. <br><br> **Resources** <ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_api_gateway_endpoint**</li><li style="margin:0px; padding:0px">**ibm_api_gateway**</li><li style="margin:0px; padding:0px">**ibm_api_gateway_endpoint_subscription**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway)|


## Certificate Manager templates
{: #cert-mgr-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-certificate-manager-order` | Create an {{site.data.keyword.cis_full_notm}} instance with a domain, and use <a href="/docs/certificate-manager?topic=certificate-manager-about-certificate-manager">IBM Cloud Certificate Manager</a> to generate a TLS certificate for this domain.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_cis**</li><li style="margin:0px; padding:0px">**ibm_cis_domain**</li><li style="margin:0px; padding:0px">**ibm_certificate_manager_order**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-certificate-manager/ibm-certificate-manager-order)|

## Cloud Foundry templates
{: #cloud-foundry-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-app` | Create and deploy a Cloud Foundry app in {{site.data.keyword.cloud_notm}}.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**null_resource**</li><li style="margin:0px; padding:0px">**ibm_app_route**</li><li style="margin:0px; padding:0px">**ibm_service_instance**</li><li style="margin:0px; padding:0px">**ibm_service_key**</li><li style="margin:0px; padding:0px">**ibm_app**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-app)|

## Direct Link templates
{: #dl-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-dl-gateway` | Create a speed and reliable direct link gateways, virtual connections, offering information, routers, and ports by using the resources.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_dl_gateway**</li><li style="margin:0px; padding:0px">**ibm_dl_virtual_connection**</li><li style="margin:0px; padding:0px">**ibm_is_vpc**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-direct-link)|

## Event Streams templates
{: #event-stream-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-event-streams` | Create a communication through an Event Streams instance, topic instance, or Kafka consumer application to connect an existing event stream instances and its topic instance by using {{site.data.keyword.bplong_notm}} workspace.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_resource_instance**</li><li style="margin:0px; padding:0px">**ibm_event_streams_topic**</li><li style="margin:0px; padding:0px">**kafka_consumer_app**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-event-streams)|

## Functions templates
{: #func-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-function-cloudant-trigger` | Create a Cloudant NoSQL service instance and a Python app deployment that creates the **database demo** database in your service instance. Then, you create an action with {{site.data.keyword.cloud_notm}} functions that is triggered when you add or edit documents to your database.<br><br>**Resources**<br>
        <ul style="margin:0px 0px 0px 20px; padding:0px">
        <li style="margin:0px; padding:0px">**null_resource**</li>
        <li style="margin:0px; padding:0px">**ibm_service_instance**</li>
        <li style="margin:0px; padding:0px">**ibm_service_key**</li>
        <li style="margin:0px; padding:0px">**ibm_app_route**</li>
        <li style="margin:0px; padding:0px">**ibm_app**</li>
        <li style="margin:0px; padding:0px">**ibm_function_package**</li>
        <li style="margin:0px; padding:0px">**ibm_function_action**</li>
        <li style="margin:0px; padding:0px">**ibm_function_trigger**</li>
        <li style="margin:0px; padding:0px">**ibm_function_rule**</li>
        </ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-function-cloudant-trigger)|

## Identity & Access (IAM) templates
{: #iam-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-iam-custom-role` | Create a custom role in IBM Cloud Identity and Access Management (IAM) for IBM Cloud Key Protect.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_iam_custom_role**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-custom-role)|
| `ibm-iam-policy` | Create an access policy in IBM Cloud Identity and Access Management (IAM) to grant permissions for a resource group to a user.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_iam_user_policy**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-policy)|

## Key Management Service templates
{: #kms-snippet}

| Name | Description and resources | Access |
| --- | --- | --- |
| `ibm-key-management-service` | Create an {{site.data.keyword.cos_full_notm}} service instance with a bucket to store your data and provide a key management service resource for Hyper Protect Crypto Services and Key Protect service instance with a root key. This allow access between these services with an IBM Cloud Identity and Access Management policy.<br><br>**Resources**<br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**ibm_kms_key**</li><li style="margin:0px; padding:0px">**ibm_kp_key**</li></ul>|[View code snippet](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-kms)|