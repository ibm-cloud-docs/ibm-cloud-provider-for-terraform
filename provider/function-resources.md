---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-04"

keywords: terraform provider plugin, terraform functions, terraform open whisk, terraform function action, terraform serverless, terraform namespace

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



# Functions resources
{: #function-resources}

Review the {{site.data.keyword.openwhisk_short}} resources that you can create, update, or delete.
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_function_action`
{: #fn-action}

Create, update, or delete a {{site.data.keyword.openwhisk_short}} action. Actions are stateless code snippets that run on the {{site.data.keyword.openwhisk_short}} platform. An action can be written as a JavaScript, Swift, or Python function, a Java method, or a custom executable program packaged in a Docker container. To bundle and share related actions, use the `function_package` resource.


### Sample Terraform code
{: #fn-action-sample}

####  Simple JavaScript action
{: #js-action}

The following example creates a JavaScript action. 
{: shortdesc}

```
resource "ibm_function_action" "nodehello" {
  name      = "action-name"
  namespace = "function-namespace-name"

  exec {
    kind = "nodejs:6"
    code = file("hellonode.js")
  }
}

```
{: codeblock}

#### Passing parameters to an action
{: #parameter-action}

The following example shows how to pass parameters to an action. 
{: shortdesc}

```
resource "ibm_function_action" "nodehellowithparameter" {
  name      = "hellonodeparam"
  namespace = "function-namespace-name"
  
  exec {
    kind = "nodejs:6"
    code = file("hellonodewithparameter.js")
  }

  user_defined_parameters = <<EOF
        [
    {
        "key":"place",
        "value":"India"
    }
        ]

EOF

}
```
{: codeblock}

#### Packaging an action as a Node.js module
{: #action-package}

The following example packages a JavaScript action to a module. 
{: shortdesc}

``` 
resource "ibm_function_action" "nodezip" {
  name      = "nodezip"
  namespace = "function-namespace-name"

  exec {
    kind      = "nodejs:6"
    code_path = "nodeaction.zip"
  }
}
```
{: codeblock}

#### Creating action sequences
{: #action-sequence}

The following example creates an action sequence. 
{: shortdesc}

``` 
resource "ibm_function_action" "swifthello" {
  name      = "actionsequence"
  namespace = "function-namespace-name"

  exec {
    kind       = "sequence"
    components = ["/whisk.system/utils/split", "/whisk.system/utils/sort"]
  }
}
```
{: codeblock}

### Creating Docker actions
{: #docker-action}

The following example creates a Docker action. 
{: shortdesc}

``` 
resource "ibm_function_action" "swifthello" {
  name      = "dockeraction"
  namespace = "function-namespace-name"

  exec {
    kind   = "blackbox"	
    image  = "janesmith/blackboxdemo"
    code   = file("helloSwift.swift")
  }
}
```
{: codeblock}

### Input parameters
{: #fn-action-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | --------|
|`name`|String|Required|The name of the action.| Yes |
|`namespace`|String|Required|The name of the function namespace.| No |
|`limits`|List of objects|Optional|A nested block to describe assigned limits. | No |
|`limits.timeout`|Integer|Optional|The timeout limit to terminate the action, specified in milliseconds. Default value is `60000`.    | No |
|`limits.memory`|Integer|Optional|The maximum memory for the action, specified in megabyte. Default value is `256`.    | No |
|`limits.log_size`|Integer|Optional|The maximum log size for the action, specified in megabyte. Default value is `10`.| No |
|`exec`|List of objects|Required|A nested block to describe executable binaries.  | No |
|`exec.image`|String|Optional| When using the `blackbox` executable, the name of the container image name.        **NOTE**: Conflicts with `exec.components`, `exec.code`.    | No |
|`exec.init`|String|Optional| When using `nodejs`, the optional archive reference.        **NOTE**: Conflicts with `exec.components`, `exec.image`.    | No |
|`exec.code`|String|Optional| When not using the `blackbox` executable, the code to execute.       **NOTE**: Conflicts with `exec.components`, `exec.image`.    | No |
|`exec.code_path`|String|Optional| When not using the `blackbox` executable, the file path of code to execute and supports only `.zip` extension to create the action.       **NOTE**: Conflicts with `exec.components`, `exec.image`, `exec.code`.    | No |
|`exec.kind`|String|Required|The type of action. You can find supported kinds in the [IBM Cloud Functions Docs](/docs/openwhisk?topic=openwhisk-runtimes).    | No |
|`exec.main`|String|Optional|The name of the action entry point (function or fully-qualified method name, when applicable).       **NOTE**: Conflicts with `exec.components`, `exec.image`.    | No |
|`exec.components`|String|Optional|The list of fully qualified actions. **NOTE**: Conflicts with `exec.code`, `exec.image`.| No |
|`publish`|Boolean|Optional|Action visibility.| No |
|`user_defined_annotations`|String|Optional|Annotations defined in key value format.| No |
|`user_defined_parameters`|String|Optional|Parameters defined in key value format. Parameter bindings included in the context passed to the action. Cloud Function backend/API.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #fn-action-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the new action.|
|`namespace`|String| The name of the function namespace.|
|`version`|String|Semantic version of the item.|
|`annotations`|List|All annotations to describe the action, including those set by you or by IBM Cloud Functions.|
|`parameters`|List|All parameters passed to the action when the action is invoked, including those set by you or by the IBM Cloud Functions.|
|`action_id`|String|The action ID.|
|`target_endpoint_url` | String | The target endpoint URL of the action. |
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #fn-action-import}

`ibm_function_action` can be imported by using the namespace and action ID.

**Example**

```
terraform import ibm_function_action.nodeAction <namespace>:<action_id>

terraform import ibm_function_action.nodeAction Namespace-01:nodezip
```
{: pre}

## `ibm_function_namespace`
{: #fn-namespace}

Create, update, or delete an IBM Cloud Functions namespace. For more information, about managing namespace, see [Managing namespace](/docs/openwhisk?topic=openwhisk-namespaces). Then, you can create IAM managed namespaces to group entities such as actions, triggers or both.

### Sample Terraform code
{: #fn-namespace-sample}

The following example creates the namespace and package at a specific location.

```
provider "ibm" {
  ibmcloud_api_key   = var.ibmcloud_api_key
  region = var.region
}

data "ibm_resource_group" "resource-group" {
   name = var.resource_group
}

resource "ibm_function_namespace" "namespace" {
   name                = var.namespace
   resource_group_id   = data.ibm_resource_group.resource-group.id
}

resource "ibm_function_package" "package" {
  name      = var.packagename
  namespace = ibm_function_namespace.namespace.name
}
```
{: codeblock}

### Input parameters
{: #fn-namespace-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
|`name`|String|Required|The name of the namespace.| No |
|`description`|String|Optional|The description of the namespace.| No|
|`resource_group_id`|String|Required| The ID of the resource group.  You can retrieve the value from data source `ibm_resource_group`. | Yes |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #fn-namespace-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the new namespace.|
|`location`|String| Target locations of the namespace.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #fn-namespace-import}

`ibm_function_namespace` can be imported using the namespace ID.

Namespace import will not return the value for `resource_group_id` attribute.
{: note}

**Syntax**

```
terraform import ibm_function_namespace.namespace <namespaceID>

```
{: pre}

**Example**

```
terraform import ibm_function_namespace.namespace 4cf78bb1-2298-413f-8575-2464948a344b

```
{: pre}


## `ibm_function_package`
{: #fn-package}

Create, update, or delete an IBM Cloud Functions package. You can the packages to bundle together a set of related actions, and share them with others. To create actions, use the `function_action` resource.

### Sample Terraform code
{: #fn-package-sample}

#### Create a package
{: #create-package}

The following example creates the `mypackage` package. 

```
resource "ibm_function_package" "package" {
  name = "mypackage"

  user_defined_annotations = <<EOF
        [
    {
        "key":"description",
        "value":"Count words in a string"
    },
    {
        "key":"sampleOutput",
        "value": {
                        "count": 3
                }
    },
    {
        "key":"final",
        "value": [
                        {
                                "description": "A string",
                                "name": "payload",
                                "required": true
                        }
                ]
    }
]
EOF
}
```
{: codeblock}

#### Create a package by using a binding
{: #package-service-binding}

The following example shows how to bind a package. 
{: shortdesc}

``` 
resource "ibm_function_package" "bindpackage" {
  name              = "bindalaram"
  bind_package_name = "/whisk.system/alarms/alarm"

  user_defined_parameters = <<EOF
        [
    {
        "key":"cron",
        "value":"0 0 1 0 *"
    },
    {
        "key":"trigger_payload ",
        "value":"{'message':'bye old Year!'}"
    },
    {
        "key":"maxTriggers",
        "value":1
    },
    {
        "key":"userdefined",
        "value":"test"
    }
]
EOF
}

```

### Input parameters
{: #fn-package-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------- |
|`name`|String|Required|The name of the package.| Yes |
|`namespace`|String|Required|The name of the function namespace.| No|
|`publish`|Boolean|Optional|Package visibility.| No |
|`user_defined_annotations`|String|Optional|Annotations defined in key value format.| No |
|`user_defined_parameters`|String| Optional|Parameters defined in key value format. Parameter bindings included in the context passed to the package.| No |
|`bind_package_name`|String|Optional| Name of package to be bound.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #fn-package-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the new package.|
|`namespace`|String| The name of the function namespace.|
|`version`|String|Semantic version of the item.|
|`annotations`|String|All annotations to describe the package, including those set by you or by IBM Cloud Functions.|
|`parameters`|String|All parameters passed to the package, including those set by you or by IBM Cloud Functions.### Import`ibm_function_package` can be imported by using the ID. For example, ```$ terraform import ibm_function_package.sample hello```|
|`package_id`|String|The package ID.|
{: caption="Table 1. Available output parameters" caption-side="top"}




## `ibm_function_rule`
{: #fn-rule}

Create, update, or delete an IBM Cloud Functions rule. Events from external and internal event sources are channeled through a trigger, and rules allow your actions to react to these events. To set triggers, use the `function_trigger` resource.
{: shortdesc}

### Sample Terraform code
{: #fn-rule-sample}

The following example creates a rule for an action. 
{: shortdesc}

```
resource "ibm_function_action" "action" {
  name = "hello"

  exec {
    kind = "nodejs:6"
    code = file("test-fixtures/hellonode.js")
  }
}

resource "ibm_function_trigger" "trigger" {
  name = "alarmtrigger"

  feed = [
    {
      name = "/whisk.system/alarms/alarm"

      parameters = <<EOF
                    [
                        {
                            "key":"cron",
                            "value":"0 */2 * * *"
                        }
                    ]
                EOF
    },
  ]
}

resource "ibm_function_rule" "rule" {
  name         = "alarmrule"
  trigger_name = ibm_function_trigger.trigger.name
  action_name  = ibm_function_action.action.name
}

```
{: codeblock}

### Input parameters
{: #fn-rule-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | ------ |
|`name`|String|Required|The name of the rule.| Yes |
|`namespace`|String|Required|The name of the function namespace.| No|
|`trigger_name`|String|Required|The name of the trigger.| No |
|`action_name`|String|Required|The name of the action.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #fn-rule-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the new rule.|
|`namespace`|String| The name of the function namespace.|
|`publish`|Boolean|Rule visibility.|
|`version`|String|Semantic version of the item.|
|`status`|String|The status of the rule.|
|`rule_id`|String|The rule ID.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #fn_rule-import}

`ibm_function_rule` can be imported by using the ID.

**Example**
```
terraform import ibm_function_rule.sampleRule alarmrule
```
{: pre}


## `ibm_function_trigger`
{: #fn-trigger}

Create, update, or delete an IBM Cloud Functions trigger. Events from external and internal event sources are channeled through a trigger, and rules allow your actions to react to these events. To set rules, use the `function_rule` resource.
{: shortdesc}

### Sample Terraform code
{: #fn-trigger-sample}

#### Creating triggers
{: #create-trigger}

The following example creates the `mytrigger` trigger. 
{: shortdesc}

```
resource "ibm_function_trigger" "trigger" {
  name = "mytrigger"

  user_defined_parameters = <<EOF
                        [
                                {
                                        "key":"place",
                                        "value":"India"
                           }
                   ]
           EOF

  user_defined_annotations = <<EOF
           [
                   {
                          "key":"Description",
                           "value":"Sample code to display hello"
                  }
          ]
  EOF
}
```
{: codeblock}

#### Creating a trigger feed
{: #create-trigger-feed}

The following example creates a feed for the `alarmFeed` trigger. 
{: shortdesc}

```
resource "ibm_function_trigger" "feedtrigger" {
  name = "alarmFeed"

  feed = [
    {
      name = "/whisk.system/alarms/alarm"

      parameters = <<EOF
                [
                        {
                                "key":"cron",
                                "value":"0 */2 * * *"
                        }
                ]
                EOF
    },
  ]

  user_defined_annotations = <<EOF
                 [
         {
                 "key":"sample trigger",
                 "value":"Trigger for hello action"
         }
                 ]
                 EOF
}
```
{: codeblock}


### Input parameters
{: #fn-trigger-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description | Forces new resource |
| ------------- |-------------| ----- | -------------- | -------- |
|`name`|String|Required|The name of the trigger.| Yes |
|`namespace`|String|Required|The name of the function namespace.| No |
|`feed`|List|Optional| A nested block to describe the feed.   | Yes |
|`feed.name`|String|Required|Trigger feed `ACTION_NAME`.    | Yes |
|`feed.parameters`|String|Optional|Parameters definitions in key value format. Parameter bindings are included in the context and passed when the action is invoked.| No |
|`user_defined_annotations`|String|Optional| Annotation definitions in key value format.| No |
|`user_defined_parameters`|String|Optional|Parameters definitions in key value format. Parameter bindings are included in the context and passed to the trigger.| No |
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #fn-trigger-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`id`|String|The ID of the new trigger.|
|`namespace`|String| The name of the function namespace.|
|`publish`|Boolean|Trigger visibility.|
|`version`|String|Semantic version of the item.|
|`annotations`|String|All annotations to describe the trigger, including those set by you or by IBM Cloud Functions.|
|`parameters`|String|All parameters passed to the trigger, including those set by you or by IBM Cloud Functions.|
|`trigger_id`|String|The trigger ID.|
{: caption="Table 1. Available output parameters" caption-side="top"}

### Import
{: #fn-trigger-import}

`ibm_function_trigger` can be imported by using the ID.

**Example**
```
terraform import ibm_function_trigger.trigger alaram
```
{: pre}
