---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-22"

keywords: install Terraform cli, set up Terraform cli, ibm cloud provider plugin, Terraform

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


# Setting up the CLI and preparing your environment
{: #setup_cli}

Before you can automate your {{site.data.keyword.cloud_notm}} resource provisioning, you must install the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in.
{: shortdesc}

## Installing the Terraform on {{site.data.keyword.cloud_notm}} CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #install_cli}

To use Terraform on {{site.data.keyword.cloud_notm}} to manage {{site.data.keyword.cloud_notm}} resources, you must install the Terraform on {{site.data.keyword.cloud_notm}} CLI and the {{site.data.keyword.cloud_notm}} provider plug-in for Terraform on {{site.data.keyword.cloud_notm}}. 
{: shortdesc}

**What is the {{site.data.keyword.cloud_notm}} Provider plug-in and why do I need it?**</br>
To support a multi-cloud approach, Terraform on {{site.data.keyword.cloud_notm}} works with cloud providers. A cloud provider is responsible for understanding the resources that you can provision, their API, and the methods to expose these resources in the cloud. To provision resources in {{site.data.keyword.cloud_notm}}, you must install the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on {{site.data.keyword.cloud_notm}}. The plug-in is aware of the {{site.data.keyword.cloud_notm}} resources that you can provision with Terraform on {{site.data.keyword.cloud_notm}} and the syntax to describe them.  

1. Install Terraform on {{site.data.keyword.cloud_notm}} on your local machine. 
   1. Create a folder on your local system that is called `terraform` and navigate into your folder. 
      ```
      mkdir terraform && cd terraform
      ```
      {: pre}

   2. [Download the Terraform on {{site.data.keyword.cloud_notm}} CLI version 0.12.x to your local machine ![External link icon](../icons/launch-glyph.svg "External link icon")](https://releases.hashicorp.com/terraform/). 
   3. Extract the Terraform on {{site.data.keyword.cloud_notm}} package and copy the binary file into your `terraform` directory. 
   4. Point the `$PATH` environment variable to your Terraform on {{site.data.keyword.cloud_notm}} binary file.
      ```
      export PATH=$PATH:$HOME/terraform
      ```
      {: pre}
      
   5. Verify that the installation is successful by using a `terraform` command.
      ```
      terraform
      ```
      {: pre}
      
      Example output: 
      ```
      Usage: terraform [-version] [-help] <command> [args]

      The available commands for execution are listed below.
      The most common, useful commands are shown first, followed by less common or more advanced commands. If you're just getting started with Terraform on {{site.data.keyword.cloud_notm}}, stick with the common commands. For the other commands, please read the help and Docs  before usage.

      Common commands:
          apply              Builds or changes infrastructure
          console            Interactive console for Terraform on {{site.data.keyword.cloud_notm}} interpolations
          destroy            Destroy Terraform on {{site.data.keyword.cloud_notm}}-managed infrastructure
          env                Workspace management
          fmt                Rewrites config files to canonical format
          get                Download and install modules for the configuration
          graph              Create a visual graph of Terraform on {{site.data.keyword.cloud_notm}} resources
          import             Import existing infrastructure into Terraform on {{site.data.keyword.cloud_notm}}
          init               Initialize a Terraform on {{site.data.keyword.cloud_notm}} working directory
          output             Read an output from a state file
          plan               Generate and show an execution plan
          providers          Prints a tree of the providers used in the configuration
          push               Upload this Terraform on {{site.data.keyword.cloud_notm}} module to Atlas to run
          refresh            Update local state file against real resources
          show               Inspect Terraform on {{site.data.keyword.cloud_notm}} state or plan
          taint              Manually mark a resource for recreation
          untaint            Manually unmark a resource as tainted
          validate           Validates the Terraform on {{site.data.keyword.cloud_notm}} files
          version            Prints the Terraform on {{site.data.keyword.cloud_notm}} version
          workspace          Workspace management

      All other commands:
          debug              Debug output management (experimental)
          force-unlock       Manually unlock the Terraform on {{site.data.keyword.cloud_notm}} state
          state              Advanced state management
      ```
      {: screen}  

2. Install the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on {{site.data.keyword.cloud_notm}}.

   **Install provider for Terraform on {{site.data.keyword.cloud_notm}} v0.13**

   You can use the provided function block to use the IBM Terraform on {{site.data.keyword.cloud_notm}} provider registry to support Terraform on {{site.data.keyword.cloud_notm}} version 0.13.0

    **Syntax**

     ```
     terraform {
        required_providers {
         ibm = {
           source = "IBM-Cloud/ibm"
           version = "<provider version>"
         }
        }
     }
     ```
     {: pre}

    **Example**

     ```
     terraform {
        required_providers {
           ibm = {
              source = "IBM-Cloud/ibm"
               version = "1.14.0"
              }
         }
      }
      ```
      {: pre}
   
   If you want to explicitly place the provider in your system location. You need to follow the steps provided in the Terraform on {{site.data.keyword.cloud_notm}} provider, For more information about Terraform on {{site.data.keyword.cloud_notm}} v0.13 plug-in download, refer to [Explicit provider](https://www.terraform.io/upgrade-guides/0-13.html#explicit-provider-source-locations){: external}.
   {: note}

   **Install provider for Terraform on {{site.data.keyword.cloud_notm}} v0.12**

    1. [Download the latest version of the {{site.data.keyword.cloud_notm}} Provider binary package ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/terraform-provider-ibm/releases). 
    2. Extract the {{site.data.keyword.cloud_notm}} provider package to retrieve the binary file.
    3. Create a hidden folder for your plug-in. The {{site.data.keyword.cloud_notm}} Provider plug-in is used only by the Terraform on {{site.data.keyword.cloud_notm}} CLI and is not meant to be accessed by the user.  
      ```
      mkdir -p $HOME/.terraform.d/plugins
      ```
      {: pre}
    4. Move the {{site.data.keyword.cloud_notm}} Provider plug-in into your hidden folder. 
      ```
      mv $HOME/Downloads/terraform-provider-ibm* $HOME/.terraform.d/plugins
      ```
      {: pre}
    5. Navigate into your hidden directory and verify that the installation is complete. 
      ```
      cd $HOME/.terraform.d/plugins && ./terraform-provider-ibm_*
      ```
      {: pre}
      
      Example output: 
      ```
      2018/09/25 17:30:14 {{site.data.keyword.cloud_notm}} Provider version 0.11.3  fdc4aa0f0547177f3ea8b14c7a58a849e240f64a
      This binary is a plugin. These are not meant to be executed directly.
      Please execute the program that consumes these plugins, which loads any plugins automatically
      ```
      {: screen}
      
## Configuring the provider plug-in
{: #configure_provider}

Because Terraform on {{site.data.keyword.cloud_notm}} supports multiple cloud providers, you must specify IBM as your cloud provider and configure the plug-in with all required parameters for the resource or data source category that you want to use. 
{: shortdesc}

1. Review the required [input parameters](/docs/terraform?topic=terraform-provider-reference#required-parameters) for the resource or data source category that you want to use and retrieve these parameters by using the [Supported input parameters](/docs/terraform?topic=terraform-provider-reference#provider-parameter-ov) documentation.

2. Optional. Create a directory on your local machine for your Terraform on {{site.data.keyword.cloud_notm}} project and navigate into the directory. This directory is used to store all Terraform on {{site.data.keyword.cloud_notm}} configuration files, the provider configuration, and variable definitions. If you have an existing directory that you want to use, navigate into this directory. 
   ```
   mkdir myproject && cd myproject
   ```
   {: pre}  
   
3. Create a local Terraform on {{site.data.keyword.cloud_notm}} variables file that is named `terraform.tfvars` to store the credentials and other input parameters that you retrieved earlier. When you initialize the Terraform on {{site.data.keyword.cloud_notm}} CLI, all variables that are defined in this file are automatically loaded by Terraform on {{site.data.keyword.cloud_notm}} and you can reference them in every Terraform on {{site.data.keyword.cloud_notm}} configuration file in the same directory. 

   Because the `terraform.tfvars` file contains confidential information, do not push this file to your version control system where you store the Terraform on {{site.data.keyword.cloud_notm}} configuration files of the resources that you want to provision. The `terraform.tfvars` file is meant to be on your local system only. 
   {: important}
   
   Example `terraform.tfvars` file:
   ```
   ibmcloud_api_key = "<ibmcloud_api_key>"
   iaas_classic_username = "<classic_infrastructure_username>"
   iaas_classic_api_key = "<classic_infrasturcture_apikey>"
   region = "<region>"
   ```
   {: codeblock}
   
   <table>
   <caption>Understanding the configuration file components</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the configuration file components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>ibmcloud_api_key</code></td>
   <td>Enter your {{site.data.keyword.cloud_notm}} API key. </td>
   </tr>
   <tr>
   <td><code>iaas_classic_username</code></td>
   <td>Enter your {{site.data.keyword.cloud_notm}} classic infrastructure user name.  </td>
   </tr>
   <tr>
   <td><code>iaas_classic_api_key</code></td>
   <td>Enter your {{site.data.keyword.cloud_notm}} classic infrastructure API key. </td>
   </tr>
   <tr>
   <td><code>region</code></td>
   <td>Enter the {{site.data.keyword.cloud_notm}} region where you want to provision your resources. </td>
   </tr>
   </tbody>
   </table>

4. create a Terraform on {{site.data.keyword.cloud_notm}} provider configuration file that is named `provider.tf`. Use this file to specify IBM as your cloud provider and to reference the credentials from your `terraform.tfvars` file. To reference a variable, declare the variable first, and then retrieve the value of the variable by using Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax.

   The {{site.data.keyword.cloud_notm}} provider offers a flexible means of providing credentials for authentication. The following two methods are supported.

    - Static credentials
    - Environment variables

     **Static credentials**

      You can provide your static credentials by adding the `ibmcloud_api_key`, `iaas_classic_username`, and `iaas_classic_api_key` arguments in the {{site.data.keyword.cloud_notm}} provider block.

      ```
      provider "ibm" {
          ibmcloud_api_key = ""
          iaas_classic_username = ""
          iaas_classic_api_key = ""
         }
       ```
      {: pre}

     **Environment variables**

      You can provide your credentials by exporting the `IC_API_KEY`, `IAAS_CLASSIC_USERNAME`, and `IAAS_CLASSIC_API_KEY` environment variables, representing your {{site.data.keyword.cloud_notm}} platform API key, {{site.data.keyword.cloud_notm}} Classic Infrastructure (SoftLayer) user name, and {{site.data.keyword.cloud_notm}} infrastructure API key. The provider block with the empty definition overrides the credentials set through the environment variables.
      {: shortdesc}

      ```
       provider "ibm" {}
      ```
      {: pre}

       **Usage**

      ```
       $ export IC_API_KEY="ibmcloud_api_key"
       $ export IAAS_CLASSIC_USERNAME="iaas_classic_username"
       $ export IAAS_CLASSIC_API_KEY="iaas_classic_api_key"
       $ terraform plan
      ```
      {: pre}

   To create or find your `ibmcloud_api_key`, refer to [API key](/docs/account?topic=account-userapikey#create_user_key). 
   To create or find your `iaas_classic_username` with the VPN credentials, refer to [VPN credentials](/docs/account?topic=account-vpnpassword).
   {: note}

5. After you configured the provider with all required input parameters, you can now start [provisioning {{site.data.keyword.cloud_notm}} resources](/docs/terraform?topic=terraform-manage_resources#provision_resources). 

