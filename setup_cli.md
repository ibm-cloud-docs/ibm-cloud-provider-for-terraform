---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-08"

keywords: install Terraform on IBM Cloud cli, set up Terraform on IBM Cloud cli, ibm cloud provider plugin, Terraform on IBM Cloud

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Installing the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #setup_cli}

Install the Terraform CLI and invoke the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform to start automating infrastructure deployments and cloud resource management with Terraform. 
{: shortdesc}

## Installing the Terraform CLI
{: #tf_installation}

Use these steps to install the Terraform CLI. 
{: shortdesc}

The {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform currently supports the Terraform stable version `1.1.x`. Make sure to select a supported Terraform version. 
{: note}

1. Create a `terraform` folder on your local machine, and navigate to your `terraform` folder. 
    ```sh
    mkdir terraform && cd terraform
    ```
    {: pre}

2. Download the [Terraform version](https://releases.hashicorp.com/terraform){: external} that you want. 
3. Extract the Terraform `zip` file and copy the files to your `terraform` directory. 
4. Set the environment `PATH` variable to your Terraform files.
    ```sh
    export PATH=$PATH:$HOME/terraform
    ```
    {: pre}

5. Verify that the installation is successful by using a `terraform` command.
    ```sh
    terraform
    ```
    {: pre}

    Example output:
    ```text
    Usage: terraform [-version] [-help] <command> [args]

    The available commands for execution are listed below.
    The most common, useful commands are shown first, followed by
    less common or more advanced commands. If you're just getting
    started with Terraform, stick with the common commands. For the
    other commands, please read the help and docs before usage.

    Common commands:
    apply              Builds or changes infrastructure
    console            Interactive console for Terraform interpolations
    destroy            Destroy Terraform-managed infrastructure
    env                Workspace management
    fmt                Rewrites config files to canonical format
    get                Download and install modules for the configuration
    graph              Create a visual graph of Terraform resources
    import             Import existing infrastructure into Terraform
    init               Initialize a Terraform working directory
    login              Obtain and save credentials for a remote host
    logout             Remove locally-stored credentials for a remote host
    output             Read an output from a state file
    plan               Generate and show an execution plan
    providers          Prints a tree of the providers used in the configuration
    refresh            Update local state file against real resources
    show               Inspect Terraform state or plan
    taint              Manually mark a resource for recreation
    untaint            Manually unmark a resource as tainted
    validate           Validates the Terraform files
    version            Prints the Terraform version
    workspace          Workspace management

    All other commands:
    0.12upgrade        Rewrites pre-0.12 module source code for v0.12
    debug              Debug output management (experimental)
    force-unlock       Manually unlock the terraform state
    push               Obsolete command for Terraform Enterprise legacy (v1)
    state              Advanced state management

    ```
    {: screen}

    To upgrade your Terraform templates from Terraform old version to new version, see [Upgrading your Terraform version](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-migration-versioncontrol#tf-0.1x-migration).
    {: tip}

6. [Install the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform](#install_provider).

## Installing the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #install_provider}

After the Terraform CLI installation is complete, you must set up the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in {{site.data.keyword.cloud_notm}}. 
{: shortdesc}

The setup of the {{site.data.keyword.cloud_notm}} Provider plug-in varies depending on the Terraform version that you want to use. After you complete the set up, you must [configure the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference). 

To upgrade the Terraform template from the old version to the latest version, refer to [Upgrading the Terraform template version](/docs/schematics?topic=schematics-migrating-terraform-version).
{: important}

### Upgrading to Terraform v0.13.x 
{: #install-provider-v13}

To run your Terraform configuration files with Terraform version 0.13.x and higher, installation of the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform is not required. Instead, you create a `versions.tf` file and specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use. For a list of supported versions, see the [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.
{: shortdesc}

Create a `versions.tf` file with the following content and store it in your Git repository or the folder where Terraform is set up. In this file, specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use with the `version` parameter. 

**Syntax**:
```terraform
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

**Example**:
```terraform
terraform {
    required_providers {
        ibm = {
            source = "IBM-Cloud/ibm"
            version = ">= 1.38.1"
        }
    }
}
```
{: codeblock} 

### Specifying Terraform version constraints
{: #terraform-operators}

Terraform supports `version` constraints to specify the range of acceptable versions to initialize. The version syntax format is specified as `<MAJOR_VERSION>.<MINOR_VERSION>.<PATCH>`. You can modify the version constraint operator in this example by using combination of the [supported operators in Terraform](https://www.terraform.io/language/expressions/version-constraints#version-constraint-syntax){: external}. Some of the constraints are shown as an example. 

|Operator|Description|
|-------|---------|
| `= (or no operator)`| Allows only extract version number. You cannot combine with other conditions. For example, `1.31.0`.|
| `!=` | Excludes an exact version number. For example, `!=1.39.0`.|
| `>, >=, <, <=` | Compares against a specified version, allows version for which the comparison is true. `Greater-than` requests newer version, and `less-than` requests older versions. For example, `>= 1.30.0 < 2.0.0`.|
| `~>` | Allows only the rightmost version component to increment. For example, `~> 1.30.0` allows new patch releases within a specific minor patch releases like `1.30.1, 1.30.2, 1.30.3`, but not `1.31.0` release.|
{: caption="Terraform template version operators"}

If you are using Terraform on IBM Cloud modules, you must add a `versions.tf` file in all the module folders. You can refer the Terraform provider block from the [{{site.data.keyword.cloud_notm}} Provider registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest){: external}.
{: note}

### Upgrading Terraform v0.12.x and earlier
{: #install-provider-v12}

Complete the following steps to install the {{site.data.keyword.cloud_notm}} provider plug-in on your local machine.
{: shortdesc}

1. Download the latest version of the [{{site.data.keyword.cloud_notm}} provider plug-in](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.
2. Extract the `zip` file and retrieve the files.
3. Create a hidden `plugins` folder on your local machine.
    ```sh
    mkdir -p $HOME/.terraform.d/plugins
    ```
    {: pre}

4. Move the {{site.data.keyword.cloud_notm}} Provider plug-in into your `plugins` folder.
    ```sh
    mv $HOME/<DOWNLOAD_FOLDER_NAME>/terraform-provider-ibm* $HOME/.terraform.d/plugins
    ```
    {: pre}

5. Navigate to your `plugins` folder and verify that the installation is complete.
    ```sh
    cd $HOME/.terraform.d/plugins && ./terraform-provider-ibm_*
    ```
    {: pre}

    Example output: 
    ```text
    2021/04/16 17:00:39 IBM Cloud Provider version 1.23.1  
    This binary is a plugin. These are not meant to be executed directly.
    Please execute the program that consumes these plugins, which will load any plugins automatically
    ```
    {: screen}

6. [Configure the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference). To view the list of supported {{site.data.keyword.cloud_notm}} Provider versions, refer to [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.
