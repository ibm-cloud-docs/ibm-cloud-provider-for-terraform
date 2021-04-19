---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

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



# Enterprise Management data sources
{: #enterprise-mgt-ds}

Review the [Enterprise Management](/docs/account?topic=account-what-is-enterprise) data source that you can connect, administer, developed with Enterprise Management and integrate with the other services. You can reference the output parameters for each resource in other resources or data sources by using [Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax](https://www.terraform.io/docs/configuration/resources.html){: external}.
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

## ibm_enterprises
{: #enterprises-ds}

Retrieve an information from an `ibm_enterprise` data source. For more information, about enterprise management, refer to [setting up an enterprise](/docs/account?topic=account-create-enterprise).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #enterprises-ds-sample}

```
data "ibm_enterprises" "enterprises" {
}
```
{: codeblock}

### Input parameters
{: #enterprises-ds-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Optional|The name of an enterprise.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #enterprises-ds-output}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id` | String | The unique identifier of an enterprises.|
| `enterprises`| String | A list of enterprise objects. Nested `resources` blocks has the following structure.|
| `enterprises.url` | String | The URL of an enterprise.|
| `enterprises.id` | String | The enterprise ID.|
| `enterprises.enterprise_account_id` | String | The enterprise account ID.|
| `enterprises.crn` | String | The Cloud Resource Name (CRN) of an enterprise.|
| `enterprises.name`| String| The name of an enterprise.|
| `enterprises.domain`| String| The domain of an enterprise.|
| `enterprises.state` | String | The state of an enterprise.|
| `enterprises.primary_contact_iam_id` | String | The IAM ID of the primary contact of an enterprise, such as `IBMid-0123ABC`.|
| `enterprises.primary_contact_email` | String | The Email address of the primary contact of an enterprise.|
| `created_at` | String | The time stamp at which an enterprise is created.|
| `created_by` | String | The IAM ID of an user or service that created an enterprise.|
| `updated_at` | String | The time stamp at which an enterprise was last updated.|
| `updated_by` | String | The IAM ID of the user or service that updated an enterprise.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## ibm_enterprise_accounts
{: #enterprise-accounts}

Retrieve an information from an `enterprise_accounts` data source. For more information, about enterprise account, refer to [setting up accounts to an enterprise](/docs/account?topic=account-enterprise-add).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #enterprise-accounts-dssample}

```
data "ibm_enterprise_accounts" "accounts" {
}
```
{: codeblock}

### Input parameters
{: #enterprise-accounts-dsinput}

Review the input parameters that you can specify to your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|----------------|
|`name`|String|Optional| The name of an account. |
{: caption="Table. Available input parameters" caption-side="top"}


### Output parameters
{: #enterprise-accounts-dsoutput}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id` | String | The unique identifier of an accounts.|
| `accounts` | String |  A list of accounts. Nested `resources` blocks has the following structure.|
| `accounts.url` | String | The URL of an account.|
| `accounts.id` | String | The account ID.|
| `accounts.enterprise_account_id` | String | The enterprise account ID.|
| `accounts.crn` | String | The Cloud Resource Name (CRN) of an account.|
| `accounts.parent`| String| The CRN of the parent of an account.|
| `accounts.enterprise_id`| String| The enterprise ID that an account is a part of.|
| `accounts.enterprise_path`| String| The path from an enterprise to the particular account.|
| `accounts.name`| String| The name of an enterprise.|
| `accounts.state` | String | The state of an account.|
| `accounts.owner_iam_id`| String| The IAM ID of the owner of an account.|
| `accounts.paid` | String | The type of account, whether it is `free`, or `paid`.|
| `accounts.owner_email` | String | The Email address of the owner of an account.|
| `accounts.is_enterprise_account` | String |The flag to indicate whether the account is an enterprise account or not.|
| `accounts.created_at` | String | The time stamp at which an account is created.|
| `accounts.created_by` | String | The IAM ID of an user or service that created an account.|
| `accounts.updated_at` | String | The time stamp at which an account was last updated.|
| `accounts.updated_by` | String | The IAM ID of the user or service that updated an account.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## ibm_enterprise_account_groups
{: #enterprise-account-grps-ds}

Retrieve an information from an `account_groups` data source.  For more information, about enterprise account groups, refer to [setting up access groups](/docs/account?topic=account-groups).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #enterprise-account-grps-dssample}

```
data "ibm_enterprise_account_groups" "account_groups" {
}
```
{: codeblock}

### Input parameters
{: #enterprise-account-grps-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|----------------|
|`name`|String|Optional| The name of an account group.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #enterprise-account-grps-dsoutput}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
| `id` | String | The unique identifier of an account groups.|
| `account_groups` | String |  A list of account groups. Nested `resources` blocks has the following structure.|
| `account_groups.url` | String | The URL of an account group.|
| `account_groups.id` | String | The account group ID.|
| `account_groups.enterprise_account_id` | String | The enterprise account ID.|
| `account_groups.crn` | String | The Cloud Resource Name (CRN) of an account group.|
| `account_groups.parent`| String| The CRN of the parent of an account group.|
| `account_groups.enterprise_id`| String| The enterprise ID that an account group is a part of.|
| `account_groups.enterprise_path`| String| The path from an enterprise to the particular account group.|
| `account_groups.name`| String| The name of an account group.|
| `accounts_groups.state` | String | The state of an account group.|
| `account_groups.primary_contact_iam_id`| String| The IAM ID of the owner of an account group.|
| `account_groups.primary_contact_email` | String | The Email address of the owner of an account group.|
| `account_groups.created_at` | String | The time stamp at which an account is created.|
| `account_groups.created_by` | String | The IAM ID of an user or service that created an account group.|
| `account_groups.updated_at` | String | The time stamp at which an account was last updated.|
| `account_groups.updated_by` | String | The IAM ID of the user or service that updated an account group.|
{: caption="Table 1. Available output parameters" caption-side="top"}


