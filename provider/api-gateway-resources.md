---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

keywords: terraform provider plugin, terraform certificate manager, terraform cert manager, terraform certificate

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



#  API Gateway resources
{: #api-gateway-resources}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

## `ibm_api_gateway_endpoint`
{: #api-gw-endpoint}

Create, update, or delete an API endpoint for an API gateway. 

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #api-gw-endpoint-sample}

#### Example for a single  API Documentation as input

```
resource "ibm_resource_instance" "apigateway"{
    name     = "testname"
    location = "global"
    service  = "api-gateway"
    plan     = "lite"
 }

resource "ibm_api_gateway_endpoint" "endpoint"{
    service_instance_crn = ibm_resource_instance.apigateway.id
    name="test-endpoint"
    managed="true"
    open_api_doc_name = var.file_path
    type="share" //optional while creating endpoint  required during updating actions of an endpoint
}
```
{: codeblock}


#### Example for a directory of  API Documentation as input

```
resource "ibm_resource_instance" "apigateway"{
    name     = "testname"
    location = "global"
    service  = "api-gateway"
    plan     = "lite"
 }

resource "ibm_api_gateway_endpoint" "endpoint"{
    for_each=fileset(var.dir_path, "*.json")
    service_instance_crn = ibm_resource_instance.apigateway.id
    managed="true"
    name=replace("endpoint-${each.key}",".json","")
    open_api_doc_name=format("%s%s",var.dir_path,each.key)
    type="share" //optional while creating endpoint  required during updating actions of an endpoint
}
```
{: codeblock}


### Input parameters 
{: #api-gw-endpoint-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`service_instance_crn`|String|Required|The CRN of the service instance.|
|`name`|String|Required|The name of the API Gateway endpoint. This value is optional when you create an API Gateway endpoint, but required when you update the endpoint.|
|`managed`|Boolean|Optional|If set to **true**, the endpoint is online. If set to **false**, the endpoint is offline. The default value is false. The API endpoint cannot be shared if this value is set to **false**.|
|`open_api_doc_name`|String|Required|The API document that represents the endpoint. |
|`routes`|List|Optional|The routes that you can invoke for an endpoint.|
|`provider_id`|String|Optional|The provider ID of an API endpoint. Supported values are `user-defined`, and `whisk`. The default value is `user-defined`.|
|`type`|String|Optional|The type of action that is performed on the API endpoint. Supported values are `share`, `unshare`, `manage`, and `unmanage`. The default value is `unshare`. The endpoint actions are performed by using the `type` parameter after the endpoint is created. As a consequence, endpoint actions are invoked during an endpoint update only.|

### Output parameters
{: #api-gw-endpoint-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the endpoint. The ID is composed of `<service_instance_crn>//<endpoint_ID>`.|
|`endpoint_id`|String|The ID of the endpoint, also referred to as the artifact ID. |
|`shared`|String|The shared status of an endpoint.|
|`base_path`|String|The base path of an endpoint. The base paths must be unique.|

### Import
{: #api-gw-endpoint-import}

The `ibm_api_gateway_endpoint` resource can be imported by using the ID. The ID is composed of `<service_instance_crn>//<endpoint_ID>`.

```
terraform import ibm_api_gateway_endpoint.endpoint <service_instance_crn>//<endpoint_id>
```
{: pre}

## `ibm_api_gateway_endpoint_subscription`
{: #api-gw-endpoint-subscript}

Create, update, or delete a subscription for an API Gateway endpoint. 
{: shortdesc}

Endpoint subscriptions can be added only if the endpoint is online. Make sure to set the `managed` input parameter to **true** in the `ibm_api_gateway_endpoint` resource.
{: important}


### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #api-gw-endpoint-subscript-sample}

```
data "ibm_api_gateway" "endpoint"{
    service_instance_crn =ibm_resource_instance.apigateway.id
}

resource "ibm_api_gateway_endpoint_subscription" "subs" {
  artifact_id = data.ibm_api_gateway.endpoint.endpoints[0].endpoint_id
  client_id   = "testid"
  name        = "testname"
  type        = "external"
}
```
{: codeblock}

### Input parameters 
{: #api-gw-endpoint-subscript-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`artifact_id`|String|Required|The ID of an API endpoint.| 
|`client_id`|String|Optional|The API key to generate an API key for the subscription. The generated API key represents the ID of a subscription.| 
|`name`|String|Required|The name for an API key.|
|`type`|String|Required|The type of API key sharing. Supported values are `External`, and `Bluemix`.
|`client_secret`|String|Optional|The secret of the API key.|
|`generate_secret`|Boolean|Optional|If set to **true**, the secret key is auto-generated. If set to **false**, the secret key is not auto-generated. |


### Output parameters
{: #api-gw-endpoint-subscript-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the subscription. The ID is composed of `<artifact_id>//<client_id>`. |
|`secret_provided`|Boolean|If set to **true**, the client secret is provided. If set to **false**, the client secret is not provided. |


### Import
{: #api-gw-endpoint-subscript-import}

The `ibm_api_gateway_endpoint_subscription` resource can be imported by using the ID. The ID is composed of `<artifact_id>//<client_id>`.

- **Endpoint ID**: The Endpoint ID can be retrieved programmatically via the API Gateway endpoint API.
- **Client ID**: The Client ID is an auto-generated string. To view the client ID in the IBM Cloud console, you must enable **Application authentication** on the **Define and secure** page of the API Gateway service. The client ID of a particular subscription is available as an API key in the **Manage and Sharing** page of the API Gateway service.

```
terraform import ibm_api_gateway_endpoint_subscription.subscription <artifact_id>//<client_id>
```
{: pre}






