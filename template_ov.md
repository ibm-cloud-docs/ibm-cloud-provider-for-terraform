---

copyright:
  years: 2017, 2021
lastupdated: "2021-08-24"

keywords: terraform templates, schematics template

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




# Sample {{site.data.keyword.cloud_notm}} Terraform templates
{: #sample_terraformtemplates}

All the templates uses the Terraform on {{site.data.keyword.cloud_notm}} version 0.12 format.
{: note}

The deploy to {{site.data.keyword.cloud_notm}} URL is an efficient way for you to enable users to deploy solutions on {{site.data.keyword.cloud_notm}} from a public Git repository sample configuration. The URL requires minimal configuration and you can insert it anywhere in your documentation that supports markup. When the user clicks the hyper link, they are taken directly to the {{site.data.keyword.bpshort}} workspace setup page and only need to click the create button for workspace creation in {{site.data.keyword.bpshort}}.
{: shortdesc}

When you click the `Deploy to {{site.data.keyword.cloud_notm}}` following actions occur:

    1. If the user does not have an active {{site.data.keyword.cloud_notm}} account, you must create a trial account or a real account.

    2. The user can select a region, resource group (available in the Dallas, Washington, London, Frankfurt, and Tokyo regions) or organization and space (available in the Dallas, London, and Frankfurt regions).

    3. The auto deploy link set up a create workspace in the {{site.data.keyword.bplong_notm}}.

    4. To execute `generate plan` successfully, you need to configure the required variables.






## API Gateway templates
{: #api-gwy-template}

<table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
        <tr>
        <td><code>ibm-api-gateway</code></td>
        <td>Create an <a href="/docs/api-gateway?topic=api-gateway-whatis_apigw">IBM Cloud API Gateway</a> service instance to set up an API for an IBM Cloud service of your choice. You can specify the API endpoint that you want to use to access your service, and define subscription keys so that developers can securely consume your API.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_resource_instance</code></li><li style="margin:0px; padding:0px"><code>ibm_api_gateway_endpoint</code></li><li style="margin:0px; padding:0px"><code>ibm_api_gateway</code></li><li style="margin:0px; padding:0px"><code>ibm_api_gateway_endpoint_subscription</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-api-gateway&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    </tbody>
    </table>

## Certificate Manager templates
{: #cert-mgr-template}

    <table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
    <tr>
    <td><code>ibm-certificate-manager-order</code></td>
        <td> Create an {{site.data.keyword.cis_full_notm}} instance with a domain, and use <a href="/docs/certificate-manager?topic=certificate-manager-about-certificate-manager">IBM Cloud Certificate Manager</a> to generate a TLS certificate for this domain.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_resource_instance</code></li><li style="margin:0px; padding:0px"><code>ibm_cis</code></li><li style="margin:0px; padding:0px"><code>ibm_cis_domain</code></li><li style="margin:0px; padding:0px"><code>ibm_certificate_manager_order</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-certificate-manager/ibm-certificate-manager-order"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-certificate-manager/ibm-certificate-manager-order&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
        </tr>
    </tbody>
    </table>

## Cloud Foundry templates
{: #cloud-foundry-template}

    <table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
        <tr>
        <td><code>ibm-app</code></td>
        <td>Create and deploy a Cloud Foundry app in {{site.data.keyword.cloud_notm}}.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>null_resource</code></li><li style="margin:0px; padding:0px"><code>ibm_app_route</code></li><li style="margin:0px; padding:0px"><code>ibm_service_instance</code></li><li style="margin:0px; padding:0px"><code>ibm_service_key</code></li><li style="margin:0px; padding:0px"><code>ibm_app</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-app"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-app&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
</tbody>
</table>


## Direct Link templates
{: #dl-template}

    <table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
    <tr>
        <td><code>ibm-dl-gateway</code></td>
        <td>Create a speed and reliable direct link gateways, virtual connections, offering information, routers, and ports by using the resources.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_dl_gateway</code></li><li style="margin:0px; padding:0px"><code>ibm_dl_virtual_connection</code></li><li style="margin:0px; padding:0px"><code>ibm_is_vpc</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-direct-link"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-direct-link&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    </tbody>
    </table>

## Event Streams templates
{: #event-stream-template}

    <table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
    <tr>
        <td><code>ibm-event-streams</code></td>
        <td>Create a communication through an Event Streams instance, topic instance, or Kafka consumer application to connect an existing event stream instances and its topic instance by using {{site.data.keyword.bplong_notm}} workspace.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_resource_instance</code></li><li style="margin:0px; padding:0px"><code>ibm_event_streams_topic</code></li><li style="margin:0px; padding:0px"><code>kafka_consumer_app</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-event-streams"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-event-streams&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    </tbody>
    </table>


## Functions templates
{: #func-template}

<table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
        <tr>
    <td><code>ibm-function-cloudant-trigger</code></td>
    <td>Create a Cloudant NoSQL service instance and a Python app deployment that creates the <code>database demo</code> database in your service instance. Then, you create an action with {{site.data.keyword.cloud_notm}} functions that is triggered when you add or edit documents to your database.<br><br><strong>Resources</strong><br>
        <ul style="margin:0px 0px 0px 20px; padding:0px">
        <li style="margin:0px; padding:0px"><code>null_resource</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_service_instance</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_service_key</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_app_route</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_app</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_function_package</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_function_action</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_function_trigger</code></li>
        <li style="margin:0px; padding:0px"><code>ibm_function_rule</code></li>
        </ul></td>
    <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-function-cloudant-trigger"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-function-cloudant-trigger&terraform_version=terraform_v0.12"><img  alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    </tbody>
    </table>

## Identity & Access (IAM) templates
{: #iam-template}

    <table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
    <tr>
        <td><code>ibm-iam-custom-role</code></td>
        <td>Create a custom role in IBM Cloud Identity and Access Management (IAM) for IBM Cloud Key Protect.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_iam_custom_role</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-custom-role"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-custom-role&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    <tr>
        <td><code>ibm-iam-policy</code></td>
        <td>Create an access policy in IBM Cloud Identity and Access Management (IAM) to grant permissions for a resource group to a user.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_iam_user_policy</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-policy"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iam-policy&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    </tbody>
    </table>

## Key Management Service templates
{: #kms-template}

    <table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
    <tr>
        <td><code>ibm-key-management-service</code></td>
        <td>Create an {{site.data.keyword.cos_full_notm}} service instance with a bucket to store your data and provide a key management service resource for Hyper Protect Crypto Services and Key Protect service instance with a root key. This allow access between these services with an IBM Cloud Identity and Access Management policy.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_kms_key</code></li><li style="margin:0px; padding:0px"><code>ibm_kp_key</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-kms"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-kms&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    </tbody>
    </table>  

## Kubernetes templates
{: #kubernetes-template}

<table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
    <tr>
    <td><code>vpc-classic-cluster</code></td>
        <td>Create an {{site.data.keyword.containerfull_notm}} cluster in a Virtual Private Cloud (VPC) for Generation 1 compute with worker nodes in a default worker pool that you spread across two zones. You can provision an IBM Cloud Object Storage service, and bind this service to the cluster.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_is_vpc</code></li><li style="margin:0px; padding:0px"><code>ibm_is_subnet</code></li><li style="margin:0px; padding:0px"><code>ibm_container_vpc_cluster</code></li><li style="margin:0px; padding:0px"><code>ibm_container_vpc_worker_pool</code></li><li style="margin:0px; padding:0px"><code>ibm_resource_instance</code></li><li style="margin:0px; padding:0px"><code>ibm_container_bind_service</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster/vpc-classic-cluster"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster/vpc-classic-cluster&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    <tr>
    <td><code>vpc-Gen2-cluster</code></td>
        <td>Create an {{site.data.keyword.containerfull_notm}} cluster in a Virtual Private Cloud (VPC) for Generation 2 compute with worker nodes in a default worker pool that you spread across two zones. Also, you provision an IBM Cloud Object Storage service, and bind this service to the cluster.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_is_vpc</code></li><li style="margin:0px; padding:0px"><code>ibm_is_subnet</code></li><li style="margin:0px; padding:0px"><code>ibm_container_vpc_cluster</code></li><li style="margin:0px; padding:0px"><code>ibm_container_vpc_worker_pool</code></li><li style="margin:0px; padding:0px"><code>ibm_resource_instance</code></li><li style="margin:0px; padding:0px"><code>ibm_container_bind_service</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster/vpc-gen2-cluster"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-cluster/vpc-gen2-cluster&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    <tr>
    <td><code>ibm-iks-classic-ROKS</code></td>
        <td>Create a Red Hat View GitHub repository on IBM Cloud cluster that runs version 3.11 of the View GitHub repository Container Platform.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_container_cluster</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iks-classic-ROKS"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-iks-classic-ROKS&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>
    </tr>
    </tbody>
    </table>


## Transit Gateway templates
{: #transit-gwy-template}

    <table>
    <thead>
    <th style="width:60px">Name</th>
    <th style="width:250px">Description and resources</th>
    <th style="width:150px">Access</th>
    </thead>
    <tbody>
    <tr>
        <td><code>ibm-transit-gateway</code></td>
        <td>Create a transit gateways, list available connections, and locations for the gateways.<br><br><strong>Resources</strong><br><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><code>ibm_tg_gateway</code></li><li style="margin:0px; padding:0px"><code>ibm_tg_connection</code></li><li style="margin:0px; padding:0px"><code>ibm_is_vpc</code></li></ul></td>
        <td><a href="https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-transit-gateway"><img alt="View Git Hub" src="/images/viewgithub.png"></a><br><br><a href="https://cloud.ibm.com/schematics/workspaces/create?repository=https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-transit-gateway&terraform_version=terraform_v0.12"><img alt="Deploy to Schematics" src="/images/deploytoschematics.png"></a></td>

    </tr>
    </tbody>
    </table>






