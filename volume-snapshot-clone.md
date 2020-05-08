---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-11"

keywords: volume snapshot, clone, restore

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Snapshotting, cloning, and restoring a volume
{: #volume-snapshot-clone}

Learn more about snapshotting, cloning, and restoring a {{site.data.keyword.powerSysShort}} volume.

![Snapshot and clone API use cases](./images/snapshot-clone-use-cases.png "Snapshot and clone API use cases"){: caption="Figure 1. Snapshot and clone API use cases" caption-side="bottom"}

## Taking a snapshot
{: #volume-snapshot}

**Best Practices**

- Before you take a snapshot, ensure that all of the data is flushed to the disk. If you take a snapshot on a running virtual machine (VM) and did not flush the file system, you might lose some content.

**Use cases**

- Taking a snapshot of a VM targeting only the boot volume
- Taking a snapshot of a VM targeting only data volumes
- Taking a snapshot of a VM targeting all volumes (both boot and data)
- Taking multiple snapshots of a single VM (the snapshots must be taken one at a time)
- Taking multiple snapshots of different VMs at the same time

**Restrictions and considerations**

- Parallel VM snapshots operations for the same shared volume is not allowed. 
- You cannot restore a VM if you are taking a snapshot and there are clone (full-copy) *FlashCopy* operations that are running in the background. The FlashCopy operations must first complete.

## Restoring a virtual machine (VM)
{: #volume-restore}
Restores all the volumes which are part of a VM snapshot. While restoring the VM, it creates a backup snapshot which can be used in case the restore operation fails. If the restore operation succeeds the backup snapshots are deleted. In case of failure, user can perform restore-retry to re-attempt the restore for the failed snapshot, or can perform restore-rollback to restore the VM using the backup snapshot. On restore failure VM enters an **Error** state.

**Prerequisites**

By default VM restore operations expects the VM to be in ShutOff state, to ensure there is no data corruption while performing restore.
If the VM has volumes hosting external DB application, it is recommended that all your applications are quiesced, and there are no active IO transactions on the disk. This can lead to data corruption and put the VM in maintenance mode.

**Use cases**

- Restoring all of the volumes that are part of a VM snapshot
- Running multiple VM restore operations (considering there are no shared volumes)
- Retrying a VM restore operation if it originally failed
- Rolling back a VM to its original volume state

**Restrictions and considerations**

- If restore operation is failed, it is recommended to get the issue analyzed by storage support administrator. Failed restore can leave behind incomplete fcmaps which requires manual cleanup before restore-rety is attempted.
- If you choose to restore a shared volume on one VM, you cannot perform the snapshot, restore, clone, or capture operations on the other VMs that are using the shared volume (while the restore operation is running).

## Cloning a volume
{: #cloning-volume}
Cloning a volume creates the full copy. User can select multiple volumes and attempt a group clone. When multiple volumes are selected clone operations ensures that consistent data copy is created.

**Prerequisites**

You **must** assign a storage template to all of the volumes you select as clone volumes.

**Use cases**

- Cloning multiple volumes in an available state
- Cloning multiple volumes that are attached to the VM

**Restrictions and considerations**

- When clone is performed on an in-use volume, the {{site.data.keyword.powerSys_notm}} service creates the consistent group snapshot and re-creates the cloned volume copy by using the group snapshot.
