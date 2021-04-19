---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19" 

keywords: terraform provider plugin, terraform container registry, container registry, container registry namespaces 

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



# Container Registry resources
{: #container-registry}


## `ibm_cr_namespace`
{: #cr-namespace}

Create, update, or delete a container registry namespace. For more information, about container registry, see [About IBM Cloud Container Registry](/docs/Registry?topic=Registry-registry_overview).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cr-namespace-sample}

The following example shows how you can configure a `namespace`.
{: shortdesc}

```
resource "ibm_cr_namespace" "test" {
  name              = "test123"
  resource_group_id = "c34128405d5742549538xxx1237"
}
```
{: codeblock}

```
data "ibm_resource_group" "rg" {
  name = "default"
}
resource "ibm_cr_namespace" "rg_namespace" {
  name              = "testaasd2312"
  resource_group_id = data.ibm_resource_group.rg.id
}
```
{: codeblock}

### Input parameter
{: #cr-namespace-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
| `name` | String | Required | The name of the namespaces to create. | Yes |
| `resource_group_id` | String | Optional | The ID of the resource group to which the namespace is assigned. If not provided, default resource group ID will be assigned. | Yes |

### Output parameters
{: #cr-namespace-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------ |-------------| -------------- |
| `id` | String | The name of the namespace.| 
| `crn` | String | The `CRN` of the namespace.|
| `created_on` | String | The created time of the namespace.|
| `updated_on` | String | The updated time of the namespace.|

### Import
{: #cr-namespace-import}

The `ibm_cr_namespace` resource can be imported by using the ID. The ID is formed from the name (namespace name) `ID=name`.

**Syntax**

```
terraform import ibm_cr_namespace.test <name of the namespace>
```

**Example**

```
terraform import ibm_cr_namespace.test namespace-name
```
