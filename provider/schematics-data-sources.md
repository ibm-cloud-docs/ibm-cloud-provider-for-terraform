---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-04"

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

## `ibm_schematics_action`
{: #schematics-actionds}

Retrieve information about a {{site.data.keyword.bpshort}} action. For more details about the Schematics and Schematics actions, see [Setting up an action](/docs/schematics?topic=schematics-action-setup).
{: shortdesc}

### Sample Terraform code
{: #schematics-action-dssample}


```
data "ibm_schematics_action" "schematics_action" {
	action_id = "action_id"
}
```
{: codeblock}

### Input parameters
{: #schematics-action-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
| `action_id`| String | Required | Use GET or actions API to look up the action IDs in your {{site.data.keyword.cloud_notm}} account.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #schematics-action-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
| `id` | String | The unique ID of the {{site.data.keyword.bpshort}} action.|
| `name` | String | The unique action name.|
| `description` | String | The action description.|
| `location` | String | List of action locations supported by {{site.data.keyword.bplong_notm}} service. **Note** this does not limit the location of the resources provisioned using {{site.data.keyword.bpshort}}.|
| `resource_group` | String | The resource group name for an action. By default, action is created in default resource group.|
| `tags` | String | The action tags.|
| `user_state` | String | User defined status of the Schematics object. Nested user_state blocks have the following structure.|
| `state` | String | User defined states * **draft Object** can be modified, and can be used by jobs run by an author, during execution * **live Object** can be modified, and can be used by jobs during execution * **locked Object** cannot be modified, and can be used by jobs during execution * **disable Object** can be modified, and cannot be used by Jobs during execution.|
| `set_by` | String | The name of an user who set the state of an Object.|
| `set_at` | String |  The user who set the state of an Object.|
| `source_readme_url` | String | URL of the `README` file, for the source.|
| `source` | String | Source of templates, playbooks, or controls. Nested `source` blocks have the following structure.|
| `source.source_type` | String | Type of source for the template.|
| `source.git` | String | The connection details to Git source. Nested `Git` blocks have the following structure.|
| `source.git.git_repo_url` | String | The URL to the Git repository that can be used to clone the template.|
| `source.git.git_token` | String | The personal access token to connect to Git URLs.|
| `source.git.git_repo_folder` | String | The name of the folder in the Git Repository, that contains the template.|
| `source.git.git_release` | String | The name of the release tag, used to fetch the Git Repository.|
| `source.git.git_branch` | String | The name of the branch, used to fetch the Git Repository.|
| `source_type` | String | Type of source for the template.|
| `command_parameter` | String | {{site.data.keyword.bpshort}} job command parameter such as  `playbook-name`, `capsule-name`, or `flow-name`.|
| `bastion` | String | The complete target details with the user inputs and the system generated data. Nested bastion blocks have the following structure.|
| `bastion.name` | String | The target name.|
| `bastion.type` | String | The target type such as, `cluster`, `vsi`, `icd`, `vpc`.|
| `bastion.description` | String | The target description.|
| `bastion.resource_query` | String | The resource selection query string.|
| `bastion.credential` | String | Override credential for each resource. Reference to credentials values, used by all the resources.|
| `bastion.id` | String | The target ID.|
| `bastion.created_at` | String | The targets creation time.|
| `bastion.created_by` | String | The Email address of the user who created the targets.|
| `bastion.updated_at` | String | The targets updation time.|
| `bastion.updated_by` | String | The Email address of user who updated the targets.|
| `bastion.sys_lock` | String | The system lock status. |Nested sys_lock blocks have the following structure.|
| `bastion.sys_lock.sys_locked` | String | Is the workspace locked by the {{site.data.keyword.bpshort}} action?|
| `bastion.sys_lock.sys_locked_by` | String | The name of the user who performed the action, that lead to lock the workspace.|
| `bastion.sys_lock.sys_locked_at` | String | When the user performed the action that lead to lock the workspace?|
| `bastion.resource_ids` | String | Array of the resource IDs.|
| `targets_ini` | String | Inventory of host and host group for the playbook in `INI` file format. For example, `"targets_ini": "[webserverhost] 172.22.192.6 [dbhost] 172.22.192.5"`. For more information, about an inventory host group syntax, see [Inventory host groups](/docs/schematics?topic=schematics-schematics-cli-reference#inventory-host-grps).|
| `credentials` | String | Credentials of an action. Nested `credentials` blocks have the following structure.|
| `credentials.name` | String | The name of the variable.
| `credentials.value` | String | The value for the variable or reference to the value.|
| `credentials.metadata` | String | User editable metadata for the variables. Nested `metadata` blocks have the following structure.|
| `credentials.metadata.type` | String | The type of the variable.|
aliases` | String | The list of an aliases for the variable name.|
| `credentials.metadata.description` | String | The description of the metadata.|
| `credentials.metadata.default_value` | String | The default value for the variable, if the override value is not specified.|
| `credentials.metadata.secure` | String | Is the variable secure or sensitive?|
| `credentials.metadata.immutable` | String | Is the variable readonly?|
| `credentials.metadata.hidden` | String | If set `true`, the variable will not be displayed on UI or CLI.
| `credentials.metadata.options` | String | The list of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `credentials.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `credentials.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `credentials.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `credentials.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `credentials.metadata.matches` | String | Regular expression for the variable value.|
| `credentials.metadata.position` | String | Relative position of this variable in a list.|
| `credentials.metadata.group_by` | String | Display name of the group this variable belongs to.|
| `credentials.metadata.source` | String | Source of the meta-data.|
| `credentials.link` | String | Reference link to the variable value By default the expression will point to `self.value`.|
| `inputs` | String | Input variables for an action. Nested `inputs` blocks have the following structure.|
| `inputs.name` | String | The name of the variable.|
| `inputs.value` | String | The value for the variable or reference to the value.|
| `inputs.metadata` | String | User editable metadata for the variables. Nested `metadata` blocks have the following structure.|
| `inputs.metadata.type` | String | The type of the variable.|
| `inputs.metadata.aliases` | String | The list of an aliases for the variable name.|
| `inputs.metadata.description` | String | The description of the metadata.|
| `inputs.metadata.default_value` | String | The default value for the variable, if the override value is not specified.|
| `inputs.metadata.secure` | String | Is the variable secure or sensitive?|
| `inputs.metadata.immutable` | String | Is the variable readonly?|
| `inputs.metadata.hidden` | String | If set to `true`, the variable will not be displayed on UI or CLI.|
| `inputs.metadata.options` | String | The list of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `inputs.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `inputs.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `inputs.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `inputs.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `inputs.metadata.matches` | String | Regular expression for the variable value.|
| `inputs.metadata.position` | String | Relative position of this variable in a list.|
| `inputs.metadata.group_by` | String | The display name of the group this variable belongs to.|
| `inputs.metadata.source` | String | The source of this metadata.|
| `inputs.link` | String | Reference link to the variable value By default the expression will point to `self.value`.|
| `outputs` | String | The output variables for an action. Nested `outputs` blocks have the following structure.|
| `outputs.name` | String | Name of the variable.|
| `outputs.value` | String | Value for the variable or reference to the value.|
| `outputs.metadata` | String | User editable metadata for the variables. Nested metadata blocks have the following structure.|
| `outputs.metadata.type` | String | Type of the variable.
| `outputs.metadata.aliases` | String | List of aliases for the variable name.|
| `outputs.metadata.description` | String | Description of the meta data.|
| `outputs.metadata.default_value` | String | Default value for the variable, if the override value is not specified.|
| `outputs.metadata.secure` | String | Is the variable secure or sensitive?|
| `outputs.metadata.immutable` | String | Is the variable readonly ?|
| `outputs.metadata.hidden` | String | If true, the variable will not be displayed on UI or CLI.|
| `outputs.metadata.options` | String | List of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `outputs.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `outputs.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `outputs.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `outputs.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `outputs.metadata.matches` | String | Regex for the variable value.|
| `outputs.metadata.position` | String | Relative position of this variable in a list.|
| `outputs.metadata.group_by` | String | Display name of the group this variable belongs to.|
| `outputs.metadata.source` | String | Source of this meta-data.|
| `outputs.link` | String | Reference link to the variable value By default the expression will point to self.value.|
| `settings` | String | Environment variables for an action. Nested settings blocks have the following structure.|
| `settings.name` | String | Name of the variable.|
| `settings.value` | String | Value for the variable or reference to the value.|
| `settings.metadata` | String | User editable metadata for the variables. Nested metadata blocks have the following structure.|
| `settings.metadata.type` | String | Type of the variable.|
| `settings.metadata.aliases` | String | List of aliases for the variable name.|
| `settings.metadata.description` | String | Description of the meta data.|
| `settings.metadata.default_value` | String | Default value for the variable, if the override value is not specified.|
| `settings.metadata.secure` | String | Is the variable secure or sensitive?|
| `settings.metadata.immutable` | String | Is the variable readonly ?.|
| `settings.metadata.hidden` | String | If true, the variable will not be displayed on UI or CLI.|
| `settings.metadata.options` | String | List of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `settings.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `settings.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `settings.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `settings.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `settings.metadata.matches` | String | Regex for the variable value.|
| `settings.metadata.position` | String | Relative position of this variable in a list.|
| `settings.metadata.group_by` | String | Display name of the group this variable belongs to.|
| `settings.metadata.source` | String | Source of this meta-data.|
| `settings.link` | String | Reference link to the variable value By default the expression will point to `self.value`.|
| `trigger_record_id` | String | ID to the trigger.|
| `id` | String | The action ID.|
| `crn` | String | The action Cloud Resource Name.|
| `account` | String | The action account ID.|
| `source_created_at` | String | The Ansible playbook cource creation time.|
| `source_created_by` | String | The Email address of user who created the Ansible playbook Source.|
| `source_updated_at` | String | The Ansible playbook updation time.|
| `source_updated_by` | String | The Email address of user who updated the Ansible playbook source.|
| `created_at` | String | The action creation time.|
| `created_by` | String | The Email address of the user who created an action.|
| `updated_at` | String | The action updation time.|
| `updated_by` | String | The Email address of the user who updated an action.|
| `namespace` | String | The name of the namespace.|
| `state` | String | Computed state of an action. Nested `state` blocks have the following structure.|
| `state.status_code` | String | The status of automation such as `workdspace`, or `action`.|
| `state.status_message` | String | Automation status message to be displayed along with the status code.|
| `playbook_names` | String | Playbook names retrieved from the respository.|
| `sys_lock` | String | System lock status. Nested sys_lock blocks have the following structure.|
| `sys_lock.sys_locked` | String | Is the Workspace locked by the Schematic action?|
| `sys_lock.sys_locked_by` | String | Name of the user who performed the action, that lead to lock the Workspace.|
| `sys_lock.sys_locked_at` | String | When the user performed the action that lead to lock the Workspace?|
{: caption="Table 1. Available output parameters" caption-side="top"}


## `ibm_schematics_job`
{: #schematics-jobds}

Retrieve information about a {{site.data.keyword.bpshort}} job. For more details about the Schematics and Schematics job, see [setting up jobs](docs/schematics?topic=schematics-action-setup#action-jobs).
{: shortdesc}

### Sample Terraform code
{: #schematics-action-dssample}


```
data "ibm_schematics_job" "schematics_job" {
	job_id = "job_id"
}
```
{: codeblock}

### Input parameters
{: #schematics-action-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type| Required / optional|Description|
|----|-----------|--------|----------------------|
| `job_id`| String | Required | Use GET or jobs API to look up the job IDs in your {{site.data.keyword.cloud_notm}} account.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #schematics-action-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|-------------|
| `id` | String | The unique ID of the {{site.data.keyword.bpshort}} job.|
| `command_object` | String | The name of the {{site.data.keyword.bpshort}} automation resource.|
| `command_object_id` | String | The job command object ID such as `workspace-id`, `action-id`, or `control-id`.|
| `command_name` | String | The {{site.data.keyword.bpshort}}job command name.|
| `command_parameter` | String |  The {{site.data.keyword.bpshort}} job command parameter  such as `playbook-name`, `capsule-name`, or `flow-name`.|
| `command_options` | String | The command line options for the command.|

| `settings` | String | Environment variables for an action. Nested settings blocks have the following structure.|
| `settings.name` | String | Name of the variable.|
| `settings.value` | String | Value for the variable or reference to the value.|
| `settings.metadata` | String | User editable metadata for the variables. Nested metadata blocks have the following structure.|
| `settings.metadata.type` | String | Type of the variable.|
| `settings.metadata.aliases` | String | List of aliases for the variable name.|
| `settings.metadata.description` | String | Description of the meta data.|
| `settings.metadata.default_value` | String | Default value for the variable, if the override value is not specified.|
| `settings.metadata.secure` | String | Is the variable secure or sensitive?|
| `settings.metadata.immutable` | String | Is the variable readonly ?.|
| `settings.metadata.hidden` | String | If true, the variable will not be displayed on UI or CLI.|
| `settings.metadata.options` | String | List of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `settings.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `settings.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `settings.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `settings.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `settings.metadata.matches` | String | Regex for the variable value.|
| `settings.metadata.position` | String | Relative position of this variable in a list.|
| `settings.metadata.group_by` | String | Display name of the group this variable belongs to.|
| `settings.metadata.source` | String | Source of this meta-data.|
| `settings.link` | String | Reference link to the variable value By default the expression will point to `self.value`.|
| `id` | String | The job ID.|
| `tags` | String |User defined tags, while running the job.|
| `id` | String | The job ID.|
| `name` | String |The unique job name, derived from the related action.|
| `description` | String | The job description derived from the related action.|
| `location` | String | List of an action locations supported by {{site.data.keyword.bplong_notm}} service. Note this does not limit the location of the resources provisioned using {{site.data.keyword.bpshort}}.|
| `resource_group` | String | The resource group name derived from the related action.|
| `submitted_at` | String |The job submission time.|
| `submitted_by` | String | The Email address of the user who submitted the job.|
| `start_at` | String | The job start time.|
| `end_at` | String |The job end time.|
| `duration` | String | Duration of job execution, for example, `40 seconds`.|
| `status` | String | The job status. Nested `status` blocks have the following structure.|
| `status.action_job_status` | String |Action Job Status. Nested a`ction_job_status` blocks have the following structure.|
| `status.action_job_status.action_name` | String | The action name.|
| `status.action_job_status.status_code` | String |Status of the jobs.|
| `status.action_job_status.status_message` | String |Action job status message to be displayed along with the `a`ction_status_code`.|
| `status.action_job_status.bastion_status_code` | String |Status of the resources.|
| `status.action_job_status.bastion_status_message` | String |Bastion status message to be displayed along with the bastion_status_code.|
| `status.action_job_status.targets_status_code` | String |Status of the resources.|
| `status.action_job_status.targets_status_message` | String |Aggregated status message for all target resources, to be displayed along with the targets_status_code.|
| `status.action_job_status.updated_at` | String |Job status updation timestamp.|
| `data| String | The Job data. Nested data blocks have the following structure.|
| `data.job_type` | String | Type of the job.|
| `data.action_job_data`| String | The action job data. Nested `action_job_data` blocks have the following structure.|
| `data.action_job_data.action_name`| String | The flow name.|
| `data.action_job_data.inputs` | String | Input variables for an action job. Nested `inputs` blocks have the following structure.|
| `data.action_job_data.inputs.name` | String | The name of the variable.|
| `data.action_job_data.inputs.value` | String | The value for the variable or reference to the value.|
| `data.action_job_data.inputs.metadata` | String | User editable metadata for the variables. Nested `metadata` blocks have the following structure.|
| `data.action_job_data.inputs.metadata.type` | String | The type of the variable.
| `data.action_job_data.inputs.metadata.aliases` | String | The list of an aliases for the variable name.|
| `data.action_job_data.inputs.metadata.description` | String | The description of the metadata.|
| `data.action_job_data.inputs.metadata.default_value` | String | The default value for the variable, if the override value is not specified.|
| `data.action_job_data.inputs.metadata.secure` | String | Is the variable secure or sensitive?|
| `data.action_job_data.inputs.metadata.immutable` | String | Is the variable readonly?|
| `data.action_job_data.inputs.metadata.hidden` | String | If set to `true`, the variable will not be displayed on UI or CLI.|
| `data.action_job_data.inputs.metadata.options` | String | The list of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `data.action_job_data.inputs.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `data.action_job_data.inputs.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `data.action_job_data.inputs.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `data.action_job_data.inputs.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `data.action_job_data.inputs.metadata.matches` | String | Regular expression for the variable value.|
| `data.action_job_data.inputs.metadata.position` | String | Relative position of this variable in a list.|
| `data.action_job_data.inputs.metadata.group_by` | String | The display name of the group this variable belongs to.|
| `data.action_job_data.inputs.metadata.source` | String | The source of this metadata.|
| `data.action_job_data.inputs.link` | String | Reference link to the variable value By default the expression will point to `self.value`.|
| `outputs` | String | The output variables for an action. Nested `outputs` blocks have the following structure.|
| `outputs.name` | String | Name of the variable.|
| `outputs.value` | String | Value for the variable or reference to the value.|
| `outputs.metadata` | String | User editable metadata for the variables. Nested metadata blocks have the following structure.|
| `outputs.metadata.type` | String | Type of the variable.
| `outputs.metadata.aliases` | String | List of aliases for the variable name.|
| `outputs.metadata.description` | String | Description of the meta data.|
| `outputs.metadata.default_value` | String | Default value for the variable, if the override value is not specified.|
| `outputs.metadata.secure` | String | Is the variable secure or sensitive?|
| `outputs.metadata.immutable` | String | Is the variable readonly ?|
| `outputs.metadata.hidden` | String | If true, the variable will not be displayed on UI or CLI.|
| `outputs.metadata.options` | String | List of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `outputs.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `outputs.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `outputs.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `outputs.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `outputs.metadata.matches` | String | Regex for the variable value.|
| `outputs.metadata.position` | String | Relative position of this variable in a list.|
| `outputs.metadata.group_by` | String | Display name of the group this variable belongs to.|
| `outputs.metadata.source` | String | Source of this meta-data.|
| `outputs.link` | String | Reference link to the variable value By default the expression will point to `self.value`.|
| `settings` | String | The environment variables used by all the templates in an action. Nested `settings` blocks have the following structure.|
| `settings.name` | String | Name of the variable.|
| `settings.value` | String | Value for the variable or reference to the value.|
| `settings.metadata` | String | User editable metadata for the variables. Nested metadata blocks have the following structure.|
| `settings.metadata.type` | String | Type of the variable.
| `settings.metadata.aliases` | String | List of aliases for the variable name.|
| `settings.metadata.description` | String | Description of the meta data.|
| `settings.metadata.default_value` | String | Default value for the variable, if the override value is not specified.|
| `settings.metadata.secure` | String | Is the variable secure or sensitive?|
| `settings.metadata.immutable` | String | Is the variable readonly ?|
| `settings.metadata.hidden` | String | If true, the variable will not be displayed on UI or CLI.|
| `settings.metadata.options` | String | List of possible values for this variable. If type is integer or date, then the array of string will be converted to array of integers or date during runtime.|
| `settings.metadata.min_value` | String | Minimum value of the variable. Applicable for integer type.|
| `settings.metadata.max_value` | String | Maximum value of the variable. Applicable for integer type.|
| `settings.metadata.min_length` | String | Minimum length of the variable value. Applicable for string type.|
| `settings.metadata.max_length` | String | Maximum length of the variable value. Applicable for string type.|
| `settings.metadata.matches` | String | Regex for the variable value.|
| `settings.metadata.position` | String | Relative position of this variable in a list.|
| `settings.metadata.group_by` | String | Display name of the group this variable belongs to.|
| `settings.metadata.source` | String | Source of this meta-data.|
| `settings.link` | String | Reference link to the variable value By default the expression will point to `self.value`.|
| `targets_ini` | String | Inventory of host and host group for the playbook in `INI` file format. For example, `"targets_ini": "[webserverhost] 172.22.192.6 [dbhost] 172.22.192.5"`. For more information, about an inventory host group syntax, see [Inventory host groups](/docs/schematics?topic=schematics-schematics-cli-reference#inventory-host-grps).|
| `bastion` | String | The complete target details with the user inputs and the system generated data. Nested bastion blocks have the following structure.|
| `bastion.name` | String | The target name.|
| `bastion.type` | String | The target type such as, `cluster`, `vsi`, `icd`, `vpc`.|
| `bastion.description` | String | The target description.|
| `bastion.resource_query` | String | The resource selection query string.|
| `bastion.credential` | String | Override credential for each resource. Reference to credentials values, used by all the resources.|
| `bastion.id` | String | The target ID.|
| `bastion.created_at` | String | The targets creation time.|
| `bastion.created_by` | String | The Email address of the user who created the targets.|
| `bastion.updated_at` | String | The targets updation time.|
| `bastion.updated_by` | String | The Email address of user who updated the targets.|
| `bastion.sys_lock` | String | The system lock status. |Nested sys_lock blocks have the following structure.|
| `bastion.sys_lock.sys_locked` | String | Is the workspace locked by the {{site.data.keyword.bpshort}} action?|
| `bastion.sys_lock.sys_locked_by` | String | The name of the user who performed the action, that lead to lock the workspace.|
| `bastion.sys_lock.sys_locked_at` | String | When the user performed the action that lead to lock the workspace?|
| `bastion.resource_ids` | String | Array of the resource IDs.|
| `log_summary` | String |Job log summary record. Nested `log_summary` blocks have the following structure.|
| `log_summary.job_id` | String | The workspace ID.|
| `log_summary.job_type` | String |The type of job.|
| `log_summary.log_start_at` | String |The job log start timestamp.|
| `log_summary.log_analyzed_till` | String | The job log update timestamp.|
| `log_summary.elapsed_time` | String |The job log elapsed time `log_analyzed_till`, `log_start_at`.|
| `log_summary.log_errors` | String |Job log errors. Nested log_errors blocks have the following structure.|
| `log_summary.log_errors.error_code` | String |The error code in the Log. |
| `log_summary.log_errors.error_msg` | String |The summary error message in the log.|
| `log_summary.log_errors.error_count` | String |  The number of occurrence.|
| `log_summary.repo_download_job` | String |Repo download Job log summary. Nested `repo_download_job `blocks have the following structure.|
| `log_summary.repo_download_job.scanned_file_count` | String | The number of files scanned.|
| `log_summary.repo_download_job.quarantined_file_count` | String | The number of files quarantined.|
| `log_summary.repo_download_job.detected_filetype` | String |Detected template or data file type.|
| `log_summary.repo_download_job.inputs_count` | String | The number of inputs detected.|
| `log_summary.repo_download_job.outputs_count` | String | The number of outputs detected.|
| `log_summary.action_job` | String |The flow job log summary. Nested `action_job` blocks have the following structure.|
| `log_summary.action_job.target_count` | String | The number of targets or hosts.| 
| `log_summary.action_job.task_count` | String |The number of tasks in playbook.|
| `log_summary.action_job.play_count` | String |number of plays in playbook.
| `log_summary.action_job.recap` | String |Recap records. Nested recap blocks have the following structure.|
| `log_summary.action_job.recap.target` | String |The list of target or host name.|
| `log_summary.action_job.recap.ok` | String |the number of OK.|
| `log_summary.action_job.recap.changed` | String | The number of changed.|
| `log_summary.action_job.recap.failed` | String | The number of failed.|
| `log_summary.action_job.recap.skipped` | String |The number of skipped.|
| `log_summary.action_job.recap.unreachable` | String |The number of unreachable.|
| `log_store_url` | String | The job log store URL.|
| `state_store_url` | String |The job state store URL.|
| `results_url` | String |The job results store URL.|
| `updated_at` | String | The job status updation timestamp.|


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
0000

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
