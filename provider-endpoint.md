---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-04"

keywords: terraform provider, terraform provider private endpoint, private endpoint

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



# Configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform to use the Cloud Service Endpoint
{: #config-provider}

The steps involved in configuring your {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform to use the private Cloud Service Endpoint (CSE) of an {{site.data.keyword.cloud_notm}} service in  public CSE in [Production environment](https://cloud.ibm.com).

You can configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform to communicate with an {{site.data.keyword.cloud_notm}} service by using the respective Cloud Service Endpoint or Private Service Endpoint.
{: shortdesc}

1. Setup the Terraform engine and an {{site.data.keyword.cloud_notm}} Provider plug-in, in {{site.data.keyword.cloud_notm}} virtual machine by using private VLAN. And provision the enabled Virtual Routing and Forwarding (VRF) account.
2. Export the following environment variables on your local machine. For more information, about supported private Cloud Service Endpoints for each {{site.data.keyword.cloud_notm}} service to support in production, see [Use service endpoints](/docs/account?topic=account-vrf-service-endpoint).
3. Initialize the Terraform command line to load the environment variables that you set.

```
terraform init
```
{: pre}

|Service|Environment variable key|Private service endpoint|
|-------------|--------|----------------|
|Account management|`IBMCLOUD_ACCOUNT_MANAGEMENT_API_ENDPOINT`|N/A|
|Certificate manager|`IBMCLOUD_CERTIFICATE_MANAGER_API_ENDPOINT`|N/A|
|Cloud Foundry|`IBMCLOUD_MCCP_API_ENDPOINT`|N/A|
|Cloud functions|`IBMCLOUD_NAMESPACE_API_ENDPOINT`|N/A|
|Containers|`IBMCLOUD_CS_API_ENDPOINT`|[Docs](/docs/containers?topic=containers-plan_clusters#workeruser-master)|
|CIS|`IBMCLOUD_CIS_API_ENDPOINT`|N/A|
|Direct Link|`IBMCLOUD_DL_API_ENDPOINT`|N/A|
|GHoST / Tagging|`IBMCLOUD_GT_API_ENDPOINT`|N/A|
|HPCS|`IBMCLOUD_HPCS_API_ENDPOINT`|N/A|
|IAM|`IBMCLOUD_IAM_API_ENDPOINT`|N/A|
|`IAMPAP`|`IBMCLOUD_IAMPAP_API_ENDPOINT`|N/A|
|ICD|`IBMCLOUD_ICD_API_ENDPOINT`|[Docs](/docs/account?topic=account-vrf-service-endpoint)|
|Key protect|`IBMCLOUD_KP_API_ENDPOINT`|[Docs](/key-protect?topic=key-protect-private-endpoints)|
|Private DNS|`IBMCLOUD_PRIVATE_DNS_API_ENDPOINT`| N/A|
|Resource management|`IBMCLOUD_RESOURCE_MANAGEMENT_API_ENDPOINT`|N/A|
|Resource controller|`IBMCLOUD_RESOURCE_CONTROLLER_API_ENDPOINT`|N/A|
|Resource catalog|`IBMCLOUD_RESOURCE_CATALOG_API_ENDPOINT`|N/A|
|Schematics|`IBMCLOUD_SCHEMATICS_API_ENDPOINT`|[Docs](/docs/schematics?topic=schematics-private-endpoints)|
|Transit Gateway|`IBMCLOUD_TG_API_ENDPOINT`| N/A|
|UAA|`IBMCLOUD_UAA_ENDPOINT`|N/A|
|User management|`IBMCLOUD_USER_MANAGEMENT_ENDPOINT`|N/A|
|VPC Gen2|`IBMCLOUD_IS_NG_API_ENDPOINT`|N/A|

