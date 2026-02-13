---

copyright:
  years: 2026, 2026
lastupdated: "2026-02-13"

keywords:

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Known issues with Red Hat OpenShift on IBM Cloud / IBM Cloud Kubernetes Service when using terraform
{: #known-issues}

## Cluster creation fails with "The specified API key could not be found"
{: #ki-apikey-error}

During cluster provisioning a containers apikey is created if one does not already exist for the given resource group and region ([learn more](https://cloud.ibm.com/docs/containers?topic=containers-access-creds)). Occasionally replication of the newly created apikey can be delayed causing the cluster creation to fail with an error like this:

`Error: Request failed with status code: 404, ServerErrorResponse: {"incidentID":"c5caf83e-5f08-48c9-9778-6f3eb0ce1d16,c5caf83e-5f08-48c9-9778-6f3eb0ce1d16","code":"E06f9","description":"The specified API key could not be found.","type":""}`

### Workaround
{: #ki-apikey-error-workaround}
To workaround the issue simply attempt a re-apply of the terraform and it should pass on second attempt. If you still face issues, an IBM Cloud support case should be created with the `Kubernetes service` and include the `incidentID` from the error.

## OpenShift cluster creation fails due to entitlement not found
{: #ki-entitlement-error}

During cluster provisioning you might encounter the following error during the terraform apply phase if a value has been set for `ocp_entitlement` even if the entitlement is valid:

```
---
id: terraform-40a3a1fe
summary: 'Request failed with status code: 400, ServerErrorResponse:
{"incidentID":"a0701484-1dcf-a82e-90b1-455464f7064c","code":"E3595","description":"The
  entitlement ''cloud_pak'' was not found. Specify ''ocp_entitled'' to search for
  any supported license or entitlement. If no match is found, then you do not have
  a supported license or entitlement.","type":"BadRequest"}'
severity: error
resource: ibm_container_vpc_cluster
operation: create
component:
  name: github.com/IBM-Cloud/terraform-provider-ibm
  version: 1.83.3
---
```

### Workaround
{: #ki-apikey-error-workaround}
If indeed your entitlement is valid, this error may occur when the OpenShift cluster API key for the target region and resource group is invalid, expired, or not properly associated with the required entitlement.

To workaround this issue, replace the API key for all clusters in the specified region and targeted resource group by running the following CLI commands:
```bash
ibmcloud target -g <resource-group>
ibmcloud oc api-key reset --region <region>
```

## Update in place identified for `kube_version`
{: #ki-kube-version-update}

Your terraform plan may identify an update in place for the `kube_version` attribute even if this value has not changed in your terraform configuration. For example:
```
kube_version = "4.12.16_openshift" -> "4.12.20_openshift"

Unless you have made equivalent changes to your configuration, or ignored the relevant attributes using ignore_changes, the following plan may include actions to undo or respond to these changes.
```
The updated patch version is detected because the Kubernetes master node is updated automatically non-disruptively by IBM outside of terraform and is detecting this as drift.

### Workaround
{: #ki-kube-version-update-workaround}
Proceeding with the terraform apply so the terraform state becomes in sync with the backend version. Since the patch version is already actually updated on the backend, the terraform apply is actually going to be a no-op and is safe to apply as there will be no disruption to the service.

## The refresh token contains subject type 'ServiceId', which is not valid for the intended operation
{: #ki-refresh-token-error}

When provisioning this module in IBM Cloud Schematics, you may encounter the following error during the Terraform plan phase:

```
| Planning failed. Terraform encountered an error while generating this plan.
|
|
| Error: [ERROR] Error downloading the cluster config [d50jqc1b0qvhhqn88k8g]: Request failed with status code: 400, BXNIM0453E: The refresh token contains subject type 'ServiceId', which is not valid for the intended operation. Supported subject types are UserId, Profile.
|
|   with module.ocp_base.data.ibm_container_cluster_config.cluster_config[0],
|   on ../../main.tf line 448, in data "ibm_container_cluster_config" "cluster_config":
|  448: data "ibm_container_cluster_config" "cluster_config" {
|
| ---
| id: terraform-82a5043b
| summary: '[ERROR] Error downloading the cluster config
| [d50jqc1b0qvhhqn88k8g]: Request
|   failed with status code: 400, BXNIM0453E: The refresh token contains subject type
|   ''ServiceId'', which is not valid for the intended operation. Supported subject
|   types are UserId, Profile.'
| severity: error
| resource: (Data) ibm_container_cluster_config
| operation: read
| component:
|   name: github.com/IBM-Cloud/terraform-provider-ibm
|   version: 1.79.2
| ---
|
```

This error typically occurs when an API key is not explicitly passed to the IBM Cloud provider configuration in Schematics and the user triggers the plan or apply action through the IBM Cloud CLI when authenticated as a Service ID. The following provider configuration will trigger this error:

```terraform
provider "ibm" {
  region = var.region
}
```

This happens because when a Service ID is used to trigger the Schematics workspace, Schematics passes an IAM access token for authentication, but OpenShift cluster operations require an API key.

### Workaround
{: #ki-refresh-token-workaround}

To resolve this issue, explicitly provide an IBM Cloud API key value in your provider configuration when running in Schematics. The API key can be associated with either a user account or a Service ID. For example:

```terraform
provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
  region           = var.region
}
```
