---

copyright:
  years: 2017, 2024
lastupdated: "2024-09-23"

keywords: terraform provider deployment, automation, schematics workspace, ibm cloud terraform provider deployment, schematics workspace creation, auto deploy

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# Creating a deployment to IBM Cloud Schematics link
{: #create_deploy_to_schematics}

The deploy to {{site.data.keyword.cloud}} URL is an efficient way for you to enable users to deploy solutions on {{site.data.keyword.cloud_notm}} from a public Git repository sample configuration. The URL requires minimal configuration and you can insert it anywhere in your documentation that supports markup. When the user clicks the hyper link, they are taken directly to the {{site.data.keyword.bpshort}} workspace setup page and only need to click the create button for workspace creation in {{site.data.keyword.bpshort}}.

The following steps show how to create a URL to deploy to `Terraform >=1.0.0, <2.0` template example in {{site.data.keyword.bplong_notm}}.
{: shortdesc}

1. Create a template example by using Terraform on IBM Cloud provider and publish in the public Git repository. To create example, see [Sample template](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples){: external}.
2. Copy the public Git repository URL, for example, `https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/app_config_collection`.
3. Use this syntax to auto deploy the {{site.data.keyword.bpshort}} workspace creation in the {{site.data.keyword.cloud_notm}}.

    Syntax

    ```text
    https://cloud.ibm.com/schematics/workspaces/create?repository=<template public Git repository example url>&terraform_version=<terraform_v1.x.x>
    ```
    {: pre}

    Example

    ```text
    https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cis&terraform_version=terraform_v1.6
    ```
    {: pre}

    The URL contains two parameters, first parameter is provided with the workspace name as `ibm-cis` and second parameter is provided with the Terraform version as `terraform_v1.0`. For more information, about the parameters refer to this example, `https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cis&terraform_version=terraform_v1.6`. If you do not provide any parameters or ignore one parameter, the `Deploy to {{site.data.keyword.cloud_notm}}` link defaults to the repository's master branch. You can provide the Terraform version parameter that you are using.
    {: important}

4. You can copy, and paste the example URL in the browser to view the {{site.data.keyword.cloud_notm}} {{site.data.keyword.bpshort}} workspace console with the create button is displayed.
5. Cross-check the parameters in the workspace console and click `Create` button.

## Adding an image on deployment to {{site.data.keyword.cloud_notm}} link
{: #add_an_image}

You can add an image on `Deploy to {{site.data.keyword.cloud_notm}} Schematics` text by using the following syntax and example.

Syntax
```html
<a href="https://cloud.ibm.com/schematics/workspaces/create?repository=<public Git repository example URL>/<workspace name>&terraform_version=terraform_xx">Deploy to IBM Cloud Schematics <img src=<image location>></a>
```
{: pre}

Example

```html
<img src="images/autodeploy_button.png" alt="Deploy to IBM Cloud" usemap="#viewgithubimage_map1t">
<map name="viewgithubimage_map1t">
    <area alt="Deploy to IBM Cloud}" title="Deploy to IBM Cloud" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cis&terraform_version=terraform_v1.6" target="_blank" coords="3,1,140,20" shape="rect">
</map>
```
{: pre}

Output

<img usemap="#deploybutton_map1t" alt="Auto deployment button" src="images/autodeploy_button.png"><map name="deploybutton_map1t" alt="This image leads to create an action.">
    <area alt="Deploy to {{site.data.keyword.cloud_notm}}" title="Deploy to {{site.data.keyword.cloud_notm}}" href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cis&terraform_version=terraform_v1.6" target="_blank" coords="1,3,139,20" shape="rect">
</map>

To view about the sample Terraform template examples, refer [Sample Terraform templates and deploy to {{site.data.keyword.bplong_notm}}](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/app_config_collection){: external}.
