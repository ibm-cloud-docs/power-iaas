---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-05"

keywords: troubleshooting, hung virtual machine, support, help, system management services, SMS, object data manager, improving performance, suboptimal, lsattr

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting AIX-related issues
{: #troubleshoot-iaas-aix}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Learn how to troubleshoot {{site.data.keyword.powerSysShort}} AIX-related issues.
{: shortdesc}

## What can I do if my AIX virtual machine (VM) does not initially boot?
{: #troubleshoot-hung-aix}
{: troubleshoot}

Symptoms: The AIX boot disk that you are using to provision an AIX VM is not successfully booting. As a result, the console displays a blank screen without standard debugging options.

Causes: The AIX boot disk might be corrupted.

Resolve: If the AIX VM does not boot, you must provision an extra AIX VM and use it as a Network Installation Management (NIM) server. Without a NIM server, you cannot debug the boot issue and must reimage your disk.

1. Determine the hostname and IP address of the system by using the following two commands:
- `hostname` and
- `ifconfig -a`

2. Using the information from the previous step, add an entry for your hostname and IP address into `/etc/hosts`. For example, `echo "192.168.0.15 aix-7100-05-04" >> /etc/hosts`.

3. Run the following command:

```code
nim_master_setup -a device=/usr/sys/inst.images -a mk_resource=no
```

4. Once completed, the NIM master file set is installed and the basic resource objects created.
    The administrator is now able to add more NIM clients and define resources.

For more information, see [Setting up NIM to boot into maintenance mode](https://www.ibm.com/support/pages/setting-nim-boot-maintenance-mode){: external}. If you are unfamiliar with this process, create a [new support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## My AIX VM Tier 1 (NVMe-based Flash Storage) disk is running at a suboptimal level. What can I do to improve its performance?
{: #troubleshoot-slow-aix}
{: troubleshoot}

Symptoms: Your AIX VM with a Tier 1 (NVMe-based Flash Storage) disk is running the following NVMe specifications.

Causes: The AIX Tier 1 (NVMe-based Flash Storage) disk's default settings are hindering optimal performance.

Resolve: To improve disk performance, increase its **queue_depth** to *64* or *128* and change the algorithm to **shortest_queue** with a **no_reserve policy**. These modifications can improve performance by up to 50%.

To look at your AIX disk's current settings, enter the following commands:

- `lsattr -El hdiskX -a algorithm`
- `lsattr -El hdiskX -a reserve_policy`
- `lsattr -El hdiskX -a queue_depth`

In the output of these `lsattr` commands, you will see either **True** or **True+** at the very end. **True** indicates that the attribute is user-changeable. **True+** indicates that the attribute is user-changeable, and can be modified while the disk is open by using the *-U* flag.
{: tip}

You can set your disk's **queue_depth** to *64* and change the algorithm to **shortest_queue** with a **no_reserve policy** by using the following command:

```code
chdev -l hdiskX -a algorithm=shortest_queue -a reserve_policy=no_reserve -a queue_depth=64
```

If the AIX disk is open, an error message appears that states that the disk is busy. To prevent this error from occuring, add a *-U* flag to the `chdev` command and the values are updated without disruption (assuming the Object Data Manager (ODM) for the disk has that feature that is enabled).
