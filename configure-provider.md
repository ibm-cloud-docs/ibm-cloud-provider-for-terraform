# Configuring the {{site.data.keyword.cloud_notm}} provider plug-in
{: #configuring_provider}

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
        <th>Parameters</th>
        <th >Description</th>
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


