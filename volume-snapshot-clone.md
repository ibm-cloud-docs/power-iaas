---

copyright:
  years: 2023, 2025

lastupdated: "2025-09-23"

keywords: cloning and restoring snapshots, power virtual server as a service, private cloud, snapshots, clone API

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Snapshots, restoring, and cloning
{: #snapshots-cloning}

---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

{{site.data.keyword.powerSysFull}} provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. Using IBM's *FlashCopy* feature, {{site.data.keyword.powerSysShort}} APIs you can create delta snapshots, volumes-clones, and restore your disks.



## Use case
{: #create-snapshot-taking-usecase}

The snapshot feature has several use cases. Consider the following example:
- An administrator plans to upgrade the middleware. If the upgrade to the middleware fails, the administrator must restore the source disk to its original state.
- The administrator completes the following steps:


   1. Initiate the snapshot of the source disk where the middleware information resides by using the GUI, API, or CLI. A snapshot of the source disk is created.

   2. Upgrade the middleware.

   3. If the upgrade fails, the administrator restores the source disk by using the snapshot.

   4. If the upgrade succeeds, the administrator deletes the snapshot.


You can initiate multiple snapshot operations. However, these concurrent snapshot operations occur on different sets of disks.
{: note}

## Creating a snapshot
{: #create-snapshot}

A snapshot is a copy of the state of a volume or a set of volumes that is taken at a specific time. By using snapshot, you can restore your volumes to the state when you took the snapshot.
{: shortdesc}



With snapshots, you can create a relationship between your source disks and a target disk at a defined time, for example **T1**. Target disks are created as part of creating a snapshot operation. The snapshot operation tracks the changes that are made to the source disk beyond **T1** time. Thus, you can restore the source disks to their **T1** state at a later point in time.

You can create and manage snapshots in your {{site.data.keyword.powerSys_notm}} workspace by using the GUI, API, and CLI.



### Prerequisites
{: #create-snapshot-prereq}

- Before you take a snapshot of a volume, it is recommended that you quiesce all the applications that access the volume. This action is required to ensure that all the data is moved to the disk to avoid loss of data.

- If you are creating a snapshot of a volume that is shared among multiple virtual server instances, then you must quiesce all the applications on all these virtual server instances. If you are not sure how to quiesce your applications, it is recommended to shut down any virtual server instances that are attached to the volumes that you want to include in the snapshot.

- Snapshot names must be unique for your workspace. If you want to reuse a snapshot name, delete the existing snapshot with that name, and then reuse the name.

- Volumes to be included in the snapshot must be in the same storage pool.

- Volumes to be included in the snapshot must not be in the `error` state and the health state of the volume must be `ok`.



### Creating a snapshot by using the {{site.data.keyword.powerSys_notm}} user interface
{: #create-snapshot-gui}

To create a snapshot by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external} and log in with your credentials.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select a workspace in which you want to create the snapshot. The Workspace details panel is displayed.

4. Click **View virtual servers**. The Virtual server instances page is displayed.

5. In the navigation panel, click **Storage** > **Instance snapshots**. The Instance snapshots page is displayed with a list of any existing snapshots.

6. Click **Create instance snapshot**. The Create instance snapshot page is displayed.

7. In the General section, enter a name for the snapshot in the **Name** field.

8. Optional: Enter user tags and description for the snapshot in the **User tags (optional)** and **Description** fields.

9. Click **Continue**.

10. In the Volumes section, select the required virtual server instance from the **Select virtual server instance** list. Any storage volumes that are attached to the selected virtual server instance are displayed.

11. Select the storage volumes to include in the snapshot and click **Finish**. The summary of the selected snapshot configuration and its total estimated cost is displayed in the Summary panel.

    You can select multiple storage volumes to include in the snapshot. However, all the selected volumes must belong to the same storage pool.
    {: note}

12. Optional: Click **Add to estimate** to add the cost information to an existing estimate or to create a new estimate.

13. Click the terms and conditions link to read the [IBM Cloud Terms of Use](/docs/overview?topic=overview-terms). To continue, select the **I agree to the Terms and conditions** checkbox and click **Create**. After the snapshot is successfully created, a success message is displayed on the screen.

The snapshot that you created is displayed in the Instance snapshots page with the following details:

- **Name**: Snapshot name.
- **Volumes**: Number of storage volumes that are included in the snapshot.
- **Description**: Snapshot description.
- **Virtual server instance**: Name of the virtual server instance to which the selected storage volumes were attached at the time of the snapshot creation.
- **Created**: Timestamp that indicates when the snapshot was created.
- **Status** and **Status details**: These two columns display the current status of a snapshot. A snapshot can have one of the following statuses:
     - **Available**: The snapshot was successfully created and is available for restore operations.
     - **Error**: An error has occurred while creating the snapshot. The snapshot cannot be recovered and must be deleted.
     - **Restoring**: A restore operation is currently in progress.
     - **Restore error**: An error has occurred during the restore process. You can use the **Restore** option from the overflow menu to retry the restore process. To revert a snapshot with *Restore error* status to its last working state, you can use the **Rollback** option from the **Actions** menu on the snapshot's details page.
     - **Restore reverted**: The restore attempt was reverted, likely because a storage volume that is included in the snapshot is currently involved in another snapshot operation. You can retry the restore once the other snapshot operation is complete.
     - **Rolling back**: A rollback operation is currently in progress. The rollback operation reverts the virtual server instance to its last working state.
     - **Rollback error**: An error has occurred during the rollback process.
- **Last update**: Timestamp that indicates when the snapshot was last updated.



### Creating a snapshot by using API or CLI commands
{: #create-snapshot-api-cli}

Use the following API and CLI commands to create a snapshot:

- **API:** [Create a PVM Instance snapshot](/apidocs/power-cloud#pcloud-pvminstances-snapshots-post).

- **CLI:** [ibmcloud pi snapshot create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-snapshot-create).

You must provide values for the following parameters in the API and CLI commands:

* `name`: (Required) Specifies the name of the snapshot.

    The `name` must be a unique value among all the snapshots for the workspace.
    {: note}

* `description`: (Optional) Describes the snapshot.
* `volumeIDs`: (Optional) Includes a list of one or more volumes to be included in the snapshot. If this parameter is left empty, all volumes that are attached to the virtual server instance (VSI) are included in the snapshot.


### Restrictions and considerations for creating a snapshot
{: #create-snapshot-rest-cons}

You must consider the following restrictions and considerations when you create a snapshot:




- You cannot create a snapshot of a virtual server instance if any of its attached volumes are currently undergoing cloning or snapshot operations.

- You cannot modify the shareable or bootable properties of any volume that is part of an existing snapshot.



- You cannot run snapshot operations in parallel from different virtual server instances for the same shared volume at a specific time.

- You cannot resize a volume if the volume is included in a virtual server instance snapshot. To resize such a volume, you must first delete all the snapshots that the volume is part of.

- You cannot detach volumes from the virtual server instance that are included in an instance snapshot. To detach such volumes, you must first delete all the snapshots these volumes are a part of.

-	You must attach all volumes that are included in the snapshot to the same virtual server instance.



-	When you create a snapshot by using the API or CLI, the `volumeIDs` parameter is optional. If the `volumeIDs` option is not specified, all volumes that are attached to the virtual server instance are included in the snapshot.




-	If the volumes that are attached to the virtual server instance are not in the same storage pool, then use the `volumeIDs` option to include the volumes that are in the same storage pool. In this case, you must group the volumes from the same storage pool and create a snapshot for each volume group in the storage pool.

If the operation to create a snapshot fails, it results in an `error` state. You can delete this snapshot so that no other operations can be performed on it.
{: important}

## Restoring a snapshot
{: #restoring-snapshot}

The `restore` operation restores the volumes that are part of a virtual server instance snapshot to the source disks. When the restore operation is in progress, {{site.data.keyword.powerSys_notm}} creates a backup snapshot, which can be used if the restore operation fails. If the restore operation succeeds, the backup snapshots are deleted. If the restore operation fails, the snapshot status is set to `restore-error`. You can attempt to retry the restore or roll back operations to their original state. Use the `restore_fail_action` query parameter with `retry` value to retry the restore operation. To roll back to a previous disk state, use the `restore_fail_action` query parameter with the `rollback` value. When the restore operation fails, the virtual server instance enters an **Error** state.

### Prerequisites
{: #restoring-snapshot-prereq}

Ensure that the following prerequisites are met before you initiate the `restore` operation:

- By default, you must shut down the virtual server instance before you initiate the `restore` operation.

- To restore the data on a live virtual server instance, use the `force restore` operations. The following conditions must be met:

  - Quiesce the applications
  - Do not run I/O operations on the volume disks

  Failure to meet the conditions for `force restore` operation can result in data corruption.
  {:important}

- If you are restoring an instance snapshot of a volume that is shared among multiple virtual server instances, then you must quiesce all the applications on all the virtual server instances. Also, no I/O operations must be running on the shared volumes during the restore operation.

- If you are not sure how to quiesce your applications, it is recommended to shut down any virtual server instances that are attached to the volumes that you want to include in the snapshot.



### Restoring a snapshot by using the {{site.data.keyword.powerSys_notm}} user interface
{: #restore-snapshot-gui}

To restore a snapshot by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external} and log in with your credentials.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace which contains the snapshot that you want to restore. The Workspace details panel is displayed.

4. Click **View virtual servers**. The Virtual server instances page is displayed.

5. In the navigation panel, click **Storage** > **Instance snapshots**. The Instance snapshots page is displayed with a list of the existing snapshots.

6. From the list of available snapshots, select the snapshot that you want to restore. The snapshot details page is displayed.

7. Select **Restore**. The Confirm restore dialog is displayed.

    To restore an instance snapshot, you must first shut down all the related virtual server instances, including the source and any shared volumes that are attached to the instance snapshot. If you cannot shut down the virtual server instances, quiesce all the related applications and set **Force restore** to **Enabled**.
    {: important}

8. Click **Restore**.

   When the restore begins, a notification is displayed to indicate that the restore process has started and a progress bar displays the completion percentage. After the snapshot is restored successfully, the **Status details** column displays the Restore successfully completed status.

A failed restore operation changes the snapshot status to **Restore error**. You can use the **Restore** option from the overflow menu to retry the restore process. To revert a snapshot with *Restore error* status to its last working state, select **Rollback** from the **Actions** menu on the snapshot's details page.
{: note}





### Restoring a snapshot by using API or CLI commands
{: #restoring-snapshot-api-cli}

Use the following API and CLI commands to restore a snapshot:

* **API**: [Restore a PVM Instance snapshot](/apidocs/power-cloud#pcloud-pvminstances-snapshots-restore-post).

* **CLI**: [ibmcloud pi snapshot-restore](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-snapshot-restore)

You must provide values for the following parameters in the API and CLI commands:

* `SNAPSHOT_ID`: (Required) Specify a unique identifier for the snapshot
* `force`: (Optional) Specify the value of the flag as `True` or `False`. By default, the flag is set to `False`. This flag is set to `true` only if the virtual server instance is shut down. By default, the virtual server instance must be shut down before you initiate a snapshot restore operation. When the `force` flag is set to `True`, the prerequisite of the virtual server instance being shut down is relaxed.
* `restore`: (Optional) Use the `restore_fail_action` query parameter only if a previous restore operation results in setting the snapshot to the `restore-error` status. The `restore_fail_action` query parameter accepts the following `retry` or `rollback` values:
  * If the snapshot status is set to `retry`, then again the failed restore operation is attempted.
  * If the snapshot status is set to `rollback`, then the volumes that were failed to be restored are rolled back to their original state.

If you are using the `force` option, you must ensure that all the applications that access the volumes in the instance snapshot are quiesced and no I/O operations are running on the volume disk.

#### Use cases
{: #restoring-snapshot-usecase}

Consider the following scenarios to restore a snapshot:

- Restoring all of the volumes that are part of a virtual server instance snapshot
- Running multiple virtual server instance restore operations
- Retrying a virtual server instance restore operation if it originally failed
- Rolling back a virtual server instance to its original volume state

### Restrictions and considerations
{: #restoring-snapshot-rest-cons}

* Before the system begins the `restore` operation of the snapshot, a temporary backup snapshot of the volumes is created for internal use only. If the snapshot `restore` operation fails, the temporary backup is used by the system to restore the virtual server instance to the state before the `restore` operation failed.

* Volume restore operation is not allowed if any copy operations are running on the target volume. The volumes in the instance snapshot are validated to ensure that no copy operations are running against them. Use the API to [get a list of FlashCopy mappings for a volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-flashcopymappings-ge) or the CLI command to [get a list of FlashCopy mappings for a volume](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-flash-copy-mapping).

* When you perform a `restore` operation, the snapshot task status changes to `restoring`, the volume status is changed to `reverting`, and no other snapshot operations are allowed.

* When `restore` operation on a virtual server instance snapshot fails, the virtual server instance status changes to `restore-Error` state. You can retry the `restore` operation or you can request to roll back the virtual server instance to its original state it was in before the `restore` operation failed.

* If you perform a `restore` operation on the shared volume, all the virtual machines that are sharing the volume are restored.

* If you perform a `restore` operation on the shared volume on one virtual machine, you cannot perform the snapshot, restore, clone, or capture operations on other virtual machines that use the shared volume.

* Before you perform a `restore` operation on a boot disk, the virtual machine must be shut down and the status must change to `shutoff` state.

* After successful `restore retry` operation, the virtual server instance state might not reset from `Error` state. Use `Reset State` feature on the GUI to reset the virtual server instance state.

* You cannot restore a virtual server instance snapshot if the snapshot was recently created and the `FlashCopy` operations are still running in the background. The `FlashCopy` operations must first get completed. Use the API to [get a list of FlashCopy mappings for a volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-flashcopymappings-ge) or the CLI command to [get a list of FlashCopy mappings for a volume](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-flash-copy-mapping).



* To restore volumes that are enabled for volume replication with Global Replication Services (GRS), all the volumes must belong to the same volume group. You cannot restore volumes when a snapshot contains multiple GRS-enabled volumes from different volume groups.





## Deleting a snapshot
{: #delete-snapshot}

You can delete a snapshot by using the GUI, API, or CLI.

You cannot delete a virtual server instance if it has one or more associated snapshots. You must delete all the associated snapshots before you can delete the virtual server instance.
{: important}

### Deleting a snapshot by using the {{site.data.keyword.powerSys_notm}} user interface
{: #deleting-snapshot-gui}

To delete a snapshot using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external} and log in with your credentials.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace which contains the snapshot that you want to delete. The Workspace details panel is displayed.

4. Click **View virtual servers**. The Virtual server instances page is displayed.

5. In the navigation panel, click **Storage** > **Instance snapshots**. The Instance snapshots page is displayed with a list of the existing snapshots.

6. From the list of available snapshots, select the snapshot that you want to delete. The snapshot details page is displayed.

7. Select **Delete** from the **Actions** menu. The Confirm delete dialog is displayed.

8. Type the confirmation text and click **Delete**.

You cannot recover a snapshot after it is successfully deleted.
{: important}


### Deleting a snapshot by using API or CLI commands
{: #deleting-snapshot-api-cli}

Use the following API and CLI commands to delete a snapshot:

* **API**: [Delete a PVM instance snapshot of a cloud instance](/apidocs/power-cloud#pcloud-cloudinstances-snapshots-delete){: external}.

* **CLI**: [ibmcloud pi snapshot-delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-snapshot-delete){: external}.

You must provide values for the following parameters in the API and CLI commands:

* `SNAPSHOT_ID`: (Required) Specify a unique identifier for the snapshot




## Metering and pricing of snapshot
{: #metering-snapshot}

Each snapshot that you create is monitored during every hour and charged depending on the disk space that is requested for the snapshot. The space that is used by a snapshot is charged at 30% of the base rate.

For example, consider that you have **M** disks on a virtual server instance that add up to 600 GB of space. The **M** disks are used as source disks for snapshots. The following charges are applicable on **M** disks:

- If you create one snapshot, you are charged for the disk space that is used by the base 600 GB of **M** disks plus 30% of 600 GB of disk space. That is, 600 GB (space of M disks) + 180 GB (30% of 600 GB) = 780 GB of disk space.
- If you create another snapshot by using same disks, you are charged for the disk space that is used by **M** disks. That is, 600 GB (space of M disks) + (30% of 600 GB) + (30% of 600 GB) = 960 GB of disk space.
- The pricing of a snapshot is calculated based on the volume size and storage tier of the individual source volumes that are present in the snapshot. For example, consider the following table to calculate the cost of a snapshot that has volume A and volume B.

| Volume name | Volume size | Tier type | Cost of a volume |
| ----------- | ----------- | --------- | ---------------- |
| Volume A    | 100 GB      | Tier 1    | 30% of 100 GB    |
| Volume B    | 30 GB       | Tier 0    | 30% of 30 GB    |
{: caption="An example to calculate the cost of a snapshot" caption-side="bottom"}

The cost of the snapshot is the sum of the costs of volume A and volume B.


## Creating a volumes-clone
{: #vol-clon-bp}

### Creating a volumes-clone request
{: #create-vol-clon-req}

The clone operation creates a full copy of the volume. You can select multiple volumes and initiate a group clone operation. When multiple volumes are selected, the clone operation ensures that a consistent data copy is created.

The clone operation continues to copy data from the source disks to target disks in the background. Depending on the size of the source disks and the amount of data to be copied, the clone operation can take a significant amount of time.

#### Prerequisites
{: #vol-clon-bp-req}

Ensure that the following prerequisites are met before you start to create a volumes-clone request:

- A volumes-clone request name must be unique for your workspace. If you want to reuse a volumes-clone request name, delete the existing volumes-clone request with that name, and then reuse the name.

- Volumes to be included in the volumes-clone request must be located in the same storage pool.

- Volumes to be included in the volumes-clone request must not be in the `error` state and the health state of the volume must be `ok`.

- Quiesce the applications that access the set of volumes that you want to include in the volumes-clone request.


#### Creating the volumes-clone request by using API and CLI commands
{: #vol-clon-bp-api-cli}

The `Prepare action` operation completes the preparatory work for creating the group snapshot of volumes that are getting cloned.

**Prerequisites**

Ensure that the following prerequisites are met before you initiate the `Prepare action` operation:

* A minimum of two volumes
* A minimum of one volume to be in the `in-use` state
* A unique volumes-clone name

When a `Prepare action` operation is in progress, you cannot trigger another `Prepare action` operation for the same set of volumes. A `Prepare action` operation must be followed by `Start` and `Execute` operations. If you are not using the existing `Prepare action` operation, you must cancel the existing operation before you initiate the next `Prepare action` operation.
{: note}

Use the following API and CLI command for initiating the `Prepare action` operation:

- **API**: [Create a new volumes clone request and initiates the Prepare action](/apidocs/power-cloud#pcloud-v2-volumesclone-post)
- **CLI**: [ibmcloud pi volume clone create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-create)

You must provide values for the following parameters in the API and CLI commands:

- `name`: (Required) Provide a name to be assigned to the volumes-clone request. The name must be unique among all the existing volumes-clone requests.
- `volumeIDs`: Provide the list of volume identifiers or names to be cloned. A minimum of two volume IDs are required and at least one of the volumes must be in the `in-use` state. All volumes to be included in the volumes-clone request must be in the same storage pool.

When the `Prepare action` operation progresses to `100%`, the `Prepare` status changes depending on the following conditions:

- If `Prepare action` completes successfully, the status changes to `prepared`.
- If `Prepare action` fails to complete successfully, the status changes to `failed`.

To check the status of the `Prepare action` operation, use the API or CLI command with `volumesCloneID` option.

#### Restrictions and considerations
{: #vol-clon-bp-res-con}

- A minimum of 2 volume IDs are required and at least one of them must be in the `in-use` state.

To clone a single volume, you can use the [Create a volume clone for specified volumes](/apidocs/power-cloud#pcloud-v2-volumes-clone-post) API or the [ibmcloud pi volume clone-async](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-async) CLI command. To check on the status of the single volumes-clone, you can use the [Get the status of a volumes clone request for the specified clone task ID](/apidocs/power-cloud#pcloud-v2-volumes-clonetasks-get) API or the [ibmcloud pi volume clone-async get](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-async-get) CLI command.
{: note}

- When a clone operation is performed on a volume that is in the `in-use` state, {{site.data.keyword.powerSys_notm}} creates a consistent group snapshot and re-creates the copy of the cloned volume by using the group snapshot.

- You cannot modify the source or target disk attributes such as disk size, while the clone operation is in progress.

- You cannot attempt to clone a volume that is part of a consistency group as part of an existing consistency group. A volume will belong to a consistency group after you must run the volumes-clone start request, or the volume is part of a snapshot `create` operation where the flash copying in the background is completed.

- A volume cannot be cloned from one storage pool to a different storage pool.

### Starting a volumes-clone request
{: #start-vol-clone-req}

This step allows the consistency group to initiate the `FlashCopy` operation.

As a prerequisite, the volumes-clone request must be in the `Prepared` state.
{: note}


#### Starting a volumes-clone request by using API and CLI command
{: #start-vol-clone-api-cli}

The initial status of the volume-colne request is set to `Starting`.

Use the following API and CLI command to initiate the volumes-clone request:

- **API**: [Initiate the Start action for a volumes-clone request](/apidocs/power-cloud#pcloud-v2-volumesclone-start-post)
- **CLI**: [ibmcloud pi volume clone start](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-start)

You must provide the unique identifier of a volumes-clone request in the `volume_clones_id` parameter. The identifier can be the volumes-clone ID or the volumes-clone name.

When the volumes-clone request is initiated, the initial status is set to `Starting`. When the group snapshot is created, the request status changes to `Available`. The `start` operation of the volumes-clone request is synchronous. When the API call returns to the client, the volumes-clone request status changes to `Available` unless an error occurs. If an error occurs during the `start` operation, the status of the volumes-clone request changes to `Failed`. The reason for failure is specified in the error that is returned with the `start` operation response. The prepared snapshot data is removed so that you can clone the same set of volumes again. If you cancel the `start` operation of a volumes-clone request, the status of the volumes-clone request changes to `Cancelling`. You can cancel a volumes-clone request when the volumes-clone request is in the `Available` state.

#### Restrictions and considerations
{: #start-vol-clone-res-con}

You must consider the following restrictions and considerations before you start the volumes-clone request:

- A minimum of two volume IDs are required and at least one of them must be in the `in-use` state.

- When a clone operation is performed on a volume that is in the `in-use` state, {{site.data.keyword.powerSys_notm}} creates a consistent group snapshot and re-creates the copy of the cloned volume by using the group snapshot.

- When a clone operation is in progress, you cannot modify the source or target disk attributes, such as disk size.


### Executing a volumes-clone request
{: #start-vol-clone-exec-req}

This step performs the remaining execution operation to create the cloned volumes from the available group snapshot.

#### Prerequisites
{: #start-vol-clone-exec-prereq}

The volumes-clone request must be in the `Available` state.


#### Executing volumes-clone request by using API and CLI command
{: #execute-vol-clone-api-cli}

After you initiate the `execute` operation, the initial `percentComplete` will be 0% and the status is set to `executing`.

Use the following API and CLI command to initiate the volumes-clone request:

- **API**: [Initiate the Execute action for a volumes-clone request](/apidocs/power-cloud#pcloud-v2-volumesclone-execute-post)
- **CLI**: [ibmcloud pi volume clone execute](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-execute)

You must provide values for the following parameters in the API and CLI commands:

- `volume-clones-id`: (Required) The unique identifier of a volumes-clone request. The identifier can be the volumes-clone ID or the volumes-clone name.
- `name`: (Required) The base name of the new cloned volumes. Cloned volume names are prefixed with `clone-` and suffixed with `-#####-N`. In the suffix, `#####` is a five-digit random number and `N` is an incremental number that starts with 1.
- `rollbackPrepare`: (Optional) Default value is `False`. When the flag is set to `False`, the system runs the failed rolls back clone activity but the prepared snapshot is left as-is. When the flag is set to `True`, the system runs the failure rollback clone activity and removes the prepared snapshot.
- `userTags`: (Optional) Provide the list of user tags to be attached to the cloned volumes.
- `targetReplicationEnabled`: (Optional) Use this flag to enable or disable replication for the cloned volumes. By default, the flag uses the replication status of the source volumes that are getting cloned. When set to `False` the cloned volumes are not enabled for replication. When set to `True` the cloned volumes are enabled for replication.

The storage pool where the source volumes reside must be enabled for replication, if the source volumes are not enabled for replication and you are enabling replication for the cloned volumes.
{: note}

- `targetStorageTier`: Provide the name of the storage tier for the cloned volumes. Use this field to clone a set of volumes from one storage tier to a different storage tier. Cloned volumes must remain in the same storage pool as the source volumes.


#### Restrictions and considerations
{: #start-vol-clone-res-cons}

You must consider the following restrictions and considerations before you start the volumes-clone request:

- A volumes-clone request is considered complete when the status of the volumes-clone request is changed to one of the `completed`, `failed`, or `cancelled` state.
- When the `volumes-clone execute` request is initiated, the initial status is set to `executing`.
- When the `execute` operation is completed successfully, the volumes-clone request status changes to `completed`.
- If an error occurs during the volume cloning process, any artifacts that are created by the cloning process are removed. The group snapshot is returned to the `available` state so that you can retry the `execute` operation.
- You can cancel a volumes-clone request when it is in the `executing` state.
- If you cancel the `execute` operation of a volumes-clone request, the status of the volumes-clone request is changed to `cancelling`.
- You can control the behavior of a failed `execute` operation by using the `rollbackPrepare` option. The default value of the `rollbackPrepare` option is `false`. The default value leads the failed `execute` operation to roll back the clone activity and does not remove the prepared snapshot. If the `rollbackPrepare` option is set to `true`, it leads the failed `execute` operation to roll back the clone activity and removes the prepared snapshot.


### Cancelling a volumes-clone request
{: #cancel-vol-clone-req}

The `Cancel a volumes-clone request` operation initiates the cleanup activity that performs the cleanup of the preparatory clones and snapshot volumes.

#### Prerequisites
{: #cancel-vol-clone-preq}

The volumes-clone request must be in the `Available` state.


#### Cancelling volumes-clone request by using API and CLI command
{: #cancel-vol-clone-api-cli}

After you initiate the `cancel` operation, the initial `percentComplete` will be 0% and the status is set to `cancelling`.

Use the following API and CLI command to cancel the volumes-clone request:

- **API**: [Cancel a volumes-clone request](/apidocs/power-cloud#pcloud-v2-volumesclone-cancel-post)
- **CLI**: [ibmcloud pi volume clone cancel](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-cancel)

You must provide values for the following parameters in the API and CLI commands:

- `volume-clones-id`:	(Required) The unique identifier of a volumes-clone request. The identifier can be the volumes-clone ID or the volumes-clone name
- `Force`: (Optional) Default status is `False`. The `cancel` operation is allowed only if the status is set to `prepared` or `available`. When the status is set to `True`, the `cancel` operation is allowed when the status is set to `NOT completed`, `cancelling`, `cancelled`, or `failed`.

#### Restrictions and considerations
{: #cancel-vol-clone-exec-req}

You must consider the following restrictions and considerations before you cancel the volumes-clone request:

- If you cancel the volumes-clone request, the initial status of the volumes-clone request is set to `Cancelling`. The status changes to `Cancelled` state when all the clean-up work is completed successfully.
- You can cancel a volumes-clone request when the volumes-clone request is in the `executing` state. The `force` option must be set to `True` in the `cancel` volumes-clone request.
- If the volumes-clone request is in the `Executing` state, any artifacts that are created by the clone operation process are removed.


### Deleting a volumes-clone request
{: #del-vol-clone-req}

When a volumes-clone request is no longer required, you can delete the request by initiating the volumes-clone delete operation.

#### Prerequisites
{: #del-vol-clone-prereq}

The volumes-clone request must be in one of these final statuses: `Completed`, `Failed`, or `Cancelled`.


#### Deleting a volumes-clone request by using API and CLI command
{: #delete-vol-clone-api-cli}

Use the following API and CLI command to delete the volumes-clone request:

- **API**: [Delete a volumes-clone request](/apidocs/power-cloud#pcloud-v2-volumesclone-delete)
- **CLI**: [ibmcloud pi volume clone delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-delete)

You must provide values for the following parameters in the API and CLI commands:

- `volume-clones-id`: (Required) The unique identifier of a volumes-clone request. The identifier can be the volumes-clone ID or the volumes-clone name.
- `Force`: (Optional) Force the cancellation of a volumes-clone request. The `cancel` operation is allowed only if the status is set to `prepared` or `available`. When the status is set to `True`, the `cancel` operation is allowed when the status is set to `NOT completed`, `cancelling`, `cancelled`, or `failed`.

#### Restrictions and considerations
{: #del-vol-clone-res-con}

If the volumes-clone request is not in one of the final statuses that is required for deletion, you can cancel the request, do any remaining cleanup, and transition the status to `Cancelled`. If the volumes-clone request is in the `Cancelled` status, the request can be deleted.

### Getting the status for a volumes-clone request
{: #get-vol-clone-req}


This API request returns detailed information about the status of the volumes-clone request. For example, the list of source volumes that are getting cloned and the list of cloned volumes when the `execute` operation is successfully completed.

#### Prerequisites
{: #get-vol-clone-prereq}

None.


#### Getting the status of volumes-clone request by using API and CLI command
{: #get-vol-clone-api-cli}


- **API**: [Get the status of a volumes clone request for the specified clone task ID](/apidocs/power-cloud#pcloud-v2-volumes-clonetasks-get)
- **CLI**: [ibmcloud pi volume clone get](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-get)

Provide a value for the `volume-clones-id` field. The value is the unique identifier of a volumes-clone request. The identifier can be the volumes-clone ID or the volumes-clone name.

#### Restrictions and considerations
{: #get-vol-clone-res-con}

None.


### Getting the list of volumes-clone request
{: #getlist-vol-clone-req}

The API request provides a list of all volumes-clone requests in a workspace and the status of each request.

#### Prerequisites
{: #getlist-vol-clone-prereq}

None.

#### Getting a list of volumes-clone request by using API and CLI command
{: #getlist-vol-clone-req-api-cli}


- **API**: [Get the list of volumes-clone request for a cloud instance](/apidocs/power-cloud#pcloud-v2-volumesclone-getall)
- **CLI**: [ibmcloud pi volume clone list](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-volume-clone-list)

Provide one of the values to the `filter` parameter from the following list:

- `prepare` - includes status values (preparing, prepared)
- `start` - includes status values (starting, available)
- `execute` - includes status values (executing, available-rollback)
- `cancel` - includes status values (cancelling)
- `completed` - includes status values (completed)
- `failed` - includes status values (failed)
- `cancelled` - includes status values (cancelled)
- `finalized` - included status values (completed, failed, cancelled)

#### Restrictions and considerations
{: #getlist-vol-clone-res-con}

You must consider the following restrictions and considerations before you get the list of volumes-clone requests:

- The detailed information about the source volumes or cloned volumes is not provided.

- The list can be limited by using the `filter` parameter. The filter is based on the status of the ‘filter’ parameter.


## Frequently asked questions
{: #snap-clone-faqs}

The following are some of the frequently asked questions on snapshots and cloning that are documented on the FAQ page:
- [What are the key differences between a snapshot and a clone?](/docs/power-iaas?topic=power-iaas-powervs-faqs#snap-vs-clone)
- [Are there any initial snapshot requirements in terms of storage?](/docs/power-iaas?topic=power-iaas-powervs-faqs#snap-storage-req)
- [Does the snapshot and volume clone support any safeguard policy?](/docs/power-iaas?topic=power-iaas-powervs-faqs#snap-clone-safeguard)
- [Can you tell me more about the backup process by using the PowerHA Toolkit for IBM i?](/docs/power-iaas?topic=power-iaas-powervs-faqs#poweha-toolkit)
