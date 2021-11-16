---

copyright:
  years: 2017, 2021
lastupdated: "2021-11-16"

keywords: ibm cloud region, location, region, ibm cloud location

subcollection: ibm-cloud-provider-for-terraform

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my database provisioning success in us-east and us-south, but fails in eu-de region?
{: #db-provisioning-eu-de}

To know about the services provided in specific region and resource deployment, refer to, [locations for resource deployment](/docs/overview?topic=overview-locations)
{: shortdesc}

{: tsSymptoms}

You have set up your database in `us-east` region and provisioning a database backup in `us-south` region, the set up is working as expected. Whereas, when you provision a backup in `eu-de` region following error message are displayed.

```
Error: Error creating database instance: Request failed with status code: 400, ServerErrorResponse: {"error_code":"RC-ServiceBrokerErrorResponse","message":"[500, Internal Server Error] We were unable to complete your request. Try again later or contact support if the issue persists.
```
{: codeblock}

There is a constraint in the {{site.data.keyword.cloud_notm}} region, that you cannot provision a database backup ID from `us-east` region to `eu-de` region. Hence, you are receiving an internal server error stating that database creation request failed.
{: tsCauses}

Use one of the following options to fix this issue:
- You configure database and workspace resources in one region.
- To access the database or to backup the database resources in another region. You need to check the region constraints in the {{site.data.keyword.cloud_notm}} location. For more detailed information, about services provided in specific regions and resource deployment, refer to [locations for resource deployment](/docs/overview?topic=overview-locations).
- You need to check the price, billing usage, and region specific capabilities before communicating between the regions.
{: tsResolve}



