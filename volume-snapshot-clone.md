---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-13"

keywords: volume, snapshot, clone, restore, powervc

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

# Snapshotting, cloning and restoring a volume
{: #volume-snapshot-clone}

Learn more about snapshotting, cloning, and restoring a {{site.data.keyword.powerSysShort}} volume.

![Snapshot and clone API use cases](./images/snapshot-clone-use-cases.png "Snapshot and clone API use cases"){: caption="Figure 2. Snapshot and clone API use cases" caption-side="bottom"}



## Taking a snapshot
{: #volume-snapshot}

**Prerequisites**

Before you take a snapshot, ensure that all of the data is flushed to the disk. If you take a snapshot on a running virtual machine (VM) and did not flush the file system, you might lose some content.

**Use cases**

- Taking a snapshot of a VM targeting only the boot volume
- Taking a snapshot of a VM targeting only data volumes
- Taking a snapshot of a VM targeting all volumes (both boot and data)
- Taking multiple snapshots of a single VM (the snapshots must be taken one at a time)
- Taking multiple snapshots of different VMs at the same time

**Restrictions and considerations**

- Parallel VM snapshot operations for the same shared volume fail. You must perform these VM snapshot operations serially.
- You cannot restore a VM if you are taking a snapshot and there are clone (full-copy) *flashcopy* operations running in the background. The flashcopy operations must first complete.
- You cannot restore a VM if the background *flashcopy* operation fails for whatever reason.

## Restoring a virtual machine (VM)
{: #volume-restore}

**Prerequisites**

While performing a VM restore operation, you must ensure that all of you've quiesced all of your applications and there are no active IO operations on the volume. If you perform the restore operation on a running VM with mounted disks, the operation might corrupt the file system, putting the VM in maintenance mode.

**Use cases**

- Restoring all of the volumes that are part of a VM snapshot
- Running multiple VM restore operations (considering there are no shared volumes)
- Retrying a VM restore operation if it originally failed
- Rolling back a VM to its original volume state

**Restrictions and considerations**

- PowerVC takes a backup snapshot of all of the volumes that are intended to be restored before it performs the restore operation. The backup snapshot operation ensures that you can rollback the VM back to its original state if a failure happens during the restore operation.
- If the VM restore operation fails, the VM enters an **Error** state. You can either retry the restore operation or rollback the VM to its original volume state.
- If you choose to restore a shared volume on one VM, you cannot perform the snapshot, restore, clone, or capture operations on the other VMs that are using the shared volume (while the restore operation is running).

## Troubleshooting
{: #snapshot-troubleshooting}

When you clone and attach a volume to the same PVM as the PVM containing the original volume, the PVIDs of both volumes are found to be the same on your AIX operating system. to resolve this issue. Enter the following commands to resolve this issue:

1. `chdev -a pv=clear -l hdisk2`
2. `recreatevg -y copyvg hdisk2`
3. `mount /fs/<original-mount-point>`

In this example, `hdisk2` refers to the cloned volume name and `copyvg` is the name to be given to the newly created volume group. The `recreatevg` command creates a new file system with the same name as the original but in the `/fs` path. For more information, see section B under [Possible Cause and Solution 2: The Disks Are Copies of Each Other](https://www.ibm.com/support/pages/resolving-lvm-and-hard-disk-pvid-issues){: new_window}{: external}.
