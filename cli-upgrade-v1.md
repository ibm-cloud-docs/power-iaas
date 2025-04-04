---

copyright:
  years: 2024
lastupdated: "2024-01-31"

---

{{site.data.keyword.attribute-definition-list}}

# Comparison between IBM {{site.data.keyword.powerSys_notm}} CLI versions 0.7.1 and 1.x.x
{: #whats-new-v1}



---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}

---


The tables in the following sections provide the comparison between the CLI version `1.0.0` or later (referred as V 1.x.x) with the version `0.7.1` (referred as V 0.7.1).

## ibmcloud pi cloud-connection
{: connection}



| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi connection-create      | ibmcloud pi cloud-connection create     |
| ibmcloud pi connection-delete      | ibmcloud pi cloud-connection delete     |
| ibmcloud pi cloud-connection       | ibmcloud pi cloud-connection get        |
| ibmcloud pi connection-update      | ibmcloud pi cloud-connection update     |
| ibmcloud pi connections            | ibmcloud pi cloud-connection list       |
| ibmcloud pi connection-vpcs        | ibmcloud pi connection-vpcs             |


## ibmcloud pi cloud-connection subnet
{: connect-subnet}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi connection-attach-network      | ibmcloud pi cloud-connection subnet attach      |
| ibmcloud pi connection-detach-network      | ibmcloud pi cloud-connection subnet detach      |

## ibmcloud pi disaster-recovery
{: dr}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi disaster-recovery-locations     | ibmcloud pi disaster-recovery      |

## ibmcloud pi ike-policy
{: ike}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi vpn-ike-policy-add     | ibmcloud pi ike-policy create      |
| ibmcloud pi vpn-ike-policy-delete  | ibmcloud pi ike-policy delete      |
| ibmcloud pi vpn-ike-policy         | ibmcloud pi ike-policy get         |
| ibmcloud pi vpn-ike-policies       | ibmcloud pi ike-policy list        |
| ibmcloud pi vpn-ike-policy-update  | ibmcloud pi ike-policy update      |

## ibmcloud pi image
{: image}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi image-create          | ibmcloud pi image create          |
| ibmcloud pi image-delete          | ibmcloud pi image delete          |
| ibmcloud pi image                 | ibmcloud pi image get             |
| ibmcloud pi image-export          | ibmcloud pi image export          |
| ibmcloud pi image-export-show     | ibmcloud pi image export-show [^footnote1] |
| ibmcloud pi image-import          | ibmcloud pi image import          |
| ibmcloud pi image-import-show     | ibmcloud pi image import-show     |
| ibmcloud pi image-list-catalog    | ibmcloud pi image list-catalog    |
| ibmcloud pi images                | ibmcloud pi image list            |

[^footnote1]: The 'image export-show' now displays information about the latest image export job without requiring a 'job_id' parameter.
## ibmcloud pi instance
{: instance}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
|ibmcloud pi instance-create    | ibmcloud pi instance create   |
|ibmcloud pi instance-delete    | ibmcloud pi instance delete   |
|ibmcloud pi instance           | ibmcloud pi instance get      |
|ibmcloud pi instances          | ibmcloud pi instance list     |
|ibmcloud pi instance-operation | ibmcloud pi instance operation|
|ibmcloud pi instance-update    | ibmcloud pi instance update   |

## ibmcloud pi instance action
{: inst-action}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
|ibmcloud pi instance-hard-reboot <br/> ibmcloud pi instance-reset-state <br/> ibmcloud pi instance-soft-reboot <br/> ibmcloud pi instance-start <br/> ibmcloud pi instance-stop <br/> ibmcloud pi instance-immediate-shutdown | ibmcloud pi instance action [^footnote3] |

[^footnote3]: You get "hard-reboot", "immediate-shutdown", "reset-state", "soft-reboot", "start", and "stop" as command options.


## ibmcloud pi instance capture
{: inst-capture}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
|ibmcloud pi instance-capture       | ibmcloud pi instance capture create   |
|ibmcloud pi instance-capture-show  | ibmcloud pi instance capture show     |

## ibmcloud pi instance console
{: inst-console}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi instance-get-console              | ibmcloud pi instance console get     |
| ibmcloud pi instance-list-console-languages   | ibmcloud pi instance console list    |
| ibmcloud pi instance-update-console-language  | ibmcloud pi instance console update  |

## ibmcloud pi instance sap
{: inst-sap}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
|ibmcloud pi sap-create-instance    | ibmcloud pi instance sap create |
|ibmcloud pi sap-profile            | ibmcloud pi instance sap profile|
|ibmcloud pi sap-list               | ibmcloud pi instance sap list   |

