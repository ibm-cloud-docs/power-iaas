---

copyright:
  years: 2024

lastupdated: "2024-06-05"

keywords: Global replication service, GRS, configure GRS, pricing for GRS, GRS APIs,  

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Global Replication Service
{: #getting-started-GRS}

Disasters are unplanned events that cause severe damage, incur a loss to our business, and affect all organizations. Since most workloads nowadays run on cloud infrastructure, it’s essential to have robust and resilient cloud infrastructure that is prepared to handle these catastrophic hits and have minimal impact on business.
{: shortdesc}

The {{site.data.keyword.powerSysFull}} provides a set of APIs that can enable disaster recovery (DR) solution for your virtual server instances. IBM Cloud infrastructure internally uses Global Mirror Change Volume (GMCV) as storage technology that provides asynchronous replication, and advance network configuration for fast data transfer.

A new resource volume group is introduced to enable, disable, and manage storage replication consistency group. Volume group holds the set of volumes that needs to be recovered at the time of disaster. To make the volume DR capable, you must add the volume in the volume group. Failover and failback operations are triggered by using the volume group start and stop operations. 

GRS aims to automate the complete DR solution and provide the API and CLI interfaces to create the recipe for the DR solution. GRS currently does not have any user interface.

The scope of the GRS service is to create and manage replicated resources that include the following items:
- Volume lifecycle operations support on replicated volumes.
- APIs to manage volume groups through create, update, delete, start, and stop operations.
- Virtual server instance life-cycle operations by using replicated volumes.
- Onboard auxiliary volume on secondary site for volume recovery.

## Additional information
{: #additional-info-GRS}

If you need a more detailed information on Global Replication Service, see [Global Replication Services Solution by using IBM Power Virtual Server](https://cloud.ibm.com/media/docs/downloads/power-iaas/Global_Replication_Services_Solution_using_IBM_Power_Virtual_Server.pdf){: external}

## Pricing for Global replication service
{: #pricing-GRS}

When you create a replicated-enabled volume, GRS creates the following four copies of volumes in the storage backend for the replication relationship:
- Master volume on primary site
- Master change volume on primary site to store changes
- Auxiliary volume on secondary site
- Auxiliary change volume on secondary site to store changes.

You are charged from the location where you create a replication-enabled volume. No charges for the auxiliary volume from the remote site.

The volume of size `X GB` is charged based on following two components:
- The master volume is charged 2x size based on its Tier under the existing part numbers for Tier 1 and Tier 3.
- Replication capability cost is charged $Y/GB under a new part number "GLOBAL_REPLICATION_STORAGE_GIGABYTE_HOURS" that is independent of volume tier.

Upon a site failure due to a catastrophe, metering is not available from the failed site. The auxiliary volumes are charged from remote site for its 2x size based on its tier. No replication capability cost for any replication-enabled volume.

## Setting up the Global replication service
{: #configure-GRS}

The GRS involves two sites where storage replication is enabled. These two sites are fixed and mapped into one-to-one relationship mode in both directions. These two sites are fixed and are in replication partnership in both directions. 

You can create a replication-enabled volume from any site, the site from where the request is initiated contains the master volume and play the role of master. The remote site is auxiliary and contains an auxiliary volume.

The following table explains how to determine the primary and secondary site based on replication-enabled volume creation:

|Replication-enabled volume creation site|Primary site (master volume)|Secondary site (auxiliary volume)|
|-------------------------------------|----------------------------|---------------------------------|
|Site 1|Site 1|Site 2|
|Site 2|Site 2|Site 1|
{: class="simple-table"}
{: caption="Table 2. Primary and secondary site reference based on volume creation" caption-side="bottom"}

## Locations that support global replication service
{: #locations-GRS}

You can use the GRS location APIs to determine the locations that support storage replication and their mapped location. For more information, see [all disaster recovery locations that are supported by {{site.data.keyword.powerSys_notm}}](/apidocs/power-cloud#pcloud-locations-disasterrecovery-getall).

The following table shows the data centers that support replication and their corresponding pool level detail:
| Site 1 |  Site 2 |
|--------|---------|
| `MAD02`| `FRA04` |
| `MAD04`| `FRA05` |
| `WDC04`| `DAL13` |
| `WDC06`| `DAL12` |
| `WDC07`| `DAL10` |
{: class="simple-table"}
{: caption="Table 1. Replication enabled data center and their supported storage pool" caption-side="bottom"}

## Preparation for disaster recovery
{: #dr-prep}

When you have the virtual server instances with data volume running workloads, you can ensure that your data volumes are replicated and can be recovered from the remote site, in case of failure by performing [actions on primary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-primary-site) and [secondary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-secondary-site).

### Actions on the primary site
{: #configure-primary-site}

To enable DR on the primary site, complete the following steps:
1. Create a replication-enabled volume by providing `replicationEnabled` flag as `True` in the [Create a new data Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post) request body.
    
    To know more about the replication properties of a volume, see the [FAQ](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#convert-to-replication-vol).

2. Create a virtual server instance with replication-enabled volumes by using {{site.data.keyword.powerSys_notm}} interface.
    
    The boot volumes of virtual server instances that you create are always set to non-replication enabled. You can provide a mix of replication and non-replication-enabled volumes for a virtual server instance if they belong to the same storage pool. All the existing storage pool affinity rules apply for replication-enabled volumes.
    {: note}

3. Create a volume group (consistency group) by using the [create a new volume group](/apidocs/power-cloud#pcloud-volumegroups-post) API with the replication-enabled volumes created before. 

    Verify that the volume group is created successfully and it is in a consistent copying state by using [get storage details of the volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get) API.

### Actions on the secondary site
{: #configure-secondary-site}

To enable DR on the secondary site, complete the following steps:
1. Onboard the auxiliary volume by using the [onboard auxiliary volume](/apidocs/power-cloud#pcloud-volume-onboarding-post) API. 
    
    For more information about onboarding operation, see [Onboarding auxiliary volumes](/docs/power-iaas?topic=power-iaas-getting-started-GRS#onboarding-auxiliary-volumes).

2. Create a standby virtual server instance with onboarded auxiliary volumes.
    
    You can create a standby virtual server instance with onboarded volumes or attach the onboarded volumes to the existing virtual server instance.
    
Now you have the setup ready for DR. See [Performing a failover and failback operation](/docs/power-iaas?topic=power-iaas-getting-started-GRS#perform-fail-over-back) section to understand the recovery when a site failure occurs.

## Onboarding auxiliary volumes
{: #onboard-aux-vol}

The onboard auxiliary volume is required to manage the replicated volume on a remote site and perform volume recovery.

You must have the editor access on the source and target {{site.data.keyword.powerSys_notm}} workspaces to onboard the auxiliary volume. The source and target workspace must be owned by the same account ID.
{: note} 

Collect the following information from the primary site to request for onboarding the auxiliary volumes on the secondary site:
1. Fetch the Cloud Resource Name (CRN) of the {{site.data.keyword.powerSys_notm}} workspace instance where the master volumes are located (primary site). 
2. Fetch the auxiliary volume names from **auxVolumeName** field of master volumes from primary site for onboarding.

The onboarding operation creates a volume ID for each onboarded auxiliary volume. When the master volume (in the primary site) is a part of a volume group, the onboarding operation creates a volume group ID for the existing volume group on the storage host. It adds the new auxiliary volume IDs to the new group ID.

Volume IDs and group ID for master-aux volume pairs are different on primary and secondary sites. However, you can check other fields such as **materVolumeName**, **auxVolumeName**, and **consistencyGroupName** to identify a mater-aux volume pair.

The onboarding operation is an asynchronous operation that can take some time that depends upon the number of volumes. Use the [Get the information of volume onboarding operation](/apidocs/power-cloud#pcloud-volume-onboarding-get) request to check the status of the onboarding operation.

## Performing a failover and failback operation
{: #perform-fail-over-back}

When you want to access the auxiliary volumes from the secondary site upon a primary site failure, stop the volume-group by using [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post)] API with **access** flag as true.

When the site is back, you can start the volume group by using [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post)] API. The failback operation resumes the replication back to the primary site. Any input and output that is performed on a remote site is lost.

## Impacts on other {{site.data.keyword.powerSys_notm}} operations
{: #impacts-on-powervs}

The impacts of global replication service on other {{site.data.keyword.powerSys_notm}} operations are as follows:

- No changes in image interfaces and no replication support for images.
- No changes in the operation interface and storage pool affinity rules for virtual server instances. The replication and non-replication-enabled volumes support volume attachment and detachment.
- Snapshot and capture operations are allowed for a virtual server instance with replication and non-replication-enabled volumes when the volumes are from the same storage pool. The snapshot and capture operations are performed by using the non-replication-enabled volumes internally even though the volumes of a virtual server instance are replication-enabled.
- The cloned volumes are replication-enabled when the source volume is replication-enabled.

## Limitations of Global replication service
{: #limitations-GRS}

The limitations of GRS are as follows:

- You cannot perform a snapshot restore operation in auxiliary volumes.
- The volume-group update operation can fail upon a mismatch in volume-group and volume replication states. If the volume group is in an error state, you can use the volume-group action API to reset the volume group status for availability.
- When you delete a volume from a site, the replicated volume that is managed on its corresponding remote site moves to an error state in an interval of 24 hours.
- When the volume is resized from a site, the replicated-enabled volume on its corresponding remote site is also resized after an interval of 24 hours.
- When you perform any operation on a volume that is deleted, it fails.

## Best practices for Global replication service
{: #best-practices-GRS}

- You must set the bootable flag explicitly on onboarded volumes, if required.
- Start the onboarding of auxiliary volumes only when the master volumes and volume-group are in a consistent copying state.
- When you add or remove a master or auxiliary volume from a volume-group from one site, you must perform the same operation from other site to keep the data is in sync.
- You must delete the volumes from primary and secondary site. Volumes are charged when you delete an auxiliary volume but fail to delete the master volume.
- You must use primary site for all the volume operations and perform operations on auxiliary volume on the secondary site only during failover.
