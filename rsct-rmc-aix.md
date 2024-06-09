---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-08"

keywords: rsct, rmc, IPv6, Reliable Scalable Cluster Technology, RSCT package, Resource Management Control, RMC

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Recommended Reliable Scalable Cluster Technology (RSCT) package levels for imported AIX images
{: #recommended-rsct-package}

RSCT is a set of software components that together provides a comprehensive clustering environment for AIX&reg;, Linux&reg;, Solaris, and Windows&reg; operating systems. RSCT is the infrastructure that is used by various IBM products to provide clusters with improved system availability, scalability, and ease of use. For the {{site.data.keyword.powerSysFull}} offering, RSCT 3.2.1 is the minimum package level that is required for an imported AIX image (provides IPv6 support). However, the {{site.data.keyword.powerSys_notm}} development team recommends that you use [RSCT 3.2.6.2](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/navigation/welcome.html){: external} for optimal performance.
{: shortdesc}

The RSCT `nodeid` is not rebuilt if you are deploying an AIX VM from a network installation management (NIM) server without `cloud-init`, and RSCT is installed.
{: important}

## Resource Management Control (RMC)
{: #rmc-aix}

The [RMC subsystem](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/admin/bl503_undrmc.html){: external} is the scalable backbone of RSCT that provides a generalized framework for managing resources within a single system or a cluster. Its generalized framework is used by cluster management tools to monitor, query, modify, and control cluster resources. RMC provides a single monitoring and management infrastructure for both RSCT peer domains and management domains.

The RMC status of the AIX VM is presented in the {{site.data.keyword.powerSys_notm}} dashboard as a health status. The RMC health status can be either `OK` or `Warning`. Warning statuses happen when the RMC subsystem between your VM and the management system is not connected.

The RMC connection between your VM and the system management service is configured when you create the AIX VM. When you deploy an AIX VM, the IPv6 management interface is injected into the VM. If you remove or overwrite this interface, an RMC connection is not possible. The following procedures can cause the injected IPv6 management interface to be lost after you deploy the AIX VM:

- Attach a different boot volume to the VM and boot from it
- Use the `mksysb restore` operation from a private cloud VM
- Use `smitty` to remove the IPv6 interface

## Diagnosing and recovering from a missing IPv6 link local address
{: #rsct-diagnosis-recovery}

One of your AIX VM network interface controllers (NICs) must include an IPv6 link local address to connect to the Novalink host. If the desired NIC does not have an associated IPv6 link local address, you must perform a recovery procedure.

### Diagnosing a missing IPv6 link local address
{: #diagnosing-ipv6}

Enter the `ifconfig -a` command on your AIX VM terminal to see whether one of your NICs shows an IPv6 link local address (`2001:1234:5723:ABCD:5678:D14E:DBCA:0764/64`). The following example is a NIC without an associated IPv6 link local address:

```text
en0: flags=1e084863,480<UP,BROADCAST,NOTRAILERS,RUNNING,SIMPLEX,MULTICAST,GROUPRT,64BIT,CHECKSUM_OFFLOAD(ACTIVE),CHAIN>
inet 192.168.2.104 netmask 0xfffffff0 broadcast 192.168.2.111
```

If one of your NICs does not contain an IPv6 link local address, continue on to the next section.

### Using a {{site.data.keyword.powerSys_notm}} boot image to recover from a missing IPv6 link local address
{: #recovering-ipv6}

1. Enter the `lslpp -L rsct.*` command to ensure that an operating system (OS) modification did not affect the RSCT file set level. For more information, see [Verifying RSCT installation on AIX nodes](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/admin/bl503_instvaix.html){: external}.

    {{site.data.keyword.powerSys_notm}} supports *3.2.1* as the minimum release. If you redeployed an AIX image with a package that is older than 3.2.1, you must upgrade RSCT first.
    {: important}

2. If you still have the {{site.data.keyword.powerSys_notm}} deployed boot image, complete the following steps:

    1. Boot to the original {{site.data.keyword.powerSys_notm}} boot image.
    2. Rerun the `ifconfig -a` command. The output includes the configured IPv6 link local address.

        If you removed the IPv6 link local address from the original boot image configuration, you can read the AIX `cloud-init` logs to find the IPv6 address.
        {: note}

    3. Open the `/var/log/cloud-init-output.log` file.
    4. Use the `grep` command to search for the IP injection.
        There is an IPv4 address and an IPv6 link local address.

3. Using the IPv6 address for the host, [refresh the RMC services](https://www.ibm.com/support/pages/fixing-no-rmc-connection-error){: external}:

    ```text
    /opt/rsct/bin/rmcctrl -p
    /opt/rsct/bin/rmcrefreshMD -s ctrmc
    ```

4. *(Optional)* If you altered the `nodeid` (that is unique to RMC), it can impact RMC. For example, when you are using PowerHA and trying to copy your `nodeid` details from a private cloud deployment that is not supported. Begin by rebuilding the node:

    ```text
    odmdelete -o CuAt -q name=cluster0 to remove 'cluster0' entry from the CuAt ODM.
    ```

5. *(Optional)* On the AIX VM, enter the `cat /etc/ct_node_id` command and save the output.

6. *(Optional)* To create new `nodeid` and restart RMC services:

   ```text
   /usr/sbin/rsct/install/bin/recfgct
   ```

7. *(Optional)* To build a `nodeid`, run the `/opt/rsct/bin/rmcctrl -p` command if not already done in step 3.

If these recovery steps do not restore the RMC status to **active** and its health to **OK**, open a case with [support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
{: tip}

## Recovering from a missing IPv6 link local address when using your own boot image
{: #recover-ipv6-own}

Complete the following steps to recover from a missing IPv6 link local address:

1. Before you shut down the AIX VM, grab the IPv6 details.

2. Gather the IP interface and adapter configuration details by using `smitty`.

3. Run the `/usr/sbin/rsct/bin/lsnodeid` command to grab the `nodeid`.

4. Confirm that the `nodeid` matches the output from `cat /etc/ct_node_id` and `cat /var/ct/cfg/ct_node_id`.

5. Power down the AIX VM and restart it by using your custom boot image.

6. Re-create the same network configuration as on the IBM boot image by using `smitty`.

7. Validate that the RSCT packages are at least *3.2.1* or later by running the `lslpp -L rsct.*` command.

8. Run the `/usr/sbin/rsct/bin/lsnodeid` command. This will not match the data from the IBM boot image.

9. Generate a `nodeid` to match the original boot ID. Start RMC again and wait 15 minutes.

    ```text
    /usr/sbin/rsct/bin/rmcctrl -p
    odmdelete -o CuAt  -q name=cluster0 (optional before the recfgct command)
    /usr/sbin/rsct/install/bin/recfgct – I value from /etc/ct_node_id (on the original IBM boot disk collected above)
    ```

10. Run the `/usr/sbin/rsct/bin/lsnodeid` command.

11. The output should be the same as the output from the IBM boot image.
