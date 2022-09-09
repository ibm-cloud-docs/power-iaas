---

copyright:
  years: 2022

lastupdated: "2022-09-08"

keywords: Global replication service, GRS, configure GRS, pricing for GRS, GRS APIs,  

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with Global replication service
{: #getting-started-GRS}

The {{site.data.keyword.powerSysFull}} provides a set of APIs through which you can enable disaster recovery (DR) solution for your virtual server instances . The storage replication uses the Global Mirror Change volume technology. 
{: shortdesc}

Global replication service (GRS) aims not to automate the complete DR solution end to end but to provide API and CLI interfaces to create the recipe for the DR solution.

GRS currently does not have any user interface.
{:note:}

<!-- <LBS link goes here > -->

The scope of the GRS service is to create and manage replicated resources that includes the following:
- Volume-based asynchronous storage replication using volume-groups (consistency groups).
- APIs to manage volume groups by performing create, update, delete, start, and stop operations.
- Volume lifecycle operations support for mirrored volumes.
- Virtual server lifecycle operations that have mirrored volumes.

## Locations supporting Global replication service

{: locations-GRS}

You can use the GRS location APIs to check about the locations that supports storage replication and their mapped location. For more information, see [GRS Location API docs (dummy link)]().

## Pricing for Global replication service

{:pricing-GRS}
Global Replication Service involves duplication of storage volumes across sites. The replication enabled volumes are charged based on following two components:
1. When both primary and secondary sites are up, and running.
2. When one site is up, and running.

### Pricing details when both sites are up, and running
{:pricing-both-sites-up}

The pricing details when both primary and secondary sites are up, and running is calculated as follows: 
- Volume infrastructure cost: When you create a replication of disk(s) of size `X GB` on the primary site, a disk space of `2X GB` from the primary site is charged based on your tier selection. No charges are applicable for auxiliary volumes from the mapped replication site.
- Replication capability cost: You are charged `$Y/GB` for the `X GB`  of the disk replicated from the primary site through a new part number `GLOBAL_REPLICATION_STORAGE_GIGABYTE_HOURS`.

### Pricing details when one sites is down
{:pricing-one-site-down}

Consider a scenario where the site 1 is down, and site 2 is up and running then metering is possible from site 2 and vice versa. The pricing details for site 2 is calculated as follows:
- Volume infrastructure cost:  
    - When you create a replication of disk(s) of size `X GB` on the site 2, a disk space of `2X GB` from the site 2 is charged based on your tier selection. 
    - When site 1 is down, auxiliary volumes are charged for a double size, as you do not pay for corresponding master volumes on site1.
- Replication capability cost:  You do not pay any charge for any replication-enabled volume in the site 2 when the site 1 is down.

## Configuring the Global replication service
{configure-GRS}

The GRS involves two sites where storage replication is enabled. These two sites are fixed and mapped into one-to-one relationship mode in both directions.
When you create a replication-enabled volume using Power System Virtual Server APIs on site 1, then it creates two volumes in the background:
1. One volume is the master volume on the storage controller of site 1.
2. Another volume is called auxiliary volume on the connected storage controller of site 2.

    In this scenario, site 1 is the primary site as it has a master volume, and the site 2 is the secondary site with an auxiliary volume. The following table explains how the primary and secondary sites are created based on your creation of replication-enabled volumes.

|You create replication enabled volume|Primary site (master volume)|Secondary site (auxiliary volume)|
|-------------------------------------|----------------------------|---------------------------------|
|Site 1|Site 1|Site 2|
|Site 2|Site 2|Site 1|
{: class="simple-table"}
{: caption="Table 1. Scenario that explains how primary and secondary site is created" caption-side="bottom"}

In addition to creating replication-enabled volumes, there are other actions that you must do on primary and secondary sites to configure the GRS.

## Configuring the primary site
{: configure-primary-site}

Configure the primary site with the following steps:
1. Create a replication enabled volumes using the [API request(dummy link)]().
    The new field `replicationEnabled` is true in the background to create new replication-enabled volumes when you call the API request.

2. Create a virtual server instance with replication-enabled volumes using the {{site.data.keyword.powerSys_notm}} user interface.
    You must provision a new virtual server instance using the created replication-enabled volumes. You can also attach the replication-enabled volumes after creating the virtual server instance.

    Boot volumes of newly created virtual server instances will always be non-replication enabled.
    {:note}

    You can provide a mix of replication and non-replication-enabled volumes for a virtual server instance if they belong to the same storage pool.  All the existing storage pool affinity rules also apply for replication-enabled volumes.

3. Create a volume-group (consistency group) with the desired replication enabled volumes using the [API request(dummy link)]().
    A new resource, “volume group,” is introduced in Power System Virtual Sever to support the life cycle of consistency groups.  You can create or update multiple volume groups with required volumes based on your requirement. 

    You can add volumes to a consistency group before or after attaching the consistency groups to a virtual server instance. The attached volumes of a virtual server instance can also belong to different volume groups.

## Configuring the secondary site
{: configure-secondary-site}

Configure the secondary site with the following steps:
1. Onboard the auxiliary volume using the API request.

2. Collect the auxiliary volume names from the primary site and onboard them to manage from secondary sites. 
    This operation will provide the new volumes IDs and volume-group Ids (if applicable). The volume IDs and volume-group Ids help to manage the failover and failback operations.

3. Create a standby virtual server instance that have onboarded auxiliary volumes using the API request.
    You can create a standby virtual server instance with onboarded volumes or attach the onboarded volumes to the existing virtual server instance.
    
4. Stop and Start volume groups to enable failover and failback operations using the volume-group [action API(dummy link)](). For more information about failover and failback, see [Performing a failover and failBack operation(dummy link)]().

## Onboarding auxiliary volumes
{: onboard-aux-vol}

The auxiliary volumes exist on the storage controller of the secondary site. You must use (onboard) the auxiliary volumes in the Power System Virtual Server workspace to manage them from the secondary site.

You must submit the following fields for an onboarding request:
1. Enter the CRN of the virtual server instance. 
2. Select the **auxVolumeName** indicator for a volume to get the auxiliary volume name from primary site.

Onboard operation is an asynchronous operation that can take some time, depending upon the number of volumes. You can use GetOnboarding API to check the status of the operation.

The onboarding operation creates  the following:
1. A new volume ID for auxiliary volumes.
2. When the master volume is a part of a volume group, it also creates the new volume-group ID for the existing consistency group on the storage host and add the newly created volume IDs to the group ID.

Volume ID and group ID for volume pair will differ on both sites, but consistency group name would be the same for the mater-aux volume pair.
{: Note}

## Performing a failover and failBack operation
{: perform-fail-over-back}

You can perform a failover by stopping volume-group with access as true. This action provides read access to volumes from the secondary site making the volumes accessible from the secondary site.

You can start a volume group with primary as `aux` to switch roles, enabling input and output operation for current workloads.

You can do a failback operation by switching the volume group role back to primary. You need to perform the following steps to perform a failback operation:
1. Stop the volume group.

2. Start the volume group with primary as `master`.


## Impacts on other {{site.data.keyword.powerSys_notm}} operations
{:impacts-on-powervs}

The impacts on other {{site.data.keyword.powerSys_notm}} operations due to global replication service are as follows:

1. There are no changes in image interfaces and no replication support for images.
2. There are no changes in the operation interface and storage pool affinity rules for virtual server instances. The replication and non-replication enabled volumes now support volume attachment and detachment.
3. Snapshot and capture are allowed for a virtual server instance with replication and non-replication enabled volumes if the volumes are from the same storage pool.
4. You can perform snapshots and capture a virtual server instance using non-replication enabled volumes internally though volumes of a virtual server instanceare replication enabled.
5. All volume operations are allowed except when the volume is a part of a volume group, like extending volume size.
6. Cloned volumes are replication enabled if source volume is replication enabled.
7. The cloned volumes are replication enabled when the source volume is replication enabled.




