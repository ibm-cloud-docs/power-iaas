---

copyright:
  years: 2019, 2025
lastupdated: "2025-09-30"

---

{{site.data.keyword.attribute-definition-list}}

# Release notes
{: #cli-release-notes}

Use these release notes to learn about the latest changes to the {{site.data.keyword.powerSysFull}} CLI plug-in.
{: shortdesc}


## September 2025
{: #sep-2025}

### CLI v1.7.0

CLI plug-in version 1.7.0 is available for the {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}. In this release, the CLI is updated to use the latest version of the internationalization package. In addition, messages and options are updated to use new description guidelines.

**New commands**

The following CLI commands are added to the IBM Power Virtual Server Private Cloud workspaces:

- [ibmcloud pi network-peer](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-network-peer). You can use this command to create, delete, get, list, and update network peering connection. In addition, you can use this command to list peer network interfaces.
- [ibmcloud pi network-peer route-filter](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-network-peer-route-filter). You can use this command to create, delete, and get the details of the route filters in the network peering connection.


**New option**

The [--preferred-processor-compatibility-mode](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) option is added to the [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) and [ibmcloud pi instance sap create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-create) commands. You can use this option to set the instance to your preferred processor compatibility mode. The processor must be compatible with the system in use.


**Changes to the command output**

The outputs to the following commands are updated:

- Added `Effective Processor Compatibility Mode` and `Preferred Processor Compatibility Mode` to the instance output.
- Added `Creation Date` to the shared-processor-pool output.
- Added `State` to the image output.
- Added `CRN` to the volume snapshot output.
- Added `sr3` value to the [ibmcloud pi instance sap list --prefix](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-list) option to filter on s1122 and e1150 profiles.
- Updated the [ibmcloud pi snapshot update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-snapshot-update) output.
- Standardized the usage of `Creation Date` and `Last Update` dates across all outputs.


### CLI v1.6.1
{: #cli-v1.6.1}
The CLI version v1.6.1 is available with updates related to translation.








## July 2025
{: #july-2025}

### CLI version 1.6.0
{: #cli-v1.6.0}

The CLI plug-in version 1.6.0 supports Power11 systems. This version is available for the {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}.


**New command**

The following CLI commands are added:

- [ibmcloud pi route](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-route): You can use this command to create, delete, get, list, report, and update the custom network routes within the Power Virtual Server workspaces in the IBM data center.
- [ibmcloud pi virtual-serial-number software-tiers](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-virtual-serial-number-software-tiers): You can use this command to list all the supported software-tiers.
- [ibmcloud pi instance operation](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-instance-operation): You can use this command to assign a server boot mode, a server operating mode, a job task, or an operation type to an IBM i virtual server instance. This command can be used for the Power Virtual Server Private Cloud.

**New option**

The following options are added to the existing CLI commands:

- `--family`: Added to the [ibmcloud pi instance sap list](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-list) command. You can use this option to filter the SAP profiles by the family type.
- `--prefix`: Added to the [ibmcloud pi instance sap list](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-list) command. You can use this option to filter the SAP profiles by their prefix.
- `--user-tags`: Added to the [ibmcloud pi placement-group create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-placement-group-create) and [ibmcloud pi shared-processor-pool placement-group create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-shared-processor-pool-placement-group-create) commands. You can use this option to add user tags to the Power Virtual Server resources.
- `--description`: Added to the [ibmcloud pi ssh-key create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ssh-key-create) command. You can use this option to add or update the description of an SSH key.
- `--visibility` option is added to the [ibmcloud pi ssh-key create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ssh-key-create) and [ibmcloud pi ssh-key update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ssh-key-update) commands. You can use this option to set the visibility of an SSH key at `account` or `workspace` level.
- `--advertise`: Added to the [ibmcloud pi subnet create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-create) and [ibmcloud pi subnet update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-update) commands. You can use this option to determine whether or not to advertise the private networks.
- `--arp-broadcast`: Added to the [ibmcloud pi subnet create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-create) and [ibmcloud pi subnet update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-update) commands. You can use this option to enable or disable the ARP broadcast.
- `--software-tier`: Added to the [ibmcloud pi instance virtual-serial-number update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-virtual-serial-number-update) command. You can use this option to set a software tier on an IBM i instance.
- `--name` and `--key`: Added to the [ibmcloud pi ssh-key update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ssh-key-update) command. These options replace the `--new-name` and `--new-key` options.



**Deprecated or removed changes**

You can no longer use the following commands or options as the Power Virtual Server VPN as a Service (VPNaaS) reached its end of life and is not available for use:

- [ibmcloud pi vpn](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-vpn)
- [ibmcloud pi ike-policy](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ike-policy)
- [ibmcloud pi ipsec-policy](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ipsec-policy).
- `--access-config`, `--jumbo`, `--peer-id`, `--peer-type`, and `--source-ip` options from the [ibmcloud pi subnet create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-create) command.

- Removed the DHCP option as a subnet type in the Power Virtual Server Private Cloud.




### CLI version 1.5.2
{: #cli-v1.6.0}


The CLI plug-in version 1.5.2 for the {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} is available. In this version, a bug in the CLI plug-in metadata is fixed.






## April 2025
{: #cli-april-2025}

New CLI version v1.5.1 is available. The Power Virtual Server CLI plug-in is available with the following features:

**What's changed**

- Security update with CLI plugin dependencies.



## March 2025
{: #mar-2025}

New CLI version v1.5.0 is available. The Power Virtual Server CLI plug-in is available with the following features:

**New commands**
- Added [ibmcloud pi instance virtual-serial-number](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-instance-virtual-serial-number) family of commands (assign, get, unassign, and update) for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces.
- Added [ibmcloud pi virtual-serial-number](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-virtual-serial-number) family of commands (delete, get, list, and update) for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces.

**New options**
- Added `--virtual-serial-number` option to [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-instance-create) command for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces. Use this option to add virtual serial number information to an IBM i instance.
- Added `--retainVSN` option to [ibmcloud pi instance delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-instance-delete) command for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces. Use this option to confirm whether the virtual serial number must be retained in your account after it is removed from the instance.

**What's changed**
- In the {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}, if you enable the `sap-subscription-mode` option for the workspace, different options are displayed in the image list-catalog.
- Added a default system to the instance SAP profile and the instance SAP list.



## February 2025
{: #feb-2025}

New CLI version v1.4.2 is available. The Power Virtual Server CLI plug-in is available with the following features:

**New commands**

* Added [ibmcloud pi network-address-group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-network-address-group) group of commands (create, delete, get, list, member-add, member-remove, and update) for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} workspaces.
* Added [ibmcloud pi network-security-group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-network-security-group) group of commands (clone, create, delete, get, list, member-add, member-move, member-remove, rule-add, rule-remove, and update) for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} workspaces.

**New options**

* Added `--network-security-group-id` option to [ibmcloud pi instance subnet attach](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-subnet-attach) for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} workspaces. Use this option to specify the network security group of which the network interface is a member.
* Added `--deployment-target` option to [ibmcloud pi instance sap create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-create) command for  {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} workspaces. Use this option to specify the deployment of the dedicated host.
* Added `--user-tags` option to the [ibmcloud pi volume onboarding create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-onboarding-create) command for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} and [ibmcloud pi volume onboarding create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-on-prem#ibmcloud-pi-volume-onboarding-create) command for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}. Use this option to add a list of user tags to be associated with the volumes when you onboard them.

**What's changed**

* Deprecated [ibmcloud pi cloud-connection](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-cloud-connection-create) create command.
* Updated `--subnets` option for [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) to allow users to specify a network-security-group for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} workspaces.
* Removed `--sys-type` default option for [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) and [ibmcloud pi instance sap create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-create). This should not impact existing scripts.



## January 2025
{: #jan-2025}

New CLI version `v1.4.1` is available. The {{site.data.keyword.powerSys_notm}} CLI plug-in is available with the following features:

**What's changed**

* Security update with CLI plugin dependencies.

* Fixed the [ibmcloud pi workspace action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-action) command to use local context.




## December 2024
{: #dec-2024}

New CLI version `v1.4.0` is available. The {{site.data.keyword.powerSys_notm}} CLI plug-in is available with the following features:

**New commands**

* Added ibmcloud pi instance virtual-serial-number family of commands (assign, unassigned, get, and update).
* Added ibmcloud pi network-peer family of commands (list) for {{site.data.keyword.on-prem}} workspaces.
* Added ibmcloud pi  virtual-serial-number family of commands (delete, get, list, and update).

**New options**

* Added `--private` option to [ibmcloud pi datacenter get and list commands](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-datacenter). Use this option to retrieve additional details about a private datacenter that you own.
* Added `--virtual-serial-number` option to [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) command. Use this option to add virtual serial number information to an IBM i instance.
* Added `--retainVSN` option to [ibmcloud pi instance delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-delete) command. Use this option to determine whether the virtual serial number is retained after it is removed from the instance.

**What's changed**

* In the [ibmcloud pi subnet create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-create) command `--access-config` option is deprecated for {{site.data.keyword.on-prem}} workspaces. Alternatively, you can use `--peer-id`, `--peer-type`, and `--source-id` options.
* The `che01` region is supported in the following commads:
    * [ibmcloud pi image export](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export)
    * [ibmcloud pi image import](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import)
    * [ibmcloud pi instance capture](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-capture)
* The `per-migrate-status` option is removed from the [ibmcloud pi workspace action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-action) command.
* Commands and options are updated with wording improvements.


## September 2024
{: #sep-2024}

New CLI version `v1.3.0` is available. The {{site.data.keyword.powerSys_notm}} CLI plug-in is available with the following features:

**New commands**
* Added  [ibmcloud pi instance volume bulk-detach](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-volume-bulk-detach) command to detach multiple volumes from an instance at once.
* Added [ibmcloud pi instance snapshot update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-snapshot-update) command to update name and description of a snapshot.
* Added [ibmcloud pi network-interface](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-network-interface) family of commands (create, delete, get, list, update).
* Added [ibmcloud pi volume bulk-delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-bulk-delete) command to delete multiple volumes at once.
* Added [ibmcloud pi volume clone-async](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-async) _create_ and _get_ commands to asynchronously create clone tasks and query their status.
* Added [ibmcloud pi volume snapshot](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-snapshot) _get_ and _list_ to retrieve information about snapshots in a workspace.
* Added [ibmcloud pi workspace action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-action) command to perform an action in a workspace.

**New options**
* Added `--user-tags` option to [ibmcloud pi host reserve](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-host-reserve), [ibmcloud pi image create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-create), [ibmcloud pi image import](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import), [ibmcloud pi instance capture create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-capture-create), [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create), [ibmcloud pi shared-processor-pool create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-shared-processor-pool-create), [ibmcloud pi instance snapshot create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-snapshot-create), [ibmcloud pi subnet create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-create), [ibmcloud pi volume clone execute](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-execute), [ibmcloud pi volume create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-create), and [ibmcloud pi workspace create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-create) commands. Use this option to add a comma separated list of user tags to be attached to the created resource.
* Added user tag option to `--hosts` option in [ibmcloud pi host-group create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-host-group-create) command. Option is now also repeatable.
* Added `--boot-volume-replication-enabled` option to [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create), and [ibmcloud pi instance sap create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-create) command. Use this to enable storage replication on the boot volume.
* Added `--replication-sites` option to [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) and [ibmcloud pi instance sap create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-sap-create) command. Use this to indicate the replication site of the boot volume.
* Added `--replication-sites` option to [ibmcloud pi volume create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-create). Use this to indicate the replication site of the volume.
* Added "maxVolumeSupport" valid value to `--storage-connection` option in [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) command.
* Added `--boot-volume` option to [ibmcloud pi instance volume attach](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-volume-attach) command. Use this to attach a boot volume to an instance.

**What's changed**
* [ibmcloud pi snapshot](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-snapshot) command and subcommands have been deprecated. Please use [ibmcloud pi instance snapshot](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-snapshot) command family instead.
* Clarified usage of [ibmcloud pi instance console list](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-console-list), [ibmcloud pi instance capture create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-capture-create) and [ibmcloud pi job list](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-job-list) commands.
* Minor wording improvements to several command and options.

## June 2024
{: #jun-2024}

New CLI version `v1.2.0` available. The {{site.data.keyword.powerSys_notm}} CLI plug-in is available with the following features:

**New commands**
 * Added [ibmcloud pi available-hosts](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-available-hosts) command to list of hosts available for reservation.
 * Added [ibmcloud pi host](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-host) family of commands (get, list, release, reserve, update).
 * Added [ibmcloud pi host-group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-host-group) family of commands (create, get, list, update).
 * Added [ibmcloud pi instance snapshot](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-snapshot) family of commands (create, delete, get, update, and restore).
 * Enabled [ibmcloud pi shared-processor-pool](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-shared-processor-pool) create, delete, get, list, update commands on {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces.
 * Enabled [ibmcloud pi shared-processor-pool placement-group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-shared-processor-pool-placement-group) create, delete, get, list, member-add, and member-remove commands on {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces.

**New options**
 * Added `--import-details` option to [ibmcloud pi image import](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) command. Use this to import details for SAP image. You must include a license, product, and vendor. Valid license value: byol. Valid product value: Hana, Netweaver. Valid vendor value: SAP.
 * Added `--storage-connection` option to [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) command.  Use this to set the connection type. Valid value is `vSCSI` (more will be added in the future).
 * Added `--storage-pool-affinity` option to [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) and [ibmcloud pi instance update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-update) command. Use this to indicate whether all volumes attached to the server must reside in the same storage pool.
 * Added `--deployment-target` option to [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) command. Use this to set the deployment of the dedicated host.
 * Added `--host-id` option to [ibmcloud pi shared-processor-pool](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-shared-processor-pool) create command. This option is only available for dedicated hosts.
 * Added `--checksum` option to [ibmcloud pi image import](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import), [ibmcloud pi image export](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export), and [ibmcloud pi instance capture](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-capture) create on {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces. This creates a checksum file after the operation is complete.
 * Enabled `--shared-processor-pool`, `--IBMiCSS-license`, `--IBMiPHA-license`, and `--IBMiRDS-users` options on [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) command on {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces.
 * Enabled `--IBMiCSS-license`, `--IBMiPHA-license`, and `--IBMiRDS-users` options on [ibmcloud pi instance update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-update) command on {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} workspaces.

**What's changed**
The [ibmcloud pi instance snapshot list](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-snapshot-list) command can now list all snapshots of an instance or all snapshots on the workspace depending on arguments.

## April 2024
{: #apr-2024}

New CLI version `v1.1.1` available. The {{site.data.keyword.powerSys_notm}} CLI plug-in is available with the following features:

 - Added virtual core support. You can now use `--virtual-cores` option in the [instance update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-update) command.
 - Added the "eu-es" region to the [image export](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export), [image-import](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import), and [instance-capture](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-capture) commands.

## March 2024
{: #mar-2024}

New CLI version `v1.1.0` available. The {{site.data.keyword.powerSys_notm}} CLI plug-in is available with the following features:

 - Added virtual core support. You can now use `--virtual-cores` option in the [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) command.
 - Added mtu support. You can now use `--mtu` in the [ibmcloud pi subnet create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-create) command. The jumbo option is deprecated.
 - The updated [ibmcloud pi volume clone](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone) commands now use the latest API.
 - Reworks [ibmcloud pi volume clone cancel](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-cancel) and [ibmcloud pi volume clone create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-create) commands.
 - Added a new [ibmcloud pi volume clone delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-delete) command.

## January 2024
{: #jan-2024}

- New CLI version `0.7.1` available. Here are the changes for the new CLI version:

    **New options**

    * "list-catalog": `--sap` Include SAP images.
    * "list-catalog": `--vtl` Include VTL images.

    **What's Changed**

    Removed `--IBMiDBQ-license` option from `instance-create` command.

    **Bug Fixes**

    Fixed issue in `instance-update` command when `--virtual-optical-device` option is not used.

## December 2023
{: #dec-2023}

New CLI version `0.7.0` available. Here are the changes for the new CLI version:

**New command**

- [List all storage tiers for the targeted region](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-storage-tiers): List all storage tiers for the targeted region.

**New options**

- A `--virtual-optical-device` option is added in [Update a server instance](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-update) command: Use this to attach a virtual optical device to this instance. Valid value is "attach".
- A `--mtu` option is added in [Create a private network](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-network-create-private) command: Use this is to define the Maximum Transmission Unit. The default value is 1450.
- A `--mtu` option is added in [Create a public network](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-network-create-public) command: Use this is to define the Maximum Transmission Unit. The default value is 1450.
- A `--target-tier` option is added in [Perform an action on a volume](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-action) command:  Use this to change the storage tier of the volume (use [List all storage tiers for the targeted region](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-storage-tiers) to see available storage tiers in the targeted region). `Tier5k` volumes cannot exceed 200 GB.


**What's Changed**

- New custom deployment type - `VMNoStorage` for [Create a server instance](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-create) command.
- Deprecate `--jumbo` option in [Create a public network](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-network-create-public) and [Create a private network](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-network-create-private) commands.
- New Power Edge Router (PER) details field when using the `workspace` command.

## November 2023
{: #nov-2023}

New CLI version `0.6.0` available. Here are the new changes for the new CLI version:
   * New commands - [Create a workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-workspace-create) and [Delete a workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-workspace-delete) added.


New CLI version `0.5.0` available. Here are the new changes for the new CLI version:
   * New `--user-data` option added in the [instance-create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-create) command.
   * New command [datacenter](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-datacenter) and [datacenters](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-datacenters) added.
   * Deprecated `service-list` command in favor of new [workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-workspace) and [workspaces](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-workspaces) commands.

## September 2023
{: #sep-2023}

- Added s1022 in `sys-type value` for [Create a server instance](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-create) and [Create a virtual tape library](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-virtual-tape-library-create) commands.

## 2022
{: #2022}

### December 2022
{: #dec-2022}

- You can now get new error messages for undefined response codes for new service endpoint response codes.

### September 2022
{: #sept-2022}

- You can now use shared processor pool that uses CLI. The following are new commands for shared processor pools:
    - [View details of a shared processor pool](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-shared-processor-pool)
    - [Create a shared processor pool](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-shared-processor-pool-create)
    - [Delete a shared processor pool](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-shared-processor-pool-delete)
    - [Update a shared processor pool](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-shared-processor-pool-update)
    - [List all shared processor pools](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-shared-processor-pools)
    - [View details of a shared processor pool placement group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-spp-placement-group)
    - [Create a shared processor pool placement group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-spp-placement-group-create)
    - [Delete a shared processor pool placement group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-spp-placement-group-delete)
    - [Add a shared processor pool to the placement group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-spp-placement-group-member-add)
    - [Remove a shared processor pool from the placement group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-spp-placement-group-member-remove)
    - [List all shared processor pool placement groups](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-spp-placement-groups)

- The command [Create a server instance](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-create) is updated to include the following new options for SPP and Epic:
    - *shared-processor-pool value*
    - *deployment-type value*

- You can now use global replication service by using CLI. The following commands are added new for global replication service:
    - [List disaster recovery locations for the current region or all regions](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-disaster-recovery-locations)
    - [Perform an action on a volume](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-action)
    - [Get a list of flash copy mappings of a volume directly from primary storage host.](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-flash-copy-mapping)
    - [View details of a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group)
    - [Create a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-create)
    - [Delete a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-delete)
    - [Get all remote copy relationships for each volume in a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-remote-copy-relationships)
    - [Reset a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-reset)
    - [List all volume groups](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-groups)
    - [Start a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-start)
    - [Stop a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-stop)
    - [View storage details of a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-storage-details)
    - [Update a volume group](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-update)
    - [Get the information of volume onboarding operation](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-onboarding)
    - [Create a volume onboarding operation](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-onboarding-create)
    - [List all volume onboarding operations](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-onboardings)
    - [Get the remote copy relationship information of a volume](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-remote-copy-relationship)

- The command [Create a volume](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-create) is updated to include a new option *replication-enabled*.

- The description of [Create a new SAP PVM Instance](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-sap-create-instance) is changed for HANA images.


### July 2022
{: #Jul-2022}

- You can now use [Transit Gateway](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-connection-create) to interconnect your {{site.data.keyword.powerSys_notm}} to the {{site.data.keyword.cloud_notm}} classic and Virtual Private Cloud (VPC).

### April 2022
{: #apr-2022}

- Provisioning VTL instances is temporarily disabled.

## 2021
{: #2021}

### December 2021
{: #dec-2021}

- You can now use [Storage pools](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-create) to set affinity policies by using CLI.
- You can now use [Create connection](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-connection-create) to set a 10 Gbps speed for your Cloud connection by using CLI.
- You can now use [Placement Groups](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-placement-group-create) to create placement groups and add VMs to set policies by using CLI.


### October 2021
{: #oct-2021}

- You can now use [VPN](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-vpn-connection-create) to create VPN connection by using CLI.
- You can now use [VPN IKE policies](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-vpn-ike-policies) to create an IKE policy for the VPN connection by using CLI.
- You can now use [VPN IKE policies](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-vpn-ike-policies) to create an IPsec policy for the VPN connection by using CLI.


### September 2021
{: #sep-2021}

- You can now use [Import Image](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-image-import) to Import an image from IBM Cloud Object Storage by using CLI.
- You can now use [Jobs](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-job) to View details of a job by using CLI.
- You can now use [Console language](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-update-console-language) to update Language to Japanese.

### May 2021
{: #may-2021}

- You can now use [Cloud connection](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-connection-create) to automate the way you connect your Power Systems Virtual Server instances to the IBM Cloud resources by using CLI.

### March 2021
{: #mar-2021}

- You can now manage [snapshots](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-snapshots) of a cloud instance by using the CLI.
- You can create and list [SAP profiles](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-sap-list) by using CLI.
- You can [list of available system pools](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-system-pool) within a particular data center by using CLI.
- You can [attach](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-connection-attach-network), [detach](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-connection-detach-network), or [list all the attached networks](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-instance-networks) to an instance.
- Added image-import progress (task) monitoring.
