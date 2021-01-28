---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-28"

keywords: Add resources, remove resources, iaas, softlayer, ibm cloud resources, ibm cloud services, Terraform, provision resources

subcollection: ibm-cloud-provider-for-terraform

---

{[METADATA_ATTRIBUTES]}



# Migrating and version controling
{: #migration-versioncontrol}

IBM continually updates the Terraform provider to give you higher levels of performance and being up-to-date. Some of the instances aren't able to be upgraded, so they must be closed and you must migrate your resources with the right version.

View the versions that are associated in the Terraform and the {{site.data.keyword.cloud_notm}} provider plug-in.
{: shortdesc}

## Migrating your Terraform version
{: #tf-0.1x-migration}
  
Update your Terraform configuration files from version 0.1x to version 0.1x so that you can run your Terraform code with the Terraform version 0.1x. 

With the release of Terraform version 0.12, the syntax for configuration files changed. If you want to run your infrastructure code by using Terraform version 0.12, you must first update your configuration files to apply the new syntax. 
{: important}

1. Follow the [instructions](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_cli) to install Terraform version 0.1x and the latest release of the Terraform. 
2. Copy your Terraform version 0.1x configuration files into your Terraform working directory. 
   ```
   mv <tf_config_file_path> $HOME/terraform
   ```
   {: pre}
   
3. Use the Terraform version 0.1x CLI to automatically apply the new syntax to your Terraform configuration files. 
  
   **Syntax**
   ```
   terraform <0.xx>upgrade
   ```
   {: pre}

   **Example to upgrade Terraform v0.12 to Terraform v0.13**
   ```
   terraform 0.13upgrade
   ```
   {: pre}
   
   Example output: 
   ```
   This command rewrites the configuration files in the given directory so
   that they use the new syntax features from Terraform v0.1x, and identify
   any constructs that may need to be adjusted for correct operation with
   Terraform v0.1x.

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
   
4. Open your Terraform configuration file to verify the changes. 

## Version control 
{: #versions}

View the versions that are associated with the resources and data sources in the documentation:

- **IBM Cloud Provider plug-in for Terraform version**: 1.14.0
- **Terraform version**: 0.12 or more

With the release of Terraform version 0.12, the syntax for configuration files changed. If you want to run your infrastructure code by using Terraform version 0.12, you must first [update your configuration files](#tf-0.1x-migration) to apply the new syntax. 
{: important}
