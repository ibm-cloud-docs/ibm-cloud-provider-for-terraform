---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-16"

keywords: terraform provider plugin, terraform secrets manager secret, terraform secrets manager secrets, secrets manager secrets, secrets manager secret

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



# Secrets Manager data sources
{: #secrets-mgr-data-sources}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_secrets_manager_secret`
{: #secrets-mgr-secret-ds}


Retrieve information about the secrets manager secret data sources.  For more information, about getting started with secrets manager, see [about secrets manager](/docs/secrets-manager?topic=secrets-manager-getting-started).
{: shortdesc}

### Sample Terraform code
{: #secrets-mgr-secret-sample}


```
data "secrets_manager_secret" "secrets_manager_secret" {
	instance_id = "36401ffc-6280-459a-ba98-456aba10d0c7"
	secret_type = "arbitrary"
	secret_id = "7dd2022c-5f54-f96d-4c32-87309e887e5"
}
```
{: codeblock}

### Input parameters
{: #secrets-mgr-secret-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`instance_id` | String | Required | The secrets manager instance GUID.|
|`secret_type` | String | Required |  The secret type. Supported options are `arbitrary`, `iam_credentials`, `username_password`.|
|`secret_id` | String | Required |  The v4 UUID that uniquely identifies the secret.|
|`endpoint_type` | String | Optional |  The type of the endpoint used to fetch secret. Supported options are `public`, and `private`. Default is `public`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #secrets-mgr-secret-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id` | String | The unique identifier of the secrets manager secret.|
|`metadata` | String | The metadata that describes the resource array. Nested `metadata` blocks have the following structure.|
|`metadata.collection_type` | String | The type of resources in the resource array.|
|`metadata.collection_total` | String | The number of elements in the resource array.|
|`type` | String | The `MIME` type that represents the secret.|
|`name` | String | A human readable alias to assign to your secret. To protect your privacy, do not use personal data, such as your name or location, as an alias for your secret.|
|`description` | String | An extended description of your secret. To protect your privacy, do not use personal data, such as your name or location, as a description for your secret.|
|`secret_group_id` | String | The `v4` UUID that uniquely identifies the secret group to assign to this secret. If you omit this parameter, your secret is assigned to the default secret group.|
|`labels` | String | Labels that you can use to filter for secrets in your instance. Only 30 labels can be created. Labels can be between `2-30` characters, including spaces. Special characters are not permitted include the angled bracket, comma, colon, ampersand, and vertical pipe character. To protect your privacy, do not use personal data, such as your name or location, as a label for your secret.|
|`state` | String | The secret state based on `NIST SP 800-57`. States are integers and correspond to the `Pre-activation = 0`, `Active = 1`, `Suspended = 2`, `Deactivated = 3`, and `Destroyed = 5` values.|
|`state_description` | String | A text representation of the secret state.|
|`crn` | String | The Cloud Resource Name (CRN) that uniquely identifies your secrets manager resource.|
|`creation_date` | String | The date the secret was created. The date format follows `RFC 3339`.|
|`created_by` | String | The unique identifier for the entity that created the secret.|
|`last_update_date` | String | Updates when the actual secret is modified. The date format follows `RFC 3339`.|
|`versions` | String | An array that contains metadata for each secret version. Nested `versions` blocks have the following structure.|
|`versions.id` | String | The ID of the secret version.
|`versions.creation_date` | String | The date that the version of the secret was created.|
|`versions.created_by` | String | The unique identifier for the entity that created the secret.|
|`versions.auto_rotated` | String | Indicates whether the version of the secret  created by automatic rotation.|
|`expiration_date` | String | The date the secret material expires. The date format follows `RFC 3339` format. You can set an expiration date on supported secret types at their creation. If you create a secret without specifying an expiration date, the secret does not expire. The `expiration_date` field is supported for the following secret types `arbitrary`, and `username_password`.|
|`secret_data` | String | Map of username, password if secret_type is `username_password` else map of payload if secret_type is `arbitrary`.|
|`payload` | String | The secret data assigned to an `arbitrary` secret.|
|`username` | String | The username assigned to an `username_password` secret.|
|`password` | String | The password assigned to an `username_password` secret.|
|`next_rotation_date` | String | The date that the secret is scheduled for automatic rotation. The service automatically creates a new version of the secret on its next rotation date. This field exists only for secrets that can be auto rotated and an existing rotation policy.|
|`ttl` | String | The time-to-live (`TTL`) or lease duration to assign to generated credentials. For `iam_credentials` secrets, the `TTL` defines for how long each generated API key remains valid. The value can be either an integer that specifies the number of seconds, or the string representation of a duration, such as 120 minutes or 24 hours.|
|`access_groups` | String | The access groups that define the capabilities of the service ID and API key that are generated for an `iam_credentials` secret. **Tip** To find the ID of an access group, go to **Manage > Access (IAM) > Access groups** in the {{site.data.keyword.cloud_notm}} console. Select the access group to inspect, and click **Details** to view its ID.|
|`api_key` | String | The API key that is generated for this secret.After the secret reaches the end of its lease (see the `ttl` field), the API key is deleted automatically. If you want to continue to use the same API key for future read operations, see the `reuse_api_key` field.|
|`service_id` | String | The service ID in which the API key (see the `api_key` field) is created. This service ID is added to the access groups that you assign for this secret.|
|`reuse_api_key` | String | (IAM credentials) Reuse the service ID and API key for future read operations.|
{: caption="Table. Available output parameters" caption-side="top"}


## `ibm_secrets_manager_secrets`
{: #secrets-mgr-secrets-ds}


Retrieve information about the secrets manager secret data sources. For more information, about getting started with secrets manager, see [about secrets manager](/docs/secrets-manager?topic=secrets-manager-getting-started).
{: shortdesc}

### Sample Terraform code
{: #secrets-mgr-secrets-sample}


```
data "secrets_manager_secrets" "secrets_manager_secrets" {
  instance_id = "36401ffc-6280-459a-ba98-456aba10d0c7"
}
```
{: codeblock}

### Input parameters
{: #secrets-mgr-secrets-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`instance_id` | String | Required | The secrets manager instance GUID.|
|`secret_type` | String | Optional |  The secret type. Supported options are `arbitrary`, `iam_credentials`, `username_password`.|
|`endpoint_type` | String | Optional |  The type of the endpoint used to fetch secret. Supported options are `public`, and `private`. Default is `public`.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #secrets-mgr-secrets-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id` | String | The unique identifier of the secrets manager secrets.|
|`metadata` | String | The metadata that describes the resource array. Nested `metadata` blocks have the following structure.|
|`metadata.collection_type` | String | The type of resources in the resource array.|
|`metadata.collection_total` | String | The number of elements in the resource array.|
|`secrets`| String | A collection of secrets. Nested `secrets` blocks have the following structure.|
|`secrets.type` | String | The `MIME` type that represents the secret.|
|`secrets.secret_id ` | String | The `v4` UUID that uniquely identifies the secret.|
|`secrets.name` | String | A human readable alias to assign to your secret. To protect your privacy, do not use personal data, such as your name or location, as an alias for your secret.|
|`secrets.description` | String | An extended description of your secret. To protect your privacy, do not use personal data, such as your name or location, as a description for your secret.|
|`secrets.secret_group_id` | String | The `v4` UUID that uniquely identifies the secret group to assign to this secret. If you omit this parameter, your secret is assigned to the default secret group.|
|`secrets.labels` | String | Labels that you can use to filter for secrets in your instance. Only 30 labels can be created. Labels can be between `2-30` characters, including spaces. Special characters are not permitted include the angled bracket, comma, colon, ampersand, and vertical pipe character (`|`). To protect your privacy, do not use personal data, such as your name or location, as a label for your secret.|
|`secrets.state` | String | The secret state based on `NIST SP 800-57`. States are integers and correspond to the `Pre-activation = 0`, `Active = 1`, `Suspended = 2`, `Deactivated = 3`, and `Destroyed = 5` values.|
|`secrets.state_description` | String | A text representation of the secret state.|
|`secrets.secret_type`| String | The secret type.|
|`crn` | String | The Cloud Resource Name (CRN) that uniquely identifies your secrets manager resource.|
|`creation_date` | String | The date the secret was created. The date format follows `RFC 3339`.|
|`created_by` | String | The unique identifier for the entity that created the secret.|
|`last_update_date` | String | Updates when the actual secret is modified. The date format follows `RFC 3339`.|
|`versions` | String | An array that contains metadata for each secret version. Nested `versions` blocks have the following structure.|
|`versions.id` | String | The ID of the secret version.
|`versions.creation_date` | String | The date that the version of the secret was created.|
|`versions.created_by` | String | The unique identifier for the entity that created the secret.|
|`versions.auto_rotated` | String | Indicates whether the version of the secret  created by automatic rotation.|
|`expiration_date` | String | The date the secret material expires. The date format follows `RFC 3339` format. You can set an expiration date on supported secret types at their creation. If you create a secret without specifying an expiration date, the secret does not expire. The `expiration_date` field is supported for the following secret types `arbitrary`, and `username_password`.|
|`secret_data` | String | Map of username, password if secret_type is `username_password` else map of payload if secret_type is `arbitrary`.|
|`payload` | String | The secret data assigned to an `arbitrary` secret.|
|`username` | String | The username assigned to an `username_password` secret.|
|`password` | String | The password assigned to an `username_password` secret.|
|`next_rotation_date` | String | The date that the secret is scheduled for automatic rotation. The service automatically creates a new version of the secret on its next rotation date. This field exists only for secrets that can be auto rotated and an existing rotation policy.|
|`ttl` | String | The time-to-live (`TTL`) or lease duration to assign to generated credentials. For `iam_credentials` secrets, the `TTL` defines for how long each generated API key remains valid. The value can be either an integer that specifies the number of seconds, or the string representation of a duration, such as 120 minutes or 24 hours.|
|`access_groups` | String | The access groups that define the capabilities of the service ID and API key that are generated for an `iam_credentials` secret. **Tip** To find the ID of an access group, go to **Manage > Access (IAM) > Access groups** in the {{site.data.keyword.cloud_notm}} console. Select the access group to inspect, and click **Details** to view its ID.|
|`api_key` | String | The API key that is generated for this secret.After the secret reaches the end of its lease (see the `ttl` field), the API key is deleted automatically. If you want to continue to use the same API key for future read operations, see the `reuse_api_key` field.|
|`service_id` | String | The service ID in which the API key (see the `api_key` field) is created. This service ID is added to the access groups that you assign for this secret.|
|`reuse_api_key` | String | (IAM credentials) Reuse the service ID and API key for future read operations.|
{: caption="Table. Available output parameters" caption-side="top"}