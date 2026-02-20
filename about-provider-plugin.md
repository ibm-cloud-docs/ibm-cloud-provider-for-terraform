---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-20"

keywords: Terraform on IBM Cloud, resources, Terraform Provider, Terraform provider plug-in, IBM Cloud provider plug-in for Terraform

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform
{: #about-ibm-cloud-provider-plugin}

To abstract the APIs and complexity of the cloud resource provisioning and management process to the user, cloud providers create a plug-in for Terraform that contains the information for how to connect to the cloud provider and what APIs to call to work with a certain cloud resource. IBM's plug-in is called the **{{site.data.keyword.cloud_notm}} Provider plug-in for Terraform**.

The plug-in analyzes the resources that you specified and determines the order in which these resources must be provisioned, including any dependencies that must be considered.

The provider plug-in acts as a bridge between Terraform and IBM Cloud, translating your Terraform configurations into API calls that create, update, or delete IBM Cloud resources.

## How does it work?
{: #resource-lifecycle-ov}
{: #how-it-works-provider-plugin}

To use Terraform on IBM Cloud, you must create a Terraform configuration file by using HashiCorp Configuration Language (HCL) that describes the {{site.data.keyword.cloud_notm}} resources that you need and how you want to configure them. Store this configuration file in a source code repository that is version-controlled and that allows teams to collaborate, such as GitHub or GitLab. And configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform.

When you run Terraform commands, the IBM Cloud Provider plug-in:

1. **Reads your configuration** - Parses your `.tf` files to understand desired state
2. **Authenticates with IBM Cloud** - Uses your API key to access IBM Cloud services
3. **Plans changes** - Creates desired state or compares desired state with current state in case of updating the existing infrastructure
4. **Executes API calls** - Creates, updates, or deletes resources via IBM Cloud APIs based on the Terraform execution plan
5. **Updates state** - Records the current state of your infrastructure

## Next steps
{: #provider-next-steps}

Once you are ready to start using the IBM Cloud Provider plug-in, follow these steps:

1. [Install Terraform CLI](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli)
2. [Configure the provider](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference)
3. [Create your first configuration](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-terraform-config)
4. [Manage resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-manage_resources)

You can further explore the [provider documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external} for more details.
