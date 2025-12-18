---

copyright:
  years: 2017, 2025
lastupdated: "2025-12-12"

keywords: question about kubernetes provider, troubleshooting guide, kubernetes service troubleshooting

subcollection: ibm-cloud-provider-for-terraform

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I resolve the network error when working with the {{site.data.keyword.containershort_notm}} provider?
{: #ks-network-error}


During the cluster upgrade from {{site.data.keyword.containershort}} older version to new version. The Terraform apply fails with the `TCP connection error message`.
{: tsSymptoms}

```text
Error: Get "http://localhost/api/v1/": dial tcp [::1]:80: connect: connection refused
```
{: screen}

Or

```text
Error: Kubernetes service cluster unreachable: invalid configuration: no configuration has been provided
```
{: screen}

You are combining the cluster provisioning and working with the {{site.data.keyword.containershort_notm}} provider at the same time in your Terraform template in the {{site.data.keyword.bplong_notm}} workspace or in your localhost. You make a change in the cluster configuration that leads to the cluster re-create. When you run `terraform refresh` command, you view strange errors such as, network or namespace issues.
{: tsCauses}

To troubleshoot this error you need to ensure:
{: tsResolve}

- You don't combine the {{site.data.keyword.containershort_notm}} provider with the cluster resource at the same time in the Terraform template.

- The resources should not be created in the same Terraform template or module where {{site.data.keyword.containershort_notm}} provider resources are in use.

- The Terraform provider evaluates the provider blocks versus actual resource, and the order in which the resources are defined. For more information, see [Provider configuration](https://developer.hashicorp.com/terraform/language/providers/configuration#provider-configuration){: external}.

If you cannot resolve this issue, contact support by opening a support case for the service that you want to work with. Make sure to include the incident ID. For more information, see [Using the Support Center](/docs/account?topic=account-using-avatar).
