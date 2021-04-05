---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-05"

keywords: terraform provider plugin, terraform event streams, terraform event stream service, terraform event

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



# Event Streams resources
{: #event-streams-resources}


Review the [Event Streams](/docs/EventStreams?topic=EventStreams-about) resource that you can connect, administer, developed with Event Streams and integrate with the other services. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration/resources.html){: external}.
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## ibm_event_streams_topic
{: #event-streams}

Create and update the Event Streams.
{: shortdesc}

### Example 1 Create an Event Streams service instance and topic
{: #event-stream-sample}

Create an Event Streams service instance and topic.
{: shortdesc}

```
resource "ibm_resource_instance" "es_instance_1" {
  name              = "terraform-integration-1"
  service           = "messagehub"
  plan              = "standard" # "lite", "enterprise-3nodes-2tb"
  location          = "us-south" # "us-east", "eu-gb", "eu-de", "jp-tok", "au-syd"
  resource_group_id = data.ibm_resource_group.group.id

  # parameters = {
  #   service-endpoints     = "private"                    # for enterprise instance only, Options are: "public", "public-and-private", "private". Default is "public" when not specified.
  #   private_ip_allowlist = "[10.0.0.0/32,10.0.0.1/32]" # for enterprise instance only. Specify 1 or more IP range in CIDR format.
  #   # Refer private service endpoint and IP allow list to restrict access documentation, (
/docs/EventStreams?topic=EventStreams-restrict_access) for more details.
  #   throughput   = "150"  # for enterprise instance only. Options are: "150", "300", "450". Default is "150".
  #   storage_size = "2048" # for enterprise instance only. Options are: "2048", "4096", "6144", "8192", "10240", "12288". Default is "2048".
  #   Note: When throughput is "300", storage_size starts from "4096",  when throughput is "450", storage_size starts from "6144".
  #   Refer support combinations of throughput and storage_size documentation (
/docs/EventStreams?topic=EventStreams-ES_scaling_capacity#ES_scaling_combinations) for more details.
  # }

  # timeouts {
  #   create = "15m" # use 3h when creating enterprise instance, add more 1h for each level of non-default throughput, add more 30m for each level of non-default storage_size
  #   update = "15m" # use 1h when updating enterprise instance, add more 1h for each level of non-default throughput, add more 30m for each level of non-default storage_size
  #   delete = "15m"
  # }
}

resource "ibm_event_streams_topic" "es_topic_1" {
  resource_instance_id = ibm_resource_instance.es_instance_1.id
  name                 = "my-es-topic"
  partitions           = 1
  config = {
    "cleanup.policy"  = "compact,delete"
    "retention.ms"    = "86400000"
    "retention.bytes" = "1073741824"
    "segment.bytes"   = "536870912"
  }
}

```

### Example 2 Create a topic on an existing Event Streams instance
{: #event-stream-sample2}

Create topic on an existing Event Streams instance.
{: shortdesc}

The owner of the `ibmcloud_api_key` has permission to create Event Streams instance in a specified resource group. However, you need the manager role to create the instance in order to create topic.
 {: important}

```
data "ibm_resource_instance" "es_instance_2" {
  name              = "terraform-integration-2"
  resource_group_id = data.ibm_resource_group.group.id
}

resource "ibm_event_streams_topic" "es_topic_2" {
  resource_instance_id = data.ibm_resource_instance.es_instance_2.id
  name                 = "my-es-topic"
  partitions           = 1
  config = {
    "cleanup.policy"  = "compact,delete"
    "retention.ms"    = "86400000"
    "retention.bytes" = "1073741824"
    "segment.bytes"   = "536870912"
  }
}

```

### Example 3 Create a Kafka consumer application connection to an Event Streams instance and its topics
{: #event-stream-sample3}

Create a Kafka consumer application connection to an existing Event Streams instance and its topics.
{: shortdesc}

```
data "ibm_resource_instance" "es_instance_3" {
  name              = "terraform-integration-3"
  resource_group_id = data.ibm_resource_group.group.id
}

data "ibm_event_streams_topic" "es_topic_3" {
  resource_instance_id = data.ibm_resource_instance.es_instance_3.id
  name                 = "my-es-topic"
}

resource "kafka_consumer_app" "es_kafka_app" {
  bootstrap_server = lookup(data.ibm_resource_instance.es_instance_3.extensions, "kafka_brokers_sasl", [])
  topics           = [data.ibm_event_streams_topic.es_topic_3.name]
  apikey           = var.es_reader_api_key
}

```

### Input parameters
{: #event-streams-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`config`|Map|Optional|The configuration parameters of the topic. Supported configurations are: `cleanup.policy`, `retention.ms`, `retention.bytes`, `segment.bytes`, `segment.ms`, `segment.index.bytes`.|
|`name`|String|Required|The name of the topic.|
|`partitions`|Integer|Optional|The number of partitions of the topic. Default value is 1.|
|`resource_instance_id`|String|Required|The ID/CRN of the Event Streams service instance.|
{: caption="Table. Available input parameters" caption-side="top"}

### Output parameters
{: #event-streams-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the topic in CRN format. For example, `crn:v1:bluemix:public:messagehub:us-south:a/6db1b0d0b5c54ee5c201552547febcd8:cb5a0252-8b8d-4390-b017-80b743d32839:topic:my-es-topic`|
|`kafka_brokers_sasl`|Array of Strings|Kafka brokers use for interacting with Kafka native API.|
|`kafka_http_url`|String|The API endpoint for interacting with Event Streams REST API.|
{: caption="Table 1. Available output parameters" caption-side="top"}


### Import
{: #event-streams-import}

This resource can be imported by using `CRN`. The three parameters of the `CRN` with the colon separator are
  - ID = CRN 
  - resource type = topic
  - resource = name of the topic.
{: shortdesc}

**Syntax**
```
terraform import ibm_event_streams_topic.es_topic <crn>

```
**Example**
```
terraform import ibm_event_streams_topic.es_topic crn:v1:bluemix:public:messagehub:us-south:a/6db1b0d0b5c54ee5c201552547febcd8:cb5a0252-8b8d-4390-b017-80b743d32839:topic:my-es-topic
```

### Timeouts
{: #event-streams-timeouts}

Event Streams topic provides the following timeouts:

|Name|Description|
|----|-----------|
|`create`| Defaults to 15 minutes. **Note**: Use `3h` to create enterprise instance. Add more `1h` for each level of non-default through put and add extra `30m` for each level of non-default storage size.|
|`delete`| Defaults to 15 minutes. |
|`update`| Defaults to 15 minutes. **Note**: Use `1h` to update enterprise instance. Add more `1h` for each level of non-default through put and add extra `30m` for each level of non-default storage size.|