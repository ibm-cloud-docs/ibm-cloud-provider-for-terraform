---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

keywords: install Terraform on {{site.data.keyword.cloud_notm}} cli, set up Terraform on {{site.data.keyword.cloud_notm}} cli, ibm cloud provider plugin, Terraform on {{site.data.keyword.cloud_notm}}

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


# Installing the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #setup_cli}

Install the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform to start automating infrastructure deployments and cloud resource management with Terraform. 
{: shortdesc}

## Installing the Terraform CLI
{: #tf_installation}

Use these steps to install the Terraform CLI. 
{: shortdesc}

The {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform currently supports Terraform version 0.12.x and 0.13.x only. Make sure to select a supported Terraform version. 
{: note}

1. Create a `terraform` folder on your local machine, and navigate to your `terraform` folder. 
   ```
   mkdir terraform && cd terraform
   ```
   {: pre}
   
2. Download the [Terraform version](https://releases.hashicorp.com/terraform){: external} that you want. 
3. Extract the Terraform `zip` file and copy the files to your `terraform` directory. 
4. Set the environment `PATH` variable to your Terraform files.
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

   To upgrade your Terraform templates from Terraform version 0.12 to 0.13, see [Upgrading your Terraform version](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-migration-versioncontrol#tf-0.1x-migration).
   {: tip}
   
6. [Install the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform](#install_provider).

## Installing the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #install_provider}

After the Terraform CLI installation is complete, you must install the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in {{site.data.keyword.cloud_notm}}. 
{: shortdesc}

1. Download the latest version of the [{{site.data.keyword.cloud_notm}} provider plug-in](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.
2. Extract the `zip` file and retrieve the files.
3. Create a hidden `plugins` folder on your local machine.
   ```
   mkdir -p $HOME/.terraform.d/plugins
   ```
   {: pre}
   
4. Move the {{site.data.keyword.cloud_notm}} Provider plug-in into your `plugins` folder.
   ```
   mv $HOME/<DOWNLOAD_FOLDER_NAME>/terraform-provider-ibm* $HOME/.terraform.d/plugins
   ```
   {: pre}
   
5. Navigate to your `plugins` folder and verify that the installation is complete.
   ```
   cd $HOME/.terraform.d/plugins && ./terraform-provider-ibm_*
   ```
   {: pre}
   
   Example output: 
   ```
   2021/04/16 17:00:39 IBM Cloud Provider version 1.23.1  
   This binary is a plugin. These are not meant to be executed directly.
   Please execute the program that consumes these plugins, which will load any plugins automatically
   ```
   {: screen}

