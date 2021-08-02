---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-02"

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
    <th style="width:80px">Releases and updates</th>
    </thead>
  <tbody>
    <tr>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">**Enhancements:** {{site.data.keyword.cloud_notm}} Provider now supports Terraform v0.15</li><li style="margin:0px; padding:0px">For the latest `Resources`, `Data sources`, `Enhancements`, and `Bug fixes`, see [Updates and fixes in v1.29.0](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.29.0)</li><li style="margin:0px; padding:0px">For the latest `Resources`, `Data sources`, `Enhancements`, and `Bug fixes`, see [Updates and fixes in v1.28.0](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.28.0)</li><li style="margin:0px; padding:0px">For the latest `Resources`, `Data sources`, `Enhancements`, and `Bug fixes`, see [Updates and fixes in v1.27.2](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.27.2)</li></ul></td>
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
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">For the latest `Resources`, `Data sources`, `Enhancements`, and `Bug fixes`, see [Updates and fixes in v1.26.0](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.26.0)</li></ul></td>
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
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">For the latest `Resources`, `Data sources`, `Enhancements`, and `Bug fixes`, see [Updates and fixes in v1.25.0](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.25.0)</li></ul></td>
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
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support `gateway_connection` attribute [ibm_is_vpn_gateway_connection](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpn_gateway_connection#attribute-reference) resource</li><li style="margin:0px; padding:0px">Support additional attributes for [ibm_is_subnet_reserved_ip](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_subnet_reserved_ip#attribure-reference) resource</li><li style="margin:0px; padding:0px">Added [ibm_iam_account_settings](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_account_settings#example-usage) data source example</li><li style="margin:0px; padding:0px">Support `resource_group_id` argument in [ibm_satellite_location](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/satellite_location#argument-reference) resources and attribute in [ibm_satellite_location](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/satellite_location#attributes-reference) data source</li><li style="margin:0px; padding:0px">Support `ca-tor` region in [ibm_cos_bucket](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket#argument-reference) resource.</li><li style="margin:0px; padding:0px">Support `private_address` attributes for [ibm_is_vpn_gateway](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpn_gateway#attribute-reference) resource and [ibm_is_vpn_gateway](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpn_gateways#attribute-reference) data source</li><li style="margin:0px; padding:0px">Support for `retention policy` argument in [ibm_cos_bucket](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket#argument-reference) bucket and attribute in [`ibm_cos_bucket`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cos_bucket#attribute-reference) bucket</li><li style="margin:0px; padding:0px">Latest [version1.23.2 change log](https://registry.terraform.io/providers/IBM-Cloud/ibm/1.23.2) and [version1.23.1 change log](https://registry.terraform.io/providers/IBM-Cloud/ibm/1.23.1)</li></ul></td>
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_iam_account_settings`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings)</li><li style="margin:0px; padding:0px">[`ibm_cm_catalog`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_catalog)</li><li style="margin:0px; padding:0px">[`ibm_cm_offering`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_offering)</li><li style="margin:0px; padding:0px">[`ibm_cm_offering_instance`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_offering_instance)</li><li style="margin:0px; padding:0px">[`ibm_cm_version`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_version)</li><li style="margin:0px; padding:0px">[`ibm_enterprise`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise)</li><li style="margin:0px; padding:0px">[`ibm_enterprise_account`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise_account)</li><li style="margin:0px; padding:0px">[`ibm_enterprise_account_group`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise_account_group)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_iam_account_settings`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_account_settings)</li><li style="margin:0px; padding:0px">[`ibm_cm_catalog`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_catalog)</li><li style="margin:0px; padding:0px">[`ibm_cm_offering`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_offering)</li><li style="margin:0px; padding:0px">[`ibm_cm_offering_instance`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_offering_instance)</li><li style="margin:0px; padding:0px">[`ibm_cm_version`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cm_version)</li><li style="margin:0px; padding:0px">[`ibm_enterprises`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/enterprises)</li><li style="margin:0px; padding:0px">[`ibm_enterprise_accounts`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/enterprise_accounts)</li><li style="margin:0px; padding:0px">[`ibm_enterprise_account_groups`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/enterprise_account_groups)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Latest [version change log](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.23.0)</li></ul></td>
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"> <li style="margin:0px; padding:0px">[`ibm_is_dedicated_host`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_dedicated_host
)</li><li style="margin:0px; padding:0px">[`ibm_is_dedicated_host_group`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_dedicated_host_group)</li><li style="margin:0px; padding:0px">[`ibm_is_subnet_reserved_ip`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_subnet_reserved_ip)</li><li style="margin:0px; padding:0px">[`ibm_kms_key_alias`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key_alias)</li><li style="margin:0px; padding:0px">[`ibm_kms_key_rings`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key_rings)</li><li style="margin:0px; padding:0px">[`ibm_ob_logging`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/ob_logging)</li><li style="margin:0px; padding:0px">[`ibm_ob_monitoring`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/ob_monitoring)</li><li style="margin:0px; padding:0px">[`ibm_pn_application_chrome`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pn_application_chrome)</li><li style="margin:0px; padding:0px">[`ibm_satellite_host`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/satellite_host)</li><li style="margin:0px; padding:0px">[`ibm_satellite_location`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/satellite_location)</li><li style="margin:0px; padding:0px">[`ibm_schematics_action`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/schematics_action)</li><li style="margin:0px; padding:0px">[`ibm_schematics_job`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/schematics_job)</li><li style="margin:0px; padding:0px">[`ibm_schematics_workspace`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/schematics_workspace)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_cis_cache_settings`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_cache_settings)</li><li style="margin:0px; padding:0px">[`ibm_is_dedicated_host`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host)</li><li style="margin:0px; padding:0px">[`ibm_is_dedicated_hosts`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_hosts)</li><li style="margin:0px; padding:0px">[`ibm_is_dedicated_host_group`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host_group)</li><li style="margin:0px; padding:0px">[`ibm_is_dedicated_host_groups`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host_groups)</li><li style="margin:0px; padding:0px">[`ibm_is_dedicated_host_profile`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_dedicated_host_profile)</li><li style="margin:0px; padding:0px">[`ibm_kms_key_rings`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_keys_rings)</li><li style="margin:0px; padding:0px">[`ibm_pn_application_chrome`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pn_application_chrome)</li><li style="margin:0px; padding:0px">[`ibm_secrets_manager_secret`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/secrets_manager_secret)</li><li style="margin:0px; padding:0px">[`ibm_secrets_manager_secrets`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/secrets_manager_secrets)</li><li style="margin:0px; padding:0px">[`ibm_satellite_location`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/satellite_location)</li><li style="margin:0px; padding:0px">[`ibm_is_subnet_reserved_ip`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet_reserved_ip)</li><li style="margin:0px; padding:0px">[`ibm_is_subnet_reserved_ips`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet_reserved_ips)</li><li style="margin:0px; padding:0px">[`ibm_schematics_action`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/schematics_action)</li><li style="margin:0px; padding:0px">[`ibm_schematics_job`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/schematics_job)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support `dh_group`, `key_lifetime`, and `authentication_algorithm` argument for [ibm_is_ipsec_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_ipsec_policy#argument-reference), [ibm_is_ike_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_ike_policy#argument-reference) resources</li><li style="margin:0px; padding:0px">Support `delegate_vpc` argument for [ibm_is_vpc_routing_table_route](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_routing_table_routes#argument-reference) resources</li><li style="margin:0px; padding:0px">Support `tags` argument for [ibm_is_security_group](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_security_group#argument-reference) resources</li><li style="margin:0px; padding:0px">Support `security-groups` argument for [ibm_is_lb](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference) resources and [ibm_is_lb](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_lb) data sources</li><li style="margin:0px; padding:0px">Support `public_key` argument for [ibm_is_ssh_key](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_ssh_key) data sources</li><li style="margin:0px; padding:0px">Support `default_network_acl_name`, `default_security_group_name`, `default_routing_table_name` argument for [ibm_is_vpc](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc#argument-reference) resources</li><li style="margin:0px; padding:0px">Support `quote_id` argument for [ibm_compute_vm_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/compute_vm_instance#argument-reference) resources</li><li style="margin:0px; padding:0px">Support `serve_stale_content` argument for [ibm_cis_cache_settings](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_cache_settings#argument-reference) resources</li><li style="margin:0px; padding:0px">Support `alias`, `key_ring_id` argument for [ibm_kms_key](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key#argument-reference) resources and `aliases` attribute for [ibm_kms_key](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_key#attribute-reference) and [ibm_kms_keys](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_keys#attribute-reference)</li>  <li style="margin:0px; padding:0px">Support `visibility` argument for [{{site.data.keyword.terraform-provider_full_notm}}](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs#argument-reference) and deprecated `generation` argument for [{{site.data.keyword.terraform-provider_full_notm}}](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs#argument-reference)</li><li style="margin:0px; padding:0px">Updated `kind = "nodejs:10"`, in example for [ibm_function_action](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/function_action) resources and [ibm_function_rule](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/function_rule)</li><li style="margin:0px; padding:0px">Latest [version change log](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.22.0)</li></ul></td>
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
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support `logging` argument description for [ibm_is_lb](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference)</li><li style="margin:0px; padding:0px">Support `accept_proxy_protocol` argument for [ibm_is_lb_listener](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_listener#argument-reference)</li><li style="margin:0px; padding:0px">Added resources timeouts and depreciated wait_time_minutes argument for [ibm_compute_vm_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/compute_vm_instance#argument-reference)</li><li style="margin:0px; padding:0px">Support `tags` argument for [ibm_is_subnet](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet#argument-reference), [ibm_is_network_acl](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_network_acl#argument-reference)resource and [ibm_is_subnet](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_subnet#argument-reference) data source</li><li style="margin:0px; padding:0px">Support `iam_id` argument for [iam_service_id](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_id#argument-reference) resource</li><li style="margin:0px; padding:0px">Added `checksum` attribute for [ibm_is_image](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_image#attribute-reference), [ibm_is_images](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_images#attribute-reference) data sources and for [ibm_is_image](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_image) resource</li><li style="margin:0px; padding:0px">Latest [version change log](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.21.2)</li></ul></td>
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
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support `sort` argument for [ibm_iam_user_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_user_policy#argument-reference) and [ibm_iam_service_policy](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/iam_user_policy#argument-reference) data sources</li><li style="margin:0px; padding:0px">Support `default_routing_table` attribute for [ibm_is_vpc](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc#attribute-reference) data source and [ibm_is_vpc](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc#attribute-reference) resources.</li><li style="margin:0px; padding:0px">Support `logging` argument for [ibm_is_lb](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference)</li><li style="margin:0px; padding:0px">Updated `boot_volume` attributes for [ibm_is_instance_template](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance_template#attribute-reference) resources</li><li style="margin:0px; padding:0px">Support `auto_delete_volume`  argument for [vpc generation 2](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference)</li><li style="margin:0px; padding:0px">Support  `resource_group_id` argument for force new resource for [ibm_cis](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis#argument-reference) and [ibm_database](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database#argument-reference) resources</li><li style="margin:0px; padding:0px">Example update  and support `code_path` argument for [ibm_function_action](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database#argument-reference) resources</li><li style="margin:0px; padding:0px">Latest [version change log](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.21.1)</li></ul></td>
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
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_pi_catalog_images`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pi_catalog_images)</li><li style="margin:0px; padding:0px">[`ibm_is_volume_profile`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_volume_profile)</li><li style="margin:0px; padding:0px">[`ibm_is_volume_profiles`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_volume_profiles)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support `lunid` argument for [ibm_storage_block](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/storage_block#argument-reference) resource</li><li style="margin:0px; padding:0px">Support `auto_delete_volume` argument for [ibm_is_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference) resource</li><li style="margin:0px; padding:0px">Support `wait_till` argument for [ibm_container_cluster](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference) resource</li><li style="margin:0px; padding:0px">Support `patch_version` argument for [ibm_container_cluster](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference), [ibm_container_vpc_cluster](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_vpc_cluster#argument-reference) resources, and [ibm_is_instance data source](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_instance#argument-reference) data source</li><li style="margin:0px; padding:0px">Support `auto_delete_volume`  argument for [vpc generation 2](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference)</li><li style="margin:0px; padding:0px">Support `session_stickiness` attribute to enable `HTTP_COOKIE` for [ibm_lbass](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/lbaas#attributes-reference) resource </li><li style="margin:0px; padding:0px">Example update for [ibm_certificate_manager_order](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/certificate_manager_order), [ibm_certificate_manager_import](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/certificate_manager_import), [ibm_resource_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/service_instance), and [ibm_resource_key](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/service_key) resource</li><li style="margin:0px; padding:0px">Latest [version change log](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.21.0)</li></ul></td>
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_dl_provider_gateway`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/service_key)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_dl_provider_gateways`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dl_provider_gateways)</li><li style="margin:0px; padding:0px">[`ibm_dl_provider_ports`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dl_provider_ports)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support for `pod_subnet` and `service-subnet` arguments for [ibm_container_cluster resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dl_provider_ports#argument-reference)</li><li style="margin:0px; padding:0px">Support `vpc_name` and `vpc` arguments to filter the instances [ibm_is_instance data source](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pi_instance#argument-reference) </li><li style="margin:0px; padding:0px">Support `patch_version` argument for [ibm_container_cluster resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference) and [ibm_container_vpc_cluster resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_vpc_cluster#argument-reference)</li><li style="margin:0px; padding:0px">Support `architecture` attribute for [vpc instance profile](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_instance_profile#attribute-reference) and [vpc_instance_profiles](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_instance_profiles#attribute-reference) data source</li><li style="margin:0px; padding:0px">Latest version change log for [IBM Cloud provider](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.20.1)</li></ul></td>
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_container_api_key_reset](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_api_key_Reset)</li><li style="margin:0px; padding:0px">[ibm_cr_namespace](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cr_namespace)</li><li style="margin:0px; padding:0px">[ibm_iam_service_api_key](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_api_key)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cr_namespaces](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cr_namespaces)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Support `api_key_id`, `api_key_owner_name`, and `api_key_owner_email` attributes for [ibm_container_cluster resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#attribute-reference)</li><li style="margin:0px; padding:0px">Support `crn` in target attribute for VPC virtual endpoint for [ibm_is_virtual_endpoint_gateway](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_endpoint_gateway#attribute-reference)</li><li style="margin:0px; padding:0px">Updated an example for [ibm_container_addons resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_addons#example-usage)</li><li style="margin:0px; padding:0px">Updated next-hop attribute as required for [ibm_is_vpc_route](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/app_route#attribute-reference)</li><li style="margin:0px; padding:0px">Latest version change log for [IBM Cloud provider](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.20.1)</li></ul></td>
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_certificate_order](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_certificate_order)</li><li style="margin:0px; padding:0px">[ibm_cis_certificate_upload](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_certificate_upload)</li><li style="margin:0px; padding:0px">[ibm_cis_dns_records_import](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_dns_records_import)</li><li style="margin:0px; padding:0px">[ibm_cis_dns_record](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_dns_record)</li><li style="margin:0px; padding:0px">[ibm_cis_page_rule](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_page_rule)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_endpoint_gateway)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway_ip](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_endpoint_gateway_ip)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_certificates](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_certificates)</li><li style="margin:0px; padding:0px">[ibm_cis_custom_certificates](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_custom_certificates)</li><li style="margin:0px; padding:0px">[ibm_cis_page_rules](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_page_rules)</li><li style="margin:0px; padding:0px">[ibm_cis_dns_record](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_dns_records)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateways](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateways)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway_ips](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateway_ips)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateway)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Status attribute for [ibm_container_alb_cert resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_virtual_endpoint_gateway#attribute-reference)</li><li style="margin:0px; padding:0px">Persistence and namespace attribute for [ibm_container_alb_cert resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_alb_cert#attribute-reference)</li><li style="margin:0px; padding:0px">Labels argument for [ibm_container_cluster resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/container_cluster#argument-reference)</li></ul></td>
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_routing](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_routing)</li><li style="margin:0px; padding:0px">[ibm_cis_cache_settings](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_cache_settings)<li style="margin:0px; padding:0px">[ibm_cis_custom_page](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_custom_page)<li style="margin:0px; padding:0px">[ibm_dns_glb](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb)<li style="margin:0px; padding:0px">[ibm_dns_glb_monitor](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb_monitor)<li style="margin:0px; padding:0px">[ibm_dns_glb_pool](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb_pool)<li style="margin:0px; padding:0px">[ibm_is_vpc_routing_table](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc_routing_table)<li style="margin:0px; padding:0px">[ibm_is_vpc_routing_table_route](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpc_routing_table_route)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_rule](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_waf_rule)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_package](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_waf_package)<li style="margin:0px; padding:0px">[ibm_cis_waf_group](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_waf_group)</li><li style="margin:0px; padding:0px">[ibm_cis_range_app](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_range_app)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_global_load_balancers](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_global_load_balancers)</li><li style="margin:0px; padding:0px">[ibm_cis_custom_pages](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_custom_pages)</li><li style="margin:0px; padding:0px">[ibm_dns_glbs](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dns_glb)</li><li style="margin:0px; padding:0px">[ibm_dns_glb_monitors](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dns_glb_monitors)</li><li style="margin:0px; padding:0px">[ibm_dns_glb_pools](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/dns_glb_pools)</li><li style="margin:0px; padding:0px">[ibm_is_vpc_default_routing_table](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_default_routing_table)</li><li style="margin:0px; padding:0px">[ibm_is_vpc_routing_tables](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_routing_tables)</li><li style="margin:0px; padding:0px">[ibm_is_vpc_routing_table_routes](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpc_routing_table_routes)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_rules](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_waf_rules)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_packages](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_waf_packages)<li style="margin:0px; padding:0px">[ibm_cis_waf_groups](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_waf_groups)</li><li style="margin:0px; padding:0px">[ibm_cis_range_apps](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_range_apps)</li><li style="margin:0px; padding:0px">[ibm_is_vpn_gateways](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpn_gateways)</li><li style="margin:0px; padding:0px">[ibm_is_vpn_gateway_connections](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_vpn_gateway_connections)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">public_ip attribute for [power network resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_network_port#attribute-reference)</li><li style="margin:0px; padding:0px">Policies attribute for [ibm_kms_key resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key#attribute-reference)</li><li style="margin:0px; padding:0px">Number of invited users and invited users attribute for [ibm_iam_user_invite](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_invite#attribute-reference) resource</li><li style="margin:0px; padding:0px">Support HTTPS protocol for [ibm_is_lb_pool](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_pool)</li><li style="margin:0px; padding:0px">Encrypted data key and encryption key argument for [image data source](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/is_image#argument-reference)</li><li style="margin:0px; padding:0px"> Archive rule argument for [COS bucket resource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket#argument-reference)</li><li style="margin:0px; padding:0px">Policies for [ibm_kms_key](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key) and [ibm_kms_keys](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/kms_keys) data source</li><li style="margin:0px; padding:0px">List bounded services argument for [ibm_container_cluster](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/container_cluster) data source</li><li style="margin:0px; padding:0px">Access rule and UA rule argument for [internet service firewall resource and datasource](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_firewall#attribute-reference)</li><li style="margin:0px; padding:0px">Allow ip spoofing argument for [ibm_is_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance#argument-reference)</li><li style="margin:0px; padding:0px">Routing table and ip version argument for [ibm_is_subnet](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/subnet#argument-reference)</li><li style="margin:0px; padding:0px">Import for [floating IP resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_floating_ip#argument-reference)</li><li style="margin:0px; padding:0px">Import for [Ike policy resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_ike_policy#argument-reference)</li><li style="margin:0px; padding:0px">Import for [images resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_image#argument-reference)</li><li style="margin:0px; padding:0px">Import for [volume resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume)<li style="margin:0px; padding:0px">Archive rule,expire rule,force delete for [COS bucket](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cos_bucket)</li><li style="margin:0px; padding:0px">Support profile argument for [is_lb](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb#argument-reference)</li><li style="margin:0px; padding:0px">Update protocol and connection limit argument for  [ibm_is_lb_listener](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_listener#argument-reference)</li><li style="margin:0px; padding:0px">Update protocol and connection limit argument for  [ibm_is_lb_listener](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_lb_listener#argument-reference)</li><li style="margin:0px; padding:0px">Support mode argument and status, created_at, members attributes for [ibm_dl_gateway](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/dl_gateway#argument-reference)</li><li style="margin:0px; padding:0px">Update the arguments and attributes for [ibm_is_vpn_gateway_connection](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_vpn_gateway_connection#attribute-reference)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
