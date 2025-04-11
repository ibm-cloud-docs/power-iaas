---

copyright:
  years: 2024

lastupdated: "2025-04-11"

keywords: Global Replication Services, GRS, configure GRS, pricing for GRS, GRS APIs,


subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Global Replication Services (GRS)
{: #getting-started-GRS}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Disasters are unplanned events that cause severe damage, incur a loss to business, and affect all organizations. Since most workloads run on cloud infrastructure nowadays, it is essential to have robust and resilient cloud infrastructure that is prepared to handle these catastrophic hits and have minimal impact on business.
{: shortdesc}


The {{site.data.keyword.powerSysFull}} provides a set of APIs to enable disaster recovery (DR) solution for your virtual server instances. IBM Cloud infrastructure internally uses Global Mirror Change Volume (GMCV) as storage technology that provides asynchronous replication.

A new resource volume group is introduced to enable, disable, and manage storage replication consistency group. The volume group holds the volumes that need to be recovered at the time of disaster. Make the volume DR capable by adding the volume to the volume group. To trigger failover and failback operations, use the volume group start and stop operations.

GRS provides an asynchronous volume-level replication service that can be used as the foundation for higher-level disaster recovery (DR) automation solutions.





The scope of the GRS service is to create and manage replicated resources that include the following items:
- Volume lifecycle operations support on replicated volumes.
- APIs to manage volume groups through create, update, delete, start, and stop operations.
- Virtual server instance lifecycle operations by using replicated volumes.
- Onboard auxiliary volume on secondary site for volume recovery.



[{{site.data.keyword.on-prem}}]{: tag-red}

## GRS in [{{site.data.keyword.on-prem}}]{: tag-red}
{: #grs-on-prem}

The GRS enablement in {{site.data.keyword.on-prem-fname}} enables asynchronous replication of data between the primary location infrastructure and the secondary location infrastructure. The two infrastructure locations have the identical set of capabilities that {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} provides.

The infrastructure in the IBM {{site.data.keyword.powerSys_notm}} Private Cloud in which your workspace is located, has the primary volumes of the replication pairs. The infrastructure in the secondary location has the auxiliary volumes.

IBM Cloud infrastructure internally uses IBM FlashSystems Global Mirror Change Volume (GMCV) as storage technology that provides asynchronous replication.

Each time a replicated volume is created, four copies of volumes are created across the infrastructure:

- Primary volume in the primary infrastructure
- Primary change volume in the primary infrastructure to store the delta changes
- Auxiliary volume in the secondary infrastructure
- Auxiliary change volume in the secondary infrastructure to update the delta changes

You must provide the required network configuration between the primary location and the secondary location for replication, which includes the following prerequisites:

* The network bandwidth must be greater than or equal to 10 Gbps.
* The network latency must be less than or equal to 200 ms.

During the first sync, the entire data from primary volumes is copied to the auxiliary volumes. For subsequent syncs, only the delta changes are copied. The effective Recovery Point Objective (RPO) depends on the capability of the underlying network throughput and the application characteristics. If the network throughput is insufficient to reach the defined RPO, then the time duration between the synchronization increases.

If the defined RPO exceeds for more than 8 hours, the IBM operations team alerts you.
{: note}




## Additional information
{: #additional-info-GRS}

If you need a more detailed information on GRS, see [Global Replication Services Solution by using IBM Power Virtual Server](https://cloud.ibm.com/media/docs/downloads/power-iaas/Global_Replication_Services_Solution_using_IBM_Power_Virtual_Server.pdf){: external}

## Pricing for GRS
{: #pricing-GRS}

The charges for GRS depend on the location where you create a replication-enabled volume.

Replication-enabled volumes incur the following charges:

- A base charge for the replication capability is based on the size of the replication-enabled volume under the part number "GLOBAL_REPLICATION_STORAGE_GIGABYTE_HOURS".
- The replication-enabled volumes charges are two times the size of the volume against the storage part numbers. This is based on the tier of the volume against the primary volume.

    Auxiliary volumes are not charged separately and are part of the primary volume charges.
    {: note}

Upon a site failure due to a catastrophe, metering becomes unavailable from the failed site. The charges for replication-enabled volumes are charged from the remote site. The charges are two times the size of the volume against the storage part numbers based on the tier of the volume. During this time, the base charge for the replication capability for the replication-enabled volumes is not charged.

## Setting up GRS
{: #configure-GRS}

GRS involves two sites where storage replication is enabled. These two sites are fixed and mapped into one-to-one relationship mode in both directions. These two sites are fixed and are in replication partnership in both directions.

You can create a replication-enabled volume from any site, the site from where the request is initiated contains the primary volume. The remote site is auxiliary and contains an auxiliary volume.


While you are creating a storage volume from the user interface, you can enable the volume for replication by completing the following steps:

1. In the **Global Replication Service** section, set the **Volume replication** to on. The name of the primary data center is displayed.
2. From the **Secondary data center** list, select the displayed secondary site name.

The GRS details of the volume are displayed when you click the storage volume.

A storage volume can have one of the following replication status:

- **Not eligible**: The storage volume is not in a GRS-enabled storage pool so GRS cannot be enabled on the storage volume. 
- **Not supported**: The site where the storage volume is created is not a GRS-supported location. So, you cannot enable replication of the storage volume.
- **Not configured**: The storage volume is in a GRS-enabled location. You can configure the storage volume for GRS.
- **Initializing**: The GRS enablement of the storage volume is in progress.
- **Configured**: The storage volume is a GRS-enabled storage volume.


For more information, see [Creating a storage volume](/docs/power-iaas?topic=power-iaas-modifying-instance#create-storage-vol).


The following table explains how to determine the primary and secondary site based on replication-enabled volume creation:

|Replication-enabled volume creation site|Primary site (primary volume)|Secondary site (auxiliary volume)|
|-------------------------------------|----------------------------|---------------------------------|
|Site 1|Site 1|Site 2|
|Site 2|Site 2|Site 1|
{: class="simple-table"}
{: caption="Primary and secondary site reference based on volume creation" caption-side="bottom"}








## {{site.data.keyword.powerSys_notm}} regions that support GRS
{: #locations-GRS}

You can use the GRS location APIs to determine the locations that support storage replication and their mapped location. For more information, see [all disaster recovery locations that are supported by {{site.data.keyword.powerSys_notm}}](/apidocs/power-cloud#pcloud-locations-disasterrecovery-getall) in API documentation.

The following table shows the location pairs that support replication pairs:




| Location 1        | Location 2               |
| ----------------- | ------------------------ |
| `mad02`           | `eu-de-1 (fra04)`        |
| `mad04`           | `eu-de-2 (fra05)`        |
| `us-east (wdc04)` | `us-south (dal13)`       |
| `wdc06`           | `dal12`                   |
| `wdc06`           | `dal14`                  |
| `wdc07`           | `dal10`                  |
| `osa21`           | `tok04`                  |
| `syd04`           | `syd05`                  |
| `sao01`           | `sao04`                  |
| `mon01`           | `tor01`                  |
| `lon04`           | `lon06`                  |
{: class="simple-table"}
{: caption="Replication-enabled {{site.data.keyword.powerSys_notm}} region pairs" caption-side="bottom"}





## Preparation for disaster recovery
{: #dr-prep}

Consider that you have the virtual server instances with data volumes that are running workloads. If a failure occurs and if the data volumes are replicated, you can recover the data volumes from the remote site. To enable the volume replication service, complete the [actions on the primary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-primary-site) and the [actions on the secondary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-secondary-site).

### Actions on the primary site
{: #configure-primary-site}

To enable volume replication on the primary site, complete the following steps:
1. Create a replication-enabled volume by providing `replicationEnabled` flag as `True` in the [Create a new data Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post) request body.

    To know more about the replication properties of a volume, see the [FAQ](/docs/power-iaas?topic=power-iaas-powervs-faqs#convert-to-replication-vol).

2. Create a virtual server instance with replication-enabled volumes by using {{site.data.keyword.powerSys_notm}} interface.

    The boot volumes of virtual server instances that you create are always set to nonreplication-enabled. You can provide a mix of replication and nonreplication-enabled volumes for a virtual server instance if they belong to the same storage pool. All the existing storage pool affinity rules apply for replication-enabled volumes.
    {: note}

3. Create a volume group (consistency group) by using the [create a new volume group](/apidocs/power-cloud#pcloud-volumegroups-post) API with the replication-enabled volumes created before.

    Verify that the volume group is created successfully and it is in a consistent copying state by using [get storage details of the volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get) API.

### Actions on the secondary site
{: #configure-secondary-site}

To enable volume replication on the secondary site, complete the following steps:
1. Onboard the auxiliary volume by using the [onboard auxiliary volume](/apidocs/power-cloud#pcloud-volume-onboarding-post) API. For more information, see [Onboarding auxiliary volumes](#onboard-aux-vol).

2. Create a standby virtual server instance with onboarded auxiliary volumes.

    You can create a standby virtual server instance with the onboarded volumes or attach the onboarded volumes to the existing virtual server instance.

Now, you have the setup ready to enable replication service. See [Performing a failover and failback operation](/docs/power-iaas?topic=power-iaas-getting-started-GRS#perform-fail-over-back) section to understand the recovery when a site failure occurs.

## Onboarding auxiliary volumes
{: #onboard-aux-vol}

The onboard auxiliary volume is needed to manage the replicated volume on a remote site and perform volume recovery.

You must have the editor access on the source and target {{site.data.keyword.powerSys_notm}} workspaces to onboard the auxiliary volume. The source and target workspace must be owned by the same account ID.
{: note}

Collect the following information from the primary site to request for onboarding the auxiliary volumes on the secondary site:

1. Fetch the Cloud Resource Name (CRN) of the {{site.data.keyword.powerSys_notm}} workspace instance where the primary volumes are located (primary site).
2. Fetch the auxiliary volume names from **auxVolumeName** field of primary volumes from primary site for onboarding.

To perform the onboarding process, use the [onboard auxiliary volume](/apidocs/power-cloud#pcloud-volume-onboarding-post) API and provide the **CRN** and **auxVolumeName** values of the primary volumes that you want to onboard.

The onboarding operation creates a volume ID for each onboarded auxiliary volume. When the primary volume (in the primary site) is a part of a volume group, the onboarding operation creates a volume group ID for the existing volume group on the storage host. It adds the new auxiliary volume IDs to the new group ID.

Volume IDs and group ID for primary-aux volume pairs are different on primary and secondary sites. However, you can check other fields such as **materVolumeName**, **auxVolumeName**, and **consistencyGroupName** to identify a mater-aux volume pair.

The onboarding operation is an asynchronous operation that can take some time that depends upon the number of volumes. Use the [Get the information of volume onboarding operation](/apidocs/power-cloud#pcloud-volume-onboarding-get) request to check the status of the onboarding operation.

## Performing a failover and failback operation
{: #perform-fail-over-back}

To access the auxiliary volumes from the secondary site upon a primary site failure, stop the volume group by using [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post) API with **access** flag set to `True`.




To switch back to the volume group on the primary site, you must perform the volume group stop and start operations from the primary site. You can use the volume group `stop` command and wait until `ReplicationStatus` status changes to `disabled` value. Then, use the volume group `start` command with the `--source master` option to start the volume group. For more information about commands, see [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post) API.




Verify that the action that you perform on a volume group meets the current state of the volume group. Otherwise, an error message appears indicating that the volume group is not in the expected state.
{: attention}

The error message appears when you perform the following actions:
- Stop a volume group when the `ReplicationStatus` is in the `disabled` state.
- Start a volume group when the `ReplicationStatus` is in the `enabled` state or `available` state.
- Reset a volume group that is not in the error state.





## Impacts on other {{site.data.keyword.powerSys_notm}} operations
{: #impacts-on-powervs}

The impacts of GRS on other {{site.data.keyword.powerSys_notm}} operations are as follows:

- No changes in image interfaces and no replication support for images.
- No changes in the operation interface and storage pool affinity rules for virtual server instances. The replication and non-replication-enabled volumes support volume attachment and detachment.
- Snapshot and capture operations are allowed for a virtual server instance with replication and non-replication-enabled volumes when the volumes are from the same storage pool. The snapshot and capture operations are performed by using the non-replication-enabled volumes internally even though the volumes of a virtual server instance are replication-enabled.
- By default, when you clone a replication-enabled volume, the cloned volume is replication-enabled. During cloning, you can optionally specify whether the cloned volume must be replication-enabled or not. If you want the cloned volume to be replication-enabled, specify the policy for the clone volume. You can use the following methods to clone a volume:

    - [Clone a volume by using API](/apidocs/power-cloud#pcloud-v2-volumesclone-execute-post){: external}.
    - [Clone a volume by using CLI](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone){: external}.
    - [Clone a volume by using Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume_clone){: external}.

## Disabling GRS
{: #disable-grs}

If you disable the replication service on a volume, it results in the deletion of the volume on the secondary site.

To disable the replication service between the primary volume and auxiliary volume and to retain the primary volume data, complete the following procedure:

Failure to complete this procedure in the specified order might result in loss of source volume data.
{: attention}

1. **Remove the volumes from the volume group on the primary site**: On the primary site, if a volume is associated with a volume group, remove the volume from its associated volume group. Use the [ibmcloud pi volume-group update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update) CLI command to remove the volumes from the volume group.

    For example, `ibmcloud pi vgu 5bbe734a-7ec6-4f0a-a34e-8bd45fc189ca --remove-member-volume-ids afd07003-a61a-45ca-97d1-4f910272306d`

2. **Disable the volume replication service**: Disable the volume replication service by setting the `replication-enabled` flag to `False`. Use the [ibmcloud pi volume action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-action) CLI command to disable the volume replication.

    For example, `ibmcloud pi vola afd07003-a61a-45ca-97d1-4f910272306d –replication_enabled=False`

    Disabling the volume replication service is an asynchronous process. Retrieve the volume details to confirm that the volume replication service is disabled.
    {: note}

    After the volume replication service is disabled, the following changes occur:
    * The replication relationship between the primary volume and auxiliary volume is removed.
    * The auxiliary volume from the storage backend is deleted.

3. **Remove the volumes from the volume group on the secondary site**: Update the volume group of the secondary site to remove the volumes from it.

    This step is required if the volume is on-boarded into a workspace on the secondary site.
    {: note}

    Use the [ibmcloud pi volume-group update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update) CLI command to remove the volumes from the volume group.

    For example, `ibmcloud pi vgu 96e037e3-9efd-4d6d-90cf-d1f6cc76d6c3 --remove-member-volume-ids ba147c20-578a-4ae1-8a94-252b6bbcd9cb`


    When you disable the replication service on the primary volume or delete a primary volume, the replication relationship between the primary volume and the secondary volume is deleted in the storage backend. If the auxiliary volume on the secondary site is associated with a volume group, remove the auxiliary volume from the volume group. Delete the auxiliary volume manually. If the auxiliary volume is not deleted from the secondary site, an out-of-band periodic check (occurring every 24 hours) sets the auxiliary volume to an error state.
    {: note}



## Updating a primary volume
{: #update-prime-vol}

You can resize the primary volume or switch the bootable or shareable options of the volume as `True` or `False`.


Use the [ibmcloud pi volume-update](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-update) CLI command with the following options to update the primary volume:

- **Resize** `--size NEW_SIZE` option: On `DAL10` and `WDC07` location pair, when you resize a replication-enabled primary volume from the primary site, the system resizes the associated auxiliary volume on its corresponding remote site within 24 hours. For all other location pairs, before you resize a replication-enabled volume, remove the volume from the volume group. After the volume resize is completed, add the volume back to the volume group.

    It is recommended not to resize a primary volume by disabling replication as it results in errors that are related to the auxiliary volume on the remote site.
    {: important}

- **Bootable** `bootable=true` option: To set a primary volume as a boot volume, update the `bootable` attribute to `True`.

- **Sharable** `shareable=true` option: To set a primary volume as a shareable volume, update the `sharable` attribute to `True`.

    If you are setting the `bootable` and `shareable` options to `True` on the primary volume, you must explicitly set the `bootable` and `shareable` options to `True` on the auxiliary volume.
    {: note}


## Deleting a primary volume
{: #delete-prime-vol}

To delete a volume or a replication-enabled primary volume, the status of the storage volume must indicate one of the following states: `available`, `error`, `error_restoring`, `error_extending`, or `error_managing`. Also, the storage volume cannot be deleted if it is in the state of migrating, attached, belongs to a group, has snapshots, or is disassociated from its snapshots after a transfer.

Once you initiate the action to delete the volume, the action cannot be undone.
{: note}

To delete a primary volume, complete the following steps:



1. Remove the primary volume from the volume group, if the primary volume is associated with a volume group.
2. Delete the primary volume from the primary site. You can use the CLI command [ibmcloud pi volume-delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-delete) to delete the volume.
3. Remove the auxiliary volume from the volume group, if the auxiliary volume is associated with a volume group.
4. Delete the auxiliary volume from the secondary site.

When you disable the replication service on the primary volume or delete a primary volume, the replication relationship between the primary volume and the secondary volume is deleted in the storage backend. If the auxiliary volume on the secondary site is associated with a volume group, remove the auxiliary volume from the volume group. Delete the auxiliary volume manually. If the auxiliary volume is not deleted from the secondary site, an out-of-band periodic check (occurring every 24 hours) sets the auxiliary volume to an error state.

When you delete a primary volume, the billing for primary volume stops.

In the following example, `afd07003-a61a-45ca-97d1-4f910272306d` is a primary volume that is associated with the volume group `5bbe734a-7ec6-4f0a-a34e-8bd45fc189ca`:

1. Remove the volume from volume group on the primary site. You can use the following CLI command:

        ibmcloud pi volume group update 5bbe734a-7ec6-4f0a-a34e-8bd45fc189ca --remove-member-volume-idsmafd07003-a61a-45ca-97d1-4f910272306d

2. Delete the primary volume from primary site. You can use the following CLI commands:

        ibmcloud pi vol delete afd07003-a61a-45ca-97d1-4f910272306d

3. Remove the auxiliary volume from volume group on the secondary site. You can use the following CLI command:

        ibmcloud pi volume group update 96e037e3-9efd-4d6d-90cf-d1f6cc76d6c3 --remove-member-volume-ids ba147c20-578a-4ae1-8a94-252b6bbcd9cb

4. Delete the auxiliary volume from the secondary site. You can use the following CLI commands:

        ibmcloud pi vol delete ba147c20-578a-4ae1-8a94-252b6bbcd9cb





## Deleting an auxiliary volume
{: #del-aux-vol}

If you delete an auxiliary volume, the associated primary volume is also deleted.
{: caution}

When you disable the replication service on the primary volume or delete a primary volume, the replication relationship between the primary volume and the secondary volume is deleted in the storage backend. If the auxiliary volume on the secondary site is associated with a volume group, remove the auxiliary volume from the volume group. Delete the auxiliary volume manually. If the auxiliary volume is not deleted from the secondary site, an out-of-band periodic check (occurring every 24 hours) sets the auxiliary volume to an error state.

Use the [ibmcloud pi volume delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-delete) CLI command to delete the auxiliary volume.

For example, `ibmcloud pi vold afd07003-a61a-45ca-97d1-4f910272306d`


## Creating a volume group
{: #create-vol-grp}

When you create a volume group and add the replication-enabled volumes to the volume group, the remote replication consistency group is created at both primary and remote storage backend. The consistency group stores the consistent copy for the volumes. When the volume group is created, the primary role attribute is set as `master`.

You can add only replication-enabled volumes to a volume group. If you try to add a non-replication-enabled volume to a volume group, the action fails.

To create a volume group, you can use the CLI command, [ibmcloud pi volume-group-create](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-create){: external}.


### Updating a volume group
{: #update-vol-grp}

You can add or remove storage volumes from a volume group. After onboarding primary volumes, if you add storage volumes to a volume group on the primary site after the primary volumes, you must onboard the associated auxiliary volumes on the secondary site. If you remove the storage volumes from a volume group on the primary site after the onboarding operation, then you must also remove the associated auxiliary volumes from the secondary site.

To update a volume group, you can use the CLI command, [ibmcloud pi volume-group-update](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-volume-group-update){: external}.




## Limitations of GRS
{: #limitations-GRS}

The limitations of GRS are as follows:


- After you performed a failback operation, the replication role of the volume group (VG) and the volume fail to change from auxiliary to primary. The issue is a recurring issue that impacts your GRS environments.
- You cannot perform a snapshot-restore operation on auxiliary volumes.
- The volume group update operation can fail upon a mismatch in the volume group and volume replication states. If the volume group is in an error state, use the [volume group action](/apidocs/power-cloud#pcloud-volumegroups-action-post) API to reset the volume group status.

- When you disable the replication service on the primary volume or delete a primary volume from the primary site, the following changes occur:

    - The replication relationship between the primary volume and the auxiliary volume is deleted at the storage backend.
    - If the auxiliary volume is not deleted from the secondary site manually, an out-of-band periodic check (occurring every 24 hours) sets the auxiliary volume to an error state.

- You cannot remove the replication-enabled volume when it is a part of a volume group.
- On `DAL10` and `WDC07` location pair, when you resize a replication-enabled primary volume from the primary site, the system resizes the associated auxiliary volume on its corresponding remote site within 24 hours. For all other location pairs, before you resize a replication-enabled volume, remove the volume from the volume group. After the volume resize is completed, add the volume back to the volume group. For more information, see [Updating a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#update-prime-vol).
- If you resize a primary volume by disabling replication service on the primary site, it results in errors that are related to the auxiliary volume on the remote site.
- Any operation that is performed on a deleted volume fails.




## Best practices for GRS
{: #best-practices-GRS}

- Set the **Shareable** and **Bootable** flag explicitly on onboarded volumes, if required.
- Start the onboarding of auxiliary volumes only when the primary volumes and volume group are in a consistent copying state. You can get the volume details by using the [get volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-get){: external} API to determine the state of the primary volumes and volume group in the mirroring state on the primary site. Verify that the volume group is created successfully and it is in a consistent copying state by using [get storage details of the volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get){: external} API.
* Get volume details by using the following methods:
    * [Power Cloud API](/apidocs/power-cloud#pcloud-cloudinstances-volumes-get){: external}.
    * [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume){: external}.
* Get volume groups storage details by using the following methods:
    * [Power Cloud API](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get){: external}.
    * [Power Virtual Server CLI](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-storage-details){: external}
    * [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pi_volume_group_storage_details){: external}.

- When you add or remove a primary or an auxiliary volume from a volume group from one site, perform the same operation from the other site to keep the data in sync.
- Delete the volumes from primary and secondary site. Volumes are charged when you delete an auxiliary volume but fail to delete the primary volume.
- Use primary site for all the volume operations and perform operations on auxiliary volume on the secondary site only during failover.
