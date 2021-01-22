---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-22"

keywords: terraform identity and access, terraform iam, terraform permissions, terraform iam policy

subcollection: ibm-cloud-provider-for-terraform

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


# Identity & Access (IAM) resources 
{: #iam-resources}

Create, modify, or delete [{{site.data.keyword.cloud_notm}} Identity and Access Management (IAM)](/docs/account?topic=account-iamoverview) resources. 
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/terraform?topic=terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_iam_access_group`
{: #iam-access-group}

Create, modify, or delete an IAM access group. Access groups can be used to define a set of permissions that you want to grant to a group of users. 
{: shortdesc}

### Sample Terraform code
{: #iam-access-group-sample}

The following example creates an access group that is named `mygroup`. 

```
resource "ibm_iam_access_group" "accgrp" {
  name        = "mygroup"
  description = "New access group"
}
```

### Input parameters
{: #iam-access-group-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `description` | String | Optional | The description of the access group. |
| `name` | String | Required | The name of the access group. |
| `tags` | Array of strings | Optional|The list of tags that you want to associated with your access group. |

`Tags` are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.
{: note}

### Output parameters
{: #iam-access-group-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the access group. |
| `version` | String | The version of the access group. |





## `ibm_iam_access_group_members`
{: #iam-access-group-members}

Add, update, or remove users from an IAM access group. 
{: shortdesc}

Multiple `ibm_iam_access_group_members` resources with the same group name produce inconsistent behavior. 
{: important}

### Sample Terraform code
{: #iam-access-group-members-sample}

The following example creates an IAM access group and a service ID. Then, the service ID and a user with the ID `user@ibm.com` is added to the access group. 

```
resource "ibm_iam_access_group" "accgroup" {
  name = "testgroup"
}

resource "ibm_iam_service_id" "serviceID" {
  name = "testserviceid"
}

resource "ibm_iam_access_group_members" "accgroupmem" {
  access_group_id = ibm_iam_access_group.accgroup.id
  ibm_ids         = ["user@iibm.com"]
  iam_service_ids = [ibm_iam_service_id.serviceID.id]
}

```

### Input parameters
{: #iam-access-group-members-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
| `access_group_id` | String | Required | The ID of the access group. | 
| `ibm_ids` | Array of strings | Optional | A list of IBM IDs that you want to add to or remove from the access group. | 
| `iam_service_ids` | Array of strings | Optional | A list of service IDS that you want to add to or remove from the access group. |


### Output parameters
{: #iam-access-group-members-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
| `id` | String | The unique identifier of the access group members. The ID is returned in the format `<iam_access_group_ID>/<random_ID>`. | 
| `members` | Array of objects | A list of members that are included in the access group. |
| `members.iam_id` | String | The IBMid or service ID of the member. |
| `members.type` | String | The type of member. Supported values are `user` or `service`. 

### Import

`ibm_iam_access_group_members` can be imported by using access group ID and random id, eg

```
$ terraform import ibm_iam_access_group_members.example AccessGroupId-5391772e-1207-45e8-b032-2a21941c11ab/2018-10-04 06:27:40.041599641 +0000 UTC
```





## `ibm_iam_access_group_policy`
{: #iam-access-group-policy}

Create, update, or delete an IAM policy for an IAM access group. 
{: shortdesc}

### Sample Terraform code
{: #iam-access-group-policy-sample}

#### Create a policy for all IAM-enabled resources
{: #all-iam-services}

The following example creates an IAM policy that grants members of the access group the IAM `Viewer` platform role to all IAM-enabled services. 
{: shortdesc}

```
resource "ibm_iam_access_group" "accgrp" {
  name = "test"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles        = ["Viewer"]
}
```

#### Create a policy for all IAM-enabled services within a resource group
{: #all-iam-services-resource-group}

The following example creates an IAM policy that grants members of the access group the IAM `Operator` platform role and the `Writer` service access role to all IAM-enabled services within a resource group. 
{: shortdesc}

```
resource "ibm_iam_access_group" "accgrp" {
  name = "test"
}

data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles        = ["Operator", "Writer"]

  resources {
    resource_group_id = data.ibm_resource_group.group.id
  }
}
```

#### Create a policy for all instances of an {{site.data.keyword.cloud_notm}} service
{: #single-service}

The following example creates an IAM policy that grants members of the access group the IAM `Viewer` platform role to all service instances of {{site.data.keyword.cos_full_notm}}. 
{: shortdesc}

```
resource "ibm_iam_access_group" "accgrp" {
  name = "test"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles        = ["Viewer"]

  resources {
    service = "cloud-object-storage"
  }
}

