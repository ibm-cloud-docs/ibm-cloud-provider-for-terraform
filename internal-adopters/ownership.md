<staging>
---

copyright:
  years: 2017, 2021
lastupdated: "2021-08-19"

keywords: terraform ownership, transferring terraform ownership, service ownership

subcollection: ibm-cloud-provider-for-terraform

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Service teams versus Terraform provider
{: #tf-engagement-process}


## Executive summary
{: #tf-exec-summary}

This is the simple process to engage with the {{site.data.keyword.cloud}} service teams to plan and update Terraform provider capabilities and features for the services. This includes 
- engaging those service teams that are yet to have the Terraform provider as required by [Service Framework item UX030](/docs/service-framework?topic=service-framework-one-cloud-3q20-updates#currency3q20-ux030-terraform-provider). 
- engaging those teams that need to pick up the current Terraform provider support and keep the services up-to-date.
- opening new requests and defects against those teams with regard to the service's Terraform providers.
{: shortdesc}

## Background
{: #tf-background}

{{site.data.keyword.cloud_notm}} services are required under [Service Framework item UX030](/docs/service-framework?topic=service-framework-one-cloud-3q20-updates#currency3q20-ux030-terraform-provider) to create and maintain critical {{site.data.keyword.cloud_notm}} automation and integration with their services. 
Automation is a cornerstone of every cloud, and also needs to be in {{site.data.keyword.cloud_notm}}, it has been repeatedly confirmed that automation is critical to our largest {{site.data.keyword.cloud_notm}} customers. This  process allows service teams, and external or internal users of those services to act on an automation requirements to track the implementation commitments and delivery dates.

## Engagement actions
{: #tf-engagement-actions}

There are several important interactions that `service teams` and `Terraform users` can engage in, with regard to Terraform providers. 

[AHA Epics](https://bigblue.aha.io/bookmarks/idea_grids/6978999499627562927/6978999940899169319) will be created on service team AHA boards for tracking.

- If you are a service team that is engaged with your own service provider task, click [Service teams](#tf-svc-teams) to know more information.
- If you need a service team to handle a new request or a problem, click [End users](#end-users) to know more information.

## Service teams
{: #tf-svc-teams}

As required in the mandatory [Service Framework item UX030](/docs/service-framework?topic=service-framework-one-cloud-3q20-updates#currency3q20-ux030-terraform-provider), all {{site.data.keyword.cloud_notm}} services need to create and maintain their Terraform Provider for their service. Some of service created by the Terraform team, need to take ownership. The service team that have not been created need to start.Here is the current tracking page for the overall [service Terraform provider ownership](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-adopting-terraform-provider-in-the-service).

### Tracking the Terraform service team ownership
{: #tf-query}

**Task** Create the Service Terraform Provider
**Description** If the Terraform provider has not already been created, it needs to be created. [Service Framework item UX030](/docs/service-framework?topic=service-framework-one-cloud-3q20-updates#currency3q20-ux030-terraform-provider) has the complete information of how to do that for the service team. As part of this activity, the teams are expected to
- create Terraform provider support for their service as per the guidelines.
- include Terraform testing as part of their sanity test runs (for every release).
- handle all support tickets raised by the customers.
- use AHA tag as **TF-service-create**.

**Task** Take ownership of the already existing Terraform Provider for their service

**Description** If the Terraform provider is created, service team need to take over the ownership. [Service Framework item UX030](/docs/service-framework?topic=service-framework-one-cloud-3q20-updates#currency3q20-ux030-terraform-provider) has the complete information of how to do that for the service team. As part of this activity, the teams are expected to
- take over the current Terraform support and keep it up-to-date.
- include Terraform testing as part of their sanity test runs (for every release).
- handle all support tickets raised by the customers. 
- use AHA tag as **TF-service-ownership**.

## End Users
{: #end-users}

The end users, internal or external, need their services to be added and fixed. These tracks those requests and defects to ensure proper attention.

## Query to track these: Terraform Service - Requests
{: #track-requests}

**Task** Service Terraform provider request
**Description** The Terraform Provider for a given service doesn't handle something it should and needs to be enhanced.
**AHA tagging** Access [AHA items](https://bigblue.aha.io/bookmarks/idea_grids/6978999499627562927/6978999940899169319){: external} and use AHA tag as `TF-service-enhancement`.
   - Access **Internal User action**. click  **Terraform Service -> Requests and Defects**.
   - Click **Add Structured idea** blue button. Provide your service name, for example, `Workspace **Schematics Service**` 
   - Enter the brief information in the **Name** field. 
   - Enter the short description having 
      * whom to coordinate for reference or a Github or something would help?
      * who exactly is requesting the project? For example, `external customer or internal enhancement`. 
      * refresh the link and make sure the description shows up. This filters automatically on **needs review** so clear that filter if it's been changed and you want to find out where it is.

## Query to track these: Terraform Service - Defects
{: #track-defects}

- **Task** Service Terraform provider defect
- **Description** The Terraform Provider for the given service has a defect and it needs to be fixed
- **AHA tagging** TF-service-defect

**Internal User Action**

Option 1: 

Raise a github issue here - https://github.com/IBM-Cloud/terraform-provider-ibm/issues. An IBMer can notify the terraform team, using this #terraform-ibmcloud-users channel. Non-IBMer can notify the terraform team using this public workspace https://ibm-cloud-schematics.slack.com/archives/C4R15M6SZ.

Please tag the issues with the appropriate Cloud Service name. The IBM Cloud Services team & the terraform team will respond.
The Terraform team will triage the issues and will open up corresponding issues on the Service offering and update the issues here with the new service team open issue.
{: note}

## FAQ
{: ownership-faq}

**Questions** - Why Epics and not GitHub?

**Reply** - we dont know your github - so we open Epics and you create the github execution step