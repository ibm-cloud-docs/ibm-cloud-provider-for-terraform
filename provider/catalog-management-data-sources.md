---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-05"

keywords:  terraform catalog management data sources, terraform catalog offering instance, catalog management, catalog management offering instance, catalog management offering, catalog management version

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



# Catalog Management data sources 
{: #cm-data-sources}

Review the data sources that you can use to retrieve information about your [{{site.data.keyword.cloud_notm}} catalog management](/docs/cli?topic=cli-manage-catalogs-plugin). All data sources are imported as read-only information. You can reference the output parameters for each data source by using Terraform interpolation syntax.
{: shortdesc}

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}


## `ibm_cm_catalog`
{: #cm-catalog-ds}

Create, modify, or delete an `cm_catalog` resources. You can manage the settings for all catalogs across your account. For more information, about managing catalog, refer to [catalog management settings](/docs/account?topic=account-account-getting-started).
{: shortdesc}


### Sample Terraform code
{: #cm-catalog-dssample}


```
data "cm_catalog" "cm_catalog" {
	catalog_identifier = "catalog_identifier"
}
```
{: codeblock}

### Input parameters
{: #cm-catalog-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | ------ |
| `catalog_identifier` | String | Required | The catalog identifier.|
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-catalog-dsoutput}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the `cm_catalog`.|
| `label` | String | Display the name in the requested language.|
| `short_description` | String | The description in the requested language.|
| `catalog_icon_url` | String | The URL for an icon associated with the catalog.|
| `tags` | String | The list of tags associated with this catalog.|
| `url` | String | The URL for the specific catalog.|
| `crn` | String | The CRN associated with the catalog.|
{: caption="Table: Available output parameters" caption-side="top"}


## `ibm_cm_offering`
{: #cm-offering-ds}

Create, modify, or delete an `cm_offering` data source. You can manage the settings for all catalogs across your account. For more information, about managing catalog, refer to [catalog management settings](/docs/account?topic=account-account-getting-started).
{: shortdesc}

### Sample Terraform code
{: #cm-offering-dssample}


```
data "cm_offering" "cm_offering" {
	catalog_identifier = "catalog_identifier"
	offering_id = "offering_id"
}
```
{: codeblock}

### Input parameters
{: #cm-offering-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | --------| 
| `catalog_identifier` | String | Required | The catalog identifier.|
| `offering_id` | String | Required | The offering identification.|
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-offering-dsoutput}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the `cm_offering`.|
| `url` | String | The URL for the specific offering.|
| `crn` | String | The CRN for the specific offering.|
| `label` | String | Display the name in the requested language.|
| `name` | String | The programmatic name of the offering.|
| `offering_icon_url` | String | The URL for an icon associated with the offering.|
| `offering_docs_url` | String | The URL for an extra documentation with the offering.|
| `offering_support_url` | String | The URL to be displayed in the consumption UI for getting support on the offering.|
| `short_description` | String | The short description in the requested language.|
| `long_description` | String | The long description in the requested language.|
| `permit_request_ibm_public_publish` | String | Is it permitted to request publishing to {{site.data.keyword.IBM_notm}} or public.|
| `ibm_publish_approved` | String | Indicates if the offering has been approved for use by all IBMers.|
| `public_publish_approved` | String | Indicates if the offering has been approved to all {{site.data.keyword.cloud_notm}} users.|
| `public_original_crn` | String | The original offering CRN that is published.|
| `publish_public_crn` | String | The CRN of the public catalog entry of the offering.|
| `portal_approval_record` | String | The portal's approval record ID.|
| `portal_ui_url` | String | The portal UI URL.|
| `catalog_id` | String | The ID of the catalog containing this offering.|
| `catalog_name` | String | The name of the catalog.|
| `disclaimer` | String | A disclaimer for the offering.|
| `hidden` | String | Determine if the offering should be displayed in the consumption UI.|
| `provider` | String | Provider of this offering.|
| `repo_info` | String | Repository information for offerings. Nested `repo_info` blocks have the following structure.|
| `repo_info.token` | String | The token for the private repository.|
| `repo_info.type` | String | The public or enterprise GitHub.|
{: caption="Table: Available output parameters" caption-side="top"}


## `ibm_cm_offering_instance`
{: #cm-offering-instanceds}

Create, modify, or delete an `ibm_cm_offering_instance` data source.  For more information, about managing catalog, refer to [catalog management settings](/docs/account?topic=account-account-getting-started).
{: shortdesc}


### Sample Terraform code
{: #cm-offering-instance-dssample}


```
data "cm_offering_instance" "cm_offering_instance" {
	instance_identifier = "instance_identifier"
}
```
{: codeblock}

### Input parameters
{: #cm-offering-instance-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `instance_identifier` | String | Required | The version instance identifier.|
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-offering-instance-dsoutput}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the `cm_offering_instance`.|
| `url` | String | The URL reference to an object.|
| `crn` | String | The platform CRN for an instance.|
| `label` | String | The label for an instance.|
| `catalog_id` | String | The catalog ID the instance that is created from.|
| `offering_id` | String | The offering ID the instance that is created from.|
| `kind_format` | String | The format this instance has such as `helm`, `operator`.|
| `version` | String | The version an instance is installed from (but not from the version ID).|
| `cluster_id` | String | The cluster ID.|
| `cluster_region` | String | The cluster region for example, `us-south`.|
| `cluster_namespaces` | String | The list of target namespaces to install.|
| `cluster_all_namespaces` | String | Designate to install into all namespaces.|
{: caption="Table: Available output parameters" caption-side="top"}


## `ibm_cm_version`
{: #cm-versionds}

Create, modify, or delete an `cm_version` data source. For more information, about managing catalog version, refer to [updating your software](/docs/account?topic=account-update-private).
{: shortdesc}

### Sample Terraform code
{: #cm-version-dssample}


```
data "cm_version" "cm_version" {
	version_loc_id = "version_loc_id"
}
```
{: codeblock}

### Input parameters
{: #cm-version-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | 
| ------------- |-------------| ----- | --------| 
| `version_loc_id` | String | Required | A dotted value of `catalogID.versionID`.| 
{: caption="Table: Available input parameters" caption-side="top"}

### Output parameters
{: #cm-version-output}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the `cm_version`.|
| `crn` | String | The CRN version.|
| `version` | String | Version of the content type.|
| `sha` | String | The hash of the content.|
| `offering_id` | String | The offering ID.|
| `catalog_id` | String | The catalog ID.|
| `repo_url` | String | The URL of the content repository.|
| `source_url` | String | The source URL of the content repository, for example, Git repository.|
| `tgz_url` | String | File used to onboard the version.|
{: caption="Table: Available output parameters" caption-side="top"}
