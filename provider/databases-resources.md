---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-26"

keywords: terraform provider plugin, terraform cloud databases, terraform databases, terraform postgres, terraform mysql, terraform compose

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



# {{site.data.keyword.databases-for}} resources
{: #databases-resources}

Review the {{site.data.keyword.databases-for}} resources that you can create, modify, or delete. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_database`
{: #db}

Create, update, or delete a {{site.data.keyword.databases-for}} instance. The `ibmcloud_api_key` that is defined in the `provider` block and used by Terraform must have sufficient IAM access to create and modify {{site.data.keyword.databases-for}} instances. Also, must have access to the resource group where you want to deploy the instance. For more information, see the [documentation](/docs/databases-for-postgresql?topic=databases-for-postgresql-user-management).

To create a {{site.data.keyword.databases-for}} instance, you must specify the `region` and `ibmcloud_api_key` parameters in the `provider` block of your Terraform configuration file. The region must match the region where you want to deploy your instance. If the region is not specified `us-south` is used by default. 
{: note}

### Sample Terraform code
{: #db-sample}

To find an example for configuring a virtual server instance that connects to a PostgreSQL database, see [here](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-database).

```
data "ibm_resource_group" "group" {
  name = "<your_group>"
}

resource "ibm_database" "<your_database>" {
  name              = "<your_database_name>"
  plan              = "standard"
  location          = "eu-gb"
  service           = "databases-for-etcd"
  resource_group_id = data.ibm_resource_group.group.id
  tags              = ["tag1", "tag2"]

  adminpassword                = "password12"
  members_memory_allocation_mb = 3072
  members_disk_allocation_mb   = 61440
  users {
    name     = "user123"
    password = "password12"
  }
  whitelist {
    address     = "172.168.1.1/32"
    description = "desc"
  }
}

output "ICD_Etcd_database_connection_string" {
value = ibm_database.<your_database>.connectionstrings.0.composed
}

```
{: codeblock}

### Sample2 Terraform code
{: #db-time-recovery-sample}

To find an example for configuring point in time recovery time by using `ibm_database` resource. 
{: shortdesc}

```
data "ibm_resource_group" "group" {
  name = "<your_group>"
}

resource "ibm_database" "test_acc" {
  resource_group_id                    = data.ibm_resource_group.group.id
  name                                 = "<your_database_name>"
  service                              = "databases-for-postgresql"
  plan                                 = "standard"
  location                             = "eu-gb"
  point_in_time_recovery_time          = "2020-04-20T05:27:36Z"
  point_in_time_recovery_deployment_id = "crn:v1:bluemix:public:databases-for-postgresql:us-south:a/4448261269a14562b839e0a3019ed980:0b8c37b0-0f01-421a-bb32-056c6565b461::"
}
```
{: codeblock}

### Sample3 Terraform code by using auto_scaling
{: #auto-scaling}

```
resource "ibm_database" "autoscale" {
    resource_group_id            = data.ibm_resource_group.group.id
    name                         = "redis"
    service                      = "databases-for-redis"
    plan                         = "standard"
    location                     = "us-south"
    service_endpoints            = "private"
    auto_scaling {
        cpu {
            rate_increase_percent       = 20
            rate_limit_count_per_member = 20
            rate_period_seconds         = 900
            rate_units                  = "count"
        }
        disk {
            capacity_enabled             = true
            free_space_less_than_percent = 15
            io_above_percent             = 85
            io_enabled                   = true
            io_over_period               = "15m"
            rate_increase_percent        = 15
            rate_limit_mb_per_member     = 3670016
            rate_period_seconds          = 900
            rate_units                   = "mb"
        }
         memory {
            io_above_percent         = 90
            io_enabled               = true
            io_over_period           = "15m"
            rate_increase_percent    = 10
            rate_limit_mb_per_member = 114688
            rate_period_seconds      = 900
            rate_units               = "mb"
        }
    }
}
```
{: codeblock}

**provider.tf**

```
provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
  region           = "eu-gb"
}
```
{: codeblock}

For more information, of an example that is related to a VSI configuration to connect to a PostgreSQL database, refer [VSI configured connection](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-database){: external}.
{: note}

### Input parameters
{: #db-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}


|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| --------|
|`name`|String|Required|A descriptive name that is used to identify the database instance. The name must not include spaces.| No |
|`plan`|String|Required|The name of the service plan that you choose for your instance. Supported values are `standard`. | No |
|`location`|String|Required|The location where you want to deploy your instance. The location must match the `region` parameter that you specify in the `provider` block of your Terraform configuration file. The default value is `us-south`. Currently, supported regions are `us-south`, `us-east`, `eu-gb`, `eu-de`, `au-syd`, `jp-tok`, `oslo01`. | No |
|`resource_group_id`|String|Optional| The ID of the resource group where you want to create the instance. To retrieve this value, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. If no value is provided, the `default` resource group is used.| Yes |
|`tags`|Array of string|Optional|A list of tags that you want to add to your instance. | No |
|`service`|String|Required| The type of {{site.data.keyword.databases-for}} that you want to create. Only the following services are currently accepted: `databases-for-etcd`, `databases-for-postgresql`, `databases-for-redis`, `databases-for-elasticsearch`, `messages-for-rabbitmq`, and `databases-for-mongodb`.| No |
|`version`|String|Optional|The version of the database to be provisioned. If omitted, the database is created with the most recent major and minor version.| Yes |
|`adminpassword`|String|Optional| The password for the database administrator. If not specified, an empty string is provided for the password and the user ID cannot be used. In this case, more users must be specified in a `user` block.| No |
|`members_memory_allocation_mb`|Integer|Optional| The amount of memory in megabytes for the database, split across all members. If not specified, the default setting of the database service is used, which can vary by database type. | No |
|`members_disk_allocation_mb`|Integer|Optional|The amount of disk space for the database, split across all members. If not specified, the default setting of the database service is used, which can vary by database type. | No |
|`members_cpu_allocation_count`|Integer|Optional|Enables and allocates the number of specified dedicated cores to your deployment.| No |
|`backup_id`|String|Optional|The CRN of a backup resource to restore from. The backup is created by a database deployment with the same service ID. The backup is loaded after provisioning and the new deployment starts up that uses that data. A backup CRN is in the format `crn:v1:<…>:backup:`. If omitted, the database is provisioned empty.| No |
|`remote_leader_id`|String|Optional|A CRN of the leader database to make the replica(read-only) deployment. The leader database is created by a database deployment with the same service ID. A read-only replica is set up to replicate all of your data from the leader deployment to the replica deployment by using asynchronous replication. For more information, see [Configuring Read-only Replicas](/docs/databases-for-postgresql?topic=databases-for-postgresql-read-only-replicas).| No |
|`key_protect_key`|String|Optional|The CRN of a Key Protect root key that you want to use for disk encryption. A key protect CRN is in the format `crn:v1:<…>:key:`. You can specify the root key during the database creation only. After the database is created, you cannot update the root key. For more information, refer [Disk encryption](/docs/cloud-databases?topic=cloud-databases-key-protect#using-the-key-protect-key) documentation. | Yes |
|`backup_encryption_key_crn`| String | Optional | The CRN of a key protect key, that you want to use for encrypting disk that holds deployment backups. A key protect CRN is in the format `crn:v1:<...>:key:`. Backup_encryption_key_crn can be added only at the time of creation and no update support  are available.| Yes |
|`key_protect_instance`|String|Optional|The CRN of a key protect instance that you want to use for disk encryption. A key protect CRN is in the format `crn:v1:<…>::`.| Yes |
|`point_in_time_recovery_deployment_id`|String|Optional|The ID of the source deployment that you want to recover back to.| No |
|`point_in_time_recovery_time`|String|Optional|The timestamp in UTC format that you want to restore to. To retrieve the timestamp, run the `ibmcloud cdb postgresql earliest-pitr-timestamp <deployment name or CRN>` command. For more information, see [Point-in-time Recovery](/docs/databases-for-postgresql?topic=databases-for-postgresql-pitr). | No |
|`service_endpoints`|String|Optional|Specify whether you want to enable the public, private, or both service endpoints. Supported values are `public`, `private`, or `public-and-private`. The default is `public`.| No |
|`users`|List of objects|Optional|A list of users that you want to create on the database. Multiple blocks are allowed. | No |
|`users.name`|String|Optional|The user ID to add to the database instance. The user ID must be in the range 5 - 32 characters.| No |
|`users.password`|String|Optional|The password for the user ID. The password must be in the range 10 - 32 characters.| No |
|`whitelist`|List of objects|Optional|A list of allowed IP addresses for the database. Multiple blocks are allowed. | No |
|`whitelist.address`|String|Optional|The IP address or range of database client addresses to be whitelisted in CIDR format. Example, `172.168.1.2/32`.| No |
|`whitelist.description`|String|Optional|A description for the allowed IP addresses range. | No |
|`guid`|String|Optional|The unique identifier of the database instance.| No |
|`auto_scaling`|List|Optional|Configure rules to allow your database to automatically increase its resources. Single block of autoscaling is allowed at once.|No|
|`auto_scaling.cpu`|List|Optional|Single block of CPU is allowed at once by CPU autoscaling.|No|
|`auto_scaling.cpu.rate_increase_percent`|Integer|Optional|Auto scaling rate in increase percent.|No|
|`auto_scaling.cpu.rate_limit_count_per_member`|Integer|Optional|Auto scaling rate limit in count per number.|No|
|`auto_scaling.cpu.rate_period_seconds`|Integer|Optional|Period seconds of the auto scaling rate.|No|
|`auto_scaling.cpu.rate_units`|String|Optional|Auto scaling rate in units.|No|
|`auto_scaling.disk`|List|Optional|Single block of disk is allowed at once in disk auto scaling.|No|
|`auto_scaling.disk.capacity_enabled`|Bool|Optional|Auto scaling scalar enables or disables the scalar capacity.|No|
|`auto_scaling.disk.free_space_less_than_percent`|Integer|Optional|Auto scaling scalar capacity free space less than percent.|No|
|`auto_scaling.disk.io_above_percent`|Integer|Optional|Auto scaling scalar I/O utilization above percent.|No|
|`auto_scaling.disk.io_enabled`|Bool|Optional|Auto scaling scalar I/O utilization enabled.|No|
|`auto_scaling.disk.rate_increase_percent`|Integer|Optional|Auto scaling rate increase percent.|No|
|`auto_scaling.disk.rate_limit_mb_per_member`|Integer|Optional|Auto scaling rate limit in megabytes per member.|No|
|`auto_scaling.disk.rate_period_seconds`|Integer|Optional|Auto scaling rate period in seconds.|No|
|`auto_scaling.disk.rate_units`|String|Optional|Auto scaling rate in units.|No|
|`auto_scaling.memory`|List|Optional|Memory Auto Scaling in single block of memory is allowed at once.|No|
|`auto_scaling.io_above_percent`|Integer|Optional|Auto scaling scalar I/O utilization above percent.|No|
|`auto_scaling.memory.io_enabled`|Bool|Optional|Auto scaling scalar I/O utilization enabled.|No|
|`auto_scaling.memory.io_over_period`|String|Optional|Auto scaling scalar I/O utilization over period.|No|
|`auto_scaling.memory.rate_increase_percent`|Integer|Optional|Auto scaling rate in increase percent.|No|
|`auto_scaling.memory.rate_limit_mb_per_member`|Integer|Optional|Auto scaling rate limit in megabytes per member.|No|
|`auto_scaling.memory.rate_period_seconds`|Integer|Optional|Auto scaling rate period in seconds.|No|
|`auto_scaling.memory.rate_units`|String|Optional|Auto scaling rate in units.|No|


### Output parameters
{: #db-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The CRN of the database instance.|
|`status`|String|The status of the instance. |
|`adminuser`|String|The user ID of the database administrator. Example, `admin` or `root`.|
|`version`|String|The database version.|
|`connectionstrings`|Array|A list of connection strings for the database for each user ID. For more information, about how to use connection strings, see the [documentation](/docs/databases-for-postgresql?topic=databases-for-postgresql-connection-strings). The results are returned in pairs of the userid and string: `connectionstrings.1.name = admin connectionstrings.1.string = postgres://admin:$PASSWORD@79226bd4-4076-4873-b5ce-b1dba48ff8c4.b8a5e798d2d04f2e860e54e5d042c915.databases.appdomain.cloud:32554/ibmclouddb?sslmode=verify-full` Individual string parameters can be retrieved by using Terraform variables and outputs `connectionstrings.x.hosts.x.port` and `connectionstrings.x.hosts.x.host`|

