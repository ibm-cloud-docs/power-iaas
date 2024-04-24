---

copyright:
  years: 2019, 2023

lastupdated: "2023-04-04"

keywords: aix mksysb, aix helper vm, attaching new disk

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Replicating a desired AIX configuration in {{site.data.keyword.powerSysFull}} using an AIX mksysb image
{: #restoring-aix-mksysb-image}

Learn how to create and restore an AIX `mksysb` image onto an {{site.data.keyword.powerSysFull}} instance.
{: shortdesc}

A simple way to migrate a local AIX environment (or workload) into {{site.data.keyword.powerSys_notm}} is to restore an operating system `rootvg` backup over an existing image and then migrate the data. The `rootvg` backup is created with the AIX `mksysb` command. The restored mksysb image applies the AIX configuration details while preserving the {{site.data.keyword.powerSys_notm}} deployed storage and networking resources.

when the restored AIX configuration is active, various methods can be used to migrate applications and related data. Those methods are outside the scope of this page.

It is assumed the reader has AIX administration experience and is familiar with deploying a {{site.data.keyword.powerSys_notm}} AIX instance by using the {{site.data.keyword.powerSys_notm}} user interface or the ibm cloud CLI.

## Considerations before creating the mksysb image on the source AIX instance
{: #consider-image-source-AIX}

1. Ensure that the installed RSCT package is at version 3.2.6.2 or later. The `/opt/rsct/install/bin/ctversion` command can be used to display the installed version. More information can be found at [Recommended Reliable Scalable Cluster Technology (RSCT) package levels for imported AIX images](/docs/allowlist/power-iaas?topic=power-iaas-recommended-rsct-package).

2. The AIX environment should be running an AIX version and technology level that is in standard support. For AIX levels that are under an extended support model, arrangements should be made to obtain an extended support agreement to cover the use of the AIX level in {{site.data.keyword.powerSys_notm}}.

Consult the [General AIX support lifecycle information](https://www.ibm.com/support/pages/aix-support-lifecycle-information) and [FAQ on OS versions that are supported](/docs/allowlist/power-iaas?topic=power-iaas-powervs-faqs#os-versions) for more details.

The AIX instance that is deployed in {{site.data.keyword.powerSys_notm}} should be at the same AIX version as the source AIX instance. For example, if the source instance is at AIX 7.2, then the deployed {{site.data.keyword.powerSys_notm}} instance should also be a 7.2 based image.

The AIX technology levels (TL) do not need to match, but you might consider using the latest TL that is available from the {{site.data.keyword.powerSys_notm}} stock images.
{: important}

1. Ensure that that NPIV file sets are installed in the AIX environment as {{site.data.keyword.powerSys_notm}} VMs use the NPIV storage virtualization model. This can be checked by using the lslpp command as follows.


```
#
# lslpp -l devices.vdevice.IBM.vfc-client.rte
  Fileset                      Level     State      Description
  -------------------------------------------------------------

Path: /usr/lib/obj repos
  devices.vdevice.IBM.vfc-client.rte
                            7.1.5.38     COMMITTED  Virtual Fibre Channel Client Support


Path: /etc/obj repos
  devices.vdevice.IBM.vfc-client.rte
                            7.1.5.38     COMMITTED  Virtual Fibre Channel Client Support

#
```
{: screen}

4. Verify that the AIX initab file does not contain entries with dependencies on unique aspects of the source environment that would not be present in {{site.data.keyword.powerSys_notm}}. Otherwise, the converted {{site.data.keyword.powerSys_notm}} AIX instance might not boot. Similarly, if other boot time actions exist such as NFS file system mounts, those might need to be disabled.

5. {{site.data.keyword.powerSys_notm}} uses IBM Storage with the built-in AIX MPIO driver. Make sure that the I/O configuration of the source LPAR does not conflict with the use of AIX MPIO.

6. Delete any temporary files or files, especially large files that are not needed on the target {{site.data.keyword.powerSys_notm}} AIX instance. The `-e` and `-x` mksysb options can also be used to exclude unneeded directories and file systems in rootvg. This reduces the size of the mksysb image for transfer to {{site.data.keyword.powerSys_notm}}.

## Creating the mksysb image on the source AIX instance
{: #create-image-source-AIX}

Refer to the [mksysb](https://www.ibm.com/docs/en/aix/7.3?topic=m-mksysb-command) documentation for full details. Ensure that there is sufficient file system space to hold the produced mksysb image. Generally, 10 to 15 GB is sufficient depending on additional non-AIX data added to the rootvg. The following example mksysb creates the image in /tmp. The `-i` builds the image from the latest rootvg details and the `-b` option can potentially improve the performance when creating the mksysb image. The `-X` mksysb option expands `/tmp` if needed for the boot image. This can be omitted if the available space is known to be sufficient.

```
# create the mksysb image
mksysb -i -X -C -b 512 /tmp/my-mksysb
```

Once the mksysb image is created, the storage volume size that is needed for the restore of the image can be extracted as follows. In this example, a 25 GB volume would be needed.


```
#
# restore -qf ./my-mksysb ./bosinst.data
x ./bosinst.data
# fgrep -p target_disk_data bosinst.data|fgrep SIZE_MB
        SIZE MB = 25600
# rm bosinst.data
#
```
{: screen}

Also, capture the image checksum for verification once the image is transferred to a {{site.data.keyword.powerSys_notm}} AIX instance for restoration.


```
#
# cksum ./my-mksysb
1999777825 1861746688 ./my-mksysb
#
```
{: screen}

## Creating a {{site.data.keyword.powerSys_notm}} AIX instance for conversion with an mksysb image
{: #create-aix-conversion-vm}
{: help}
{: support}

An AIX instance is needed in {{site.data.keyword.powerSys_notm}} that can be converted with the mksysb image.

The instance must be at the same AIX version as the AIX instance where the mksyb image was created. {{site.data.keyword.powerSys_notm}} provides a set of stock images that can be used to facilitate the conversion. When deployed, the AIX instance needs some updates to host the mksysb image. Choose the needed stock image and deploy a new {{site.data.keyword.powerSys_notm}} AIX instance via the user interface or CLI with the cpu, memory, and network details that are needed for the final converted instance.

For example, if an AIX 7.2 based mksysb image is being used, choose the `7200-05-05` stock image. When deploying the instance, attach an additional storage volume with sufficient capacity for the mksysb image restore. Use the information from the bosinst.data file to get the minimum needed size in Megabytes. Below is an example AIX 7.2 deployed instance with an additional 30 GB volume (hdisk1).

The following details should be observed with the deployed AIX instance.


```
#
# oslevel -s
7200-05-05-2246
# lspv
hdiskO          00fa00d66c59c9d7          rootvg       active
hdiskl          none                      None
# bootinfo -s hdiskl
30720
#
```
{: screen}

To make room for the mksysb image, disk space must be freed in the instance to hold it. This can be done by removing the `/usr/sys/inst.images` file system and creating a new one called `/mksysb-staging`.

This should result in sufficient space for most mksysb image use cases. If more space is needed, then a new larger storage volume needs to be attached to the instance with the {{site.data.keyword.powerSys_notm}} user interface and a JFS2 file system will need to be created on it. The below example removes `/usr/sys/inst.images` and creates a new 12 GB `mksysb-staging` file system.



```
#
# umount /usr/sys/inst.images
# rmfs -r /usr/sys/inst.images
rmlv: Logical volume repo00 is removed.
#
```
{: screen}


```
#
# crfs -v jfs2 -g rootvg -m /mksysb-staging -a size=12G
File system created successfully.
12582324 kilobytes total disk space.
New File System size is 25165824
# mount /mksysb-staging
# mount
  node       mounted        mounted over    vfs       date        options
-------- ---------------  ---------------  ------ ------------ ---------------
         /dev/hd4         /                jfs2   Oct 11 17:47 rw,log=/dev/hd8
         /dev/hd2         /usr             jfs2   Oct 11 17:47 rw,log=/dev/hd8
         /dev/hd9var      /var             jfs2   Oct 11 17:47 rw,log=/dev/hd8
         /dev/hd3         /tmp             jfs2   Oct 11 17:48 rw,log=/dev/hd8
         /dev/hd1         /home            jfs2   Oct 11 17:48 rw,log=/dev/hd8
         /dev/hdlladmin   /admin           jfs2   Oct 11 17:48 rw,log=/dev/hd8
         /proc            /proc            procfs Oct 11 17:48 rw
         /dev/hd10opt     /opt             jfs2   Oct 11 17:48 rw,log=/dev/hd8
         /dev/lLivedump   /var/adm/ras/livedump jfs2   Oct 11 17:48 rw,log=/dev/hd8
         /ahafs           /aha             ahafs  Oct 11 17:49 rw
         /dev/fslv00      /mksysb-staging  jfs2   Oct 11 18:35 rw,log=/dev/hd8
#
```
{: screen}

In the above example, hdisk1 is the free storage volume where the mksysb image is restored.

Once the {{site.data.keyword.powerSys_notm}} instance is created, the mksysb image is placed into the /mksysb-staging directory. Transferring the mksysb image to the `/mksysb-staging` directory depends on your connectivity options to the IBM Cloud and {{site.data.keyword.powerSys_notm}} workspace.

For example, if you are able to access your {{site.data.keyword.powerSys_notm}} instance over a network connection from your local system where the mksyb image resides, you might use scp.

For example,
`# scp ./my-mksysb root@xxx.xxx.xxx.xxx:/mksysb-staging`

Use the `cksum` command to confirm the `my-mksysb` image file was successfully transferred.

Now the mksysb image can be restored onto the attached free storage volume that will become the new rootvg boot disk with the configuration from the source AIX instance. This is done by using the [alt_disk_mksysb](https://www.ibm.com/docs/en/aix/7.3?topic=alt-disk-mksysb-command) command. In the example mksysb restore below, `alt_disk_mksysb` sets hdisk1 as the boot disk for subsequent boots.

```
alt_disk_mksysb -c /dev/vty0 -d hdisk1 -m /mksysb-staging/my-mksysb
```

Once this completes successfully, an `lspv` indicates that hdisk1 is now the altinst_rootvg.


```
#
# lspv
hdisk0          00fa00d66c59c9d7              rootvg          active
hdisk1          00c939202144313b              altinst_rootvg
```
{: screen}

The AIX `bootlist` command can be used to confirm that hdisk1 is now the active AIX boot disk.


```
#
# bootlist -m normal -o
hdiskl blv=hd5 pathid=0
hdiskl blv=hd5 pathid=1
hdiskl blv=hd5 pathid=2
hdiskl blv=hd5 pathid=3
hdiskl blv=hd5 pathid=4
#
```
{: screen}

The AIX instance can be rebooted to the new hdisk1 rootvg.

`sync;sync;shutdown -Fr`

Once the AIX instance restarts, it has been converted with the mksysb image. An `lspv` shows hdisk1 as the new rootvg.


```
#
# lspv
hdisk0          00fa00d66c59c9d7              old_rootvg
hdisk1          00c939202144313b              rootvg         active
#
```
{: screen}

Before proceeding, consider running some basic tests on your new converted {{site.data.keyword.powerSys_notm}} AIX instance.

1. Run `oslevel -s` to confirm that the converted lpar matches the AIX level from the source system where the mksysb backup was created. More detailed verification can optionally be done by using the `lslpp -h` command.

2. Using the user interface, do testing by changing the CPU and RAM with your instance. You might also try adding and removing a small storage volume. These tests confirm that the instance is properly interacting with PowerVM dynamic LPAR operations for live resource updates to the instance.

Now the `old_rootvg` storage volume (hdisk0) can be detached from the instance and deleted by using the user interface. First, remove the volume from the AIX configuration with the `rmdev` command.

`# rmdev -dl hdisk0`

Before detaching the `old_rootvg` volume (hdisk0), you need to set the new rootvg volume (hdisk1) to bootable and the `old_rootvg` volume to not bootable in {{site.data.keyword.powerSys_notm}}.

Complete the following steps in {{site.data.keyword.powerSys_notm}} user interface under the details of the AIX instance in the `Attached volumes` section:

- Change the bootable indicator of the new rootvg volume from **off** to **on**.
- Set the bootable indicator of the old boot volume from **on** to **off**.

This allows the old boot volume to be detached and deleted in the {{site.data.keyword.powerSys_notm}} user interface. This can also be done by using the IBM Cloud CLI.


When the old boot volume is detached and deleted by using the user interface, the conversion of the AIX instance by using the mksysb is complete with a single rootvg volume. Now the instance is ready for installation of applications and related data.

## Additional Information Resources
{: #restore-aix-image-resources}

* [Getting Started with IBM Power Systems Virtual Servers](/docs/allowlist/power-iaas?topic=power-iaas-getting-started).
* [{{site.data.keyword.powerSys_notm}} CLI Reference](https://cloud.ibm.com/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference).