## ibmcloud pi instance snapshot
{: inst-snap}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi instance-list-snapshots   | ibmcloud pi instance snapshot list    |

## ibmcloud pi instance subnet
{: inst-subnet}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi instance-attach-network       | ibmcloud pi instance subnet attach  |
| ibmcloud pi instance-detach-network       | ibmcloud pi instance subnet detach  |
| ibmcloud pi instance-networks             | ibmcloud pi instance subnet list    |

## ibmcloud pi instance volume
{: inst-vol}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi volume-attach | ibmcloud pi instance volume attach    |
| ibmcloud pi volume-detach | ibmcloud pi instance volume detach    |

## ibmcloud pi ipsec-policy
{: ipsec}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi vpn-ipsec-policy-add      | ibmcloud pi ipsec-policy create   |
| ibmcloud pi vpn-ipsec-policy-delete   | ibmcloud pi ipsec-policy delete   |
| ibmcloud pi vpn-ipsec-policy          | ibmcloud pi ipsec-policy get      |
| ibmcloud pi vpn-ipsec-policies        | ibmcloud pi ipsec-policy list     |
| ibmcloud pi vpn-ipsec-policy-update   | ibmcloud pi ipsec-policy update   |

## ibmcloud pi job
{: job}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi job-delete    | ibmcloud pi job delete  |
| ibmcloud pi job           | ibmcloud pi job get     |
| ibmcloud pi jobs          | ibmcloud pi job list    |

## ibmcloud pi placement-group
{: pg}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi placement-group-create        | ibmcloud pi placement-group create        |
| ibmcloud pi placement-group-delete        | ibmcloud pi placement-group delete        |
| ibmcloud pi placement-group               | ibmcloud pi placement-group get           |
| ibmcloud pi placement-groups              | ibmcloud pi placement-group list          |
| ibmcloud pi placement-group-server-add    | ibmcloud pi placement-group server-add    |
| ibmcloud pi placement-group-server-remove | ibmcloud pi placement-group server-remove |

## ibmcloud pi shared-processor-pool
{: spp}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi shared-processor-pool-create |ibmcloud pi shared-processor-pool create  |
| ibmcloud pi shared-processor-pool-delete |ibmcloud pi shared-processor-pool delete  |
| ibmcloud pi shared-processor-pool        |ibmcloud pi shared-processor-pool get     |
| ibmcloud pi shared-processor-pools       |ibmcloud pi shared-processor-pool list    |
| ibmcloud pi shared-processor-pool-update |ibmcloud pi shared-processor-pool update  |


## ibmcloud pi shared-processor-pool placement-group
{: spp-pg}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi spp-placement-group-create        | ibmcloud pi shared-processor-pool placement-group create        |
| ibmcloud pi spp-placement-group-delete        | ibmcloud pi shared-processor-pool placement-group delete        |
| ibmcloud pi spp-placement-group               | ibmcloud pi shared-processor-pool placement-group get           |
| ibmcloud pi spp-placement-groups              | ibmcloud pi shared-processor-pool placement-group list          |
| ibmcloud pi spp-placement-group-member-add    | ibmcloud pi shared-processor-pool placement-group member-add    |
| ibmcloud pi spp-placement-group-member-remove | ibmcloud pi shared-processor-pool placement-group member-remove |

## ibmcloud pi snapshot
{: snap}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi snapshot-create       | ibmcloud pi snapshot create   |
| ibmcloud pi snapshot-delete       | ibmcloud pi snapshot delete   |
| ibmcloud pi snapshot              | ibmcloud pi snapshot get      |
| ibmcloud pi snapshots             | ibmcloud pi snapshot list     |
| ibmcloud pi snapshot-restore      | ibmcloud pi snapshot restore  |

## ibmcloud pi ssh-key
{: ssh-key}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi key           | ibmcloud pi ssh-key get       |
| ibmcloud pi key-create    | ibmcloud pi ssh-key create    |
| ibmcloud pi key-delete    | ibmcloud pi ssh-key delete    |
| ibmcloud pi key-update    | ibmcloud pi ssh-key update    |
| ibmcloud pi keys          | ibmcloud pi ssh-key list      |

## ibmcloud pi storage-pools
{: storage-pool}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:
|ibmcloud pi storage-pools  | ibmcloud pi storage-pools <br/> (Unchanged) |

## ibmcloud pi subnet
{: subnet}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi network-create-private <br/> ibmcloud pi network-create-public [^footnote2]    | ibmcloud pi subnet create |
| ibmcloud pi network-delete    | ibmcloud pi subnet delete   |
| ibmcloud pi network           | ibmcloud pi subnet get      |
| ibmcloud pi networks          | ibmcloud pi subnet list     |
| ibmcloud pi network-update    | ibmcloud pi subnet update   |

