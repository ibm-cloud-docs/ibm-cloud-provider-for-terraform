---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-22"

keywords: terraform provider deployment, automation, schematics workspace, ibm cloud terraform provider deployment, schematics workspace creation, auto deploy 

subcollection: ibm-cloud-provider-for-terraform

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:step: data-tutorial-type='step'}


# Creating a deployment to IBM Cloud Schematics link
{: #create_deploy_to_schematics}

The deployment to {{site.data.keyword.cloud_notm}} link is an efficient way to share your public Git repository so that other people can to create workspace by using Schematics without affecting your original code. The link requires minimal configuration and you can insert it anywhere that supports markup. If you click the hyper link, the configuration for the Schematic workspace is setup and you need to only click create button for workspace creation in Schematics.
{: shortdesc}

The following steps help to create a deployment to Terraform v0.12 provider template example in {{site.data.keyword.bplong_notm}}.

1. Create a template example by using Terraform provider and publish in the public Git repository. To create example, refer [Sample template example](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples){: external}.
2. Copy the public Git repository URL, for example, `https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway`.
3. Use this syntax to auto deploy the Schematics workspace creation in the {{site.data.keyword.cloud_notm}}.

  **Syntax**

  ```
  https://cloud.ibm.com/schematics/workspaces/create?repository=<template public Git repository example url>&terraform_version=<terraform_v0.xx>
  ```
  {: pre}

  **Example**

  ```
  https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway&terraform_version=terraform_v0.12
  ```
  {: pre}

  The URL contains two parameters, first parameter is provided with the workspace name as `ibm-api-gateway` and second parameter is provided with the Terraform version as `terraform_v0.12`. For more information, about the parameters refer to this example, `https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/<ibm-api-gateway>.&<terraform_version=terraform_v0.12>`. If you do not provide any parameters of ignore one parameter, the `Deploy to {{site.data.keyword.cloud_notm}}` link defaults to the repository's master branch. You can provide the Terraform version parameter that you are using.
  {: important}

4. You can copy, and paste the example URL in the browser to view the {{site.data.keyword.cloud_notm}} Schematics workspace UI with the create button is display.
5. Cross-check the parameters in the workspace UI and click `Create` button.

## Adding an image on deployment to {{site.data.keyword.cloud_notm}} hyperlink
{: #add_an_image}

You can add an image on `Deploy to {{site.data.keyword.cloud_notm}} Schematics` text by using the following syntax and example.

**Syntax**
```
<a href="https://cloud.ibm.com/schematics/workspaces/create?repository=<public Git repository example URL>/<workspace name>&terraform_version=terraform_xx">Deploy to {{site.data.keyword.bplong_notm}} <img src=<image location>></a>
```
{: pre}

**Example**

```
<a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway&terraform_version=terraform_v0.12">Deploy to {{site.data.keyword.cloud_notm}}<img src="/images/deploytoschematics.png"></a>
```
{: pre}

**Output**

<img src="/images/deploytoschematics.png" alt="Deploy to {{site.data.keyword.cloud_notm}}" width="200" style="width: 200px; border-style: none"/>

To view about the sample Terraform template examples, refer [Sample Terraform templates and deploy to {{site.data.keyword.bplong_notm}}](/docs/terraform?topic=terraform-sample_terraformtemplates#api-gwy-template).

