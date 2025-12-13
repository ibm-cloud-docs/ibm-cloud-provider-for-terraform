---

copyright:
  years: 2025
lastupdated: "2025-12-13"

keywords: terraform quickstart, terraform getting started, terraform tutorial

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with Terraform on IBM Cloud
{: #getting-started}

Terraform on IBM Cloud enables predictable and consistent provisioning of {{site.data.keyword.cloud}} platform, services, and VPC infrastructure resources so that you can rapidly build complex, multitier cloud environments, and adopt an Infrastructure as Code (IaC) approach to deploying environments.
{: shortdesc}

An alternative to configuring {{site.data.keyword.cloud}} with the stand-alone Terraform CLI is {{site.data.keyword.bplong_notm}}. {{site.data.keyword.bpshort}} is an easy to use, managed Terraform as a service capability on {{site.data.keyword.cloud}}, with a full featured UI along with CLI and API support. {{site.data.keyword.bpshort}} is integrated with the IBM Cloud Platform, with support for team usage, with locking and centralized state file management, IAM access controls, logging and monitoring. Free to use, it supports many extra features, including drift detection and configuration management with Red Hat Ansible. Get started now with [{{site.data.keyword.bplong_notm}}](/docs/schematics?topic=schematics-getting-started).
{: tip}

Here you learn how to install the Terraform command-line and the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on a local machine, laptop, or server. Then how to configure the provider plug-in to create, update, or delete {{site.data.keyword.cloud_notm}} services with Terraform.

See [{{site.data.keyword.bplong_notm}}](/docs/schematics?topic=schematics-getting-started) if you want to start working with Terraform immediately without installation of the CLI and provider.

Watch the video or follow the steps to install Terraform and configure the IBM Cloud Provider plug-in for Terraform.

![Installing the IBM Cloud provider plug-in for Terraform](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_juwigbeb){: video output="iframe" data-script="none" id="mediacenterplayer" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}

## Installing the Terraform CLI
{: #tf_installation_step}
{: step}

Install Terraform on your machine is by following the [instructions](https://developer.hashicorp.com/terraform/install){: external} provided by [HashiCorp](https://www.hashicorp.com/en/products/terraform){: external}. This guide provides installation steps for major operating systems, including Windows, macOS, and Linux.

Ensure that the Terraform installation directory has been added to your PATH environment variable.
{: note}

Verify that the installation is successful by using the following command.

    ```sh
    terraform -version
    ```
    {: pre}

## Configuring the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #install_provider-step}
{: step}

After the Terraform command-line installation is complete, set up and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

The following steps show how to set up the provider plug-in for Terraform v1.x or higher.

1. In your Terraform installation directory, create a folder for your first Terraform project and navigate into the folder. This folder is used to store all configuration files and variable definitions.

    ```sh
    mkdir myproject && cd myproject
    ```
    {: pre}

2. Create a `versions.tf` file with the following content. In this file, specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use with the `version` parameter for {{site.data.keyword.cloud_notm}} Provider plug-in, and `required_version` to specify the Terraform template version. If no `version` parameter is specified, {{site.data.keyword.cloud_notm}} automatically uses the latest version of the provider. For a list of supported {{site.data.keyword.cloud_notm}} Provider versions, see [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.

    Example with `version` parameter in `versions.tf` file

    ```terraform
    terraform {
        required_providers {
            ibm = {
            source = "IBM-Cloud/ibm"
            version = "<provider_version>"
            }
        }
    }
    ```
    {: codeblock}

    Example with `required_version` parameter in `versions.tf` file

    ```terraform
    terraform {
    required_version = ">=1.0.0, <2.0"
    required_providers {
        ibm = {
        source = "IBM-Cloud/ibm"
        }
    }
    }
    ```
    {: codeblock}

    Example with both `required_version` and `version` parameter in `versions.tf` file

    ```terraform
    terraform {
    required_version = ">=1.0.0, <2.0"
    required_providers {
        ibm = {
        source = "IBM-Cloud/ibm"
        version = "<provider_version>"
        }
    }
    }
    ```
    {: codeblock}

    The version is specified in the following format `<MAJOR_VERSION>.<MINOR_VERSION>.<PATCH>`. You can modify the version constraint operator in this example by using combination of the [supported operators in Terraform](https://developer.hashicorp.com/terraform/language/expressions/version-constraints#version-constraint-syntax){: external}.
    {: tip}

3. [Create or retrieve an {{site.data.keyword.cloud_notm}} API key](/docs/account?topic=account-userapikey&interface=ui). The API key is used to authenticate with the {{site.data.keyword.cloud_notm}} platform and to determine your permissions for {{site.data.keyword.cloud_notm}} services.
4. Create a variables file that is named `terraform.tfvars` and specify the {{site.data.keyword.cloud_notm}} API key that you retrieved. In addition, you can specify the region where you want your {{site.data.keyword.cloud_notm}} resources to be created. If no region is specified, Terraform on IBM Cloud automatically creates your resources in the `us-south` region. Variables that are defined in the `terraform.tfvars` file are automatically loaded by Terraform when the {{site.data.keyword.cloud_notm}} Provider plug-in is initialized and you can reference them in every Terraform configuration file that you use.

    Because the `terraform.tfvars` file contains confidential information, do not push this file to a version control system. This file is meant to be on your local system only.
    {: important}

    Example of `terraform.tfvars` file

    ```terraform
    ibmcloud_api_key = "<ibmcloud_api_key>"
    region = "<region>"
    ```
    {: codeblock}

5. Create a providers file to configure your endpoint URLs, cloud regions, or other settings before Terraform can use them, so that Terraform can install and use them in the [provider configuration](https://developer.hashicorp.com/terraform/language/providers/configuration){: external} file that is named `providers.tf`. Use this file to configure the {{site.data.keyword.cloud_notm}} Provider plug-in with the {{site.data.keyword.cloud_notm}} API key from your `terraform.tfvars` file. The plug-in uses this key to access {{site.data.keyword.cloud_notm}} and to work with your {{site.data.keyword.cloud_notm}} service. To access a variable value from the `terraform.tfvars` file, you must first declare the variable in the `providers.tf` file and then reference the variable by using the `var.<variable_name>` syntax.

    Example of `providers.tf` file

    ```terraform
    variable "ibmcloud_api_key" {}
    variable "region" {}

    provider "ibm" {
        ibmcloud_api_key   = var.ibmcloud_api_key
        region = var.region
        }
    ```
    {: codeblock}

    **Classic infrastructure, Functions, Power Systems**: Extra parameters are required when configuring the {{site.data.keyword.cloud_notm}} Provider plug-in. To find sample configurations for these services, see [Specifying the `provider` block](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#provider-example).
    {: tip}

## Testing your configuration
{: #test-terraform-template}
{: step}

Now that you have configured the {{site.data.keyword.cloud_notm}} Provider plug-in for your resource, you can start by using Terraform on IBM Cloud to initialize, execute plan, and apply commands to provision the resource. For more information about Terraform commands to test your configuration, see [Provisioning IBM Cloud resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-manage_resources#provision_resources).
{: shortdesc}

Explore [Terraform IBM Modules](https://github.com/terraform-ibm-modules){: external} along with the complete Terraform configuration files to test. Review the module [code structure](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-tim-structure) and follow the deployment instructions provided [here](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-deploy-tim-module).

For an overview of the Terraform resources and data sources that you can use, see the [Terraform on {{site.data.keyword.cloud_notm}} resources and data sources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external}.
