---

copyright:
  years: 2017, 2025
lastupdated: "2025-11-21"

keywords: terraform, sitemap

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Site map
{: #sitemap}



## About {{site.data.keyword.terraform-provider_full}}
{: #sitemap_about_}


[About {{site.data.keyword.terraform-provider_full}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about#about)

* [How does Terraform on IBM Cloud work?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about#how-it-works)

    * [What is the {{site.data.keyword.cloud_notm}} Provider plug-in?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about#provider-plugin-ov)

    * [How does Terraform on IBM Cloud provision and manage cloud services?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about#resource-lifecycle-ov)

* [What are the benefits of using Terraform on IBM Cloud?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about#abt-benefits)

* [Key terms](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about#terms)


## Getting started with Terraform on IBM Cloud
{: #sitemap_getting_started_with_terraform_on_ibm_cloud}


[Getting started with Terraform on IBM Cloud](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#getting-started)

* [Step 1: Installing the Terraform CLI](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#tf_installation_step)

* [Step 2: Configuring the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#install_provider-step)

* [Step 3: Testing your configuration](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#test-terraform-template)


## Configuring the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #sitemap_configuring_the_provider_plug-in}


[Configuring the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#provider-reference)

* [Required input parameters for each resource category](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters)

* [Supported input parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#provider-parameter-ov)

* [Specifying the `provider` block](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#provider-example)

    * [Creating a static `provider.tf` file](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#static)

    * [Referencing credentials from a `terraform.tfvars` file](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#tf-variables)

    * [Using environment variables](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#env-vars)

* [Creating multiple `provider` configurations](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#multiple-providers)

* [Configuring non-default cloud service endpoints](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#config-provider)


## Creating Terraform on IBM Cloud templates
{: #sitemap_creating_terraform_on_ibm_cloud_templates}


[Creating Terraform on IBM Cloud templates](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config#create-tf-config)

* [Configuring the `provider` block](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config#configure-provider)

* [Adding {{site.data.keyword.cloud_notm}} resources to the `resource` block](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config#configure-resources)

    * [Referencing resources in other resource blocks](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config#reference-resource-info)

* [Using `variable` blocks to customize resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config#configure-variables)

    * [Referencing variables](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config#reference-variables)

* [Storing your Terraform on IBM Cloud templates](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config#store-template)


## Creating a deployment to IBM Cloud Schematics link
{: #sitemap_creating_a_deployment_to_ibm_cloud_schematics_link}


[Creating a deployment to IBM Cloud Schematics link](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create_deploy_to_schematics#create_deploy_to_schematics)

* [Adding an image on deployment to {{site.data.keyword.cloud_notm}} link](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create_deploy_to_schematics#add_an_image)


## IBM Cloud Provider release and updates
{: #sitemap_ibm-cloud-provider-release-and-updates}

[IBM Cloud Provider release and updates](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}


## FAQs
{: #sitemap_faqs}


[FAQs](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#faqs)

* [How do I find the flavor and parameters to configure a virtual service instance in {{site.data.keyword.Bluemix_notm}}?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#vsi_config)

* [How long does it take for my resources to provision and delete?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#provisioning_times)

* [How do I set up Terraform on IBM Cloud greater than v0.13.0 ?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#ibm-terraform-provider-v13)

* [How can I resolve the error when provisioning a `ibm_container_alb_cert` resource with secret?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#provision-ibm-container-alb-cert)

* [How can I set or add multiple address prefixes to the configuration file when provisioning VPC?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#addressprefix)

* [How do I define a policy which has all resource groups?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#policy-faq)

* [How do I configure policy for all services in all the resource groups for an user?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#user-policy-faq)

* [How can I configure a target resource to connect from different regions?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#target-regions-faq)

* [How can I connect and retrieve information from multiple region at once in the same template?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-parameter-faq)

* [How do I assign multiple resources to a group policy?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-resource-gpolicy)

* [How can I create access group policies and add memo as an attribute to the policy?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-attributes-gpolicy)

* [How do I create the Terraform resources of the same type in sequential order?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-squential-terrreso)

* [How do I enable the User list visibility for the IAM in Terraform?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-userlistvisibility-iam)

* [Can I configure the `ibm_container_cluster` Terraform resource to control the IPs on the {{site.data.keyword.cos_full_notm}} bucket?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-ibmcontainerclus-terraform)

* [Can I retrieve a list of all the existing {{site.data.keyword.vsi_is_short}}s from all the regions by using Terraform?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-retrievelist-terraform)

* [How can I edit the flavor of an existing IKS worker pool without deleting or destroying an existing one by updating its machine_type?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-flavoriks-machinetype)

* [How can I secure a workspace by setting an environment variable?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-squential-envvariable)

* [How can I create `ibm_function_trigger` with Terraform that connects to an Event Stream?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-functional-trigger)

* [How do I associate a public gateway while creating multiple zones with a Subnet for each zone?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#alias-multiplezone-subnet)

* [How can I resolve the unexpected HTTP status code 502 (502 Bad Gateway) null error when deploying an instance of IBM Cloud Database RabbitMQ by using Terraform?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#deploy-icdrabbitmq-faq)

* [How can I resolve cross-origin resource sharing (CORS) configuration issue while creating a cloudant instance?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#cos-instance-faq)

* [Can I increase or decrease timeouts while deleting Terraform resource?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#timeouts-resource-faq)

* [Can I update the changes into the current existing Terraform file?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#setchanges-terraform-faq)

* [How can I run Terraform files sequentially based on the results in {{site.data.keyword.bplong_notm}}?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#terraform-result-faq)

* [Can I always set Terraform to use the latest or default version?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#terraform-defaultversion-faq)

* [If I set `"type”: = “terraform_v1.0"` in the JSON file as shown in the code block, will `Terraform version 1.0` continue to use even if `Terraform version 2.0` or higher are released?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#terraform-type-faq)

* [Can I specify only the provider version in the `version` parameter? Or is it mandatory to provide the `required_version` parameter in the `versions.tf` file?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#terraform-reqparam-faq)

* [How can I deploy one resources in two different {{site.data.keyword.cloud_notm}} account?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#terraform-depolyresource-faq)

* [Can I automate the certificates to the Secrets Manager by using Terraform provider?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-faqs#terraform-secretmanager-faq)


## Getting help and support
{: #sitemap_getting_help_and_support}


[Getting help and support](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-gettinghelp#gettinghelp)

* [For instance](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-gettinghelp#for-instance)


## What's new in Terraform on IBM Cloud?
{: #sitemap_whats_new_in_terraform_on_ibm_cloud}


[What's new in Terraform on IBM Cloud?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#new-in-terraform)

* [September 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#sept-2021)

* [August 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#aug-2021)

* [31 July 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#31-July-2021)

* [9 June 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#9-June-2021)

* [20 May 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#20-may-2021)

* [26 April 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#26-april-2021)

* [4 April 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#4-april-2021)

* [1 April 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#1-april-2021)

* [16 March 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#16-march-2021)

* [04 March 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#04-march-2021)

* [17 February 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#17-february-2021)

* [28 January 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#28-january-2021)

* [13 January 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#13-january-2021)

* [29 December 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#29-december-2020)

* [14 December 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-new-in-terraform#14-december-2020)


## Version changelog
{: #sitemap_version_changelog}


[Version changelog](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#provider-changelog)

* [Change log from 1.23.2 till date](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-versiontaglist)

* [Change log for 1.23.2, released 20 April 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1232)

* [Change log for 1.23.1, released 9 April 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1231)

* [Change log for 1.23.0, released 4 April 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1230)

* [Change log for 1.22.0, released 31 March 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1220)

* [Change log for 1.21.2, released 16 March 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1212)

* [Change log for 1.21.1, released 4 March 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1211)

* [Change log for 1.21.0, released 12 February 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1210)

* [Change log for 1.20.1, released 27 January 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1201)

* [Change log for 1.20.0, released 25 January 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1200)

* [Change log for 1.19.0, released 9 January 2021](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1190)

* [Change log for 1.18.0, released 24 December 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1180)

* [Change log for 1.17.0, released 10 December 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1170)

* [Change log for 1.16.1, released 2 December 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1161)

* [Change log for 1.16.0, released 2 December 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1160)

* [Change log for 1.15.0, released 26 November 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1150)

* [Change log for 1.14.0, released 29 October 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1140)

* [Change log for 1.13.1, released 7 October 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1131)

* [Change log for 1.13.0, released 1 October 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1130)

* [Change log for 1.12.0, released 14 September 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1120)

* [Change log for 1.11.2, released 3 September 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1112)

* [Change log for 1.11.1, released 28 August 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1111)

* [Change log for 1.11.0, released 25 August 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1110)

* [Change log for 1.10.0, released 6 August 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v1100)

* [Change log for 1.9.0, released 22 July 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v190)

* [Change log for 1.8.0, released 23 June 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v180)

* [Change log for 1.7.1, released 11 June 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v171)

* [Change log for 1.7.0, released 29 May 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v170)

* [Change log for 1.6.0, released 20 May 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v160)

* [Change log for 1.5.3, released 19 May 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v153)

* [Change log for 1.5.2, released 7 May 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v152)

* [Change log for 1.5.1, released 4 May 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v151)

* [Change log for 1.5.0, released 29 April 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v150)

* [Change log for 1.4.0, released 16 April 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v140)

* [Change log for 1.3.0, released 2 April 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v130)

* [Change log for 1.2.6, released 26 March 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v126)

* [Change log for 1.2.5, released 19 March 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v125)

* [Change log for 1.2.4, released 10 March 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v124)

* [Change log for 1.2.3, released 3 March 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v123)

* [Change log for 1.2.2, released 26 February 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#changelog-v122)

* [Change log for 1.2.1, released 13 February 2020](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-changelog#121)


## Troubleshooting
{: #sitemap_troubleshooting}



### Debugging Kubernetes service errors
{: #sitemap_debugging_kubernetes_service_errors}


[How can I resolve the network error when working with the {{site.data.keyword.containershort_notm}} provider?](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-ks-network-error#ks-network-error)
