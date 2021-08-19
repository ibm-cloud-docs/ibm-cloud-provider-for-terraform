---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-19"

keywords: terraform resources, terraform modules, terraform provider, terraform autodeploy, 

subcollection: ibm-cloud-provider-for-terraform

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# What's new in Terraform on {{site.data.keyword.cloud_notm}}?
{: #new-in-terraform}

Learn about the latest changes to the Terraform on {{site.data.keyword.cloud_notm}} service that are grouped by month.

## 31 July 2021
{: #31-July-2021}

<table>
    <thead>
    <th style="width:80px">Releases, updates and enhancements</th>
    </thead>
    <tbody>
        <tr>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><strong>Enhancements:</strong> {{site.data.keyword.cloud_notm}} Provider now supports Terraform v0.15</li><li style="margin:0px; padding:0px">For the latest <code>Resources</code>, <code>Data sources</code>, <code>Enhancements</code>, and <code>Bug fixes</code>, see <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.29.0">Updates and fixes in v1.29.0</a></li><li style="margin:0px; padding:0px">For the latest <code>Resources</code>, <code>Data sources</code>, <code>Enhancements</code>, and <code>Bug fixes</code>, see <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.28.0">Updates and fixes in v1.28.0</a></li><li style="margin:0px; padding:0px">For the latest <code>Resources</code>, <code>Data sources</code>, <code>Enhancements</code>, and <code>Bug fixes</code>, see <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.27.2">Updates and fixes in v1.27.2</a></li></ul></td>
    </tr>
    </tbody>
    </table> 

## 9 June 2021
{: #9-June-2021}

<table>
    <thead>
    <th style="width:80px">Releases and updates</th>
    </thead>
    <tbody>
        <tr>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">For the latest <code>Resources</code>, <code>Data sources</code>, <code>Enhancements</code>, and <code>Bug fixes</code>, see <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.26.0">Updates and fixes in v1.26.0</a></li></ul></td>
    </tr>
    </tbody>
    </table> 

## 20 May 2021
{: #20-may-2021}

<table>
    <thead>
    <th style="width:80px">Releases and updates</th>
    </thead>
    <tbody>
        <tr>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">For the latest <code>Resources</code>, <code>Data sources</code>, <code>Enhancements</code>, and <code>Bug fixes</code>, see <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.25.0">Updates and fixes in v1.25.0</a></li></ul></td>
    </tr>
    </tbody>
    </table> 

## 26 April 2021
{: #26-april-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">NA</li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">NA</li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support <code>gateway_connection</code> attribute <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpn_gateway_connection#attribute-reference">ibm_is_vpn_gateway_connection</a> resource</li><li style="margin:0px; padding:0px">Support additional attributes for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_subnet_reserved_ip#attribure-reference">ibm_is_subnet_reserved_ip</a> resource</li><li style="margin:0px; padding:0px">Added <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_account_settings#example-usage">ibm_iam_account_settings</a> data source example</li><li style="margin:0px; padding:0px">Support <code>resource_group_id</code> argument in <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/satellite_location#argument-reference">ibm_satellite_location</a> resources and attribute in <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/satellite_location#attributes-reference">ibm_satellite_location</a> data source</li><li style="margin:0px; padding:0px">Support <code>ca-tor</code> region in <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket#argument-reference">ibm_cos_bucket</a> resource.</li><li style="margin:0px; padding:0px">Support <code>private_address</code> attributes for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpn_gateway#attribute-reference">ibm_is_vpn_gateway</a> resource and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpn_gateways#attribute-reference">ibm_is_vpn_gateway</a> data source</li><li style="margin:0px; padding:0px">Support for <code>retention policy</code> argument in <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket#argument-reference">ibm_cos_bucket</a> bucket and attribute in <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cos_bucket#attribute-reference"><code>ibm_cos_bucket</code></a> bucket</li><li style="margin:0px; padding:0px">Latest <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/1.23.2">version1.23.2 change log</a> and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/1.23.1">version1.23.1 change log</a></li></ul></td>
    </tr>
    </tbody>
    </table> 

## 4 April 2021
{: #4-april-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings"><code>ibm_iam_account_settings</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_catalog"><code>ibm_cm_catalog</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_offering"><code>ibm_cm_offering</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_offering_instance"><code>ibm_cm_offering_instance</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_version"><code>ibm_cm_version</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise"><code>ibm_enterprise</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise_account"><code>ibm_enterprise_account</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise_account_group"><code>ibm_enterprise_account_group</code></a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_account_settings"><code>ibm_iam_account_settings</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_catalog"><code>ibm_cm_catalog</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_offering"><code>ibm_cm_offering</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_offering_instance"><code>ibm_cm_offering_instance</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_version"><code>ibm_cm_version</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/enterprises"><code>ibm_enterprises</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/enterprise_accounts"><code>ibm_enterprise_accounts</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/enterprise_account_groups"><code>ibm_enterprise_account_groups</code></a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Latest <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.23.0">version change log</a></li></ul></td>
    </tr>
    </tbody>
    </table> 


## 1 April 2021
{: #1-april-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"> <li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_dedicated_host
"><code>ibm_is_dedicated_host</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_dedicated_host_group"><code>ibm_is_dedicated_host_group</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_subnet_reserved_ip"><code>ibm_is_subnet_reserved_ip</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key_alias"><code>ibm_kms_key_alias</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key_rings"><code>ibm_kms_key_rings</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/ob_logging"><code>ibm_ob_logging</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/ob_monitoring"><code>ibm_ob_monitoring</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pn_application_chrome"><code>ibm_pn_application_chrome</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/satellite_host"><code>ibm_satellite_host</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/satellite_location"><code>ibm_satellite_location</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/schematics_action"><code>ibm_schematics_action</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/schematics_job"><code>ibm_schematics_job</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/schematics_workspace"><code>ibm_schematics_workspace</code></a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_cache_settings"><code>ibm_cis_cache_settings</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host"><code>ibm_is_dedicated_host</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_hosts"><code>ibm_is_dedicated_hosts</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host_group"><code>ibm_is_dedicated_host_group</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host_groups"><code>ibm_is_dedicated_host_groups</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host_profile"><code>ibm_is_dedicated_host_profile</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_keys_rings"><code>ibm_kms_key_rings</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pn_application_chrome"><code>ibm_pn_application_chrome</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/secrets_manager_secret"><code>ibm_secrets_manager_secret</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/secrets_manager_secrets"><code>ibm_secrets_manager_secrets</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/satellite_location"><code>ibm_satellite_location</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet_reserved_ip"><code>ibm_is_subnet_reserved_ip</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet_reserved_ips"><code>ibm_is_subnet_reserved_ips</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/schematics_action"><code>ibm_schematics_action</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/schematics_job"><code>ibm_schematics_job</code></a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support <code>dh_group</code>, <code>key_lifetime</code>, and <code>authentication_algorithm</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_ipsec_policy#argument-reference">ibm_is_ipsec_policy</a>, <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_ike_policy#argument-reference">ibm_is_ike_policy</a> resources</li><li style="margin:0px; padding:0px">Support <code>delegate_vpc</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_routing_table_routes#argument-reference">ibm_is_vpc_routing_table_route</a> resources</li><li style="margin:0px; padding:0px">Support <code>tags</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_security_group#argument-reference">ibm_is_security_group</a> resources</li><li style="margin:0px; padding:0px">Support <code>security-groups</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference">ibm_is_lb</a> resources and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_lb">ibm_is_lb</a> data sources</li><li style="margin:0px; padding:0px">Support <code>public_key</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_ssh_key">ibm_is_ssh_key</a> data sources</li><li style="margin:0px; padding:0px">Support <code>default_network_acl_name</code>, <code>default_security_group_name</code>, <code>default_routing_table_name</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc#argument-reference">ibm_is_vpc</a> resources</li><li style="margin:0px; padding:0px">Support <code>quote_id</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/compute_vm_instance#argument-reference">ibm_compute_vm_instance</a> resources</li><li style="margin:0px; padding:0px">Support <code>serve_stale_content</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_cache_settings#argument-reference">ibm_cis_cache_settings</a> resources</li><li style="margin:0px; padding:0px">Support <code>alias</code>, <code>key_ring_id</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key#argument-reference">ibm_kms_key</a> resources and <code>aliases</code> attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_key#attribute-reference">ibm_kms_key</a> and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_keys#attribute-reference">ibm_kms_keys</a></li>  <li style="margin:0px; padding:0px">Support <code>visibility</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs#argument-reference">{{site.data.keyword.terraform-provider_full_notm}}</a> and deprecated <code>generation</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs#argument-reference">{{site.data.keyword.terraform-provider_full_notm}}</a></li><li style="margin:0px; padding:0px">Updated <code>kind = "nodejs:10"</code>, in example for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/function_action">ibm_function_action</a> resources and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/function_rule">ibm_function_rule</a></li><li style="margin:0px; padding:0px">Latest <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.22.0">version change log</a></li></ul></td>
    </tr>
    </tbody>
    </table> 


## 16 March 2021
{: #16-march-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">NA</li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">NA</li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support <code>logging</code> argument description for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference">ibm_is_lb</a></li><li style="margin:0px; padding:0px">Support <code>accept_proxy_protocol</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_listener#argument-reference">ibm_is_lb_listener</a></li><li style="margin:0px; padding:0px">Added resources timeouts and depreciated wait_time_minutes argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/compute_vm_instance#argument-reference">ibm_compute_vm_instance</a></li><li style="margin:0px; padding:0px">Support <code>tags</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet#argument-reference">ibm_is_subnet</a>, <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_network_acl#argument-reference">ibm_is_network_acl</a>resource and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet#argument-reference">ibm_is_subnet</a> data source</li><li style="margin:0px; padding:0px">Support <code>iam_id</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_id#argument-reference">iam_service_id</a> resource</li><li style="margin:0px; padding:0px">Added <code>checksum</code> attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_image#attribute-reference">ibm_is_image</a>, <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_images#attribute-reference">ibm_is_images</a> data sources and for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_image">ibm_is_image</a> resource</li><li style="margin:0px; padding:0px">Latest <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.21.2">version change log</a></li></ul></td>
    </tr>
    </tbody>
    </table> 


## 04 March 2021
{: #04-march-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">NA</li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">NA</li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support <code>sort</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_user_policy#argument-reference">ibm_iam_user_policy</a> and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_user_policy#argument-reference">ibm_iam_service_policy</a> data sources</li><li style="margin:0px; padding:0px">Support <code>default_routing_table</code> attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc#attribute-reference">ibm_is_vpc</a> data source and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc#attribute-reference">ibm_is_vpc</a> resources.</li><li style="margin:0px; padding:0px">Support <code>logging</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference">ibm_is_lb</a></li><li style="margin:0px; padding:0px">Updated <code>boot_volume</code> attributes for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance_template#attribute-reference">ibm_is_instance_template</a> resources</li><li style="margin:0px; padding:0px">Support <code>auto_delete_volume</code>  argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference">vpc generation 2</a></li><li style="margin:0px; padding:0px">Support  <code>resource_group_id</code> argument for force new resource for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis#argument-reference">ibm_cis</a> and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database#argument-reference">ibm_database</a> resources</li><li style="margin:0px; padding:0px">Example update  and support <code>code_path</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database#argument-reference">ibm_function_action</a> resources</li><li style="margin:0px; padding:0px">Latest <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.21.1">version change log</a></li></ul></td>
    </tr>
    </tbody>
    </table> 

## 17 February 2021
{: #17-february-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">NA</li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pi_catalog_images"><code>ibm_pi_catalog_images</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_volume_profile"><code>ibm_is_volume_profile</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_volume_profiles"><code>ibm_is_volume_profiles</code></a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support <code>lunid</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/storage_block#argument-reference">ibm_storage_block</a> resource</li><li style="margin:0px; padding:0px">Support <code>auto_delete_volume</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference">ibm_is_instance</a> resource</li><li style="margin:0px; padding:0px">Support <code>wait_till</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference">ibm_container_cluster</a> resource</li><li style="margin:0px; padding:0px">Support <code>patch_version</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference">ibm_container_cluster</a>, <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_vpc_cluster#argument-reference">ibm_container_vpc_cluster</a> resources, and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_instance#argument-reference">ibm_is_instance data source</a> data source</li><li style="margin:0px; padding:0px">Support <code>auto_delete_volume</code>  argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference">vpc generation 2</a></li><li style="margin:0px; padding:0px">Support <code>session_stickiness</code> attribute to enable <code>HTTP_COOKIE</code> for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/lbaas#attributes-reference">ibm_lbass</a> resource </li><li style="margin:0px; padding:0px">Example update for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/certificate_manager_order">ibm_certificate_manager_order</a>, <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/certificate_manager_import">ibm_certificate_manager_import</a>, <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/service_instance">ibm_resource_instance</a>, and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/service_key">ibm_resource_key</a> resource</li><li style="margin:0px; padding:0px">Latest <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.21.0">version change log</a></li></ul></td>
    </tr>
    </tbody>
    </table> 


## 28 January 2021
{: #28-january-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/service_key"><code>ibm_dl_provider_gateway</code></a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dl_provider_gateways"><code>ibm_dl_provider_gateways</code></a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dl_provider_ports"><code>ibm_dl_provider_ports</code></a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support for <code>pod_subnet</code> and <code>service-subnet</code> arguments for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dl_provider_ports#argument-reference">ibm_container_cluster resource</a></li><li style="margin:0px; padding:0px">Support <code>vpc_name</code> and <code>vpc</code> arguments to filter the instances <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pi_instance#argument-reference">ibm_is_instance data source</a> </li><li style="margin:0px; padding:0px">Support <code>patch_version</code> argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference">ibm_container_cluster resource</a> and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_vpc_cluster#argument-reference">ibm_container_vpc_cluster resource</a></li><li style="margin:0px; padding:0px">Support <code>architecture</code> attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_instance_profile#attribute-reference">vpc instance profile</a> and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_instance_profiles#attribute-reference">vpc_instance_profiles</a> data source</li><li style="margin:0px; padding:0px">Latest version change log for <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.20.1">IBM Cloud provider</a></li></ul></td>
    </tr>
    </tbody>
    </table>


## 13 January 2021
{: #13-january-2021}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_api_key_Reset">ibm_container_api_key_reset</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cr_namespace">ibm_cr_namespace</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_api_key">ibm_iam_service_api_key</a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cr_namespaces">ibm_cr_namespaces</a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support <code>api_key_id</code>, <code>api_key_owner_name</code>, and <code>api_key_owner_email</code> attributes for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#attribute-reference">ibm_container_cluster resource</a></li><li style="margin:0px; padding:0px">Support <code>crn</code> in target attribute for VPC virtual endpoint for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_endpoint_gateway#attribute-reference">ibm_is_virtual_endpoint_gateway</a></li><li style="margin:0px; padding:0px">Updated an example for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_addons#example-usage">ibm_container_addons resource</a></li><li style="margin:0px; padding:0px">Updated next-hop attribute as required for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/app_route#attribute-reference">ibm_is_vpc_route</a></li><li style="margin:0px; padding:0px">Latest version change log for <a href="https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.20.1">IBM Cloud provider</a></li></ul></td>
    </tr>
    </tbody>
    </table>


## 29 December 2020
{: #29-december-2020}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_certificate_order">ibm_cis_certificate_order</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_certificate_upload">ibm_cis_certificate_upload</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_dns_records_import">ibm_cis_dns_records_import</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_dns_record">ibm_cis_dns_record</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_page_rule">ibm_cis_page_rule</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_endpoint_gateway">ibm_is_virtual_endpoint_gateway</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_endpoint_gateway_ip">ibm_is_virtual_endpoint_gateway_ip</a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_certificates">ibm_cis_certificates</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_custom_certificates">ibm_cis_custom_certificates</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_page_rules">ibm_cis_page_rules</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_dns_records">ibm_cis_dns_record</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateways">ibm_is_virtual_endpoint_gateways</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateway_ips">ibm_is_virtual_endpoint_gateway_ips</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateway">ibm_is_virtual_endpoint_gateway</a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Status attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateway#attribute-reference">ibm_container_alb_cert resource</a></li><li style="margin:0px; padding:0px">Persistence and namespace attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_alb_cert#attribute-reference">ibm_container_alb_cert resource</a></li><li style="margin:0px; padding:0px">Labels argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference">ibm_container_cluster resource</a></li></ul></td>
    </tr>
    </tbody>
    </table>

## 14 December 2020
{: #14-december-2020}

<table>
    <thead>
    <th style="width:80px">New resources</th>
    <th style="width:80px">New data sources</th>
    <th style="width:500px">Enhancements</th>
    </thead>
    <tbody>
        <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_routing">ibm_cis_routing</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_cache_settings">ibm_cis_cache_settings</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_custom_page">ibm_cis_custom_page</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb">ibm_dns_glb</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb_monitor">ibm_dns_glb_monitor</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb_pool">ibm_dns_glb_pool</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc_routing_table">ibm_is_vpc_routing_table</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc_routing_table_route">ibm_is_vpc_routing_table_route</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_waf_rule">ibm_cis_waf_rule</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_waf_package">ibm_cis_waf_package</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_waf_group">ibm_cis_waf_group</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_range_app">ibm_cis_range_app</a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_global_load_balancers">ibm_cis_global_load_balancers</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_custom_pages">ibm_cis_custom_pages</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb">ibm_dns_glbs</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dns_glb_monitors">ibm_dns_glb_monitors</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dns_glb_pools">ibm_dns_glb_pools</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_default_routing_table">ibm_is_vpc_default_routing_table</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_routing_tables">ibm_is_vpc_routing_tables</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_routing_table_routes">ibm_is_vpc_routing_table_routes</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_waf_rules">ibm_cis_waf_rules</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_waf_packages">ibm_cis_waf_packages</a><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_waf_groups">ibm_cis_waf_groups</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_range_apps">ibm_cis_range_apps</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpn_gateways">ibm_is_vpn_gateways</a></li><li style="margin:0px; padding:0px"><a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpn_gateway_connections">ibm_is_vpn_gateway_connections</a></li></ul></td>
        <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">public_ip attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_network_port#attribute-reference">power network resource</a></li><li style="margin:0px; padding:0px">Policies attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key#attribute-reference">ibm_kms_key resource</a></li><li style="margin:0px; padding:0px">Number of invited users and invited users attribute for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_invite#attribute-reference">ibm_iam_user_invite</a> resource</li><li style="margin:0px; padding:0px">Support HTTPS protocol for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_pool">ibm_is_lb_pool</a></li><li style="margin:0px; padding:0px">Encrypted data key and encryption key argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_image#argument-reference">image data source</a></li><li style="margin:0px; padding:0px"> Archive rule argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket#argument-reference">COS bucket resource</a></li><li style="margin:0px; padding:0px">Policies for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key">ibm_kms_key</a> and <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_keys">ibm_kms_keys</a> data source</li><li style="margin:0px; padding:0px">List bounded services argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/container_cluster">ibm_container_cluster</a> data source</li><li style="margin:0px; padding:0px">Access rule and UA rule argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_firewall#attribute-reference">internet service firewall resource and datasource</a></li><li style="margin:0px; padding:0px">Allow ip spoofing argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference">ibm_is_instance</a></li><li style="margin:0px; padding:0px">Routing table and ip version argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/subnet#argument-reference">ibm_is_subnet</a></li><li style="margin:0px; padding:0px">Import for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_floating_ip#argument-reference">floating IP resources</a></li><li style="margin:0px; padding:0px">Import for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_ike_policy#argument-reference">Ike policy resources</a></li><li style="margin:0px; padding:0px">Import for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_image#argument-reference">images resources</a></li><li style="margin:0px; padding:0px">Import for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume">volume resources</a><li style="margin:0px; padding:0px">Archive rule,expire rule,force delete for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket">COS bucket</a></li><li style="margin:0px; padding:0px">Support profile argument for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference">is_lb</a></li><li style="margin:0px; padding:0px">Update protocol and connection limit argument for  <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_listener#argument-reference">ibm_is_lb_listener</a></li><li style="margin:0px; padding:0px">Update protocol and connection limit argument for  <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_listener#argument-reference">ibm_is_lb_listener</a></li><li style="margin:0px; padding:0px">Support mode argument and status, created_at, members attributes for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dl_gateway#argument-reference">ibm_dl_gateway</a></li><li style="margin:0px; padding:0px">Update the arguments and attributes for <a href="https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpn_gateway_connection#attribute-reference">ibm_is_vpn_gateway_connection</a></li></ul></td>
    </tr>
    </tbody>
    </table> 