[^footnote2]: These commands have changed in {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}.
## ibmcloud pi system-pools
{: sys-pool}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi system-pool   | ibmcloud pi system-pools  |

## ibmcloud pi volume
{: vol}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi volume-action                     | ibmcloud pi volume action                     |
| ibmcloud pi volume-create                     | ibmcloud pi volume create                     |
| ibmcloud pi volume-delete                     | ibmcloud pi volume delete                     |
| ibmcloud pi volume-flash-copy-mapping         | ibmcloud pi volume flash-copy-mapping         |
| ibmcloud pi volume                            | ibmcloud pi volume get                        |
| ibmcloud pi volumes                           | ibmcloud pi volume list                       |
| ibmcloud pi volume-remote-copy-relationship   | ibmcloud pi volume remote-copy-relationship   |
| ibmcloud pi volume-update                     | ibmcloud pi volume update                     |

## ibmcloud pi volume-clone
{: vol-cone}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi volume-clone          | ibmcloud pi volume clone get      |
| ibmcloud pi volume-create-clone   | ibmcloud pi volume clone create   |

## ibmcloud pi volume-group
{: vol-group}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi volume-group-create                       | ibmcloud pi volume-group create                     |
| ibmcloud pi volume-group-delete                       | ibmcloud pi volume-group delete                     |
| ibmcloud pi volume-group                              | ibmcloud pi volume-group get                        |
| ibmcloud pi volume-groups                             | ibmcloud pi volume-group list                       |
| ibmcloud pi volume-group-remote-copy-relationships    | ibmcloud pi volume-group remote-copy-relationships  |
| ibmcloud pi volume-group-storage-details              | ibmcloud pi volume-group storage-details            |
| ibmcloud pi volume-group-update                       | ibmcloud pi volume-group update                     |

## ibmcloud pi volume-group action
{: vol-inst-action}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi volume-group-reset  <br/> ibmcloud pi volume-group-start <br/>  ibmcloud pi volume-group-stop    | ibmcloud pi volume-group action [^footnote4]|

[^footnote4]: You get reset, start, and stop as command options.
## ibmcloud pi volume-onboarding
{: vol-onboard}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi volume-onboarding-create      | ibmcloud pi volume onboarding create  |
| ibmcloud pi volume-onboarding             | ibmcloud pi volume onboarding get     |
| ibmcloud pi volume-onboardings            | ibmcloud pi volume onboarding list    |

## ibmcloud pi vpn
{: vpn}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi vpn-connection-create      | ibmcloud pi vpn create    |
| ibmcloud pi vpn-connection-delete      | ibmcloud pi vpn delete    |
| ibmcloud pi vpn-connection             | ibmcloud pi vpn get       |
| ibmcloud pi vpn-connections            | ibmcloud pi vpn list      |
| ibmcloud pi vpn-connection-update      | ibmcloud pi vpn update    |

## ibmcloud pi vpn peer-subnet
{: vpn-peer-subnet}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi vpn-connection-peer-subnet-attach     | ibmcloud pi vpn peer-subnet attach  |
| ibmcloud pi vpn-connection-peer-subnet-detach     | ibmcloud pi vpn peer-subnet detach  |
| ibmcloud pi vpn-connection-peer-subnets           | ibmcloud pi vpn peer-subnet list    |

## ibmcloud pi vpn subnet
{:vpn-subnet}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi vpn-connection-network-attach | ibmcloud pi vpn subnet attach |
| ibmcloud pi vpn-connection-network-detach | ibmcloud pi vpn subnet detach |
| ibmcloud pi vpn-connection-networks       | ibmcloud pi vpn subnet list   |

## ibmcloud pi workspace
{: workspace}

| V 0.7.1  | V 1.x.x |
| ------------- |:-------------:|
| ibmcloud pi service-list      | ibmcloud pi workspace list    |
| ibmcloud pi service-target    | ibmcloud pi workspace target  |


## Removed Commands in Version 1.0.0 or later
{: removedcmd}

1. ibmcloud pi task
2. ibmcloud pi task-delete

## New Commands in Version 1.0.0 or later
{: newcmd}

1. ibmcloud pi datacenter get
2. ibmcloud pi datacenter list
3. ibmcloud pi instance volume list
4. ibmcloud pi volume clone cancel
5. ibmcloud pi volume clone execute
6. ibmcloud pi volume clone list
7. ibmcloud pi volume clone start
8. ibmcloud pi workspace create
9. ibmcloud pi workspace delete
