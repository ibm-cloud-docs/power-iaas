---

copyright:
  years: 2024

lastupdated: "2024-08-26"

keywords: Global Replication Services, GRS, configure GRS, pricing for GRS, GRS APIs,

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Global Replication Services (GRS)
{: #getting-started-GRS}

---

IBM {{site.data.keyword.powerSys_notm}} located in IBM data centers: [Off-premises]{: tag-blue}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

---

Disasters are unplanned events that cause severe damage, incur a loss to our business, and affect all organizations. Since most workloads run on cloud infrastructure nowadays, it is essential to have robust and resilient cloud infrastructure prepared to handle these catastrophic hits and have minimal impact on business.
{: shortdesc}

The {{site.data.keyword.powerSysFull}} provides a set of APIs to enable disaster recovery (DR) solution for your virtual server instances. IBM Cloud infrastructure internally uses Global Mirror Change Volume (GMCV) as storage technology that provides asynchronous replication, and advanced network configuration for fast data transfer.

A new resource volume group is introduced to enable, disable, and manage storage replication consistency group. The volume group holds the volumes that need to be recovered at the time of disaster. Make the volume DR capable by adding the volume to the volume group. To trigger failover and failback operations, use the volume group start and stop operations.

GRS aims to automate the complete DR solution and provide the API and CLI interfaces to create the recipe for the DR solution. GRS currently does not have any user interface.

The scope of the GRS service is to create and manage replicated resources that include the following items:
- Volume lifecycle operations support on replicated volumes.
- APIs to manage volume groups through create, update, delete, start, and stop operations.
- Virtual server instance lifecycle operations by using replicated volumes.
- Onboard auxiliary volume on secondary site for volume recovery.

## Additional information
{: #additional-info-GRS}

If you need a more detailed information on Global Replication Services, see [Global Replication Services Solution by using IBM Power Virtual Server](https://cloud.ibm.com/media/docs/downloads/power-iaas/Global_Replication_Services_Solution_using_IBM_Power_Virtual_Server.pdf){: external}

## Pricing for GRS
{: #pricing-GRS}

The charges for GRS depend on the location where you create a replication-enabled volume.

Replication-enabled volumes incur the following charges:

- A base charge for the replication capability is based on the size of the replication-enabled volume under the part number "GLOBAL_REPLICATION_STORAGE_GIGABYTE_HOURS".
- The charges for replication-enabled volumes are two times the size of the volume against the storage part numbers based on the tier of the volume against the primary volume.

    Auxiliary volumes are not charged separately and are part of the primary volume charges.
    {: note}

Upon a site failure due to a catastrophe, metering becomes unavailable from the failed site. The charges for replication-enabled volumes are charged from remote site and the charges are two times the size of the volume against the storage part numbers based on the tier of the volume. During this time, the base charge for the replication capability for the replication-enabled volumes is not charged.

## Setting up GRS
{: #configure-GRS}

GRS involves two sites where storage replication is enabled. These two sites are fixed and mapped into one-to-one relationship mode in both directions. These two sites are fixed and are in replication partnership in both directions.

You can create a replication-enabled volume from any site, the site from where the request is initiated contains the primary volume. The remote site is auxiliary and contains an auxiliary volume.

The following table explains how to determine the primary and secondary site based on replication-enabled volume creation:

|Replication-enabled volume creation site|Primary site (primary volume)|Secondary site (auxiliary volume)|
|-------------------------------------|----------------------------|---------------------------------|
|Site 1|Site 1|Site 2|
|Site 2|Site 2|Site 1|
{: class="simple-table"}
{: caption="Table 2. Primary and secondary site reference based on volume creation" caption-side="bottom"}

## {{site.data.keyword.powerSys_notm}} regions that support GRS
{: #locations-GRS}

You can use the GRS location APIs to determine the locations that support storage replication and their mapped location. For more information, see [all disaster recovery locations that are supported by {{site.data.keyword.powerSys_notm}}](/apidocs/power-cloud#pcloud-locations-disasterrecovery-getall) in API documentation.

The following table shows the location pairs that support replication:
| Location 1        | Location 2               |
| ----------------- | ------------------------ |
| `mad02`           | `eu-de-1 (fra04)`        |
| `mad04`           | `eu-de-2 (fra05)`        |
| `us-east (wdc04)` | `us-south (dal13)`       |
| `wdc06`           | `dal12`                  |
| `wdc07`           | `dal10`                  |
| `osa21`           | `tok04`                  |
| `syd04`           | `syd05`                  |
| `sao01`           | `sao04`                  |
| `mon01`           | `tor01`                  |
{: class="simple-table"}
{: caption="Table 1. Replication enabled {{site.data.keyword.powerSys_notm}} region pairs" caption-side="bottom"}

## Preparation for disaster recovery
{: #dr-prep}

Consider that you have the virtual server instances with data volumes that are running workloads. If a failure occurs and if the data volumes are replicated, you can recover the data volumes from the remote site. To enable the DR, perform [actions on the primary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-primary-site) and [actions on the secondary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-secondary-site).

### Actions on the primary site
{: #configure-primary-site}

To enable DR on the primary site, complete the following steps:
1. Create a replication-enabled volume by providing `replicationEnabled` flag as `True` in the [Create a new data Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post) request body.

    To know more about the replication properties of a volume, see the [FAQ](/docs/power-iaas?topic=power-iaas-powervs-faqs#convert-to-replication-vol).

2. Create a virtual server instance with replication-enabled volumes by using {{site.data.keyword.powerSys_notm}} interface.

    The boot volumes of virtual server instances that you create are always set to nonreplication-enabled. You can provide a mix of replication and nonreplication-enabled volumes for a virtual server instance if they belong to the same storage pool. All the existing storage pool affinity rules apply for replication-enabled volumes.
    {: note}

3. Create a volume group (consistency group) by using the [create a new volume group](/apidocs/power-cloud#pcloud-volumegroups-post) API with the replication-enabled volumes created before.

    Verify that the volume group is created successfully and it is in a consistent copying state by using [get storage details of the volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get) API.

### Actions on the secondary site
{: #configure-secondary-site}

To enable DR on the secondary site, complete the following steps:
1. Onboard the auxiliary volume by using the [onboard auxiliary volume](/apidocs/power-cloud#pcloud-volume-onboarding-post) API. For more information, see [Onboarding auxiliary volumes](#onboard-aux-vol).

2. Create a standby virtual server instance with onboarded auxiliary volumes.

    You can create a standby virtual server instance with the onboarded volumes or attach the onboarded volumes to the existing virtual server instance.

Now you have the setup ready for DR. See [Performing a failover and failback operation](/docs/power-iaas?topic=power-iaas-getting-started-GRS#perform-fail-over-back) section to understand the recovery when a site failure occurs.

## Onboarding auxiliary volumes
{: #onboard-aux-vol}

The onboard auxiliary volume is required to manage the replicated volume on a remote site and perform volume recovery.

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

To access the auxiliary volumes from the secondary site upon a primary site failure, stop the volume group by using [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post)] API with **access** flag set to `True`.

When the site is back, you can start the volume group by using [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post)] API. The failback operation resumes the replication back to the primary site but any input and output that is performed on a remote site is lost.

## Impacts on other {{site.data.keyword.powerSys_notm}} operations
{: #impacts-on-powervs}

The impacts of GRS on other {{site.data.keyword.powerSys_notm}} operations are as follows:

- No changes in image interfaces and no replication support for images.
- No changes in the operation interface and storage pool affinity rules for virtual server instances. The replication and non-replication-enabled volumes support volume attachment and detachment.
- Snapshot and capture operations are allowed for a virtual server instance with replication and non-replication-enabled volumes when the volumes are from the same storage pool. The snapshot and capture operations are performed by using the non-replication-enabled volumes internally even though the volumes of a virtual server instance are replication-enabled.
- By default, when you clone a replication-enabled volume, the cloned volume is replication-enabled. During cloning, you can optionally specify whether the cloned volume must be replication-enabled or not. If you want the cloned volume to be replication-enabled, specify the policy for the clone volume. You can use the following methods to clone a volume:

    - [Clone a volume by using API](/apidocs/power-cloud#pcloud-v2-volumesclone-execute-post){: external}.
    - [Clone a volume by using CLI](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone){: external}.
    - [Clone a volume by using Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume_clone){: external}.

## Disabling GRS
{: #disable-grs}

If you disable the replication service on a volume, it results in the deletion of the volume on the secondary site.

To disable the replication service between the primary volume and auxiliary volume and to retain the primary volume data, complete the following procedure:

Failure to complete this procedure in the specified order might result in loss of source volume data.
{: attention}

1. **Remove the volumes from the volume group on the primary site**: On the primary site, if a volume is associated with a volume group, remove the volume from its associated volume group. Use the [ibmcloud pi volume-group update](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update) CLI command to remove the volumes from the volume group.

    For example, `ibmcloud pi vgu 5bbe734a-7ec6-4f0a-a34e-8bd45fc189ca --remove-member-volume-ids afd07003-a61a-45ca-97d1-4f910272306d`

2. **Disable the volume replication service**: Disable the volume replication service by setting the `replication-enabled` flag to `False`. Use the [ibmcloud pi volume action](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-volume-action) CLI command to disable the volume replication.

    For example, `ibmcloud pi vola afd07003-a61a-45ca-97d1-4f910272306d –replication_enabled=False`

    Disabling the volume replication service is an asynchronous process. Retrieve the volume details to confirm that the volume replication service is disabled.
    {: note}

    After the volume replication service is disabled, the following changes occur:
    * The replication relationship between the primary volume and auxiliary volume is removed.
    * The auxiliary volume from the storage backend is deleted.

3. **Remove the volumes from the volume group on the secondary site**: Update the volume group of the secondary site to remove the volumes from it.

    This step is required if the volume is on-boarded into a workspace on the secondary site.
    {: note}

    Use the [ibmcloud pi volume-group update](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update) CLI command to remove the volumes from the volume group.

    For example, `ibmcloud pi vgu 96e037e3-9efd-4d6d-90cf-d1f6cc76d6c3 --remove-member-volume-ids ba147c20-578a-4ae1-8a94-252b6bbcd9cb`

    After you disable the replication service, volumes no longer exist in the storage backend. If the auxiliary volume is not deleted from the secondary site, an out-of-band periodic check (occurring every 24 hours) sets the volume to an error state.
    {: note}


## Deleting an auxiliary volume
{: #resize-rep-vol}

To delete an auxiliary volume from the remote site, disable the replication service on the primary volume. Before you delete the auxiliary volume, make sure that it is not associated with any volume group.


Use the [ibmcloud pi volume delete](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-volume-delete) CLI command to delete the auxiliary volume.

For example, `ibmcloud pi vold afd07003-a61a-45ca-97d1-4f910272306d`


## Resizing a replication-enabled volume
{: #resize-rep-vol}

Before you resize a replication-enabled volume, remove the volume from the volume group. After the volume resize is completed, add the volume back to the volume group.

When you resize a volume from a site, the system also resizes the replication-enabled volume on its corresponding remote site after an interval of 24 hours.

It is recommended not to resize a volume by disabling replication as it results in errors that are related to the volume on the remote site.
{: important}


## Limitations of GRS
{: #limitations-GRS}

The limitations of GRS are as follows:

- You cannot perform a snapshot-restore operation on auxiliary volumes.
- The volume group update operation can fail upon a mismatch in the volume group and volume replication states. If the volume group is in an error state, use the [volume group action](/apidocs/power-cloud#pcloud-volumegroups-action-post) API to reset the volume group status.
- When you disable the replication of a volume or delete a volume from a site, the following changes occur:

    - If the auxiliary volume is not deleted from the secondary site, an out-of-band periodic check (occurring every 24 hours) sets the volume to an error state.
    - The remote copy relationship is deleted at the storage backend and the replicated volume is deleted on the secondary storage of the corresponding remote site.

- You cannot remove the replication-enabled volume when it is a part of a volume group.
- When you resize a volume from a site, the system also resizes the replication-enabled volume on its corresponding remote site after an interval of 24 hours. For more information, see [Resizing a replication-enabled volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#resize-rep-vol).
- Any operation that is performed on a deleted volume fails.

## Best practices for GRS
{: #best-practices-GRS}

- You must set the bootable flag explicitly on onboarded volumes, if required.
- Start the onboarding of auxiliary volumes only when the primary volumes and volume group are in a consistent copying state. You can get the volume details by using the [get volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-get){: external} API to determine the state of the primary volumes and volume group in the mirroring state on the primary site. Verify that the volume group is created successfully and it is in a consistent copying state by using [get storage details of the volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get){: external} API.
* Get volume details by using the following methods:
    * [Power Cloud API](/apidocs/power-cloud#pcloud-cloudinstances-volumes-get){: external}.
    * [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume){: external}.
* Get volume groups storage details by using the following methods:
    * [Power Cloud API](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get){: external}.
    * [Power Virtual Server CLI](https://cloud.ibm.com/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-storage-details){: external}
    * [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pi_volume_group_storage_details){: external}.

- When you add or remove a primary or an auxiliary volume from a volume group from one site, perform the same operation from the other site to keep the data in sync.
- You must delete the volumes from primary and secondary site. Volumes are charged when you delete an auxiliary volume but fail to delete the primary volume.
- You must use primary site for all the volume operations and perform operations on auxiliary volume on the secondary site only during failover.
