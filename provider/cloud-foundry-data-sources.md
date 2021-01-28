---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider plugin, terraform cloud foundry, terraform cf resources, terraform cf org, terraform cf space

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
{:swift-ios: .ph data-hd-programlang='iOS Swift'}
{:swift-server: .ph data-hd-programlang='server-side Swift'}
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



# Cloud Foundry data sources
{: #cloud-foundry-data-sources}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}


## `ibm_account`
{: #cf-account}

Retrieve information about an existing {{site.data.keyword.cloud_notm}} account. 
{: shortdesc}


### Sample Terraform code
{: #cf-account-sample}

The following example retrieves information about an {{site.data.keyword.cloud_notm}} account that belongs to the `myorg` Cloud Foundry organization. 
{: shortdesc}

```
data "ibm_org" "orgData" {
  org = "myorg"
}

data "ibm_account" "accountData" {
  org_guid = data.ibm_org.orgData.id
}
```

### Input parameters
{: #cf-account-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`org_guid`|String|Required|The GUID of the {{site.data.keyword.cloud_notm}} organization. You can retrieve the value from the `ibm_org` data source or by running the `ibmcloud iam orgs --guid` command.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-account-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id`|String|The unique identifier of the {{site.data.keyword.cloud_notm}} account.  |
|`account_users`|List of objects|The list of account user's in the account. |
|`account_users.id`| String| The user ID of the account user.  |
|`account_users.email`|String|The email address of the account user.  |
|`account_users.state`|String| The state of the account user.  |
|`account_users.role`| String | The Cloud Foundry account role that is assigned to the account user.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_app`
{: #cf-app}

Retrieve information about an existing Cloud Foundry app. 
{: shortdesc}

### Sample Terraform code
{: #cf-app-sample}

The following example retrieves information about the `my-app` Cloud Foundry app.  
{: shortdesc}

```
data "ibm_app" "testacc_ds_app" {
  name       = "my-app"
  space_guid = ibm_app.app.space_guid
}
```

### Input parameters
{: #cf-app-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`name`|String|Required|The name of the app. You can retrieve the value by running the `ibmcloud app list` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`space_guid`|String|Required|The GUID of the {{site.data.keyword.cloud_notm}} space where the app is deployed. You can retrieve the value with the `ibm_space` data source or by running the `ibmcloud iam space <space-name> --guid` command in the {{site.data.keyword.cloud_notm}} CLI.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-app-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|---------|
|`id`|String|The unique identifier of the app.|
|`memory`|Integer|The amount of memory, specified in megabytes, that is allocated to the app.|
|`instances`|Integer|The number of app instances that are deployed.|
|`disk_quota`|Integer|The maximum amount of disk space that an app instance can use, specified in megabytes.|
|`buildpack`|String|The buildpack that is used by the app. Supported values are: <ul><li>Blank, indicates auto-detection</li><li>A Git URL that points to a buildpack</li><li>The name of an installed buildpack</li></ul>|
|`environment_json`|List of strings|A list of environment variables that the app uses. Environment variables are listed as key-value pairs and do not include system or service variables. |
|`route_guid`|String|The GUIDs of the routes that are assigned to the app.|
|`service_instance_guid`|String|The GUIDs of the service instances that are bound to the app.|
|`package_state`|String|The state of the app package, such as `staged` or `pending`.|
|`state`|String|The state of the app.|
|`health_check_http_endpoint`|String|The endpoint that is used to perform an HTTP health check and determine if the app is healthy.|
|`health_check_type`|String|Type of health check that is performed.|
|`health_check_timeout`|Integer|The timeout in seconds that the app remains unresponsive before the app is considered to be unhealthy. |
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_app_domain_private`
{: #cf-private-domain}

Retrieve information about an existing private domain for an app. 
{: shortdesc}

### Sample Terraform code
{: #cf-private-domain-sample}

The following example retrieves information about the `example.com` domain. 
{: shortdesc}

```
data "ibm_app_domain_private" "private_domain" {
  name = "example.com"
}
```

### Input parameters
{: #cf-private-domain-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|------|--------|
|`name`|String|Required|The name of the private domain that is assigned to the app.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-private-domain-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|---------|
|`id`|String|The unique identifier of the private app domain.  |
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_app_domain_shared`
{: #cf-shared-domain}

Retrieve information about an existing shared domain for an app. 
{: shortdesc}

### Sample Terraform code
{: #cf-shared-domain-sample}

The following example retrieves information about the `example.com` domain. 
{: shortdesc}

```
data "ibm_app_domain_shared" "shared_domain" {
  name = "example.com"
}
```

### Input parameters
{: #cf-shared-domain-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|------|--------|
|`name`|String|Required| The name of the shared domain.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-shared-domain-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------|
|`id`|String|The unique identifier of the shared domain.  |
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_app_route`
{: #cf-app-route}

Retrieve information about an existing app route. 
{: shortdesc}

### Sample Terraform code
{: #cf-app-route-sample}

The following example retrieves information about an app route. 
{: shortdesc}

```
data "ibm_app_route" "route" {
  domain_guid = data.ibm_app_domain_shared.domain.id
  space_guid  = data.ibm_space.spacedata.id
  host        = "myhost"
  path        = "/app"
}
```

### Input parameters
{: #cf-app-route-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|------|--------|
|`domain_guid`|String| Required| The GUID of the domain that the route belongs to. You can retrieve the value from the `ibm_app_domain_shared` data source.|
|`space_guid`|String|Required|The GUID of the space that the route belongs to. You can retrieve the value from the `ibm_space` data source or by running the `ibmcloud iam space <space-name> --guid` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`host`|String|Optional| The host name of the route. Required for shared domains.|
|`port`|String|Optional| The port of the route. This value is supported for TCP router group domains only.|
|`path`|String|Optional| The path for a route. Paths must contain 2-128 characters. Paths must start with a forward slash (/). Paths must not contain a question mark (?).|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-app-route-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------------|
|`id`|String|The unique identifier of the route.  |
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_org`
{: #cf-org}

Retrieve information about an existing Cloud Foundry organization. 
{: shortdesc}

### Sample Terraform code
{; #cf-org-sample}

The following example retrieves information about the `myorg` Cloud Foundry organization. 
{: shortdesc}

```
data "ibm_org" "orgdata" {
  org = "myorg"
}
```

### Input parameters
{: #cf-org-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|------|--------|
|`name`|String|Optional|The name of the {{site.data.keyword.cloud_notm}} organization.|
|`org`|String|Deprecated|The name of the {{site.data.keyword.cloud_notm}} organization.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-org-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-----------|
|`id`|String|The unique identifier of the Cloud Foundry organization.  |
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_org_quota`
{: #cf-org-quota}

Retrieve information about a quota for a Cloud Foundry organization. 
{: shortdesc}

### Sample Terraform code
{: #cf-org-quota-sample}

The following example retrieves information for an existing quota plan. 
{: shortdesc}

```
data "ibm_org_quota" "orgquotadata" {
  name = "quotaname"
}
```

### Input parameters
{: #cf-org-quota-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|-----------|-------------------|
|`name`|String|Required| The name of the quota plan for the Cloud Foundry organization. You can retrieve the value by running the `ibmcloud cf quotas` command in the {{site.data.keyword.cloud_notm}} CLI.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id`|String|The unique identifier of the Cloud Foundry organization.|
|`app_instance_limit`|Integer|Defines the total number of app instances that are allowed for the Cloud Foundry organization.|
|`app_tasks_limit`|Integer|Defines the total number of app tasks for a Cloud Foundry organization.|
|`instance_memory_limit`|Integer|Defines the total amount of memory that an instance can use in a Cloud Foundry organization.|
|`memory_limit`|Integer|Defines the total amount of memory that can be used by the Cloud Foundry organization.|
|`non_basic_services_allowed`|Boolean|Defines if non-basic (paid) services are allowed for the Cloud Foundry organization.|
|`total_private_domains`|Integer|Defines the total number of private domains that can be created for a Cloud Foundry organization.|
|`total_reserved_route_ports`|Integer|Defines the number of routes with reserved ports for the Cloud Foundry organization. |
|`total_routes`|Integer|Defines the maximum number of routes that can be created for a Cloud Foundry organization.|
|`total_service_keys`|Integer|Defines the maximum number of service keys for the Cloud Foundry organization.|
|`total_services`|Integer|Defines the maximum number of services that can be created in a Cloud Foundry organization.|
|`trial_db_allowed`|Boolean|Defines if a trial database is allowed for the Cloud Foundry organization.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_service_instance`
{: #cf-service-instance}

Retrieve information about a Cloud Foundry service instance. 
{: shortdesc}

### Sample Terraform code
{: #cf-service-instance-sample}

The following example retrieves information about the `mycloudantdb` instance. 
{: shortdesc}

```
data "ibm_space" "space" {
  org   = "myorg"
  space = "dev"
}

data "ibm_service_instance" "serviceInstance" {
  name = "mycloudantdb"
  space_guid   = data.ibm_space.space.id
}
```

### Input parameters
{: #cf-service-instance-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|------------|------------------------|
|`name`|String|Required| The name of the service instance. You can retrieve the value by running the `ibmcloud service list` command.|
|`space_guid`|String|Required|The GUID of the Cloud Foundry space where the service instance is deployed to. You can retrieve the value from data source `ibm_space`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-service-instance-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-----------------|
|`id`|String|The unique identifier of the service instance.|
|`credentials`|String|The credentials provided by the service broker to use this service.|
|`service_keys`|String|The service keys associated with this service.|
|`service_plan_guid`|String|The plan GUID for the service offering used by this service instance.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_service_key`
{: #cf-service-key}

Retrieve information about existing service credentials that a Cloud Foundry service instance uses. 
{: shortdesc}

### Sample Terraform code
{: #cf-service-key-sample}

The following example retrieves service key information for the `mycloudantdb` service instance. 
{: shortdesc}

```
data "ibm_space" "space" {
  org   = "example.com"
  space = "dev"
}

data "ibm_service_key" "serviceKeydata" {
  name                  = "mycloudantdbKey"
  service_instance_name = "mycloudantdb"
  space_guid            = data.ibm_space.space.id
}
```

### Input parameters
{: #cf-service-key-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`name`|String|Required|The name of the service key. You can retrieve the value by running the `ibmcloud service keys` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`service_instance_name`|String|Required| The name of the service instance that the service key is associated with. You can retrieve the value by running the `ibmcloud service list` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`space_guid`|String|Required |The GUID of the Cloud Foundry space where the service instance exists. You can retrieve the value from the data source `ibm_space`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-service-key-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`|String|The unique identifier of the service key.|
|`credentials`|String|The credentials associated with the key.  |
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_service_plan`
{: #cf-service-plan}

Retrieve information about a service plan for a Cloud Foundry service. 
{: shortdesc}

### Sample Terraform code
{: #cf-service-plan-sample}

The following example retrieves information about the `Lite` service plan for the `CloudantNOSQLDB` service. 

```
data "ibm_service_plan" "service_plan" {
  service = "cloudantNoSQLDB"
  plan    = "Lite"
}
```

### Input parameters
{: #cf-service-plan-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|------------|-----------------------------|
|`service`|String| Required|The name of the service offering. You can retrieve the name of the service by running the `ibmcloud service offerings` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`plan`|String|Required| The name of the plan type supported by the service. You can retrieve the plan type by running the `ibmcloud service offerings` command in the {{site.data.keyword.cloud_notm}} CLI.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-service-plan-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id`|String|The unique identifier of the service plan.  |
{: caption="Table 1. Available output parameters" caption-side="top"}



## `ibm_space`
{: #cf-space}

Retrieve information about an existing Cloud Foundry space.
{: shortdesc}

### Sample Terraform code
{: #cf-space-sample}

The following example retrieves information about the `prod` Cloud Foundry space.
{: shortdesc}

```
data "ibm_space" "spaceData" {
  space = "prod"
  org   = "myorg"
}
```
The following example shows how you can use the data source to reference the space ID in the `ibm_service_instance` resource.

```
resource "ibm_service_instance" "service_instance" {
  name       = "test"
  space_guid = data.ibm_space.spaceData.id
  service    = "speech_to_text"
  plan       = "lite"
  tags       = ["cluster-service", "cluster-bind"]
}
```

### Input parameters
{: #cf-space-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}


|Name|Data type| Required / optional|Description|
|----|-----------|--------|-------------------|
|`name`|String|Optional| The name of your space.|
|`org`|String|Deprecated| The name of your Cloud Foundry organization that the space belongs to. You can retrieve the value by running the `ibmcloud iam orgs` command in the {{site.data.keyword.cloud_notm}} CLI. |
|`space`|String|Deprecated| The name of your Cloud Foundry space. You can retrieve the value by running the `ibmcloud iam spaces` command in the IBM Cloud CLI. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-space-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------------------|
|`auditors`|String|The email addresses (associated with IBMid) of the users who have an auditor role in this space.|
|`developers`|String|The email addresses (associated with IBMid) of the users who have a developer role in this space.|
|`id`|String|The unique identifier of the space.  |
|`managers`|String|The email addresses (associated with IBMid) of the users who have a manager role in this space.|
{: caption="Table 1. Available output parameters" caption-side="top"}
