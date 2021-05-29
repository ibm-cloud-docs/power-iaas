---

copyright:
  years: 2020, 2021

lastupdated: "2020-04-19"

keywords: aix mksysb, volume group, backup multiple volumes, savevg, dd command

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

# Moving data to the cloud
{: move-data-to-cloud}

Depending on your network bandwidth and size constraints, data moving process is as simple as creating an *OVA* or *mksysb* (root volume group) image, and a set of *savevg* images for data volumes. By using an *OVA* or *mksysb* image, you can build or provision a VM and then proceed to migrate the data volume groups of the VM by using the **restvg** command.

You can use following methods to back up your on-premise data and move the data to IBM {{site.data.keyword.powerSys_notm}}.

## Migrating volume group data by using the *savevg* command
{: migrate-data-using-savevg}

A volume group is a collection of physical volumes of various sizes and types. When a physical volume is assigned to a volume group, the physical blocks of storage media are organized into physical partitions of a size that you specify when you create the volume group. You can use built-in AIX *savevg* and *restvg* commands to back up and restore non-root volume groups. The *savevg* and *restvg* commands simplify the creation of your new volume groups and file systems on your new VM.

The *savevg* command finds and backs up all files that belong to a specified volume group. The volume group must be varied-on, and the file systems must be mounted. The *savevg* command uses the data file created by the *mkvgdata* command.

Use the following command to find and back up all files in a specific volume group.

```
# savevg –f <destination path> -i <non root vg files to be backed up>
```
{: codeblock}

For example:

```
# savevg –f /home/admin01/datavg_bkup –i  datavg
```

## Backing up multiple volume groups by using the *mkvgdata* and *restvg* commands
{: multiple-volume-backups}

Small systems might require only one data volume group to contain all the physical volumes for the non-root volume data. You might want to create separate volume groups, for security reasons, because each volume group can have its own security permissions. Separate volume groups are easier to maintain because if a volume group stops working, other volume groups can remain active.

Run the following commands to back up multiple volume groups:

```
# lsvg -o | xargs -i mkvgdata {}
# tar -cvf /backup/vgdata.tar /tmp/vgdata
```
{: codeblock}

Run the *mkvgdata* command for each online volume group to generate output file that contains information about the volume group in `/tmp/vgdata` directory. The resulting output file is compressed and stored in the `/backup` file system directory. This output file contains information regarding all volume groups, logical volumes, and file systems that can be used as a single image. The resulting image can be transferred or stored within an *mksysb* backup if the `/backup` directory is located on *rootvg*.

Run the following command to recreate the volume groups, logical volumes, and file systems:

```
# tar -xvf /backup/vgdata.tar
```

Now edit the `/tmp/vgdata/{volume group name}/{volume group name}.data file` and look for the line with `VG_SOURCE_DISK_LIST=`. Change the line to have the *hdisks*, *vpaths*, or *hdiskpowers* based on your requirement.

For example:

```
# restvg -r -d /tmp/vgdata/{volume group name}/{volume group name}.data
```

## Migrating raw partitions by using the dd command
{: migrating-raw-partitions}

The output file of the *savevg* command can be restored by using the *restvg* command. The size of a *savevg* backup file is small in comparison to the size of the physical volumes in the volume group. If the environments have data more than several TBs, the prescribed method of moving volume data by using *savevg* may present a disadvantage when considering transference and restoration procedures.

You can use the *savevg* command to back up volume groups. All logical volume information, Journaled File System (JFS), and JFS2 mounted file systems are archived. However, you can not use the *savevg* command to back up raw logical volumes.

Use the following methods to back up and restore content of a file system:

1. Unmount the file system.
2. Save the raw logical volume content into a file by running the following command:

```
  # dd if=/dev/lvname of=/file/system/lvname.dd
```
{: codeblock}

This command creates a copy of logical volume **lvname** to a file **lvname.dd** in file system `/file/system`. Make sure that the specified directory where the output file is stored (`/file/system` in the example) has enough disk space available to hold a full copy of the logical volume. If the logical volume is 100 GB, you need 100 GB file system space for the logical volume copy.

On the destination server, recreate the logical volume and the file system. If you are using an unmounted file system, run the following command to restore the backup copy:

```
# dd if=/file/system/lvname.dd of=/dev/lvname
```
{: codeblock}


