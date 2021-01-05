---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-05"

keywords: terraform provider plugin, terraform key management service, terraform key management, terraform kms, kms, terraform key protect, terraform kp, terraform root key, hyper protect crypto service, hpcs

subcollection: terraform

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:step: data-tutorial-type='step'}


# Key Management Service data sources
{: #kms-data-sources}

You can reference the output parameters for each resource in other resources or data sources by using [IBM Cloud Provider plug-in for Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/terraform?topic=terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your IBM Cloud Provider plug-in for Terraform configuration file. 
{: important}

## `ibm_kms_key`
{: #kms-key-ds}

Retrieves the list of keys from the Hyper Protect Crypto Services (HPCS) and Key Protect services for the given key name. The region parameter in the `provider.tf` file must be set. If region parameter is not specified, `us-south` is used by default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by IBM Cloud Provider plug-in for Terraform and the IBM Cloud Provider plug-in for Terraform action fails. 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #kms-key-ds-sample}

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

### Input parameters
{: #kms-key-ds-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`instance_id`|String|Required|The key-protect instance ID.|
|`key_name`|String|Required|The name of the key. Only matching name of the keys are retrieved |
|`endpoint_type`|String|Optional|The type of the public or private endpoint to be used for fetching keys. |

### Output parameters
{: #kms-key-ds-output}

Review the output parameters that are exported.
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`keys`|String|Lists the Keys of HPCS or Key-protect instance. |
|`keys.name`|String|The name for the key. |
|`keys.id`|String|The unique ID for the key. |
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

Retrieves the list of keys from the Hyper Protect Crypto Services (HPCS) and Key Protect services for the given key name. The region parameter in the `provider.tf` file must be set. If region parameter is not specified, `us-south` is used by default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by IBM Cloud Provider plug-in for Terraform and the IBM Cloud Provider plug-in for Terraform action fails. 
{: shortdesc}

### Sample IBM Cloud Provider plug-in for Terraform code
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

### Input parameters
{: #kms-keys-ds-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`instance_id`|String|Required|The key-protect instance ID.|
|`key_name`|String|Optional|The name of the key. Only matching name of the keys are retrieved |
|`endpoint_type`|String|Optional|The type of the public or private endpoint to be used for fetching keys. |

### Output parameters
{: #kms-keys-ds-output}

Review the output parameters that are exported.
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`keys`|String|Lists the Keys of HPCS or Key-protect instance. |
|`keys.name`|String|The name for the key. |
|`keys.id`|String|The unique ID for the key. |
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

To use the `ibm_kp_key` data source, the region parameter in the `provider.tf` file must be set to the same region that your Key Protect service instance. If region parameter is not specified, `us-south` is used by default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by IBM Cloud Provider plug-in for Terraform and the IBM Cloud Provider plug-in for Terraform action fails. 
{: note}

`ibm_kp_key` resource will be deprecated shortly, as a replacement, you can use `ibm_kms_keys` data source.
{: important}

### Sample IBM Cloud Provider plug-in for Terraform code
{: #kp-key-sample}

The following example creates a read-only copy of the `mydatabase` instance in `us-east`.  
{: shortdesc}

```
data "ibm_kp_key" "test" {
  key_protect_id = "my-kp-id"
}
```

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
