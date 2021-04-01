---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-01"

keywords: terraform provider plugin, terraform key management service, terraform key management, terraform kms, kms, terraform key protect, terraform kp, terraform root key, hyper protect crypto service, hpcs

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



# Key Management Service data sources
{: #kms-data-sources}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_kms_key`
{: #kms-key-ds}

Retrieves the list of keys from the Hyper Protect Crypto Services (HPCS) and Key Protect services by using the key name or alias. The region parameter in the `provider.tf` file must be set. If region parameter is not specified, `us-south` is used by default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by Terraform and the Terraform action fails. 
{: shortdesc}

### Sample Terraform code
{: #kms-key-ds-sample}

**Example to retrieve the key by using the name of the key**: 
```
data "ibm_kms_key" "test" {
  instance_id = "<guid-of-keyprotect-or hs-crypto-instance>"
  key_name = "<key_name>"
}
resource "ibm_cos_bucket" "flex-us-south" {
  bucket_name          = "atest-bucket"
  resource_instance_id = "cos-instance-id"
  region_location      = "us-south"
  storage_class        = "flex"
  key_protect          = data.ibm_kms_key.test.key.0.crn
}
```
{: codeblock}

**Example to retrieve the key by using the key alias**: 
```
data "ibm_kms_key" "test" {
  instance_id = "<guid-of-keyprotect-or hs-crypto-instance>"
  alias = "<alias_name>"
}
```
{: codeblock}

### Input parameters
{: #kms-key-ds-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`instance_id`|String|Required|The key-protect instance ID.|
|`key_name`|String|Optional|The name of the key. If you want to retrieve the key using the key alias, use the `alias` option.  You must provide either the `key_name` or `alias`. |
|`alias`|String|Optional|The alias of the key. If you want to retrieve the key using the key name, use the `key_name` option.You must provide either the `key_name` or `alias`.|
|`endpoint_type`|String|Optional|The type of the public or private endpoint to be used for fetching keys. |

### Output parameters
{: #kms-key-ds-output}

Review the output parameters that are exported.
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`keys`|String|Lists the Keys of HPCS or Key-protect instance. |
|`keys.name`|String|The name for the key. |
|`keys.aliases`|String|A list of alias names that are assigned to the key.|
|`keys.id`|String|The unique ID for the key. |
|`keys.key_ring_id`|String|The ID of the key ring that the key belongs to.|
|`keys.crn`|String|The CRN of the key. |
|`keys.standard_key`|String|Set the flag `true` for standard key, and `false` for root key. Default value is **false**.|
|`keys.policy`|String|The policies associated with the key.|
|`keys.policy.rotation`|String|The key rotation time interval in months, with a minimum of 1, and a maximum of 12.|
|`keys.policy.rotation.created_by`|String|The unique ID for the resource that created the policy.|
|`keys.policy.rotation.creation_date`|Timestamp|The date the policy was created. The date format follows RFC 3339.|
|`keys.policy.rotation.id`|String|The v4 UUID used to uniquely identify the policy resource, as specified by RFC 4122.|
|`keys.policy.rotation.interval_month`|String|The key rotation time interval in months.|
|`keys.policy.rotation.last_update_date`|Timestamp| The date when the policy last replaced or modified. The date format follows RFC 3339.|
|`keys.policy.rotation.updated_by`|String|The unique ID for the resource that updated the policy.|
|`keys.policy.dual_auth_delete`|String|The data associated with the dual authorization delete policy.|
|`keys.policy.dual_auth_delete.created_by`|String|The unique ID for the resource that created the policy.|
|`keys.policy.dual_auth_delete.creation_date`|Timestamp|The date the policy was created. The date format follows RFC 3339.|
|`keys.policy.dual_auth_delete.id`|String|The v4 UUID used to uniquely identify the policy resource, as specified by RFC 4122.|
|`keys.policy.dual_auth_delete.enabled`|String|If set to `true`, Key Protect enables a dual authorization policy on the key.|
|`keys.policy.dual_auth_delete.last_update_date`|Timestamp| The date when the policy last replaced or modified. The date format follows RFC 3339.|
|`keys.policy.dual_auth_delete.updated_by`|String|The unique ID for the resource that updated the policy.|


## `ibm_kms_keys`
{: #kms-keys-ds}

Retrieves the list of keys from the Hyper Protect Crypto Services (HPCS) and Key Protect services for the given key name. The region parameter in the `provider.tf` file must be set. If region parameter is not specified, `us-south` is used by default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by Terraform and the Terraform action fails. 
{: shortdesc}

### Sample Terraform code
{: #kms-keys-ds-sample}

```
data "ibm_kms_key" "test" {
  instance_id = "guid-of-keyprotect-or hs-crypto-instance"
  key_name = "name-of-key"
}
resource "ibm_cos_bucket" "flex-us-south" {
  bucket_name          = "atest-bucket"
  resource_instance_id = "cos-instance-id"
  region_location      = "us-south"
  storage_class        = "flex"
  key_protect          = data.ibm_kms_key.test.key.0.crn
}
```
{: codeblock}

### Input parameters
{: #kms-keys-ds-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`instance_id`|String|Required|The key-protect instance ID.|
|`key_name`|String|Optional|The name of the key. Only matching name of the keys are retrieved |
|`alias`|String|Optional|The alias of the key.|
|`endpoint_type`|String|Optional|The type of the public or private endpoint to be used for fetching keys. |

### Output parameters
{: #kms-keys-ds-output}

Review the output parameters that are exported.
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`keys`|String|Lists the Keys of HPCS or Key-protect instance. |
|`keys.name`|String|The name for the key. |
|`keys.aliases`|String|A list of alias names that are assigned to the key.|
|`keys.id`|String|The unique ID for the key. |
|`keys.key_ring_id`|String|The ID of the key ring that the key belongs to.|
|`keys.crn`|String|The CRN of the key. |
|`keys.standard_key`|String|Set the flag `true` for standard key, and `false` for root key. Default value is **false**.|
|`keys.policy`|String|The policies associated with the key.|
|`keys.policy.rotation`|String|The key rotation time interval in months, with a minimum of 1, and a maximum of 12.|
|`keys.policy.rotation.created_by`|String|The unique ID for the resource that created the policy.|
|`keys.policy.rotation.creation_date`|Timestamp|The date the policy was created. The date format follows RFC 3339.|
|`keys.policy.rotation.id`|String|The v4 UUID used to uniquely identify the policy resource, as specified by RFC 4122.|
|`keys.policy.rotation.interval_month`|String|The key rotation time interval in months.|
|`keys.policy.rotation.last_update_date`|Timestamp| The date when the policy last replaced or modified. The date format follows RFC 3339.|
|`keys.policy.rotation.updated_by`|String|The unique ID for the resource that updated the policy.|
|`keys.policy.dual_auth_delete`|String|The data associated with the dual authorization delete policy.|
|`keys.policy.dual_auth_delete.created_by`|String|The unique ID for the resource that created the policy.|
|`keys.policy.dual_auth_delete.creation_date`|Timestamp|The date the policy was created. The date format follows RFC 3339.|
|`keys.policy.dual_auth_delete.id`|String|The v4 UUID used to uniquely identify the policy resource, as specified by RFC 4122.|
|`keys.policy.dual_auth_delete.enabled`|String|If set to `true`, Key Protect enables a dual authorization policy on the key.|
|`keys.policy.dual_auth_delete.last_update_date`|Timestamp| The date when the policy last replaced or modified. The date format follows RFC 3339.|
|`keys.policy.dual_auth_delete.updated_by`|String|The unique ID for the resource that updated the policy.|

## `ibm_kp_key`
{: #kp-key}

Retrieve information about an existing Key Protect standard or root key. 
{: shortdesc}

To use the `ibm_kp_key` data source, the region parameter in the `provider.tf` file must be set to the same region that your Key Protect service instance. If region parameter is not specified, `us-south` is used by default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by Terraform and the Terraform action fails. 
{: note}

`ibm_kp_key` resource will be deprecated shortly, as a replacement, you can use `ibm_kms_keys` data source.
{: important}

### Sample Terraform code
{: #kp-key-sample}

The following example creates a read-only copy of the `mydatabase` instance in `us-east`.  
{: shortdesc}

```
data "ibm_kp_key" "test" {
  key_protect_id = "my-kp-id"
}
```
{: codeblock}

### Input parameters
{: #kp-key-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `key_protect_id`|String|Required|The ID of the Key Protect service instance.|
| `key_name`| String|Optional| The name of the key. Only the keys with matching name will be retrieved.|
{: caption="Table. Available input parameters" caption-side="top"}


### Output parameters
{: #kp-key-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `keys` | List of objects | A list of all keys in your Key Protect service instance.|
| `keys.name`|String| The name of the key.|
| `keys.id`|String| The unique identifier of the key.|
| `keys.crn`|String| The CRN of the key.|
| `keys.standard_key` |Boolean|Set the flag `true` for standard key, and `false` for root key. Default value is **false**. |
