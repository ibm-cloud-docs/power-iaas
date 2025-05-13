---

copyright:
  years: 2024

lastupdated: "2025-05-13"

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


{{site.data.keyword.powerSysFull}} supports Global Replication Services (GRS). GRS provides volume replication services based on Storage Area Network (SAN) that can be used as the foundation for building disaster recovery (DR) solutions. GRS is based on an asynchronous replication technology called IBM FlashSystem Global Mirror Change Volume (GMCV).

You can create a replication-enabled volume from the GRS-enabled location. The replication-enabled volume is considered as the primary volume. The replicated volume on the secondary location is known as the auxiliary volume.

GRS on {{site.data.keyword.powerSys_notm}} has the following benefits:

- Maintains a consistent and recoverable copy of the data at a secondary location. The copy of the data is created with minimal impact to applications at your primary location.

- Synchronizes the data between primary and secondary locations. The failover and fail back modes in the primary and secondary locations reduces the time that is required to switch back to the primary location after a planned or unplanned outage.

- Maintains redundant data centers in distant locations for fast recovery from disasters.

- Eliminates the dedicated networks that are expensive for replication and avoids bandwidth upgrades.

The GRS enablement in IBM {{site.data.keyword.powerSys_notm}} allows asynchronous replication of data between two IBM Cloud regional data centers where storage replication is enabled. The data center pairs are fixed and mapped in a one-to-one relationship mode in both directions.



