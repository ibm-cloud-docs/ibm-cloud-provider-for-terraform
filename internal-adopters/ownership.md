---

copyright:
    years: 2017, 2024
lastupdated: "2024-03-15"

keywords: terraform ownership, transferring terraform ownership, service ownership

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}


# Service team's Terraform provider engagement
{: #tf-engagement-process}


## Summary
{: #tf-exec-summary}

This is the process to engage with the {{site.data.keyword.cloud}} service teams to plan and update Terraform provider capabilities and features for their services. This includes
- Engaging those service teams that have yet to create the Terraform provider as required by [Service Framework item UX030](/docs/service-framework?topic=service-framework-user-experience-ux-#ux030-terraform-provider)
- Engaging those teams that need to pick up the current Terraform provider support and keep the services up-to-date
- Opening new requests and defects against those teams with regard to the service's Terraform providers
{: shortdesc}

## Background
{: #tf-background}

{{site.data.keyword.cloud_notm}} services are required according to the [Service Framework item UX030](/docs/service-framework?topic=service-framework-user-experience-ux-#ux030-terraform-provider) to create and maintain critical {{site.data.keyword.cloud_notm}} automation and integration with their services.
Automation is a cornerstone of every cloud, it has been repeatedly confirmed that automation is critical to our largest {{site.data.keyword.cloud_notm}} customers. This process allows service teams, and external or internal users of those services, to act on automation requirements to track the implementation commitments and delivery dates.
{: shortdesc}

## Engagement actions
{: #tf-engagement-actions}

There are important interactions that `service teams` and `Terraform users` can engage in, with regard to the Terraform providers. AHA board structured ideas will be created for service teams to consider on the query [Terraform Provider ideas for all services](https://bigblue.aha.io/bookmarks/custom_pivots/7015632373147204205/7015632562260682181).

- If you are a service team that is engaged with your own service provider task, refer to [Service teams](#tf-svc-teams) to know more information.
- If you need a service team to handle a new request or a problem, refer to [users](#end-users) to know more information.

## Service teams
{: #tf-svc-teams}

As required in the mandatory [Service Framework item UX030](/docs/service-framework?topic=service-framework-user-experience-ux-#ux030-terraform-provider, all {{site.data.keyword.cloud_notm}} services need to create and maintain their Terraform provider for their service. 

For more information, about creating Terraform provider for your service, see [Creating and owning your Terraform provider](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-tf-transfer-ownership) documentation.
{: shortdesc}

The overall ownership details of the Terraform provider support are listed [here](https://github.ibm.com/blueprint/terraform-getting-started/blob/master/Adopters.md).
{: important}

### Tracking the Terraform service team ownership
{: #tf-query}

**Task** Create the Service Terraform provider.

**Description** If the Terraform provider has not already been created, it needs to be created. [Service Framework item UX030](/docs/service-framework?topic=service-framework-user-experience-ux-#ux030-terraform-provider) has the complete information. As part of this activity, the teams are expected to
- have an [AHA item](https://bigblue.aha.io/bookmarks/idea_grids/6978999499627562927/6978999940899169319){: external} in your service board and add the tag as `TF-service-create`.
- create Terraform provider support for their service according to the guidelines.
- include Terraform testing as part of their sanity test runs on every release.
- handle all support tickets raised by the customers.

**Task** Take ownership of the already existing Terraform provider for their service.

**Description** If the Terraform provider is created, service team need to take over the ownership. [Service Framework item UX030](/docs/service-framework?topic=service-framework-user-experience-ux-#ux030-terraform-provider) has the complete information. As part of this activity, the team is expected to following these steps.
- Have an [AHA item](https://bigblue.aha.io/bookmarks/idea_grids/6978999499627562927/6978999940899169319){: external} in your service board and add the tag as `TF-service-ownership`.
- Take over the current Terraform support and keep it up to date.
- Include Terraform testing as part of their sanity test runs (for every release).
- Handle all support tickets raised by the customers.
 

## Users
{: #end-users}

Users, internal, or external, may have new enhancement requirements and defects that need to be addressed by the Service Terraform provider.

### Tracking the Terraform service enhancement and defects
{: #tf-req-defects-query}

**Task** Service Terraform provider enhancement

**Description** The Terraform provider for a given service needs enhancements to the current implementation.

**Internal user action:**

- Raise a GitHub issue [here](https://github.com/IBM-Cloud/terraform-provider-ibm/issues) or if you know the team information, open up an [Internal structured idea](https://internal-ibmcloud.ideas.aha.io/ideas) yourself. Please provide requirement details such as, who exactly is requesting? the requesting project details, and customer need.
- Tag the issues with the cloud service name and the enhancement tag as `TF-service-enhancement`.
- Notify the request to the Terraform team on `#terraform-ibmcloud-users` slack channel.
- The Terraform team will triage the issues and will open up corresponding issues on the service offering AHA board, and update the AHA issue with the required information by using AHA tagging as `TF-service-enhancement`.

**Task** Service Terraform provider defect

**Description** The Terraform provider for the given service has a defect and it needs to be fixed.

**Internal user action:**

- Raise a GitHub issue [here](https://github.com/IBM-Cloud/terraform-provider-ibm/issues) or if you know the team information, open up an [Internal structured idea](https://internal-ibmcloud.ideas.aha.io/ideas) yourself.
- An IBMer can notify the request to the Terraform team on `#terraform-ibmcloud-users` slack channel. Non-IBMer can notify the Terraform team by using the [public workspace](https://ibm-cloud-schematics.slack.com/archives/C4R15M6SZ).
- Tag the issues with the appropriate cloud service name and the defect tag as `TF-service-defect`.
- Notify the request to the Terraform team on `#terraform-ibmcloud-users` slack channel.
- The Terraform team will triage the issues and will open up corresponding issues on the service offering AHA board, and update the AHA issue with the required information by using AHA tagging as `TF-service-defect`.

## FAQ
{: #ownership-faq}

### Why AHA and not GitHub?
{: #faq-epic}

 AHA is used only because it's the proper way for teams to communicate with each other to ensure tracking and resolution of the issues. More importantly, although AHA workspaces are well known, GitHub are not. Thus you need to take the AHA Epics opened against the service to create the GitHub execution steps as you need. But the AHA Epic will always be the master record, please do not delete or remove that Epic until resolved.
