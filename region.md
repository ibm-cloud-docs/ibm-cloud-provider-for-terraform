---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-05"

keywords: ibm cloud region, location, region, ibm cloud location

subcollection: terraform

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:step: data-tutorial-type='step'}



# Why is my database provisioning success in us-east and us-south, but fails in eu-de region?
{: #db-provisioning-eu-de}

In the {{site.data.keyword.cloud_notm}} global network of location to host your highly available resources and service instances workload. You can create resources in different regions but with the same billing and usage view, and deploy your resources and application to the location that is nearest to your customers to achieve low application latency. For more information, about location, refer to [Locations](/docs/overview?topic=overview-locations)
{: shortdesc}

**What’s happening?**

You have setup database in `us-east` and provisioning a database backup in `us-south`, the setup is working as expected. Whereas, when you provision a backup in `eu-de` region following error message is displayed.

```
Error: Error creating database instance: Request failed with status code: 400, ServerErrorResponse: {"error_code":"RC-ServiceBrokerErrorResponse","message":"[500, Internal Server Error] We were unable to complete your request. Try again later or contact support if the issue persists.
```
{: pre}

**Why it’s happening?**

There is a constraint in the {{site.data.keyword.cloud_notm}} region, that you cannot provision a database backup ID from `us-east` region to `eu-de` region. Hence, you are receiving and internal server error stating that creating database request failed.

**How to fix it?**

Use one of the following options to fix this issue:
 - You configure database and workspace resources in one region.
 - To access the database or store a backup of the database resources in another region. You need to cross refer the constraints of the region in the {{site.data.keyword.cloud_notm}} location documentation. For more information, about the services provided in specific region, refer to [Services region](/docs/overview?topic=overview-services_region#paas-services).
 - You need to check the price, billing usage, and capability of the region before communicating between the regions.

