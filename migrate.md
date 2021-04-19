---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

keywords: Add resources, remove resources, iaas, softlayer, ibm cloud resources, ibm cloud services, Terraform on {{site.data.keyword.cloud_notm}}, provision resources

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




# Migrating and version controlling
{: #migration-versioncontrol}

IBM continually updates the Terraform on {{site.data.keyword.cloud_notm}} provider to give you higher levels of performance and being up-to-date. Some of the instances aren't able to be upgraded, so they must be closed and you must migrate your resources with the right version.

View the versions that are associated in the Terraform on {{site.data.keyword.cloud_notm}} and the {{site.data.keyword.cloud_notm}} provider plug-in.
{: shortdesc}

## Upgrading the Terraform on {{site.data.keyword.cloud_notm}} version
{: #tf-0.1x-migration}
  
You can upgrade your Terraform on {{site.data.keyword.cloud_notm}}, for example, `Terraform v0.12 to Terraform v0.13`. With the release of Terraform on {{site.data.keyword.cloud_notm}} v0.13, the syntax for configuration files have changed.
{: shortdesc}

Complete the following steps to upgrade your configuration files: 

1. Follow the [instructions](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli) to install existing Terraform on {{site.data.keyword.cloud_notm}} and the latest version of the Terraform on {{site.data.keyword.cloud_notm}}.
2. Copy your existing Terraform on {{site.data.keyword.cloud_notm}} version configuration files into your Terraform on {{site.data.keyword.cloud_notm}} working directory. 
   ```
   mv <tf_config_file_path> $HOME/terraform
   ```
   {: codeblock}
   
3. Use the Terraform on {{site.data.keyword.cloud_notm}} upgrade command to automatically apply the new syntax to your Terraform on {{site.data.keyword.cloud_notm}} configuration files. 
  
   **Syntax**
   ```
   terraform <0.xx>upgrade
   ```
   {: codeblock}

   **Example to upgrade Terraform on {{site.data.keyword.cloud_notm}} v0.12 to Terraform on {{site.data.keyword.cloud_notm}} v0.13**
   ```
   terraform 0.13upgrade
   ```
   {: codeblock}
   
   Example output: 
   ```
   This command rewrites the configuration files in the given directory to
   use the new syntax features from Terraform on {{site.data.keyword.cloud_notm}} v0.12, and identify
   any constructs that may need to be adjusted for correct operation with
   Terraform on {{site.data.keyword.cloud_notm}} v0.13.

   We recommend to use this command in a clean version control work tree, so that
   you can easily see the proposed changes as a diff against the latest commit.
   If you have uncommited changes already present, we recommend aborting this
   command and dealing with them before running this command again.

   Would you like to upgrade the module in the current directory?
     Only 'yes' is accepted to confirm.

     Enter a value: yes

   -----------------------------------------------------------------------------

   Upgrade complete!

   The configuration files were upgraded successfully. Use your version control
   system to review the proposed changes, make any necessary adjustments, and
   then commit.
   ```
   {: screen}

4. Verify `versions.tf` file is generated as shown in the example.

   **Example versions.tf:**

   ```
   terraform {
      required_providers {
        ibm = {
          # TF-UPGRADE-TODO
          #
          # No source detected for this provider. You must add a source address
          # in the following format:
          #
          # source = "your-registry.example.com/organization/ibm"
          #
          # For more information, see the provider source documentation:
          #
          # https://www.terraform.io/docs/configuration/providers.html#provider-source
        }
      }
      required_version = ">= 0.13"
    }
   ```
   {: codeblock}

5. Edit the `versions.tf` configuration file. Comment out `source = "your-registry.example.com/organization/ibm"` parameter and provide source value as `source = "IBM-Cloud/ibm"` as shown in the example. For more information, about the provider registry, see [IBM Cloud provider registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest){: external}.

    **Example versions.tf:**

    ```
    terraform {
      required_providers {
        ibm = {
          # TF-UPGRADE-TODO
          #
          # No source detected for this provider. You must add a source address
          # in the following format:
          #
          source = "IBM-Cloud/ibm"
          #
          # For more information, see the provider source documentation:
          #
          # https://www.terraform.io/docs/configuration/providers.html#provider-source
        }
      }
      required_version = ">= 0.13"
     }
    ```
    {: codeblock}

This completes your Terraform on {{site.data.keyword.cloud_notm}} upgrade.

## Version control 
{: #versions}

The versions that are associated with the resources and data sources are:

- IBM Cloud Provider plug-in for Terraform on {{site.data.keyword.cloud_notm}}. For more information, see [provider version releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.
- Terraform on {{site.data.keyword.cloud_notm}}. For more information, see [Terraform version](https://releases.hashicorp.com/terraform/){: external}.

With the release of Terraform on {{site.data.keyword.cloud_notm}} version 0.12, the syntax for configuration files changed. If you want to run your infrastructure code by using Terraform on {{site.data.keyword.cloud_notm}} version 0.12, you must first [update your configuration files](#tf-0.1x-migration) to apply the new syntax. 
{: important}


