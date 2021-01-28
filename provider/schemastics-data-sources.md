---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider plugin, terraform schematics data source, terraform schematics workspace 

subcollection: ibm-cloud-provider-for-terraform

---

{[METADATA_ATTRIBUTES]}


# Schematics data sources
{: #schematics-data-sources}

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_schematics_workspace`
{: #schematics-workspace}

Retrieve information about a Schematics workspace. 
{: shortdesc}

### Sample Terraform code
{: #schematics-workspace-sample}

The following example retrieves information about the `my-workspace-id` workspace.  
{: shortdesc}

```
data "ibm_schematics_workspace" "test" {
  workspace_id = "my-workspace-id"
}
```

### Input parameters
{: #schematics-workspace-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`workspace_id`|String|Required|The ID of the Schematics workspace. You can retrieve this information by running `ibmcloud terraform workspace list`. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #schematics-workspace-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
| `name`|String| The name of the workspace.|
|`types`|String|The supported types of the Terraform version. |
|`status`|String| The status of the workspace.|
|`is_frozen`|Boolean|If set to **true**, the workspace is frozen and disabled for changes. If set to **false**, the workspace is unfrozen and updates can be made to the workspace.|
| `is_locked`|Boolean|If set to **true**, the workspace is locked and disabled for changes. If set to **false**, the workspace is unlocked and updates can be made to the workspace.|
|`template_id` |Array|The ID of the templates that are present in the workspace.|
|`tags`|Array|The tags that were added to the workspace.|
|`resource_group`|String|The resource group associated with the workspace.|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_schematics_output`
{: #schematics-output}

Retrieve state information for a Schematics workspace. For detailed information about how to use this data source, see [Accessing Terraform state information across workspaces](/docs/schematics?topic=schematics-remote-state). 
{: shortdesc}

### Sample Terraform code
{: #schematics-output-sample}

The following example retrieves information about the `my-workspace-id` workspace.  
{: shortdesc}

```
data "ibm_schematics_workspace" "vpc" {
  workspace_id = "<schematics_workspace_id>"
}

data "ibm_schematics_output" "test" {
  workspace_id = "<schematics_workspace_id>"
  template_id= data.ibm_schematics_workspace.vpc.template_id.0
}
```

### Input parameters
{: #schematics-output-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`workspace_id`|String|Required|The ID of the Schematics workspace. You can retrieve this information by running `ibmcloud terraform workspace list`. |
|`template_id`|String|Required|The ID of the template that the workspace uses. This value must be retrieved from the `ibm_schematics_workspace` data source and set to `data.ibm_schematics_workspace.vpc.template_id.0`. |
{: caption="Table. Available input parameters" caption-side="top"}


### Output parameters
{: #schematics-output-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`output_values`|Map|A list of Terraform output values that were exported for the workspace. All map entries are listed as key-value pairs.|
|`output_json`|String|The output values of a Schematics workspace in JSON format. |
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_schematics_state`
{: #schematics-state}

Retrieve information about the Terraform state file for a Schematics workspace.
{: shortdesc}

### Sample Terraform code
{: #schematics-state-sample}

The following example retrieves information about the `my-workspace-id` workspace.  
{: shortdesc}

```
data "ibm_schematics_state" "test" {
  workspace_id = "my-worspace-id"
  template_id= "my-template-id"
}
```

### Input parameters
{: #schematics-state-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`workspace_id`|String|Required|The ID of the Schematics workspace. You can retrieve this information by running `ibmcloud terraform workspace list`. |
|`template_id`|String|Required|The of the template that the workspace uses. |
{: caption="Table. Available input parameters" caption-side="top"}


### Output parameters
{: #schematics-state-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`state_store`|String|The URL to the location where the Terraform state file is stored. |
|`state_store_json`|String|The JSON representation of the Terraform state file.
{: caption="Table 1. Available output parameters" caption-side="top"}
