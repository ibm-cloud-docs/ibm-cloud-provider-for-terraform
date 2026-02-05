---

copyright:
  years: 2026, 2026
lastupdated: "2026-02-05"

keywords: KMS, Key Protect, Key Management Services, Key Deletion, terraform, HPCS

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Managing encryption keys in Terraform IBM Modules(TIM)
{: #kms-key-deletion}

IBM Cloud Key Management Services (KMS) - [Key Protect (KP)](/docs/key-protect/index.html) and [Hyper Protect Crypto Services (HPCS)](/docs/hs-crypto?topic=hs-crypto-get-started) - encrypt critical customer data across multiple IBM Cloud services.

Since keys are closely linked with encrypted data, key deletion must be handled with extreme caution. This topic explains key deletion considerations and how to handle them in Terraform IBM Modules (TIM).

A key is the owner of your data. Deleting a key permanently deletes access to everything encrypted with it.
{: note}

## Understanding `force_delete`
{: #kms-key-deletion-understanding}

In Terraform on IBM Cloud, `force_delete` is a specific argument that controls whether a key can be deleted while it is still in use by other IBM Cloud services. It is a boolean value that can be set to `true` or `false` in your Terraform configuration.

If `force_delete` is set to `false`, it:

* Prevents deletion of a key if it is actively referenced by any IBM Cloud service.
* Acts as a safety guardrail.
* Helps prevent accidental data loss and unrecoverable cloud resources.

This is the recommended and safest setting, especially for production environments.

If `force_delete` is set to `true`, it:

* Deletes the key even if it is currently in use.
* Immediately breaks encryption dependencies.
* May cause:
    * Permanent data loss.
    * Unrecoverable services.
    * Orphaned or unusable cloud resources.

Different IBM Cloud services may react differently when an encryption key is forcefully deleted. You must test key deletion behavior per service before allowing forced deletion in any environment.
{: note}

## Guidance to use `force_delete` in Terraform IBM Modules
{: #key-deletion-tim}

Enabling `force_delete` allows Terraform to destroy resources without dependency blocking.

When you use a Terraform IBM Module, the following approach is recommended:

1. Always set `force_delete` to `false` by default.
1. If you need to delete the keys, set `force_delete` to `true`. Ensure that you intend to proceed, as this action is irreversible.
1. Run `terraform apply` to update the state, and then run `terraform destroy` to permanently purge the key.

## Examples
{: #kms-key-deletion-examples}

The following example ensures that keys cannot be deleted until all dependent services are safely removed.

```hcl
resource "ibm_kms_key" "example" {
  instance_id  = var.kms_instance_id
  key_name     = "application-root-key"
  standard_key = true

  force_delete = false
}
```

You can refer to [Terraform IBM Modules](https://github.com/terraform-ibm-modules) to see usage examples. For example, see [terraform-ibm-kms-key](https://github.com/terraform-ibm-modules/terraform-ibm-kms-key/blob/main/main.tf) and [terraform-ibm-kms-all-inclusive](https://github.com/terraform-ibm-modules/terraform-ibm-kms-all-inclusive).

## Summary
{: #kms-key-deletion-summary}

To summarize this topic, the following list enlists the best practices for deleting keys:

* By default, forced deletion should not be allowed (`force_delete = false`).
* For production environments, never use forced deletion. Production keys must fail-safe, not fail-fast.
* You should use `force_delete = true` only in test environments.
* Deleting a key permanently deletes access to everything encrypted with it.

## Learn more
{: #kms-key-deletion-references}

To learn more, check the following resources:

* [Key Protect keys deletion](/docs/hs-crypto?topic=hs-crypto-delete-keys&interface=api#delete-key-force)
* [Hyper Protect keys deletion](/docs/hs-crypto?topic=hs-crypto-delete-keys&interface=api#delete-key-force)
* [Considerations before deleting and purging a key](/docs/key-protect?topic=key-protect-delete-purge-keys#delete-purge-keys-considerations)
