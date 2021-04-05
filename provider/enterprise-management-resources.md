---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-05"

keywords: terraform provider plugin, terraform enterprise management, terraform enterprise account, terraform enterprise accounts, enterprise management

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



# Enterprise Management resources
{: #enterprise-mgt-resources}


Review the [Enterprise Management](/docs/account?topic=account-what-is-enterprise) resource that you can connect, administer, developed with Enterprise Management and integrate with the other services. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration/resources.html){: external}.
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}


## ibm_enterprise
{: #enterprise}

Create and update an enterprise. Delete operation is not supported. For more information, about enterprise management, refer to [setting up an enterprise](/docs/account?topic=account-create-enterprise).
{: shortdesc}

### Sample Terraform code
{: #enterprise-sample}

```
resource "ibm_enterprise" "enterprise" {
  source_account_id = "source_account_id"
  name = "name"
  primary_contact_iam_id = "primary_contact_iam_id"
}
```
{: codeblock}

### Input parameters
{: #enterprise-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`source_account_id`|String|Required|The ID of an account that is used to create the enterprise.|
|`name`|String|Required|The name of an enterprise. The minimum and maximum character should be from `3 to 60` characters.|
|`primary_contact_iam_id`|String|Required|The IAM ID of an enterprise primary contact, such as `IBMid-0123ABC.` The IAM ID must already exist.|
|`domain`|String|Optional| A domain or subdomain for an enterprise, such as `example.com`, or `my.example.com`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #enterprise-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id` | String | The unique identifier of an enterprise.|
| `url` | String | The URL of an enterprise.|
| `enterprise_account_id` | String | The enterprise account ID.|
| `crn` | String | The Cloud Resource Name (CRN) of an enterprise.|
| `state` | String | The state of an enterprise.|
| `primary_contact_email` | String | The Email of the primary contact of an enterprise.|
| `created_at` | String | The time stamp at which an enterprise is created.|
| `created_by` | String | The IAM ID of an user or service that created an enterprise.|
| `updated_at` | String | The time stamp at which an enterprise was last updated.|
| `updated_by` | String | The IAM ID of the user or service that updated an enterprise.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## ibm_enterprise_account
{: #enterprise-account}

Create and update an `enterprise_account`resource. Delete operation is not supported. For more information, about enterprise account, refer to [setting up accounts to an enterprise](/docs/account?topic=account-enterprise-add).
{: shortdesc}

### Sample Terraform code
{: #enterprise-account-sample}

```
resource "ibm_enterprise_account" "enterprise_account" {
  parent = "parent"
  name = "name"
  owner_iam_id = "owner_iam_id"
}

resource "ibm_enterprise_account" "enterprise_import_account"{
  parent = "parent"
  enterprise_id = "enterprise_id"
  account_id = "account_id"
}
```
{: codeblock}

### Input parameters
{: #enterprise-account-input}

Review the input parameters that you can specify to create a new account in an enterprise resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|----------------|
|`parent`|String|Required|The CRN of the parent in which the account is created. The parent can be an existing account group or an enterprise itself.|
|`name`|String|Required| The name of an enterprise. The minimum and maximum character should be from `3 to 60` characters.|
|`owneriam_id`|String|Required| The IAM ID of an account owner, such as `IBMid-0123ABC.` The IAM ID must already exist.|
{: caption="Table. Available input parameters" caption-side="top"}

Review the input parameters that you can specify to import a new account in an enterprise resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|----------------|
|`parent`|String|Required|The CRN of the parent in which the account is created. The parent can be an existing account group or an enterprise itself.|
|`enterprise_id`|String|Required| The enterprise ID where the account is imported.|
|`account_id`|String|Required| The standalone account ID that needs to be imported, such as `521ac39afd1b40aaad96fde2c6ad97xx`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #enterprise-account-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id` | String | The unique identifier of an enterprise account.|
| `account_id` | String | The source account ID.|
| `url` | String | The URL of an account.|
| `crn` | String | The Cloud Resource Name (CRN) of an account.|
| `enterprise_account_id` | String | The enterprise account ID.|
| `enterprise_id` | String | The enterprise ID that the account is a part of.|
| `enterprise_path` | String |The path from the enterprise to the particular account.|
| `state` | String | The state of an account.|
| `paid` | String | The type of account, whether it is `free`, or `paid`.|
| `owner_email` | String | The Email address of the owner of an account.|
| `is_enterprise_account` | String |The flag to indicate whether the account is an enterprise account or not.|
| `created_at` | String | The time stamp at which an account is created.|
| `created_by` | String | The IAM ID of an user or service that created an account.|
| `updated_at` | String | The time stamp at which an account was last updated.|
| `updated_by` | String | The IAM ID of the user or service that updated an account.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## ibm_enterprise_account_group
{: #enterprise-account-grp}

Create and update an `enterprise_account_group`resource. Delete operation is not supported. For more information, about enterprise account group, refer to [setting up access groups](/docs/account?topic=account-groups).
{: shortdesc}

### Sample Terraform code
{: #enterprise-account-grp-sample}

```
resource "ibm_enterprise_account_group" "enterprise_account_group" {
  parent = "parent"
  name = "name"
  primary_contact_iam_id = "primary_contact_iam_id"
}
```
{: codeblock}

### Input parameters
{: #enterprise-account-grp-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|----------------|
|`parent`|String|Required|The CRN of the parent in which the account group is created. The parent can be an existing account group or an enterprise itself.|
|`name`|String|Required| The name of an enterprise. The minimum and maximum character should be from `3 to 60` characters.|
|`primary_contact_iam_id`|String|Required| The IAM ID of an enterprise primary contact, such as `IBMid-0123ABC.` The IAM ID must already exist.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #enterprise-account-grp-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id` | String | The unique identifier of an enterprise account group.|
| `url` | String | The URL of an account group.|
| `enterprise_account_id` | String | The enterprise account ID.|
| `enterprise_id` | String | The enterprise ID that the account group is a part of.|
| `enterprise_path` | String |The path from the enterprise to the particular account group.|
| `crn` | String | The Cloud Resource Name (CRN) of an account group.|
| `state` | String | The state of an account group.|
| `primary_contact_email` | String | The Email address of the primary contact of an account group.|
| `created_at` | String | The time stamp at which an account group is created.|
| `created_by` | String | The IAM ID of an user or service that created an account group.|
| `updated_at` | String | The time stamp at which an account group was last updated.|
| `updated_by` | String | The IAM ID of the user or service that updated an account group.|
{: caption="Table 1. Available output parameters" caption-side="top"}

