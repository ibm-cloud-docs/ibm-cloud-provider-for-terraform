---

copyright:
  years: 2017, 2022
lastupdated: "2022-03-08"

keywords: Add resources, remove resources, iaas, softlayer, ibm cloud resources, ibm cloud services, Terraform on IBM Cloud, provision resources

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# Migrating and version controlling
{: #migration-versioncontrol}

IBM continually updates the Terraform on IBM Cloud provider to give you higher levels of performance and being up-to-date. Some instances aren't able to be upgraded, so they must be closed and you must migrate your resources with the right version.

View the versions that are associated in the Terraform and the {{site.data.keyword.cloud_notm}} provider plug-in.
{: shortdesc}

## Upgrading the Terraform} version
{: #tf-0.1x-migration}

You can upgrade your Terraform version from `Terraform v0.12 to Terraform v0.13`. With the release of Terraform v0.13, the syntax for configuration files have changed.
{: shortdesc}

To upgrade the Terraform template from the old version to the latest version, refer to [Upgrading the Terraform template version](/docs/schematics?topic=schematics-migrating-terraform-version).
{: important}

Complete the following steps to upgrade your configuration files: 

1. Follow the [instructions](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli) to install existing Terraform with the latest version of the Terraform.
2. Copy your existing Terraform version configuration files into your Terraform working directory. 
    ```sh
    mv <tf_config_file_path> $HOME/terraform
    ```
    {: codeblock}

3. Use the Terraform upgrade command to automatically apply the new syntax to your Terraform configuration files. 

    **Syntax**
    ```sh
    terraform <0.xx>upgrade
    ```
    {: codeblock}

    **Example to upgrade Terraform v0.12 to Terraform v0.13**
    ```sh
    terraform 0.13upgrade
    ```
    {: codeblock}

    Example output: 
    ```text
    This command rewrites the configuration files in the given directory to
    use the new syntax features from Terraform on IBM Cloud v0.12, and identify
    any constructs that may need to be adjusted for correct operation with
    Terraform on IBM Cloud v0.13.

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

    ```terraform
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

    ```terraform
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

This completes your Terraform version upgrade.

## Version control 
{: #versions}

The versions that are associated with the resources and data sources are:

- IBM Cloud Provider plug-in for Terraform. For more information, see [Provider version releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.
- Terraform. For more information, see [Terraform version](https://releases.hashicorp.com/terraform/){: external}.

With the release of Terraform version 0.12, the syntax for configuration files changed. If you want to run your infrastructure code by using Terraform version 0.12, you must first refer to refer to [Upgrading the Terraform template version](/docs/schematics?topic=schematics-migrating-terraform-version).
{: important}




