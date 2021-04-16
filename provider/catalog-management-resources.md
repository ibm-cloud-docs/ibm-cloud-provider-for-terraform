---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-16"

keywords: terraform catalog management resources, terraform catalog offering instance, catalog management, catalog management offering instance, catalog management offering, catalog management version

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



# Catalog Management resources 
{: #cm-resources}

Create, modify, or delete [{{site.data.keyword.cloud_notm}} catalog management](/docs/cli?topic=cli-manage-catalogs-plugin) resources. 
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}



## `ibm_cm_catalog`
{: #cm-catalog}

Create, modify, or delete an `cm_catalog` resources. You can manage the settings for all catalogs across your account. For more information, about managing catalog, refer to [catalog management settings](/docs/account?topic=account-account-getting-started).
{: shortdesc}


### Sample Terraform code
{: #cm-catalog-sample}


```
resource "ibm_cm_catalog" "cm_catalog" {
  label = "placeholder"
  short_description = "placeholder"
}
```
{: codeblock}

### Input parameters
{: #cm-catalog-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | ------ | -------- |
| `label` | String | Required | The display name in the requested language.| Yes |
| `short_description` | String | Optional | The short description in the requested language.| Yes |
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-catalog-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the `cm_catalog`.|
| `url` | String | The URL for this specific catalog.|
| `crn` | String | The CRN associated with the catalog.|
| `offerings_url` | String | The URL path to offerings.|
{: caption="Table: Available output parameters" caption-side="top"}


## `ibm_cm_offering`
{: #cm-offering}

Create, modify, or delete an `cm_offering` resources. You can manage the settings for all catalogs across your account. For more information, about managing catalog, refer to [catalog management settings](/docs/account?topic=account-account-getting-started).
{: shortdesc}

### Sample Terraform code
{: #cm-offering-sample}


```
resource "ibm_cm_offering" "cm_offering" {
  catalog_id = "catalog_id"
  label = "placeholder"
  tags = [ "placeholder" ]
}
```
{: codeblock}

### Input parameters
{: #cm-offering-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | --------| 
| `catalog_identifier` | String | Required | Catalog identifier.|
| `label` | String | Optional | Display the name in the requested language.|
| `tags` | List | Optional |  The list of tags associated with the catalog.|
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-offering-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the `cm_offering`.|
| `url` | String | The URL for the specific offering.|
| `crn` | String | The CRN for the specific offering.|
| `name` | String | The programmatic name of the offering.|
| `short_description` | String | The short description in the requested language.|
| `long_description` | String | The long description in the requested language.|
| `permit_request_ibm_public_publish` | String | Is it permitted to request publishing to {{site.data.keyword.IBM_notm}} or public.|
| `ibm_publish_approved` | String | Indicates if the offering has been approved for use by all IBMers.|
| `public_publish_approved` | String | Indicates if the offering has been approved for use by all {{site.data.keyword.cloud_notm}} users.|
| `public_original_crn` | String | The original offering CRN has published.|
| `publish_public_crn` | String | The CRN of the public catalog entry of an offering.|
| `portal_approval_record` | String | The portal's approval record ID.|
| `portal_ui_url` | String | The portal console URL.|
| `catalog_id` | String | The ID of the catalog containing this offering.|
| `catalog_name` | String | The name of the catalog.|
| `disclaimer` | String | A disclaimer for the offering.|
| `repo_info` | String | Repository information for an offerings.|
| `repo_info.token` | String | Token for the private repository.|
| `repo_info.type` | String | The public or enterprise GitHub.|
{: caption="Table: Available output parameters" caption-side="top"}


## `ibm_cm_offering_instance`
{: #cm-offering-instance}

Create, modify, or delete an `ibm_cm_offering_instance` resources. You can manage the settings for all catalogs across your account. Management tasks include setting the visibility of the {{site.data.keyword.cloud_notm}} catalog and controlling access to products in the public catalog and private catalogs for users in your account. For more information, about managing catalog, refer to [catalog management settings](/docs/account?topic=account-account-getting-started).
{: shortdesc}


### Sample Terraform code
{: #cm-offering-instance-sample}


```
resource "ibm_cm_offering_instance" "cm_offering_instance" {
  catalog_id = "catalog_id"
  label = "placeholder"
  kind_format = "operator"
  version = "placeholder"
  cluster_id = "placeholder"
  cluster_region = "placeholder"
  cluster_namespaces = [ "placeholder", "placeholder2" ]
  cluster_all_namespaces = false
}
```
{: codeblock}

### Input parameters
{: #cm-offering-instance-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `label` | String | Required | The label for this instance.|
| `catalog_id` | String | Required | The catalog ID an instance  is created.|
| `offering_id` | String | Required | The offering ID an instance is created .|
| `kind_format` | String | Required | The format an instance such as `helm`, `operator`.|
| `version` | String | Required | The version an instance was installed from (but not from the version ID).|
| `cluster_id` | String | Required | The cluster ID.|
| `cluster_region` | String | Required | The cluster region for example, `us-south`.|
| `cluster_namespaces`| List | Required | The list of target namespaces to install into.|
| `cluster_all_namespaces`| Bool | Required | Designate to install into all namespaces.|
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-offering-instance-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the `cm_offering_instance`.|
| `url` | String | The URL reference to an object.|
| `crn` | String | The platform CRN for an instance.|
{: caption="Table: Available output parameters" caption-side="top"}


## `ibm_cm_version`
{: #cm-version}

Create, modify, or delete an `cm_version` resources. For more information, about managing catalog version, refer to [updating your software](/docs/account?topic=account-update-private).
{: shortdesc}

### Sample Terraform code
{: #cm-version-sample}


```
resource "cm_version" "cm_version" {
  catalog_identifier = "catalog_identifier"
  offering_id = "offering_id"
  zipurl = "placeholder"
}
```
{: codeblock}

### Input parameters
{: #cm-version-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource  |
| ------------- |-------------| ----- | --------| ------ |
| `catalog_identifier` | String | Required | Catalog identifier.| Yes |
| `offering_id` | String | Required | Offering identification.|
| `tags` | List | Optional |  The tags array.| Yes |
|  `target_kinds` | List | Optional | The target kinds. Current supported values are `iks`, `roks`, `vcenter`, and `terraform`.| Yes |
| `content` | TypeString | Optional | The byte array representing the content to import. Currently supports only `OVA` images.| Yes |
| `zipurl` | String | Optional | The URL path to `.zip` location. If not specified, must provide content in the body of the call.| Yes |
| `target_version` | String | Optional | The version value for the new version, if not found in the `zip` URL package content.| Yes |
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-version-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier and version locator of the version.|
| `crn` | String | The CRN version.|
| `url` | String | The URL for the specific offering.|
| `version` | String | Version of the content type.|
| `sha` | String | The hash of the content.|
| `catalog_id` | String | The catalog ID.|
| `kind_id` | String | The kind ID.|
| `repo_url` | String | The URL of the content repository.|
| `source_url` | String | The source URL of the content repository, for example, Git repository.|
| `tgz_url` | String | File used to onboard the version.|
{: caption="Table: Available output parameters" caption-side="top"}
