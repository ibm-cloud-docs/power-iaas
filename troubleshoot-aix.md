---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-03"

keywords: troubleshooting, hung virtual machine, support, help, system management services, SMS, object data manager, improving performance, suboptimal

subcollection: power-iaas

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Troubleshooting AIX-related issues
{: #troubleshoot-iaas-aix}

Learn how to troubleshoot {{site.data.keyword.powerSysShort}} AIX-related issues.
{: shortdesc}

## What can I do if my AIX virtual machine (VM) does not initially boot?
{: #troubleshoot-hung-aix}
{: troubleshoot}

{: tsSymptoms}
The AIX boot disk that you are using to provision an AIX VM is not successfully booting. As a result, the console displays a blank screen without standard debugging options.

{: tsCauses}
The AIX boot disk might be corrupted.

{: tsResolve}
If the AIX VM does not boot, you must provision an additional AIX VM and use it as a Network Installation Management (NIM) server. Without a NIM server, you cannot debug the boot issue and must reimage your disk.

1. Determine the hostname and IP address of the system by using the following two commands, `hostname` and `ifconfig -a`.

    ![Determining your hostname and IP address](./images/terminal-aix-hostname.png "Determining your hostname and IP address"){: caption="Figure 1. Determining your hostname and IP address" caption-side="bottom"}

2. Using the information from the previous step, add an entry for your hostname and IP address into `/etc/hosts`. For example, `echo "192.168.0.15 aix-7100-05-04" >> /etc/hosts`.

3. Run the following command, `nim_master_setup -a device=/usr/sys/inst.images -a mk_resource=no`.

    ![Creating a NIM master](./images/terminal-aix-nim.png "Creating a NIM master"){: caption="Figure 2. Creating a NIM master" caption-side="bottom"}

4. Once completed, the NIM master file set has been installed and the basic resource objects created. The administrator is now able to add more NIM clients and define resources.

    ![NIM master installation summary](./images/terminal-aix-nim-summary.png "NIM master installation summary"){: caption="Figure 3. NIM master installation summary" caption-side="bottom"}

For more information, see [Setting up NIM to boot into maintenance mode](https://www.ibm.com/support/pages/setting-nim-boot-maintenance-mode){: new_window}{: external}. If you are unfamiliar with this process, create a [new support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## My AIX VM Tier 1 (NVMe-based flash storage) disk is running at a suboptimal level. What can I do to improve its performance?
{: #troubleshoot-slow-aix}
{: troubleshoot}

{: tsSymptoms}
Your AIX VM with a Tier 1 (NVMe-based flash storage) disk is running below NVMe specifications.

{: tsCauses}
The AIX Tier 1 (NVMe-based flash storage) disk's deafult settings are hindering optimal performance.

{: tsResolve}
To improve your AIX VM performance, increase your disk's **queue_depth** to *64* or *128* and change its algorithm to **shortest_queue** with **no_reserve policy**. These changes can improve performance up to %50.

To look at the current settings for your AIX disk, enter the following commands:

1. `lsattr -El hdiskX -a algorithm`
2. `lsattr -El hdiskX -a reserve_policy`
3. `lsattr -El hdiskX -a queue_depth`

In the output of these `lsattr` commands, you'll see either **True** or **True+** at the very end. **True** indicates that the attribute is changeable by the user. **True+** indicates that the attribute is user changeable, and can be changed while the disk is open using the *-U* flag.
{: tip}

You can set your disk's **queue_depth** to *64* and changes its algorithm to **shortest_queue** with **no_reserve policy** with the following command:

chdev -l hdiskX -a algorithm=shortest_queue -a reserve_policy=no_reserve -a queue_depth=64
{: codeblock}

If the disk is currently open, you will receive and error message about the device being busy. To prevent this error message from appearing, add a *-U* flag to the above command and the values are updated without disruption (assuming the Object Data Manager (ODM) for the disks has that feature enabled).
{: note}


The ODM in AIX for IBM storage devices does have it enabled.....some third party ODM for third party storage may not.   In the output of the lsattr commands above, the last thing on the line is either "True" or "True+".  "True" says that the attribute is changeable by the user; "True+" means that it is user changeable, and can be changed while the disk is open using the -U flag.