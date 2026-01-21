---

copyright:
  years: 2025, 2026
lastupdated: "2026-01-21"

keywords: Package module as DA, Publish in Private Catalog, DA, Catalog

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Package a Deployable Architecture and Publish to a Private Catalog
{: #package-and-publish-da}

A [Deployable Architecture](/docs/secure-enterprise?topic=secure-enterprise-understand-module-da&interface=ui)(DA) is a terraform solution often built using multiple TIM modules to create an architectural pattern. The DA can be published as a deployable solution in the IBM Cloud catalog that creates a self-service experience, allowing developers and other teams to deploy this entire architecture with just a few clicks in the IBM Cloud console, without needing to understand the underlying Terraform code.

Considering you have successfully built and tested a secure infrastructure using Terraform by following this [guide](/docs/secure-enterprise?topic=secure-enterprise-create-da&interface=ui). This tutorial provides you a [sample DA](https://github.com/IBM/deployable-architecture-iac-lab-materials/tree/main) for reference. The next step in the platform engineering lifecycle is to package this automation so it can be easily reused across your organization.

In this tutorial you will learn how to package the source code and publish it to a private catalog.

## Before you begin

Ensure that you have the following:

- An IBM Cloud account with permissions to create and manage private catalogs.

## Package the Terraform code
{: #create-da-bundle}
{: step}

The [catalog manifest file](/docs/secure-enterprise?topic=secure-enterprise-create-da&interface=ui#create-manifest) located at root of your DA code, defines the metadata required to create a catalog tile. Before onboarding a DA, you must package the source code.

The packaged source code(`.tar.gz` file) is typically generated from a release in a source code repository like GitHub or GitLab. Detailed instructions are available [here](/docs/secure-enterprise?topic=secure-enterprise-onboard-da#package-source). For the purpose of this tutorial, a public URL to a pre-packaged bundle is provided to simplify the process.

```text
https://github.com/IBM/deployable-architecture-iac-lab-materials/archive/refs/tags/v1.0.3.tar.gz
```

Use this URL as the **Source URL** in the next step.

## Publish to a Private Catalog
{: #publish-da}
{: step}

Now, you will create a private catalog and add your deployable architecture to the private catalog within your IBM Cloud account.

### Create a private catalog

Create a private catalog to host and distribute your Deployable Architectures.

1. In the IBM Cloud console, select **Manage > Catalogs**.
2. Click **Create a catalog**.
3. Enter a name, description (optional), and resource group.
4. Select **No products** as the template.
5. Click **Create**.

Your catalog is now ready for onboarding.


### Onboard the Deployable Architecture

Add your Terraform bundle to the catalog.

1. Open your private catalog and click **Add product**.
2. Configure:

   - **Product type:** Deployable architecture
   - **Delivery method:** Terraform
   - **Repository type:** Public repository
   - **Source URL:** Your `.tar.gz` bundle URL
   - **Version:** For example, `v1.0.0`
   - **Variation:** `standard`
   - **Category:** Select an appropriate category

3. Click **Add product**.

The product enters **Draft** state.

### Mark the version as pre-release

To enable testing without full validation:

1. Open the product page and select **Versions**.
2. Click the version.
3. Open the **⋮** menu.
4. Select **Ready to pre-release**.
5. Confirm.


### View the Deployable Architecture in the catalog

1. In the IBM Cloud console, open **Catalog**.
2. Under **My private catalogs**, choose your catalog.
3. Locate the DA tile and open it.
4. Review:
   - Description
   - Architecture diagram (optional)
   - Configuration options
   - **Configure and deploy** button

Users can now deploy the full architecture without writing Terraform code. This is the key benefit of creating a Deployable Architecture, your organization can now deploy this complex infrastructure consistently with just a few clicks, reducing deployment time while maintaining security standards.

## Next steps

- Explore how to [edit your private catalog](/docs/secure-enterprise?topic=secure-enterprise-onboard-da) entry.
- Learn how to [deploy a Deployable Architecture](/docs/secure-enterprise?topic=secure-enterprise-setup-project&interface=ui) by using IBM Cloud Projects.
