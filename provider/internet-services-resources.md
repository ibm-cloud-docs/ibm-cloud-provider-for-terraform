---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider, terraform resources internet service, terraform resources cis, tf provider plugin

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
{:swift-ios: .ph data-hd-programlang='iOS Swift'}
{:swift-server: .ph data-hd-programlang='server-side Swift'}
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



# Internet services resources
{: #cis-resources}

Review the [{{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis) resources that you can create, modify, or delete. You can reference the output parameters for each resource in other resources or data sources by using [Terraform interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 
{: shortdesc}

Before you start working with your resource, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}

## `ibm_cis`
{: #cis}

Create, update, or delete an {{site.data.keyword.cis_full_notm}} instance. 

### Sample Terraform code
{: #cis-sample}

```
data "ibm_resource_group" "group" {
  name = "test"
}

resource "ibm_cis" "cis_instance" {
  name              = "test"
  plan              = "standard"
  resource_group_id = data.ibm_resource_group.group.id
  tags              = ["tag1", "tag2"]
  location          = "global"

  //User can increase timeouts
  timeouts {
    create = "15m"
    update = "15m"
    delete = "15m"
  }
}
```
{: codeblock}

### Input parameters
{: #cis-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`name`|String|Required|A descriptive name for your {{site.data.keyword.cis_full_notm}} instance.|
|`plan`|String|Required|The name of the plan for your instance. To retrieve this value, run `ibmcloud catalog service internet-svcs`. |
|`location`|String|Required|The target location where you want to create your instance.|
|`resource_group_id`|String|Optional|The ID of the resource group where you want to create the service. To retrieve this value, run `ibmcloud resource groups` or use the `ibm_resource_group` data source. If no value is specified, the `default` resource group is used. |
|`tags`|Array|Optional|A list of tags that you want to associate with the instance.|

### Output parameters
{: #cis-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The CRN of the {{site.data.keyword.cis_full_notm}} instance.|
|`guid`|String|The unique identifier of the {{site.data.keyword.cis_full_notm}} instance.|
|`status`|String|The status of the {{site.data.keyword.cis_full_notm}} instance.|

### Timeouts
{: #cis-timeouts}

The following timeouts are defined for this resource.
{: shortdesc}

- **Create**: The creation of the {{site.data.keyword.cis_full_notm}} instance is considered failed if no response is received for 10 minutes.
- **Update**: The update of the {{site.data.keyword.cis_full_notm}} instance is considered failed if no response is received for 10 minutes.
- **Delete**: The deletion of the {{site.data.keyword.cis_full_notm}} instance is considered failed if no response is received for 10 minutes.

### Import
{: #cis-import}

The {{site.data.keyword.cis_full_notm}} instance can be imported by using the `crn`. 

```
terraform import ibm_cis.myorg <crn>
```
{: pre}





## `ibm_cis_cache_settings`
{: #cis-cache}

 Provides an {{site.data.keyword.cis_full_notm}} cache settings resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS Domain resource. It allows to create, update, or delete cache settings of a domain of an {{site.data.keyword.cis_full_notm}} CIS instance. For more information about cache setting, refer to [CIS cache concepts](/docs/cis?topic=cis-caching-concepts).
 {: shortdesc}

### Sample Terraform code
{: #cis-cache-sample}

```
# Change Cache Settings of the domain

resource "ibm_cis_cache_settings" "cache_settings" {
  cis_id             = data.ibm_cis.cis.id
  domain_id          = data.ibm_cis_domain.cis_domain.domain_id
  caching_level      = "aggressive"
  browser_expiration = 14400
  development_mode   = "off"
  query_string_sort  = "off"
  purge_all          = true
}
```
{: codeblock}

### Input parameters
{: #cis-cache-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`browser_expiration`|Integer|Optional|The Browser expiration settings. Valid values are `0, 30, 60, 300, 1200, 1800, 3600, 7200, 10800, 14400, 18000, 28800, 43200, 57600, 72000, 86400, 172800, 259200, 345600, 432000, 691200, 1382400, 2073600, 2678400, 5356800, 16070400, 31536000`. |
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`caching_level`|String|Optional|The cache level settings. Valid values are `basic`, `simplified`, `aggressive`.|
|`domain_id`|String|Required|The ID of the domain to change cache settings. |
|`development_mode`|String|Optional|The development mode enable or disable settings. Valid values are `on`, and `off`.|
|`purge_all`|Boolean|Optional| Purge all cached files.|
|`purge_by_urls`|List of String|Optional| Purge cached URLs.|
|`purge_by_hosts`|List of String|Optional| Purge cached hosts.|
|`purge_by_tags`|List of String|Optional| Purge cached item that matches the tags.|
|`query_string_sort`|String|Optional|The query string sort settings. Valid values are `on`, and `off`.|

- Among all the purge actions `purge_all`, `purge_by-urls`, `purge_by_hosts`, and `purge_by_tags`, only one is allowed to give inside a resource.
- `serve_stale_content` is not supported yet.
{: note}

### Output parameters
{: #cis-cache-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The record ID. It is a combination of `<domain_id>,<cis_id>` attributes concatenated with `:`.|

### Import
{: #cis-cache-import}

The `ibm_cis_cache_settings` resource can be imported using the ID. The ID is formed from the domain ID of the domain and the CRN concatenated  using a `:` character.

The domain ID and CRN will be located on the overview page of the {{site.data.keyword.cis_full_notm}} instance of the UI domain heading, or by using the `ibmcloud cis` CLI commands.

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**Syntax**

```
terraform import ibm_cis_cache_settings.cache_settings <domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_cache_settings.cache_settings 9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_certificate_order`
{: #cis-certificate-order}

 Provides an {{site.data.keyword.cis_full_notm}} certificate order resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS domain resource. It allows to order and delete dedicated certificates of a domain of a CIS instance. For more information about CIS certificate order, refer to [managing origin certificates](/docs/cis?topic=cis-cis-origin-certificates).
 {: shortdesc}

 ### Sample Terraform code
{: #cis-certificate-order-sample}

```
resource "ibm_cis_certificate_order" "test" {
	cis_id    = data.ibm_cis.cis.id
	domain_id = data.ibm_cis_domain.cis_domain.domain_id
	hosts     = ["example.com"]
}
```
{: codeblock}

### Input parameters
{: #cis-certificate-order-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the domain. |
|`hosts`|String|Required|The hosts for the certificates to be ordered.|


### Output parameters
{: #cis-certificate-order-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The record ID. It is a combination of `<certificate_id>,<domain_id>,<cis_id>` attributes concatenated with `:`.|
|`certificate_id`|String |The certificate ID.|
|`status`|String |The certificate status.|

### Import
{: #cis-certificate-order-import}

The `ibm_cis_certificate_order` resource can be imported using the ID. The ID is formed from the certificate ID, the domain ID of the domain and the CRN  Concatenated  by using a `:` character.

The domain ID and CRN is located on the **Overview** page of the {{site.data.keyword.cis_full_notm}} instance of the UI domain heading, or by using the `ibmcloud cis` CLI commands.

**Domain ID** is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

**CRN** is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**Certificate ID** is a 32 digit character string of the form: `489d96f0da6ed76251b475971b097205c`.


**Syntax**

```
terraform import ibm_cis_certificate_order.myorg <certificate_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_certificate_order.myorg certificate_order 48996f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}


## `ibm_cis_certificate_upload`
{: #cis-certificate-upload}

 Provides an {{site.data.keyword.cis_full_notm}} certificate upload resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS domain resource. It allows to upload, update, and delete certificates of a domain of a CIS instance. For more information about CIS certificate upload, refer to [Installing an origin certificate on your server](/docs/cis?topic=cis-cis-origin-certificates#cis-origin-certificates-installing).
 {: shortdesc}

 ### Sample Terraform code
{: #cis-certificate-upload-sample}

```
# Upload a certificate for a domain

resource "ibm_cis_certificate_upload" "cert" {
    cis_id        = data.ibm_cis.cis.id
    domain_id     = data.ibm_cis_domain.cis_domain.domain_id
    certificate   = "xxxxx"
    private_key   = "xxxxx
    bundle_method = "ubiquitous"
    priority      = 20
}
```
{: codeblock}

### Input parameters
{: #cis-certificate-upload-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the domain to add the rules certificate upload. |
|`certificate`|String|Required| The intermediate(s) certificate key.|
|`private_key`|String|Required| The certificate private key.|
|`bundle_method`|String|Optional| The certificate bundle method. The valid values are `ubiquitous`, `optimal`, `force`.|
|`priority`|Integer|Optional | The order or priority in which the certificate is used in a request.|

### Output parameters
{: #cis-certificate-upload-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The record ID. It is a combination of `<custom_cert_id>:<domain_id>:<cis_id>` attributes concatenated with `:`.|
|`certificate_id`|String |The certificate ID.|
|`status`|String |The certificate status.|
|`custom_cert_id`|String|The certificate upload rule ID.|
|`status`|String|The certificate status.|
|`issuer`|String|The certificate issuer.|
|`signature`|String| The certificate signature.|
|`expires_on`|String| The expiry date and time of the certificate.|
|`uploaded_on`|String| The uploaded date and time of the certificate.|
|`modified_on`|String| The modified date and time of the certificate.|

### Import
{: #cis-certificate-upload-import}

The `ibm_cis_certificate_upload` resource can be imported using the ID. The ID is formed from the certificate upload ID, the domain ID of the domain and the CRN  Concatenated  by using a `:` character.

The domain ID and CRN is located on the **Overview** page of the {{site.data.keyword.cis_full_notm}} instance of the UI domain heading, or by using the `ibmcloud cis` CLI commands.

**Domain ID** is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

**CRN** is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**Certificate upload ID** is a 32 digit character string of the form: `489d96f0da6ed76251b475971b097205c`.


**Syntax**

```
terraform import ibm_cis_certificate_upload.ratelimit <custm_cert_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_certificate_upload.certificate 48996f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_custom_page`
{: #cis-custom}

 Provides an {{site.data.keyword.cis_full_notm}} custom page resource that is associated with an IBM CIS instance and a CIS domain resource. It allows to create, update, and delete a custom page of a domain of a CIS instance. For more information about custom page, refer to [CIS custom page](/docs/cis?topic=cis-custom-page).
 {: shortdesc}

### Sample Terraform code
{: #cis-custom-sample}

```
# Change Custom Page of the domain

resource "ibm_cis_custom_page" "custom_page" {
	cis_id    = data.ibm_cis.cis.id
	domain_id = data.ibm_cis_domain.cis_domain.domain_id
	page_id   = "basic_challenge"
	url       = "https://test.com/index.html"
}
```
{: codeblock}

### Input parameters
{: #cis-custom-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the domain to change custom page. |
|`page_id`|String|Required|The custom page identifier. Valid values are `basic_challenge`, `waf_challenge`, `waf_block`, `ratelimit_block`, `country_challenge`, `ip_block`, `under_attack`, `500_errors`, `1000_errors`, `always_online`.|
|`url`|String|Required| The URL for custom page settings. By default URL is set with empty string `""`. Setting a duplicate empty string throws an error.|

### Output parameters
{: #cis-custom-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

The following attributes are exported:

|Name|Data type|Description|
|----|-----------|--------|
|`created_on`|String|Created date and time of the custom page.|
|`description`|String|The description of the custom page.|
|`id`|String|The record ID. It is a combination of `<domain_id>,<cis_id>` attributes concatenated with `:`.|
|`modified_on`|String|Modified date and time of the custom page.|
|`preview_target`|String|The custom page target.|
|`required_tokens`|List|The custom page required token which is expected from URL page. |
|`state`|String|The custom page state. This is set default when there is an empty URL and can customize when URL is set with some URL.|

### Import
{: #cis-custom-import}

The `ibm_cis_custom_page` resource can be imported using the ID. The ID is formed from the page_id, domain ID of the domain and the CRN concatenated  using a `:` character.

The domain ID and CRN will be located on the overview page of the {{site.data.keyword.cis_full_notm}} instance of the UI domain heading, or by using the `ibmcloud cis` CLI commands.

Page ID is a string of the form: `basic_challenge`

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**Syntax**

```
terraform import ibm_cis_custom_page.custom_page <page_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_custom_page.custom_page basic_challenge:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_dns_records_import`
{: #cis-dns-records-import}

Provides an {{site.data.keyword.cis_full_notm}} DNS records import resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS domain resource. It allows to import DNS records from file of a domain of a CIS instance. For more information, about CIS DNS records, refer to [managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records).
{: shortdesc}

### Sample Terraform code
{: #cis-dns-records-import-sample}

```
# Import DNS Records of the domain

resource "ibm_cis_dns_records_import" "test" {
	cis_id    = data.ibm_cis.cis.id
	domain_id = data.ibm_cis_domain.cis_domain.domain_id
	file      = "dns_records.txt"
}
```
{: codeblock}

### Input parameters
{: #cis-dns-records-import-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description| Forces new resource |
|----|-----------|-----------|---------------------| ------- |
|`domain_id`|String|Required|The ID of the domain to import the DNS records. | No |
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.| No |
|`file`|String|Required| The DNS zone file that contains the details of the DNS records.| Yes |


### Output parameters
{: #cis-dns-records-import-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The record ID. It is a combination of `<total_records_parsed>:<records_added>:<file>:<domain_id>:<cis_id>` attributes concatenated with `:`.|
|`total_records_parsed`|Integer|The parsed records count from imported file.|
|`records_added`|String|The added records count from imported file.|


### Import
{: #cis-dns-records-imports}

The `ibm_cis_dns_records_import` resource can be imported by using the ID. The ID is formed from the zone file, the domain ID of the domain and the CRN (Cloud Resource Name)  Concatenated  using a `:` character with the prefix of `0:0:`.

The domain ID and CRN is located on the **Overview** page of the internet services instance under the domain heading of the UI, or via by using the `ibmcloud cis` CLI commands.

**File** is a string of the form: `records.txt`

**Domain ID** is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

**CRN** is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

```
terraform import ibm_cis_dns_records_import.myorgs <total_records_parsed>:<records_added>:<file>:<domain-id>:<crn>
```
{: pre}

```
terraform import ibm_cis_dns_records_import.myorgs 0:0:records.txt:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_domain`
{: #cis-domain}

Create, update, or delete an {{site.data.keyword.cis_full_notm}} domain.
{: shortdesc}

### Sample Terraform code
{: #cis-domain-sample}

```
resource "ibm_cis_domain" "example" {
  domain = "example.com"
  cis_id = ibm_cis.instance.id
}

resource "ibm_cis" "instance" {
  name = "test-domain"
  plan = "standard"
}
```
{: codeblock}

### Input parameters
{: #cis-domain-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`domain`|String|Required|The DNS domain name that you want to add to your {{site.data.keyword.cis_full_notm}} instance. |
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|


### Output parameters
{: #cis-domain-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The unique identifier of the domain.|
|`paused`|Boolean|Indicates if the domain is paused and network traffic bypasses your {{site.data.keyword.cis_full_notm}} instance. The default values is **false**.|
|`status`|String|The status of the domain. Valid values are `active`, `pending`, `initializing`, `moved`, `deleted`, and `deactivated`. After creation, the status remains pending until the DNS Registrar is updated with the CIS name servers, exported in the `name_servers` variable.|
|`name_servers`|String|The name servers that are assigned to your {{site.data.keyword.cis_full_notm}} instance. |
|`original_name_servers`|String|The name servers that were used when the domain was first registered with the DNS Registrar. |


### Import
{: #cis-domain-import}

The {{site.data.keyword.cis_full_notm}} domain can be imported by using the domain ID and service instance CRN. The ID is formed from the Domain ID of the domain concatenated by using a `:` character with the CRN (Cloud Resource Name).
The Domain ID and CRN will be located on the **Overview** page of the Internet Services instance under the Domain heading of the UI, or via the `ibmcloud cis` CLI commands.
The domain ID is a 32 digit character string in the format `1aaa11111aa1a1a1111aaa111111a11a`. CRN is a 120 digit character string of the format `crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::`.

```
terraform import ibm_cis_domain.myorg <domain-id>:<crn>
```
{: pre}

```
terraform import ibm_cis_domain.myorg 1aaa11111aa1a1a1111aaa111111a11a:crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::
```
{: pre}


## `ibm_cis_domain_settings`
{: #cis-domain-settings}

Customize the {{site.data.keyword.cis_full_notm}} domain settings.
{: shortdesc}

### Sample Terraform code
{: #cis-domain-settings-sample}

```
resource "ibm_cis_domain_settings" "test" {
  cis_id          = ibm_cis.instance.id
  domain_id       = ibm_cis_domain.example.id
  waf             = "on"
  ssl             = "full"
  min_tls_version = "1.2"
}
```
{: codeblock}

```
resource "ibm_cis_domain_settings" "test_domain_settings" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  dnssec                      = "disabled"
  waf                         = "off"
  ssl                         = "flexible"
  min_tls_version             = "1.2"
  cname_flattening            = "flatten_all"
  opportunistic_encryption    = "off"
  automatic_https_rewrites    = "on"
  always_use_https            = "off"
  ipv6                        = "off"
  browser_check               = "off"
  hotlink_protection          = "off"
  http2                       = "on"
  image_load_optimization     = "off"
  image_size_optimization     = "lossless"
  ip_geolocation              = "off"
  origin_error_page_pass_thru = "off"
  brotli                      = "off"
  pseudo_ipv4                 = "off"
  prefetch_preload            = "off"
  response_buffering          = "off"
  script_load_optimization    = "off"
  server_side_exclude         = "off"
  tls_client_auth             = "off"
  true_client_ip_header       = "off"
  websockets                  = "off"
  challenge_ttl               = 31536000
  max_upload                  = 300
  cipher                      = ["AES128-SHA256"]
  minify {
    css  = "off"
    js   = "off"
    html = "off"
  }
  security_header {
    enabled            = false
    include_subdomains = false
    max_age            = 0
    nosniff            = false
  }
  mobile_redirect {
    status           = "on"
    mobile_subdomain = "m.domain.com"
    strip_uri        = true
  }
}
```
{: codeblock}

### Input parameters
{: #cis-domain-settings-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`always_use_https`|String|Optional|Supported values are `off` and `on`.|
|`automatic_https_rewrites`|String|Optional|Enable HTTPS rewrites. Allowed values are `off` and `on`. |
|`browser_check`|String|Optional|Enable a client browser check to look for common HTTP headers that are used by malicious users. If HTTP headers are found,  access to your website is blocked. Supported values are `off` and `on`.|
|`brotli`|String|Optional|Supported values are `off` and `on`.|
|`challenge_ttl`|String|Optional|Challenge TTL values are `300`, `900`, `1800`, `2700`, `3600`, `7200`, `10800`, `14400`, `28800`, `57600`, `86400`, `604800`, `2592000`, and `31536000`.|
|`cipher`|String|Optional|Cipher setting values are  `ECDHE-ECDSA-AES128-GCM-SHA256`, `ECDHE-ECDSA-CHACHA20-POLY1305`,`ECDHE-RSA-AES128-GCM-SHA256`, `ECDHE-RSA-CHACHA20-POLY1305`, `ECDHE-ECDSA-AES128-SHA256`, `ECDHE-ECDSA-AES128-SHA`, `ECDHE-RSA-AES128-SHA256`, `ECDHE-RSA-AES128-SHA`, `AES128-GCM-SHA256`, `AES128-SHA256`, `AES128-SHA`, `ECDHE-ECDSA-AES256-GCM-SHA384`, `ECDHE-ECDSA-AES256-SHA384`, `ECDHE-RSA-AES256-GCM-SHA384`, `ECDHE-RSA-AES256-SHA384`, `ECDHE-RSA-AES256-SHA`, `AES256-GCM-SHA384`, `AES256-SHA256`, `AES256-SHA`, `DES-CBC3-SHA`.|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`cname_flattening`|String|Optional|Supported values are `flatten_at_root`, `flatten_all`, and `flatten_none`.|
|`domain_id`|String|Required|The ID of the domain that you want to customize. |
|`dnssec`|String|Optional|Can set to `active` only once. Allowed values are `active`, `disabled`.|
|`hotlink_protection`|String|Optional|Supported values are `off` and `on`.|
|`http2`|String|Optional|Supported values are `off` and `on`.|
|`image_load_optimization`|String|Optional|Supported values are `off` and `on`.|
|`image_size_optimization`|String|Optional|Supported values are `lossless`,  `off`, and `lossy`.|
|`ipv6`|String|Optional|Supported values are `off` and `on`.|
|`ip_geolocation`|String|Optional|Supported values are `off` and `on`.|
|`max_upload`|String|Optional|Maximum upload values are `100`, `125`, `150`, `175`, `200`, `225`, `250`, `275`, `300`, `325`, `350`, `375`, `400`, `425`, `450`, `475`, and `500`.|
|`min_tls_version`|String|Optional|The minimum TLS version that you want to allow. Allowed values are `1.1`, `1.2`, or `1.3`. |
|`minify`|List|Optional|Minify the setting as stated.|
|`minify.css`|String|Required|CSS supported values are `on` and `off`.|
|`minify.html`|String|Required|HTML supported values are `on` and `off`.|
|`minify.js`|String|Required|JS supported values are `on` and `off`.|
|`mobile_redirect`|List|Optional|Mobile redirect setting. |
|`mobile_redirect.status`|Boolean|Required|Mobile redirect setting status values are `true` and `false`. |
|`mobile_redirect.mobile_subdomain`|String|Optional|Mobile redirect subdomain. For example `m.domain.com` |
|`mobile_redirect.strip_uri`|Boolean|Optional|Strip URI for mobile redirect. |
|`origin_error_page_pass_thru`|String|Optional|Supported values are `off` and `on`.|
|`opportunistic_encryption`|String|Optional|Supported values are `off` and `on`.|
|`pseudo_ipv4`|String|Optional|Supported values are `overwrite_header`, `off`, and `add_header`.|
|`prefetch_preload`|String|Optional|Supported values are `off` and `on`.|
|`response_buffering`|String|Optional|Supported values are `off` and `on`.|
|`script_load_optimization`|String|Optional|Supported values are `off` and `on`.|
|`server_side_exclude`|String|Optional|Supported values are `off` and `on`.|
|`security_header`|List|Optional|Security headers as stated.|
|`security_header.enabled`|Boolean|Required|Supported values are `true` and `false`. |
|`security_header.include_subdomains`|Boolean|Required|Supported values are `true` and `false`. |
|`security_header.max_age`|Integer|Required|Maximum age of the security header. |
|`security_header.nosniff`|Boolean|Required|No sniff.|
|`ssl`|String|Optional|Allowed values: `off`, `flexible`, `full`, `strict`, `origin_pull`.|
|`tls_client_auth`|String|Optional|Supported values are `off` and `on`.|
|`true_client_ip_header`|String|Optional|Supported values are `off` and `on`.|
|`waf`|String|Optional|Enable a web application firewall (WAF). Supported values are `off` and `on`.|
|`websockets`|String|Optional|Supported values are `off` and `on`.|

 Extra settings are not implemented in this version of the provider.
 {: note}

### Output parameters
{: #cis-domain-settings-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`certificate_status`|String| Value of: `none`, `initializing`, `authorizing`, or `active`.|





## `ibm_cis_dns_record`
{: #cis-dns-record}

Create, update, or delete an {{site.data.keyword.cis_full_notm}} DNS record resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS domain resource. For more information, about CIS DNS record, refer to [managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records).
{: shortdesc}

### Sample Terraform code
{: #cis-dns-record-sample}

**Example Usage 1** Create a record.

```
# Add a DNS record to the domain
resource "ibm_cis_dns_record" "example" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
  name      = "terraform"
  content   = "192.168.0.11"
  type      = "A"
}
```
{: codeblock}

**Example Usage 1** Create `A` record.

```
resource "ibm_cis_dns_record" "test_dns_a_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple"
  type    = "A"
  content = "1.2.3.4"
  ttl     = 900
}

output "a_record_output" {
  value = ibm_cis_dns_record.test_dns_a_record
}
```

**Example Usage 2** Create `AAAA` record.

```
resource "ibm_cis_dns_record" "test_dns_aaaa_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple.aaaa"
  type    = "AAAA"
  content = "2001::4"
  ttl     = 900
}

output "aaaa_record_output" {
  value = ibm_cis_dns_record.test_dns_aaaa_record
}
```

**Example Usage 3** Create `CNAME` record.

```
resource "ibm_cis_dns_record" "test_dns_cname_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple.cname.com"
  type    = "CNAME"
  content = "domain.com"
  ttl     = 900
}

output "cname_record_output" {
  value = ibm_cis_dns_record.test_dns_cname_record
}
```
**Example Usage 4** Create `MX` record.

```
resource "ibm_cis_dns_record" "test_dns_mx_record" {
  cis_id   = var.cis_crn
  domain_id  = var.zone_id
  name     = "test-exmple.mx"
  type     = "MX"
  content  = "domain.com"
  ttl      = 900
  priority = 5
}

output "mx_record_output" {
  value = ibm_cis_dns_record.test_dns_mx_record
}
```

**Example Usage 5** Create `LOC` record.

```
resource "ibm_cis_dns_record" "test_dns_loc_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple.loc"
  type    = "LOC"
  ttl     = 900
  data = {
    altitude       = 98
    lat_degrees    = 60
    lat_direction  = "N"
    lat_minutes    = 53
    lat_seconds    = 53
    long_degrees   = 45
    long_direction = "E"
    long_minutes   = 34
    long_seconds   = 34
    precision_horz = 56
    precision_vert = 64
    size           = 68
  }
}

output "loc_record_output" {
  value = ibm_cis_dns_record.test_dns_loc_record
}
```

**Example Usage 6** Create `CAA` record.

```
resource "ibm_cis_dns_record" "test_dns_caa_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple.caa"
  type    = "CAA"
  ttl     = 900
  data = {
    tag   = "http"
    value = "domain.com"
  }
}

output "caa_record_output" {
  value = ibm_cis_dns_record.test_dns_caa_record
}
```
**Example Usage 7** Create `SRV` record.

```
resource "ibm_cis_dns_record" "test_dns_srv_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  type = "SRV"
  ttl  = 900
  data = {
    name     = "test-example.srv"
    port     = 1
    priority = 1
    proto    = "_udp"
    service  = "_sip"
    target   = "domain.com"
    weight   = 1
  }
}

output "srv_record_output" {
  value = ibm_cis_dns_record.test_dns_srv_record
}
```
**Example Usage 8** Create `SPF` record.

```
resource "ibm_cis_dns_record" "test_dns_spf_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple.spf"
  type    = "SPF"
  content = "test"
}

output "spf_record_output" {
  value = ibm_cis_dns_record.test_dns_spf_record
}
```

**Example Usage 9** Create `TXT` record.

```
resource "ibm_cis_dns_record" "test_dns_txt_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple.txt"
  type    = "TXT"
  content = "test"
}

output "txt_record_output" {
  value = ibm_cis_dns_record.test_dns_txt_record
}
```

**Example Usage 10** Create `NS` record.

```
resource "ibm_cis_dns_record" "test_dns_ns_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  name    = "test-exmple.ns"
  type    = "NS"
  content = "ns1.name.ibm.com"
}

output "ns_record_output" {
  value = ibm_cis_dns_record.test_dns_ns_record
}

output "caa_record_output" {
  value = ibm_cis_dns_record.test_dns_caa_record
}

## Example Usage 7 : Create SRV record

```hcl
resource "ibm_cis_dns_record" "test_dns_srv_record" {
  cis_id  = var.cis_crn
  domain_id = var.zone_id
  type = "SRV"
  ttl  = 900
  data = {
    name     = "test-example.srv"
    port     = 1
    priority = 1
    proto    = "_udp"
    service  = "_sip"
    target   = "domain.com"
    weight   = 1
  }
}

output "srv_record_output" {
  value = ibm_cis_dns_record.test_dns_srv_record
}
```

### Input parameters
{: #cis-dns-record-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`domain_id`|String|Required|The ID of the domain to add a DNS record. It can be a combination of `<domain_id>:<cis_id> or <domain_id>`. |
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`name`|String|Required|The name of the DNS record.|
|`type`|String|Required|The type of the DNS record to be created. Allowed values are `A`, `AAAA`, `CNAME`, `NS`, `MX`, `TXT`, `LOC`, `SRV`, `SPF`, or `CAA`. |
|`content`|String|Optional|The value of the record. For example, `192.168.127.127`. You need to provide this or data to be specified.|
|`priority`|String|Optional|The priority of the record. Mandatory field for `SRV` record type.|
|`proxied`|Boolean|Optional|Indicates if the record receives origin protection by {{site.data.keyword.cis_full_notm}}. The default value is **false**.|
|`ttl`|Integer|Optional|The time to live `(TTL)` record. The automatic is `ttl=1`. if the record is proxied. Terraform provider takes `TTL` in unit seconds. Therefore, it starts with value 120. |
|`data`|Map|Optional|A map of attributes that constitute the record value. This value is required for `LOC`, `CAA` and `SRV` record types. |
|`data.weight`|Integer|Optional|The weight of distributing queries among multiple target servers. Mandatory field for `SRV` record type. |
|`data.port`|Integer|Optional|The port number of the target server. Mandatory field for `SRV` record type.|
|`data.service`|Integer|Optional|The symbolic name of the required service, start with an underscore `_`. Mandatory field for `SRV` record type. |
|`data.protocol`|Integer|Optional|The symbolic name of the required protocol. Mandatory field for `SRV` record type. |
|`data.altitude`|Integer|Optional|The `LOC` altitude. Mandatory field for `LOC` record type. |
|`data.size`|Integer|Optional|The `LOC` altitude size. Mandatory field for `LOC` record type. |
|`data.lat_degrees`|Integer|Optional|The `LOC` latitude degrees. Mandatory field for `LOC` record type. |
|`data.lat_direction`|String|Optional|The `LOC` latitude direction `N`, `E`, `S`, `W`. Mandatory field for `LOC` record type. |
|`data.lat_minutes`|Integer|Optional|The `LOC` latitude minutes. Mandatory field for `LOC` record type. |
|`data.lat_seconds`|Integer|Optional|The `LOC` latitude seconds. Mandatory field for `LOC` record type. |
|`data.long_degrees`|Integer|Optional|The `LOC` longitude degrees. Mandatory field for `LOC` record type. |
|`data.long_direction`|String|Optional|The `LOC` longitude direction `N`, `E`, `S`, `W`. Mandatory field for `LOC` record type. |
|`data.long_minutes`|Integer|Optional|The `LOC` longitude minutes. Mandatory field for `LOC` record type. |
|`data.long_seconds`|Integer|Optional|The `LOC` longitude seconds. Mandatory field for `LOC` record type. |
|`data.precision_horz`|Integer|Optional|The `LOC` horizontal precision. Mandatory field for `LOC` record type. |
|`data.precision_vert`|Integer|Optional|The `LOC` vertical precision. Mandatory field for `LOC` record type. |
|`data.priority`|Integer|Optional|The priority of the record. |
|`proxied`|Bool|Optional|Indicates the record gets CIS's origin protection. Default is `false`. |

### Output parameters
{: #cis-dns-record-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The ID of the record, zone and CRN with `:` separator . |
|`name`|String| The name of the DNS record. |
|`proxiable`|Bool|Indicates if the record can be proxied. |
|`proxied`|Bool|Indicates the record gets CIS's origin protection. Default is `false`. |
|`record_id`|String|The DNS record ID.|
|`created_on`|String|The created date of the DNS record. |
|`modified_on`|String|The modified date of the DNS record. |
|`zone_name`|String|The DNS zone name.|

### Import
{: #cis-dns-record-import}

The `ibm_cis_dns_record` resource can be imported by using the ID. The ID is formed from the DNS record ID, the domain ID, and the CRN (Cloud Resource Name). All values are  Concatenated  by using a `:` character. 

The domain ID and CRN are located on the **Overview** page of the internet services instance in the **Domain** heading of the UI, or via using the `ibmcloud cis` CLI commands.

**Domain ID** is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

**CRN** is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**DNS Record ID** is a 32 digit character string of the form: `489d96f0da6ed76251b475971b097205c`. The ID of an existing DNS record is not available via the UI. You can retrieve programmatically via the CIS API or via the CLI using the CIS command `ibmcloud cis dns-records <domain_id>` to list the defined DNS records.


```
terraform import ibm_cis_dns_record.myorg <dns_record_id>:<domain-id>:<crn>
```
{: pre}

```
terraform import ibm_cis_dns_record.myorg  48996f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}





## `ibm_cis_edge_functions_action`
{: #cis-edge-functions-action}

Create, update, or delete an edge functions action for a domain to include in your CIS edge functions action resource.
{: shortdesc}

### Sample Terraform code
{: #cis-edge-functions-action-sample}

The example to add an edge functions action to the domain.

```
# Add a Edge Functions Action to the domain
resource "ibm_cis_edge_functions_action" "test_action" {
  cis_id      = data.ibm_cis.cis.id
  domain_id   = data.ibm_cis_domain.cis_domain.domain_id
  action_name = "sample-script"
  script      = file("./script.js")
}
```
{: codeblock}

### Input parameters
{: #cis-edge-functions-action-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`action_name`|String|Required|The action name of an edge functions action.|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the domain to add the edge functions action.|
|`script`|String|Required|The script of an edge functions action.|


### Output parameters
{: #cis-edge-functions-action-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The action ID with a combination of `<action_name>`,`<domain_id>`,`<cis_id>` attributes concatenate with colon (`:`).|

### Import
{: #cis-edge-functions-action-import}

The `ibm_cis_edge_functions_action` resource can be imported by using the ID. The ID is composed from an edge functions action name or script name, the domain ID of the domain and the CRN (Cloud Resource Name) is concatenated with colon (`:`).
{: shortdesc}

The domain ID and CRN are located on the overview page of the Internet Services instance in the domain heading of the UI, or by using the {{site.data.keyword.cloud_notm}} CIS CLI commands.
Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`.
CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`.
Edge functions action name or script name is a string: `sample_script`.
{: note}

**Syntax**

```
terraform import ibm_cis_edge_functions_action.test_action <action_name>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_edge_functions_action.test_action sample_script:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_edge_functions_trigger`
{: #cis-edge-functions-trigger}

Create, update, or delete an edge functions trigger for a domain to include in your CIS edge functions trigger resource.
{: shortdesc}

### Sample Terraform code
{: #cis-edge-functions-trigger-sample}

The example to add an edge functions trigger to the domain.

```
# Add a Edge Functions Trigger to the domain
resource "ibm_cis_edge_functions_trigger" "test_trigger" {
  cis_id      = ibm_cis_edge_functions_action.test_action.cis_id
  domain_id   = ibm_cis_edge_functions_action.test_action.domain_id
  action_name = ibm_cis_edge_functions_action.test_action.action_name
  pattern_url = "example.com/*"
}
```
{: codeblock}

### Input parameters
{: #cis-edge-functions-trigger-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`action_name`|String|Optional|An action name of the edge functions action on which the trigger associates. If it is not specified, then the trigger will be disabled.|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the domain to add the edge functions trigger.|
|`pattern_url`|String|Required|The domain name pattern on which the edge function action trigger should be executed.|

### Output parameters
{: #cis-edge-functions-trigger-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`action_name`|String|An edge functions action Script name.|
|`id`|String|The action ID with a combination of `<trigger_id>`,`<domain_id>`,`<cis_id>` attributes concatenate with colon (`:`).|
|`pattern_url`|String|The Route pattern. It is a domain name on which the action is performed.|
|`request_limit_fail_open`|String|An action request limit fail open.|
|`trigger_id`|String|The route ID of an action trigger.|

### Import
{: #cis-edge-functions-trigger-import}

The `ibm_cis_edge_functions_trigger` resource can be imported by using the ID. The ID is composed from an edge functions trigger route ID, the domain ID of the domain and the CRN (Cloud Resource Name) is concatenated with colon (`:`).
{: shortdesc}

The domain ID and CRN are located on the overview page of the Internet Services instance in the domain heading of the UI, or by using the {{site.data.keyword.cloud_notm}} CIS CLI commands.
Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`.
CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`.
Edge functions trigger route ID is a 32 digit character string of the form: `48996f0da6ed76251b475971b097205c`.
{: note}

**Syntax**

```
terraform import ibm_cis_edge_functions_trigger.test_trigger <trigger_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_edge_functions_trigger.test_trigger 48996f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:ibmcloud:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_firewall`
{: #cis-firewall}

Create, update, or delete a firewall for a domain that you included in your {{site.data.keyword.cis_full_notm}} instance. For more information, see [firewall rule actions](/docs/cis?topic=cis-actions).
{: shortdesc}

### Sample Terraform code
{: #cis-firewall-sample}

```
resource "ibm_cis_firewall" "lockdown" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
  firewall_type = "lockdowns"
  lockdown {
    paused      = "false"
    description = "test"
    urls = ["www.cis-terraform.com"]
    configurations {
      target = "ip"
      value  = "127.0.0.2"
    }
    priority=1
  }
}

resource "ibm_cis_firewall" "access_rules" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
  firewall_type = "access_rules"
  access_rule {
    mode  = "block"
    notes = "access rule notes"
    configuration {
      target = "asn"
      value  = "AS12346"
    }
  }
}

resource "ibm_cis_firewall" "ua_rules" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
  firewall_type = "ua_rules"
  ua_rule {
    mode = "challenge"
    configuration {
      target = "ua"
      value  = "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/603.2.4 (KHTML, like Gecko) Version/10.1.1 Safari/603.2.4"
    }
  }
}
```
{: codeblock}

### Input parameters
{: #cis-firewall-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance where you want to create the firewall.|
|`domain_id`|String|Required|The ID of the domain where you want to apply the firewall rules.|
|`firewall_type`|String|Required|The type of firewall that you want to create for your domain. Supported values are `lockdowns`, `access_rules`, and `ua_rules`. Consider the following information when choosing your firewall type: <ul><li><strong><code>access_rules</code></strong>: Access rules allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.</li><li><strong><code>ua_rules</code></strong>: Apply firewall rules only if the user agent that is used by the client matches the user agent that you defined. </li><li><strong><code>lockdowns</code></strong>: Allow access to your domain for specific IP addresses or IP address ranges only. If you choose this firewall type, you must define your firewall rules in the `lockdown` input parameter.</li></ul>|
|`lockdown`|List of firewall rules|Required for `lockdowns` firewall| A list of firewall rules that you want to create for your `lockdowns` firewall. You can specify one item in this list only.|
|`lockdown.paused`|Boolean|Required|If set to **true**, the firewall rule is disabled. If set to **false**, the firewall rule is enabled.|
|`lockdown.description`|String|Optional|A description for your firewall rule.|
|`lockdown.priority`|Integer|Optional|The priority of the firewall rule. A low number is associated with a high priority. |
|`lockdown.urls`|List of URLs|Required|A list of URLs that you want to include in your firewall rule. You can specify wildcard URLs. The URL pattern is escaped before use.|
|`lockdown.configurations`|List of IP addresses|Required|A list of IP address or CIDR ranges that you want to allow access to the URLs that you defined in `lockdown.urls`. |
|`lockdown.configurations.target`|String|Optional|Specify if you want to target an `IP` or `ip_range`.|
|`lockdown.configurations.value`|String|Optional|The IP address or IP address range that you want to target. Make sure that the value that you enter here matches the type of target that you specified in `lockdown.configurations.target`. |
|`access_rule`|String|Optional| Create the data the describing access rule. (Maximum item is 1) |
|`access_rule.notes`|String|Optional| The free text for notes. |
|`access_rule.mode`|String|Required| The mode of access rule. The valid modes are `block`, `challenge`, `whitelist`, `js_challenge`.|
|`access_rule.configuration`|List|Required| The Configuration of firewall. (Maximum items is 1) |
|`access_rule.configuration.target`|String|Required| The request property to target. Valid values are `ip`, `ip_range`, `asn`, `country`. |
|`access_rule.configuration.value`|String|Required| IP address or CIDR or Autonomous or Country code. |
|`ua_rule`|String|Optional|Create the data describing the user agent rule. (Maximum item is 1) |
|`ua_rule.description `|String|Optional|The free text for description. |
|`ua_rule.mode`|String|Optional|The mode of access rule. The valid modes are `block`, `challenge`,  `js_challenge`. |
|`ua_rule.paused`|String|Optional|Whether the rule is currently disabled. |
|`ua_rule.configuration`|List|Required| The Configuration of firewall. (Maximum items is 1) |
|`ua_rule.configuration.target`|String|Required| The request property to target. Valid values are `ua`. |
|`ua_rule.configuration.value`|String|Required|  The exact User Agent string to match the rule. |


Exactly one of `lockdown`, `access_rule`, and `ua_rule` is allowed for the firewall types `lockdowns`, `access_rules`, and `ua_rules`.
{: note}

### Output parameters
{: #cis-firewall-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the record. The ID is composed of `<firewall_type>,<lockdown_id/access_rule_id/ua_rule_id>,<domain_ID>,<cis_crn>`. Attributes are concatenated with `:`.|
|`lockdown_id`|String|The lock down ID.|
|`access_rule_id`|String|The access rule ID.|
|`ua_rule_id`|String|The user agent rule ID.|

### Import
{: #cis-firewall-import}

The `ibm_cis_firewall` resource is imported by using the ID. The ID is formed from the firewall type, the firewall ID, the domain ID of the domain and the CRN (Cloud Resource Name) concatenated  using a `:` character.

The domain ID and CRN is located on the Overview page of the internet services instance of the domain heading of the UI, or by using the `ibm cis` CLI commands.

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`.

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`.

Firewall ID is a 32 digit character string of the form: `489d96f0da6ed76251b475971b097205c`.

Firewall type is a string. It can be either of `lockdowns`, `access_rules`, `ua_rules`.

**Syntax**

```
terraform import ibm_cis_firewall.myorg <firewall_type>:<firewall_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_firewall.myorg lockdowns lockdowns:48996f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}


## `ibm_cis_global_load_balancer`
{: #cis-global-lb}

Create, update, or delete a global load balancer. 
{: shortdesc}

The IBM Cloud Terraform Provider plug-in does not support the setup of a region pool for a global load balancer. 
{: note}

### Sample Terraform code
{: #cis-global-lb-sample}

```
# Define a global load balancer which directs traffic to defined origin pools
# In normal usage different pools would be set for data centers/availability zones and/or for different regions
# Within each availability zone or region we can define multiple pools in failover order

resource "ibm_cis_global_load_balancer" "example" {
  cis_id           = ibm_cis.instance.id
  domain_id        = ibm_cis_domain.example.id
  name             = "www.example.com"
  fallback_pool_id = ibm_cis_origin_pool.example.id
  default_pool_ids = [ibm_cis_origin_pool.example.id]
  description      = "example load balancer using geo-balancing"
  proxied          = true
}

resource "ibm_cis_origin_pool" "example" {
  cis_id = ibm_cis.instance.id
  name   = "example-lb-pool"
  origins {
    name    = "example-1"
    address = "192.0.2.1"
    enabled = false
  }
}
```
{: codeblock}

### Input parameters
{: #cis-global-lb-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`domain_id`|String|Required|The ID of the domain for which you want to add a global load balancer. |
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`name`|String|Required|The DNS name to associate with the load balancer. This value can be a hostname, like `www`, or the fully qualified domain name, such as `www.example.com`. `example.com` is also accepted.|
|`fallback_pool_id`|String|Required|The ID of the pool to use when all other pools are considered unhealthy. |
|`default_pools_ids`|String|Required|A list of pool IDs that are ordered by their failover priority. |
|`description`|String|Optional|A description of the global load balancer. |
|`enabled`|Boolean|Optional|If set to **true**, the load balancer is enabled and can receive network traffic. If set to **false**, the load balancer is not enabled.|
|`proxied`|Boolean|Optional|Indicates if the host name receives origin protection by {{site.data.keyword.cis_full_notm}}. The default value is **false**.|
|`ttl`|Integer|Optional|The time to live (TTL) in seconds for how long the load balancer must cache a resolved IP address for a DNS entry before the load balancer must look up the IP address again. If your global load balancer is proxied, this value is automatically set and cannot be changed. If your global load balancer is not in proxy, you can enter a value that is 120 or greater. |
|`region_pools`| Set of Strings | Optional | A set of containing mappings of region and country codes to the list of pool of IDs. IDs are ordered by their failover priority.|
|`region_pools.region`| String | Required | Enter a region code. Should not specify the multiple entries with the same region. |
|`region_pools.pool_ids`| String | Required | A list of pool IDs in failover priority for the provided region.|
|`pop_pools`| Set of Strings | Optional | A set of mappings of the IBM Point-of-Presence (PoP) identifiers to the list of pool IDs (ordered by their failover priority) for the PoP (datacenter). This feature is only available to the enterprise customers. |
|`pop_pools.pop`| Strings | Required | Enter a 3-letter code. Should not specify the multiple entries with the same PoP. |
|`pop_pools.pool_ids`| Strings | Required | A list of pool IDs in failover priority to use for the traffic reaching the provided PoP. |


### Output parameters
{: #cis-global-lb-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The ID of the global load balancer. |
|`name`|String| The fully qualified domain name that is associated with the load balancer. |
|`created_on`|String|The RFC3339 timestamp of when the load balancer was created. |
|`modified_on`|String|The RFC3339 timestamp of when the load balancer was last modified. |

### Import
{: #cis-global-lb-import}

The DNS record can be imported by using the `id`. The ID is formed from the global load balancer ID, the domain ID, and the CRN (Cloud Resource Name). All values are concatenated with a `:` character.
The Domain ID and CRN are located on the **Overview** page of the Internet Services instance under the **Domain** heading of the UI, or via the `ibmcloud cis` CLI.

- **Domain ID**: The domain ID is a 32 digit character string of the format `1aaa11111aa1a1a1111aaa111111a11a`.
- **CRN**: The CRN is a 120 digit character string of the format `crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::` 
- **Global load balancer ID**: The global load balancer ID is a 32 digit character string in the format 11a11a1aa1aa11111a111111a111111a. The ID of the load balancer is not available via the UI. It can be retrieved via the CIS API or via the CLI by running `ibmcloud cis glbs <domain_id>`.

```
terraform import ibm_cis_global_load_balancer.myorg <loadbalancer_ID>:<domain_ID>:<crn>
```
{: pre}

```
terraform import ibm_cis_dns_record.myorg  111a11a1aa1aa11111a111111a111111a:1aaa11111aa1a1a1111aaa111111a11a:crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::
```
{: pre}





## `ibm_cis_healthcheck`
{: #cis-health}

Create, update, or delete an HTTPS health check for your {{site.data.keyword.cis_full_notm}} instance. 
{: shortdesc}

### Sample Terraform code
{: #cis-health-sample}

```
resource "ibm_cis_healthcheck" "test" {
  cis_id         = ibm_cis.instance.id
  expected_body  = "alive"
  expected_codes = "2xx"
  method         = "GET"
  timeout        = 7
  path           = "/health"
  interval       = 60
  retries        = 5
  description    = "example load balancer"
}
```
{: codeblock}

### Input parameter
{: #cis-health-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`allow_insecure`|Boolean|Optional|If set to **true**, the certificate is not validated when the health check uses HTTPS. If set to **false**, the certificate is validated, even if the health check uses HTTPS. The default value is **false**.|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`expected_body`|String|Required|A case-insensitive sub-string to look for in the response body. If this string is not found, the origin will be marked as unhealthy. A null value of “” is allowed to match on any content. |
|`expected_codes`|String|Required|The expected HTTP response code or code range of the health check. For example, 200.|
|`follow_redirects`|Boolean|Optional|If set to **true**, a redirect is followed when a redirect is returned by the origin pool. Is set to **false**, redirects from the origin pool are not followed.|
|`method`|String|Optional|The HTTP method to use for the health check. Default: `GET`.|
|`timeout`|Integer|Optional|The timeout in seconds before marking the health check as failed. Default: 5.|
|`path`|String|Optional|The endpoint path to health check against. Default: `/`.|
|`port`|Integer|Optional|The TCP port number that you want to use for the health check.|
|`interval`|Integer|Optional|The interval between each health check. Shorter intervals may improve failover time, but will increase load on the origins as we check from multiple locations. Default: 60.|
|`retries`|Integer|Optional|The number of retries to attempt in case of a timeout before marking the origin as unhealthy. Retries are attempted immediately. Default: 2.|
|`type`|String|Optional|The protocol to use for the health check. Currently supported protocols are `http` and `https`. Default: `http`.
|`description`|String|Optional|A description for your health check. |
|`headers`|String|Optional|The health check headers. |
|`headers.header`|String|Optional|The value of a header. |
|`headers.values`|String|Optional|The list of values for a header field. `[expected_body]`, and `[expected_codes]` are required arguments when the type is `HTTP` or `HTTPS`. **Note** Header is not currently supported in this version of the provider.|

### Output parameter
{: #cis-health-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The ID of the load balancer to monitor. |
|`created_on`|String|The RFC3339 timestamp of when the health check was created. |
|`modified_on`|String|The RFC3339 timestamp of when the health check was last modified. |
|`monitor_id`|String| The load balancer monitor ID.|

### Import
{: #cis-health-import}

The health check can be imported by using the `id`. The ID is formed from the health check ID and the CRN (Cloud Resource Name). All values are concatenated with a `:` character.
The CRN can be located on the **Overview** page of the Internet Services instance under the **Domain** heading of the UI, or via using the `ibmcloud cis` CLI.

- **CRN**: The CRN is a 120 digit character string of the format `crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::` 
- **`Healthcheck ID`**: The health check ID is a 32 digit character string in the format 1aaaa111111aa11111111111a1a11a1. The ID of a health check is not available via the UI. It can be retrieved programmatically via the CIS API or via the CLI by running `ibmcloud cis glb-monitors`.

```
terraform import ibm_cis_healthcheck.myorg <healthcheck_ID>:<crn>
```
{: pre}

```
terraform import ibm_cis_healthcheck.myorg 1aaaa111111aa11111111111a1a11a1:crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::
```
{: pre}





## `ibm_cis_origin_pool`
{: #cis-origin-pool}

Create, update, or delete an origin pool for your {{site.data.keyword.cis_full_notm}} instance.
{: shortdesc}

### Sample Terraform code
{: #cis-origin-pool-sample}

```
resource "ibm_cis_origin_pool" "example" {
  cis_id = ibm_cis.instance.id
  name   = "example-pool"
  origins {
    name    = "example-1"
    address = "192.0.2.1"
    enabled = false
  }
  origins {
    name    = "example-2"
    address = "192.0.2.2"
    enabled = false
  }
  description        = "example load balancer pool"
  enabled            = false
  minimum_origins    = 1
  notification_email = "someone@example.com"
  check_regions      = ["WEU"]
}
```
{: codeblock}

### Input parameter 
{: #cis-origin-pool-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`name`|String|Required|A short name (tag) for the pool. Only alphanumeric characters, hyphens, and underscores are allowed.|
|`origins`|List of origins|Required|A list of origin servers within this pool. Traffic directed to this pool is balanced across all currently healthy origins, provided the pool itself is healthy. |
|`origins.name`|String|Required|The name of the origin server.|
|`origins.address`|String|Required|The IPv4 or IPv6 address of the origin server. You can also provide a hostname for the origin that is publicly accessible. Make sure that the hostname resolves to the origin server, and is not proxied by {{site.data.keyword.cis_full_notm}}.|
|`origins.enabled`|Boolean|Optional|If set to **true**, the origin sever is enabled within the origin pool. If set to **false**, the origin server is not enabled. Disabled origin servers cannot receive incoming network traffic and are excluded from {{site.data.keyword.cis_full_notm}} health checks.|
|`check_regions`|Array|Required| A list of regions (specified by region code) from which to run health checks. If the list is empty, all regions are included, but you must use the Enterprise plan. This is the default setting. Region codes can be found on the [Cloudflare’s website](https://developers.cloudflare.com/load-balancing/understand-basics/traffic-steering/#geo-steering-enterprise-plans-only){: external}.
|`description`|String|Optional|A description for your origin pool. | 
|`enabled`|Boolean|Required|If set to **true**, this pool is enabled and can receive incoming network traffic. Disabled pools do not receive network traffic and are excluded from health checks. Disabling a pool causes any load balancers that use the pool to failover to the next pool (if applicable).|
|`minimum_origins`|Integer|Optional| The minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls within this number, the pool will be marked unhealthy and we will failover to the next available pool. Default: 1.|
|`monitor`|String|Optional|The ID of the monitor to use for health checking origins within this pool.|
|`notification_email`|String|Optional|The email address to send health status notifications to. This can be an individual mailbox or a mailing list.|


### Output parameter
{: #cis-origin-pool-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The ID of the origin pool. |
|`created_on`|String|The RFC3339 timestamp of when the origin pool was created. |
|`modified_on`|String|The RFC3339 timestamp of when the origin pool was last modified. |
|`health`|String|The status of the origin pool.|
|`origins`|List|A list of origin servers that belong to the load balancer pool.|
|`origins.healthy`|Boolean|If set to **true**, the origin server is healthy. If set to **false**, the origin server is not healthy.|

### Import
{: #cis-origin-pool-import}

The origin pool can be imported by using the `id`. The ID is formed from the origin pool ID and the CRN (Cloud Resource Name). All values are concatenated with a `:` character.
The CRN can be located on the **Overview** page of the Internet Services instance under the **Domain** heading of the UI, or via the `ibmcloud cis` CLI.

- **CRN**: The CRN is a 120 digit character string of the format `crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::` 
- **Origin pool ID**: The origin pool ID is a 32 digit character string in the format 1aaaa111111aa11111111111a1a11a1. The ID of a origin pool is not available via the UI. It can be retrieved programmatically via the CIS API or via the CLI by running `ibmcloud cis glb-pools`.

```
terraform import ibm_cis_origin_pool.myorg <origin_pool_ID>:<crn>
```
{: pre}

```
terraform import ibm_cis_origin_pool.myorg 1aaaa111111aa11111111111a1a11a1:crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::
```
{: pre}





## `ibm_cis_page_rule`
{: #cis-page-rule}

Provides an {{site.data.keyword.cis_full_notm}} page rule resource, to create, update, delete page rules of a domain. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and an {{site.data.keyword.cis_full_notm}} domain resource. For more information, about {{site.data.keyword.cis_full_notm}} page rules, see [using page rules](/docs/cis?topic=cis-use-page-rules).
{: shortdesc}

### Sample Terraform code
{: #cis-page-rule-sample}

```
# Add a page rule to the domain

resource "ibm_cis_page_rule" "page_rule" {
  cis_id    = var.cis_crn
  domain_id = var.zone_id
  targets {
    target = "url"
    constraint {
      operator = "matches"
      value    = "example.com"
    }
  }
  actions {
    id    = "email_obfuscation"
    value = "on"
  }
  actions {
    id          = "forwarding_url"
    url         = "https://ibm.travis-kuganes1.sdk.cistest-load.com/*"
    status_code = 302
  }
} 
```
{: codeblock}

### Input parameter 
{: #cis-page-rule-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} domain.|
|`status`|String|Optional|The status of the page rule. Valid values are `active` and `disabled`. Default value is `disabled`.|
|`priority`|Integer|Optional|The priority of the page rule. Default value is `1`. `Set` and `Update` are not supported yet.|
|`targets`|Set|Required|The targets, where rule is added.|
|`targets.target`|String|Required|The target type. Valid value is `url`.|
|`targets.constraint`|List |Required|The constraint of the page rule. Maximum items is `1`.|
|`targets.constraint.operator`|String |Required|The operation on the page rule. Valid value is `matches`.|
|`targets.constraint.value`|String |Required|The URL value on which page rule is applied.|
|`actions`|List|Required|The list of actions performed on URL. Minimum items is `1`.|
|`actions.id`|String|Required| The action ID. Valid values are `page rule action field map from UI` to `API CF-UI map API`). |
|`actions.id.disable_security`|String| The action conflicts with `email_obfuscation`, `server_side_exclude`, `waf`. |
|`actions.id.always_online`|String| The action conflicts with all other settings. |
|`actions.id.forwarding_url`|String| The action conflicts with all other settings. |
|`actions.id.always_use_https`|String| The action conflicts with all other settings. |
|`actions.id.ssl`|String| The TLS settings. |
|`actions.id.browser_cache_ttl`|String| The browser cache TTL. |
|`actions.id.security_level`|String| The security level. |
|`actions.id.cache_level`|String| The cache level. |
|`actions.id.edge_cache_ttl`|String| The edge cache TTL.|
|`actions.id.bypass_cache_on_cookie`|String| The bypass cache on cookie. |
|`actions.id.browser_check`|String| The browser integrity check. |
|`actions.id.server_side_exclude`|String| The server side excludes. |
|`actions.id.server_stale_content`|String| The server stale content. |
|`actions.id.email_obfuscation`|String| The Email obfuscation. |
|`actions.id.automatic_https_rewrites`|String| The automatic HTTPS rewrites. |
|`actions.id.opportunistic_encryption`|String| The opportunistic encryption. |
|`actions.id.ip_geolocation`|String| The IP geography location header. |
|`actions.id.explicit_cache_control`|String| The origin cache control. |
|`actions.id.cache_deception_armor`|String| The cache deception armor. |
|`actions.id.waf`|String| The Web Application Firewall. |
|`actions.id.host_header_override`|String| The host header override. |
|`actions.id.resolve_override`|String| The resolve override. |
|`actions.id.cache_on_cookie`|String| The cache on cookie. |
|`actions.id.disable_apps`|String| The disable apps. |
|`actions.id.disable_performance`|String| The disable performance. |
|`actions.id.image_load_optimization`|String| The image load optimization. |
|`actions.id.origin_error_page_pass_thru`|String| The origin error page pass-through. |
|`actions.id.response_buffering`|String| The response buffering. |
|`actions.id.image_size_optimization`|String| The image size optimization. |
|`actions.id.script_load_optimization`|String| The script load optimization. |
|`actions.id.true_client_ip_header`|String| The true client IP header. |
|`actions.id.sort_query_string_for_cache`|String| The sort query string. |
|`value`|String|Required| The values for corresponding actions.|
|`actions.value.always_online`|String| The valid values are `on`, `off`.|
|`actions.value.ssl`|String| The valid values are `off`, `flexible`, `full`, `strict`, `origin_pull`.|
|`actions.value.browser_cache_ttl`|Integer| The valid values are `0, 1800, 3600, 7200, 10800, 14400, 18000, 28800, 43200, 57600, 72000, 86400, 172800, 259200, 345600, 432000, 691200, 1382400, 2073600, 2678400, 5356800, 16070400, 31536000`.|
|`actions.value.security_level`|String| The valid values are `disable_security`, `always_use_https`.|
|`actions.value.cache_level`|String| The valid values are `bypass`, `aggressive`, `basic`, `simplified`, `cache_everything`.|
|`actions.value.edge_cache_ttl`|String| The valid values are `0, 30, 60, 300, 600, 1200, 1800, 3600, 7200, 10800, 14400, 18000, 28800, 43200, 57600, 72000, 86400, 172800, 259200, 345600, 432000, 518400, 604800, 1209600, 2419200`.|
|`actions.value.bypass_cache_on_cookie`|String| The valid values are `cookie tags`.|
|`actions.value.browser_check`|String| The valid values are `on`, `off`.|
|`actions.value.server_side_exclude`|String| The valid values are `on`, `off`.|
|`actions.value.server_stale_content`|String| The valid values are `on`, `off`.|
|`actions.value.email_obfuscation`|String| The valid values are `on`, `off`.|
|`actions.value.automatic_https_rewrites`|String| The valid values are `on`, `off`.|
|`actions.value.opportunistic_encryption`|String| The valid values are `on`, `off`.|
|`actions.value.ip_geolocation`|String| The valid values are `on`, `off`.|
|`actions.value.explicit_cache_control`|String| The valid values are `on`, `off`.|
|`actions.value.cache_deception_armor`|String| The valid values are `on`, `off`.|
|`actions.value.waf`|String| The valid values are `on`, `off`.|
|`actions.value.host_header_override`|String| The header value.|
|`actions.value.resolve_override`|String| The value for resolving URL override.|
|`actions.value.cache_on_cookie`|String| The cookie value.|
|`actions.value.disable_apps`|String| The value is not required.|
|`actions.value.disable_performance`|String| The value is not required.|
|`actions.value.image_load_optimization`|String| The valid values are `on`, `off`.|
|`actions.value.origin_error_page_pass_thru`|String| The valid values are `on`, `off`.|
|`actions.value.response_buffering`|String| The valid values are `on`, `off`.|
|`actions.value.image_size_optimization`|String| The valid values are `on`, `off`.|
|`actions.value.script_load_optimization`|String| The valid values are `off`, `lossless`, `lossy`.|
|`actions.value.true_client_ip_header`|String| The valid values are `on`, `off`.|
|`actions.value.sort_query_string_for_cache`|String| The valid values are `on`, `off`.|
|`actions.value.minify`|String| This is not supported yet.|
|`url`|String|Optional| The forward rule URL, a required attribute for `forwarding_url` action.|
|`status_code`|String|Optional| The status code to check for URL forwarding. The required attribute for `forwarding_url` action. Valid values are `301` and `302`. It returns `0` for all other actions.|


### Output parameter
{: #cis-page-rule-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The record ID. It is a combination of `<rule_id>:<domain_id>:<cis_id>` attributes of the origin pool. |
|`rule_id`|String|The page rule ID.|

### Import
{: #cis-page-rule-import}

The `ibm_cis_page_rule` resource can be imported by using the ID. The ID is formed from the rule ID, the domain ID of the domain and the CRN concatenated by using a `:` character.

The domain ID and CRN is located on the **Overview** page of the Internet Services instance under the **Domain** heading of the UI, or via the `ibmcloud cis` CLI.

- **Domain ID** is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`.

- **CRN** is a 120 digit character string of the format `crn:v1:bluemix:public:internet-svcs:global:a/1aa1111a1a1111aa1a111111111111aa:11aa111a-11a1-1a11-111a-111aaa11a1a1::` 

- **Rule ID** is a 32 digit character string in the format `489d96f0da6ed76251b475971b097205c`.

```
terraform import ibm_cis_page_rule.myorg <rule_id>:<domain-id>:<crn>
```
{: pre}

```
terraform import ibm_cis_page_rule.myorg page_rule 48996f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}






## `ibm_cis_rate_limit`
{: #rate-limit}

Create, update, or delete custom rate limits for an {{site.data.keyword.cis_full_notm}} domain. For more information, about rate limits, see [Rate limiting](/docs/cis?topic=cis-cis-rate-limiting).
{: shortdesc}

Rate limiting rule can only be created when you have the enterprise plan for {{site.data.keyword.cis_full_notm}}.
{: note}

### Sample Terraform code
{: #rate-limit-sample}

The following example shows how you can add a rate limit to an {{site.data.keyword.cis_full_notm}} domain. 

```
resource "ibm_cis_rate_limit" "ratelimit" {
    cis_id = data.ibm_cis.cis.id
    domain_id = data.ibm_cis_domain.cis_domain.id
    threshold = 20
    period = 900
    match {
        request {
            url = "*.example.org/path*"
            schemes = ["HTTP", "HTTPS"]
            methods = ["GET", "POST", "PUT", "DELETE", "PATCH", "HEAD"]
        }
        response {
            status = [200, 201, 202, 301, 429]
            origin_traffic = false
        }
    }
    action {
        mode = "ban"
        timeout = 43200
        response {
            content_type = "text/plain"
            body = "custom response body"
        }
    }
    correlate {
        by = "nat"
    }
    disabled = false
    description = "example rate limit for a zone"
}
```
{: codeblock}

### Input parameter 
{: #rate-limit-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance. |
|`domain_id`|String|Required|The ID of the domain where you want to add a rate limit. |
|`threshold`|Integer|Required|The number of requests received within a specific time period (`period`) before connections to the domain are refused. The threshold value must be between 2 and 1000000. |
|`period`|Integer|Required|The period of time in seconds where incoming requests to a domain are counted. If the number of requests exceeds the `threshold`, then connections to the domain are refused. The `period` value must be between 1 and 3600. | 
|`match`|List of matching rules|Optional|A list of characteristics that incoming network traffic must match the `threshold` count. | 
|`match.request`|List of request characteristics|Optional|A list of characteristics that the incoming request match the `threshold` count. If this list is not provided, all incoming requests are matched the count of the `threshold`.|
|`match.request.url`|String|Optional|The URL that the request uses. Wildcard domains are expanded to match applicable traffic, query strings are not matched. You can use `*` to apply the rule to all URLs. The maximum length of this value can be 1024.|
|`match.request.schemes`|Set of strings|Optional|The scheme of the request that determines the protocol that you want. Supported values are `HTTPS`, `HTTP,HTTPS`, and `ALL`. |
|`match.request.methods`|Set of strings|Optional|The HTTP methods that the incoming request that match the `threshold` count. Supported values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, and `ALL`. You can also combine multiple methods and separate them with a comma. For example `POST,PUT`. |
|`response`|List of HTTP responses|Optional|A list of HTTP responses that outgoing packets must match before they can be returned to the client. If an incoming request matches the request criteria, but the response does not match the response criteria, then the request packet is not counted with the `threshold`.| 
|`response.status`|Set of integers|Optional|The HTTP status that the response must have so that the request is matched with the `threshold` count. You can specify one (`403`) or multiple (`401,403`) HTTP response codes. The value that you enter must be between 100 and 999. |
|`response.header`|List of response headers|Optional|A list of HTTP response headers that the response packet must match so that the original request is matched with the `threshold` count.|
|`response.header.name`|String|Optional|The name of the HTTP response header.|
|`response.header.op`|String|Optional|The operator that you want to apply to your HTTP response header. Supported values are `eq` (equals) and `ne` (not equals). |
|`response.header.value`|String|Optional|The value that the HTTP response header must match. |
|`action`|List of actions|Required|A list of actions that you want to perform when incoming requests exceed the specified `threshold`.|
|`action.mode`|String|Required|The type of action that you want to perform. Supported values are `simulate`, `ban`, `challenge`, or `js_challenge`. For more information, about each type, see [Configure response](/docs/cis?topic=cis-cis-rate-limiting#rate-limiting-configure-response).|
|`action.timeout`|Integer|Optional|The time to wait in seconds before the action is performed. The timeout must be equal or greater than the `period` and can be provided only for actions of type `simulate` or `ban`. The value that you enter must be between 10 and 86400.|
|`action.response`|List of response information|Optional|A list of information that you want to return to the client, such as the `content-type` and specific body information. The information provided in this parameter overrides the default HTML error page that is returned to the client. You can use this option only for actions of type `simulate` or `ban`.  |
|`action.response.content_type`|String|Optional|The `content-type` of the body that you want to return. Supported values are `text/plain`, `text/xml`, and `application/json`.|
|`action.response.body`|String|Optional|The body of the response that you want to return to the client. The information that you provide must match the `action.response.content_type` that you specified. The value that you enter can have a maximum length of 1024.|
|`disabled`|Boolean|Optional|Set to **true** to disable rate limiting for a domain and **false** to enable rate limiting.|
|`description`|String|Optional|Enter a description for your rate limiting rule. |
|`correlate`|List of NAT-based rate limits|Optional|Enable NAT-based rate limiting.|
|`correlate.by`|String|Optional|Enter `nat` to enable NAT-based rate limiting.|
|`bypass`|List of bypass criteria|Optional|A list of key-value pairs that, when matched, allow the rate limiting rule to be ignored. For example, use this option if you want to ignore the rate limiting for certain URLs.  |
|`bypass.name`|String|Optional|The name of the key that you want to apply. Supported values are `url`. |
|`bypass.value`|String|Optional|The value of the key that you want to match. When `bypass.name` is set to `url`, `bypass.value` must be set to the URL that you want to exclude from the rate limiting rule. |

### Output parameter
{: #rate-limit-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the rate limiting rule in the format `<rule_ID>:<domain_ID>:<cis_ID>`. 

### Import
{: #rate-limit-import}

The resource can be imported by using the ID. 

```
terraform import ibm_cis_rate_limit.ratelimit <rule_id>:<domain-id>:<crn>
```
{: pre}


## `ibm_cis_range_app`
{: #cis_range_app}

Create, update, or delete range application an {{site.data.keyword.cis_full_notm}} domain. For more information, about range, see [protecting TCT traffic](/docs/cis?topic=cis-cis-range).
{: shortdesc}


### Sample Terraform code
{: #cis_range_app-sample}

The following example shows how you can add a rate limit to an {{site.data.keyword.cis_full_notm}} domain. 

```
resource "ibm_cis_range_app" "app" {
	cis_id         = data.ibm_cis.cis.id
	domain_id      = data.ibm_cis_domain.cis_domain.id
	protocol       = "tcp/22"
	dns_type       = "CNAME"
	dns            = "ssh.example.com"
	origin_direct  = ["tcp://12.1.1.1:22"]
	ip_firewall    = true
	proxy_protocol = "v1"
	traffic_type   = "direct"
	tls            = "off"
}
```
{: codeblock}

### Input parameter 
{: #cis_range_app-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance. |
|`domain_id`|String|Required|The ID of the domain where you want  to add the range app. |
|`protocol`|String|Required|The edge application protocol type. Valid values are `tcp`, `udp`. This attribute specified along with port number. For example, `tcp/22`. |
|`dns`|String|Required|The name of DNS record for the range application. | 
|`dns_type`|String|Required|The DNS record type. | 
|`origin_direct`|List of Strings|Optional|A list of destination addresses to the origin. IP address and port of the origin for range application. If configuring a Load Balancer, use `origin_dns` and `origin_port`. This cannot be combined with `origin_dns` and `origin_port`. For example, `tcp://192.0.2.1:22`.|
|`origin_dns`|String|Optional| DNS record pointing to the origin for the range application. This is used for configuring a Load Balancer. This requires `origin_port` and cannot be combined with `origin_direct`. When specifying an individual IP address, use `origin_direct`. For example, `origin.net`.|
|`origin_port`|Integer|Optional|Port at the origin that listens to traffic from the range application. Requires `origin_dns` and cannot be combined with `origin_direct`. |
|`ip_firewall`|Boolean|Optional|Enables the IP firewall for the application. Only available for TCP applications. |
|`proxy_protocol`|String|Optional| Allows for the true client IP to be passed to the service. Valid values are `off`, `v1`, `v2`, `simple`. Default value is `off`.| 
|`edge_ips_type`|String|Optional|The type of edge IP configuration. Valid value is `dynamic`. Default value is `dynamic`. |
|`edge_ips_connectivity`|String|Optional|Specified IP version. Valid values are `ipv4`, `ipv6`, `all`. Default value is `all`.|
|`traffic_type`|String|Optional|Configure how traffic is handled at the edge. If set to direct traffic is passed through to the service. In the case of HTTP or HTTPS, HTTPS features at the edge are applied to this traffic. Valid values are `direct`, `http`, `https`. Default value is `direct`.|
|`tls`|String|Optional|Configure how TLS connections are terminated at the edge. Valid values are `off`, `flexible`, `full`, `strict`. Default value is `off`.|

### Output parameter
{: #cis_range_app-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the range application in the format `<app_id>:<domain_id>:<cis_id>`. |
|`app_id`|String|The range application ID. |

### Import
{: #cis_range_app-import}

The `ibm_cis_range_app` resource can be imported using the ID. The ID is formed from the application ID, the Domain ID of the domain and the CRN (Cloud Resource Name)  Concatenated  by using a `:` character.

The Domain ID and CRN will be located on the overview page of the Internet Services instance from the Domain heading of the UI, or by using the `ibm cis` CLI commands.

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

App ID is a 32 digit character string of the form: `489d96f0da6ed76251b475971b097205c.`

**Syntax**

```
terraform import ibm_cis_range_app.myorg <app_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_range_app.myorg 48996f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_routing`
{: #cis-routing}

Provides an {{site.data.keyword.cis_full_notm}} routing resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and an {{site.data.keyword.cis_short}} domain resource. It allows to change routing of a domain of an {{site.data.keyword.cis_short}} instance. For more information, refer to [about {{site.data.keyword.cis_short}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis).
{: shortdesc}

### Sample Terraform code
{: #routing-sample}

The following example shows how you can add a routing resource to an {{site.data.keyword.cis_full_notm}} domain. 

```
# Change Routing of the domain

resource "ibm_cis_routing" "routing" {
	cis_id          = data.ibm_cis.cis.id
	domain_id       = data.ibm_cis_domain.cis_domain.domain_id
	smart_routing   = "on"
}
```
{: codeblock}

### Input parameter 
{: #routing-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance. |
|`domain_id`|String|Required|The ID of the domain where you want to change routing. |
|`smart_routing`|String|Optional|The smart routing to set enable or disable. Valid values are `on` and `off`. |

`tiered_caching` is not supported yet.
{: note}

### Output parameter
{: #routing-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The record ID. It is a combination of `<domain_id>,<cis_id>` attributes concatenated with `:`.|

### Import
{: #routing-import}

The `ibm_cis_routing` resource can be imported using the ID. The ID is formed from the domain ID of the domain and the CRN concatenated  using a `:` character.

The domain ID and CRN will be located on the overview page of the {{site.data.keyword.cis_full_notm}} instance of the UI domain heading, or by using the `ibmcloud cis` CLI commands.

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**Syntax**

```
terraform import ibm_cis_routing.routing <domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_routing.routing 9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_tls_settings`
{: #cis-tls}

Create, update, or delete an {{site.data.keyword.cis_full_notm}} TLS settings resources. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and an {{site.data.keyword.cis_full_notm}}Domain resource.
{: shortdesc}

### Sample Terraform code
{: #cis-tls-sample}

```
# Change TLS Settings of the domain

resource "ibm_cis_tls_settings" "%[1]s" {
	cis_id          = data.ibm_cis.cis.id
	domain_id       = data.ibm_cis_domain.cis_domain.domain_id
	tls_1_3         = "off"
	tls_1_2_only    = "on"
	min_tls_version = "1.2"
	universal_ssl   = true
}
```
{: codeblock}

### Input parameters
{: #cis-tls-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the domain to change TLS settings. |
|`tls_1_3`|String|Optional|The TLS 1.3 version setting. Valid values are `on`, `off`, `zrt`. `zrt` will enable TLS 1.3 and the Zero RTT feature. If `on` is set, then `zrt` is enabled by default.|
|`min_tls_version`|String|Optional|The Minimum TLS version setting. Valid values are `1.1`, `1.2`, `1.3`, or `1.4`.|
|`universal_ssl`|Boolean|Optional|The Universal SSL `enable` or `disable` setting.|
|`ssl_mode`|String|Optional|The SSL mode settings. This is yet to support.|

### Output parameters
{: #cis-tls-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The record ID. It is a combination of <domain_id>,<cis_id> attributes concatenated with `:`. |

### Timeouts
{: #cis-tls-timeouts}

The following timeouts are defined for this resource.
{: shortdesc}

- **Create**: The creation of the {{site.data.keyword.cis_full_notm}} instance is considered failed if no response is received for 10 minutes.
- **Update**: The update of the {{site.data.keyword.cis_full_notm}} instance is considered failed if no response is received for 10 minutes.
- **Delete**: The deletion of the {{site.data.keyword.cis_full_notm}} instance is considered failed if no response is received for 10 minutes.

### Import
{: #cis-tls-import}

The `ibm_cis_tls_settings` resource is imported using the ID. The ID is formed from the domain ID of the domain and the CRN (Cloud Resource Name) Concatenated using a `:` character.
{: shortdesc}

 The domain ID and CRN will be located on the **Overview** page of the Internet Services instance in the domain heading of the UI, or through using the {{site.data.keyword.cis_full_notm}} CLI commands.

 Domain ID is a 32 digit character string of the form: 9caf68812ae9b3f0377fdf986751a78f

 CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`
 {: note}

 **Syntax**

 ```
 terraform import ibm_cis_tls_settings.tls_settings <domain-id>:<crn>
 ```
 {: pre}

**Example**

 ```
 terraform import ibm_cis_tls_settings.tls_settings 9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
 ```
 {: pre}

 ## `ibm_cis_waf_group`
{: #cis-waf-grp}

Provides an {{site.data.keyword.cis_full_notm}} WAF rule group resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS Domain resource. It allows to change WAF Groups mode of a domain of a CIS instance. It is also named as CIS rule set. Please find `OWASP` rule set set tab under WAF of your instance in UI. For more information, refer to [{{site.data.keyword.cis_full_notm}} rule sets](/docs/cis?topic=cis-waf-settings#cis-ruleset-for-waf).
{: shortdesc}

### Sample Terraform code
{: #cis-waf-grp-sample}

The following example shows how you can add a WAF group resource to an {{site.data.keyword.cis_full_notm}} domain. 

```
resource "ibm_cis_waf_group" "test" {
  cis_id     = data.ibm_cis.cis.id
  domain_id  = data.ibm_cis_domain.cis_domain.domain_id
  package_id = "c504870194831cd12c3fc0284f294abb"
  group_id   = "3d8fb0c18b5a6ba7682c80e94c7937b2"
  mode       = "on"
}
```
{: codeblock}

### Input parameter 
{: #cis-waf-grp-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance. |
|`domain_id`|String|Required|The ID of the domain to change WAF rule group mode. |
|`package_id`|String|Required|The WAF rule group package ID. |
|`group_id`|String|Required|The WAF rule group ID.|
|`mode`|String|Required|The WAF group mode. Valid values are `on` and `off`. |

### Output parameter
{: #cis-waf-grp-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The WAF rule group ID. It is a combination of `<group_id>:<package_id>:<domain-id>:<crn>` attributes concatenated with `:`.|
|`name`|String| The WAF rule group name.|
|`description`|String|The WAF rule group description.|
|`rules_count`|String| Number of rules in WAF Group.|
|`modified_rules_count`| String |Number of rules modified in WAF Group.|

### Import
{: #cis-waf-grp-import}

The `ibm_cis_waf_group` resource can be imported by using the ID. The ID is formed from the WAF Rule Group ID, the WAF rule package ID, the domain ID of the domain and the CRN (Cloud Resource Name)  Concatenated  by using `:` character.

The domain ID and CRN will be located on the **Overview** page of the Internet Services instance of the domain heading of the UI, or by using the `ibmcloud cis` CLI commands.

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

Group ID is a 32 digit character string of the form: `57d96f0da6ed76251b475971b097205c`. The ID of an existing WAF rule group is not available in the UI. It can be retrieved programmatically from the CIS API or the CLI by using the CIS command to list the defined WAF Groups `ibmcloud cis waf-groups <domain_id> <waf_package_id>`.

**Syntax**

```
terraform import ibm_cis_waf_group.myorg <group_id>:<package_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_domain.myorg  3d8fb0c18b5a6ba7682c80e94c7937b2:57d96f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

 
## `ibm_cis_waf_package`
{: #cis-waf-package}

Provides an {{site.data.keyword.cis_full_notm}} WAF package resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS domain resource. It allows to change WAF package settings of a domain of an {{site.data.keyword.cis_full_notm}} instance. It is also named as `OWASP` rule set. For more information, about WAF refer to [Web Application Firewall concepts](/docs/cis?topic=cis-waf-q-and-a).
{: shortdesc}

### Sample Terraform code
{: #cis-waf-package-sample}

The following example shows how you can add a WAF package resource to an {{site.data.keyword.cis_full_notm}} domain. 

```
# Change WAF Package settings of the domain

resource "ibm_cis_waf_package" "waf_package" {
	cis_id      = data.ibm_cis.cis.id
	domain_id   = data.ibm_cis_domain.cis_domain.domain_id
	package_id  = "c504870194831cd12c3fc0284f294abb"
	sensitivity = "low"
	action_mode = "block"
}
```
{: codeblock}

### Input parameter 
{: #cis-waf-package-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance. |
|`domain_id`|String|Required|The ID of the domain where you want to change TLS settings. |
|`package_id`|String|Required|The WAF package ID. This cannot be modified. |
|`sensitivity`|String|Required|The WAF package sensitivity. Valid values are `high`, `medium`, `low`, `off`.|
|`action_mode`|String|Required|The WAF package action mode. Valid values are `simulate`, `block`, `challenge`. |


### Output parameter
{: #cis-waf-package-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The WAF package ID. It is a combination of `<package_id>:<domain_id>:<cis_id>` attributes concatenated with `:`.|

### Import
{: #cis-waf-package-import}

The `ibm_cis_waf_package` resource can be imported by using the ID. The ID is formed from the package ID, domain ID of the domain and the CRN (Cloud Resource Name)  Concatenated  by using a : character.

The domain ID and CRN will be located on the **Overview** page of the Internet Services instance of the Domain heading of the UI, or by using the `ibmcloud cis` CLI commands.

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**Syntax**

```
terraform import ibm_cis_waf_package.waf_package <package-id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_waf_package.waf_package 489d96f0da6ed76251b475971b097205c:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}

## `ibm_cis_waf_rule`
{: #cis-waf-rule}

Provides an {{site.data.keyword.cis_full_notm}} WAF rule settings resource. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and a CIS Domain resource. It allows to change WAF rule settings of a domain of a CIS instance. For more information, refer to [{{site.data.keyword.cis_full_notm}} rule sets](/docs/cis?topic=cis-waf-settings#cis-ruleset-for-waf).
{: shortdesc}

### Sample Terraform code
{: #cis-waf-rule-sample}

The following example shows how you can add a WAF rule resource to an {{site.data.keyword.cis_full_notm}} domain. 

```
resource "ibm_cis_waf_rule" "test" {
	cis_id     = data.ibm_cis.cis.id
	domain_id  = data.ibm_cis_domain.cis_domain.id
	package_id = "c504870194831cd12c3fc0284f294abb"
	rule_id    = "100000356"
	mode       = "on"
}
```
{: codeblock}

### Input parameter 
{: #cis-waf-rule-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance. |
|`domain_id`|String|Required|The ID of the domain where you want to change TLS settings. |
|`package_id`|String|Required|The WAF rule package ID. This cannot be modified. |
|`rule_id`|String|Required|The WAF rule ID. The filed cannot be modified.|
|`mode`|String|Required|The mode to use when the rule is triggered. Value is restricted based on the allowed_modes of the rule. Valid values are `on`, `off`, `default`, `disable`, `simulate`, `block`, `challenge`.| |


### Output parameter
{: #cis-waf-rule-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String| The WAF package ID. It is a combination of `<rule_id>,<package_id>,<domain_id>,<cis_id>` attributes concatenated with `:`.|
|`description`|String|The WAF rule description. |
|`priority`|String|The WAF rule priority. |
|`group`|String|The WAF rule group. |
|`group.id`|String|The WAF rule group ID. |
|`group.name`|String|The name of the WAF rule group. |
|`allowed_modes`|String|The allowed modes for setting the WAF rule mode. |

### Import
{: #cis-waf-rule-import}

The `ibm_cis_waf_rule` resource can be imported by using the ID. The ID is formed from the rule_id, `<package_id>, <domain ID>, <package ID>` of the domain and the CRN (Cloud Resource Name)  Concatenated  by using a `:` character.

The domain ID and CRN will be located on the **Overview** page of the Internet Services instance of the domain heading of the UI, or by using the `ibmcloud cis` CLI commands.

Rule ID is a digit character string of the form: `100000356`

Package ID is a 32 digit character string of the form: `c504870194831cd12c3fc0284f294abb`

Domain ID is a 32 digit character string of the form: `9caf68812ae9b3f0377fdf986751a78f`

CRN is a 120 digit character string of the form: `crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::`

**Syntax**

```
terraform import ibm_cis_waf_rule.waf_rule <rule_id>:<package_id>:<domain-id>:<crn>
```
{: pre}

**Example**

```
terraform import ibm_cis_waf_rule.waf_rule 100000356:c504870194831cd12c3fc0284f294abb:9caf68812ae9b3f0377fdf986751a78f:crn:v1:bluemix:public:internet-svcs:global:a/4ea1882a2d3401ed1e459979941966ea:31fa970d-51d0-4b05-893e-251cba75a7b3::
```
{: pre}