```
#### Create a policy for a service instance 
{: #single-service-instance}

The following example creates an IAM policy that grants members of the access group the IAM `Viewer` and `Administrator` platform role, and the `Manager` service access role to a single service instance. 
{: shortdesc}

```
resource "ibm_iam_access_group" "accgrp" {
  name = "test"
}

resource "ibm_resource_instance" "instance" {
  name     = "test"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles        = ["Manager", "Viewer", "Administrator"]

  resources {
    service              = "kms"
    resource_instance_id = element(split(":",ibm_resource_instance.instance.id),7)
  }
}

```

#### Create a policy to all instances of an {{site.data.keyword.cloud_notm}} service within a resource group
{: #instances-resource-group}

The following example creates an IAM policy that grants members of the access group the IAM `Viewer` platform role to all instances of {{site.data.keyword.containerlong_notm}} that are created within a specific resource group. 
{: shortdesc}

```
resource "ibm_iam_access_group" "accgrp" {
  name = "test"
}

data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles        = ["Viewer"]

  resources {
    service           = "containers-kubernetes"
    resource_group_id = data.ibm_resource_group.group.id
  }
}

```

#### Access Group Policy by using resource and resource type 

```
resource "ibm_iam_access_group" "accgrp" {
  name = "test"
}

data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles        = ["Administrator"]

  resources {
    resource_type = "resource-group"
    resource      = data.ibm_resource_group.group.id
  }
}

```

#### Access Group Policy by using attributes

```
resource "ibm_iam_access_group" "accgrp" {
  name = "test"
}

data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_access_group_policy" "policy" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles           = ["Viewer"]

  resources {
    service = "is"

    attributes {
      "vpcId" = "*"
    }

    resource_group_id = data.ibm_resource_group.group.id
  }
}

resource "ibm_iam_access_group_policy" "policy_kube" {
  access_group_id = ibm_iam_access_group.accgrp.id
  roles           = ["Viewer", "Manager"]
  
  resources {
    service              = "containers-kubernetes"
    resource_instance_id = "myinstance"
    
    attributes = {
      "namespace" = "default"
    }
  }
}
```

### Input parameters
{: #iam-access-group-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| -------- |
|`access_group_id`|String|Required|The ID of the access group.| Yes |
| `roles`|List|Required| A comma separated list of roles. Valid roles are `Writer`, `Reader`, `Manager`, `Administrator`, `Operator`, `Viewer`, and `Editor`. | No |
|`resources` |List|Optional|A nested block describes the resource of this policy.|  No |
|`resources.service`|String|Optional|The service name that you want to include in your policy definition. For account management services, you can find supported values in the [documentation](/docs/account?topic=account-account-services#api-acct-mgmt). For other services, run the `ibmcloud catalog service-marketplace` command and retrieve the value from the **Name** column of your CLI output. | No |
|`resources.resource_instance_id`|String|Optional|The ID of resource instance of the policy definition.| No |
|`resources.region` |String|Optional|The region of the policy definition.| No |
|`resources.resource_type` |String|Optional|The resource type of the policy definition.| No |
|`resources.resource` |String|Optional|The resource of the policy definition.| No |
|`resources.resource_group_id`|String|Optional|The ID of the resource group. To retrieve the ID, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. | No |
|`resources.attributes`|Map|Optional|Set resource attributes in the form of `name=value,name=value`.  If you set this option, do not specify `account_management` at the same time. | No |
|`account_management`|Boolean|Optional|Gives access to all account management services if set to `true`. Default value `false`. If you set this option, do not specify `resources` at the same time. | No |
|`tags` |Array of Strings|Optional|A list of tags that you want to add to the access group policy. Tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |

### Output parameters
{: #iam-access-group-policy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The unique identifier of the access group policy. The ID is composed of `<access_group_id>/<access_group_policy_id>`.|
|`version`|String|The version of the access group policy.|

### Import
{: #iam-access-group-policy-import}

The access group policy can be imported by using the access group ID and the access group policy ID.

```
$ terraform import ibm_iam_access_group_policy.example <access_group_ID>/<access_group_policy_ID>
```





## `ibm_iam_access_group_dynamic_rule`
{: #iam-group-dynamic-rule}

Create, update, or delete a dynamic rule for an IAM access group. With dynamic rules, you can automatically add federated users to access groups based on specific identity attributes. When your users log in with a federated ID, the data from the identity provider dynamically maps your users to an access group based on the rules that you set.
{: shortdesc}

For more information, see [Creating dynamic rules for access groups](/docs/account?topic=account-rules). 

### Sample Terraform code
{: #iam-group-dynamic-rule-sample}

```
resource "ibm_iam_access_group_dynamic_rule" "rule1" {
  name              = "newrule"
  access_group_id   = "AccessGroupId-dsnd4bvsaf"
  expiration        = 4
  identity_provider = "test-idp.com"
  conditions {
    claim    = "blueGroups"
    operator = "CONTAINS"
    value    = "\"test-bluegroup-saml\""
  }
}
```
{: codeblock}

### Input parameters
{: #iam-group-dynamic-rule-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the dynamic rule for the IAM access group.|
|`access_group_id`|String|Required|The ID of the access group.|
|`expiration`|Integer|Required|The number of hours that authenticated users can work in IBM Cloud before they must refresh their access. This value must be between 1 and 24. |
|`identity_provider`|String|Required|Enter the URI for your identity provider. This is the SAML `entity ID` field, which is sometimes referred to as the issuer ID, for the identity provider as part of the federation configuration for onboarding with IBMid. For example, `https://idp.example.org/SAML2`.|
|`conditions`|List of rule conditions|Required|A list of conditions that the rule must satisfy.|
|`conditions.claim`|String|Required|The key value to evaluate the condition against. The key that you enter depends on what key-value pairs your identity provider provides. For example, your identity provider might include a key that is named `blueGroups` and that holds all the user groups that have access. To apply a condition for a specific user group within the `blueGroups` key, you specify `blueGroups` as your claim and add the value that you are looking for in `conditions.value`. |
|`conditions.operator`|String|Required|The operation to perform on the claim. Supported values are `EQUALS`, `EQUALS_IGNORE_CASE`, `IN`, `NOT_EQUALS_IGNORE_CASE`, `NOT_EQUALS`, and `CONTAINS`.|
|`conditions.value`|String|Required|The value that the claim is compared by using the `conditions.operator`.|

