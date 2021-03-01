---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-01"

keywords: install Terraform cli, set up Terraform cli, ibm cloud provider plugin, Terraform

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



# Setting up your environment
{: #setup_cli}

Before you automate and provision your {{site.data.keyword.cloud_notm}} resource, you must install the Terraform and the {{site.data.keyword.cloud_notm}} Provider plug-in.
{: shortdesc}

## Installing the Terraform
{: #install_cli}

You can use Terraform to manage {{site.data.keyword.cloud_notm}} resources. Terraform works with multi-cloud providers, a cloud provider is responsible to provision and expose the resources in the cloud.
{: shortdesc}

### Terraform v0.12 and v0.13 installation
{: #tf_installation}

IBM Cloud provider supports Terraform v0.12, and v0.13. You can complete the following steps to install Terraform v0.12 and Terraform v0.13 on your local machine.
{: shortdesc}

1. Create a `terraform` folder on your local machine, and navigate to your `terraform` folder. 

   ```
    mkdir terraform && cd terraform
   ```
   {: codeblock}
2. Download the specific [Terraform version](https://releases.hashicorp.com/terraform){: external}.
3. Extract the Terraform `zip` file and copy the files to your `terraform` directory. 
4. Set the environment `PATH` variable to your Terraform files.

   ```
   export PATH=$PATH:$HOME/terraform
   ```
   {: codeblock}
5. Verify that the installation is successful by using a `terraform` command.
   ```
   terraform
   ```
   {: codeblock}

   **Output:**

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

      To migrate from the Terraform v0.12 to Terraform v0.13, see [Upgrading Terraform version](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-migration-versioncontrol#tf-0.1x-migration).


## Installing the {{site.data.keyword.cloud_notm}} provider plug-in for Terraform
{: #install_provider}

After the Terraform installation is complete. You need to configure the {{site.data.keyword.cloud_notm}} provider plug-in for Terraform to provision and expose the resources. {{site.data.keyword.cloud_notm}} provider supports plug-in to support Terraform v0.12.x, v0.13.x, and higher version.
{: shortdesc}

### Terraform v0.13.x and higher
{: #install-provider-v13}

Complete the following steps to configure the {{site.data.keyword.cloud_notm}} provider plug-in for Terraform v0.12 and Terraform v0.13.
{: shortdesc}

You need not explicitly download the `plugins` for Terraform v0.13.x and higher version.
{: note}

Create a `versions.tf` file, and add the shared Terraform block by specifying the right Terraform provider version in `version` parameter to automatically provision the plug-ins for Terraform v0.13.x and higher version.

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
{: codeblock}

Terraform supports `version` constraints to specify the range of acceptable versions to initialize. The version syntax format is specified as `<MAJOR_VERSION>.<MINOR_VERSION>.<PATCH>`. You can use the following operators:

|Operator|Description|
|-------|---------|
| `= (or no operator)`| Allows only extract version number. You cannot combine with other conditions. For example, `1.21.0`.|
| `!=` | Excludes an exact version number. For example, `!=1.19.0`.|
| `>, >=, <, <=` | Compares against a specified version, allows version for which the comparison is true. `Greater-than` requests newer version, and `less-than` requests older versions. For example, `>= 1.20.0 < 2.0.0`.|
| `~>` | Allows only the rightmost version component to increment. For example, `~> 1.20.0` allows new patch releases within a specific minor patch releases like `1.20.1, 1.20.2, 1.20.3`, but not `1.21.0` release.|




**Example**

```
 terraform {
   required_providers {
      ibm = {
         source = "IBM-Cloud/ibm"
         version = "1.20.0"
      }
    }
  }
```
{: codeblock}

If you are using Terraform modules, the shared Terraform block should be used in all the module folders. You can refer the Terraform provider block from the [provider registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest){: external}.
{: note}

### Terraform v0.12.x
{: #install-provider-v12}

Complete the following steps to configure the {{site.data.keyword.cloud_notm}} provider plug-in for Terraform v0.12.

1. Download the latest version of the [{{site.data.keyword.cloud_notm}} provider plug-in](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.
2. Extract the `zip` file and retrieve the files.
3. Create a `plugins` hidden folder.
   ```
    mkdir -p $HOME/.terraform.d/plugins
   ```
   {: codeblock}
4. Move the {{site.data.keyword.cloud_notm}} provider plug-in into your `plugins` folder.
   ```
   mv $HOME/<DOWNLOAD_FOLDER_NAME>/terraform-provider-ibm* $HOME/.terraform.d/plugins
   ```
   {: codeblock}
5. Navigate to your `plugin` hidden folder and verify that the installation is complete.
   ```
   cd $HOME/.terraform.d/plugins && ./terraform-provider-ibm_*
   ```
   {: codeblock}

## Configuring the {{site.data.keyword.cloud_notm}} provider plug-in
{: #configure_provider}

As Terraform supports multiple cloud providers, you must specify `ibm` as your {{site.data.keyword.cloud_notm}} provider and configure the plug-in with all required parameters for the resource or data source category that you want to provision.
{: shortdesc}

1. Review the required [input parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) for the resource or data source category that you want to use and retrieve these parameters by using the [Supported input parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#provider-parameter-ov) documentation.
2. Optional. Create a directory on your local machine for your Terraform on {{site.data.keyword.cloud_notm}} project and navigate into the directory. This directory is used to store all Terraform on {{site.data.keyword.cloud_notm}} configuration files, the provider configuration, and variable definitions. If you have an existing directory that you want to use, navigate into your existing directory.
   ```
   mkdir myproject && cd myproject
   ```
   {: codeblock}
3. Create a local Terraform on {{site.data.keyword.cloud_notm}} variables file that is named `terraform.tfvars` to store the credentials and other input parameters that you retrieved earlier. When you initialize the Terraform on {{site.data.keyword.cloud_notm}} CLI, all variables that are defined in this file are automatically loaded by Terraform on {{site.data.keyword.cloud_notm}} and you can reference them in every Terraform on {{site.data.keyword.cloud_notm}} configuration file in the same directory. 

   The `terraform.tfvars` file contains confidential information, do not push this file to your version control system where you store the Terraform on {{site.data.keyword.cloud_notm}} configuration files of the resources that you want to provision. The `terraform.tfvars` file is meant to be on your local system only. 
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
   <caption>The configuration file parameters</caption>
   <thead>
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

4. Create a Terraform on {{site.data.keyword.cloud_notm}} provider configuration file named `provider.tf`. Use this file to specify `ibm` as your cloud provider to reference the credentials from your `terraform.tfvars` file. To reference a variable, declare the variable first, and then retrieve the value of the variable by using Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax.

   The {{site.data.keyword.cloud_notm}} provider offers a flexible methods of providing credentials for authentication. The following two methods are supported.

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
      {: codeblock}

     **Environment variables**

      You can provide your credentials by exporting the `IC_API_KEY`, `IAAS_CLASSIC_USERNAME`, and `IAAS_CLASSIC_API_KEY` environment variables, representing your {{site.data.keyword.cloud_notm}} platform API key, {{site.data.keyword.cloud_notm}} Classic Infrastructure (SoftLayer) user name, and {{site.data.keyword.cloud_notm}} infrastructure API key. The provider block with the empty definition overrides the credentials set through the environment variables.
      {: shortdesc}

      ```
      provider "ibm" {}
      ```
      {: codeblock}

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

5. After you configured the provider with all required input parameters, you can now start [provisioning {{site.data.keyword.cloud_notm}} resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-manage_resources#provision_resources). 

