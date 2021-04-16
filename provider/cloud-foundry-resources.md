---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-16"

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



# Cloud Foundry resources
{: #cloud-foundry-resources}

Review the [Cloud Foundry](/docs/cloud-foundry-public?topic=cloud-foundry-public-getting-started) resources that you can create, modify, or delete. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_app`
{: #cf-app}

Create, update, or delete a Cloud Foundry app. 
{: shortdesc}

### Sample Terraform code
{: #cf-app-sample}

The following example creates the `my-app` Node.js Cloud Foundry app. 
{: shortdesc}

```
data "ibm_space" "space" {
  org   = "example.com"
  space = "dev"
}

resource "ibm_app" "app" {
  name                 = "my-app"
  space_guid           = data.ibm_space.space.id
  app_path             = "hello.zip"
  wait_timeout_minutes = 90
  buildpack            = "sdk-for-nodejs"
}
```
{: codeblock}

### Input parameters
{: #cf-app-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the app that you want to create, update, or delete. You can retrieve the value by running the `ibmcloud app list` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`memory`|Integer|Optional|The amount of memory, specified in megabytes, that is allocated to each instance. If you don't specify a value, the system assigns pre-defined values based on the app quota. You can check the default values by running `ibmcloud cf org <org-name>`. The command lists the quotas that are defined in your Cloud Foundry organization and space. If space quotas are defined, you can see them by running `ibmcloud cf space-quota <space-quota-name>`, where `<quota-name>` is the name of the quota. To check the organization quotas, run `ibmcloud cf quota <quota-name>`.|
|`instances`|Integer|Optional|The number of app instances that you want to create.|
|`disk_quota`|Integer|Optional|The maximum amount of disk space, specified in megabytes, that is available to an app instance. The default value is [1024 MB](http://bosh.io/jobs/cloud_controller_ng?source=github.com/cloudfoundry/cf-release&version=234#p=cc.default_app_disk_in_mb). |
|`space_guid`|String| Required| The GUID of the space where the app is deployed. You can retrieve the value from data source `ibm_space` or by running the `ibmcloud iam space <space-name> --guid` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`buildpack`|String| Optional|The buildpack to use when compiling or preparing the app. Provide the buildpack in one of the following ways: <ul><li>Leave it blank for auto-detection.</li><li>Enter the GitHub URL to a buildpack, such as `https://github.com/cloudfoundry/nodejs-buildpack.git`.</li><li>List the name of an installed buildpack. For example, `go_buildpack`</li></ul>|
|`environment_json`|Map|Optional|A list of environment variables to run your app, specified as key-value pairs. Do not provide any key-value pairs for system or service variables.|
|`command`|String|Optional| The initial command to run when the app starts. |
|`route_guid`|Set|Optional| The GUIDs of the routes that you want to bind to the application. The route must be in the same Cloud Foundry space as the app.|
|`service_instance_guid`|Set|Optional| The GUID of the service instance that you want to bind to the app.|
|`wait_time_minutes`|Integer|Optional| The duration, expressed in minutes, to wait for the app to restage or start. The default value is `20`. A value of `0` means that there is no wait period.|
|`app_path`|String| Required| The path to the compressed file of the app. The compressed file must contain all the app files without subdirectories. To create the compressed file, go to the directory where your app files are and run `zip -r myapplication.zip *`.|
|`app_version`	|String|Optional|The version of the app. If you make changes to the content in the app compressed file specified by _app_path_, Terraform can't detect the changes. You can let Terraform know that your file content has changed by either changing the application compressed file name or by using this argument to indicate the version of the file.|
|`health_check_http_endpoint`|String|Optional|The endpoint that you want to use to determine if the app is healthy. |
|`health_check_type`|String| Optional|The type of health check that you want to perform. Supported values are `port`, and `process`. The default values is `port`. |
|`health_check_timeout`|Integer|Optional| The number of seconds to wait for the health check to respond during the start of your app before the health check is considered failed. |
|`tags`|Array of string| Optional| The tags that you want to add to your app instance. Tags can help you find your app more easily.  **NOTE**: `Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-app-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}


|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the app.|
{: caption="Table 1. Available output parameters" caption-side="top"}



## `ibm_app_domain_private`
{: #cf-private-domain}

Create, update, or delete a private domain for your Cloud Foundry app. 
{: shortdesc}

### Sample Terraform code
{: #cf-app-private-domain-sample}

The following example creates the `example.com` private domain. 
{: shortdesc}

```
data "ibm_org" "orgdata" {
  org = "myorg"
}

resource "ibm_app_domain_private" "domain" {
  name     = "example.com"
  org_guid = data.ibm_org.orgdata.id
  tags     = ["tag1", "tag2"]
}
```
{: codeblock}

### Input parameters
{: #cf-private-domain-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|------------|------------------------|
|`name`|String| Required| The name of the private domain.|
|`org_guid`|String|Required|The GUID of the Cloud Foundry organization where you want to create the domain. You can retrieve the value from data source `ibm_org` or by running the `ibmcloud iam orgs --guid` command in the {{site.data.keyword.cloud_notm}} CLI. |
|`tags`|Array of Strings|Optional| The tags that you want to add to your private domain. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{:#cf-private-domain-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the private domain.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_app_domain_shared`
{: #cf-shared-domain}

Create, update, or delete a shared domain for your Cloud Foundry app. 
{: shortdesc}

### Sample Terraform code
{: #cf-shared-domain-sample}

The following example creates the `example.com` shared domain. 
{: shortdesc}

```
resource "ibm_app_domain_shared" "domain" {
  name              = "example.com"
  router_group_guid = "3hG5jkjk4k34JH5666"
  tags              = ["tag1", "tag2"]
}
```
{: codeblock}

### Input parameters
{: #cf-shared-domain-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|------------|------------------------|
|`name`|String|Required|The name of the domain.|
|`router_group_guid`|String|Optional|The GUID of the router group.|
|`tags`|Array of string|Optional|The tags that you want to add to the shared domain. Tags can help you find the domain more easily later.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-shared-domain-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the shared domain.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_app_route`
{: #cf-route}

Create, update, or delete a route for your Cloud Foundry app. 
{: shortdesc}

### Sample Terraform code
{: #cf-route-sample}

The following example creates a route for the `example.com` shared domain. 
{: shortdesc}

```
data "ibm_space" "spacedata" {
  space = "space"
  org   = "myorg"
}

data "ibm_app_domain_shared" "domain" {
  name = "example.com"
}

resource "ibm_app_route" "route" {
  domain_guid = data.ibm_app_domain_shared.domain.id
  space_guid  = data.ibm_space.spacedata.id
  host        = "myhost"
  path        = "/app"
}
```
{: codeblock}

### Input parameters
{: #cf-route-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|------------|------------------------|
|`domain_guid`|String|Required|The GUID of the associated domain. You can retrieve the value from data source `ibm_app_domain_shared` or `ibm_app_domain_private`.|
|`space_guid`|String|Required| The GUID of the Cloud Foundry space where you want to create the route. You can retrieve the value from data source `ibm_space` or by running the `ibmcloud iam space <space_name> --guid` command in the {{site.data.keyword.cloud_notm}} CLI. |
|`host`|String|Optional|The hostname of the route. The hostname is required for shared domains.|
|`port`|String|Optional|The port of the route. This option is supported for TCP router group domains only.|
|`path`|String|Optional|The path for the route. Paths must be between 2-128 characters, must start with a forward slash (/), and cannot contain a question mark (?).|
|`tags`|Array of string|Optional|The tags that you want to add to the route. Tags can help you find the route more easily later. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-route-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the route.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_org`
{: #cf-org}

Create, update, or delete a Cloud Foundry organization. 
{: shortdesc}

### Sample Terraform code
{: #cf-org-sample}

The following example create the `myorg` Cloud Foundry organization and assigns users access to the organization. 
{: shortdesc}

```
resource "ibm_org" "testacc_org" {
    name = "myorg"
    org_quota_definition_guid = "myorgquotaguid"
    auditors = ["auditor@in.ibm.com"]
    managers = ["manager@in.ibm.com"]
    users = ["user@in.ibm.com"]
    billing_managers = ["billingmanager@in.ibm.com"]
}
```
{: codeblock}

### Input parameters
{: #cf-org-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|------------|------------------------|
|`name`|String|Required|The descriptive name used of the Cloud Foundry organization. The name must be unique in {{site.data.keyword.cloud_notm}}. |
|`org_quota_definition_guid`|String|Optional|The GUID for the quota that is assigned to organization. The quota sets memory, service, and instance limits for the organization.|
|`managers`|Set|Optional|The email addresses of the users that you want to assign Cloud Foundry **Manager** access to. The email address needs to be associated with an IBMId. Managers have the following permissions within the org: <ul><li>Create, view, edit, or delete spaces.</li><li>View usage and quota information.</li><li>Invite users and manage user access. </li><li> Assign roles to users.</li><li>Manage custom domains.</li></ul>|
|`users`|Set|Optional|The email addresses of the users that you want to grant org-level access to. The email address needs to be associated with an IBMId. |
|`auditors`|Set|Optional|The email addresses of the users that you want to assign Cloud Foundry **Auditor** access to. The email address needs to be associated with an IBMId. Auditors have the following permissions within the org: <ul><li>View users and their assigned roles.</li><li>View quota information.</li></ul>|
|`billing_managers`|Set|Optional|The email addresses of the users that you want to assign the **Billing manager** access to. The email address needs to be associated with an IBMId. Billing managers have the following permissions within the org: <ul><li>View runtime and service usage information on the usage dashboard.</li></ul>|
|`tags`|(Optional, array of strings) Tags associated with the org.     **NOTE**: Tags are managed locally and not stored on the IBM Cloud service endpoint.|
{: caption="Table. Available input parameters" caption-side="top"}


By default, the user that creates this resource is assigned the **Manager** Cloud Foundry role. Terraform returns an error when you assign the **Manager** or Cloud Foundry user role to yourself. User information is not persisted in the Terraform state file to avoid any incorrect information.
{: important}

### Output parameters
{: #cf-org-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the Cloud Foundry organization.  |
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #cf-org-import}

The Cloud Foundry organization can be imported by using the `id`. 

```
terraform import ibm_org.myorg abde-12345
```
{: codeblock}


## `ibm_service_instance`
{: #cf-service}

Create, update, or delete a Cloud Foundry service instance. 
{: shortdesc}

### Sample Terraform code
{: #cf-service-sample}

The following example creates the `speech_to_text` Cloud Foundry service instance. 
{: shortdesc}

```
data "ibm_space" "spacedata" {
  space = "prod"
  org   = "myorg"
}

resource "ibm_service_instance" "service_instance" {
  name       = "myspeech"
  space_guid = data.ibm_space.spacedata.id
  service    = "speech_to_text"
  plan       = "lite"
  tags       = ["cluster-service", "cluster-bind"]
}
```
{: codeblock}

### Input parameters
{: #cf-service-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|------------|------------------------|
|`name`|String|Required|A descriptive name for the service instance.|
|`space_guid`|String|Required|The GUID of the Cloud Foundry space where you want to create the service. You can retrieve the value from data source `ibm_space`.|
|`service`|String|Required|The name of the service offering. You can retrieve the value by running the `ibmcloud service offerings` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`plan`|String|Required|The name of the service plan that you want. You can retrieve the value by running the `ibmcloud service offerings` command in the {{site.data.keyword.cloud_notm}} CLI.|
|`tags`|Array of string| Optional| The tags that you want to add to the service instance. Tags can help you to find the instance more easily later. |
|`parameters`|Map|Optional| Arbitrary parameters to pass to the service broker. The value must be a JSON object.|
|`wait_time_minutes`|Integer|Optional|The number of minutes to wait for the service instance to become available before declaring it as created. The same number of minutes is used for the deletion to finish. The default value is `10`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-service-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the new service instance.|
|`credentials`|String|The credentials provided by the service broker to use the service.|
|`service_keys`|String|The service keys associated with the service.|
|`service_plan_guid`|String|The plan of the service offering used by this service instance.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_service_key`
{: #cf-service-key}

Create, update, or delete a service key for your Cloud Foundry service instance. 
{: shortdesc}

### Sample Terraform code
{: #cf-service-key-sample}

The following example creates the `mycloudantkey` service key. 
{: shortdesc}

```
data "ibm_service_instance" "service_instance" {
  name = "mycloudant"
}

resource "ibm_service_key" "serviceKey" {
  name                  = "mycloudantkey"
  service_instance_guid = data.ibm_service_instance.service_instance.id
}
```
{: codeblock}

### Input parameters
{: #cf-service-key-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|------------|------------------------|
|`name`|String|Required|A descriptive name for the service key.|
|`parameters`|Map|Optional|Arbitrary parameters to pass along to the service broker. Must be a JSON object.|
|`service_instance_guid`|String|Required|The GUID of the service instance for which you create the service key.|
|`tags`|Array of string|Optional|The tags that you want to add to the service key instance. Tags can help you find the service keys more easily later. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #cf-service-key-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the new service key.|
|`credentials`|String|The credentials associated with the key.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_space`
{: #cf-space}

Create, update, or delete a Cloud Foundry space. 
{: shortdesc}

### Sample Terraform code
{: #cf-space-sample}

The following example creates the `myspace` Cloud Foundry space. 
{: shortdesc}

```
resource "ibm_space" "space" {
  name        = "myspace"
  org         = "myorg"
  space_quota = "myspacequota"
  managers    = ["manager@example.com"]
  auditors    = ["auditor@example.com"]
  developers  = ["developer@example.com"]
}
```
{: codeblock}

### Input parameters
{: #cf-space-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|------------|------------------------|
|`name`|String|Required|The descriptive name for the space.|
|`org`|String|Required|The name of the Cloud Foundry organization to which this space belongs.|
|`space_quota`|String|Optional|The name of the space quota definition that is associated with the space.|
|`managers`|Set|Optional|The email addresses (associated with IBM IDs) of the users to whom you want to give a manager role in this space. Users with the manager role can invite users, manage users, and enable features for the given space.|
|`developers`|Set|Optional|The email addresses (associated with IBM IDs) of the users to whom you want to give a developer role in this space. Users with the developer role can create apps and services, manage apps and services, and see logs and reports in the given space.|
|`auditors`|Set|Optional| The email addresses (associated with IBM IDs) of the users to whom you want to give an auditor role in this space. Users with the auditor role can view logs, reports, and settings in the given space.  |
|`tags`|Array of string|Optional|The tags that you want to add to the space. Tags can help you find the space more easily later. |
{: caption="Table. Available input parameters" caption-side="top"}

 By default, the newly created space has no user associated with it. Add your own email address to the `managers` or `developers` field in order to be able to use the space correctly for the first time.
 {: important}

### Output parameters
{: #cf-space-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the new space.|
{: caption="Table 1. Available output parameters" caption-side="top"}
