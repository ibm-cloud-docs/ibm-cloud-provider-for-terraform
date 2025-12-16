---

copyright:
  years: 2025, 2025
lastupdated: "2025-12-16"

keywords: Package module as DA, Publish in Private Catalog, DA, Catalog

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Package as a Deployable Architecture and Publish to a Private Catalog
{: #package-and-publish-da}

A [Deployable Architecture](https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-understand-module-da&interface=ui)(DA) is a terraform solution often built using multiple TIM modules to create an architectural pattern. The DA can be published as a deployable solution in the IBM Cloud catalog that creates a self-service experience, allowing developers and other teams to deploy this entire architecture with just a few clicks in the IBM Cloud console, without needing to understand the underlying Terraform code.

Considering you have successfully built and tested a secure infrastructure using Terraform . The next step in the platform engineering lifecycle is to package this automation so that others in your organization can easily reuse it. In this tutorial you will learn how to package a TIM module as a Deployable Architecture (DA) and publish it to a private catalog.

## Before you begin

Ensure that you have the following:

- An IBM Cloud account with permissions to create and manage private catalogs.

## Package the Terraform code
{: #create-da-bundle}
{: step}

Before you onboard a Deployable Architecture, you must create a Terraform bundle from your repository.

### Create a release

1. In your GitHub repository, go to **Releases** → **Draft a new release**.
2. In **Tag version**, create a new tag. For example,  `v1.0.0-test`.
3. Select the target branch. For example, `main`.
4. Provide a release title.  
5. (Optional) Select **Set as a pre-release**.
6. Click **Publish release**.

### Copy the `.tar.gz` bundle link

GitHub automatically generates the bundle.

1. Open the release you created.
2. Under **Assets**, locate `Source code (tar.gz)`
3. Right-click and select **Copy link address**.

The link follows this format:

```text
https://github.com/<org>/<repo>/archive/refs/tags/<tag>.tar.gz
```

Use this URL as the **Source URL** when onboarding the Deployable Architecture.

## Publish to a Private Catalog
{: #publish-da}
{: step}

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

- Learn how to [deploy a Deployable Architecture](https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-setup-project&interface=ui) by using IBM Cloud Projects:  
