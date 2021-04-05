---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-04"
 
keywords: terraform provider plugin, terraform satellite host, terraform satellite location

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



# {{site.data.keyword.satelliteshort}} data sources
{: #satellite-data-sources}

With {{site.data.keyword.satellitelong_notm}}, you can bring your own infrastructure that is in your on-premises data center, in other cloud providers, or in edge environments to {{site.data.keyword.cloud_notm}} by creating a {{site.data.keyword.satelliteshort}} host and location.
{: shortdesc}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}


## `ibm_satellite_host`
{: #satellite-host-ds}

Retrieve information about all the add-ons that are enables on a cluster. For more information, about setting up {{site.data.keyword.satelliteshort}} hosts, see [{{site.data.keyword.satelliteshort}} hosts](/docs/satellite?topic=satellite-hosts).
{: shortdesc}

Import the details of an existing {{site.data.keyword.satellitelong_notm}} location registration script as a data source. Creates a script to run on a Red Hat Enterprise Linux 7 or AWS EC2 host in your on-premises infrastructure. The script attaches the host to your {{site.data.keyword.satellitelong_notm}} location. The host must have access to the public network in order for the script to complete.

### Sample Terraform code
{: #satellite-host-dssample}

The example to create {{site.data.keyword.satelliteshort}} host script to attach {{site.data.keyword.IBM_notm}} host to {{site.data.keyword.satelliteshort}} control plane.

```
data "ibm_satellite_attach_host_script" "script" {
  location          = var.location
  labels            = var.labels
  host_provider     = "ibm"
}
```
{: codeblock}

The example to create {{site.data.keyword.satelliteshort}} host script to attach AWS EC2 host to {{site.data.keyword.satelliteshort}} control plane.

```
data "ibm_satellite_attach_host_script" "script" {
  location          = var.location
  labels            = var.labels
  script_dir        = "/tmp"
  host_provider     = "aws"
}
```
{: codeblock}

### Input parameters
{: #satellite-host-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `location` | String | Required | The name or ID of the {{site.data.keyword.satelliteshort}} location.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #satellite-host-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `id` | String | The unique identifier of the location.|
| `labels` | String | The key value pairs to label the host, such as `cpu=4` to describe the host capabilities.|
| `script_dir` | String | The directory path to store the generated script. |
| `host_provider` | String | The name of the host provider, such as `ibm`, `aws`, or `azure`.|
| `script_path` | String | The directory path to store the generated script. |
| `host_script` | String | The raw content of the script file that is read.|
{: caption="Table. Available output parameters" caption-side="top"}


## `ibm_satellite_location`
{: #satellite-location-ds}

Retrieve information of an existing {{site.data.keyword.satelliteshort}} location. You can then reference the fields of the data source in other resources within the same configuration by using interpolation syntax. For more information, about {{site.data.keyword.cloud_notm}} regions for {{site.data.keyword.satelliteshort}} see [{{site.data.keyword.satelliteshort}} regions](/docs/satellite?topic=satellite-sat-regions).
{: shortdesc}

### Sample Terraform code
{: #satellite-location-dssample}


```
data "ibm_satellite_location" "location" {
  location  = var.location
}
```
{: codeblock}

### Input parameters
{: #satellite-location-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `location` | String | Required | The name or ID of the {{site.data.keyword.satelliteshort}} location to  be created or pass existing location.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #satellite-location-dsoutput}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `id` | String | The unique identifier of the location.|
| `crn` | String | The CRN for this satellite location.|
| `managed_from` | String | The {{site.data.keyword.cloud_notm}} metro from which the {{site.data.keyword.satelliteshort}} location is managed. To list available multizone regions, run `ibmcloud ks locations`. such as `wdc04`, `wdc06`, or `lon04`.|
| `description` | String | Description of the new Satellite location.
| `logging_account_id` | String |  The account ID for {{site.data.keyword.loganalysislong_notm}} with {{site.data.keyword.loganalysislong_notm}} log forwarding.|
| `zone` | String | The names for the host zones. For high availability, allocate your hosts across these three zones based on your infrastructure provider zones. For example, `us-east-1`, `us-east-2`, `us-east-3`.|
{: caption="Table. Available output parameters" caption-side="top"}