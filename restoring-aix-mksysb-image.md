---

copyright:
  years: 2019, 2023

lastupdated: "2023-04-04"

keywords: aix mksysb, aix helper vm, attaching new disk

subcollection: power-iaas

---

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

# Restoring an AIX mksysb image onto an IBM Power Systems Virtual Server instance
{: #restoring-aix-mksysb-image}

Learn how to restore an AIX `mksysb` image onto an IBM Power Systems Virtual Server instance
{: shortdesc}

The IPv6 interface that is used for VM management might be affected when you restore an AIX `mksysb` image. Before proceeding onto the next section, review [Recommended Reliable Scalable Cluster Technology (RSCT) package levels for imported AIX images](/docs/power-iaas?topic=power-iaas-recommended-rsct-package).
{: important}

## Defining an AIX Helper VM
{: #defining-aix-helper-vm}
{: help}
{: support}

You can use an existing AIX VM to copy an AIX mksysb archive. The `alt_disk_mksysb` command copies the mksysb archive onto a new volume. The `alt_disk_mksysb` command also gives you the option of rebooting from a specific disk image. 

Before you can copy an AIX `mksysb` archive, determine the amount of space the _helper VM_ needs to hold the _mksysb_ image. In the following example, the _mksysb_ image (`gdrh10v1.sysb`) is roughly 5.8 GB. Determining the space needed as follow:

```
:>ls -l gdrh10v1.sysb
-rw-r--r--  1 root   system    5806899200 Jul 18 2017 gdrh10v1.sysb
```
{: codeblock}

Next, you must identify a _helper VM_ file system with enough space to hold the mksysb image. If such a file system does not exist, you can attach a data volume as a _staging area_. To display information about a volume group, use the `lsvg` command.

```
# lsvg rootvg
VOLUME GROUP:       rootvg                  VG IDENTIFIER:      00f6db0a00004c000000016b94f02
VG STATE:           active                  PP SIZE:            32 megabyte(s)
VG PERMISSION:      read/write              TOTAL PPs:          639 (20448 megabytes)
MAX LVs:            256                     FREE PPs:           477 (15264 megabytes)
LVs:                12                      USED PPs:           162 (5184 megabytes)
OPEN LVs:           11                      QUORUM:             2 (Enabled)
TOTAL PVs:          1                       VG DESCRIPTIORS:    2
STALE PVs:          0                       STALE PPs:          0
ACTIVE PVs:         1                       AUTO ON:            yes
MAX PPs per VG:     32512
MAX PPs per PV:     1016                    MAX PVs:            32
LTG size(Dynamic):  512 kilobyte(s)         AUTO SYNC:          no
HOT SPARE:          no                      BB POLICY:          relocatable
PV RESTRICTION:     none                    INFINITE RETRY:      no
DISK BLOCK SIZE:    512                     CRITICAL VG:        no
FS SYNC OPTION:     no                      CRITICAL PVs:       no
#
```

Running the `df -g` command displays information about the total space and available space on a file system. In this instance, the `rootvg` volume group has enough space for creating a new file system, expanding an existing one, and storing the _mksysb_ source image.

The storage information is shown as follow:

```
# df -g
Filesystem          GB blocks       Free        %Used       Iused       %Iused      Mounted on
/dev/hd4                0.09        0.06        41%         2619        17%         /
/dev/hd2                2.16        0.26        89%        36565        37%         /usr
/dev/hd9var             0.19        0.16        17%          953         3%         /var
/dev/hd3                0.22        0.22         1%           33         1%         /tmp
/dev/hd1                0.03        0.03         2%            7         1%         /home
/dev/hd11admin          0.12        0.12         1%            5         1%         /admin
/proc                      -           -          -            -         -          /proc
/dev/hd10opt            0.44        0.05        90%        11651        49%         /opt
/dev/||vedump           0.25        0.25         1%            4         1%         /var/admin/ras/||vedump
#
```

## Attaching a new (disk) volume
{: #attaching-new-volume}

If your disk is not at the correct size, complete the following steps:

You must also complete these steps if you want to store the mksysb image in a data disk for shared access or long-term storage.
{: note}

1. Create a file system to hold the _mksysb_ archive.

2. Click **Add new** under **Attached volumes**.

3. Give your data volume a **Name**. Select the **Type**, **Size**, and make it **Shareable**. In the following example, _mksysbfs_ is the volume name and it has 20 GB of space for multiple _mksysb_ archive files:

4. After successfully attaching the _mksysbfs_ volume to the _helper VM_, log in to the VM. The volume appears as a new hdisk. Run the `lspv` and `cfgmgr` commands on the _helper VM_ to configure and show the new disk. The new disk is labeled as _hdisk1_.
    Using the lspv command:

    ```
    # lspv
    hdisk0        00f6db0acc7aece5        rootvg        active
    ```
    Using the cfgmr command:
    
    ```
    # cfgmr
    #lspv
    hdisk0        00f6db0acc7aece5        rootvg        active
    hdisk1        none                     none        
    #
    ```

5. Create an _AIX Volume Group_ by running the `mkvg` command. On the _helper VM_, _mksysbvg_ is the volume group name.

    ```
    mkvg -fy mksysbvg hdlsk1
    0516-1254 mkvg: Changing the PVID in the ODM.
    mksysbvg
    #
    ```

6. Run the `crfs` command to create a file system and the `mount` command to mount it. The following example shows a mounted file system (`/mksysb`) on the _helper VM_:

    ```
    #crfs -v jfs2 -a size=18G -m/mksysb -g mksysbvg
    File system created successfully.
    18873588 kilobytes total on disk space.
    New File System size Is 37748736
    # mount /mksysb
    # df -g /mksysb
    Filesystem      GB blocks       Free        %Used       Iused       %Iused      Mounted on
    /dev/fslv00         18.00      12.26          32%           6           1%      /mksysb
    #
    ```

After you complete these steps, you must decide on the best access option. IBM provides several different private access options. Each option allows VM instances with internal IP addresses to reach certain APIs and services.

Log on to the source VM where the source `mksysb` resides and copy the image to the _helper VM_ after you choose an option. In the following example, the customer is using Secure Copy Protocol (scp) from an on-premises system and copying it into the `/mksysb` file system of the _helper VM_:

If you did not decide on a private access option, or chose a different option for your internal IP access, your steps might vary.
{: note}

Running the cksum command:
```
 : >cksum gdrh10v1.sysb
371420133 5806899200 gdrh10v1.sysb
 : >scp gdrh10v1.sysb root@192.168.111.3:/mksysb/gdrh10v1.sysb
 root@192.168.111.3's password:
 gdrh10v1.sysb                                            100%
 ```

## Creating the alternate disk image volume
{: #creating-alternate-volume}

Log on to the helper VM and verify that the image under `/mksysb` has an identical `cksum` as the reported size from the on-premises system. After verifying the matching sizes, you can create a volume large enough to hold the restored root volume group.

To determine the necessary volume size of the alternate disk, examine the contents of the `bosinst.data` file within the mksysb archive. The `bosinst.data` file in the archive contains stanza information that indicates the minimum space that is required to restore the _mksysb_. An easy way to accomplish this is to usfe the `restore` command to extract the `./images/bosinst.data` file from the _mksysb_ archive.

Search the `bosinst.data` file and find the stanza that is named `target_disk_data`. This stanza indicates the minimum size in megabytes of the required volume in a `SIZE_MB = size` key value pair. The recorded size is used when creating the alternate disk image volume and attaching it to the _helper VM.

The restore -qf command:
<!-- check for errors -->
```
# restore -qf gdrh10v1.sysb ./bosinst.data
x ./bosinst.data
# grep -p target_disk_data bosinst.data
target_disk_data:
        PVID = 00c04e279d9ce46e
   PHYSICAL_LOCATION = U9117.MMC.0604E27-V9-C3-T1-L8100000000000000
        CONNECTION = vscsi0//810000000000
        LOCATION =
        SIZE_MB = 20480
        HDI SKNAME = hdisk0
```

To create and attach a new volume to **AIX-7200-03-03**, complete the following steps:

1. Click **Add new** under **Attached volumes**.

2. Create a data volume and enter the recorded size in gigabytes (it must be large enough to hold the restored root volume group) by selecting the correct options. For example, you can enter the volume name as **AIX-7200-03-03-altdisk**.

3. After successfully attaching the **AIX-7200-03-03-altdisk** volume to the _helper VM_, log on to the VM. Use the `cfgmgr` and `lspv` commands on the _helper VM_ to show the new disk. The new disk is named `hdisk2`.

Displaying storage information:

```
# cfgmgr
# lspv
hdisk0      00f6db0a6c7aece5        rootvg      active
hdisk1      00c25ab0056a002a        mksysbvg    active
hdisk2      none                    None
#
```

## Restoring the alternate disk mksysb
{: #restoring-alternate-disk}

You can now create an AIX boot disk from the source _mksysb_ archive. To create an AIX boot disk from the source _mksysb_ archive, run the `alt_disk_mksysb` command with the following options:

**-m**: Specify the mksysb archive that you transferred to the _helper VM_. In this example, the source mksysb archive is named `/mksysb/gdrh10v1.sysb`.
**-d**: Specify the logical disk (hdisk) that is empty of a volume group label. In the example, the target disk is named `hdisk2`.
**-c**: Use this option to set up a terminal device during VM deployment. Without a valid terminal, the VM does not boot if it needs to open the terminal for any reason.

After you run the `alt_disk_mksysb` command, the terminal displays information similar to the following output:

```
# alt_disk_mksysb -c /dev/vty0 -d hdi sk2 -m/mksysb/gdrh10v1.sysb
Restoring/image.data from mksysb image.
Checking disk sizes.
Creating cloned rootvg volume group and associated logical volumes. 
Creating logical volume alt_hd5.
Creating logical volume alt_hd6.
Creating logical volume alt_hd8.
Creating logical volume alt_hd4.
Creating logical volume alt_hd2.
Creating logical volume alt_hd9var. 
Creating logical volume alt_hd3.
Creating logical volume alt_hd1.
Creating logical volume alt_hd10opt.
Creating logical volume alt_hd11admin.
Creating logical volume alt_lg_dumpiv.
Creating logical volume alt_livedump.
Creating /alt_inst/ file system 
Creating /alt_inst/admin file system 
Creating /alt_inst/home file system 
Creating /alt_inst/opt file system 
Creating /alt_inst/tmp file system 
Creating /alt_inst/usr file system
Creating /alt_inst/var file system
Creating /alt_inst/var/adm/ras/livedump file system 
Restoring mksysb image to alternate disk(s).
Linking to 64bit kernel.
Changing logical volume names in volume group descriptor area. 
Fixing LV control blocks...
forced unmount of /alt_inst/var/adm/ras/livedump
forced unmount of /alt_inst/var/adm/ras/livedump
forced unmount of /alt_inst/var 
forced unmount of /alt_inst/var 
forced unmount of /alt_inst/usr 
forced unmount of /alt_inst/usr 
forced unmount of /alt_inst/tmp 
forced unmount of /alt_inst/tmp 
forced unmount of /alt_inst/opt 
forced unmount of /alt_inst/opt 
forced unmount of /alt_inst/home 
forced unmount of /alt_inst/home 
forced unmount of /alt_inst/admin 
forced unmount of /alt_inst/admin 
forced unmount of /alt_inst
forced unmount of /alt_inst
Fixing file system superblocks...
Bootlist is set to the boot disk: hdisk2 bl v=hd5
#
```

Now, the target volume contains a valid root volume group (`rootvg`) that is boot-ready. Additionally, the bootlist is set. Before rebooting, perform the following checks:

Perform a check by using the bootlist command:
```
# bootlist -m normal -o
hdisk2 blv=hd5 pathid=0
hdisk2 blv=hd5 pathid=1
hdisk2 blv=hd5 pathid=2
hdisk2 blv=hd5 pathid=3
# lspv
hdisk0      00f6db0a6c7aece5        rootvg      active
hdisk1      00c25ab0056a002a        mksysbvg    active
hdisk2      00c25ab0062fa576        altinst_rootvg
#
```

When you are ready for the new environment to take effect, reboot the disk by using the `shutdown -Fr` command.
The device configuration can take several minutes. Upon its completion, the system's login prompt appears and the newly restored system is ready for login.

AIX login prompt:

```
Last login: Sun Jul 21 08:09:27 2019 on /dev/pts/0 from 10.150.0.8
***********************************************************************************************
*                                                                                             *
*                                                                                             *
*       Welcome to AIX Version 7.2!                                                           *
*                                                                                             *
*       Please see the README file in /usr/lpp/bos for information pertinent to this release  *
*       of the AIX Operating System                                                           *
*                                                                                             *
************************************************************************************************
[YOU HAVE NEW MAIL]
root@aix-7200-03-03: /
 :> spv
hdisko      00f6db0a6c7aece5        old_rootvg
hdisk1      00c25ab0062fa576        rootvg          active
hdisk2      00c25ab0056a002a        mksysbvg        active
root@aix-7200-03-03: /
 :> sfs -a
Name                    Nodename    Mount Pt                VFS     Size          Options   Auto    Accounting
/dev/hd4                --          /                       jfs2    21823488        --      yes     no
/dev/hd1                --          /home                   jfs2    65536           --      yes     no
/dev/hd2                --          /usr                    jfs2    4390912         --      yes     no
/dev/hd9var             --          /var                    jfs2    458752          --      yes     no
/dev/hd3                --          /tmp                    jfs2    786432          --      yes     no
/dev/hd11admin          --          /admin                  jfs2    262144          --      yes     no
/proc                   --          /proc                   procfs  --              --      yes     no
/dev/hd10opt            --          /opt                    jfs2    2097152         --      yes     no
/dev/livedump           --          /var/adm/ras/livedump   jfs2    524288          --      yes     no
/dev/fslv00             --          /mksysb                 jfs2    37748736        --      no      no
root@aix-7200-03-03: /
 :>
```

You have successfully restored the AIX _mksysb_ archive and the environment is ready for your use.

## (Optional) Detaching the staging volume
{: #detaching-staging-volume}

In the previous section, we used a separate image volume for storing the source _mksysb_. To detach, keep, or delete a volume, review the following information.

After the completion of the `alt_disk_mksysb` command, you can detach the staging volume (`mksysbvg`) from the _helper VM_. Before you detach the staging volume, you must close all available file systems by unmounting them. If no action is required, then it is safe to remove the volume group definition from the _helper VM_.

1. Use the `varyoffvg` and `exportvg` commands to remove the _mksysbvg_ volume group.   

    Using the varyoffvg and exportvg commands:
    ```
    root@aix-7200-03-03: / 
     :>lsvg -l mksysbvg
    mksysbvg:
    LV NAME        TYPE        LPs         PPs         PVs         LV STATE        MOUNT POINT
    loglv00        jfs2l og    1           1           1           closed/syncd    N/A
    fslv00         jfs2        576         576         1           closed/syncd    /mksysb
    root@aix-7200-03-03: / 
     :>varyoffvg mksysbvg 
    root@aix-7200-03-03: / 
    :>exportvg mksysbvg 
    root@aix-7200-03-03: / 
     :>lsvg
    old_rootvg
    rootvg
    root@aix-7200-03-03: /
     :>lspv
    hdisk0          00f6db0a6c7aece5            old_rootvg
    hdisk1          00c25ab0062fa576            rootvg            active
    hdisk2          00c25ab0056a002a            none
    root@aix-7200-03-03: /
     :>
    ```
2. Upon the successful removal of the volume group definition, remove the disk definition by using the `rmdev` command.

    ```
    root@aix-7200-03-03: /
     :>lspv
    hdisk0         00f6db0a6c7aece5            old_rootvg
    hdisk1         00c25ab0062fa576            rootvg             active
    hdisk2         00c25ab0056a002a            None
    root@aix-7200-03-03: / 
    :>rmdev - dl hdisk2
    hdisk2 deleted
    root@aix-7200-03-03: /
     :>lspv
    hdisk0         00f6db0a6c7aece5            old_rootvg
    hdisk1         00c25ab0062fa576            rootvg             active
    root@aix-7200-03-03: /
     :>
    ```

3. You can now detach the image volume (disk) containing the source mksysb from the _helper VM_. To detach the disk from **AIX-7200-03-03**, select **Manage existing volumes** and click a volume.

4. After you successfully detach the disk from **AIX-7200-03-03**, you can attach the saved image volume to other VM instances.
