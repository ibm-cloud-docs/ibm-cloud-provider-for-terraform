---

copyright:
  years: 2017, 2021
lastupdated: "2021-12-11"

keywords: terraform provider deployment, automation, schematics workspace, ibm cloud terraform provider deployment, schematics workspace creation, auto deploy 

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# Creating a deployment to IBM Cloud Schematics link
{: #create_deploy_to_schematics}

The deploy to {{site.data.keyword.cloud_notm}} URL is an efficient way for you to enable users to deploy solutions on {{site.data.keyword.cloud_notm}} from a public Git repository sample configuration. The URL requires minimal configuration and you can insert it anywhere in your documentation that supports markup. When the user clicks the hyper link, they are taken directly to the {{site.data.keyword.bpshort}} workspace setup page and only need to click the create button for workspace creation in {{site.data.keyword.bpshort}}.

The following steps show how to create a URL to deploy to Terraform v0.12 template example in {{site.data.keyword.bplong_notm}}.
{: shortdesc}

1. Create a template example by using Terraform on {{site.data.keyword.cloud_notm}} provider and publish in the public Git repository. To create example, see [Sample template](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples){: external}.
2. Copy the public Git repository URL, for example, `https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway`.
3. Use this syntax to auto deploy the Schematics workspace creation in the {{site.data.keyword.cloud_notm}}.

    **Syntax**

    ```text
    https://cloud.ibm.com/schematics/workspaces/create?repository=<template public Git repository example url>&terraform_version=<terraform_v0.xx>
    ```
    {: pre}

    **Example**

    ```text
    https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway&terraform_version=terraform_v0.12
    ```
    {: pre}

    The URL contains two parameters, first parameter is provided with the workspace name as `ibm-api-gateway` and second parameter is provided with the Terraform on {{site.data.keyword.cloud_notm}} version as `terraform_v0.12`. For more information, about the parameters refer to this example, `https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/<ibm-api-gateway>.&<terraform_version=terraform_v0.12>`. If you do not provide any parameters or ignore one parameter, the `Deploy to {{site.data.keyword.cloud_notm}}` link defaults to the repository's master branch. You can provide the Terraform on {{site.data.keyword.cloud_notm}} version parameter that you are using.
    {: important}

4. You can copy, and paste the example URL in the browser to view the {{site.data.keyword.cloud_notm}} Schematics workspace console with the create button is displayed.
5. Cross-check the parameters in the workspace console and click `Create` button.

## Adding an image on deployment to {{site.data.keyword.cloud_notm}} hyperlink
{: #add_an_image}

You can add an image on `Deploy to {{site.data.keyword.cloud_notm}} Schematics` text by using the following syntax and example.

**Syntax**
```html
<a href="https://cloud.ibm.com/schematics/workspaces/create?repository=<public Git repository example URL>/<workspace name>&terraform_version=terraform_xx">Deploy to {{site.data.keyword.bplong_notm}} <img src=<image location>></a>
```
{: pre}

**Example**

```html
<a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway&terraform_version=terraform_v0.12">Deploy to {{site.data.keyword.cloud_notm}}<img src="/images/deploytoschematics.png"></a>
```
{: pre}

**Output:**

![Deploy to {{site.data.keyword.cloud_notm}}](/images/deploytoschematics.png "Deploy to {{site.data.keyword.cloud_notm}}"){: caption="Deploy to {{site.data.keyword.cloud_notm}}" caption-side="bottom"}

To view about the sample Terraform on {{site.data.keyword.cloud_notm}} template examples, refer [Sample Terraform on {{site.data.keyword.cloud_notm}} templates and deploy to {{site.data.keyword.bplong_notm}}](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway){: external}.



