---

copyright:
  years: 2026, 2026
lastupdated: "2026-03-03"

keywords: VPC, Virtual Private Cloud, Landing Zone, Subnet, Prefix, terraform, IBM Cloud

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Known issues with Terraform IBM Module for Virtual Private Cloud (VPC)
{: #known-issues-vpc}

You might encounter the following known issues when you work with the [terraform-ibm-landing-zone-vpc](https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone-vpc/){: external} module..

## Changing prefix value recreates subnets and address prefixes
{: #ki-vpc-prefix-change-recreate}

The issue can occur when the `prefix` value is modified after initial deployment. For more details about this behavior and guidance, see [Changing prefix value recreates subnets and address prefixes](/docs/secure-infrastructure-vpc?topic=secure-infrastructure-vpc-known-issues#ki-vpc-prefix-change-recreate).
