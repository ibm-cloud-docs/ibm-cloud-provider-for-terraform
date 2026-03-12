---

copyright:
  years: 2026, 2026
lastupdated: "2026-03-12"

keywords: watsonx, watson, watsonx.ai, watsonx ai

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Known issues with Terraform IBM Module for watsonx.ai
{: #known-issues-watsonx-ai}

You might encounter the following known issues when you work with the [terraform-ibm-watsonx-ai](https://github.com/terraform-ibm-modules/terraform-ibm-watsonx-ai) module.


## Error attaching existing COS instance to watsonx.ai project
{: #ki-cos-error}

When you configure a watsonx.ai project and attach an existing Cloud Object Storage instance from your account, you may encounter:

```
Error creating project: Error retrieving Administrator API key token for your Cloud Object Storage instance. Please try again later.
```

API response details:
```json
{
  "message": "Error retrieving Administrator API key token for your Cloud Object Storage instance. Please try again later.",
  "messageId": "projects_api_create_unexpected",
  "statusCode": 500
}
```

### Reason
{: #ki-cos-error-reason}

This error can occur due to missing authorization policies or issues with the COS resource key credentials.

### Workaround
{: #ki-cos-error-workaround}

Use a new COS instance for your deployments instead of reusing an existing COS instances.


## Non-existing COS instances appear in storage delegation list
{: #ki-non-existing-cos}

In the IBM watsonx platform, `Configuration & Settings → Storage Delegation` page, you may see old Object Storage service instances that have been deleted. 

### Reason
{: #ki-non-existing-cos-reason}

The platform does not have access to automatically remove storage delegation entries when COS instances are deleted. This is an account-level setting that requires manual cleanup.

### Solution
{: #ki-non-existing-cos-solution}

Delete all existing storage delegations for non-existing COS instances using the following curl command:

```bash
curl -X DELETE \
  "https://<region>.dataplatform.cloud.ibm.com/api/rest/v1/storage-delegations/{cos_instance_guid}"\
  -H "Authorization: Bearer $token" \
  -H "Content-Type: application/json"
```

Note: For regions `au-syd` and `ca-tor`, the URL will be `https://<region>.dai.cloud.ibm.com/api/rest/v1/storage-delegations/<cos_instance_guid>`.

After cleanup, the UI will properly display only existing COS instances.


## Insufficient account entitlements error (403) during storage delegation
{: #ki-insufficient-acc-entitlement}

You may encounter the following error when setting storage delegation:

```
Error: unexpected response code '403': {"statusCode":403,"message":"Insufficient account entitlements."}
```

This error is not consistent and may occur intermittently, sometimes resolving on retry.

### Reason
{: #ki-insufficient-acc-entitlement-reason}

Entitlements are a separate dependency for storage delegations. Before making storage delegation active, the system checks whether a user has permission to create the required watsonx (especially Studio) instances in that specific region.

When creating instances and immediately attempting to enable storage delegation, sometimes the response may not reflect the new entitlements, causing the "Insufficient account entitlements" error.

### Solution
{: #ki-insufficient-acc-entitlement-solution}

Sometimes waiting or retrying after creating watsonx instances helps before enabling storage delegation.


## User profile does not exist error (400) when configuring project
{: #ki-user-profile-error}

When running the configure_project API, you may receive:

```json
{
  "code": 400,
  "error": "Bad Request",
  "reason": "Missing or Invalid Data",
  "message": "The server cannot or will not process the request due to an apparent client error (e.g. malformed request syntax)."
}
```

### Reason
{: #ki-user-profile-error-reason}

It generally happens when you are trying out directly through API without creating a user profile in that region. The `configure_project` API requires an existing user profile.

### Solution
{: #ki-user-profile-error-solution}

Before running the configure_project API:

1. Log in to `<region>.dataplatform.cloud.ibm.com` in your browser
2. This creates your user profile in that region
3. Then run the configure_project API


## Project creation succeeds despite 502 error
{: #ki-project-create-error}

When creating a watsonx.ai project, the operation may fail with a 502 error:

```
Error: unexpected response code '502': error code: 502
```

However, the project may actually be created successfully despite the error message.

### Reason
{: #ki-project-create-error-reason}

This can occur when:
- A sub-dependency fails with a 502 error that gets propagated
- The application crashes before completing all operations but after creating the project

### Workaround
{: #ki-project-create-error-workaround}

1. Check if the project was actually created before retrying.
2. If you retry and receive an error like `"Project name <xx> already used"`, the project was successfully created.
3. Use the existing project or delete it before creating a new one with the same name.


## Entitlement failure after deleting and recreating storage delegation
{: #ki-entitlement-fail-error}

After deleting a storage delegation in a region and attempting to recreate it immediately, you may encounter a 403 entitlement failure.

### Reason
{: #ki-entitlement-fail-error-reason}

There may be a delay in the system recognizing that the previous delegation has been deleted and that entitlements are still valid for creating a new delegation.

### Workaround
{: #ki-entitlement-fail-error-workaround}

Wait for few minutes after deleting a storage delegation before attempting to recreate it.
