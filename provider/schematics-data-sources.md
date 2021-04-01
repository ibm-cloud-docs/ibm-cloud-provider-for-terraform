---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-01"

keywords: terraform provider plugin, terraform schematics data source, terraform schematics workspace 

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



# Schematics data sources
{: #schematics-data-sources}

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_schematics_workspace`
{: #schematics-workspace}

Retrieve information about a Schematics workspace. For more details about the Schematics and Schematics workspace, see [Setting up workspaces](docs/schematics?topic=schematics-getting-started).
{: shortdesc}

### Sample Terraform code
{: #schematics-workspace-sample}

The following example retrieves information about the `my-workspace-id` workspace.  
{: shortdesc}

```
data "ibm_schematics_workspace" "schematics_workspace" {
	workspace_id = "workspace_id"
}
```
{: codeblock}

### Input parameters
{: #schematics-workspace-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`workspace_id`|String|Required|The workspace ID that you want to retrieve. To find the workspace ID, use the `GET /v1/workspaces API`. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #schematics-workspace-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
| `id` | String | The unique ID of the Schematics workspace.|
| `applied_shareddata_ids` | String | List of applied shared dataset ID.|
|`catalog_ref`| String | Information about the software template that you select from the {{site.data.keyword.cloud_notm}} catalog. This information is returned for {{site.data.keyword.cloud_notm}} catalog offerings only. Nested `catalog_ref` blocks have the following structure:|
|`catalog_ref.dry_run`| Bool | Dry run. |
|`catalog_ref.item_icon_url`| String | Optional | The icon URL of the software template in the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.item_id`| String | The ID of the software template that you select to install from the {{site.data.keyword.cloud_notm}} catalog. This software is provisioned with {{site.data.keyword.bpshort}}.|
|`catalog_ref.item_name` | String | The name of the software that you select to install from the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.item_readme_url`| String | The URL to the readme file of the software template in the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.item_url` | String | The URL to the software template in the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.launch_url` | String | Optional | The dashboard URL to access the software.|
|`catalog_ref.offering_version` | String | The version of the software template that you select to install from the {{site.data.keyword.cloud_notm}} catalog.|
| `created_at` | Timestamp | The workspace created timestamp.|
| `created_by` | Timestamp | The user ID that created the workspace.|
| `crn` | String | The workspace CRN.|
|`description` | String | Optional |  The description of the workspace.|
| `id` | String | The unique ID of the workspace. |
| `last_health_check_at` | Timestamp | The timestamp when the last health check was performed by Schematics. |
|`location` | String | The {{site.data.keyword.cloud_notm}} location where your workspace was provisioned.|
|`name` | String | The name of your workspace.|
|`resource_group` | String | The ID of the resource group where you want to provision the workspace.|
|`runtime_data` | String | Information about provisioning engine, state file, and runtime logs. Nested runtime_data blocks have the following structure.|
|`runtime_data.engine_cmd`| String |The command used to apply the Terraform template or {{site.data.keyword.cloud_notm}} catalog software template.|
|`runtime_data.engine_name`| String | The provisioning engine used to apply the Terraform template or {{site.data.keyword.cloud_notm}} catalog software template.|
|`runtime_data.engine_version`| String |The version of the provisioning engine.|
|`runtime_data.id`| String |The ID that was assigned to your Terraform template or {{site.data.keyword.cloud_notm}} catalog software template.|
|`runtime_data.log_store_url`| String | The URL to access the logs created during the creation, update, or deletion of your {{site.data.keyword.cloud_notm}} resources.|
|`runtime_data.output_values`| String | The list of output values.|
|`runtime_data.resources`| String | The list of resources.|
|`runtime_data.state_store_url`| String | The URL where the Terraform statefile `terraform.tfstate` is stored. You can use the statefile to find an overview of {{site.data.keyword.cloud_notm}}  resources created by Schematics. Schematics uses the statefile as an inventory list to determine future create, update, or deletion actions.|
|`shared_data` | String | Information that is shared across templates in {{site.data.keyword.cloud_notm}} catalog offerings. This information is not provided when you create a workspace from your own Terraform template. Nested `shared_data` blocks have the following structure.|
|`shared_data.cluster_id` | String | The ID of the cluster where you want to provision the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering.|
|`shared_data.cluster_name` | String |  The target cluster name.|
|`shared_data.entitlement_keys` | `String` | The entitlement key that you want to use to install {{site.data.keyword.cloud_notm}} entitled software.|
|`shared_data.namespace` | String |  The {site.data.keyword.containershort}} namespace or {{site.data.keyword.openshiftshort}} project where the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering are deployed into.|
|`shared_data.region` | String |  The {{site.data.keyword.cloud_notm}} region that you want to use for the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering.|
|`shared_data.resource_group_id` | String |  The ID of the resource group that you want to use for the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering.|
|`status` | String | The status of the workspace. For more information, about the Schematics workspace status, see [workspace states](/docs/schematics?topic=schematics-workspace-setup#wks-state).|
|`tags`| List | A list of tags that are associated with the workspace. |
|`template_data`| List |  Information about the Terraform or {{site.data.keyword.cloud_notm}} software template to use. Nested `template_data` blocks have the following structure:|
|`template_data.env_values`| String | List of environment values. Nested `env_values` blocks have the following structure:|
|`template_data.env_values.hidden`| String | The environment variable is hidden.|
|`template_data.env_values.name`| String | The environment variable name.|
|`template_data.env_values.secure`| String | The environment variable is secure.|
|`template_data.env_values.value`| String |  Value for an environment variable.|
|`template_data.folder` | String |  The subfolder in your GitHub or GitLab repository where your Terraform template is stored.|
|`template_data.has_githubtoken` | String | Has GitHub token. |
|`template_data.id` | String | The ID assigned to your Terraform template or {{site.data.keyword.cloud_notm}} catalog software template.|
|`template_data.template_type` | String | The Terraform version used to run your Terraform code. |
|`template_data.uninstall_script_name` | String | The script name to uninstall. |
|`template_data.values` | String | A list of variable values that you want to apply during the Helm chart installation. The list must be provided in JSON format, such as `autoscaling: enabled: true minReplicas: 2`. The values that you define here overrides the default Helm chart values. This field is supported only for {{site.data.keyword.cloud_notm}} catalog offerings that are provisioned by using the Terraform Helm provider.|
|`template_data.values_metadata` | String | A list of input variables that are associated with the workspace.|
|`template_data.values_url` | String | The API endpoint to access the input variables that you defined for your template.|
|`template_data.variablestore` | String | Information about the input variables that your template uses. Nested variablestore blocks have the following structure. |
|`template_data.variablestore.description` | String | The description of your input variable.|
|`template_data.variablestore.name` | String | The name of your variable.|
|`template_data.variablestore.secure` | String | If set to `true`, the value of your input variable is protected and not returned in your API response.|
|`template_data.variablestore.type` | String | Terraform v0.11 supports string, list, map data type. For more information, about the syntax, see [Configuring input variables]((/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-new).
Terraform v0.12 additionally, supports bool, number and complex data types such as list(type), map(type), object({attribute name=type,..}), set(type), tuple([type]). For more information, about the syntax to use the complex data type, see [Configuring variables](/docs/schematics?topic=schematics-create-tf-config#configure-variables).|
|`template_data.variablestore.value` | String |  Enter the value as a string for the primitive types such as bool, number, string, and HCL format for the complex variables, as you provide in a `.tfvars` file. You need to enter escaped string of HCL format for the complex variable value. For more information, about how to declare variables in a terraform configuration file and provide value to schematics, see [Providing values for the declared variables](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-new).|
|`template_ref` | String |  The workspace template reference.|
|`template_repo` | List | The input parameter to specify the source repository where your {{site.data.keyword.bpshort}} template is stored.|
|`template_repo.branch` | String |  The branch in GitHub where your Terraform template is stored.|
|`template_repo.full_url` | String |  The full URL repository.|
|`template_repo.has_uploadedgitrepotar` | String |  Has uploaded Git repository tar.|
|`template_repo.release` | String |  The release tag in GitHub of your Terraform template.|
|`template_repo.repo_sha_value` | String | The SHA value from the repository.|
|`template_repo.repo_url` | String | The URL to the repository where the {{site.data.keyword.cloud_notm}} catalog software template is stored.|
|`template_repo.url` | String |   The GitHub or GitLab repository URL where your Terraform template is stored.|
|`type`| List | The Terraform version that you want to use to run your Terraform code. |
|`updated_at`| Timestamp | The timestamp when the workspace updated. |
|`updated_by`| Timestamp | The user ID of the workspace updated. |
|`workspace_status`| List |  Response parameter that indicate if a workspace is frozen or locked. Nested `workspace_status` blocks have the following structure.|
|`workspace_status.frozen`| Bool | Optional | If set to `true`, the workspace is frozen and changes to the workspace are disabled.|
|`workspace_status.frozen_at` | String | The timestamp when the workspace was frozen.|
|`workspace_status.frozen_by` | String |  The user ID that froze the workspace.|
|`workspace_status.locked` | Bool |   If set to `true`, the workspace is locked and disabled for changes.|
|`workspace_status.locked_by` | Timestamp | The workspace locked for the user who initiates a resource-related action, such as applying or destroying resources.|
|`workspace_status.locked_time` | Timestamp |  The timestamp when the workspace is locked.|
|`workspace_status_msg`| String |Information about the last action that ran against the workspace. Nested `workspace_status_msg` blocks have the following structure.|
|`workspace_status_msg.status_code`| String | The success or error code that was returned for the last plan, apply, or destroy action that ran against your workspace. |
|`status_msg`| String | The success or error message returned for the last plan, apply, or destroy action of your workspace.|
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

data "ibm_schematics_output" "schematics_output" {
	workspace_id = "workspace_id"
  template_id = "template_id"
}
```
{: codeblock}

### Input parameters
{: #schematics-output-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`workspace_id`|String|Required|The ID of the workspace for which you want to retrieve output values. To find the workspace ID, use the `GET /workspaces` API. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #schematics-output-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
|`id`| String | The unique identifier of the Schematics output.|
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
data "ibm_schematics_state" "schematics_state" {
	workspace_id = "workspace_id"
	template_id = "template_id"
}
```
{: codeblock}

### Input parameters
{: #schematics-state-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
|`workspace_id`|String|Required| The workspace ID for which you want to retrieve the Terraform statefile. To find the workspace ID, use the `GET /v1/workspaces` API. |
|`template_id`|String|Required|The ID of the Terraform template for which you want to retrieve the Terraform statefile. When you create a workspace, the Terraform template that your workspace points to is assigned a unique ID. To find this ID, use the `GET /v1/workspaces` API and review the `template_data.id` value. |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #schematics-state-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
| `id` | String | The unique ID of the Schematics state.|
| `version`| String | The Schematics version. |
| `terraform_version`| String | The Terraform version. |
| `serial` | String | The state store serial number details. |
| `lineage`| Integer | The state store lineage number details. |
| `modules`| String | The state store module details.|
{: caption="Table 1. Available output parameters" caption-side="top"}
