---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-12"

keywords: terraform provider plugin, terraform functions, terraform openwhisk, terraform function action, terraform serverless

subcollection: ibm-cloud-provider-for-terraform

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


# Index of IBM Cloud Provider plug-in for Terraform resources and data sources 

## API Gateway
{: #ibm-api-gateway}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
  </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_api_gateway_endpoint`](/docs/terraform?topic=terraform-api-gateway-resources#api-gw-endpoint)</li><li style="margin:0px; padding:0px">[`ibm_api_gateway_endpoint_subscription`](/docs/terraform?topic=terraform-api-gateway-resources#api-gw-endpoint-subscript)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_api_gateway`](/docs/terraform?topic=terraform-api-gw-data-sources#api-gw)</li></ul></td>
    </tr>
  </tbody>
  </table>

## Certificate Manager
{: #ibm-certificate-manager}
  
  <table>
    <thead>
     <th style="width:180px">Resources</th>
     <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
   <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_certificate_manager_import`](/docs/terraform?topic=terraform-cert-manager-resources#cert-manager)</li><li style="margin:0px; padding:0px">[`ibm_certificate_manager_order`](/docs/terraform?topic=terraform-cert-manager-resources#certmanager-order)</li></ul></td>
     <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_certificate_manager_certificates`](/docs/terraform?topic=terraform-cert-manager-data-sources#cert-manager-certificates)</li></ul></td>
    </tr>
  </tbody>
  </table>

## Classic infrastructure
{: #ibm-classic-infrastructure}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
  </thead>
  <tbody>
<tr>
<td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_cdn`](/docs/terraform?topic=terraform-infrastructure-resources#cdn)</li><li style="margin:0px; padding:0px">[`ibm_compute_autoscale_group`](/docs/terraform?topic=terraform-infrastructure-resources#autoscale-group)</li><li style="margin:0px; padding:0px">[`ibm_compute_autoscale_policy`](/docs/terraform?topic=terraform-infrastructure-resources#autoscale-policy)</li><li style="margin:0px; padding:0px">[`ibm_compute_bare_metal`](/docs/terraform?topic=terraform-infrastructure-resources#bm)</li><li style="margin:0px; padding:0px">[`ibm_compute_dedicated_host`](/docs/terraform?topic=terraform-infrastructure-resources#dedicated-host)</li><li style="margin:0px; padding:0px">[`ibm_compute_monitor`](/docs/terraform?topic=terraform-infrastructure-resources#compute-monitor)</li><li style="margin:0px; padding:0px">[`ibm_compute_placement_group`](/docs/terraform?topic=terraform-infrastructure-resources#plmt-group)</li><li style="margin:0px; padding:0px">[`ibm_compute_provisioning_hook`](/docs/terraform?topic=terraform-infrastructure-resources#provision-hook)</li><li style="margin:0px; padding:0px">[`ibm_compute_ssh_key`](/docs/terraform?topic=terraform-infrastructure-resources#ssh-key)</li><li style="margin:0px; padding:0px">[`ibm_compute_ssl_certificate`](/docs/terraform?topic=terraform-infrastructure-resources#ssl-compute-cert)</li><li style="margin:0px; padding:0px">[`ibm_compute_user`](/docs/terraform?topic=terraform-infrastructure-resources#compute-user)</li><li style="margin:0px; padding:0px">[`ibm_compute_vm_instance`](/docs/terraform?topic=terraform-infrastructure-resources#vm)</li><li style="margin:0px; padding:0px">[`ibm_dns_domain`](/docs/terraform?topic=terraform-infrastructure-resources#dns-domain)</li><li style="margin:0px; padding:0px">[`ibm_dns_domain_registration_nameservers`](/docs/terraform?topic=terraform-infrastructure-resources#dns-register)</li><li style="margin:0px; padding:0px">[`ibm_dns_secondary`](/docs/terraform?topic=terraform-infrastructure-resources#dns-second)</li><li style="margin:0px; padding:0px">[`ibm_dns_reverse_record`](/docs/terraform?topic=terraform-infrastructure-resources#dns-rev-rec)</li> <li style="margin:0px; padding:0px">[`ibm_dns_record`](/docs/terraform?topic=terraform-infrastructure-resources#dns-record)</li><li style="margin:0px; padding:0px">[`ibm_firewall`](/docs/terraform?topic=terraform-infrastructure-resources#firewall)</li><li style="margin:0px; padding:0px">[`ibm_multivlan_firewall`](/docs/terraform?topic=terraform-infrastructure-resources#multivlan-firewall)</li><li style="margin:0px; padding:0px">[`ibm_firewall_policy`](/docs/terraform?topic=terraform-infrastructure-resources#firewall-policy)</li><li style="margin:0px; padding:0px">[`ibm_hardware_firewall_shared`](/docs/terraform?topic=terraform-infrastructure-resources#shared-fw)</li><li style="margin:0px; padding:0px">[`ibm_ipsec_vpn`](/docs/terraform?topic=terraform-infrastructure-resources#ipsec-vpn)</li><li style="margin:0px; padding:0px">[`ibm_lb`](/docs/terraform?topic=terraform-infrastructure-resources#lb)</li><li style="margin:0px; padding:0px">[`ibm_lbaas`](/docs/terraform?topic=terraform-infrastructure-resources#lbaas)</li><li style="margin:0px; padding:0px">[`ibm_lbaas_health_monitor`](/docs/terraform?topic=terraform-infrastructure-resources#health-monitor)</li><li style="margin:0px; padding:0px">[`ibm_lbaas_server_instance_attachment`](/docs/terraform?topic=terraform-infrastructure-resources#instance-attachment)</li><li style="margin:0px; padding:0px">[`ibm_lb_service`](/docs/terraform?topic=terraform-infrastructure-resources#lb-service)</li><li style="margin:0px; padding:0px">[`ibm_lb_service_group`](/docs/terraform?topic=terraform-infrastructure-resources#service-group)</li><li style="margin:0px; padding:0px">[`ibm_lb_vpx`](/docs/terraform?topic=terraform-infrastructure-resources#lb-vpx)</li><li style="margin:0px; padding:0px">[`ibm_lb_vpx_ha`](/docs/terraform?topic=terraform-infrastructure-resources#lb-vpx-ha)</li><li style="margin:0px; padding:0px">[`ibm_lb_vpx_service`](/docs/terraform?topic=terraform-infrastructure-resources#vpx-svc)</li><li style="margin:0px; padding:0px">[`ibm_lb_vpx_vip`](/docs/terraform?topic=terraform-infrastructure-resources#lb-vpx-vip)</li><li style="margin:0px; padding:0px">[`ibm_network_gateway`](/docs/terraform?topic=terraform-infrastructure-resources#network-gateway)</li><li style="margin:0px; padding:0px">[`ibm_network_gateway_vlan_association`](/docs/terraform?topic=terraform-infrastructure-resources#network-vlan-associate)</li><li style="margin:0px; padding:0px">[`ibm_network_interface_sg_attachment`](/docs/terraform?topic=terraform-infrastructure-resources#network-sg-attachment)</li><li style="margin:0px; padding:0px">[`ibm_network_public_ip`](/docs/terraform?topic=terraform-infrastructure-resources#public-ip)</li><li style="margin:0px; padding:0px">[`ibm_network_vlan`](/docs/terraform?topic=terraform-infrastructure-resources#vlan)</li><li style="margin:0px; padding:0px">[`ibm_network_vlan_spanning`](/docs/terraform?topic=terraform-infrastructure-resources#vlan-spanning)</li><li style="margin:0px; padding:0px">[`ibm_object_storage_account`](/docs/terraform?topic=terraform-infrastructure-resources#os-account)</li><li style="margin:0px; padding:0px">[`ibm_security_group`](/docs/terraform?topic=terraform-infrastructure-resources#sec-group)</li><li style="margin:0px; padding:0px">[`ibm_security_group_rule`](/docs/terraform?topic=terraform-infrastructure-resources#sec-group-rule)</li><li style="margin:0px; padding:0px">[`ibm_storage_block`](/docs/terraform?topic=terraform-infrastructure-resources#storage-block)</li><li style="margin:0px; padding:0px">[`ibm_storage_evault`](/docs/terraform?topic=terraform-infrastructure-resources#storage-evault)</li><li style="margin:0px; padding:0px">[`ibm_storage_file`](/docs/terraform?topic=terraform-infrastructure-resources#storage-file)</li><li style="margin:0px; padding:0px">[`ibm_subnet`](/docs/terraform?topic=terraform-infrastructure-resources#subnet)</li><li style="margin:0px; padding:0px">[`ibm_ssl_certificate`](/docs/terraform?topic=terraform-infrastructure-resources#ssl-cert)</li></ul></td>
<td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_compute_bare_metal`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-bare-metal)</li><li style="margin:0px; padding:0px">[`ibm_compute_image_template`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-image)</li><li style="margin:0px; padding:0px">[`ibm_compute_placement_group`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-placement-group)</li><li style="margin:0px; padding:0px">[`ibm_compute_ssh_key`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-ssh-key)</li><li style="margin:0px; padding:0px">[`ibm_compute_vm_instance`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-vm)</li><li style="margin:0px; padding:0px">[`ibm_dns_domain`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-domain)</li><li style="margin:0px; padding:0px">[`ibm_dns_secondary`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-dns-secondary)</li><li style="margin:0px; padding:0px">[`ibm_lbaas`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-lbaas)</li><li style="margin:0px; padding:0px">[`ibm_network_vlan`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-vlan)</li><li style="margin:0px; padding:0px">[`ibm_security_group`](/docs/terraform?topic=terraform-infrastructure-data-sources#classic-security-group)</li></ul></td>
</tr>
  </tbody>
  </table>
 
  ## Cloud Databases
{: #ibm-Cloud-Databases}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
  </thead>
  <tbody>
  <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_database`](/docs/terraform?topic=terraform-databases-resources#db)</li></ul></td>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_database`](/docs/terraform?topic=terraform-databases-data-sources#database)</li></ul></td>
    </tr>
  </tbody>
  </table>
  
## Cloud Foundry
{: #ibm-Cloud-Foundry}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
  <tr>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_app`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-app)</li><li style="margin:0px; padding:0px">[`ibm_app_domain_private`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-private-domain)</li><li style="margin:0px; padding:0px">[`ibm_app_domain_shared`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-shared-domain)</li><li style="margin:0px; padding:0px">[`ibm_app_route`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-route)</li><li style="margin:0px; padding:0px">[`ibm_org`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-org)</li><li style="margin:0px; padding:0px">[`ibm_service_instance`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-service)</li><li style="margin:0px; padding:0px">[`ibm_service_key`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-service-key)</li><li style="margin:0px; padding:0px">[`ibm_space`](/docs/terraform?topic=terraform-cloud-foundry-resources#cf-space)</li></ul></td>
    <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_account`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-account)</li><li style="margin:0px; padding:0px">[`ibm_app`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-app)</li><li style="margin:0px; padding:0px">[`ibm_app_domain_private`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-private-domain)</li><li style="margin:0px; padding:0px">[`ibm_app_domain_shared`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-shared-domain)</li><li style="margin:0px; padding:0px">[`ibm_app_route`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-app-route)</li><li style="margin:0px; padding:0px">[`ibm_org`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-org)</li><li style="margin:0px; padding:0px">[`ibm_org_quota`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-org-quota)</li><li style="margin:0px; padding:0px">[`ibm_service_instance`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-service-instance)</li><li style="margin:0px; padding:0px">[`ibm_service_key`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-service-key)</li><li style="margin:0px; padding:0px">[`ibm_service_plan`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-service-plan)</li><li style="margin:0px; padding:0px">[`ibm_space`](/docs/terraform?topic=terraform-cloud-foundry-data-sources#cf-space)</li></ul></td>
    </tr>
  </tbody>
  </table>
  
  ## Direct Link Gateway
  {: #ibm-directlink-gateway}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_dl_gateway`](/docs/terraform?topic=terraform-dl-gateway-resource#dl-gwy)</li><li style="margin:0px; padding:0px">[`ibm_dl_virtual_connection`](/docs/terraform?topic=terraform-dl-gateway-resource#dl-vc)</li></li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_dl_gateway`](/docs/terraform?topic=terraform-dl-gateway-ds#dl_gateway_ds)</li><li style="margin:0px; padding:0px">[`ibm_dl_gateways`](/docs/terraform?topic=terraform-dl-gateway-ds#dl_gateways_ds)</li><li style="margin:0px; padding:0px">[`ibm_dl_locations`](/docs/terraform?topic=terraform-dl-gateway-ds#dl_loc_ds)</li><li style="margin:0px; padding:0px">[`ibm_dl_offering_speeds`](/docs/terraform?topic=terraform-dl-gateway-ds#dl_offering_spd_ds)</li><li style="margin:0px; padding:0px">[`ibm_dl_port`](/docs/terraform?topic=terraform-dl-gateway-ds#dl_port_ds)</li><li style="margin:0px; padding:0px">[`ibm_dl_ports`](/docs/terraform?topic=terraform-dl-gateway-ds#dl_ports_ds)</li><li style="margin:0px; padding:0px">[`ibm_dl_routers`](/docs/terraform?topic=terraform-dl-gateway-ds#dl_routers_ds)</li></ul></td>
    </tr>
  </tbody>
  </table>
  
  
  ## DNS Services
  {: #ibm-dns-service}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_dns_glb`](/docs/terraform?topic=terraform-dns-resources#dns-glb)</li><li style="margin:0px; padding:0px">[`ibm_dns_glb_monitor`](/docs/terraform?topic=terraform-dns-resources#dns-glb-monitor)</li><li style="margin:0px; padding:0px">[`ibm_dns_glb_pool`](/docs/terraform?topic=terraform-dns-resources#dns-glb-pool)</li><li style="margin:0px; padding:0px">[`ibm_dns_permitted_network`](/docs/terraform?topic=terraform-dns-resources#dns-permitted-network)</li><li style="margin:0px; padding:0px">[`ibm_dns_resource_record`](/docs/terraform?topic=terraform-dns-resources#dns-record)</li><li style="margin:0px; padding:0px">[`ibm_dns_zone`](/docs/terraform?topic=terraform-dns-resources#dns-zone)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_dns_glbs`](/docs/terraform?topic=terraform-dns-data-sources#dns-glbs-ds)</li><li style="margin:0px; padding:0px">[`ibm_dns_glb_monitors`](/docs/terraform?topic=terraform-dns-data-sources#dns-glb-monitors-ds)</li><li style="margin:0px; padding:0px">[`ibm_dns_glb_pools`](/docs/terraform?topic=terraform-dns-data-sources#dns-glb-pools-ds)</li><li style="margin:0px; padding:0px">[`ibm_dns_permitted_networks`](/docs/terraform?topic=terraform-dns-data-sources#dns-permitted-network)</li><li style="margin:0px; padding:0px">[`ibm_dns_resource_records`](/docs/terraform?topic=terraform-dns-data-sources#dns-record)</li><li style="margin:0px; padding:0px">[`ibm_dns_zones`](/docs/terraform?topic=terraform-dns-data-sources#dns-zones)</li></ul></td>
    </tr>
  </tbody>
  </table>
  
  ## Event Streams
  {: #ibm-event-streams}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_resource_instance`](/docs/terraform?topic=terraform-event-streams-resources#event-stream-sample)</li><li style="margin:0px; padding:0px">[`ibm_event_streams_topic`](/docs/terraform?topic=terraform-event-streams-resources#event-stream-sample2)</li><li style="margin:0px; padding:0px">[`kafka_consumer_app`](/docs/terraform?topic=terraform-event-streams-resources#event-stream-sample3)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_event_streams_topic`](/docs/terraform?topic=terraform-event-streams-ds#event-streams-topic)</li></ul></td>
    </tr>
  </tbody>
  </table>
  
  ## Functions
  {: #ibm-Functions}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_function_action`](/docs/terraform?topic=terraform-function-resources#fn-action)</li><li style="margin:0px; padding:0px">[`ibm_function_namespace`](/docs/terraform?topic=terraform-function-resources#fn-namespace)</li><li style="margin:0px; padding:0px">[`ibm_function_package`](/docs/terraform?topic=terraform-function-resources#fn-package)</li><li style="margin:0px; padding:0px">[`ibm_function_rule`](/docs/terraform?topic=terraform-function-resources#fn-rule)</li><li style="margin:0px; padding:0px">[`ibm_function_trigger`](/docs/terraform?topic=terraform-function-resources#fn-trigger)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_function_action`](/docs/terraform?topic=terraform-function-data-sources#fn-action)</li><li style="margin:0px; padding:0px">[`ibm_function_namespace`](/docs/terraform?topic=terraform-function-data-sources#fn-namespace_ds)</li><li style="margin:0px; padding:0px">[`ibm_function_package`](/docs/terraform?topic=terraform-function-data-sources#fn-package)</li><li style="margin:0px; padding:0px">[`ibm_function_rule`](/docs/terraform?topic=terraform-function-data-sources#fn-rule)</li><li style="margin:0px; padding:0px">[`ibm_function_trigger`](/docs/terraform?topic=terraform-function-data-sources#fn-trigger)</li></ul></td>
    </tr>
  </tbody>
  </table>
  
 ## Identity & Access (IAM)
  {: #ibm-iam-resource}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
  </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_iam_access_group`](/docs/terraform?topic=terraform-iam-resources#iam-access-group)</li><li style="margin:0px; padding:0px">[`ibm_iam_access_group_members`](/docs/terraform?topic=terraform-iam-resources#iam-access-group-members)</li><li style="margin:0px; padding:0px">[`ibm_iam_access_group_policy`](/docs/terraform?topic=terraform-iam-resources#iam-access-group-policy)</li><li style="margin:0px; padding:0px">[`ibm_iam_access_group_dynamic_rule`](/docs/terraform?topic=terraform-iam-resources#iam-group-dynamic-rule)</li><li style="margin:0px; padding:0px">[`ibm_iam_authorization_policy`](/docs/terraform?topic=terraform-iam-resources#iam-auth-policy)</li><li style="margin:0px; padding:0px">[`ibm_iam_authorization_policy_detach`](/docs/terraform?topic=terraform-iam-resources#iam-auth-policy-detach)</li><li style="margin:0px; padding:0px">[`ibm_iam_custom_role`](/docs/terraform?topic=terraform-iam-resources#iam-custom-role)</li>
<li style="margin:0px; padding:0px">[`ibm_iam_service-api-key`](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-iam-resources#iam-service-api-key)</li><li style="margin:0px; padding:0px">[`ibm_iam_service_id`](/docs/terraform?topic=terraform-iam-resources#iam-service-id)</li><li style="margin:0px; padding:0px">[`ibm_iam_service_policy`](/docs/terraform?topic=terraform-iam-resources#iam-service-policy)</li><li style="margin:0px; padding:0px">[`ibm_iam_user_policy`](/docs/terraform?topic=terraform-iam-resources#iam-user-policy)</li><li style="margin:0px; padding:0px">[`ibm_iam_user_settings`](/docs/terraform?topic=terraform-iam-resources#iam-user-settings)</li><li style="margin:0px; padding:0px">[`ibm_iam_user_invite`](/docs/terraform?topic=terraform-iam-resources#iam-user-invite)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_iam_access_group`](/docs/terraform?topic=terraform-iam-data-sources#access_group)</li><li style="margin:0px; padding:0px">[`ibm_iam_auth_token`](/docs/terraform?topic=terraform-iam-data-sources#iam-token)</li><li style="margin:0px; padding:0px">[`ibm_iam_role_actions`](/docs/terraform?topic=terraform-iam-data-sources#iam-role-actions)</li><li style="margin:0px; padding:0px">[`ibm_iam_roles`](/docs/terraform?topic=terraform-iam-data-sources#iam-roles)</li><li style="margin:0px; padding:0px">[`ibm_iam_service_id`](/docs/terraform?topic=terraform-iam-data-sources#iam-service)</li><li style="margin:0px; padding:0px">[`ibm_iam_service_policy`](/docs/terraform?topic=terraform-iam-data-sources#iam-service-policy)</li><li style="margin:0px; padding:0px">[`ibm_iam_user_policy`](/docs/terraform?topic=terraform-iam-data-sources#iam-user-policy)</li><li style="margin:0px; padding:0px">[`ibm_iam_user_profile`](/docs/terraform?topic=terraform-iam-data-sources#iam-user-profile)</li><li style="margin:0px; padding:0px">[`ibm_iam_users`](/docs/terraform?topic=terraform-iam-data-sources#iam-users)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
  ## Internet services
  {: #ibm-internet-services}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_cis`](/docs/terraform?topic=terraform-cis-resources#cis)</li><li style="margin:0px; padding:0px">[`ibm_cis_cache_settings`](/docs/terraform?topic=terraform-cis-resources#cis-cache)</li><li style="margin:0px; padding:0px">[`ibm_cis_certificate_order`](/docs/terraform?topic=terraform-cis-resources#cis-certificate-order)</li><li style="margin:0px; padding:0px">[`ibm_cis_certificate_upload`](/docs/terraform?topic=terraform-cis-resources#cis-certificate-upload)</li><li style="margin:0px; padding:0px">[`ibm_cis_custom_page`](/docs/terraform?topic=terraform-cis-resources#cis-custom)</li><li style="margin:0px; padding:0px">[`ibm_cis_domain`](/docs/terraform?topic=terraform-cis-resources#cis-domain)</li><li style="margin:0px; padding:0px">[`ibm_cis_domain_settings`](/docs/terraform?topic=terraform-cis-resources#cis-domain-settings)</li><li style="margin:0px; padding:0px">[`ibm_cis_dns_record`](/docs/terraform?topic=terraform-cis-resources#cis-dns-record)</li><li style="margin:0px; padding:0px">[`ibm_cis_dns_records_import`](/docs/terraform?topic=terraform-cis-resources#cis-dns-records-import)</li><li style="margin:0px; padding:0px">[`ibm_cis_edge_functions_action`](/docs/terraform?topic=terraform-cis-resources#cis-edge-functions-action)</li><li style="margin:0px; padding:0px">[`ibm_cis_edge_functions_trigger`](/docs/terraform?topic=terraform-cis-resources#cis-edge-functions-trigger)</li><li style="margin:0px; padding:0px">[`ibm_cis_firewall`](/docs/terraform?topic=terraform-cis-resources#cis-firewall)</li><li style="margin:0px; padding:0px">[`ibm_cis_global_load_balancer`](/docs/terraform?topic=terraform-cis-resources#cis-global-lb)</li><li style="margin:0px; padding:0px">[`ibm_cis_healthcheck`](/docs/terraform?topic=terraform-cis-resources#cis-health)</li><li style="margin:0px; padding:0px">[`ibm_cis_origin_pool`](/docs/terraform?topic=terraform-cis-resources#cis-origin-pool)</li><li style="margin:0px; padding:0px">[`ibm_cis_page_rule`](/docs/terraform?topic=terraform-cis-resources#cis-page-rule
)</li><li style="margin:0px; padding:0px">[`ibm_cis_rate_limit`](/docs/terraform?topic=terraform-cis-resources#rate-limit)</li><li style="margin:0px; padding:0px">[`ibm_cis_routing`](/docs/terraform?topic=terraform-cis-resources#cis-routing)</li><li style="margin:0px; padding:0px">[`ibm_cis_waf_rule`](/docs/terraform?topic=terraform-cis-resources#cis-waf-rule)</li><li style="margin:0px; padding:0px">[`ibm_cis_waf_package`](/docs/terraform?topic=terraform-cis-resources#cis-waf-package)<li style="margin:0px; padding:0px">[`ibm_cis_waf_group`](/docs/terraform?topic=terraform-cis-resources#cis-waf-grp)</li><li style="margin:0px; padding:0px">[`ibm_cis_range_app`](/docs/terraform?topic=terraform-cis-resources#cis_range_app)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_cis`](/docs/terraform?topic=terraform-cis_data#cis)</li><li style="margin:0px; padding:0px">[`ibm_cis_certificates`](/docs/terraform?topic=terraform-cis_data#cis-certificates)</li><li style="margin:0px; padding:0px">[`ibm_cis_custom_certificates`](/docs/terraform?topic=terraform-cis_data#cis-custom-certificates)</li><li style="margin:0px; padding:0px">[`ibm_cis_custom_pages`](/docs/terraform?topic=terraform-cis_data#cis-custom-pages)</li><li style="margin:0px; padding:0px">[`ibm_cis_domain`](/docs/terraform?topic=terraform-cis_data#cis_domain)</li><li style="margin:0px; padding:0px">[`ibm_cis_edge_functions_actions`](/docs/terraform?topic=terraform-cis_data#cis-edge-functions-actions-ds)</li><li style="margin:0px; padding:0px">[`ibm_cis_edge_functions_triggers`](/docs/terraform?topic=terraform-cis_data#cis-edge-functions-triggers-ds)</li><li style="margin:0px; padding:0px">[`ibm_cis_firewall`](/docs/terraform?topic=terraform-cis_data#cis-firewallds)</li><li style="margin:0px; padding:0px">[`ibm_cis_global_load_balancers`](/docs/terraform?topic=terraform-cis_data#cis-global-lb-ds)</li><li style="margin:0px; padding:0px">[`ibm_cis_healthcheck`](/docs/terraform?topic=terraform-cis_data#cis-healthchecks)</li><li style="margin:0px; padding:0px">[`ibm_cis_ip_addresses`](/docs/terraform?topic=terraform-cis_data#cis_ip)</li><li style="margin:0px; padding:0px">[`ibm_cis_rate_limit`](/docs/terraform?topic=terraform-cis_data#rate-limit)</li><li style="margin:0px; padding:0px">[`ibm_cis_page_rules`](/docs/terraform?topic=terraform-cis_data#cis-page-rules
)</li><li style="margin:0px; padding:0px">[`ibm_cis_waf_rules`](/docs/terraform?topic=terraform-cis_data#cis-waf-rules)</li><li style="margin:0px; padding:0px">[`ibm_cis_waf_packages`](/docs/terraform?topic=terraform-cis_data#cis-waf-packages)<li style="margin:0px; padding:0px">[`ibm_cis_waf_groups`](/docs/terraform?topic=terraform-cis_data#cis-waf-groups)</li><li style="margin:0px; padding:0px">[`ibm_cis_range_apps`](/docs/terraform?topic=terraform-cis_data#cis-range-apps)</li></ul></td>
    </tr>
  </tbody>
  
  ## Key Management Service
  {: #ibm-kms}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_kms_key`](/docs/terraform?topic=terraform-kms-resources#kms-key)</li><li style="margin:0px; padding:0px">[`ibm_kp_key`](/docs/terraform?topic=terraform-kms-resources#kp-key)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_kms_key`](/docs/terraform?topic=terraform-kms-data-sources)</li><li style="margin:0px; padding:0px">[`ibm_kms_keys`](/docs/terraform?topic=terraform-kms-data-sources#kms-keys-ds)</li><li style="margin:0px; padding:0px">[`ibm_kp_key`](/docs/terraform?topic=terraform-kms-data-sources#kp-key)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
  ## Kubernetes Service
  {: #ibm-kubernetes-service}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_container_addons`](/docs/terraform?topic=terraform-container-resources#container-addons)</li><li style="margin:0px; padding:0px">[`ibm_container_alb`](/docs/terraform?topic=terraform-container-resources#container-alb)</li><li style="margin:0px; padding:0px">[`ibm_container_alb_cert`](/docs/terraform?topic=terraform-container-resources#container-alb-cert)</li><li style="margin:0px; padding:0px">[`ibm_container_api_key_reset`](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-container-resources#container-api-key-reset)</li><li style="margin:0px; padding:0px">[`ibm_container_bind_service`](/docs/terraform?topic=terraform-container-resources#container-bind)</li><li style="margin:0px; padding:0px">[`ibm_container_cluster`](/docs/terraform?topic=terraform-container-resources#container-cluster)</li><li style="margin:0px; padding:0px">[`ibm_container_cluster_feature`](/docs/terraform?topic=terraform-container-resources#container-cluster-feature)</li><li style="margin:0px; padding:0px">[`ibm_cr_namespace`](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-container-resources#cr-namespace)</li><li style="margin:0px; padding:0px">[`ibm_container_worker_pool`](/docs/terraform?topic=terraform-container-resources#container-pool)</li><li style="margin:0px; padding:0px">[`ibm_container_worker_pool_zone_attachment`](/docs/terraform?topic=terraform-container-resources#container-pool-zone)</li><li style="margin:0px; padding:0px">[`ibm_container_vpc_alb`](/docs/terraform?topic=terraform-container-resources#vpc-alb)</li><li style="margin:0px; padding:0px">[`ibm_container_vpc_cluster`](/docs/terraform?topic=terraform-container-resources#vpc-cluster)</li><li style="margin:0px; padding:0px">[`ibm_container_vpc_worker_pool`](/docs/terraform?topic=terraform-container-resources#vpc-worker-pool)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_container_addons`](/docs/terraform?topic=terraform-container-data-sources#container-addons-ds)</li><li style="margin:0px; padding:0px">[`ibm_container_alb`](/docs/terraform?topic=terraform-container-data-sources#container-alb-ds)</li><li style="margin:0px; padding:0px">[`ibm_container_alb_cert`](/docs/terraform?topic=terraform-container-data-sources#container-albcert-ds)</li><li style="margin:0px; padding:0px">[`ibm_container_bind_service`](/docs/terraform?topic=terraform-container-data-sources#container-bind-ds)</li><li style="margin:0px; padding:0px">[`ibm_container_cluster`](/docs/terraform?topic=terraform-container-data-sources#container-cluster)</li><li style="margin:0px; padding:0px">[`ibm_container_cluster_config`](/docs/terraform?topic=terraform-container-data-sources#container-cluster-config)</li><li style="margin:0px; padding:0px">[`ibm_container_cluster_worker`](/docs/terraform?topic=terraform-container-data-sources#container-worker)</li><li style="margin:0px; padding:0px">[`ibm_container_cluster_versions`](/docs/terraform?topic=terraform-container-data-sources#container-cluster-versions)</li><li style="margin:0px; padding:0px">[`ibm_cr_namespaces`](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-container-data-sources#cr-namespaces-ds)</li><li style="margin:0px; padding:0px">[`ibm_container_worker_pool`](/docs/terraform?topic=terraform-container-data-sources#container-worker-pool)</li><li style="margin:0px; padding:0px">[`ibm_container_vpc_alb`](/docs/terraform?topic=terraform-container-resources#vpc-alb)</li><li style="margin:0px; padding:0px">[`ibm_container_vpc_cluster`](/docs/terraform?topic=terraform-container-data-sources#container-vpc-cluster)</li><li style="margin:0px; padding:0px">[`ibm_container_vpc_cluster_worker`](/docs/terraform?topic=terraform-container-data-sources#container-vpc-worker)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
   ## Object Storage
  {: #ibm-object-storage}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_cos_bucket`](/docs/terraform?topic=terraform-object-storage-resources#cos-bucket)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_cos_bucket`](/docs/terraform?topic=terraform-object-storage-data-sources#cos-bucket)</li></ul></td>
    </tr>
  </tbody>
  </table>
  
   ## Power Systems
  {: #ibm-power-system}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
       <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_pi_image`](/docs/terraform?topic=terraform-power-vsi#power-image)</li><li style="margin:0px; padding:0px">[`ibm_pi_instance`](/docs/terraform?topic=terraform-power-vsi#power-instance)</li><li style="margin:0px; padding:0px">[`ibm_pi_key`](/docs/terraform?topic=terraform-power-vsi#ssh-key)</li><li style="margin:0px; padding:0px">[`ibm_pi_network`](/docs/terraform?topic=terraform-power-vsi#pi-networkport)</li><li style="margin:0px; padding:0px">[`ibm_pi_network_port`](/docs/terraform?topic=terraform-power-vsi#power-network)</li><li style="margin:0px; padding:0px">[`ibm_pi_snapshot`](/docs/terraform?topic=terraform-power-vsi#pi-snapshot)</li><li style="margin:0px; padding:0px">[`ibm_pi_volume`](/docs/terraform?topic=terraform-power-vsi#power-volume)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_pi_image`](/docs/terraform?topic=terraform-power-data-sources#power-image)</li><li style="margin:0px; padding:0px">[`ibm_pi_images`](/docs/terraform?topic=terraform-power-data-sources#power-images)</li><li style="margin:0px; padding:0px">[`ibm_pi_instance`](/docs/terraform?topic=terraform-power-data-sources#power-instance)</li><li style="margin:0px; padding:0px">[`ibm_pi_instance_ip`](/docs/terraform?topic=terraform-power-data-sources#power-instance-ip)</li><li style="margin:0px; padding:0px">[`ibm_pi_key`](/docs/terraform?topic=terraform-power-data-sources#power-ssh-key)</li><li style="margin:0px; padding:0px">[`ibm_pi_network`](/docs/terraform?topic=terraform-power-data-sources#power-network)</li><li style="margin:0px; padding:0px">[`ibm_pi_public_network`](/docs/terraform?topic=terraform-power-data-sources#power-public-network)</li><li style="margin:0px; padding:0px">[`ibm_pi_tenant`](/docs/terraform?topic=terraform-power-data-sources#power-tenant)</li><li style="margin:0px; padding:0px">[`ibm_pi_volume`](/docs/terraform?topic=terraform-power-data-sources#power-volume)</li><li style="margin:0px; padding:0px">[`ibm_pi_instance_volumes`](/docs/terraform?topic=terraform-power-data-sources#power-instance-volumes)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
  ## Resource management
  {: #ibm-resource-management}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
       <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_resource_group`](/docs/terraform?topic=terraform-resource-mgmt-resources#rg)</li><li style="margin:0px; padding:0px">[`ibm_resource_instance`](/docs/terraform?topic=terraform-resource-mgmt-resources#resource-instance)</li><li style="margin:0px; padding:0px">[`ibm_resource_key`](/docs/terraform?topic=terraform-resource-mgmt-resources#resource-key)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_resource_group`](/docs/terraform?topic=terraform-resource-management-data-sources#resource-group)</li><li style="margin:0px; padding:0px">[`ibm_resource_instance`](/docs/terraform?topic=terraform-resource-management-data-sources#resouce-instance)</li><li style="margin:0px; padding:0px">[`ibm_resource_key`](/docs/terraform?topic=terraform-resource-management-data-sources#resource-key)</li><li style="margin:0px; padding:0px">[`ibm_resource_quota`](/docs/terraform?topic=terraform-resource-management-data-sources#resource-quota)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
  ## Schematics 
  {: #ibm-schematics-data}
  
  <table>
    <thead>
     <th style="width:180px">Resources</th>
     <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
       <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">N/A</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_schematics_workspace`](/docs/terraform?topic=terraform-schematics-data-sources#schematics-workspace)</li><li style="margin:0px; padding:0px">[`ibm_schematics_output`](/docs/terraform?topic=terraform-schematics-data-sources#schematics-output)</li><li style="margin:0px; padding:0px">[`ibm_schematics_state`](/docs/terraform?topic=terraform-schematics-data-sources#schematics-state)</li></ul></td>
    </tr>
  </tbody>
  </table> 
  
  ## Transit Gateway 
  {: #ibm-transit-gateway}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_tg_connection`](/docs/terraform?topic=terraform-tg-resource#tg-connection)</li><li style="margin:0px; padding:0px">[`ibm_tg_gateway`](/docs/terraform?topic=terraform-tg-resource#tg-gateway-resource)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_tg_gateway`](/docs/terraform?topic=terraform-transit-gateway-ds#tg-gateway-ds)</li><li style="margin:0px; padding:0px">[`ibm_tg_gateways`](/docs/terraform?topic=terraform-transit-gateway-ds#tg-gateways-ds)</li><li style="margin:0px; padding:0px">[`ibm_tg_location`](/docs/terraform?topic=terraform-transit-gateway-ds#tg-location-ds)</li><li style="margin:0px; padding:0px">[`ibm_tg_locations`](/docs/terraform?topic=terraform-transit-gateway-ds#tg-locations-ds)</li></ul></td>
    </tr>
  </tbody>
  </table>
  

  
  ## VPC infrastructure
 {: #vpc-infrastructure}
  
  <table>
    <thead>
    <th style="width:180px">Resources</th>
    <th style="width:150px">Data sources</th>
    </thead>
  <tbody>
    <tr>
 <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_is_floating_ip`](/docs/terraform?topic=terraform-vpc-gen2-resources#provider-floating-ip)</li><li style="margin:0px; padding:0px">[`ibm_is_flow_log`](/docs/terraform?topic=terraform-vpc-gen2-resources#ibm_is_flow_log)</li><li style="margin:0px; padding:0px">[`ibm_is_ike_policy`](/docs/terraform?topic=terraform-vpc-gen2-resources#provider-ike-policy)</li><li style="margin:0px; padding:0px">[`ibm_is_image`](/docs/terraform?topic=terraform-vpc-gen2-resources#image)</li><li style="margin:0px; padding:0px">[`ibm_is_instance`](/docs/terraform?topic=terraform-vpc-gen2-resources#provider-instance)</li><li style="margin:0px; padding:0px">[`is_instance_group`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-is-instance-grp)</li><li style="margin:0px; padding:0px">[`is_instance_group_manager`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-is-instance-grp-manager)</li><li style="margin:0px; padding:0px">[`is_instance_group_manager_policy`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-is-instance-grp-manager-policy)</li><li style="margin:0px; padding:0px">[`ibm_is_ipsec_policy`](/docs/terraform?topic=terraform-vpc-gen2-resources#provider-ipsec)</li><li style="margin:0px; padding:0px">[`ibm_is_lb`](/docs/terraform?topic=terraform-vpc-gen2-resources#lb)</li><li style="margin:0px; padding:0px">[`ibm_is_lb_listener`](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-listener)</li><li style="margin:0px; padding:0px">[`ibm_is_lb_listener_policy`](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-listener-policy)</li><li style="margin:0px; padding:0px">[`ibm_is_lb_listener_policy_rule`](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-listener-policy-rule)</li><li style="margin:0px; padding:0px">[`ibm_is_lb_pool`](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-pool)</li><li style="margin:0px; padding:0px">[`ibm_is_lb_pool_member`](/docs/terraform?topic=terraform-vpc-gen2-resources#lb-pool-member)</li><li style="margin:0px; padding:0px">[`ibm_is_network_acl`](/docs/terraform?topic=terraform-vpc-gen2-resources#network-acl)</li><li style="margin:0px; padding:0px">[`ibm_is_public_gateway`](/docs/terraform?topic=terraform-vpc-gen2-resources#provider-public-gateway)</li><li style="margin:0px; padding:0px">[`ibm_is_security_group`](/docs/terraform?topic=terraform-vpc-gen2-resources#sec-group)</li><li style="margin:0px; padding:0px">[`ibm_is_security_group_rule`](/docs/terraform?topic=terraform-vpc-gen2-resources#sec-group-rule)</li><li style="margin:0px; padding:0px">[`ibm_is_security_group_network_interface_attachment`](/docs/terraform?topic=terraform-vpc-gen2-resources#sec-group-netint)</li><li style="margin:0px; padding:0px">[`ibm_is_subnet`](/docs/terraform?topic=terraform-vpc-gen2-resources#subnet)</li><li style="margin:0px; padding:0px">[`ibm_is_ssh_key`](/docs/terraform?topic=terraform-vpc-gen2-resources#ssh-key)</li><li style="margin:0px; padding:0px">[`is_instance_template`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-is-instance-template)</li><li style="margin:0px; padding:0px">[`ibm_is_virtual_endpoint_gateway`](/docs/terraform?topic=terraform-vpc-gen2-resources#virtual-endpoint-gwy)</li><li style="margin:0px; padding:0px">[`ibm_is_virtual_endpoint_gateway_ip`](/docs/terraform?topic=terraform-vpc-gen2-resources#virtual-endpoint-gwyip)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc`](/docs/terraform?topic=terraform-vpc-gen2-resources#provider-vps)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc_address_prefix`](/docs/terraform?topic=terraform-vpc-gen2-resources#address-prefix)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc_route`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-route)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc_routing_table`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-routing-table)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc_routing_table_route`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpc-routing-table-route)</li><li style="margin:0px; padding:0px">[`ibm_is_vpn_gateway`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpn-gateway)</li><li style="margin:0px; padding:0px">[`ibm_is_vpn_gateway_connection`](/docs/terraform?topic=terraform-vpc-gen2-resources#vpn-gateway-connection)</li><li style="margin:0px; padding:0px">[`ibm_is_volume`](/docs/terraform?topic=terraform-vpc-gen2-resources#volume)</li></ul></td>
      <td><ul style="margin:0px 0px 0px 20px; padding:0px"><li style="margin:0px; padding:0px">[`ibm_is_floating_ip`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#floating-ip-g2-ds)</li><li style="margin:0px; padding:0px">[`is_instance_group`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#instance-group)</li>
<li style="margin:0px; padding:0px">[`is_instance_group_manager_policies`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#instance-group-managerpolicies)</li>
<li style="margin:0px; padding:0px">[`is_instance_group_manager_policy`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#instance-group-managerpolicy)</li>
<li style="margin:0px; padding:0px">[`is_instance_group_managers`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#instance-group-managers)</li><li style="margin:0px; padding:0px">[`ibm_is_flow_logs`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#ibm-is-flow-logs)</li><li style="margin:0px; padding:0px">[`ibm_is_lb`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#ibm-is-lb)</li><li style="margin:0px; padding:0px">[`ibm_is_lbs`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#ibm-is-lbs)</li><li style="margin:0px; padding:0px">[`ibm_is_lb_profiles`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#ibm-is-lb-profiles)</li><li style="margin:0px; padding:0px">[`ibm_is_image`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-image)</li><li style="margin:0px; padding:0px">[`ibm_is_images`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-images)</li><li style="margin:0px; padding:0px">[`is_instance_group_profiles`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-instance-profiles)</li><li style="margin:0px; padding:0px">[`ibm_is_instance_profile`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-instance-profile)</li><li style="margin:0px; padding:0px">[`ibm_is_instance`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#instance)</li><li style="margin:0px; padding:0px">[`ibm_is_instance_profiles`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-instance-profiles)</li><li style="margin:0px; padding:0px">[`ibm_is_instances`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#instances)</li><li style="margin:0px; padding:0px">[`is_instance_profile`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-instance-profile)</li><li style="margin:0px; padding:0px">[`ibm_is_public_gateway`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#public-gwy-g2)</li><li style="margin:0px; padding:0px">[`ibm_is_region`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-region)</li><li style="margin:0px; padding:0px">[`ibm_is_security_group`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#sec-group-datasource)</li><li style="margin:0px; padding:0px">[`ibm_is_ssh_key`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-ssh-key)</li><li style="margin:0px; padding:0px">[`ibm_is_subnet`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-subnet)</li><li style="margin:0px; padding:0px">[`ibm_is_subnets`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-subnets)</li><li style="margin:0px; padding:0px">[`is_instance_templates`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-instance-templates)</li><li style="margin:0px; padding:0px">[`ibm_is_virtual_endpoint_gateways`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-endpoint-gwysds)</li><li style="margin:0px; padding:0px">[`ibm_is_virtual_endpoint_gateway_ips`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-endpoint-gwy-ipsds)</li>
<li style="margin:0px; padding:0px">[`ibm_is_virtual_endpoint_gateway`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-endpoint-gwyds)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc_default_routing_table`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-default-routing-tableds)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc_routing_table_routes`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-routing-tableds)</li><li style="margin:0px; padding:0px">[`ibm_is_vpc_routing_tables`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-routing-tablesds)</li><li style="margin:0px; padding:0px">[`ibm_is_vpn_gateways`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-gateways-ds)</li><li style="margin:0px; padding:0px">[`ibm_is_vpn_gateway_connections`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-gateways-connection-ds)</li><li style="margin:0px; padding:0px">[`ibm_is_zone`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-zone)</li><li style="margin:0px; padding:0px">[`ibm_is_zones`](/docs/terraform?topic=terraform-vpc-gen2-data-sources#vpc-zones)</li></ul></td>
    </tr>
  </tbody>
  </table>