### Timeouts
{: #db-timeout}

The following timeouts are defined for this resource. 
{: shortdesc}

- **Create** The creation of the instance is considered failed when no response is received for 60 minutes.
- **Update** The update of the instance is considered failed when no response is received for 20 minutes.
- **Delete** The deletion of the instance is considered failed when no response is received for 10 minutes.

ICD create instance typically takes between 30-45 minutes. Delete and update takes a minute. Provisioning time is unpredictable. If the apply fails due to a timeout, import the database resource once the create is completed.
{: note}


### Import
{: #db-import}

The database instance can be imported by using the ID, that is formed from the CRN. To import the resource, you must specify the `region` parameter in the `provider` block of your Terraform configuration file. If the region is not specified, `us-south` is used by default. An Terraform refresh or apply fails, if the database instance is not in the same region as configured in the provider or its alias.

CRN is a 120 digit character string of the form -  `crn:v1:bluemix:public:databases-for-postgresql:us-south:a/4ea1882a2d3401ed1e459979941966ea:79226bd4-4076-4873-b5ce-b1dba48ff8c4::`
{: important}


**Syntax**
```
terraform import ibm_database.my_db <crn>
```
{: pre}

**Example**
```
terraform import ibm_database.my_db crn:v1:bluemix:public:databases-for-postgresql:us-south:a/4ea1882a2d3401ed1e459979941966ea:79226bd4-4076-4873-b5ce-b1dba48ff8c4::
```

Import requires a minimal Terraform config file to allow importing.

```
resource "ibm_database" "<your_database>" {
  name              = "<your_database_name>"
```

Run `terraform state show ibm_database.<your_database>` after import to retrieve the more values to be included in the resource config file. Observe the ICD exports the admin userid. It does not export any more user IDs and passwords that are configured on the instance. These values must be retrieved from an alternative source. If new passwords need to be configured or the connection string that is retrieved to use the service, a new users block must be defined to create new users. This limitation is due to a lack of ICD functionality.
