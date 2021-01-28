---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: terraform provider plugin, terraform api gateway

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



# Certificate Manager data sources
{: #cert-manager-data-sources}

Review the data sources that you can use to retrieve information about the certificates that your manage in Certificate Manager. All data sources are imported as read-only information. You can reference the output parameters for each data source by using Terraform interpolation syntax.

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform configuration file. 
{: important}


## `ibm_certificate_manager_certificate`
{: #cert-manager-certificate}

Retrieve the details of an existing certificate instance resource and lists all the certificates.
{: shortdesc}

### Sample Terraform code
{: #cert-manager-certificate-sample}

```
data "ibm_resource_instance" "cm" {
    name     = "testname"
    location = "us-south"
    service  = "cloudcerts"
}
data "ibm_certificate_manager_certificate" "source_certificate"{
    certificate_manager_instance_id=data.ibm_resource_instance.cm.id
    name = "certificate name"
}
```
{: codeblock}

### Input parameters
{: #cert-manager-certificate-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`certificate_manager_instance_id`|String|Required|The CRN of the Certificate Manager service instance. |
|`name`|String|Required|The display name for the certificate.|

### Output parameters
{: #cert-manager-certificate-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`algorithm`|String|The algorithm that is used for the certificate.| 
|`begins_on`|Timestamp|The timestamp when the certificate was created in UNIX epoch time format.| 
|`certificate_details`|String|List of certificates for the provided name. |
|`certificate_details.cert_id`|String|The CRN based certificate ID. |
|`certificate_details.name`|String|The name of the certificate. | 
|`certificate_details.domains`|Array|A list of domains that the certificate is associated with. The first domain is referred to as the primary domain. Any more domains are referred to as secondary domains.|
|`certificate_details.data`|String|The certificate data. |
|`certificate_details.data.content`|String|The content of certificate data, escaped. |
|`certificate_details.data.priv_key`|String|The private key data, escaped. |
|`certificate_details.data.intermediate`|String| The intermediate certificate data, escaped.|
|`expires_on`|Date|The date when the certificate expires in UNIX epoch time format.|
|`has_previous`|Boolean|If set to **true**, the certificate has a previous version.| 
|`id`|String|The ID of the certificate that is managed in Certificate Manager. The ID is composed of `<certificate_manager_instance_ID>:<certificate_ID>`. |
|`issuer`|String|The issuer of the certificate.|
|`issuance_info`|List of objects|The issuance information of the certificate.| 
|`issuance_info.status`|String|The status of the certificate.|
|`issuance_info.ordered_on`|Date|The date when the certificate was ordered.|
|`issuance_info.code`|String|The code of the certificate.|
|`issuance_info.additional_info`|String|Any more information for the certificate.| 
|`imported`|Boolean|If set to **true**, the certificate is imported. |
|`key_algorithm`|String|The key algorithm of the certificate. |
|`serial_number`|String|The serial number of the certificate.|
|`status`|String|The status of the certificate.|


## `ibm_certificate_manager_certificates`
{: #cert-manager-certificates}

Retrieve the details of one or lists all certificates that are managed by your Certificate Manager service instance resource. 
{: shortdesc}

### Sample Terraform code
{: #cert-manager-certificates-sample}

```
data "ibm_resource_instance" "cm" {
    name     = "testname"
    location = "us-south"
    service  = "cloudcerts"
}
data "ibm_certificate_manager_certificates" "certs"{
    certificate_manager_instance_id=data.ibm_resource_instance.cm.id
}
```
{: codeblock}

### Input parameters
{: #cert-manager-certificates-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`certificate_manager_instance_id`|String|Required|The CRN of the Certificate Manager service instance. |


### Output parameters
{: #cert-manager-certificates-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`algorithm`|String|The Algorithm of a certificate.|
|`begins_on`|String|The creation date of the certificate in UNIX epoch time.|
|`domains`|String| An array of valid domains for the issued certificate. The first domain is the primary domain. extra domains are secondary domains. |
|`expires_on`|String|The expiration date of the certificate in Unix epoch time.|
|`has_previous`|String|Indicates whether a certificate has a previous version.|
|`key_algorithm`|String|The Key Algorithm of a certificate.|
|`name`|String|The display name of the certificate. |
|`id`|String|The ID of the certificate that is managed in Certificate Manager. The ID is composed of `<certificate_manager_instance_ID>:<certificate_ID>`. |
|`issuer`|String|The issuer of the certificate.|
|`issuance_info`|String| The issuance information of a certificate.|
|`issuance_info.status`|String| The status of a certificate.|
|`issuance_info.ordered_on`|String| The certificate ordered date.|
|`issuance_info.code`|String| The code of a certificate.|
|`issuance_info.additional_info`|String| The extra information of a certificate.|
|`imported`|String|Indicates whether a certificate has imported or not.|
|`serial_number`|String| The serial number of a certificate.|
|`status`|String|The status of a certificate.|