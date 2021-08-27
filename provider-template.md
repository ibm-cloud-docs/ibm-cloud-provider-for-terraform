---

copyright:
  years: 2017, 2021
lastupdated: "2021-08-27"

keywords: provider templates, schematics template

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

## Onboard to IBM Cloud private catalog
{: #provider-onboard}

Click the **Onboard to IBM Cloud catalog** button to automatically load the following sample terraform templates into your catalog. In order to run this automation, press the **Create** button in **Create an action** page in the console.
{: shortdesc}

For more information, about how the Ansible based automation is configured to load the template to private catalogs? refer to [Onboard to IBM Catalog readme file](https://github.com/Cloud-Schematics/onboard-to-ibm-catalog/blob/main/README.md).
{: note}

<img src="images/onboardtoibmcatalog.png" usemap="#image-map2"><map name="image-map2"><area target="_blank" alt="bulk onboard Terraform templates into private catalog" title="onboard Terraform template to private catalog" href="https://cloud.ibm.com/schematics/actions/create?name=ansible-is-instance-actions&url=https://github.com/Cloud-Schematics/onboard-to-ibm-catalog" coords="1,1,200,40" shape="rect"></map>

## Using sample templates
{: #provider-sample}

The following sample templates allows you to provision your resource by using {{site.data.keyword.bpshort}}. 

In the **Workspace details** page, click **Next** button to view the **Create** button active to create {{site.data.keyword.bpshort}} workspace.
{: note}

|  Repository link | Description | Link to provision |
| ---- | ---- | --- |
| [Add all users to new account](https://github.com/Cloud-Schematics/add-all-users-to-new-account)| Adds all the IAM users from one account into a second account. | <img usemap="#deploybutton_mapcs1" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs1" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/add-all-users-to-new-account&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Autoscale the Classic virtual servers VSI on {{site.data.keyword.cloud_notm}}](https://github.com/Cloud-Schematics/classic-vsi-autoscaling-solution) | Perform classic infrastructure autoscaling by using {{site.data.keyword.bpshort}}, {{site.data.keyword.openwhisk_short}} and Sysdig | <img usemap="#deploybutton_mapcs2" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs2" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/classic-vsi-autoscaling-solution&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [ {{site.data.keyword.containerlong_notm}} logging and monitoring agents](https://github.com/Cloud-Schematics/iks-logging-and-monitoring) | Automate the deployment of logging and monitoring agents onto your {{site.data.keyword.containerlong_notm}} on {{site.data.keyword.vsi_is_short}} cluster. | <img usemap="#deploybutton_mapcs3" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs3" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-logging-and-monitoring&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Deploy Ingress app](https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-ingress-app) | Deploy an app to an {{site.data.keyword.containerlong_notm}} on {{site.data.keyword.vsi_is_short}} cluster by using Ingress.| <img usemap="#deploybutton_mapcs4" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs4" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-ingress-app&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Deploy Load Balancer app](https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-load-balancer-app) | Deploy a Load Balancer app on {{site.data.keyword.containerlong_notm}} on {{site.data.keyword.vsi_is_short}}.| <img usemap="#deploybutton_mapcs5" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs5" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/iks-on-vpc-deploy-demo-load-balancer-app&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [KMS encrypted cross region {{site.data.keyword.cos_full_notm}} bucket ](https://github.com/Cloud-Schematics/kms-encrypted-cos-bucket) | Create an {{site.data.keyword.cos_full_notm}} encrypted with {{site.data.keyword.keymanagementservicelong_notm}}. | <img usemap="#deploybutton_mapcs6" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs6" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/kms-encrypted-cos-bucket&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [LogDNA provider](https://github.com/Cloud-Schematics/logdna-provider-example) | Use the LogDNA Terraform provider with {{site.data.keyword.cloud_notm}}. | <img usemap="#deploybutton_mapcs7" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs7" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/logdna-provider-example&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multitier Bastion VPC LAMP](https://github.com/Cloud-Schematics/multitier-bastion-vpc-lamp) | Provision infrastructure to deploy {{site.data.keyword.vsi_is_short}} with SSH access and Bastion Host for {{site.data.keyword.redhat_notm}} Ansible.| <img usemap="#deploybutton_mapcs8" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs8" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multitier-bastion-vpc-lamp&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multitier VPC network](https://github.com/Cloud-Schematics/multitier-vpc-network) | Create a multitier {{site.data.keyword.vsi_is_short}} in a single region upto 3 zones. Also create an ACL and public gateways for each zone.| <img usemap="#deploybutton_mapcs9" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs9" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multitier-vpc-network&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Multitier cluster workspace](https://github.com/Cloud-Schematics/multizone-iks-on-vpc-cluster) | Create an {{site.data.keyword.containerlong_notm}} cluster on an existing {{site.data.keyword.vsi_is_short}} network and enables private Application Load Balancers.| <img usemap="#deploybutton_mapcs10" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs10" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/multizone-iks-on-vpc-cluster&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [{{site.data.keyword.openshiftshort}} cluster](https://github.com/Cloud-Schematics/openshift-cluster) | {{site.data.keyword.cloud_notm}} Terraform template to deploy {{site.data.keyword.openshiftshort}} cluster. | <img usemap="#deploybutton_mapcs11" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs11" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/openshift-cluster&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [{{site.data.keyword.openshiftshort}} development cluster](https://github.com/Cloud-Schematics/openshift-dev-cluster) | Provision a new team development {{site.data.keyword.openshiftshort}} cluster that are preconfigured with the {{site.data.keyword.cloud_notm}} operator, {{site.data.keyword.redhat_notm}} CodeReady workspaces, and CodeReady pipelines.| <img usemap="#deploybutton_mapcs11" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs11" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/openshift-dev-cluster&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Monitoring Sysdig provider example](https://github.com/Cloud-Schematics/sysdig-provider-example) | Use the monitoring Sysdig Terraform Provider with the {{site.data.keyword.cloud_notm}}. | <img usemap="#deploybutton_mapcs12" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs12" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/sysdig-provider-example&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [Observability service](https://github.com/Cloud-Schematics/terraform-ibm-observability) | Create an instance of {{site.data.keyword.loganalysislong_notm}}, {{site.data.keyword.monitoringlong_notm}}, and {{site.data.keyword.at_full_notm}} in your account.| <img usemap="#deploybutton_mapcs13" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs13" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/terraform-ibm-observability&terraform_version=terraform_v0.13" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
| [VSI workspace with load balancer](https://github.com/Cloud-Schematics/vpc-vsi-with-volumes-and-lb) | Create {{site.data.keyword.vsi_is_short}} with block storage volumes connected to a {{site.data.keyword.alb_full}}. | <img usemap="#deploybutton_mapcs14" alt="Auto deployment button"  src="images/autodeploy_button.png"><map name="deploybutton_mapcs14" alt="This image leads to create a workspace."><area alt="Deploy to IBM Cloud" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/Cloud-Schematics/vpc-vsi-with-volumes-and-lb&terraform_version=terraform_v0.12" target="_blank" coords="1,3,139,20"  shape="rect"></map>|
{: caption="Terraform templates to provision resource using {{site.data.keyword.bpshort}} workspace" caption-side="top"}