## Terms and definitions
{: #GRS-terminology}


| Term               | Definition                                                                            |
|--------------------|---------------------------------------------------------------------------------------|
| Primary location   | Location where the volume is created.                                                 |
| Secondary location | Location where the auxiliary volume for replication is created.                       |
| Primary volume     | Initial instance of the replication volume at the primary location. \n This volume is visible to the user and managed by IBM {{site.data.keyword.powerSys_notm}}.    |
| Auxiliary volume   | Instance of the replicated volume at the secondary location. When the auxiliary volume is onboarded, it is visible and managed by IBM {{site.data.keyword.powerSys_notm}}.    |
| IBM Cloud Resource Names (CRNs)  | Identifiers that are assigned to uniquely identify resources within IBM Cloud.        |
{: class="simple-table"}
{: caption="Terms and definitions related to Global Replication Services" caption-side="bottom"}


## GRS in [{{site.data.keyword.on-prem}}]{: tag-red}
{: #grs-on-prem}

The GRS enablement in {{site.data.keyword.on-prem-fname}} enables asynchronous replication of data between the primary location infrastructure and the secondary location infrastructure. The two infrastructure locations have the identical set of capabilities that {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} provides.

Provide the network configuration between the primary location and the secondary location for replication, which includes the following prerequisites:

* The network bandwidth must be greater than or equal to 10 Gbps.
* The network latency must be less than or equal to 200 ms.

During the first synchronization, the entire data from primary volumes is copied to the auxiliary volumes. For subsequent synchronizations, only the changes between the two synchronization operations are copied. The effective Recovery Point Objective (RPO) depends on the capability of the underlying network throughput and the application characteristics. If the network throughput is insufficient to reach the defined RPO, then the time duration between the synchronization increases.

If the defined RPO exceeds for more than 8 hours, the IBM operations team alerts you.
{: note}

Replication is not supported between the VMs in {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} environment and {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} environment.











## Pricing for GRS
{: #pricing-GRS}

Part numbers are used for calculating the cost of GRS based on the storage tier that is associated with the primary volume. For more information, see [Pricing for Global Replication Services (GRS)](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#price-grs).


## {{site.data.keyword.powerSys_notm}} regions that support GRS
{: #locations-GRS}



The following table shows the location pairs that support replication:




| Location 1        | Location 2               |
| ----------------- | ------------------------ |
| `mad02`           | `eu-de-1 (fra04)`        |
| `mad04`           | `eu-de-2 (fra05)`        |
| `us-east (wdc04)` | `us-south (dal13)`       |
| `wdc06`           | `dal12`                  |
| `wdc06`           | `dal14`                  |
| `wdc07`           | `dal10`                  |
| `osa21`           | `tok04`                  |
| `syd04`           | `syd05`                  |
| `sao01`           | `sao04`                  |
| `mon01`           | `tor01`                  |
| `lon04`           | `lon06`                   |
{: class="simple-table"}
{: caption="Replication-enabled {{site.data.keyword.powerSys_notm}} region pairs" caption-side="bottom"}

To get a list of replication-enabled location names, use the following API or CLI commands:

- **API**: [Get the disaster recovery site details for the current location](https://cloud.ibm.com/apidocs/power-cloud#pcloud-locations-disasterrecovery-get){: external}

- **CLI**: [`ibmcloud pi disaster-recovery`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-disaster-recovery){: external}. Set the `--all-regions` flag as `true`.


Verify whether the primary and secondary locations to be used for replication are enabled for replication services and are in the list of replication-enabled pairs.
{: note}

In the following example, the `wdc07` and `dal10` data centers are in a replication-enabled pair:

```code

{
  "location": "dal10",
  "replicationSites": [
    {
      "ReplicationPoolMap": [
        {
          "remotePool": "General-Flash-92",
          "volumePool": "General-Flash-83"
        }
      ],
      "isActive": true,
      "location": "wdc07"
    }
  ]
}

```

## {{site.data.keyword.powerSys_notm}} storage pools that support GRS
{: storage-pool-grs}

You can allocate replication-enabled volumes only from storage pools that support replication. To identify the storage pools that support replication, use the following API or CLI commands:

- **API**: [Storage capacity for all available storage pools in a region](https://cloud.ibm.com/apidocs/power-cloud#pcloud-storagecapacity-pools-getall){: external}

- **CLI**: [`ibmcloud pi storage-pools`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-storage-pools){: external}


If a storage pool supports replication, the `replication-enabled` property is set to `true`.

When you create a volume that is replication-enabled, by default the volume is created within one of the storage pools that supports replication. If you want to update a volume to enable replication, ensure that you create it within a storage pool that supports replication. Otherwise, the update operation fails.


## Creating a volume group for GRS
{: #create-vol-grp}

A volume group is a {{site.data.keyword.powerSys_notm}} managed resource. By using the volume group, you can enable, disable, and manage a storage replication consistency group. The volume group contains the volumes that must be recovered at the time of disaster. You can add the replication-enabled volumes to a volume group. A replication-enabled volume can be a part of only one volume group at a time. In addition, all volumes in a volume group must be a part of the same storage pool.





When you create a volume group on the primary location, the storage replication consistency group is created in the storage backend at both primary and secondary locations. The storage replication consistency group stores the consistent copy for the volumes in the volume group. To perform any operations on the consistency group, you must perform the operation on the volume group that represents the consistency group. {{site.data.keyword.powerSys_notm}} does not directly manage the consistency group in the storage backend. A storage backend is the storage subsystem that contains the storage pool and the storage controller.

When you onboard a volume on the secondary location, if the volume group is not yet created, the volume is created and the onboarded auxiliary volume is added to it. This volume group is visible and managed by {{site.data.keyword.powerSys_notm}} on the secondary location. For more information, see [Onboarding an auxiliary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#onboarding-an-auxiliary-volume).

During the first data synchronization, the entire data from the primary volume is copied to the auxiliary volumes. For subsequent data synchronizations, only the changes between the two synchronization operations are copied. The effective Recovery Point Objective (RPO) depends on the capability of the network throughput and the application characteristics. If the network throughput is insufficient to meet the defined RPO, the duration between the data synchronization increases.

A volume group is used to enable, disable, and manage a replication-enabled consistency group in storage volumes. By using a consistency group, you can perform operations on multiple volumes instead of managing each volume individually. The consistency group has a `state` property that indicates the state of the `copy` operation of the volumes in the group.

Refer to the following table that lists different states of the replication-enabled consistency group in storage volumes.

| State  |  Description             |
| ------------------------------------- | ------------------------ |
| `inconsistent_stopped` | The primary volumes are accessible for `read` and `write` I/O operations, but the auxiliary volumes are not accessible. This state indicates that copying the data from primary to auxiliary volume is stopped. Start the `copy` operation on the auxiliary volume to make it consistent with primary volume.|
| `inconsistent_copying` | The primary volumes are accessible for `read` and `write` I/O but the auxiliary volumes are not accessible and the `copy` operation is started. This state indicates that the `copy` operation is started on the consistency group that was previously in the `inconsistent_stopped` state. |
| `consistent_copying` | The primary volumes are accessible for `read` and `write` I/O operation. The auxiliary volumes contain a consistent copy of the data on the primary volumes. The data on the auxiliary volume can become outdated and so the data must be updated with the data on the primary volume. This state indicates that copying is in progress and auxiliary volumes are updated with the current copy of the primary volumes. |
| `consistent_stopped` | The auxiliary volumes contain a consistent copy of the primary volumes, but can be outdated with the data on the primary volumes. The state indicates that the consistency group was in a `consistent_copying` state and it was stopped. |
| `idling` | The primary and auxiliary volumes are both operating in the primary role and both are accessible for `read` and `write` I/O operations. This state indicates that the data from one set of volumes is not copied to the other set of volumes in the replication pair because the replication process is disabled. |
| `idling_disconnected` | This state indicates that the volumes in the consistency group are operating in the primary role and can accept `read` and `write` I/O operations. |
| `consistent_disconnected` | This state indicates that the volumes in the consistency groups are operating in the non-primary role and you cannot perform `read` or `write` I/O operations. |
| `empty` | This state indicates that the volumes in the consistency group do not have any relationship with each other. |
{: class="simple-table"}
{: caption="Different states of storage replication consistency group and their descriptions." caption-side="bottom"}

If you perform any operation on a volume group at one location, it affects the associated volume group on the other location. For example, consider that a volume group is stopped on a primary location. After sometime, the associated volume group on the secondary location is updated to reflect the replication status of the pair in the volume group. In this case, the `replicationStatus` field displays the state of the volume group as `disabled` on both primary and secondary locations.

Before you perform any operation on a volume group at one location, confirm the replication status of both the volume groups at the primary and secondary locations.

You can group the replication-enabled volumes that are similar in function. For example, volumes that are related to a specific workload can be grouped under one volume group. When additional replication-enabled volumes are created, you can add a volume to an existing volume group with similar volumes based on the function. You can create a new volume group for the volumes if their function is not same as the existing volumes.




## Preparation for disaster recovery
{: #dr-prep}

Consider that you have virtual server instances with data volumes that are running workloads. If a failure occurs and if the data volumes are replicated, you can recover the data volumes from the secondary location. To enable the volume replication service, complete the following actions:

- [Actions on the primary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-primary-site)
- [Actions on the secondary site](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-secondary-site)

You must complete the actions on the primary site before you proceed with the actions on the secondary site.
{: note}


### Prerequisites
{: #prereq-prep-dr}

Complete the following prerequisites before you prepare a replication-enabled volume for disaster recovery (DR):

- Use the same IBM Cloud account ID to create two workspaces, each in the primary and secondary locations that supports GRS
- Ensure that two workspaces have different CRNs
- Do not define additional properties for the workspaces to denote that they contain replication-enabled volumes

### Actions on the primary site
{: #configure-primary-site}

To enable volume replication on the primary site, complete the following steps:

1. [Create a volume for replication](#create-vol-rep)
2. [Verify the replication status of the volume](#veri-vol-rep)
3. [Update an existing volume as a replication-enabled volume](#update-vol-rep-enabled)
4. [Create a volume group](#create-vol-grp)
5. [Verify the status of the volume group](#verify-vol-grp-stat)

#### Creating a volume for replication
{: #create-vol-rep}

Use {{site.data.keyword.powerSys_notm}} interface to create a virtual server instance with replication-enabled volumes.

The boot volumes of virtual server instances that you create are always set to nonreplication-enabled. You can provide a combination of replication- and nonreplication-enabled volumes for a virtual server instance if they belong to the same storage pool. All the affinity policies that are related to a storage pool are valid for replication-enabled volumes. For more information, see [Configuring affinity policies](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#affinity-pol).
{: note}

You can also create a replication-enabled volume by using the following API or CLI commands:

- **API**: [Create a new data Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post).
- **CLI**: [ibmcloud pi volume create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-create).

Set the values for the following parameters:
-  `VOLUME_ID`: Set the value to the primary volume ID
-  `--size`: Set the unit of measurement to gigabytes (GB)
-  `replicationEnabled`: Set the flag to `True`

For more information about the replication properties of a volume, see [FAQ](/docs/power-iaas?topic=power-iaas-powervs-faqs#convert-to-replication-vol).


#### Verifying the replication status of a volume
{: #veri-vol-rep}

After you create a replication-enabled volume, retrieve the details of the volume to verify the replication status of the volume. The `replicationEnabled` property must be set to `true`. The replication-enabled status might not be enabled immediately as the creation of the volume is asynchronous. Continue to monitor the state of the volume. If the volume is in the `available` state and the replication-enabled status is not yet set to `true`, update the volume to set the replication-enabled status to `true`. For more information, see [Updating a volume to be replication-enabled](#update-vol-rep-enabled).

Use the following API and CLI commands to get the replication-status of a volume:

- **API**: [List all volumes for this cloud instance](/apidocs/power-cloud#pcloud-cloudinstances-volumes-getall). Set the value of the `VOLUME_ID` parameter to the primary volume ID.
- **CLI**: [ibmcloud pi volume get](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-get). Set the value of the `VOLUME_ID` parameter to the primary volume ID.

Refer to the following table for the properties of a replication-enabled volume.

| Property               | Description |
| ---------------------- | ----------- |
| `consistencyGroupName` | Indicates the name of the consistency group when a volume is part of a volume group. |
| `masterVolumeName`     | Indicates the name of the `master` volume in the storage. The storage controller auto-generates this name. |
| `mirroringState`       | Indicates the mirrored state of the replication-enabled volume. This state is related to the current state of replication between the primary and the auxiliary volumes. For more information, see [Status of volume groups](#vol-grop-status-table). |
| `outOfBandDeleted`     | Indicates the status of the replication-enabled volume when deleted. If the replication status is `disabled` on the primary volume and the auxiliary volume on the secondary location is not deleted within 24 hours, the status of the `outOfBandDeleted` property is set to `true`. In this state, you cannot perform any actions on the primary volume. When primary volumes are in this state, they are not billed. |
| `primaryRole`          | Indicates the active volume in the primary and auxiliary volume. If this property value is set to `master`, the primary volume is the active volume where you can perform I/O operations. If this property value is set to `aux`, the auxiliary volume is the active volume where you can perform I/O operations. An inactive volume does not allow I/O operations to be performed on it. For a replication-enabled volume pair, the value of this property is the same. |
| `replicationEnabled`   | Indicates the replication status of a volume. Set to `True` if the volume is replication-enabled. |
| `replicationStatus`    | Returns the value of the replication status for a volume. If the returned value is `enabled`, the replication is active for the volume. If the returned value is `disabled`, the replication is inactive for the volume. If the returned value is `not-capable`, the volume is not replication-enabled and not associated with another volume on a different location. |
{: class="simple-table"}
{: caption="Properties of replication-enabled volume and their descriptions." caption-side="bottom"}


#### Creating a volume group
{: #create-vol-grp}

Create a volume group (consistency group) to add replication-enabled volumes to it. You can create a volume group by using the following API or CLI commands:

- **API**: [create a new volume group](/apidocs/power-cloud#pcloud-volumegroups-post)
- **CLI**: [ibmcloud pi volume-group create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-create)

Set the value of the `VOLUME_ID` parameter to the primary volume ID. Provide a name for the primary volume group and the primary volume IDs to create the volume group.

A replication-enabled volume can be attached to a volume group when you create it. To attach the volume, provide the volume ID of the replication-enabled volume that is created on the primary location. Replication-enabled volumes can be attached to an existing volume group. For more information, see [Adding a replication-enabled volume to an existing volume group](#add-rep-vol-existing-vol-grp).


#### Verifying the status of the volume group
{: #verify-vol-grp-stat}

Verify that the volume group is created successfully and it is in a `consistent_copying` state by using the following API or CLI commands:

- **API**: [get storage details of the volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get)
- **CLI**: [ibmcloud pi volume-group storage-details](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-storage-details)

Set the value of the `VOLUME_GROUP_ID` parameter to the primary volume group ID. Provide the primary volume group IDs to get the details.

Refer to the following table for the properties and its definitions.

| Property               | Description |
| ---------------------- | ----------- |
| `consistencyGroupName` | Indicates the name of the replication consistency group that is created at the storage level. The name is same as the replication consistency group on the secondary location. The storage controller creates the name and not defined by the user. |
| `auxiliary` | Indicates whether the volume group is for the auxiliary volumes or for the primary volumes. If the volume group is for the auxiliary volumes on the secondary location, the returned value is `true`. If the volume group is for the primary volumes on the primary location, the returned value is `false`. |
| `name` | Indicates the name of the volume group that you provide when you created it in the primary location. In the secondary location, the name property is same as the `consistencyGroupName` property. |
| `volumeIDs` | Lists the volume IDs that are part of the volume group. |
| `statusDescription` | Assigned with a status, if any failure occurs when you add volumes to a volume group.|
| `status` | Indicates one of the following volume group states: \n - `available` - ready to be managed\n - `error` - encountered an error. Volume group is not manageable in this state and you can only perform a `delete` operation\n - `updating` - `update` operation on the volume group is in progress\n - `creating` - `create` operation on the volume group is in progress |
| `replicationStatus` | Indicates that replication status is active for the volume group. If this property value is set to `disabled`, replication is not active for the volume group. |
| `state` | Indicates the status of the consistency group. |
{: class="simple-table"}
{: caption="Properties of a volume group and their descriptions." caption-side="bottom"}
{: #vol-grop-status-table}

The status of the volume group changes to `consistent_copying` state when the primary volume data is replicated to the auxiliary volume on the secondary location and is ready to continue the replication process. The {{site.data.keyword.powerSys_notm}} manages the auxiliary volume after it is onboarded to the secondary location.

You must have the following information before you start onboarding the auxiliary volumes on the secondary location:

- CRN of the workspace where the primary volumes are added
- Auxiliary volume names associated with the primary volumes that are replication-enabled. You can get the auxiliary volume names by querying the details of the primary volumes.

After you collect the CRN and auxiliary volume names, you can switch to the secondary location and the workspace where the auxiliary volumes are located.

The workspace must be part of the same IBM Cloud account ID as the primary location workspace.
{: note}

### Actions on the secondary location
{: #configure-secondary-site}

Complete the following actions to onboard auxiliary volumes on the secondary location:

- [Onboarding an auxiliary volume](#onboard-aux-vol)
- [Verifying the auxiliary volume for replication](#verify-aux-vol)

#### Onboarding an auxiliary volume
{: onboard-aux-vol}

To manage the replicated volume on a remote location and perform volume recovery, onboard an auxiliary volume. For {{site.data.keyword.powerSys_notm}} to manage the auxiliary volume, onboard the auxiliary volume to the secondary location.

You must have the `editor` role access on the source and target {{site.data.keyword.powerSys_notm}} workspaces to onboard the auxiliary volume. The source and target workspace must be created by using the same account ID.
{: note}

Obtain the following information from the primary location to request for onboarding the auxiliary volumes on the secondary location:

- Have editor role access on both the primary and the secondary location workspaces
- Maintain the same IBM Cloud account ID on both primary and secondary location workspaces
- Fetch the Cloud Resource Name (CRN) of the {{site.data.keyword.powerSys_notm}} workspace instance where the primary volumes are located (primary location)
- Fetch the auxiliary volume names from the **auxVolumeName** field of primary volumes in the primary location for onboarding


When onboarding an auxiliary volume, the following conditions apply:

- If a volume group of the auxiliary volume exists at the secondary location, the auxiliary volume is added to it.
- If a volume group of the auxiliary volume does not exist at the secondary location, the onboarding operation automatically creates a volume group. The volume group is associated with the auxiliary volume on the secondary location.

The onboarded auxiliary volume is added to this volume group. The volume group that is created on the secondary location is associated with the volume group on the primary location. The volume group on the primary location contains the primary volume that is associated with the auxiliary volume. To verify the replication status between the two primary and the auxiliary volumes, compare the consistency group name of the volume group on both the locations.

Use the [ibmcloud pi workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace) CLI command to set the value of the workspace to the service workspace where the auxiliary volumes are located. For example, `ibmcloud pi ws target AUXILIARY_WS_CRN`.
{: note}

To onboard the auxiliary volume on the secondary site, use the following API or CLI commands:

- **API**: [onboard auxiliary volume](/apidocs/power-cloud#pcloud-volume-onboarding-post)
- **CLI**: [ibmcloud pi volume onboarding create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-onboarding-create)

Specify the following parameters:
- source CRN: Specify the CRN parameter of the workspace where the primary volume is located
- auxiliary volume: Specify the auxiliary volume name

#### Verifying the replication status of the auxiliary volume
{: #verify-aux-vol}

An onboarding task ID is returned when you complete onboarding the auxiliary volumes on the secondary location. Use the task ID to check the status of the onboarding operation by using the following API and CLI commands:

- **API**: [List all volume onboardings for this cloud instance](/apidocs/power-cloud#pcloud-volume-onboarding-getall)
- **CLI**: [ibmcloud pi volume onboarding get](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-onboarding-get)


Refer to the following table for the properties and its definitions.

| Property               | Description |
| ---------------------- | ----------- |
| `progress` | Indicates the progress of the onboarding operation of the auxiliary volume in percentage |
| `results` | Contains the list of onboarded volume names or details of any failures that occurred during the onboarding operation of the auxiliary volume |
| `status` | Indicates the status of the volume onboarding operation. If the operation is successful, the return value is `Success`. If an error occurred during the onboarding operation, the return value is `Failure`. |
{: class="simple-table"}
{: caption="Properties of an auxiliary volume and their descriptions." caption-side="bottom"}


If the onboarding process of the auxiliary volume on the secondary location is successful, both the onboarded volume and volume group are present in the {{site.data.keyword.powerSys_notm}} workspace on the secondary location. The resources in the secondary location have their own IDs. The IDs are different from the IDs and CRNs of the associated volumes on the primary location.

Obtain the status of the auxiliary volumes by using the auxiliary volume names. If the onboarding operation is successful, the auxiliary volume names are available. Verify the status of the auxiliary volumes by using the following API and CLI commands:

- **API**: [Get a Cloud Instance's current state/information](/apidocs/power-cloud#pcloud-cloudinstances-get)
- **CLI**: [ibmcloud pi volume get](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-get)


Refer to the following table to verify whether the replication properties of the volume are as expected.

| Property               | Verifying the replication status |
| ---------------------- | ----------- |
| `auxVolumeName` | Matches the `auxVolumeName` value that is used to onboard the volume |
| `auxiliary` | Set to `true` because the volume is the auxiliary volume |
| `consistencyGroupName` | Matches the consistency group name of the volume group on the primary location |
| `groupID` | Returns the ID of the volume group |
| `masterVolumeName` | Matches the `masterVolumeName` value of the primary volume on the primary location |
| `mirroringState` |Set to `consistent_copying` state |
| `primaryRole` | Set to `master` as the primary volume is acting as the active volume |
| `replicationEnabled` | Set to `true` |
| `replicationStatus` | Set to `enabled` |
{: class="simple-table"}
{: caption="Verifying the replication status of an auxiliary volume." caption-side="bottom"}


Using the `groupID` value of the auxiliary volume, query the details of the volume group. Verify whether the auxiliary volume is enabled for replication by using the following API and CLI commands:


- **CLI**: [ibmcloud pi volume-group get](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-get)
- **API**: [Get all volume groups](/apidocs/power-cloud#pcloud-volumegroups-getall)

Refer to the following table to verify that the replication status of the volume group is as expected.

| Property               | Verifying the replication status |
| ---------------------- | ----------- |
| `auxiliary` | Set to `true` |
| `state` | Set to `consistent_copying` state to match the `mirroringState` of the auxiliary volume |
| `volumeIDs` | Contains a list of volume IDs that belongs to the volume group. Verify whether it contains the ID of the auxiliary volume that was onboarded |
{: class="simple-table"}
{: caption="Verifying the replication-enabled status of a volume group." caption-side="bottom"}


## Performing a failover and fallback operation
{: #perform-fail-over-back}

If a disaster occurs on the primary location, access to all the storage volumes that are allocated on the primary location is lost. The replication relationship for the replication-enabled primary volumes is broken with the secondary location. The state of the consistency group (volume group) changes to `inconsistent-disconnected`. On the primary location, no volume is associated with the primary role in the volume group.



Complete the following steps to perform the failover operations on the secondary location:

1. Stop the auxiliary volume group and access the auxiliary volume on the secondary location. See, [Failover to the secondary location](#failover-sec-loc)
2. [Verify that the auxiliary volume group is in an idling state](#verify-aux-vol-grp-idling)

When you complete the failover steps, the volumes are ready to accept I/O requests. The virtual server instance that these volumes are attached to can be powered on and you can continue the execution.


### Failover to the secondary location
{: #failover-sec-loc}

To access the auxiliary volumes from the secondary location due to a primary location failure, stop the volume group. Allow the auxiliary volumes in the volume group to access the auxiliary volumes on the secondary location.

You can perform the failover operation by using the following API and CLI commands:

- **API**: [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post) API with **access** flag set to `True`



- **CLI**: [ibmcloud pi workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace)





If you are using the CLI command to onboard an auxiliary volume, the service workspace must be set to the workspace where the auxiliary volumes are located. For example, `ibmcloud pi ws target AUXILIARY_WS_CRN`.
{: note}

Verify that the action that you perform on a volume group meets the current state of the volume group. Otherwise, an error message appears indicating that the volume group is not in the expected state.
{: attention}


When you perform an action on a volume group, an error is returned if the following state and actions on the volume group do not match:
- Stop a volume group when the `replicationStatus` is in the `disabled` state
- Start a volume group when the `replicationsStatus` is in the `enabled` or `available` state
- Reset a volume group that is not in the `error` state

### Verifying the volume group for idling state
{: #verify-aux-vol-grp-idling}

When you stop the volume group, the status of the consistency group is changed to `idling`, replication is disabled, and the auxiliary volumes allow I/O operations.

Get the volume group details to verify the status of the volume group by using the following API and CLI commands:

- **API**: [Get storage details of volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get)
- **CLI**: [ibmcloud pi volume-group storage-details](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-storage-details)


### Fallback to the primary location
{: #fallback-prim-loc}

When the primary location is recovered, you can re-enable the primary volume group for replication. When the primary volume is ready for replication, you can fallback to the primary location. Complete the following steps to synchronize the data between the auxiliary volumes and primary volumes:

1. Turn off the virtual server instance on the secondary location
2. [Synchronize the I/O updates from auxiliary volume to primary volume](#sync-io-aux-prim)
3. [Stop the primary volume group to disable replication](#stop-prim-vol-grp-disable-rep)
4. [Re-enable replication on the primary volume group](#re-enabl-repl)

After replication is re-enabled, you can start the virtual server instance and its workload at the primary location. When the primary server instance is the active instance, you can turn off the virtual server instance at the secondary location.

#### Synchronizing I/O updates from auxiliary volume to primary volume
{: #sync-io-aux-prim}

To fallback to the primary volume, any I/O updates made to the auxiliary volume must be replicated to the primary volume. Start the primary volume group in the auxiliary mode to synchronize the data from auxiliary volume to primary volume.

Use the [ibmcloud pi workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace) CLI command to set the service workspace to the workspace where the auxiliary volumes are located. For example, `ibmcloud pi ws target AUXILIARY_WS_CRN`.
{: note}

Use the following API or CLI commands to start the primary volume in auxiliary mode:

- **API**: [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post). Set the `VOLUME_GROUP_ID` parameter to the auxiliary volume group ID. Using the API, start the volume group and to set it as the `aux` volume as defined in the following code:


```code

    Request Body:
    {
      "start": {
        "source": "aux"
      }
    }

```
- **CLI**: [ibmcloud pi volume-group action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-action). Set the `VOLUME_GROUP_ID` parameter to the auxiliary volume group ID, `--operation` flag to `start`, and set `--source` flag to `aux`.

Verify whether the `primaryRole` value of the volume group is set to `aux`. Monitor the state of the volume group until the replication of data from the auxiliary volume to the primary volume is completed. The change in the state of the primary volume group to `consistent_copying` value indicates that the data is synchronized from the secondary location to the primary location.

#### Stopping the primary volume group to disable replication
{: #stop-prim-vol-grp-disable-rep}

When you complete data replication from the auxiliary volume to the primary volume, it is time to fallback to the primary volume. To enable the primary volume, use the following API and CLI commands to stop the primary volume group and disable the replication:

- **API**: [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID. The API must stop the volume group and allow read access. For example, the request body must be defined as follows:


```code

    Request Body:
    {
      "stop": {
        "access": true
      }
    }

```

- **CLI**: [ibmcloud pi volume-group action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-action). Set the `VOLUME_GROUP_ID` parameter to primary volume group ID, `--operation` flag to `stop`, and `--allow-read-access` flag to `True`.

Wait for the `replicationStatus` parameter of the primary volume group to change to the `disabled` state. In this state, the primary and secondary locations do not replicate with each other. Therefore, I/O operations on the auxiliary volume do not replicate to the primary volume.

#### Reenabling replication on the primary volume group
{: #re-enabl-repl}

To restart the primary volume group that is in the disabled state, use the `start` command. When you start the volume group to re-enable replication, the primary volumes of the primary volume group are the `master` volumes again.

- **API**: [Perform an action on a volume group](/apidocs/power-cloud#pcloud-volumegroups-action-post). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID. Using the API, start the volume group and set it as the `master` volume as defined in the following code:


```code

    Request Body:
    {
      "start": {
        "source": "master"
      }
    }

```

- **CLI**: [ibmcloud pi volume-group action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-action). Set the `VOLUME_GROUP_ID` parameter to primary volume group ID, `--operation` flag to `start`, and set `--source` flag to `master`.


Wait for the volume group to be replication-enabled and in a `consistent_copying` state. When replication is active, the I/O operations on the primary volume are replicated to the auxiliary volume on the secondary location.















## Updating an existing volume as a replication-enabled volume
{: #update-vol-rep-enabled}

You can modify an existing volume to be replication-enabled if it is created in a storage pool that supports the replication process. To verify, query the details of the volume, get the details of the storage pool that contains the volume, and verify it with the list of storage pools that support replication. For more information about storage pools that support replication, see [{{site.data.keyword.powerSys_notm}} storage pool that supports GRS](#locations-GRS).

Use the following API and CLI commands to query the volume details:

- **API**: [Perform an action on a volume group](apidocs/power-cloud#pcloud-cloudinstances-volumes-action-post). Set the `VOLUME_ID` parameter to the primary volume ID. Using the API, query the volume details as defined in the following code:

```code

    Request Body:
    {
      "replicationEnabled": true
    }

```

- **CLI**: [ibmcloud pi volume-group action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-update). Set the `VOLUME_ID` parameter to the primary volume ID, and query if the `--replication-enabled` flag is set to `True`.


## Adding a replication-enabled volume to an existing volume group
{: #add-rep-vol-existing-vol-grp}

You can add replication-enabled volumes to an existing volume group by using the following API and CLI commands:

- **API**: [updates the volume group](/apidocs/power-cloud#pcloud-volumegroups-put). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID. Using the API, add the primary volume IDs to the volume group as defined in the following code:

```code

    Request Body:
    {
      "addVolumes": [
        "PRIMARY_VOLUME_ID"
      ]
    }

```

- **CLI**: [ibmcloud pi volume-group update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID, and set the `--add-member-ids` flag to the primary volume IDs that must be added to the volume group.

## Disabling replication of a volume
{: #disable-grs}

When you disable replication of a primary volume, the associated auxiliary volume on the secondary location is deleted.

Failure to complete this procedure in the specified order might result in the loss of source volume data. First, you must complete the actions on the primary location and then complete the actions on the secondary location.
{: attention}

To disable replication of a primary volume, perform the following steps:

1. Actions on the primary location

   1. [Remove the primary volume from the volume group](#rem-prim-vol-grp)
   2. [Delete the primary volume group, if empty](#del-prim-vol-grp)
   3. [Disable replication for the primary volume](#dis-repl-prim-vol)
   4. [Verify whether the replication is disabled for the primary volume](#ver-repl-prim-vol)

2. Actions on the secondary location

You can perform these steps only if you complete the onboarding operation of the auxiliary volume.
{: note}

   1. [Remove the auxiliary volume from the volume group](#rem-aux-vol-grp)
   2. [Delete the auxiliary volume group, if empty](#del-aux-vol-grp)
   3. [Delete the auxiliary volume](#del-aux-vol)


### Removing the primary volume from the volume group
{: #rem-prim-vol-grp}

Use the following API and CLI commands to remove the primary volume from the volume group:

- **API**: [updates the volume group](/apidocs/power-cloud#pcloud-volumegroups-put). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID and the `VOLUME_ID` parameter to the primary volume ID. Use the API to remove the primary volume ID from the volume group as defined in the following code:

```code

    Request Body:
    {
      "removeVolumes": [
        "PRIMARY_VOLUME_ID"
      ]
    }

```

- **CLI**: [ibmcloud pi volume-group update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID, and set the `--remove-member-volume-ids` flag to the primary volume IDs that must be removed from the volume group.

Use the [ibmcloud pi workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace) CLI command to set the service workspace to the workspace where the primary volumes are located. For example, `ibmcloud pi ws target PRIMARY_WS_CRN`.
{: note}

You can remove multiple replication-enabled volumes from a volume group.

### Deleting an empty a primary volume group
{: #del-prim-vol-grp}

Use the following API and CLI commands to delete the primary volume group if it is empty:

- **API**: [Delete a cloud instance volume group](/apidocs/power-cloud#pcloud-volumegroups-delete). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID.

- **CLI**: [ibmcloud pi volume-group delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-delete). Set the `VOLUME_GROUP_ID` parameter to a primary volume group ID that must be deleted.


### Disabling replication for the primary volume
{: #dis-repl-prim-vol}

Use the following API and CLI commands to disable replication for the primary volume, if it is removed from the volume group:

- **API**: [Perform an action on a Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-action-post). Set the `VOLUME_ID` parameter to the primary volume ID. Use the API to disable the replication for the primary volume ID as defined in the following code:

```code

    Request Body:
    {
      "replicationEnabled": false
    }

```

- **CLI**: [ibmcloud pi volume action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-action). Set the `VOLUME_ID` parameter to the primary volume ID that must be disabled and set the `--replication-enabled` flag to `False`.

### Verifying whether replication is disabled for the primary volume
{: #ver-repl-prim-vol}

Use the following API and CLI commands to verify whether replication is disabled for the primary volume:

- **API**: [List all volumes for this cloud instance](/apidocs/power-cloud#pcloud-cloudinstances-volumes-getall). Set the `VOLUME_ID` parameter to the primary volume ID to query the replication status.

- **CLI**: [ibmcloud pi volume get](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-get). Set the `VOLUME_ID` parameter to the primary volume ID to query the replication status.


### Removing auxiliary volume from the volume group
{: #rem-aux-vol-grp}

Use the following API and CLI commands to remove the auxiliary volume from the volume group:

- **API**: [updates the volume group](/apidocs/power-cloud#pcloud-volumegroups-put). Set the `VOLUME_GROUP_ID` parameter to the volume group ID and the`VOLUME_ID` parameter to the auxiliary volume ID. Use the API to remove the auxiliary volume ID from the volume group as defined in the following code:

```code

    Request Body:
    {
      "removeVolumes": [
        "AUXILIARY_VOLUME_ID"
      ]
    }

```

- **CLI**: [ibmcloud pi volume-group update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update). Set the `VOLUME_GROUP_ID` parameter to an auxiliary volume group ID, and set the `--remove-member-volume-ids` flag to the auxiliary volume IDs that must be removed from the volume group.


### Deleting an empty auxiliary volume group
{: #del-aux-vol-grp}

Use the following API and CLI commands to delete the auxiliary volume group if it is empty:

- **API**: [Delete a cloud instance volume group](/apidocs/power-cloud#pcloud-volumegroups-delete). Set the `VOLUME_GROUP_ID` parameter to auxiliary volume group ID.

- **CLI**: [ibmcloud pi volume-group delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-delete). Set the `VOLUME_GROUP_ID` parameter to an auxiliary volume group ID that must be deleted.


### Deleting an auxiliary volume
{: #del-aux-vol}

Use the following API and CLI commands to delete the auxiliary volume:

- **API**: [Delete a cloud instance volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-delete). Set the `VOLUME_ID` parameter to an auxiliary volume ID that must be deleted.

- **CLI**: [ibmcloud pi volume delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-delete). Set the `VOLUME_ID` parameter to an auxiliary volume ID that must be deleted.

## Modifying a replication-enabled primary volume
{: #modify-rep-prim-vol}

You can modify the attributes of a replication-enabled primary volume. To modify some of the properties of the primary and auxiliary volumes, you must perform related actions on the primary and secondary locations.

### Changing the size of a primary volume

To change the size of a replication-enabled, complete the following steps:

1. Remove the primary volume from the volume group
2. Change the size of the primary volume
3. Add the primary volume back to the volume group

In the next 24 hours, the size of the auxiliary volume on the secondary location is changed.

For example, on the `dal10` and `wdc07` location pair, when you change the size of a replication-enabled primary volume on the primary location, the system changes the size of the auxiliary volume on the secondary location in the next 24 hours.

Use the following API and CLI commands to change the size of the replication-enabled primary volume:


-**API**: [Update a cloud instance volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-put). Set the `VOLUME_ID` parameter to primary volume ID and set the size in GB by using the following request body:

```code
  Request Body:
  {
    "size": SIZE_IN_GB
  }

```

-**CLI**: [ibmcloud pi volume update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-update). Set the value in the `VOLUME_ID` parameter to the primary volume ID and set the `--size` value to be in GB.

Do not resize a primary volume by disabling replication of the volume as it results in errors on the auxiliary volume on the secondary location.
{: important}




## Changing the bootable and shareable properties of a primary volume
{: #chang-prop-prim-vol}

To change the values of the `bootable` or `shareable` properties on the primary volume, use the following API or CLI commands:

-**API**: [Update a cloud instance volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-put). Set the `VOLUME_ID` parameter to the primary volume ID and set the `--bootable` or `--shareable` flags to `True` or `False` value.

-**CLI**: [ibmcloud pi volume update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-update). Set the value of the `VOLUME_ID` parameter to the primary volume ID and set the value of the `--bootable` or `--shareable` flags to `True` or `False` value.

A volume can be either shareable or bootable, but cannot be both.
{: note}

After you change the `bootable` or `shareable` property values for a primary volume on the primary location, you must update the same property for the auxiliary volume on the secondary location.

## Changing the tier of a primary volume
{: #chang-tier-prim-vol}

You cannot change the tier of a replication-enabled volume.




## Deleting a replication-enabled primary volume
{: #delete-prime-vol}

To delete a volume or a replication-enabled primary volume, the status of the volume must indicate one of the following states: `available`, `error`, `error_restoring`, `error_extending`, or `error_managing`. In addition, you cannot delete the volume if it is in the `migrating` or `attached` state, belongs to a volume group, has snapshots, or if it is disassociated from its snapshots after a transfer.

To delete a primary volume, you must complete the actions on the primary and secondary locations:

- Complete the following actions on the primary location:
    1. [Remove the primary volume from its volume group, if the primary volume is associated with a volume group](rem-prim-vol-vol-grp)
    2. [Delete the primary volume](#del-prim-vol)

- Complete the following actions on the secondary location, if the auxiliary volume is onboarded on the secondary location:
    1. [Remove an auxiliary volume from its volume group, if the auxiliary volume is associated with a volume group](#rem-aux-vol-grp)
    2. [Delete the auxiliary volume](#del-aux-vol)

If the auxiliary volume is not deleted from the secondary site, an out-of-band periodic check that occurs every 24 hours sets the auxiliary volume to an `ERROR` state. You cannot use volume when it is in `ERROR` state and the only operation that you can perform is to delete the volume.
{: note}


### Removing the primary volume from its volume group
{: rem-prim-vol-vol-grp}

Use the following API or CLI commands to remove the primary volume from its volume group:

Use the [ibmcloud pi workspace](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace) CLI command to set the target workspace to the workspace where the primary volumes are located. For example, `ibmcloud pi ws target PRIMARY_WS_CRN`.
{: note}


- **API**: [updates the volume group](/apidocs/power-cloud#pcloud-volumegroups-put). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID and the `VOLUME_ID` parameter to the primary volume ID. Use the API to remove the primary volume ID from the volume group as defined in the following code:

```code

    Request Body:
    {
      "removeVolumes": [
        "PRIMARY_VOLUME_ID"
      ]
    }

```

- **CLI**: [ibmcloud pi volume-group update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-update). Set the `VOLUME_GROUP_ID` parameter to the primary volume group ID, and set the `--remove-member-volume-ids` flag to the primary volume ID that must be removed from the volume group.


### Deleting the primary volume
{: #del-prim-vol}

Use the following API and CLI commands to delete the primary volume:

- **API**: [Delete a cloud instance volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-delete). Set the `VOLUME_ID` parameter to a primary volume ID that must be deleted.

- **CLI**: [ibmcloud pi volume delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-delete). Set the `VOLUME_ID` parameter to a primary volume ID that must be deleted.


## Deleting a replication-enabled auxiliary volume
{: #del-aux-vol}

If you delete an auxiliary volume, the associated primary volume is also deleted.
{: attention}


When you [disable the replication service on the primary volume](#disable-vol-repli) or [delete the primary volume](#del-prim-vol), the replication relationship between the primary volume and the secondary volume is deleted in the storage backend. If the auxiliary volume on the secondary location is associated with a volume group, [remove the auxiliary volume from the volume group](#rem-aux-vol-grp). Delete the auxiliary volume manually. If you do not delete the auxiliary volume from the secondary site, an out-of-band periodic check that occurs every 24 hours sets the auxiliary volume to an `ERROR` state. Confirm the status of the auxiliary volume by checking the `outOfBandDeleted` property of the auxiliary volume.

## GRS impacts on other {{site.data.keyword.powerSys_notm}} operations
{: #impacts-on-powervs}

The impacts of GRS on other {{site.data.keyword.powerSys_notm}} operations are as follows:

- Image interface is not changed and replication is not supported for images
- Operation interface and the affinity policies for storage pool for virtual server instances are not changed. The replication and non-replication-enabled volumes support volume attachment and detachment.
- Snapshot and capture operations are allowed for a virtual server instance with replication and non-replication-enabled volumes when the volumes are from the same storage pool. The snapshot and capture operations are performed by using the non-replication-enabled volumes internally even though the volumes of a virtual server instance are replication-enabled.
- Cloned volume is replication-enabled when you clone a replication-enabled volume by default. During cloning, you can specify whether the cloned volume must be replication-enabled or not. If you want the cloned volume to be replication-enabled, specify the policy for the clone volume. You can use the following methods to clone a volume:
    - [Clone a volume by using API](/apidocs/power-cloud#pcloud-v2-volumesclone-execute-post){: external}.
    - [Clone a volume by using CLI](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone){: external}.
    - [Clone a volume by using Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume_clone){: external}.


## Best practices for GRS
{: #best-practices-GRS}

- Set the **Shareable** and **Bootable** flag explicitly on onboarded volumes, if required.
- Start the onboarding of auxiliary volumes only when the primary volumes and volume group are in a consistent copying state. You can get the volume details by using the [get volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-get){: external} API to determine the state of the primary volumes and volume group in the mirroring state on the primary site. Verify that the volume group is created successfully and it is in a consistent copying state by using the [get storage details of the volume group](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get){: external} API.
* Get volume details by using the following methods:
    * [Power Cloud API](/apidocs/power-cloud#pcloud-cloudinstances-volumes-get){: external}.
    * [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_volume){: external}.
* Get the details of the volume groups storage details by using the following methods:
    * [Power Cloud API](/apidocs/power-cloud#pcloud-volumegroups-storagedetails-get){: external}.
    * [Power Virtual Server CLI](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-group-storage-details){: external}
    * [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/pi_volume_group_storage_details){: external}.

- When you add or remove a primary or an auxiliary volume from a volume group from one location, perform the same operation from the other location to keep the data in sync.
- Delete the volumes from the primary and secondary location. Volumes are charged when you delete an auxiliary volume but fail to delete the primary volume.
- Use the primary location for all the volume operations and perform operations on the auxiliary volume on the secondary location only during failover.
