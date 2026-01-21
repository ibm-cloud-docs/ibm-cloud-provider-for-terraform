---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-21"

keywords: terraform identity and access, terraform iam, terraform permissions, terraform iam policy

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #provider-reference}

Before you can start working with Terraform on IBM Cloud, you must retrieve the credentials and parameters that are required for a Terraform resource or data source, and specify them in the `provider` configuration. This configuration is used by the {{site.data.keyword.cloud_notm}} Provider plug-in to authenticate with the {{site.data.keyword.cloud_notm}} platform and to view, create, update, or delete {{site.data.keyword.cloud_notm}} resources and services.
{: shortdesc}

## Required input parameters for each resource category
{: #required-parameters}

The configuration of the {{site.data.keyword.cloud_notm}} Provider plug-in varies depending on the resource or data source category that you want to work with as shown in the following table. The values in this table are required. To retrieve the values or view more parameters that you can specify, see the [Supported input parameters](#provider-parameter-ov).

By default, the {{site.data.keyword.cloud_notm}} Provider plug-in is configured to create resources in the `us-south` region. If you want to create your resources in a different region, specify this region by adding the `region` parameter to your `provider` configuration.
{: note}

|Required parameters|Classic infrastructure|Cloud Foundry|Functions|Power Systems|Other IAM-enabled services|
|--|:--:|:--:|:--:|:--:|:--:|
|`ibmcloud_api_key`|![Check mark](../images/checkmark.svg "Check mark")|![Check mark](../images/checkmark.svg "Check mark")|![Check mark](../images/checkmark.svg "Check mark")|![Check mark](../images/checkmark.svg "Check mark")|![Check mark](../images/checkmark.svg "Check mark")|
|`iaas_classic_username`|![Check mark](../images/checkmark.svg "Check mark")|||||
|`iaas_classic_api_key`|![Check mark](../images/checkmark.svg "Check mark")|||||
|`function_namespace`|||![Check mark](../images/checkmark.svg "Check mark")|||
|`zone`||||![Check mark](../images/checkmark.svg "Check mark") <br> For multi-zone regions only||
{: caption="Required Parameters" caption-side="top"}

## Supported input parameters
{: #provider-parameter-ov}

Review what parameters you can set in the `provider` block of your Terraform on IBM Cloud configuration file. For more information, about the {{site.data.keyword.cloud_notm}} provider input parameters, see [{{site.data.keyword.cloud_notm}}](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs#argument-reference){: external}.
{: shortdesc}

|Input parameter|Required / optional|Description|
|-------------|--------|-----------------------|
|`iaas_classic_api_key`|Required for classic infrastructure|The API key to access classic {{site.data.keyword.cloud_notm}} infrastructure. For more information, about how to retrieve your API key, see [Managing classic infrastructure API keys](/docs/account?topic=account-classic_keys). This value is required when you want to work with classic infrastructure resources. You can specify the API key in the `provider` block or retrieve the value from the `IAAS_CLASSIC_API_KEY` environment variable.|
|`iaas_classic_username`|Required for classic infrastructure|The user name to access classic {{site.data.keyword.cloud_notm}} infrastructure. For more information, about how to retrieve your user name, see [Managing classic infrastructure API keys](/docs/account?topic=account-classic_keys). This value is required when you want to work with classic infrastructure resources. You can specify the user name in the `provider` block or retrieve the value from the `IAAS_CLASSIC_USERNAME` environment variable.|
|`iaas_classic_endpoint_url`|Optional|The API endpoint that you want to use to access {{site.data.keyword.cloud_notm}} classic infrastructure. If this value is not specified, `https://api.softlayer.com/rest/v3` is used by default. You can specify the URL in the `provider` block or retrieve the value from the `IAAS_CLASSIC_ENDPOINT_URL`. |
|`iaas_classic_timeout`|Optional|The number of seconds to wait until the classic infrastructure API is considered unavailable. The default values is `60`. You can specify this information in the `provider` block or retrieve it from the `IAAS_CLASSIC_TIMEOUT` environment variable.|
|`ibmcloud_api_key`|Required|The {{site.data.keyword.cloud_notm}} API key to authenticate with the {{site.data.keyword.cloud_notm}} platform. For more information, about how to create an API key, see [Creating an API key](/docs/account?topic=account-userapikey&interface=ui). You can specify the API key in the `provider` block or retrieve the value from the `IC_API_KEY` or `IBMCLOUD_API_KEY` environment variables. If both environment variables are defined, `IC_API_KEY` takes precedence.|
|`ibmcloud_timeout`|Optional|The number of seconds that you want to wait until the {{site.data.keyword.cloud_notm}} API is considered unavailable. The default value is `60`. You can specify the timeout in the `provider` block or retrieve the value from the `IC_TIMEOUT` or `IBMCLOUD_TIMEOUT` environment variables. If both variables are specified, `IC_TIMEOUT` takes precedence.|
|`function_namespace`|Required for Functions|The {{site.data.keyword.openwhisk}} namespace that you want to use. The namespace is composed from your Cloud Foundry organization and space in the format `<org>_<space>`. You can specify the namespace in your `provider` block or retrieve the value from the `FUNCTION_NAMESPACE` environment variable.
|`generation`|Required for VPC infrastructure|(Deprecated) The generation of Virtual Private Cloud infrastructure that you want to use. If this value is not specified, `2` is used by default. You can specify the generation in your `provider` block or retrieve the value from the `IC_GENERATION` or `IBMCLOUD_GENERATION` environment variables. If both environment variables are defined, `IC_GENERATION` takes precedence.|
|`max_retries`|Optional|The maximum number of times that a request to the {{site.data.keyword.cloud_notm}} infrastructure API is sent before the request is considered failed. The default value is `10`. Use this parameter when you receive network-related timeouts or rate limit exceeded error codes. You can specify the number in your `provider` block or retrieve the value from the `MAX_RETRIES` environment variable.|
|`region`|Optional|The {{site.data.keyword.cloud_notm}} region where you want to create your resources. If this value is not specified, `us-south` is used by default. You can specify the region in the `provider` block or retrieve the value from the `IBMCLOUD_REGION` or `IC_REGION` environment variables. If both environment variables are specified, `IC_REGION` takes precedence.|
|`resource_group`|Optional|The ID of the resource group that you want to use for your {{site.data.keyword.cloud_notm}} resources. To retrieve the ID, run `ibmcloud resource groups`. You can specify the resource group in the `provider` block or retrieve the value from the `IC_RESOURCE_GROUP` or `IBMCLOUD_RESOURCE_GROUP` environment variables. If both environment variables are defined, `IC_RESOURCE_GROUP` takes precedence. |
|`zone`|Required for Power Systems|The zone of an {{site.data.keyword.cloud_notm}} region where you want to create Power System resources. This value is required if you want to work with resources in a multizone-capable region. For example, if you want to work in the `eu-de` region, you must enter `eu-de-1` or `eu-de-2`. You can specify the zone in the `provider` block or retrieve the value from the `IC_ZONE` or `IBMCLOUD_ZONE` environment variables. If both environment variables are specified, `IC_ZONE` takes precedence.|
|`visibility` |Optional| The visibility to {{site.data.keyword.cloud_notm}} endpoint. Allowable values are`public`, `private`, `public-and-private`. Default value is `public`. <ul><li>If visibility is set to **public**, use the regional public endpoint or global public endpoint. The regional public endpoints has higher precedence.</li><li>If visibility is set to **private**, use the regional private endpoint or global private endpoint. The regional private endpoint is given higher precedence. To use the private endpoint from an {{site.data.keyword.cloud_notm}} resource (such as, a classic VM instance), one must have VRF-enabled account. If the {{site.data.keyword.cloud_notm}} service does not support private endpoint, the Terraform resource or datasource will log an error.</li><li>If visibility is set to **public-and-private**, use regional private endpoints or global private endpoint. If service does not support regional or global private endpoints it uses the regional or global public endpoint.</li><li>This can be retrieved from the `IC_VISIBILITY` higher precedence or `IBMCLOUD_VISIBILITY` environment variable.</li></ul>|
{: caption="Supported input parameters in configuration file" caption-side="top"}

## Specifying the `provider` block
{: #provider-example}

After you [retrieved the required parameters](#required-parameters) to work with a Terraform resource or data source, you can now specify your provider block.

### Creating a static `provider.tf` file
{: #static}

You can declare the input parameters in the `provider` block directly.
{: shortdesc}

Because the `provider` block includes sensitive information, do not commit this file into a public source repository. To add version control to your provider configuration, use a local [`terraform.tfvars` file](#tf-variables).
{: important}

1. Create a `provider.tf` file and specify the input parameters that are required for your resource or data source.
    ```terraform
    provider "ibm" {
        ibmcloud_api_key = "<api_key>"
        iaas_classic_username = "<classic_username>"
        iaas_classic_api_key = "<classic_api_key>"
    }
    ```
    {: codeblock}

2. Initialize the Terraform CLI.
    ```sh
    terraform init
    ```
    {: pre}

### Referencing credentials from a `terraform.tfvars` file
{: #tf-variables}

You can store sensitive information, such as credentials, in a local `terraform.tfvars` file and reference these credentials in your `provider` block.
{: shortdesc}

Do not commit the `terraform.tfvars` into a public source repository. This file is meant to be stored in your local machine only.
{: important}

1. Create a `terraform.tfvars` file on your local machine and add the input parameters that are required for your resource or data source.
    ```sh
    ibmcloud_api_key = "<ibmcloud_api_key>"
    iaas_classic_username = "<classic_infrastructure_username>"
    iaas_classic_api_key = "<classic_infrasturcture_apikey>"
    ```
    {: codeblock}

2. Create a `provider.tf` file and use Terraform interpolation syntax to reference the variables from the `terraform.tfvars`.
    ```terraform
    variable "ibmcloud_api_key" {}
    variable "iaas_classic_username" {}
    variable "iaas_classic_api_key" {}

    provider "ibm" {
        ibmcloud_api_key    = var.ibmcloud_api_key
        iaas_classic_username = var.iaas_classic_username
        iaas_classic_api_key  = var.iaas_classic_api_key
    }
    ```
    {: codeblock}

3. Initialize the Terraform CLI.
    ```sh
    terraform init
    ```
    {: pre}


### Using environment variables
{: #env-vars}

You can configure the {{site.data.keyword.cloud_notm}} Provider plug-in by exporting required parameters as environment variables on your local machine. Environment variables are automatically loaded when you initialize the Terraform CLI.
{: shortdesc}

1. [Retrieve the environment variable names](#provider-parameter-ov) for the provider parameters that you want to export. For example, to specify a classic infrastructure username, use `IAAS_CLASSIC_USERNAME`.
2. Create a `provider.tf` file and add an empty provider block.
    ```terraform
    provider "ibm" {}
    ```
    {: codeblock}

3. Set the environment variables on your local machine.
    ```sh
    export IC_API_KEY="<ibmcloud_api_key>"
    export IAAS_CLASSIC_USERNAME="<classic_username>"
    export IAAS_CLASSIC_API_KEY="<classic_api_key>"
    ```
    {: codeblock}

4. Initialize the Terraform CLI.
    ```sh
    terraform init
    ```
    {: pre}


## Creating multiple `provider` configurations
{: #multiple-providers}

You can add multiple `provider` configurations within the same Terraform on IBM Cloud configuration file to create your {{site.data.keyword.cloud_notm}} resources with different provider parameters.
{: shortdesc}

Creating multiple `provider` configurations is useful when you want to use different input parameters, such as different regions, zones, infrastructure generations, or accounts to create the {{site.data.keyword.cloud_notm}} resources in your Terraform on IBM Cloud configuration file. For more information, see [Multiple Provider Instances](https://developer.hashicorp.com/terraform/language/block/provider){: external}.

1. In your Terraform on IBM Cloud configuration or `provider.tf` file, create multiple provider blocks with the same provider name. The provider configuration without an alias is considered the default provider configuration and is used for every resource where you do not specify a specific provider configuration. Any more provider configurations must include an alias so that you can reference this provider from your resource definition.
    ```terraform
    provider "ibm" {
        ibmcloud_api_key    = var.ibmcloud_api_key
        region = "us-south"
    }

    provider "ibm" {
        alias = "east"
        ibmcloud_api_key    = var.ibmcloud_api_key
        region = "us-east"
    }
    ```
    {: codeblock}

2. In your resource definition, specify the provider configuration that you want to use. If you do not specify a provider, the default provider configuration is used.
    ```terraform
    resource "ibm_container_cluster" "cluster" {
        provider = ibm.east
    ...
    }
    ```
    {: codeblock}

## Configuring non-default cloud service endpoints
{: #config-provider}

The {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform can be configured to use non-default {{site.data.keyword.cloud_notm}} service endpoints.
{: shortdesc}

Support for using non-default {{site.data.keyword.cloud_notm}} service endpoints is offered as best effort. Individual Terraform resources might require compatibility updates to support the declaration of custom service endpoints.
{: important}

The steps that are involved in configuring your {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on IBM Cloud to use the private Cloud Service Endpoint (CSE) of an {{site.data.keyword.cloud_notm}} service in  public CSE in [Production environment](https://cloud.ibm.com).

1. Set up the Terraform on IBM Cloud engine and an {{site.data.keyword.cloud_notm}} Provider plug-in, in {{site.data.keyword.cloud_notm}} virtual machine by using private VLAN. And provision the enabled Virtual Routing and Forwarding (VRF) account.
2. Export the environment variables that are listed in the table to your local machine. For more information, about supported private Cloud Service Endpoints for each {{site.data.keyword.cloud_notm}} service to support in production, see [Use service endpoints](/docs/account?topic=account-vrf-service-endpoint).
3. Initialize the Terraform on IBM Cloud command line to load the environment variables that you set.
    ```sh
    terraform init
    ```
    {: pre}



|Service|Environment variable key|Private service endpoint|
|-------------|--------|----------------|
|Account management|`IBMCLOUD_ACCOUNT_MANAGEMENT_API_ENDPOINT`|N/A|
|API Gateway | ` IBMCLOUD_API_GATEWAY_ENDPOINT`|N/A|
|Certificate manager|`IBMCLOUD_CERTIFICATE_MANAGER_API_ENDPOINT`|N/A|
|Cloud Foundry|`IBMCLOUD_MCCP_API_ENDPOINT`|N/A|
|Cloud functions|`IBMCLOUD_NAMESPACE_API_ENDPOINT`|N/A|
|CIS|`IBMCLOUD_CIS_API_ENDPOINT`|N/A|
|Containers|`IBMCLOUD_CS_API_ENDPOINT`|[Docs](/docs/containers?topic=containers-strategy)|
|Content Catalog | `IBMCLOUD_CATALOG_MANAGEMENT_API_ENDPOINT`|N/A|
|Container Registry | `IBMCLOUD_CR_API_ENDPOINT`|N/A|
|COS config | `IBMCLOUD_COS_CONFIG_ENDPOINT`|N/A|
|COS-S3 | `IBMCLOUD_COS_ENDPOINT`|N/A|
|Direct Link | `IBMCLOUD_DL_PROVIDER_API_ENDPOINT`|N/A|
|Enterprise Management | `IBMCLOUD_ENTERPRISE_API_ENDPOINT`|N/A|
|Global tagging |`IBMCLOUD_GT_API_ENDPOINT`| [Endpoint URLs](https://{DomainName}/apidocs/tagging#endpoint-url) |
|HPCS|`IBMCLOUD_HPCS_API_ENDPOINT`|N/A|
|IAM|`IBMCLOUD_IAM_API_ENDPOINT`| [Endpoint URLs](https://{DomainName}/apidocs/iam-access-groups#endpoint-urls) |
|IAMPAP|`IBMCLOUD_IAMPAP_API_ENDPOINT`|N/A|
|ICD|`IBMCLOUD_ICD_API_ENDPOINT`|[Docs](/docs/account?topic=account-vrf-service-endpoint)|
|Key protect|`IBMCLOUD_KP_API_ENDPOINT`|[Docs](/docs/key-protect?topic=key-protect-private-endpoints)|
|Power|`IBMCLOUD_PI_API_ENDPOINT`| [Endpoint URL](https://{DomainName}/apidocs/power-cloud#endpoint) |
|Private DNS|`IBMCLOUD_PRIVATE_DNS_API_ENDPOINT`| N/A|
|Resource management|`IBMCLOUD_RESOURCE_MANAGEMENT_API_ENDPOINT`| [Endpoint URLs](https://{DomainName}/apidocs/resource-controller/resource-manager#endpoint-urls) |
|Resource controller|`IBMCLOUD_RESOURCE_CONTROLLER_API_ENDPOINT`|N/A|
|Resource catalog|`IBMCLOUD_RESOURCE_CATALOG_API_ENDPOINT`|N/A|
|Resource management|`IBMCLOUD_RESOURCE_MANAGEMENT_API_ENDPOINT`|N/A|
|Satellite | `IBMCLOUD_SATELLITE_API_ENDPOINT`|N/A|
|Schematics|`IBMCLOUD_SCHEMATICS_API_ENDPOINT`|[Docs](/docs/schematics?topic=schematics-private-endpoints)|
|Transit Gateway|`IBMCLOUD_TG_API_ENDPOINT`| N/A|
|UAA|`IBMCLOUD_UAA_ENDPOINT`|N/A|
|User management|`IBMCLOUD_USER_MANAGEMENT_ENDPOINT`| [Endpoint URLs](`https://{DomainName}/apidocs/user-management#endpoint-urls`) |
|VPC Gen2|`IBMCLOUD_IS_NG_API_ENDPOINT`|N/A|
{: caption="Terraform on IBM Cloud environment variables" caption-side="top"}
