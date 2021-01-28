---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider plugin, terraform key management service, terraform key management, terraform kms, kms, terraform key protect, terraform kp, terraform root key, hyper protect crypto service, HPCS

subcollection: ibm-cloud-provider-for-terraform

---

{[METADATA_ATTRIBUTES]}


# Key Management Service resources
{: #kms-resources}

Create, modify, or delete [{{site.data.keyword.cloud_notm}} Key Protect](/docs/key-protect?topic=key-protect-about) resources.
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_kms_key`
{: #kms-key}

This resource can be used for management of keys in both Key Protect and Hyper Protect Crypto Service (HPCS). It allows standard and root keys to be created and deleted. The region parameter in the `provider.tf` file must be set. If region parameter is not specified, `us-south` is used as default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by Terraform and the Terraform action fails. 
{: shortdesc}

After creating an  Hyper Protect Crypto Service instance you need to initialize the instance properly with the crypto units, in order to create, or manage Hyper Protect Crypto Service keys. For more information, about how to initialize the Hyper Protect Crypto Service instance, see [Initialize Hyper Protect Crypto](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) only for HPCS instance. 
{: note}


### Example usage to provision Key Protect service and Key Management
{: #kms-key-sample}

```
resource "ibm_resource_instance" "kms_instance" {
  name     = "instance-name"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}
resource "ibm_kms_key" "test" {
  instance_id  = ibm_resource_instance.kms_instance.guid
  key_name     = "key-name"
  standard_key = false
  force_delete = true
}
resource "ibm_cos_bucket" "flex-us-south" {
  bucket_name          = "atest-bucket"
  resource_instance_id = "cos-instance-id"
  region_location      = "us-south"
  storage_class        = "flex"
  key_protect          = ibm_kms_key.test.id
}
```
### Example usage to provision HPCS and Key Management
{: #hpcs-key-sample}

Complete the following steps to provision an HPCS, initialize the service and Key Management:
{: shortdesc}

**Step 1: Provision the service by using `ibm_resource_instance`**

 ```
 resource "ibm_resource_instance" "hpcs"{
  name = "hpcsservice"
  service = "hs-crypto"
  plan = "standard"
  location = "us-south"
  parameters = {
      units = 2
  }
}

 ```
 **Step 2: Initialize your service instance manually**
 
 1. To manage your keys, you need to initialize your service instance.
 2. The two options that are provided to initialize a service instance are: 
    - The IBM HPCS management utilities by using master key parts stored on smart card.
    - The {{site.data.keyword.cloud_notm}} Trusted Key Entry CLI plug-in to initialize your service instance.
    For more information, about initialize the service instance, refer [Initialize your service instance](/docs/hs-crypto?topic=hs-crypto-get-started#initialize-crypto).
    
**Step 3: Manage your keys by using `ibm_kms_key`**
 
```
  resource "ibm_kms_key" "key" {
  instance_id  = ibm_resource_instance.hpcs.guid
  key_name     = var.key_name
  standard_key = false
  force_delete = true
}
```

### Example usage to provision Key Management Service Key with Key Policies
{: #kms-key-policies-sample}

Set policies for a key, for an automatic rotation policy or a dual authorization policy to protect against the accidental deletion of keys.
{: shortdesc}

```
resource "ibm_resource_instance" "kp_instance" {
  name     = "test_kp"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}
resource "ibm_kms_key" "key" {
  instance_id = ibm_resource_instance.kp_instance.guid
  key_name       = "key"
  standard_key   = false
  expiration_date = "2020-12-05T15:43:46Z"
  policies {
    rotation {
      interval_month = 3
    }
    dual_auth_delete {
      enabled = false
    }
  }
}
```

### Example usage to provision Key Management Service and Import a Key
{: #kms-import-key-sample}

Provision Key Management Service and import a key by using `ibm_resource_instance` and `ibm_kms_key`.
{: shortdesc}

```
resource "ibm_resource_instance" "kp_instance" {
  name     = "test_kp"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}
resource "ibm_kms_key" "key" {
  instance_id = ibm_resource_instance.kp_instance.guid
  key_name       = "key"
  standard_key   = false
  payload = "aW1wb3J0ZWQucGF5bG9hZA=="
}
```

### Input parameters
{: #kms-key-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`endpoint_type`|String|Optional|The type of the public or private endpoint to be used for creating keys. | Yes |
|`encrypted_nonce`|String|Optional|The encrypted nonce value that verifies your request to import a key to Key Protect. This value must be encrypted by using the key that you want to import to the service. To retrieve a nonce, use the `ibmcloud kp import-token get` command. Then, encrypt the value by running `ibmcloud kp import-token encrypt-nonce`. Only for imported root key.| Yes |
|`expiration_date`|String|Optional| Expiry date of the key material. The date format follows with RFC 3339. You can set an expiration date on any key on its creation. A key moves into the deactivated state within one hour past its expiration date, if one is assigned. If you create a key without specifying an expiration date, the key does not expire. For example, `2018-12-01T23:20:50.52Z`.|  Yes |
|`force_delete`|Boolean|Optional|If set to **true**, Key Protect forces the deletion of a root or standard key, even if this key is still in use, such as to protect an {{site.data.keyword.cos_full_notm}} bucket. Note that the key cannot be deleted if the protected cloud resource is set up with a retention policy. Successful deletion includes the removal of any registrations that are associated with the key. Default value is **false**.| No |
|`instance_id`|String|Required|The HPCS or key-protect instance ID.| Yes |
|`iv_value`|String|Optional| Used with import tokens. The initialization vector (IV) that is generated when you encrypt a nonce. The IV value is required to decrypt the encrypted nonce value that you provide when you make a key import request to the service. To generate an IV, encrypt the nonce by running `ibmcloud kp import-token encrypt-nonce`. Only for imported root key.|  Yes |
|`key_name`|String|Required|The name of the key.| Yes |
|`payload`|String|Optional| The base64 encoded key that you want to store and manage in the service. To import an existing key, provide a 256-bit key. To generate a new key, omit this parameter.| Yes |
|`standard_key`|Bool|Optional|Set flag `true` for standard key, and `false` for root key. Default value is **false**.| Yes |
|`policies`|List|Optional|Set policies for a key, for an automatic rotation policy or a dual authorization policy to protect against the accidental deletion of keys. Policies follow the following structure.| No |
|`policies.rotation`|List|Optional|Specifies the key rotation time interval in months, with a minimum of 1, and a maximum of 12. | No |
|`policies.rotation.interval_month`|Integer|Required|Specifies the key rotation time interval in months. CONSTRAINTS: 1 ≤ value ≤ 12 **NOTE:** Rotation policy cannot be set for standard key and imported key. Once the rotation policy is set, it cannot be unset or removed by using Terraform. | No |
|`policies.dual_auth_delete`|List|Required|Data associated with the dual authorization delete policy.| No |
|`policies.dual_auth_delete.enabled`|Bool|Required|If set to `true`, Key Protect enables a dual authorization policy on a single key. **NOTE:** Once the dual authorization policy is set on the key, it cannot be reverted. A key with dual authorization policy enabled cannot be destroyed by using Terraform.| No |


### Output parameters
{: #kms-key-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The CRN of the key.|
|`crn`|String|The CRN of the key.|
|`status`|String|The status of the key.|
|`key_id`|String|The ID of the key.|
|`type`|String|The type of the key KMS or HPCS.|
|`policy`|String|The policies associated with the key.|
|`policy.rotation`|String|The key rotation time interval in months, with a minimum of 1, and a maximum of 12.|
|`policy.rotation.created_by`|String|The unique ID for the resource that created the policy.|
|`policy.rotation.creation_date`|Timestamp|The date the policy was created. The date format follows RFC 3339.|
|`policy.rotation.crn`|String|The Cloud Resource Name (CRN) that uniquely identifies your cloud resources.|
|`policy.rotation.id`|String|The v4 UUID used to uniquely identify the policy resource, as specified by RFC 4122.|
|`policy.rotation.interval_month`|String|The key rotation time interval in months.|
|`policy.rotation.last_update_date`|Timestamp| The date when the policy last replaced or modified. The date format follows RFC 3339.|
|`policy.rotation.updated_by`|String|The unique ID for the resource that updated the policy.|
|`policy.dual_auth_delete`|String|The data associated with the dual authorization delete policy.|
|`policy.dual_auth_delete.created_by`|String|The unique ID for the resource that created the policy.|
|`policy.dual_auth_delete.creation_date`|Timestamp|The date the policy was created. The date format follows RFC 3339.|
|`policy.dual_auth_delete.crn`|String|The Cloud Resource Name (CRN) that uniquely identifies your cloud resources.|
|`policy.dual_auth_delete.id`|String|The v4 UUID used to uniquely identify the policy resource, as specified by RFC 4122.|
|`policy.dual_auth_delete.enabled`|String|If set to `true`, Key Protect enables a dual authorization policy on the key.|
|`policy.dual_auth_delete.last_update_date`|Timestamp| The date when the policy last replaced or modified. The date format follows RFC 3339.|
|`policy.dual_auth_delete.updated_by`|String|The unique ID for the resource that updated the policy.|

### Import
{: #kms-key-import}

`ibm_kms_key` can be imported by using the `id` and `crn`.

**Example**

```
terraform import ibm_kms_key.crn crn:v1:bluemix:public:kms:us-south:a/faf6addbf6bf4768hhhhe342a5bdd702:05f5bf91-ec66-462f-80eb-8yyui138a315:key:52448f62-9272-4d29-a515-15019e3e5asd
```
{: pre}

## `ibm_kp_key`
{: #kp-key}

Create, or delete a Key Protect standard or root key.  
{: shortdesc}

To use the `ibm_kp_key` resource, the region parameter in the `provider.tf` file must be set to the same region that your Key Protect service instance. If region parameter is not specified, `us-south` is used as default. If the region in the `provider.tf` file is different from the Key Protect instance, the instance cannot be retrieved by Terraform and the Terraform action fails. 
{: note}

`ibm_kp_key` resource will be deprecated shortly, as a replacement, you can use `ibm_kms_key` resource.
{: important}

### Sample Terraform code
{: #kp-key-sample}

```
resource "ibm_resource_instance" "kp_instance" {
  name     = "instance-name"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}
resource "ibm_kp_key" "test" {
  key_protect_id  = ibm_resource_instance.kp_instance.guid
  key_name     = "key-name"
  standard_key = false
}
resource "ibm_cos_bucket" "flex-us-south" {
  bucket_name          = "atest-bucket"
  resource_instance_id = "cos-instance-id"
  region_location      = "us-south"
  storage_class        = "flex"
  key_protect          = ibm_kp_key.test.id
}
```

### Input parameters
{: #kp-key-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`key_protect_id`|String|Required|The Key Protect service instance ID.| Yes |
|`key_name`|String|Required|The name of the key.| Yes |
|`standard_key`|Boolean|Optional|Set flag `true` for standard key, and `false` for root key. Default value is **false**.| Yes |
|`payload`|String|Optional| The base64 encoded key that you want to store and manage in the service. To import an existing key, provide a 256-bit key. To generate a new key, omit this parameter.| Yes |
|`encrypted_nonce`|String|Optional|The encrypted nonce value that verifies your request to import a key to Key Protect. This value must be encrypted by using the key that you want to import to the service. To retrieve a nonce, use the `ibmcloud kp import-token get` command. Then, encrypt the value by running `ibmcloud kp import-token encrypt-nonce`. Only for imported root key.| Yes |
|`force_delete`|Boolean|Optional|If set to **true**, Key Protect forces the deletion of a root or standard key, even if this key is still in use, such as to protect an {{site.data.keyword.cos_full_notm}} bucket. Note, the key cannot be deleted if the protected cloud resource is set up with a retention policy. Successful deletion includes the removal of any registrations that are associated with the key. Default value is **false**.| No |
|`iv_value`|String|Optional| Used with import tokens. The Initialization Vector (IV) that is generated when you encrypt a nonce. The IV value is required to decrypt the encrypted nonce value that you provide when you make a key import request to the service. To generate an IV, encrypt the nonce by running `ibmcloud kp import-token encrypt-nonce`. Only for imported root key.|  Yes |

### Output parameters
{: #kp-key-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The CRN of the key.|
|`crn`|String|The CRN of the key.|
|`status`|String|The status of the key.|
|`key_id`|String|The ID of the key.|

### Import
{: #kp-key-import}

`ibm_kp_key` can be imported by using the `id` and `crn`.

```
terraform import ibm_kp_key.crn crn:v1:bluemix:public:kms:us-south:a/faf6addbf6bf4768hhhhe342a5bdd702:05f5bf91-ec66-462f-80eb-8yyui138a315:key:52448f62-9272-4d29-a515-15019e3e5asd
```
{: pre}

