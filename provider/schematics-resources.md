---

copyright:
  years: 2017, 2021
lastupdated: "2021-07-19"

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
{:terraform: .ph data-hd-interface='terraform'}
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



# Schematics resources
{: #schematics-resources}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

## `ibm_schematics_action`
{: #schematics-action}

Create, update, and delete `ibm_schematics_action`. For more information, about {{site.data.keyword.bplong_notm}} action, refer to [setting up actions](/docs/schematics?topic=schematics-action-setup).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #action-sample}

```
resource "ibm_schematics_action" "schematics_action" {
  name = "<action_name>"
  description = "<action_description>"
  location = "us-east"
  resource_group = "default"
}
```
{: codeblock}

### Input parameters
{: #action-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`| String| Optional | The unique name of an action.|
|`description`| String| Optional | The description of an action.|
|`location`| String| Optional | List of action locations supported by {{site.data.keyword.bplong_notm}} service. **Note** this does not limit the location of the resources provisioned using Schematics.|
|`resource_group`| String | Optional | Resource-group name for an action. By default, action is created in default resource group.|
|`tags`| List | Optional | An actions tags.|
|`user_state`| List | Optional | User defined status of the {{site.data.keyword.bpshort}} object.|
|`user_state.state`| String | Optional | User defined states * **draft Object** can be modified, and can be used by jobs run by an author, during execution * **live Object** can be modified, and can be used by jobs during execution * **locked Object** cannot be modified, and can be used by jobs during execution * disable Object can be modified, and cannot be used by Jobs during execution.|
|`user_state.set_by`| String | Optional | Name of the user who set the state of an Object.|
|`user_state.set_at`| `TypeString` | Optional | When the user who set the state of an Object.|
|`source_readme_url`| String | Optional | The URL of the `README` file, for the source.|
|`source`| List | Optional | Source of templates, playbooks, or controls.|
|`source.source_type`| String | Required | Type of source for the Template.|
|`source.git`| `ExternalSourceGit` | Optional | Connection details to Git source.|
|`source_type`| String | Optional | Type of source for the Template.|
|`command_parameter`| String | Optional | {{site.data.keyword.bpshort}} job command parameter such as `playbook-name`, `capsule-name` or `flow-name`.|
|`bastion`| List | Optional | Complete target details with the user inputs and the system generated data.|
|`bastion.name`| String | Optional | The target name.|
|`bastion.type`| String | Optional | The target type  such as `cluster`, `vsi`, `icd`, `vpc`.|
|`bastion.description`| String | Optional | Target description.|
|`bastion.resource_query`| String | Optional | Resource selection query string.|
|`bastion.credential` | String | Optional | Override credential for each resource. Reference to credentials values, used by all the resources.|
|`bastion.id`| String | Optional | The Target ID.|
|`bastion.created_at`| `TypeString` | Optional | The targets creation time.|
|`bastion.created_by`| String | Optional | The Email address of an user who created the targets.|
|`bastion.updated_at`| `TypeString` | Optional | The targets update time.|
|`bastion.updated_by`| String | Optional | The Email address of an user who updated the targets.|
|`bastion.sys_lock`| `SystemLock` | Optional | The System lock status.|
|`bastion.resource_ids`| `[]interface{}` | Optional | Array of the resource IDs.|
|`targets_ini`| String | Optional | Inventory of host and host group for the playbook in `INI` file format. For example, `targets_ini` such as `"[webserverhost] 172.22.192.6 [dbhost] 172.22.192.5"`. For more information, about an inventory host group syntax, see [Inventory host groups](/docs/schematics?topic=schematics-schematics-cli-reference#inventory-host-grps).|
|`credentials`| List | Optional | credentials of an action.|
|`credentials.name`| String | Optional | Name of the variable.|
|`credentials.value`| String | Optional | Value for the variable or reference to the value.|
|`credentials.metadata`| `VariableMetadata` | Optional | User editable metadata for the variables.|
|`credentials.link`| String | Optional | The reference link to the variable value. By default the expression will point to `self.value`.|
|`inputs`| List | Optional | The input variables for an action.|
|`inputs.name`| String | Optional | The name of the variable.|
|`inputs.value`| String | Optional | Value for the variable or reference to the value.|
|`inputs.metadata`| `VariableMetadata` | Optional | User editable metadata for the variables.|
|`inputs.link`| String | Optional | The reference link to the variable value. By default the expression will point to `self.value`.|
|`outputs`| List | Optional | The output variables for an action.|
|`outputs.name`| String | Optional | The name of the variable.|
|`outputs.value`| String |Optional | The value for the variable or reference to the value.|
|`outputs.metadata`| `VariableMetadata` | Optional | The user editable metadata for the variables.|
|`outputs.link`| String | Optional | The reference link to the variable value By default the expression will point to `self.value`.|
|`settings`| List | Optional | The environment variables for an action.|
|`settings_name`| String | Optional | The name of the variable.|
|`settings_value`| String | Optional | The value for the variable or reference to the value.|
|`settings_metadata`| `VariableMetadata` | Optional | User editable metadata for the variables.|
|`settings_link`| String | Optional | The reference link to the variable value. By default the expression will point to `self.value`.|
|`trigger_record_id`| String | Optional | The ID to the trigger.|
|`state`| List | Optional | Computed state of an action.|
|`state.status_code`| String | Optional | Status of automation  such as `workspace`, or `action`.|
|`state.status_message`| String | Optional | The automation status message to display along with the `status_code`.|
|`sys_lock`| List | Optional | The system lock status.|
|`sys_lock.sys_locked`| Bool | Optional | Is the Workspace locked by the Schematic action?|
|`sys_lock.sys_locked_by`| String | Optional | The name of the user who performed an action, that lead to lock the Workspace.|
|`sys_lock.sys_locked_at`| `TypeString` | Optional | When the user performed the action that lead to lock the Workspace?|
|`x_github_token`| String | Optional | The personal access token to authenticate with your private GitHub or GitLab repository and access your Terraform template.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #action-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the {{site.data.keyword.bpshort}} workspace.|
|`crn`|String| An action Cloud Resource Name (`CRN`).|
|`account`|String|An action account ID.|
|`source_created_at`|String| An Ansible playbook source creation time.|
|`source_created_by`|String| An Email address of the user who created an Ansible playbook source.|
|`source_updated_at`|String|The action playbook update time.|
|`source_updated_by`|String|An Email address of the user who updated the action playbook source.|
|`created_at`|String| An action creation time.|
|`created_by`|String|An Email address of the user who created an action.|
|`updated_at`|String|An action update time.|
|`updated_by`|String|An Email address of the user who updated an action.|
|`namespace`|String| The name of the namespace.|
|`playbook_names`|String|The playbook names retrieved from the repository.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_schematics_job`
{: #schematics-job}

Create, update, and delete `ibm_schematics_job`. For more information, about {{site.data.keyword.bpfull}} job, refer to [setting up jobs](/docs/schematics?topic=schematics-action-setup#action-jobs).
{: shortdesc}


### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #job-sample}

```
resource "ibm_schematics_job" "schematics_job" {
  command_object = "action"
  command_object_id = "<action_id>"
  command_name = "ansible_playbook_run | ansible_playbook_check"
  command_parameter = "<yml_file_name>"
  location = "us-east"
}
```
{: codeblock}

### Input parameters
{: #job-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`command_object`| String | Optional | The name of the {{site.data.keyword.bpshort}} automation resource.|
|`command_object_id`| String | Optional | The job command object ID. Supported values are `workspace-id`, `action-id`, or `control-id`.|
|`command_name`| String | Optional | The {{site.data.keyword.bpshort}} job command name.|
|`command_parameter`| String | Optional | The {{site.data.keyword.bpshort}} job command parameter. Supported values are  `playbook-name`, `capsule-name`, or `flow-name`.|
|`command_options`| List | Optional | The command line options for the command.|
|`inputs`| List | Optional | The job inputs used by an action.|
|`inputs.name`| String | Optional | The name of the variable.|
|`inputs.value`| String | Optional | The value for the variable or reference to the value.|
|`inputs.metadata`| `VariableMetadata` | Optional | User editable metadata for the variables.|
|`inputs.link`| String | Optional | The reference link to the variable value By default the expression will point to self.value.|
|`settings`| List | Optional | Environment variables used by the job while performing an action.|
|`settings.name`| String | Optional | Name of the variable.|
|`settings.value`| String | Optional | Value for the variable or reference to the value.|
|`settings.metadata`| `VariableMetadata` | Optional | User editable metadata for the variables.|
|`settings.link`| String | Optional | Reference link to the variable value. By default the expression will point to `self.value`.|
|`tags`| List | Optional | User defined tags, while running the job.|
|`location`| String | Optional | List of action locations supported by {{site.data.keyword.bpshort}} service. **Note** this does not limit the location of the resources provisioned by using {{site.data.keyword.bpshort}}.|
|`status`| List | Optional | The job status.|
|`status.action_job_status`| String | Optional | The action job status.|
|`data`| List | Optional | The job data.|
|`data.job_type`| String | Required | Type of the job.|
|`data.action_job_data`| String | Optional | Action Job data.|
|`bastion`| List | Optional | Complete target details with the user inputs and the system generated data.|
|`bastion.name`| String | Optional | The target name.|
|`bastion.type`| String | Optional | The target type such as `cluster`, `vsi`, `icd`, `vpc`.|
|`bastion.description`| String | Optional | The target description.|
|`bastion.resource_query`| String | Optional | The resource selection query string.|
|`bastion.credential`| String | Optional | Override the credential for each resource. Reference to credentials values, used by all the resources.|
|`bastion.id`| String | Optional | The target ID.|
|`bastion.created_at`| `TypeString` | Optional | The targets creation time.|
|`bastion.created_by`| String | Optional | The Email address of the user who created the targets.|
|`bastion.updated_at`| `TypeString` | Optional | The targets update time.|
|`bastion.updated_by`| String | Optional | The Email address of user who updated the targets.|
|`bastion.sys_lock`| `SystemLock` | Optional | The system lock status.|
|`bastion.resource_ids`| `[]interface{}` | Optional | An array of the resource IDs.|
|`log_summary`| List | Optional | The job log summary record.|
|`log_summary.job_id`| String | Optional | The workspace ID.|
|`log_summary.job_type`| String | Optional | The type of Job.|
|`log_summary.log_start_at`| `TypeString` | Optional | The job log start timestamp.|
|`log_summary.log_analyzed_till`| `TypeString` | Optional | The job log update timestamp.|
|`log_summary.elapsed_time`| float64 | Optional | The job log elapsed time `log_analyzed_till`, `log_start_at`.|
|`log_summary.log_errors`| `[]interface{}` | Optional | The job log errors.|
|`log_summary.repo_download_job`| String| Optional | The repository download job log summary.|
|`log_summary.action_job`| String | Optional | The job log summary flow.|
|`x_github_token`| String | Optional | Create a job record and launch the job.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #job-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the {{site.data.keyword.bpshort}} job.|
|`name`|String|The job name, uniquely derived from the related action.|
|`description`|String| The job description derived from the related action.|
|`resource_group`|String| The resource group name derived from the related action.|
|`submitted_at`|String| The job submission time.|
|`submitted_by`|String|The Email address of the user who submitted the job.|
|`start_at`|String| The job start time.|
|`end_at`|String|The job end time.|
|`duration`|String| The duration of the job execution, for example, `40 seconds`.|
|`targets_ini`|String|An inventory of host and host group for the playbook in `INI` file format. For example, `"targets_ini": "[webserverhost] 172.22.192.6 [dbhost] 172.22.192.5"`. For more information, about an inventory host group syntax, see [Inventory host groups](/docs/schematics?topic=schematics-schematics-cli-reference#inventory-host-grps).|
|`log_store_url`|String|The job log store URL.|
|`state_store_url`|String|The job state store URL.|
|`results_url`|String| The job results store URL.|
|`updated_at`|String| The job status update timestamp.|
{: caption="Table 1. Available output parameters" caption-side="top"}

## `ibm_schematics_workspace`
{: #schematics-wks}

Create, update, and delete `ibm_schematics_workspace`. For more information, about {{site.data.keyword.bpfull}} workspace, refer to [setting up workspaces](/docs/schematics?topic=schematics-workspace-setup).
{: shortdesc}

You can use `ibm_schematics_workspace` resource to perform create, read, update, and delete operations of {{site.data.keyword.bpshort}} workspace. Other {{site.data.keyword.bpshort}} operations such as plan, apply, destroy that are available through {{site.data.keyword.bplong_notm}} user interface are currently not supported.
{: note}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #wks-sample}

```
resource "ibm_schematics_workspace" "schematics_workspace" {
  name = "<workspace_name>"
  description = "<workspace_description>"
  location = "us-east"
  resource_group = "default"
  template_type = "terraform_v0.13.5"
}

```
{: codeblock}

### Input parameters
{: #wks-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`applied_shareddata_ids`| List | Optional | List of applied shared data set ID.|
|`catalog_ref`| List | Optional | The software template that you select from the {{site.data.keyword.cloud}} catalog and returned for {{site.data.keyword.cloud_notm}} catalog offerings only.|
|`catalog_ref.dry_run`| Bool | Optional | Dry run. |
|`catalog_ref.item_icon_url`| String | Optional | The icon URL of the software template in the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.item_id`| String | Optional | The ID of the software template that you select to install from the {{site.data.keyword.cloud_notm}} catalog. This software is provisioned with {{site.data.keyword.bpshort}}.|
|`catalog_ref.item_name` | String | Optional | The name of the software that you select to install from the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.item_readme_url`| String | Optional | The URL to the readme file of the software template in the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.item_url` | String | Optional | The URL to the software template in the {{site.data.keyword.cloud_notm}} catalog.|
|`catalog_ref.launch_url` | String | Optional | The dashboard URL to access the software.|
|`catalog_ref.offering_version` | String | Optional |  The version of the software template that you select to install from the {{site.data.keyword.cloud_notm}} catalog.|
|`description` | String | Optional |  The description of the workspace.|
|`location` | String | Optional |  The location where you want to create your {{site.data.keyword.bpshort}} workspace and run {{site.data.keyword.bpshort}} actions. The location that you enter should match the API endpoint that you use. For example, if you use the `Frankfurt API endpoint`, you should specify `eu-de` as your location. If you use an API endpoint for a geography and you do not specify a location, {{site.data.keyword.bpshort}} determines the location based on availability.|
|`name` | String | Optional | The name of your workspace. The name can be up to **128** characters long and can include alphanumeric characters, spaces, dashes, and underscores. When you create a workspace for your own Terraform template, consider including the microservice component that you set up with your Terraform template and the {{site.data.keyword.cloud_notm}} environment where you want to deploy your resources in your name.|
|`resource_group` | String | Optional |  The ID of the resource group where you want to provision the workspace.|
|`shared_data` | String | Optional |  Information that is shared across templates in {{site.data.keyword.cloud_notm}} catalog offerings. This information is not provided when you create a workspace from your own Terraform template.|
|`shared_data.cluster_created_on` | String | Optional |  The cluster created on.|
|`shared_data.cluster_id` | String | Optional |  The ID of the cluster where you want to provision the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering.|
|`shared_data.cluster_name` | String | Optional |  The cluster name.|
|`shared_data.cluster_type` | String | Optional |  The cluster type.|
|`shared_data.entitlement_keys` | `[]interface{}]` | Optional | The entitlement key that you want to use to install {{site.data.keyword.cloud_notm}} entitled software.|
|`shared_data.namespace` | String | Optional |  The Kubernetes namespace or OpenShift project where the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering are deployed into.|
|`shared_data.region` | String | Optional |   The IBM Cloud region that you want to use for the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering.|
|`shared_data.resource_group_id` | String | Optional |   The ID of the resource group that you want to use for the resources of all {{site.data.keyword.cloud_notm}} catalog templates that are included in the catalog offering.|
|`shared_data.worker_count` | Integer | Optional |   Cluster worker count.|
|`shared_data.worker_machine_type` | String | Optional |  Cluster worker type.|
|`tags`| List | Optional | A list of tags that are associated with the workspace. |
|`template_data`| List | Optional | List of template data.|
|`template_data.env_values`| `[]interface{}]` | Optional | A list of environment variables that you want to apply during the execution of a bash script or Terraform action. This field contains the list of key-value pairs, for example, `TF_LOG=debug`. Each entry is map with one entry where key is the environment variable name and value is value. You can define environment variables for {{site.data.keyword.cloud_notm}} catalog offerings that are provisioned by using a bash script.|
|`template_data.folder` | String | Optional |  The subfolder in your GitHub or GitLab repository where your Terraform template is stored.|
|`template_data.init_state_file` | String | Optional |  The content of an existing Terraform statefile that you want to import to your workspace. To get the content of a Terraform statefile for a specific Terraform template in an existing workspace, run `ibmcloud terraform state pull --id <workspace_id> --template <template_id>`.|
|`template_data.type` | String | Optional |  The Terraform version that you want to run your Terraform code. Enter `terraform_v0.12` to use Terraform version 0.12. Make sure that your Terraform configuration files are compatible with the Terraform version that you select.|
|`template_data.uninstall_script_name` | String | Optional | The script name to uninstall. |
|`template_data.values` | String | Optional |  A list of variable values that you want to apply during the Helm chart installation. The list must be provided in JSON format, such as `autoscaling: enabled: true minReplicas: 2`. The values that you define here overrides the default Helm chart values. This field is supported only for {{site.data.keyword.cloud_notm}} catalog offerings that are provisioned by using the Terraform Helm provider.|
|`template_data.values_metadata` | `[]interface{}]` | Optional |  The list of values metadata.|
|`template_data.variablestore` | `[]interface{}]` | Optional |  The variable request. |
|`template_ref` | String | Optional |  The workspace template reference.|
|`template_repo` | List | Optional |  The input parameter to specify the source repository where your {{site.data.keyword.bpshort}} template is stored.|
|`template_repo.branch` | String | Optional |  The branch in GitHub where your Terraform template is stored.|
|`template_repo.release` | String | Optional |  The release tag in GitHub of your Terraform template.|
|`template_repo.repo_sha_value` | String | Optional |  The SHA value from the repository.|
|`template_repo.repo_url` | String | Optional |  The URL to the repository where the {{site.data.keyword.cloud_notm}} catalog software template is stored.|
|`template_repo.url` | String | Optional |  The GitHub or GitLab repository URL where your Terraform and public bit bucket template is stored. For more information of the environment variable syntax, see [Create workspace new](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-new).|
|`type`| List | Optional | The Terraform version that you want to use to run your Terraform code. Enter terraform_v0.12 to use Terraform version 0.12. Make sure that your Terraform config files are compatible with the Terraform version that you select.
|`workspace_status`| List | Optional | The Workspace status request.|
|`workspace_status.frozen`| Bool | Optional | If set to `true`, the workspace is frozen and changes to the workspace are disabled.|
|`workspace_status.frozen_at` | `TypeString` | Optional |  The timestamp when the workspace was frozen.|
|`workspace_status.frozen_by` | String | Optional |  The user ID that froze the workspace.|
|`workspace_status.locked` | Bool | Optional |  If set to `true`, the workspace is locked and disabled for changes.|
|`workspace_status.locked_by` | String | Optional | The user ID that initiated a resource-related action, such as applying or destroying resources, that locked the workspace.|
|`workspace_status.locked_time` | `TypeString` | Optional | The timestamp when the workspace was locked.|
|`x_github_token` | String | Optional |  The personal access token to authenticate with your private GitHub or GitLab repository and access your Terraform template.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #wks-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the {{site.data.keyword.bpshort}} workspace.|
|`created_at`|String|The timestamp when the workspace is created.|
|`created_by `|String|The user ID that created the workspace.|
|`crc`|String|The workspace CRN.|
|`last_health_check_at` | String | The timestamp when the last health check is executed by {{site.data.keyword.bpshort}}.|
|`runtime_data` | String | The information about the provisioning engine, state file, and runtime logs.|
|`status`| String | The status of the workspace. For more information, see [workspace status](/docs/schematics?topic=schematics-workspace-setup#wks-state).|
|`updated_at`| String | The timestamp when the workspace last updated.|
|`updated_by`| String | The user ID that updated the workspace.|
|`workspace_status_msg` |String | The last action information that workspace run.|
{: caption="Table 1. Available output parameters" caption-side="top"}

