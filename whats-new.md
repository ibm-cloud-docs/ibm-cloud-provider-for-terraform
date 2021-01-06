---

copyright:
  years: 2019, 2021
lastupdated: "2021-01-06"

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

# What's new in IBM Cloud Provider plug-in for Terraform?
{: #new-in-terraform}

Learn about the latest changes to the IBM Cloud Provider plug-in for Terraform service that are grouped by month.

  
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_certificate_order](/docs/terraform?topic=terraform-cis-resources#cis-certificate-order)</li><li style="margin:0px; padding:0px">[ibm_cis_certificate_upload](/docs/terraform?topic=terraform-cis-resources#cis-certificate-upload)<li style="margin:0px; padding:0px">[ibm_cis_dns_records_import](/docs/terraform?topic=terraform-cis-resources#cis-dns-records-import)<li style="margin:0px; padding:0px">[ibm_cis_dns_record](/docs/terraform?topic=terraform-cis-resources#cis-dns-record)<li style="margin:0px; padding:0px">[ibm_cis_page_rule](/docs/terraform?topic=terraform-cis-resources#cis-page-rule)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway](/docs/terraform?topic=terraform-vpc-gen2-resources#virtual-endpoint-gwy)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway_ip](/docs/terraform?topic=terraform-vpc-gen2-resources#virtual-endpoint-gwyip)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_certificates](/docs/terraform?topic=terraform-cis_data#cis-certificates)</li><li style="margin:0px; padding:0px">[ibm_cis_custom_certificates](/docs/terraform?topic=terraform-cis_data#cis-custom-certificates)</li><li style="margin:0px; padding:0px">[ibm_cis_page_rules](/docs/terraform?topic=terraform-cis_data#cis-page-rules)</li><li style="margin:0px; padding:0px">[ibm_cis_dns_record](/docs/terraform?topic=terraform-cis_data#cis-dns-record
)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateways](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-endpoint-gwysds)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway_ips](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-endpoint-gwy-ipsds)</li><li style="margin:0px; padding:0px">[ibm_is_virtual_endpoint_gateway](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-endpoint-gwyds)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">Status attribute for [ibm_container_alb_cert resource](/docs/terraform?topic=terraform-container-resources#container-alb-cert)</li><li style="margin:0px; padding:0px">Persistence and namespace attribute for [ibm_container_alb_cert resource](/docs/terraform?topic=terraform-container-resources#container-alb-cert)</li><li style="margin:0px; padding:0px">Labels argument for [ibm_container_cluster resource](/docs/terraform?topic=terraform-container-resources#container-cluster)</li></ul></td>
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
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_routing](/docs/terraform?topic=terraform-cis-resources#cis-routing)</li><li style="margin:0px; padding:0px">[ibm_cis_cache_settings](/docs/terraform?topic=terraform-cis-resources#cis-cache)<li style="margin:0px; padding:0px">[ibm_cis_custom_page](/docs/terraform?topic=terraform-cis-resources#cis-custom)<li style="margin:0px; padding:0px">[ibm_dns_glb](/docs/terraform?topic=terraform-dns-resources#dns-glb)<li style="margin:0px; padding:0px">[ibm_dns_glb_monitor](/docs/terraform?topic=terraform-dns-resources#dns-glb-monitor)<li style="margin:0px; padding:0px">[ibm_dns_glb_pool](/docs/terraform?topic=terraform-dns-resources#dns-glb-pool)<li style="margin:0px; padding:0px">[ibm_is_vpc_routing_table](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-routing-table)<li style="margin:0px; padding:0px">[ibm_is_vpc_routing_table_route](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-routing-table-route)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_rule](/docs/terraform?topic=terraform-cis-resources#cis-waf-rule)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_package](/docs/terraform?topic=terraform-cis-resources#cis-waf-package)<li style="margin:0px; padding:0px">[ibm_cis_waf_group](/docs/terraform?topic=terraform-cis-resources#cis-waf-grp)</li><li style="margin:0px; padding:0px">[ibm_cis_range_app](/docs/terraform?topic=terraform-cis-resources#cis_range_app)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[ibm_cis_global_load_balancers](/docs/terraform?topic=terraform-cis_data#cis-global-lb-ds)</li><li style="margin:0px; padding:0px">[ibm_cis_custom_pages](/docs/terraform?topic=terraform-cis-resources#cis-custom)</li><li style="margin:0px; padding:0px">[ibm_dns_glbs](/docs/terraform?topic=terraform-dns-data-sources#dns-glbs-ds)</li><li style="margin:0px; padding:0px">[ibm_dns_glb_monitors](/docs/terraform?topic=terraform-dns-data-sources#dns-glb-monitors-ds)</li><li style="margin:0px; padding:0px">[ibm_dns_glb_pools](/docs/terraform?topic=terraform-dns-data-sources#dns-glb-pools-ds)</li><li style="margin:0px; padding:0px">[ibm_is_vpc_default_routing_table](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-default-routing-tableds)</li><li style="margin:0px; padding:0px">[ibm_is_vpc_routing_tables](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-routing-tableds)</li><li style="margin:0px; padding:0px">[ibm_is_vpc_routing_table_routes](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-routing-tablesds)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_rules](/docs/terraform?topic=terraform-cis_data#cis-waf-rules)</li><li style="margin:0px; padding:0px">[ibm_cis_waf_packages](/docs/terraform?topic=terraform-cis_data#cis-waf-packages)<li style="margin:0px; padding:0px">[ibm_cis_waf_groups](/docs/terraform?topic=terraform-cis_data#cis-waf-groups)</li><li style="margin:0px; padding:0px">[ibm_cis_range_apps](/docs/terraform?topic=terraform-cis_data#cis-range-apps)</li><li style="margin:0px; padding:0px">[ibm_is_vpn_gateways](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-gateways-ds)</li><li style="margin:0px; padding:0px">[ibm_is_vpn_gateway_connections](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-gateways-connection-ds)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">public_ip attribute for [power network resource](/docs/terraform?topic=terraform-power-vsi#power-network)</li><li style="margin:0px; padding:0px">Policies attribute for [ibm_kms_key resource](/docs/terraform?topic=terraform-kms-resources#kms-key)</li><li style="margin:0px; padding:0px">Number of invited users and invited users attribute for [ibm_iam_user_invite resource](/docs/terraform?topic=terraform-iam-resources#iam-user-invite-output)</li><li style="margin:0px; padding:0px">Support HTTPS protocol for [ibm_is_lb_pool](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-pool)</li><li style="margin:0px; padding:0px">Encrypted data key and encryption key argument for [image data source](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-image)</li><li style="margin:0px; padding:0px"> Archive rule argument for [COS bucket resource](/docs/terraform?topic=terraform-object-storage-resources#cos-bucket)</li><li style="margin:0px; padding:0px">Policies for [ibm_kms_key and ibm_kms_keys data source](/docs/terraform?topic=terraform-kms-data-sources)</li><li style="margin:0px; padding:0px">List bounded services argument for [ibm_container_cluster data source](/docs/terraform?topic=terraform-container-data-sources#container-cluster)</li><li style="margin:0px; padding:0px">Access rule and UA rule argument for [internet service firewall resource and datasource](/docs/terraform?topic=terraform-cis_data#cis-firewall-dsoutput)</li><li style="margin:0px; padding:0px">Allow ip spoofing argument for [ibm_is_instance](/docs/terraform?topic=terraform-vpc-gen2-resources#instance-input)</li><li style="margin:0px; padding:0px">Routing table and ip version argument for [ibm_is_subnet](/docs/terraform?topic=terraform-vpc-gen2-resources#subnet-input)</li><li style="margin:0px; padding:0px">Import for [floating IP resources](/docs/terraform?topic=terraform-vpc-gen2-resources#floating-ip-import)</li><li style="margin:0px; padding:0px">Import for [Ike policy resources](/docs/terraform?topic=terraform-vpc-gen2-resources#provider-ike-policy-import)</li><li style="margin:0px; padding:0px">Import for [images resources](/docs/terraform?topic=terraform-vpc-gen2-resources#image-import)</li><li style="margin:0px; padding:0px">Import for [volume resources](/docs/terraform?topic=terraform-vpc-gen2-resources#volume-import)<li style="margin:0px; padding:0px">Archive rule,expire rule,force delete for [COS bucket](/docs/terraform?topic=terraform-object-storage-resources#hpvs-cos-bucket-input)</li><li style="margin:0px; padding:0px">Support profile argument for [is_lb](/docs/terraform?topic=terraform-vpc-gen2-resources#lb)</li><li style="margin:0px; padding:0px">Update protocol and connection limit argument for  [ibm_is_lb_listener](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-listener)</li><li style="margin:0px; padding:0px">Update protocol and connection limit argument for  [ibm_is_lb_listener](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-listener)</li><li style="margin:0px; padding:0px">Support mode argument and status, created_at, members attributes for [ibm_dl_gateway](/docs/terraform?topic=terraform-dl-gateway-resource#dl-gwy-input)</li><li style="margin:0px; padding:0px">Update the arguments and attributes for [ibm_is_vpn_gateway_connection](/docs/terraform?topic=terraform-vpc-gen2-resources#vpn-gateway-connection)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
