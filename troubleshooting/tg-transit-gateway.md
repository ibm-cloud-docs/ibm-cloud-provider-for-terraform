<staging>
---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-08"

keywords: getting help, troubleshooting guide, transit gateway troubleshooting

subcollection: ibm-cloud-provider-for-terraform

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# How can I create a Transit Gateway to connect from different regions?
{: #tg-transit-gwy}

A Terraform plan in “eu-de” region as stated in the first code block is not retrieving a VPC that are located in "eu-gb" as stated in the second code block
{: tsSymptoms}

**first code block**

```
provider "ibm" {
    ibmcloud_api_key   = xxxxxx
    region             = "eu-de"
}
```
**second code block**

```
data "ibm_is_vpc" "vpc1" {
  name            = "aa-kubecf-a"
}
```


Without manually write CRN for VPC, You need to get information about the VPC from the different region to create a Transit Gateway to connect different regions. Is there a way to accomplish this error?

```
Error: No VPC found with name aa-kubecf-a 
```
{: tsCauses}


You can accomplish to connect and retrieve information from a remote system by using `aliases` targeting multiple regions. Refer the example code block for the syntax. For more information, refer to [Multiple provider configurations](https://www.terraform.io/docs/language/providers/configuration.html#alias-multiple-provider-configurations).

{: tsResolve}

**Example**

```
provider "ibm" {
  ibmcloud_api_key = "${var.ibmcloud_api_key}"
  generation = 2
  region = "eu-de"
}
```

**Example configuring `aliases` to target multiple regions**

```
provider "ibm" {
  ibmcloud_api_key = "${var.ibmcloud_api_key}"
  region = "eu-de-2"
}

provider "ibm" {
  ibmcloud_api_key = "${var.ibmcloud_api_key}"
  alias  = "eu-gb"
  region = "eu-gb-2"
}
```

