<staging>
---

copyright:
  years: 2017, 2021
lastupdated: "2021-08-16"

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


# IBM Cloud service teams Terraform Provider engagement process
{: #tf-engagement-process}


## Executive summary
{: #tf-exec-summary}

This is the simple process to engage with IBM Cloud service teams and how to plan and update Terraform provider capabilities and features for the services. It includes
engaging those teams that don't yet have the TF provider as required by Service Framework item UX030
engaging those teams that need to pick up the current TF Provider support and keep it up-to-date
opening new requests & defects against those teams with regard to the service's TF providers


## Background
{: #tf-background}

IBM Cloud services are required under Service Framework item UX030 to create and maintain critical IBM Cloud automation integration with their service. Automation is a cornerstone of every Cloud, and also needs to be in IBM Cloud, it has been repeatedly confirmed that automation is critical to our largest IBM Cloud customers. This very simple process allows Service Teams and external / internal users of those services to act on these automation requirements, and to track the implementation commitments and delivery dates.


## Engagement actions
{: #tf-engagement-actions}

There are several important interactions that "Service Teams" and "Terraform Users" can engage in with regard to Terraform Providers. AHA Epics will be created on Service Team AHA boards for tracking.

If you are a Service Team that is engaged with your own Service Provider work, go to "Service Teams".
If you need a Service Team to handle a new request or problem, go to "End Users".


## Service teams
{: #tf-svc-teams}

As required in the mandatory Service Framework item UX030, all IBM Cloud services need to create and maintain their Terraform Provider for their service. Some of been previous created for them and they need to take ownership, others have not been created and need to be started. This is the current tracking page for the overall service TF Provider ownership is here

## Query to track the Terraform service team ownership
{: #tf-query}

- **Task** Create the Service Terraform Provider
- **Description** If the TF provider has not already been created, it needs to be created. SF UX030 has full details how to do that for the Service Team. As part of this activity, the teams are expected to
            - Create TF provider support for their service as per the guidelines.
            - Include TF testing as part of their sanity test runs (for every release)
            - Handle all support tickets raised by customers
            - Use this AHA tagging: TF-service-create


- **Task** Take ownership of the already existing Terraform Provider for their service
- **Description** If the TF provider has been created, it needs to be taken over and owned by the Service team. SF UX030 has full details how to do that for the Service Team. As part of this activity, the teams are expected to
            - Take over the current Terraform support and keep it up-to-date
            - Include TF testing as part of their sanity test runs (for every release)
            - Handle all support tickets raised by customers. Use this AHA tagging: TF-service-ownership

## End Users
{: #end-users}

End users, internal or external, need things added and fixed. These track those requests and defects to ensure proper attention.

## Query to track these: TF Service - Requests
{: #track-requests}


- **Task** Service Terraform Provider Request
- **Description** The TF Provider for a given service doesn't handle something it should and needs to be enhanced
- **AHA tagging** Access AHA items, provide tag as `TF-service-enhancement`.
    1. Access **Internal User action** Go here => TF Service - Requests & Defects
    2. Hit "Add Structured idea" blue button
    3. Workspace: "Schematics Service" 
    4. Name: <Brief information>
    5. Description: More details - who to talk to for reference or a Github or something would help, who exactly is requesting project it is for, external customer needing, etc - the more meta-data the more it helps. Refresh that link and make sure it shows up. This filters automatically on "needs review" so clear that filter if it's been changed and you want to find out where it is

## Query to track these: TF Service - Defects
{: #track-defects}

- **Task** Service Terraform provider defect
- **Description** The TF Provider for the given service has a defect and it needs to be fixed
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