### Output parameters
{: #iam-group-dynamic-rule-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The unique identifier of the dynamic rule. The ID is composed of `<access_group_ID>/<rule_ID>`. |
|`rule_id`|String|The ID of the rule.|

### Import 
{: #iam-group-dynamic-rule-import}

The dynamic rule can be imported by using the access group ID and rule ID. 

```
terraform import ibm_iam_access_group_dynamic_rule.example <access_group_ID>/<rule_ID>
```
{: pre}





## `ibm_iam_authorization_policy`
{: #iam-auth-policy}

Create or delete an IAM service authorization policy. 
{: shortdesc} 

### Sample Terraform code
{: #iam-auth-policy-sample}

#### Authorization policy between two services

```
resource "ibm_iam_authorization_policy" "policy" {
  source_service_name = "cloud-object-storage"
  target_service_name = "kms"
  roles               = ["Reader"]
}
```

#### Authorization policy between two services with specific resource type

```
resource "ibm_iam_authorization_policy" "policy" {
  source_service_name  = "is"
  source_resource_type = "image"
  target_service_name  = "cloud-object-storage"
  roles                = ["Reader"]
}
```

#### Authorization policy between two specific instances

```
resource "ibm_resource_instance" "instance1" {
  name     = "mycos"
  service  = "cloud-object-storage"
  plan     = "lite"
  location = "global"
}

resource "ibm_resource_instance" "instance2" {
  name     = "mykms"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}

resource "ibm_iam_authorization_policy" "policy" {
  source_service_name         = "cloud-object-storage"
  source_resource_instance_id = ibm_resource_instance.instance1.id
  target_service_name         = "kms"
  target_resource_instance_id = ibm_resource_instance.instance2.id
  roles                       = ["Reader"]
}
```

#### Authorization policy between two resource groups

```
resource "ibm_resource_group" "source_resource_group" {
  name     = "rg1"
}
	  
resource "ibm_resource_group" "target_resource_group" {
  name     = "rg2"
}

resource "ibm_iam_authorization_policy" "policy" {
  source_service_name         = "cloud-object-storage"
  source_resource_group_id    = ibm_resource_group.source_resource_group.id
  target_service_name         = "kms"
  target_resource_group_id    = ibm_resource_group.target_resource_group.id
  roles                       = ["Reader"]
}
```
{:  codeblock}

### Input parameters
{: #iam-auth-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------ |
|`source_service_name`|String|Required|The source service name.| Yes |
|`target_service_name`|String|Required|The target service name.| Yes |
|`roles`|List|Required|A comma separated list of roles. | No |
|`source_resource_instance_id`|String|Optional|The source resource instance ID.| Yes |
|`target_resource_instance_id`|String|Optional| The target resource instance ID.| Yes |
|`source_resource_type`|String|Optional| The resource type of the source service.| Yes |
|`target_resource_type`|String|Optional|The resource type of the target service.| Yes |
|`source_resource_group_id`|String|Optional|The ID of the resource group from which you want to allow access to IBM Cloud services in another resource group.| Yes |
|`target_resource_group_id`|String|Optional|The ID of the resource group that holds the IBM Cloud services that you want to allow access to.|  Yes |
|`source_service_account`|String|Optional|The GUID of the account where the source service is provisioned.| Yes |

### Output parameters
{: #iam-auth-policy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The unique identifier of the authorization policy.|
|`version`|String|The version of the authorization policy.|

### Import
{: #iam-auth-policy-import}

The IAM authorization policy can be imported by using the ID. 

```
terraform import ibm_iam_authorization_policy.example 11aa1a11-11a1-11aa-1111-11111a11a11a
```

## `ibm_iam_authorization_policy_detach`
{: #iam-auth-policy-detach}

Provides a resource for IAM Service Authorizations policy to be detached. This allows authorization policy to deleted.
{: shortdesc}

### Sample Terraform code
{: #iam-auth-policy-detach-sample}

```
resource "ibm_iam_authorization_policy_detach" "policy" {
  authorization_policy_id = "11aa1a11-11a1-11aa-1111-11111a11a11a"
}
```

### Input parameters
{: #iam-auth-policy-detach-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Name | Data type | Required / optional|Description | Forces new resource |
|----|-----------|-----------|---------------------| ---------|
|`authorization_policy_id`|String|Required|The authorization policy ID.| Yes |

### Output parameters
{: #iam-auth-policy-detach-output}

This resource does not provide output parameters. 
{: shortdesc}





## `ibm_iam_custom_role`
{: #iam-custom-role}

Create, update, or delete a custom IAM role. 
{: shortdesc}

For more information, about IAM custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

### Sample Terraform code
{: #iam-custom-role-sample}

```
resource "ibm_iam_custom_role" "customrole" {
  name         = "Role1"
  display_name = "Role1"
  description  = "This is a custom role"
  service = "kms"
  actions      = ["kms.secrets.rotate"]
}
```
{: codeblock}

### Input parameters
{: #iam-custom-role-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the custom role.|
|`display_name`|String|Required|The display name of the custom role.|
|`description`|String|Optional|The description of the custom role. Make sure to include information about the level of access this role assignment gives a user. |
|`service`|String|Required|The name of the service for which you want to create the custom role. To retrieve the name, run `ibmcloud catalog service-marketplace`.
|`actions`|Array of strings|Required|A list of action IDs that you want to add to your custom role. The action IDs vary by service. To retrieve supported action IDs, follow the [documentation](/docs/account?topic=account-custom-roles) to create the custom role from the UI. |

### Output parameters
{: #iam-custom-role-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the custom role.|
|`crn`|String|The CRN of the custom role.|





## `ibm_iam_service_api_key`
{: #iam-service-api-key}

Create, update, or delete an IAM service API key by using resource group and resource type.For more information, about IAM service API key, see [Managing IAM acces, API keys](/docs/cli?topic=cli-ibmcloud_commands_iam).
{: shortdesc}

### Sample Terraform code
{: #iam-service-api-key-code}

```
resource "ibm_iam_service_id" "serviceID" {
  name = "servicetest"
}

resource "ibm_iam_service_api_key" "testacc_apiKey" {
  name = "testapikey"
  iam_service_id = ibm_iam_service_id.serviceID.iam_id
}
```

### Input parameters
{: #iam-service-api-key-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the service API key.|
|`description` |String|Optional|The description of the service API key.|
|`iam_service_id` |String|Required|The IAM ID of the service.|
|`apikey` |String|Optional|The API key value. This property only contains the API key value for the following cases: `create an API key`, `update a Service API key that stores the API key value as retrievable`, or `get a service API key that stores the API key value as retrievable`. All other operations do not return the API key value. For example, all user API key related operations, except for create, do not contain the API key value.|
|`locked`|Bool|Optional| The API key cannot be changed if set to `true`.|
|`store_value`|Bool|Optional| The boolean value whether API key value is retrievable in the future.|
|`file`|String|Optional| The file name where API key is to be stored.|

### Output parameters
{: #iam-service-api-key-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`account_id` |String| The account Id of the API key.|
|`entity_tag `| String|The version or entity tag of the service API key.|
|`id`|String|The unique identifier of the API key.|
|`crn` |String| The `CRN` of the service API key.|
|`created_by`|String|The IAM ID of the service that is created by the API key.|
|`created_at`|String|The date and time service API key was created.|
|`modified_at`|String|The date and time service API key was modified.|





### Import
{: #iam-service-api-key-import}

The `ibm_iam_service_api_key` can be imported by using service API Key.

**Example**

```
terraform import ibm_iam_service_api_key.testacc_apiKey ApiKey-9d12342134f-41c2-a541-7b0be37c3da0
```

## `ibm_iam_service_id`
{: #iam-service-id}

Create, update, or delete an IAM service ID by using resource group and resource type.
{: shortdesc}

### Sample Terraform code
{: #iam-service-id-sample}

```
resource "ibm_iam_service_id" "serviceID" {
  name        = "test"
  description = "New ServiceID"
}
```

### Input parameters
{: #iam-service-id-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|The name of the service ID.|
|`description` |String|Optional|The description of the service ID.|
|`tags`|Array of strings|Optional| A list of tags that you want to add to the service ID. The tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.|

### Output parameters
{: #iam-service-id-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`crn` |String| The CRN of the service ID.|
|`iam_id`| String|The IAM ID of the service ID.  |
|`id`|String|The unique identifier of the service ID.|
|`version` |String| The version of the service ID.|





## `ibm_iam_service_policy`
{: #iam-service-policy}

Create, update, or delete an IAM service policy. 
{: shortdesc}

### Sample Terraform code
{: #iam-service-policy-sample}

#### Service Policy for All Identity and Access enabled services 

```
resource "ibm_iam_service_id" "serviceID" {
  name = "test"
}

resource "ibm_iam_service_policy" "policy" {
  iam_service_id = ibm_iam_service_id.serviceID.id
  roles        = ["Viewer"]
}

```

#### Service Policy by using service with region

```
resource "ibm_iam_service_id" "serviceID" {
  name = "test"
}

resource "ibm_iam_service_policy" "policy" {
  iam_service_id = ibm_iam_service_id.serviceID.id
  roles        = ["Viewer"]

  resources {
    service = "cloud-object-storage"
    region = "us-south"
  }
}

```
#### Service Policy by using resource instance 

```
resource "ibm_iam_service_id" "serviceID" {
  name = "test"
}

resource "ibm_resource_instance" "instance" {
  name     = "test"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}

resource "ibm_iam_service_policy" "policy" {
  iam_service_id = ibm_iam_service_id.serviceID.id
  roles        = ["Manager", "Viewer", "Administrator"]

  resources {
    service              = "kms"
    resource_instance_id = element(split(":",ibm_resource_instance.instance.id),7)
  }
}

```

#### Service Policy by using resource group

```
resource "ibm_iam_service_id" "serviceID" {
  name = "test"
}

data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_service_policy" "policy" {
  iam_service_id = ibm_iam_service_id.serviceID.id
  roles        = ["Viewer"]

  resources {
    service           = "containers-kubernetes"
    resource_group_id = data.ibm_resource_group.group.id
  }
}

```

#### Service Policy by using resource and resource type 

```
resource "ibm_iam_service_id" "serviceID" {
  name = "test"
}

data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_service_policy" "policy" {
  iam_service_id = ibm_iam_service_id.serviceID.id
  roles        = ["Administrator"]

  resources {
    resource_type = "resource-group"
    resource      = data.ibm_resource_group.group.id
  }
}

```

#### Service Policy by using attributes 

```
resource "ibm_iam_service_id" "serviceID" {
  name = "test"
}

data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_service_policy" "policy" {
  iam_service_id = ibm_iam_service_id.serviceID.id
  roles        = ["Administrator"]

  resources {
    service = "is"

    attributes {
      "vpcId" = "*"
    }
    
  }
}

```

### Input parameters
{: #iam-service-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`iam_service_id`|String|Required|The UUID of the service ID.| Yes |
|`roles`|List|Required|A comma separated list of roles. Valid roles are `Writer`, `Reader`, `Manager`, `Administrator`, `Operator`, `Viewer`, and `Editor`.| No |
|`resources`|List of objects|Optional| A nested block describes the resource of this policy.| No |
|`resources.service` |String|Optional|The service name of the policy definition. You can retrieve the value by running the `ibmcloud catalog service-marketplace` or `ibmcloud catalog search`.| No |
|`resources.resource_instance_id`|String|Optional| The ID of the resource instance of the policy definition.| No |
|`resources.region` |String|Optional|The region of the policy definition.| No |
|`resources.resource_type`|String|Optional| The resource type of the policy definition.| No |
|`resources.resource`|String|Optional|The resource of the policy definition.| No |
|`resources.resource_group_id`|String|Optional| The ID of the resource group. To retrieve the value, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. | No |
|`resources.attributes`|Map|Optional| A set of resource attributes in the format `name=value,name=value`. If you set this option, do not specify `account_management` at the same time.| No |
|`account_management`|Boolean|Optional|Gives access to all account management services if set to `true`. Default value `false`. If you set this option, do not set `resources` at the same time. | No |
|`tags` |Array of strings|Optional| A list of tags that are associated with the service policy instance.  Tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |

### Output parameters
{: #iam-service-policy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id` |String|The unique identifier of the service policy. The ID is composed of `<iam_service_id>/<service_policy_id>`.|
|`version` |String|The version of the service policy.|

### Import
{: #iam-service-policy-import}

The service policy can be imported by using the service ID and service policy ID.

```
$ terraform import ibm_iam_service_policy.example <service_ID>/<service_policy_ID>
```






## `ibm_iam_user_policy`
{: #iam-user-policy}

Create, update, or delete an IAM user policy. To assign a policy to one user, the user must exist in the account to which you assign the policy. 

### Sample Terraform code
{: #iam-user-policy-sample}

#### User Policy for All Identity and Access enabled services 

```
resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@in.ibm.com"
  roles  = ["Viewer"]
}

```

#### User Policy by using service with region

```
resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@in.ibm.com"
  roles  = ["Viewer"]

  resources {
    service = "kms"
  }
}

```
#### User Policy by using resource instance 

```
resource "ibm_resource_instance" "instance" {
  name     = "test"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}

resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@in.ibm.com"
  roles  = ["Manager", "Viewer", "Administrator"]

  resources {
    service              = "kms"
    resource_instance_id = element(split(":",ibm_resource_instance.instance.id),7)
  }
}

```

#### User Policy by using resource group 

```
data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@in.ibm.com"
  roles  = ["Viewer"]

  resources {
    service           = "containers-kubernetes"
    resource_group_id = data.ibm_resource_group.group.id
  }
}

```

#### User Policy using resource and resource type

```
data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@in.ibm.com"
  roles  = ["Administrator"]

  resources {
    resource_type = "resource-group"
    resource      = data.ibm_resource_group.group.id
  }
}

```

#### User Policy by using attributes 

```
data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_user_policy" "policy" {
  ibm_id = "test@in.ibm.com"
  roles  = ["Administrator"]

  resources {
    service = "is"

    attributes {
      "vpcId" = "*"
    }
    
  }
}

```


### Input parameters
{: #iam-user-policy-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| --------- |
|`ibm_id`|String|Required| The IBMid or email address of the user.| Yes |
|`roles`|List|Required| A comma separated list of roles. Valid roles are `Writer`, `Reader`, `Manager`, `Administrator`, `Operator`, `Viewer`, and `Editor`.| No |
|`resources`|List of objects|Optional| A nested block describes the resource of this policy.| No |
|`resources.service` |String|Optional|The service name of the policy definition. You can retrieve the value by running the `ibmcloud catalog service-marketplace` or `ibmcloud catalog search`.| No |
|`resources.resource_instance_id`|String|Optional| The ID of the resource instance of the policy definition.| No |
|`resources.region` |String|Optional|The region of the policy definition.| No |
|`resources.resource_type`|String|Optional| The resource type of the policy definition.| No |
|`resources.resource`|String|Optional|The resource of the policy definition.| No |
|`resources.resource_group_id`|String|Optional| The ID of the resource group. To retrieve the value, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. | No |
|`resources.attributes`|Map|Optional| A set of resource attributes in the format `name=value,name=value`. If you set this option, do not specify `account_management` at the same time.| No |
|`account_management`|Boolean|Optional|Gives access to all account management services if set to `true`. Default value `false`. If you set this option, do not set `resources` at the same time. | No |
|`tags` |Array of strings|Optional| A list of tags that are associated with the service policy instance.  Tags are managed locally and not stored on the IBM Cloud Service Endpoint at this moment.| No |


### Output parameters
{: #iam-user-policy-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id` |String|The unique identifier of the user policy. The ID is composed of `<ibm_id>/<user_policy_id>`.|
|`version` |String|The version of the user policy.|


### Import
{: #iam-user-policy-import}

The user policy can be imported by using the IBMid and user policy ID.

```
$ terraform import ibm_iam_user_policy.example <ibm_id>/<user_policy_ID>
```





## `ibm_iam_user_settings`
{: #iam-user-settings}

Retrieve information about an IAM user settings. The IP addresses configured here are the only details a user can use to log in to the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

### Sample Terraform code
{: #iam-users-sample}

```
  resource "ibm_iam_user_settings" "user_setting" {
  iam_id = "example@in.ibm.com"
  allowed_ip_addresses = ["192.168.0.2","192.168.0.3","192.168.0.4"]
}

```

### Input parameters
{: #iam-user-settings-input}

The following attributes are supported:

|Name|Data type|Required / Optional|Description|
|----|-----------|-------------| ------------|
|`iam_id`|String|Required|The users IAM or email ID.|
|`allowed_ip_addresses`|List|Optional|Lists the IP addresses in common separated format.|

### Output parameters
{: #iam-user-settings-output}

The following attributes are exported:

|Name|Data type|Description|
|----|-----------|-------------|
|`id`|String|The unique identifier of the IAM user setting as `account_id`/`iam_id`.|






## `ibm_iam_user_invite`
{: #iam-user-invite}

Invite, update, or delete IAM users to your IBM Cloud account. User to be invited can be added to one or more access groups. For more information, see [inviting users](/docs/account?topic=account-access-getstarted).
{: shortdesc}

### Sample Terraform code
{: #iam-user-invite-sample}

#### Inviting batch of users

```
resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
}
```

#### Inviting batch of users with access groups

```
resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    access_groups = ["accessgroup-id-9876543210"]
}
```

#### Inviting batch of Users with Classic Infrastructure permissions

```
resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    classic_infra_roles {
      permissions = ["PORT_CONTROL", "DATACENTER_ACCESS"]
    }
}
```

#### Inviting batch of users with Classic Infrastructure permission set

```
resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    classic_infra_roles {
      permission_set = "superuser"
    }
}
```

#### Inviting batch of users with user policy for All Identity and Access enabled services

```
resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    iam_policy {
      roles  = ["Viewer"]
    }
}
```

#### Inviting batch of users with user policy by using service with region

```
resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    iam_policy {
      roles  = ["Viewer"]
      resources {
        service = "kms"
      }
    }
}
```

#### Inviting batch of users with user policy by using resource instance

```
resource "ibm_resource_instance" "instance" {
  name     = "test"
  service  = "kms"
  plan     = "tiered-pricing"
  location = "us-south"
}

resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    iam_policy {
      roles  = ["Manager", "Viewer", "Administrator"]
      resources {
        service              = "kms"
        resource_instance_id = element(split(":",ibm_resource_instance.instance.id),7)
      }
      }
}
```

#### Inviting batch of users with user policy by using resource group

```
data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    iam_policy {
      roles  = ["Manager", "Viewer", "Administrator"]
      resources {
        service           = "containers-kubernetes"
        resource_group_id = data.ibm_resource_group.group.id
      }
    }
}
```

#### Inviting batch of users with user policy by using resource and resource type

```
data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    iam_policy {
      roles  = ["Manager", "Viewer", "Administrator"]
      resources {
        resource_type = "resource-group"
        resource      = data.ibm_resource_group.group.id
      }
    }
}
```

#### Inviting batch of users with user policy by using attributes

```
data "ibm_resource_group" "group" {
  name = "default"
}

resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    iam_policy {
      roles  = ["Manager", "Viewer", "Administrator"]
      resources {
        service = "is"
        attributes {
          "vpcId" = "*"
        }
      }
    }
}
```

#### User invite with access cloud foundry roles

```
provider "ibm" {}

data "ibm_org" "org" {
  org = var.org
}

data "ibm_space" "space" {
  org   = var.org
  space = var.space
}

resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
    cloud_foundry_roles {
      organization_guid = data.ibm_org.org.id
      org_roles = ["Manager", "Auditor"]
      spaces {
          space_guid = data.ibm_space.space.id
          space_roles = ["Manager", "Developer"]
      }
    }
}
```

### Input parameters
{: #iam-user-invite-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`users`|List|Required|A comma separated list of user email IDs.|
|`access_groups`|List|Optional|A comma separated list of access group IDs.|
|`classic_infra_roles`|Map|Optional|A nested block describes the classic infrastructure roles for the inviting users. </br></br>**Note**: If you have an IBM Cloud Lite account, you cannot set classic infrastructure roles. For more information, about Lite accounts, see [What's available?](/docs/account?topic=account-accounts#lite-account-features).|
|`classic_infra_roles.permissions`|List|Optional|A comma separated list of classic infrastructure permissions.|
|`classic_infra_roles.permission_set`|String|Optional|The permission set to be applied. The valid permission sets are `noacess`, `viewonly`, `basicuser`, and `superuser`.|
|`iam_policy`|List|Optional|A nested block describes the IAM policies for invited users. |
|`iam_policy_roles`|List|Required|A comma separated list of roles. Valid roles are `Writer`, `Reader`, `Manager`, `Administrator`, `Operator`, `Viewer`, and `Editor`.|
|`iam_policy.resources`|List of objects|Optional| A nested block describes the resource of this policy.|
|`iam_policy.resources.service` |String|Optional|The service name of the policy definition. You can retrieve the value by running the `ibmcloud catalog service-marketplace` or `ibmcloud catalog search`.|
|`iam_policy.resources.resource_instance_id`|String|Optional| The ID of the resource instance of the policy definition.|
|`iam_policy.resources.region` |String|Optional|The region of the policy definition.|
|`iam_policy.resources.resource_type`|String|Optional| The resource type of the policy definition.|
|`iam_policy.resources.resource`|String|Optional|The resource of the policy definition.|
|`iam_policy.resources.resource_group_id`|String|Optional| The ID of the resource group. To retrieve the value, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. |
|`iam_policy.resources.attributes`|Map|Optional| A set of resource attributes in the format `name=value,name=value`. If you set this option, do not specify `account_management` at the same time.|
|`iam_policy.account_management`|Boolean|Optional|Gives access to all account management services if set to `true`. Default value is `false`. If you set this option, do not set `resources` at the same time. |
|`cloud_foundry_roles`|List|Optional|A nested block describes the cloud foundry roles of inviting user. |
|`cloud_foundry_roles.organization_guid`|String|Required|The ID of the Cloud Foundry organization.|
|`cloud_foundry_roles.org_roles`|List|Required|The organization roles that are assigned to invited user. The supported roles are `Manager`, `Auditor`, `BillingManager`.|
|`cloud_foundry_roles.spaces`|List|Optional|A nested block describes the Cloud Foundry space roles and space details.|
|`cloud_foundry_roles.spaces.space_guid`|String|Required|The ID of the Cloud Foundry space.|
|`cloud_foundry_roles.spaces.space_roles`|List|Required|The space roles that you want to assign to the invited user. The supported space roles are `Manager`, `Developer`, `Auditor`.|

 {{site.data.keyword.cloud_notm}} `Lite account` does not support classic infrastructure roles. For more information, see [What's available in lite account?](/docs/account?topic=account-accounts#lite-account-features).
{: note}

### Output parameters
{: #iam-user-invite-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`number_of_invited_users`|String|Number of users invited to a particular account.|
|`invited_users`|String|List of invited users. Nested invited_users block have the following structure.|
|`invited_users.user_id`|String|The Email ID of the member.|
|`invited_users.user_policies`|String| List of policies associated to a particular user. Nested user_policies block has following structure.|
|`invited_users.user_policies.id`|String|The policy ID.|
|`invited_users.user_policies.roles`|String|Comma separated list of the roles.|
|`invited_users.user_policies.resources`|String| A nested block describes the resource of the policy. Nested resources block have the following structure.|
|`invited_users.user_policies.resources.service`|String| Service name of the policy definition.|
|`invited_users.user_policies.resources.resource_instance_id`|String| The resource instance ID of the policy definition.|
|`invited_users.user_policies.resources.region`|String|The region of the policy definition.|
|`invited_users.user_policies.resources.resource_type`|String|The resource type of the policy definition.|
|`invited_users.user_policies.resources.resource`|String|The resource of the policy definition.|
|`invited_users.user_policies.resources.resource_group_id`|String|The ID of the resource group.|
|`invited_users.user_policies.resources.attributes`|String|The set of resource attributes.|
|`access_groups`|String|The lock down ID.|
|`access_groups.name`|String|The name of the access group.|
|`access_groups.policies`|String|The access group policies of invited user. Nested policies block have the following structure.|
|`access_groups.policies.id`|String|The policy ID.|
|`access_groups.policies.roles`|String|The roles associated to the policy.|
|`access_groups.policies.resources`|String| A nested block describes the resource of the policy. Nested resources block have the following structure.|
|`access_groups.policies.resources.service`|String| Service name of the policy definition.|
|`access_groups.policies.resources.resource_instance_id`|String| The resource instance ID of the policy definition.|
|`access_groups.policies.resources.region`|String|The region of the policy definition.|
|`access_groups.policies.resources.resource_type`|String|The resource type of the policy definition.|
|`access_groups.policies.resources.resource`|String|The resource of the policy definition.|
|`access_groups.policies.resources.resource_group_id`|String|The ID of the resource group.|
|`access_groups.policies.resources.attributes`|String|The set of resource attributes.|

### Import
{: #iam-user-invite-import}

The import functionality is not supported for this resource.
