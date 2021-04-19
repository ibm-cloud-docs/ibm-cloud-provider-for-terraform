---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

keywords: terraform internet services, terraform cis, terraform provider plugin

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



# Internet Services data sources
{: #cis_data}

You can reference the output parameters for each resource in other resources or data sources by using [Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html){: external}. 

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

## `ibm_cis`
{: #cis}

Retrieve information about an {{site.data.keyword.cis_full_notm}} instance. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-sample}

The following example retrieves information about an {{site.data.keyword.cis_full_notm}} instance. 
{: shortdesc}

```
data "ibm_cis" "cis_instance" {
  name              = "myinstance"
}
```
{: codeblock}

### Input parameters
{: #cis-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `name` | String | Required | The name of an {{site.data.keyword.cis_full_notm}} instance. |

### Output parameters
{: #cis-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `id` | String | The CRN of your instance. |
| `guid` | String| The unique identifier of the instance.|
| `plan` | String | The service plan for the instance. |
| `location` | String | The location of your instance. |
| `status` | String | The status of your instance. |


## `ibm_cis_cache_settings`
{: #cis-cache-settings}

Retrieve an information of an existing internet services cache settings. For more information, about understanding CIS cache settings, see [caching concepts](/docs/cis?topic=cis-caching-concepts).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-cache-settings-dssample}

```
data "ibm_cis_cache_settings" "test" {
  cis_id    = data.ibm_cis_cache_settings.test.cis_id
  domain_id = data.ibm_cis_cache_settings.test.domain_id
}
```
{: codeblock}

### Input parameters
{: #cis-cache-settings-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`cis_id`|String|Required| The resource CIS ID of the CIS on which zones were created. |
|`domain_id`|String|Required|The resource domain ID of the DNS on which zones were created. |
{: caption="Table 1. Available input parameters" caption-side="top"}


### Output parameters
{: #cis-cache-settings-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `caching_level` | String | The cache level setting of a specific zone.|
| `caching_level.id` | String | The cache level ID.|
| `caching_level.value` | String | The cache level value `basic`, `simplified`, or `aggressive`.|
| `caching_level.editable` | String | The cache level editable value.|
| `caching_level.modified_on` | String | The cache level modified date.|
| `browser_expiration` | String | The browser cache TTL (in seconds) specifies how long `CDN` edge servers cached resources will remain on your visitors' computers.|
| `browser_expiration.id` | String | The browser expiration TTL type id.|
| `browser_expiration.value` | String | The browser expiration TTL value.|
| `browser_expiration.editable` | String | The browser expiration editable value.|
| `browser_expiration.modified_on` | String | The browser expiration modified date.|
| `development_mode` | String | The development mode settings of a specific zone.|
| `development_mode.id` | String | The development mode object ID.|
| `development_mode.value` | String | The development mode value. on and off.|
| `development_mode.editable` | String | The development mode editable value.|
| `development_mode.modified_on` | String | The development mode modified date.|
| `query_string_sort` | String | Enables query string sort settings.|
| `query_string_sortid` | String | The query string sort cache ID.|
| `query_string_sort.value` | String | The query string sort value.on and off.|
| `query_string_sort.editable` | String | The query string sort editable property.|
| `query_string_sort.modified_on` | String | The query string sort modified date.|
| `serve_stale_content` | String | The serve stale content will serve pages from `CDN` edge servers cache if your server is offline.|
| `serve_stale_content.id` | String | The serve stale content cache ID.|
| `serve_stale_content.value` | String | The serve stale content value.on and off.|
| `serve_stale_content.editable` | String | The serve stale content editable value.|
| `serve_stale_content.modified_on` | String | The serve stale content modified date.|

## `ibm_cis_certificates`
{: #cis-certificates}

 Imports a read only copy of an existing {{site.data.keyword.cis_full_notm}} certificates resource. For more information about CIS certificate order, refer to [managing origin certificates](/docs/cis?topic=cis-cis-origin-certificates).
 {: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-certificates-dssample}

```
data "ibm_cis_certificates" "test" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
}
```
{: codeblock}

### Input parameters
{: #cis-certificates-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|Required|The ID of the domain. |


### Output parameters
{: #cis-certificates-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`certificates`|String|The collection of the certificates.|
|`certificates.id`|String| It is a combination of `<certificate_id>:<domain_id>:<cis_id>`.|
|`certificates.certificate_id`|String| The certificate ID.|
|`certificates.type`|String| The certificate type.|
|`certificates.hosts`|String|  The hosts of the ordered certificates.|
|`certificates.status`|String| The certificate status.|
|`certificates.primary_certificate`|String| The primary certificate ID.|
|`certificates.certificates`|List| The list of certificates associated with the ordered certificate.|
|`certificates.certificates.id`|String| The certificate ID.|
|`certificates.certificates.hosts`|String| The hosts of the associated with the certificates.|
|`certificates.certificates.status`|String| The certificate status.|

## `ibm_cis_custom_certificates`
{: #cis-custom-certificates}

 Imports a read only copy of an existing {{site.data.keyword.cis_full_notm}} custom certificates resource. For more information about CIS certificate order, refer to [upload custom certificates](/docs/cis?topic=cis-manage-your-ibm-cis-for-optimal-security#upload-custom-certs).
 {: shortdesc}
 
### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-custom-certificates-dssample}

```
# Get custom certificates of the domain

data "ibm_cis_custom_certificates" "custom_certificates" {
    cis_id    = data.ibm_cis.cis.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
}
```
{: codeblock}

### Input parameters
{: #cis-custom-certificates-dsinput}

The input parameters are not support for this data source. 
{: shortdesc}


### Output parameters
{: #cis-custom-certificates-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`cis_id`|String|The ID of the {{site.data.keyword.cis_full_notm}} instance.|
|`domain_id`|String|The ID of the domain to change custom certificate. |
|`custom_certificates`|String|The collection of the custom certificates.|
|`custom_certificates.id`|String| It is a combination of `<custom_cert_id>:<domain_id>:<cis_id>`.|
|`custom_certificates.custom_cert_id`|String| The custom certificate ID.|
|`custom_certificates.bundle_method`|String| The custom certificate bundle method.|
|`custom_certificates.type`|String| The certificate type.|
|`custom_certificates.hosts`|String|  The list of hosts that are uploaded in a certificate.|
|`custom_certificates.priority`|String|  The custom certificate priority.|
|`custom_certificates.status`|String| The custom certificate status.|
|`custom_certificates.issuer`|String| The custom certificate issuer.|
|`custom_certificates.signature`|String| The custom certificate signature.|
|`custom_certificates.expires_on`|String| The expiry date and time of the certificate.|
|`custom_certificates.uploaded_on`|String| The uploaded date and time of the certificate.|
|`custom_certificates.modified_on`|String| The modified date and time of the certificate.|


## `ibm_cis_custom_pages`
{: #cis-custom-pages}

 Imports a read only copy of an existing {{site.data.keyword.cis_full_notm}} custom pages resource. For more information, about custom page, refer to [CIS custom page](/docs/cis?topic=cis-custom-page).
 {: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-custom-pages-sample}

```
# Get custom pages of the domain

data "ibm_cis_custom_pages" "custom_pages" {
    cis_id    = data.ibm_cis.cis.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
}
```
{: codeblock}

### Output parameters
{: #cis-custom-pages-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`created_on`|String|Created date and time of the custom page.|
| `cis_id` | String | The ID of the CIS service instance.  |
| `description` | String | The description of the custom page.|
| `domain_id` | String | The domain ID to change custom page. |
| `id` | String | The custom page ID. It is a combination of `<page_id>, <domain_id>, <cis_id>` attributes concatenated with `:`.|
|`modified_on`|String|Modified date and time of the custom page.|
| `page_id ` | String | The custom page identifier. Valid values are `basic_challenge`, `waf_challenge`, `waf_block`, `ratelimit_block`, `country_challenge`, `ip_block`, `under_attack`, `500_errors`, `1000_errors`, `always_online`. |
| `preview_target` | String | The target custom page.|
| `required_tokens` | String | The custom page required token which is expected from the URL page.|
| `state` | String | The custom page state. This is set default when there is an empty URL and can customize when URL is set with some URL.|
| `url` | String | The URL for custom page settings. By default URL is set with empty string `""`. Setting a duplicate empty string throws an error.|


## `ibm_cis_dns_record`
{: #cis-dns-record}

Retrieve information about an {{site.data.keyword.cis_full_notm}} domain name service record. For more information, about DNS records, refer to [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records). 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-dns-record-sample}

The following example retrieves information about an {{site.data.keyword.cis_full_notm}} domain. 
{: shortdesc}

```
data "ibm_cis_dns_records" "test" {
  cis_id    = var.cis_crn
  domain_id = var.zone_id
  file      = "records.txt"
}
```
{: codeblock}

### Input parameters
{: #cis-dns-record-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `domain_id` | String | Required |  The resource domain ID of the DNS on which zones were created.|
| `cis_id` | String | Required | The ID of the {{site.data.keyword.cis_full_notm}} instance on which zones were created. |
|`file`| String | Optional| The file that DNS records to be exported.|

### Output parameters
{: #cis-dns-record-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `cis_dns_records` | List | The list of DNS records. |
| `cis_dns_records.id` | String | The ID which consists of record id, zone id and CRN with `:` separator . |
| `cis_dns_records.record_id` | String | The DNS record identifier. |
| `cis_dns_records.name` | String | The name of a DNS record. |
| `cis_dns_records.proxiable` | String | Whether the record has option to set proxied. |
| `cis_dns_records.proxied` | String | Whether the record gets CIS's origin protection; defaults to `false`. |
| `cis_dns_records.created_on` | String | The created date of the DNS record. |
| `cis_dns_records.modified_on` | String | The modified date of the DNS record. |
| `cis_dns_records.zone_name` | String | The DNS zone name. |
| `cis_dns_records.type` | String | The type of the DNS record to be created. Supported Record types are `A`, `AAAA`, `CNAME`, `LOC`, `TXT`, `MX`, `SRV`, `SPF`, `NS`, `CAA`. |
| `cis_dns_records.ttl` | String | TTL of the record. It should be automatic that is `ttl=1`, if the record is proxied. Terraform provider takes `ttl` in unit seconds. |
| `cis_dns_records.priority` | String | The priority of the record. Mandatory field for `SRV` record type. |
| `cis_dns_records.data` | String | Map of attributes that constitute the record value. Only for `LOC`, `CAA` and `SRV` record types. |
  
## `ibm_cis_domain`
{: #cis_domain}

Retrieve information about an {{site.data.keyword.cis_full_notm}} domain. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-domain-sample}

The following example retrieves information about an {{site.data.keyword.cis_full_notm}} domain. 
{: shortdesc}

```
data "ibm_cis_domain" "cis_instance_domain" {
  domain = "mydomain.com"
  cis_id = ibm_cis.instance.id
}

data "ibm_cis" "cis_instance" {
  name = "myinstance"
}
```
{: codeblock}

### Input parameters
{: #cis-domain-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `domain` | String | Required | The DNS domain name that is added and managed for an {{site.data.keyword.cis_full_notm}} instance. |
| `cis_id` | String | Required | The ID of the {{site.data.keyword.cis_full_notm}} instance. |

### Output parameters
{: #cis-domain-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `id` | String | The unique identifier of your domain. |
| `paused` | Boolean | If set to **true**, network traffic to this domain is paused. If set to **false**, network traffic to this domain is permitted. The default value is **false**.  |
| `status` | String | The status of your domain. Valid values are `active`, `pending`, `initializing`, `moved`, `deleted`, and `deactivated`. After creation, the status remains pending until the DNS Registrar is updated with the CIS name servers, exported in the ‘name_servers’ variable. |
| `name_servers` | String | The {{site.data.keyword.cis_full_notm}} assigned name servers, to be passed by interpolation to the resource dns_domain_registration_nameservers. |
| `original_name_servers` | String | The name servers from when the Domain was initially registered with the DNS Registrar.|

## `ibm_cis_edge_functions_actions`
{: #cis-edge-functions-actions-ds}

Retrieve information about an {{site.data.keyword.cis_full_notm}} edge function actions resource.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-edge-functions-actions-dssample}

The following example retrieves information about an {{site.data.keyword.cis_full_notm}} edge function actions resource.
{: shortdesc}

```
data "ibm_cis_edge_functions_actions" "test_actions" {
    cis_id    = data.ibm_cis.cis.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
}
```
{: codeblock}

### Input parameters
{: #cis-edge-functions-actions-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `domain_id` | String | Required | The ID of the domain to add an edge functions action. |
| `cis_id` | String | Required | The ID of the {{site.data.keyword.cis_full_notm}} instance. |

### Output parameters
{: #cis-edge-functions-actions-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `created_on` | String | An action created date. |
| `etag` | String | An action E-Tag. |
| `handler` | String | An action handler methods.  |
| `modified_on` | String | An action modified date. |
| `routes` | String | An action route detail.|
| `routes.action_name` | String | An action route detail.|
| `routes.pattern_url` | String | The Route pattern. It is a domain name in which the action is performed.|
| `routes.request_limit_fail_open` | String | An action request limit fail open.|
| `routes.trigger_id` | String | The Trigger ID of an action.|


## `ibm_cis_edge_functions_triggers`
{: #cis-edge-functions-triggers-ds}

Retrieve information about an {{site.data.keyword.cis_full_notm}} edge function triggers resource.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-edge-functions-triggers-dssample}

The following example retrieves information about an {{site.data.keyword.cis_full_notm}} edge function actions resource.
{: shortdesc}

```
data "ibm_cis_edge_functions_triggers" "test_triggers" {
    cis_id    = data.ibm_cis.cis.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
}
```
{: codeblock}

### Input parameters
{: #cis-edge-functions-triggers-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `domain_id` | String | Required | The ID of the domain to add an edge functions triggers. |
| `cis_id` | String | Required | The ID of the {{site.data.keyword.cis_full_notm}} instance. |

### Output parameters
{: #cis-edge-functions-triggers-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `action_name` | String | An action script for execution.|
| `pattern_url` | String | The Route pattern. It is a domain name in which the action is performed.|
| `request_limit_fail_open` | String | An action request limit fail open.|
| `trigger_id` | String | The route ID of an action trigger.|

## `ibm_cis_firewall`
{: #cis-firewallds}

Retrieves an existing {{site.data.keyword.cis_full_notm}} instance. For more information, see [firewall rule actions](/docs/cis?topic=cis-actions).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-firewall-dssample}

```
data "ibm_cis_firewall" "lockdown" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
  firewall_type = "lockdowns"
}
```
{: codeblock}

IBM Terraform on {{site.data.keyword.cloud_notm}} provider supports only lock down rules.
{: note}

### Input parameters
{: #cis-firewall-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required / optional|Description|
|----|-----------|-----------|---------------------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance where you want to create the firewall.|
|`domain_id`|String|Required|The ID of the domain where you want to add the lock down.|
|`firewall_type`|String|Required|The type of firewall that you want to create for your domain. Supported values are `lockdowns`, `access_rules`, and `ua_rules`. Consider the following information when choosing your firewall type: <ul><li><strong><code>access_rules</code></strong>: Access rules allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.</li><li><strong><code>ua_rules</code></strong>: Apply firewall rules only if the user agent that is used by the client matches the user agent that you defined. </li><li><strong><code>`lockdowns`</code></strong>: Allow access to your domain for specific IP addresses or IP address ranges only. If you choose this firewall type, you must define your firewall rules in the `lockdown` input parameter.</li></ul>|

### Output parameters
{: #cis-firewall-dsoutput}

Review the output parameters that you can access after your data source is created. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|--------|
|`id`|String|The ID of the record. The ID is composed of `<firewall_type>,<lockdown_id/access_rule_id/ua_rule_id>,<domain_ID>,<cis_crn>`. Attributes are concatenated with `:`.|
|`lockdown.lockdown_id`|List|List of lock down to be created. The data describing a lock down rule.|
|`lockdown.paused`|Boolean|Required|If set to **true**, the firewall rule is disabled. If set to **false**, the firewall rule is enabled.|
|`lockdown.description`|String|A description for your firewall rule.|
|`lockdown.priority`|Integer|The priority of the firewall rule. A low number is associated with a high priority. |
|`lockdown.urls`|List of URLs|A list of URLs that you want to include in your firewall rule. You can specify wildcard URLs. The URL pattern is escaped before use.|
|`lockdown.configurations`|List of IP addresses|A list of IP address or CIDR ranges that you want to allow access to the URLs that you defined in `lockdown.urls`. |
|`lockdown.configurations.target`|String|Specify if you want to target an `IP` or `ip_range`.|
|`lockdown.configurations.value`|String|The IP addresses or CIDR. |
|`access_rule`|String|Create the data describing the access rule. |
|`access_rule.rule_id`|String| The access rule ID. |
|`access_rule.notes`|String| The free text for notes. |
|`access_rule.mode`|String| The mode of access rule. The valid modes are `block`, `challenge`, `whitelist`, `js_challenge`.|
|`access_rule.configuration`|List| The Configuration of firewall. (Maximum items is 1) |
|`access_rule.configuration.target`|String| The request property to target. Valid values are `ip`, `ip_range`, `asn`, `country`. |
|`access_rule.configuration.value`|String| IP address or CIDR or Autonomous or Country code. |
|`ua_rule`|String|Create the data describing the user agent rule. |
|`ua_rule.ua_rule_id`|String| The user agent rule ID. |
|`ua_rule.description `|String|The free text for description. |
|`ua_rule.mode`|String|The mode of access rule. The valid modes are `block`, `challenge`,  `js_challenge`. |
|`ua_rule.paused`|String|Whether the rule is currently disabled. |
|`ua_rule.configuration`|List| The Configuration of firewall. |
|`ua_rule.configuration.target`|String| The request property to target. Valid values are `ua`. |
|`ua_rule.configuration.value`|String| The exact User Agent string to match the rule. |

Exactly one of `lockdown`, `access_rule`, and `ua_rule` is allowed for the firewall types `lockdowns`, `access_rules`, and `ua_rules`.
{: note}

## `ibm_cis_global_load_balancers`
{: #cis-global-lb-ds}

Retrieve information 24 X 7 availability and performance of your application by using the {{site.data.keyword.cis_full_notm}} global load balancers. For more information, refer to [CIS global loadbalancer](/docs/cis?topic=cis-configure-glb).Import the details of an existing {{site.data.keyword.cis_full_notm}} global load balancers as a read-only data source. You can then reference the fields of the data source in other resources within the same configuration using interpolation syntax.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-global-lb-dssample}

The following example retrieves information about an {{site.data.keyword.cis_full_notm}} global load balancer resource.
{: shortdesc}

```
data "ibm_cis_global_load_balancers" "test" {
  cis_id    = var.cis_crn
  domain_id = var.zone_id
}
```
{: codeblock}

### Input parameters
{: #cis-global-lb-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `domain_id` | String | Required | The ID of the domain to retrieve the load balancers from. |
| `cis_id` | String | Required | The resource CRN ID of the CIS on which zones were created. |

### Output parameters
{: #cis-global-lb-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `id` | String | The Load balancer ID, domain ID and CRN. For example, `id:domain-id:crn`. |
| `description` | String | Free text description. |
| `default_pool_ids` | String | A list of pool IDs ordered by their failover priority. Used whenever region or pop pools are not defined. |
| `fallback_pool_id` | String | The pool ID to use when all other pools are detected as unhealthy. |
| `glb_id` | String | The Load balancer ID. |
| `enabled` | String | Indicates if the load balancer is enabled or not. Region and pop pools are not currently implemented in this version of the provider. |
| `name` | String | The DNS name to associate with the load balancer. This can be a hostname, for example, `www` or the fully qualified name `www.example.com`, or `example.com`. |
| `proxied` | String | Whether the hostname gets IBM's origin protection. Defaults to `false`.  |
| `pop_pools` | String | A set containing mappings of IBM Point-of-Presence (PoP) identifiers to a list of pool IDs (ordered by their failover priority) for the PoP (datacenter). This feature is only available to enterprise customers.|
| `pop_pools.pop` | String | A 3-letter code for the Point-of-Presence. Multiple entries should not be specified with the same PoP.|
| `pop_pools.pool_ids` | String | A list of pool IDs in failover priority to use for traffic reaching the given PoP.|
| `region_pools` | String | A set containing mappings of region or country codes to a list of pool IDs (ordered by their failover priority) for the given region.|
| `region_pools.region` | String | A region code. Multiple entries is not allowed with the same region.|
| `region_pools.pool_ids` | String | A list of pool IDs in failover priority to use in the given region.|
| `session_affinity` | String | Associates all requests coming from an end-user with a single origin. IBM will set a cookie on the initial response to the client, such that consequent requests with the cookie in the request will go to the same origin, as long as it is available. |
| `ttl` | String | Time to live (TTL) of the DNS entry for the IP address returned by this load balancer.  |


## `ibm_cis_healthchecks`
{: #cis-healthchecks}

Retrieve information about an {{site.data.keyword.cis_full_notm}} global load balancer health monitor or check as a read-only data source.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-healthchecks-sample}

The following example retrieves information about an {{site.data.keyword.cis_full_notm}} domain. 
{: shortdesc}

```
data "ibm_cis_glb_health_checks" "test" {
  cis_id = var.cis_crn
}
```
{: codeblock}

### Input parameters
{: #cis-healthchecks-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
| `cis_id` | String | Required | The resource CRN ID of the {{site.data.keyword.cis_full_notm}} on which zones were created. |

### Output parameters
{: #cis-healthchecks-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `allow_insecure` | String | Do not validate the certificate when health check uses `HTTPS`.|
| `created_on` | String | The RFC3339 timestamp of when the load balancer monitor was created.|
| `description` | String | Free text description.|
| `expected_body` | String | The requested body.|
| `expected_codes` | String | The expected HTTP response code or code range of the health check. For example, `2xx`.|
| `headers` | String | The health check header.|
| `id` | String | The load balancer monitor ID and CRN. For example, `monitor_id:crn`.|
| `interval` | String | The interval between each health check. Shorter intervals improve failover time, but can increase load on the origins as you check from multiple locations. The default value is `60`.|
| `modified_on` | String | The RFC3339 timestamp of when the load balancer monitor was last modified.|
| `monitor_id` | String | The load balancer monitor ID.|
| `method` | String | The HTTP method to use for the health check.|
| `path` | String | The endpoint path to health check.|
| `port` | String | The TCP port to use for the health check.|
| `retries` | String | The number of retries to attempt in case of a timeout before marking the origin as unhealthy. Retries are attempted immediately. The default value is `2`.|
| `timeout` | String | The timeout (in seconds) before marking the health check as failed. The default value is `5`.|
| `type` | String | The protocol to use for the health check. Currently supported protocols are `HTTP`, `HTTPS`, and `TCP`. The default value is `HTTP`.|
| `follow_redirects` | String | Follow redirects if returned by the origin.|

## `ibm_cis_ip_addresses`
{: #cis_ip}

Import a list of all IP addresses that the CIS proxy uses. The CIS proxy uses these IP addresses for both `client-to-proxy` and `proxy-to-origin` communication. You can reference the IP addresses by using Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax to configure and allowed IP addresses in firewalls, network ACLs, and security groups. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-ip-sample}

The following example retrieves information about IP addresses that {{site.data.keyword.cis_full_notm}} uses for name servers. 
{: shortdesc}

```
data "ibm_cis_ip_addresses" "cisname" {
}
```
{: codeblock}

### Input parameters
{: #cis-ip-input}

No input parameters are required for this data source. 

### Output parameters
{: #cis-ip-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
| `ipv4_cidrs` | String | The IPv4 address ranges that the CIS proxy uses and that you can reference to configure and allowed IP addresses in firewalls, network ACLs, and security groups. |
| `ipv6_cidrs` | String | The IPv6 address ranges that the CIS proxy uses and that you can reference to configure and allowed IP addresses in firewalls, network ACLs, and security groups.|

## `ibm_cis_origin_pools`
{: #origin-pools}

Retrieves an {{site.data.keyword.cis_full_notm}} origin pool resource. This provides a pool of origins that is used by an {{site.data.keyword.cis_full_notm}} Global Load Balancer. This resource is associated with an {{site.data.keyword.cis_full_notm}} instance and optionally an {{site.data.keyword.cis_full_notm}} Health check monitor resource.
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #origin-pools-sample}

```
data "ibm_cis_origin_pools" "test" {
  cis_id = var.cis_crn
}
```
{: codeblock}

### Input parameters
{: #origin-pools-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`cis_id`|String|Required|The ID of the CIS service instance. |  

### Output parameters
{: #origin-pools-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`created_on`|String|Created RFC3339 timestamp of the Load Balancer. |
|`description`|String|The description of the origin pool. |
|`enabled`|String|The default value is `enabled`. Disabled pools do not receive traffic, and are excluded from health checks. Disabling a pool cause any Load Balancers using it to failover to the next pool (if any). |
|`healthy`|String|The status of the origin pool. |
|`id`|String|The ID of the Load Balancer pool.|
|`modified_on`|String|Last modified RFC3339 timestamp of the Load Balancer. |
|`monitor`|String|The ID of the monitor to use for health checking origins within this pool.|
|`name`|String|A short name `tag` for the pool. Only alphanumeric characters, hyphens, and underscores are allowed. |
|`notification_email`|String|The Email address to send health status notifications. This can be an individual mailbox or a mailing list.|
|`origins`|String|The list of origins within this pool. Traffic directed at this pool is balanced across all currently healthy origins, provided the pool itself is healthy. Description of it's complex value is stated. |
|`origins.name`|String|A human-identifiable name of the origin. |
|`origins.address`|String|The IP address `IPv4` or `IPv6` of the origin, or the publicly addressable hostname. Hostnames entered is resolved directly to the origin, and not be a hostname proxied by CIS.|
|`origins.enabled`|String|The default value is `enable`. Disabled origins do not receive traffic, and are excluded from health checks. The origin is disabled only for the current pool.|
|`origins.weight`|String|The weight of the origin pool.|
|`origins.healthy`|String|The status of origins health.|
|`origins.disabled_at`|String|The disabled date and time.|
|`origins.failure_reason`|String|The failure reason.|


## `ibm_cis_rate_limit`
{: #rate-limit}

Retrieve information for a rate limiting rule of an {{site.data.keyword.cis_full_notm}} domain.
{: shortdesc}

To retrieve information about a rate limiting rule, you must have the enterprise plan for an {{site.data.keyword.cis_full_notm}}. 
{: note}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #rate-limit-sample}

```
data "ibm_cis_rate_limit" "ratelimit" {
    cis_id = data.ibm_cis.cis.id
    domain_id = data.ibm_cis_domain.cis_domain.id
}
```
{: codeblock}

### Input parameters
{: #rate-limit-input}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance where you created the rate limiting rule. |  
|`domain_id`|String|Required|The ID of the domain where you created the rate limiting rule. |

### Output parameters
{: #rate-limit-output}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id`|String|The record ID of the rate limiting rule in the format `<rule_ID>:<domain_ID>:<cis_ID>`.|
|`rule_id`|String|The ID of the rate limiting rule. |
|`threshold`|Integer|The number of requests received within a specific time period (`period`) before connections to the domain are refused. The threshold value can be between 2 and 1000000. |
|`period`|Integer|The period of time in seconds where incoming requests to a domain are counted. If the number of requests exceeds the `threshold`, then connections to the domain are refused. The `period` value can be between 1 and 3600. |
|`match`|List of matching rules|A list of characteristics that incoming network traffic must match to be counted toward the `threshold`. | 
|`match.request`|List of request characteristics|A list of characteristics that the incoming request must match to be counted toward the `threshold`. If no list is provided, all incoming requests are counted toward the `threshold`.|
|`match.request.url`|String|The URL that the request uses. Wildcard domains are expanded to match applicable traffic, query strings are not matched. If `*` is returned, the rule is applied to all URLs. The maximum length of this value can be 1024.|
|`match.request.schemes`|Set of strings|The scheme of the request that determines the protocol that you want. Supported values are `HTTPS`, `HTTP,HTTPS`, and `ALL`. |
|`match.request.methods`|Set of strings|The HTTP methods that the incoming request can use to be counted toward the `threshold`. Supported values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, and `ALL`. You can also combine multiple methods and separate them with a comma. For example `POST,PUT`. |
|`response`|List of HTTP responses|A list of HTTP responses that outgoing packets must match before they can be returned to the client. If an incoming request matches the request criteria, but the response does not match the response criteria, then the request packet is not counted toward the `threshold`.| 
|`response.status`|Set of integers|The HTTP status code that the response must have so that the request is counted toward the `threshold`. The value can be between 100 and 999. If you want to use multiple response codes, you must separate them with a comma, such as `401,403`.|
|`response.header`|List of response headers|A list of HTTP response headers that the response packet must match so that the original request is counted toward the `threshold`.|
|`response.header.name`|String|The name of the HTTP response header.|
|`response.header.op`|String|The operator that applied to your HTTP response header. Supported values are `eq` (equals) and `ne` (not equals). |
|`response.header.value`|String|The value that the HTTP response header must match. |
|`action`|List of actions|A list of actions that you want to perform when incoming requests exceed the specified `threshold`.|
|`action.mode`|String|The type of action that you want to perform. Supported values are `simulate`, `ban`, `challenge`, or `js_challenge`. For more information, about each type, see [Configure response](/docs/cis?topic=cis-cis-rate-limiting#rate-limiting-configure-response).|
|`action.timeout`|Integer|The time to wait in seconds before the action is performed. The timeout must be equal to or greater than the `period` and is valid only for actions of type `simulate` or `ban`. The value can be between 10 and 86400.|
|`action.response`|List of response information|A list of information that you want to return to the client, such as the `content-type` and specific body information. The information provided in this parameter overrides the default HTML error page that is returned to the client. This option is valid only for actions of type `simulate` or `ban`.  |
|`action.response.content_type`|String|The `content-type` of the body that you want to return. Supported values are `text/plain`, `text/xml`, and `application/json`.|
|`action.response.body`|String|The body of the response that you want to return to the client. The information must match the `action.response.content_type` that you specified. The value can have a maximum length of 1024.|
|`disabled`|Boolean|If set to **true**, rate limiting is disabled for the domain.|
|`description`|String|The description for your rate limiting rule. |
|`correlate`|List of NAT-based rate limits|If provided, NAT-based rate limiting is enabled.|
|`correlate.by`|String|If set to `nat`, NAT-based rate limiting is enabled.|
|`bypass`|List of bypass criteria|A list of key-value pairs that, when matched, allow the rate limiting rule to be ignored.  |
|`bypass.name`|String|The name of the key that you want to apply. Supported values are `url`. |
|`bypass.value`|String|The value of the key that you want to match. When `bypass.name` is set to `url`, `bypass.value` contains the URL that you want to exclude from the rate limiting rule. |


## `ibm_cis_page_rules`
{: #cis-page-rules}

Retrieve an information of an {{site.data.keyword.cis_full_notm}} page rules resource. For more information, about {{site.data.keyword.cis_full_notm}} page rules, see [using page rules](/docs/cis?topic=cis-use-page-rules).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-page-rules-dssample}

```
data "ibm_cis_page_rules" "rules" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
}
```
{: codeblock}

### Input parameters
{: #cis-page-rules-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`cis_id`|String|Required|The ID of the {{site.data.keyword.cis_full_notm}} instance . |
|`domain_id`|String|Required|The ID of the domain. |


### Output parameters
{: #cis-page-rules-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`cis_page_rules`|String| The page rules detail.|
|`cis_page_rules.rule_id`|String| The page rule ID.|
|`cis_page_rules.priority`|String| The priority of the page rule.|
|`cis_page_rules.status`|String|  The status of the page rule. Default value is `active`.|
|`cis_page_rules.targets`|String|  The targets, of the added rule.|
|`cis_page_rules.targets.target`|String| The target type. Valid value is `url`.|
|`cis_page_rules.targets.constraint`|String| The constraint of the page rule.|
|`cis_page_rules.targets.constraint.operator`|String| The operation on page rule. Valid value is `matches`.|
|`cis_page_rules.targets.constraint.value`|String| The URL value on the applied page rule.|
|`cis_page_rules.actions`|String|  The actions to be performed on the URL.|
|`cis_page_rules.id`|String| The action ID. Valid values are `page rule action field map from UI` to `API CF-UI map API`). |
|`cis_page_rules.id.disable_security`|String| The action conflicts with `email_obfuscation`, `server_side_exclude`, `waf`. |
|`cis_page_rules.id.always_online`|String| The action conflicts with all other settings. |
|`cis_page_rules.id.forwarding_url`|String| The action conflicts with all other settings. |
|`cis_page_rules.id.always_use_https`|String| The action conflicts with all other settings. |
|`cis_page_rules.id.ssl`|String| The TLS settings. |
|`cis_page_rules.id.browser_cache_ttl`|String| The browser cache TTL. |
|`cis_page_rules.id.security_level`|String| The security level. |
|`cis_page_rules.id.cache_level`|String| The cache level. |
|`cis_page_rules.id.edge_cache_ttl`|String| The edge cache TTL.|
|`cis_page_rules.id.bypass_cache_on_cookie`|String| The bypass cache on cookie. |
|`cis_page_rules.id.browser_check`|String| The browser integrity check. |
|`cis_page_rules.id.server_side_exclude`|String| The server side excludes. |
|`cis_page_rules.id.server_stale_content`|String| The server stale content. |
|`cis_page_rules.id.email_obfuscation`|String| The Email obfuscation. |
|`cis_page_rules.id.automatic_https_rewrites`|String| The automatic HTTPS rewrites. |
|`cis_page_rules.id.opportunistic_encryption`|String| The opportunistic encryption. |
|`cis_page_rules.id.ip_geolocation`|String| The IP geography location header. |
|`cis_page_rules.id.explicit_cache_control`|String| The origin cache control. |
|`cis_page_rules.id.cache_deception_armor`|String| The cache deception armor. |
|`cis_page_rules.id.waf`|String| The Web Application Firewall. |
|`cis_page_rules.id.host_header_override`|String| The host header override. |
|`cis_page_rules.id.resolve_override`|String| The resolve override. |
|`cis_page_rules.id.cache_on_cookie`|String| The cache on cookie. |
|`cis_page_rules.id.disable_apps`|String| The disable apps. |
|`cis_page_rules.id.disable_performance`|String| The disable performance. |
|`cis_page_rules.id.image_load_optimization`|String| The image load optimization. |
|`cis_page_rules.id.origin_error_page_pass_thru`|String| The origin error page pass-through. |
|`cis_page_rules.id.response_buffering`|String| The response buffering. |
|`cis_page_rules.id.image_size_optimization`|String| The image size optimization. |
|`cis_page_rules.id.script_load_optimization`|String| The script load optimization. |
|`cis_page_rules.id.true_client_ip_header`|String| The true client IP header. |
|`cis_page_rules.id.sort_query_string_for_cache`|String| The sort query string. |
|`cis_page_rules.value`|String| The values for corresponding actions.|
|`cis_page_rules.value.always_online`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.ssl`|String| The valid values are `off`, `flexible`, `full`, `strict`, `origin_pull`.|
|`cis_page_rules.value.browser_cache_ttl`|Integer| The valid values are `0, 1800, 3600, 7200, 10800, 14400, 18000, 28800, 43200, 57600, 72000, 86400, 172800, 259200, 345600, 432000, 691200, 1382400, 2073600, 2678400, 5356800, 16070400, 31536000`.|
|`cis_page_rules.value.security_level`|String| The valid values are `disable_security`, `always_use_https`.|
|`cis_page_rules.value.cache_level`|String| The valid values are `bypass`, `aggressive`, `basic`, `simplified`, `cache_everything`.|
|`cis_page_rules.value.edge_cache_ttl`|String| The valid values are `0, 30, 60, 300, 600, 1200, 1800, 3600, 7200, 10800, 14400, 18000, 28800, 43200, 57600, 72000, 86400, 172800, 259200, 345600, 432000, 518400, 604800, 1209600, 2419200`.|
|`cis_page_rules.value.bypass_cache_on_cookie`|String| The valid values are `cookie tags`.|
|`cis_page_rules.value.browser_check`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.server_side_exclude`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.server_stale_content`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.email_obfuscation`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.automatic_https_rewrites`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.opportunistic_encryption`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.ip_geolocation`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.explicit_cache_control`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.cache_deception_armor`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.waf`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.host_header_override`|String| The header value.|
|`cis_page_rules.value.resolve_override`|String| The value for resolving URL override.|
|`cis_page_rules.value.cache_on_cookie`|String| The cookie value.|
|`cis_page_rules.value.disable_apps`|String| The value is not required.|
|`cis_page_rules.value.disable_performance`|String| The value is not required.|
|`cis_page_rules.value.image_load_optimization`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.origin_error_page_pass_thru`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.response_buffering`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.image_size_optimization`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.script_load_optimization`|String| The valid values are `off`, `lossless`, `lossy`.|
|`cis_page_rules.value.true_client_ip_header`|String| The valid values are `on`, `off`.|
|`cis_page_rules.value.sort_query_string_for_cache`|String| The valid values are `on`, `off`.|
|`cis_page_rules.url`|String| The forward rule URL, a required attribute for `forwarding_url` action.|
|`cis_page_rules.status_code`|String| The status code to check for URL forwarding. The required attribute for `forwarding_url` action. Valid values are `301` and `302`. It returns `0` for all other actions.|

## `ibm_cis_range_apps`
{: #cis-range-apps}

Retrieve an information of an {{site.data.keyword.cis_full_notm}} range applications. For more information, about CIS range application, see [getting started with range](/docs/cis?topic=cis-cis-range).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-range-apps-dssample}

```
data "ibm_cis_range_apps" "apps" {
  cis_id    = ibm_cis.instance.id
  domain_id = ibm_cis_domain.example.id
}
```
{: codeblock}

### Input parameters
{: #cis-range-apps-dsinput}

Input parameters are not supported for this data source. 
{: shortdesc}


### Output parameters
{: #cis-range-apps-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id`|String| The range application ID. It is a combination of `<app_id>,<domain_id>,<cis_id>` attributes are concatenated with `:` character.|
|`app_id`| String| The Range application id.|
|`cis_id`| String| The ID of the CIS service instance.|
|`domain_id`|String| The ID of the domain to add the range application.|
|`protocol`| String| The Edge application protocol type. Valid values are `tcp`, `udp`. This attribute specified along with port number. For example, `tcp/22`.|
|`dns`| String| The name of DNS record for the range application.|
|`dns_type`| String| The DNS record type.
|`origin_direct`| String| A list of destination addresses to the origin. IP address and port of the origin for Range application. If configuring a Load Balancer, use `origin_dns` and `origin_port`. This cannot be combined with `origin_dns` and `origin_port`. For example, `tcp://192.0.2.1:22`.
|`ip_firewall`|String| Enables the IP firewall for the application. Only available for `TCP` applications.|
|`proxy_protocol`| String| Allows for the true client IP to be passed to the service. Valid values are `off`, `v1`, `v2`, `simple`. Default value is `off`.|
|`edge_ips_type`| String| The type of edge IP configuration. Valid value and default value is `dynamic`.|
|`edge_ips_connectivity`|String| Specified IP version. Valid values are `ipv4`, `ipv6`, `all`. Default value is `all`.|
|`traffic_type`| String| Configure how traffic is handled at the edge. If set to direct traffic is passed through to the service. In the case of HTTP or HTTPS, HTTPS features at the edge are applied to this traffic. Valid values are `direct`, `http`, `https`. Default value is `direct`.|
|`tls`| String| Configure how TLS connections are terminated at the edge. Valid values are `off`, `flexible`, `full`, `strict`. Default value is `off`.|


## `ibm_cis_waf_groups`
{: #cis-waf-groups}

Import the details of an existing {{site.data.keyword.cis_full_notm}} WAF rule groups. For more information, about WAF refer to [Web Application Firewall concepts](/docs/cis?topic=cis-waf-q-and-a).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-waf-groups-dssimple}

```
data "ibm_cis_waf_groups" "waf_groups" {
  cis_id     = data.ibm_cis.cis.id
  domain_id  = data.ibm_cis_domain.cis_domain.id
  package_id = "c504870194831cd12c3fc0284f294abb"
}
```
{: codeblock}

### Input parameters
{: #cis-waf-groups-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`cis_id`|String|Required| The resource CRN ID of the CIS on which zones were created.|
|`domain_id`|String|Required|The ID of the domain to retrieve the Load Balancers. |
|`package_id`|String|Required|The WAF Rule Package ID. |

### Output parameters
{: #cis-waf-groups-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`name`|String| The name of the  WAF rule group.|
|`group_id`|String| The WAF group ID.|
|`mode` |String| The `on`, `off` mode setting of the WAF rule group.|
|`description` |String| The WAF rule group description.|
|`rules_count`|String|  Number of rules in WAF Group.|
|`modified_rules_count`|String|  Number of rules modified in WAF Group.|

## `ibm_cis_waf_packages`
{: #cis-waf-packages}

Import the details of an existing {{site.data.keyword.cis_full_notm}} WAF package resource. For more information, about WAF refer to [CIS rule sets](/docs/cis?topic=cis-waf-settings).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-waf-packages-dssimple}

```
data "ibm_cis_rate_limit" "ratelimit" {
    cis_id = data.ibm_cis.cis.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
}
```
{: codeblock}

### Input parameters
{: #cis-waf-packages-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`cis_id`|String|Required| The ID of the {{site.data.keyword.cis_full_notm}} service instance.|
|`domain_id`|String|Required|The ID of the domain. |

### Output parameters
{: #cis-waf-packages-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`id`|String| The ID of resource. It is the combination of `<package_id>:<domain_id>:<cis_id>`.|
|`description`|String|  The WAF package description.|
|`package_id`|String| The WAF package ID.|
|`detection_mode`|String| The WAF package detection mode.|


## `ibm_cis_waf_rules`
{: #cis-waf-rules}

Import the details of an existing {{site.data.keyword.cis_full_notm}} WAF rules resource. For more information, see [CIS rule sets](/docs/cis?topic=cis-waf-settings#cis-ruleset-for-waf).
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #cis-waf-rules-dssimple}

```
data "ibm_cis_waf_rules" "rules" {
		cis_id    = data.ibm_cis.cis.id
		domain_id = data.ibm_cis_domain.cis_domain.id
		package_id = "1e334934fd7ae32ad705667f8c1057aa"
}
```
{: codeblock}

### Input parameters
{: #cis-waf-rules-dsinput}

Review the input parameters that you can specify for your data source. 
{: shortdesc}

|Name|Data type|Required/optional|Description|
|----|-----------|------|--------|
|`cis_id`|String|Required| The ID of the {{site.data.keyword.cis_full_notm}} service instance.|
|`domain_id`|String|Required|The ID of the domain to add the rate limit rule. |
|`package_id`|String|Required|The ID of WAF rule package. |

### Output parameters
{: #cis-waf-rules-dsoutput}

Review the output parameters that you can access after you retrieved your data source. 
{: shortdesc}

|Name|Data type|Description|
|----|-----------|----------|
|`waf_rules`|List| The list of WAF rules. |
|`waf_rules.id`|String| It is a combination of `<rule_id>,<package_id>,<domain_id>,<cis_id>` attributes concatenated with `:` character. |
|`waf_rules.rule_id`|String| The ID of WAF rule package.|
|`waf_rules.package_id`|String| The ID of WAF rule package.|
|`waf_rules.mode`|String| The mode setting that can be set only once. Valid values are `on`, `off`, `default`, `disable`, `simulate`, `block`, `challenge`.|
|`waf_rules.description`|String| The WAF rule description.|
|`waf_rules.priority`|String| The WAF rule priority.|
|`waf_rules.group`|String| The WAF rule group.|
|`waf_rules.group.id`|String| The WAF rule group ID.|
|`waf_rules.group.name`|String| The name of the WAF rule group.|
|`waf_rules.allowed_modes`|String| The allowed modes for setting the WAF rule mode.|
