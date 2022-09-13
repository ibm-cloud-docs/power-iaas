---

copyright:
  years: 2022

lastupdated: "2022-09-12"

keywords: Global replication service, GRS, configure GRS, pricing for GRS, GRS APIs,  

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing Global replication service
{: #getting-started-GRS}

The {{site.data.keyword.powerSysFull}} provides a set of APIs through which you can enable disaster recovery (DR) solution for your virtual server instances. The storage replication uses the Global Mirror Change volume technology. 
{: shortdesc}

Global replication service (GRS) aims not to automate the complete DR solution end to end but to provide API and CLI interfaces to create the recipe for the DR solution.

GRS currently does not have any user interface.
{:note:}

<!-- <LBS link goes here > -->

The scope of the GRS service is to create and manage replicated resources that includes:
- Volume-based asynchronous storage replication that uses volume-groups (consistency groups).
- APIs to manage volume groups through create, update, delete, start, and stop operations.
- Volume lifecycle operations support for mirrored volumes.
- Manage virtual server instance lifecycle operations with mirrored volumes.

## Locations supporting Global replication service
{: #locations-GRS}

You can use the GRS location APIs to check about the locations that support storage replication and their mapped location. For more information, see [GRS Location API docs (dummy link)]().

## Pricing for Global replication service
{: #pricing-GRS}

Global Replication Service involves duplication of storage volumes across sites. The replication-enabled volumes are charged based on following two components:
- Volume infrastructure cost
- Replication capability cost

Two scenarios that explains how the volume infrastructure cost and replication capability cost are calculated:
- When both primary and secondary sites are up, and running
- When there is one site failure

### Pricing details when both sites are running
{: #pricing-both-sites-up}

The pricing details when both primary and secondary sites are up, and running is calculated as follows: 
- Volume infrastructure cost: When you create a replication of disk of size `X GB` on the primary site, a disk space of `2X GB` from the primary site is charged based on your tier selection. No charges are applicable for auxiliary volumes from the mapped replication site.
- Replication capability cost: You are charged `$Y/GB` for the `X GB` of the disk that is replicated from the primary site through a new part number `GLOBAL_REPLICATION_STORAGE_GIGABYTE_HOURS`.

### Pricing details of one site failure
{: #pricing-one-site-down}

Consider a scenario where one site (site 1) fails due to a catastrophe. The other site (site 2) is up and running then metering is possible from site 2 and vice versa. The pricing details for site 2 are calculated as follows:
- Volume infrastructure cost:
    - When you create a replication of disk of size `X GB` on the site 2, a disk space of `2X GB` from the site 2 is charged based on your tier selection.
    - When site 1 is down, auxiliary volumes are charged for a double size, as you do not pay for corresponding master volumes on site 1.
- Replication capability cost:  You do not pay any charge for any replication-enabled volume in the site 2 when the site 1 is down.

## Setting up the Global replication service
{: #configure-GRS}

The GRS involves two sites where storage replication is enabled. These two sites are fixed and mapped into one-to-one relationship mode in both directions.
When you create a replication-enabled volume that uses {{site.data.keyword.powerSys_notm}} APIs on site 1, then it creates two volumes in the background:
1. One volume is the master (primary) volume on the storage controller of site 1.
2. Another volume is called auxiliary volume on the connected storage controller of site 2.

    In this scenario, site 1 is the primary site as it has a master (primary) volume, and the site 2 is the secondary site with an auxiliary volume. The following table explains how the primary and secondary sites are considered concerning volume creation:

|Replication-enabled volume creation site|Primary site (master volume)|Secondary site (auxiliary volume)|
|-------------------------------------|----------------------------|---------------------------------|
|Site 1|Site 1|Site 2|
|Site 2|Site 2|Site 1|
{: class="simple-table"}
{: caption="Table 1. Primary and secondary site reference based on volume creation" caption-side="bottom"}

In addition to creating replication-enabled volumes, you must complete other actions on primary and secondary sites to enable the Disaster Recovery solution. You can check whether a volume is master or auxiliary volume. For more information, see [How can I check whether a volume is master or auxiliary volume?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#check-for-primary-vol)

## Actions on the primary site
{: #configure-primary-site}

Actions that you must do to enable GRS on the primary site are as follows:
1. Create a replication-enabled volume by using the [API request(dummy link)]().
    The new field `replicationEnabled` is true in the background to create new replication-enabled volumes when you call the API request. You can convert existing volumes to replication enabled volumes. For more information, see [How do I convert existing volumes to replication-enabled volumes?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#convert-to-replication-vol).

2. Create a virtual server instance with replication-enabled volumes by using the {{site.data.keyword.powerSys_notm}} user interface.
    You must provision a new virtual server instance by using the created replication-enabled volumes. You can also attach the replication-enabled volumes post creation of a virtual server instance.

    Boot volumes of newly created virtual server instances are always non-replication enabled.
    {:note}

    You can provide a mix of replication and non-replication-enabled volumes for a virtual server instance if they belong to the same storage pool. All the existing storage pool affinity rules also apply for replication-enabled volumes.

3. Create a volume group (consistency group) with the replication-enabled volumes by using the [API request(dummy link)]().
    A new resource, `volume group`, is introduced in {{site.data.keyword.powerSys_notm}} to manage the consistency groups. You can create or update multiple volume groups with multiple volumes based on your requirement. 

    You can add volumes to a volume group before or after attaching the volumes to a virtual server instance. The attached volumes of a virtual server instance can also belong to different volume groups.

## Actions on the secondary site
{: #configure-secondary-site}

Actions that you must do to enable GRS on the secondary site are as follows:
1. Onboard the auxiliary volume by using the [API request(dummy link)](). For more information about onboarding, see [Onboarding auxiliary volumes](/docs/power-iaas?topic=power-iaas-getting-started-GRS#onboarding-auxiliary-volumes).
    Collect the auxiliary volume names from the primary site and onboard them to manage from secondary sites. This operation provides the new volumes IDs and volume-group IDs (if applicable). The volume IDs and volume-group IDs help to manage the failover and failback operations.

2. Create a standby virtual server instance with onboarded auxiliary volumes by using the [API request(dummy link)]().
    You can create a standby virtual server instance with onboarded volumes or attach the onboarded volumes to the existing virtual server instance.
    
3. Stop and Start volume groups to enable failover and failback operations by using the volume group [action API(dummy link)](). For more information about failover and failback, see [Perform a failover and failBack operation(dummy link)]().

## Onboarding auxiliary volumes
{: #onboard-aux-vol}

The auxiliary volumes exist on the storage controller of the secondary site that you can onboard in the Power System Virtual Server workspace to manage them from the secondary site. Collect the following information from the primary site and enter them in the onboarding request to onboard the auxiliary volumes:
1. Fetch the CRN of the {{site.data.keyword.powerSys_notm}} workspace instance where the master volumes are located (primary site). 
2. Fetch the names from **auxVolumeName** field of master volumes from primary site to onboard a list of names of auxiliary volume. 

Onboard operation is an asynchronous operation that can take some time, depending upon the number of volumes. You can use [GetOnboarding API(dummy link)]() to check the status of the operation.

The onboarding operation creates a new volume ID for each onboarded auxiliary volume.
When the master volume (in primary site) is a part of a volume group, the onboarding operation creates a new volume group ID for the existing volume group on the storage host. It adds the new auxiliary volume IDs to the new group ID.

Volume IDs and group ID for master-aux volume pair are different on primary and secondary sites. However, you can check other fields such as **materVolumeName**, **auxVolumeName**, and **consistencyGroupName** to identify mater-aux volume pair.
{: Note}

## Perform a failover and failback operation
{: #perform-fail-over-back}

You can do a failover by stopping volume-group with access as true. This action provides read access to volumes from the secondary site that makes the volumes accessible from the secondary site.

You can start a volume group with master volume as auxiliary to switch roles that enable input and output operation for current workloads.

You can do a failback operation by switching the volume group role back to primary. Perform the following steps to do a failback operation:
1. Stop the volume group.
2. Start the volume group with primary as `master`.

## Impacts on other {{site.data.keyword.powerSys_notm}} operations
{: #impacts-on-powervs}

The impacts on other {{site.data.keyword.powerSys_notm}} operations due to global replication service are as follows:

- No changes in image interfaces and no replication support for images.
- No changes in the operation interface and storage pool affinity rules for virtual server instances. The replication and non-replication-enabled volumes now support volume attachment and detachment.
- Snapshot and capture are allowed for a virtual server instance with replication and non-replication-enabled volumes when the volumes are from the same storage pool. The snapshot and capture is done by using the non-replication-enabled volumes internally even though the volumes of a virtual server instance are replication-enabled.
- The cloned volumes are replication-enabled when the source volume is replication-enabled.

## Limitations of Global replication service
{: #limitations-GRS}

The limitations of GRS are as follows:

- You cannot perform a snapshot restore in auxiliary volumes as it is not allowed.
- The update volume-group operation can fail upon a mismatch in volume-group and volume replication states. If the volume group is in an error state, then the user can use the volume-group action API to reset the volume group status for availability.
- When you switch the volume-group role, it can take a few minutes (max 5 minutes) to update the primary role for the remote volume.
- Some fields of volume and volume group on the secondary site might not match with actual storage host data when you perform `outofband` operations on the primary site. You can use volume group storage details and volume remote copy APIs to check the actual data.
- `OutOfBand` operations like volume resize and deletion are reflected on the storage host of the remote site usually in few minutes. However, it can take longer, maximum one day, to sync across the upper software stack of {{site.data.keyword.powerSys_notm}} on the remote site.
- All volume operations are allowed except when the volume is a part of a volume group, such as extending volume size.

## Best practices for Global replication service
{: #best-practices-GRS}

- You must set the bootable flag explicitly on onboarded volumes if required.
- Start the onboarding of auxiliary volumes only when the master volumes and volume-group are in `consistent_copying` state.
- When you add or remove a master or auxiliary volume from a volume-group from one site then, you must perform the same operation from other site to keep the data is in sync.
- It is recommended to delete the volumes from primary and secondary site. Volume is charged when auxiliary volume is deleted but not the master volume.