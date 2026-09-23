---

copyright:
  years: 2026

lastupdated: "2026-09-23"

keywords: metadata service, troubleshooting, configuration, trusted profiles, power virtual server, network connectivity, AIX, Linux, IBM i

subcollection: power-iaas

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Configuring and troubleshooting metadata service connectivity
{: #troubleshoot-metadata-service}

Learn how to configure the metadata service network interface on your virtual server instance (VSI) and troubleshoot connectivity issues on AIX, IBM i, and Linux operating systems.
{: shortdesc}

To complete the procedures in this topic, log in to the operating system (OS) of your VSI by using SSH or the {{site.data.keyword.powerSysFull}} console.
{: requirement}

The metadata service uses a link-local network with IP address `169.254.169.253` on your VSI and connects to the metadata service endpoint at `169.254.169.254`. {{site.data.keyword.powerSys_notm}} creates this network automatically. Do not modify this network configuration unless you need to resolve connectivity issues or remove residual network interfaces after disabling the metadata service, as described in this topic.



{{site.data.keyword.powerSys_notm}} uses `cloud-init` package to configure connectivity from a VSI to the metadata service. The `cloud-init` package is required for each OS. If you use a custom image and your OS does not have the IP address 169.254.169.253 configured after you enable metadata service access for your VSI, ensure that your custom image includes the `cloud-init` package.
{: requirement}

## Reconfiguring the metadata service interface on IBM i after an OS disk overwrite
{: #reconfigure-ibmi-after-capture}

When you overwrite the OS disk of an IBM i VSI with a backup image, the network configuration, including the metadata service interface might be lost. Before you overwrite the disk, record the resource name and hardware address of the metadata service interface. After you overwrite the disk, reconfigure the metadata service interface by using the recorded hardware address.

### Recording the interface details before an OS disk overwrite
{: #reconfigure-ibmi-before}

To preserve the resource name and hardware address required to restore the metadata service interface after an OS disk overwrite, use one of the following methods from a 5250 emulator session:

#### Method 1: Using the line description
{: #reconfigure-ibmi-method1}

1. Run the following command to display the TCP/IP interfaces:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

2. Find the interface with the IP address `169.254.169.253` and record the line description name from the **Line Description** column (for example, `ETH01`).

3. Run the following command to display the line description details:

   ```text
   DSPLIND LIND(ETH01)
   ```
   {: pre}

   Replace `ETH01` with the line description name that you identified in step 2.

4. Record and save the following details. Use this information to reconfigure the interface after you overwrite the disk:

   * Resource name (for example, `CMN05`)
   * Hardware address (MAC address, for example, `FA163EA1B2C3`)

#### Method 2: Using communication resources
{: #reconfigure-ibmi-method2}

1. Run the following command to display communication resources:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

2. On the Work with Communication Resources screen, select option 5 (**Display details**) next to the Ethernet adapter to display the resource details.

3. Record and save the following details. Use this information to reconfigure the interface after you overwrite the disk:

   * Resource name (for example, `CMN05`)
   * Hardware address (MAC address, for example, `FA163EA1B2C3`)

### Reconfiguring the metadata service interface after an OS disk overwrite
{: #reconfigure-ibmi-after}

After the OS disk overwrite is complete, use the resource name and hardware address that you recorded to reconfigure the metadata service interface.

To reconfigure the metadata service interface, complete the following steps:

1. From a 5250 session, run the following command to display the hardware resources:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

   The Work with Communication Resources screen is displayed with a list of communication hardware resources.

2. Select option 5 (Display details) for each Ethernet adapter to identify which resource has the hardware address that you recorded.

3. Run the following command to create a line description for the metadata service interface. The following example uses `CMN05` as the resource name and `1G` as the line speed:

   ```text
   CRTLINETH LIND(METADATA) RSRCNAME(CMN05) LINESPEED(1G) DUPLEX(*FULL)
   ```
   {: pre}

   Replace `CMN05` with the resource name that you recorded. Set the `LINESPEED` value to match the speed of your Ethernet adapter.

4. Run the following command to activate the line description:

   ```text
   VRYCFG CFGOBJ(METADATA) CFGTYPE(*LIN) STATUS(*ON)
   ```
   {: pre}

5. Run the following command to add the TCP/IP interface:

   ```text
   ADDTCPIFC INTNETADR('169.254.169.253') LIND(METADATA) SUBNETMASK('255.255.255.252') AUTOSTART(*YES)
   ```
   {: pre}

   This command creates a TCP/IP interface on the `METADATA` line description and assigns the link-local IP address `169.254.169.253` to the interface. The interface enables communication with the metadata service endpoint.

### Verifying the metadata service interface configuration
{: #reconfigure-ibmi-verify}

To verify that the metadata service interface is configured correctly and active, complete the following steps:

1. Run the following command to verify the metadata service interface configuration:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   Find the metadata service interface with IP address `169.254.169.253` in the output and verify that its status is `Active`. If the interface is not active, see [Resolving interface activation issues](#troubleshoot-ibmi-activation).

2. Run the following command to test connectivity to the metadata service interface:

   ```text
   PING RMTSYS('169.254.169.254')
   ```
   {: pre}

3. After you verify connectivity, press **F3** to end the ping. If the ping fails, see [Validating network connectivity to the metadata service endpoint](#troubleshoot-ibmi-validate).

The metadata service network uses the link-local IP range `169.254.169.254/30`. The metadata service interface IP address is `169.254.169.253`. You do not need to configure a gateway for this network.
{: tip}

## Reconfiguring the metadata service interface on Linux after an OS disk overwrite
{: #reconfigure-linux-after-capture}

When you overwrite the OS disk of a Linux VSI with a previously created disk image, the OS disk overwrite might remove the network configuration, including the metadata service interface. You can configure the network settings before you capture the image, or use the MAC address to restore the metadata service interface configuration after the overwrite.

### Preventing network configuration loss
{: #reconfigure-linux-prevent}

To avoid losing connectivity to the metadata service endpoint, take one of the following actions:

* [Remove the network persistence rules](#reconfigure-linux-remove-rules) before you capture the image.
* [Record the MAC address](#reconfigure-linux-before) of the interface before you overwrite the OS disk with an image.

#### Removing network persistence rules before capturing the image
{: #reconfigure-linux-remove-rules}

To prevent network configuration loss by removing network persistence rules before you capture the image, complete the following steps:

1. Run the following command to back up the file that contains the network persistence rules, including the MAC address:

   ```bash
   cp /etc/udev/rules.d/70-persistent-net.rules /home/admin/.
   ```
   {: pre}

   The `admin` user might not exist in your environment. Modify the path for your environment.
   {: note}

2. Delete the contents of the `/etc/udev/rules.d/70-persistent-net.rules` file. Ensure that file permissions are retained.

3. Run the following command to back up the file that generates the network persistence rules:

   ```bash
   cp /lib/udev/rules.d/85-persistent-net-generator.rules /home/admin/.
   ```
   {: pre}

4. Delete the contents of the `/lib/udev/rules.d/85-persistent-net-generator.rules` file. Ensure that file permissions are retained.

### Recording the MAC address before overwriting your image
{: #reconfigure-linux-before}

If you want to retain the network persistence rules, record the MAC address of the interface that communicates with the metadata service endpoint. After you overwrite the boot disk of your VSI with the saved image, you can reconfigure the interface by using the MAC address.

To record the MAC address before you overwrite the OS disk with an image, complete the following steps:

1. Run the following command to identify the metadata service interface:

   ```bash
   ip addr show | grep -B 2 "169.254.169.253"
   ```
   {: pre}

   The output shows the metadata service interface details, including the MAC address and IP address.

   ```text
   2: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP
       link/ether fa:16:3e:a1:b2:c3 brd ff:ff:ff:ff:ff:ff
       inet 169.254.169.253/30 brd 169.254.169.255 scope link eth1
   ```
   {: screen}

2. Record the MAC address from the output.

   In this example, the MAC address is `fa:16:3e:a1:b2:c3`.

3. Optional: Run the following command to retrieve only the MAC address:

   ```bash
   ip link show eth1 | grep link/ether | awk '{print $2}'
   ```
   {: pre}

   Replace `eth1` with the interface name from the previous output.

4. Save the MAC address to reconfigure the metadata service interface after the OS disk overwrite.

### Reconfiguring the metadata service interface after the OS disk overwrite
{: #reconfigure-linux-after}

If you remove the network persistence rules before you capture the image, you do not need to configure the metadata service interface after the OS disk overwrite. If you retain the network persistence rules and record the MAC address, complete the following steps to reconfigure the metadata service interface:

1. Run the following command to identify the interface with the MAC address that you record:

   ```bash
   ip link show | grep -B 1 "fa:16:3e:a1:b2:c3"
   ```
   {: pre}

   Replace `fa:16:3e:a1:b2:c3` with the MAC address that you record in the [Recording the MAC address before overwriting your image](#reconfigure-linux-before) section.

   The output shows the metadata service interface name (for example, `eth1` or `ens4`).

2. Configure the interface based on your Linux distribution.

   The following procedures are organized by Linux distribution and network management tool. RHEL or CentOS 7 and earlier versions use the network service, RHEL or CentOS 8 and later versions use NetworkManager, and SLES uses the Wicked network management tool.

#### Configuring the interface on RHEL or CentOS 7 and earlier versions
{: #reconfigure-linux-rhel7}

To configure the metadata service interface on RHEL or CentOS 7 and earlier versions, complete the following steps:

1. Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth1` file with the following content:

   ```text
   DEVICE=eth1
   BOOTPROTO=none
   ONBOOT=yes
   IPADDR=169.254.169.253
   NETMASK=255.255.255.252
   ```
   {: codeblock}

   Replace `eth1` with your metadata service interface name.

2. Run the following command to restart the network service:

   ```bash
   systemctl restart network
   ```
   {: pre}

   The network service restarts and applies the new interface configuration.

#### Configuring the interface on RHEL or CentOS 8 and later versions by using NetworkManager
{: #reconfigure-linux-rhel8}

To configure the metadata service interface on RHEL or CentOS 8 and later versions with NetworkManager, run the following commands:

```bash
nmcli connection add type ethernet con-name trusted-profile ifname eth1 ip4 169.254.169.253/30
nmcli connection up trusted-profile
```
{: pre}

The connection is activated and the interface is configured with the metadata service IP address.

Replace `trusted-profile` with a connection name of your choice and `eth1` with your metadata service interface name.

#### Configuring the interface on SLES by using Wicked
{: #reconfigure-linux-sles}

To configure the metadata service interface on SLES by using the Wicked network management tool, complete the following steps:

1. Create or edit the `/etc/sysconfig/network/ifcfg-eth1` file with the following content:

   ```text
   BOOTPROTO='static'
   IPADDR='169.254.169.253/30'
   STARTMODE='auto'
   ```
   {: codeblock}

   Replace `eth1` with your metadata service interface name.

2. Run the following command to bring up the metadata service interface:

   ```bash
   wicked ifup eth1
   ```
   {: pre}

   The metadata service interface is brought up with the metadata service IP address.

   Replace `eth1` with your metadata service interface name.

### Verifying the metadata service interface configuration
{: #reconfigure-linux-verify}

To verify that the metadata service interface is configured correctly and is active, complete the following steps:

1. Run the following command to verify the interface configuration:

   ```bash
   ip addr show eth1
   ```
   {: pre}

   Replace `eth1` with your metadata service interface name.

   The output must include the following IP address configuration:

   ```text
   inet 169.254.169.253/30 brd 169.254.169.255 scope link eth1
   ```
   {: screen}

2. Verify that the metadata service interface starts automatically when the system boots:

   * For RHEL or CentOS 7 and earlier: Verify that the `ONBOOT` parameter is set to `yes` in the `/etc/sysconfig/network-scripts/ifcfg-eth1` file, where `eth1` is your metadata service interface name.

   * For NetworkManager-based systems: NetworkManager configures the connection to start automatically when the system boots.

3. Run the following command to verify that the VSI can reach the metadata service and request an identity token:

   ```bash
   curl -X PUT "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token" -H "Metadata-Flavor: ibm" -H "Accept: application/json"
   ```
   {: pre}

   If the command succeeds, it returns a JSON response with an `access_token`, `created_at`, `expires_at`, and `expires_in` field, confirming that the VSI can reach the metadata service endpoint. If the VSI cannot reach the metadata service endpoint, see [Troubleshooting metadata service connectivity on Linux](#troubleshoot-linux).

## Removing network interfaces after disabling the metadata service on AIX
{: #aix-metadata-interface-removal}

When you [disable access to the metadata service](/docs/power-iaas?topic=power-iaas-instance_metadata_pvs#metadata-disable-instance-ui) on an AIX VSI, the network interfaces are not automatically removed. Network interfaces that are left in a `Defined` state must be removed.

To remove the metadata service network interfaces, complete the following steps:

1. Run the following command to list all network adapters:

   ```bash
   lsdev -Cc adapter
   ```
   {: pre}

2. From the output, identify and record the adapter number that is in the `Defined` state.

3. Run the following command to display the adapter attributes:

   ```bash
   lsattr -El en<X>
   ```
   {: pre}

   Replace `<X>` with the adapter number that you recorded.

4. Verify that the IP address in the output is `169.254.169.253`.

5. Run the following commands to remove the logical and physical device entries:

   ```bash
   rmdev -dl en<X>
   rmdev -dl ent<X>
   ```
   {: pre}

   Replace `<X>` with the adapter number that you recorded.

## Removing network interfaces after disabling the metadata service on Linux
{: #cleanup-linux}

If you use the `--metadata-service-force-disable` option with the `ibmcloud pi instance update` command to disable the metadata service on an active Linux VSI, you must manually remove the network interface. The `--metadata-service-force-disable` option disables the metadata service but does not automatically remove the network interface. The tool that configures the metadata service interface varies based on the Linux distribution. The following example uses NetworkManager and the `nmcli` command to remove the network interface.

To remove the metadata service network interface, complete the following steps:

1. Run the following command to identify the interface with the IP address `169.254.169.253`:

   ```bash
   ip a
   ```
   {: pre}

2. Run the following command to list all connections:

   ```bash
   nmcli con show
   ```
   {: pre}

   The output lists the connection name, UUID, type, and device for each connection:

   ```text
   NAME                UUID                                  TYPE      DEVICE
   trusted-profile     1875ae2a-0235-48de-b451-777154597ea9  ethernet  eth1
   lo                  fc819d11-25f8-456a-a026-a926639ba021  loopback  lo
   ```
   {: screen}

3. From the output, locate the connection that uses your metadata service interface name and record the UUID.

4. Optional: Run the following command to filter the output by interface name:

   ```bash
   nmcli con show | grep <interface_name>
   ```
   {: pre}

   Replace `<interface_name>` with your metadata service interface name. Record the UUID from the output.

5. Run the following command to delete the connection from your OS configuration:

   ```bash
   nmcli con delete <UUID>
   ```
   {: pre}

   Replace `<UUID>` with the UUID that you recorded.

   Do not delete the connection for your primary network interface.
   {: important}

   The connection is deleted from your OS configuration.

## Troubleshooting metadata service connectivity on AIX
{: #troubleshoot-aix}
{: troubleshoot}

If your AIX VSI cannot reach the metadata service endpoint, complete the following steps to validate and restore connectivity.
{: shortdesc}

### Validating and restoring network connectivity
{: #troubleshoot-aix-validate}

To validate and restore network connectivity to the metadata service endpoint, complete the following steps:

1. Run the following command to verify whether the IP address `169.254.169.253` is configured on any interface:

   ```bash
   ifconfig -a
   ```
   {: pre}

2. If the IP address is present in the output, go to step 5 to validate connectivity. If the IP address is not present in the output, identify an interface that does not have an IP address assigned.

3. Run the following command to configure the IP address and bring up the interface:

   ```bash
   chdev -l en2 -a netaddr=169.254.169.253 -a netmask=255.255.0.0 -a state=up
   ```
   {: pre}

   Replace `en2` with the interface name that you identified.

4. Run the following command to ensure that the interface is active:

   ```bash
   ifconfig en2 up
   ```
   {: pre}

   Replace `en2` with your interface name.

5. Run the following command to validate connectivity to the metadata service endpoint:

   ```bash
   curl -X PUT "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token" -H "Metadata-Flavor: ibm" -H "Accept: application/json"
   ```
   {: pre}

   If the command succeeds, it returns a JSON response with an `access_token`, `created_at`, `expires_at`, and `expires_in` field, confirming that the VSI can reach the metadata service endpoint. If the command fails or returns an error, open a [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## Troubleshooting metadata service connectivity on Linux
{: #troubleshoot-linux}
{: troubleshoot}

If your Linux VSI cannot reach the metadata service endpoint, complete the following steps to validate and restore connectivity.
{: shortdesc}

### Validating the metadata service network configuration
{: #troubleshoot-linux-validate}

To validate the metadata service network configuration, complete the following steps:

1. Run the following command to verify whether the IP address `169.254.169.253` is configured on any interface:

   ```bash
   ip a
   ```
   {: pre}

2. If the IP address is present in the output, the interface is configured correctly. If the IP address is not present in the output, identify an interface that does not have an IP address assigned.

3. Configure the IP address on that interface by following the steps in [Reconfiguring the metadata service interface](#reconfigure-linux-after).

### Troubleshooting an unreachable metadata service endpoint
{: #troubleshoot-linux-unreachable}

If the metadata service interface is configured but you cannot reach the metadata service endpoint at `169.254.169.254`, complete the following steps:

1. Run the following command to verify that the route exists:

   ```bash
   ip route show dev eth1
   ```
   {: pre}

   Replace `eth1` with your metadata service interface name.

   The output shows a route for the `169.254.169.252/30` network. If the route is not present, reconfigure the metadata service interface by following the steps in [Reconfiguring the metadata service interface](#reconfigure-linux-after).

2. Run one of the following commands to verify the firewall rules, depending on your firewall tool:

   For `firewalld`:

   ```bash
   firewall-cmd --list-all
   ```
   {: pre}

   For `iptables`:

   ```bash
   iptables -L -n
   ```
   {: pre}

3. Optional: Add a rule to allow traffic to IP address `169.254.169.254`.

4. Run the following command to verify that no conflicting routes exist:

   ```bash
   ip route show | grep 169.254
   ```
   {: pre}

   If you see conflicting routes, carefully review the routes before making any changes. Your custom image might include routes that were intentionally configured for your environment. Removing routes without understanding their purpose might disrupt other network connectivity. Ensure that removing a route does not break any other intentional network configurations.
   {: important}

## Troubleshooting metadata service connectivity on IBM i
{: #troubleshoot-ibmi}
{: troubleshoot}

If your IBM i VSI cannot reach the metadata service endpoint, use these procedures to diagnose and resolve the connectivity issue.
{: shortdesc}

### Resolving interface activation issues
{: #troubleshoot-ibmi-activation}

If the interface configuration is in place but the interface does not activate, complete the following steps:

1. Run the following command to check the line description status:

   ```text
   WRKLIND LIND(METADATA)
   ```
   {: pre}

   The status shows `VARIED ON`.

2. If the line is varied off, run the following command to vary it on:

   ```text
   VRYCFG CFGOBJ(METADATA) CFGTYPE(*LIN) STATUS(*ON)
   ```
   {: pre}

3. Run the following command to check for error messages in the job log:

   ```text
   DSPJOBLOG
   ```
   {: pre}

   Look for messages that are related to the line description or TCP/IP interface.

4. Run the following command to verify that the resource name is correct and not in use by another line description:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

   Ensure that the resource is not allocated to another line description.

5. Run the following command to check if the interface is set to autostart:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   Look at the Auto-Start column. If it shows `NO`, run the following command to update the interface:

   ```text
   CHGTCPIFC INTNETADR('169.254.169.253') AUTOSTART(*YES)
   ```
   {: pre}

### Validating network connectivity to the metadata service endpoint
{: #troubleshoot-ibmi-validate}

If the metadata service interface is configured but you cannot reach the metadata service endpoint at `169.254.169.254`, complete the following steps:

1. Run the following command to verify that the route exists:

   ```text
   NETSTAT *RTE
   ```
   {: pre}

   The output shows a route for the `169.254.169.252/30` network associated with your metadata service interface.

   If you see conflicting routes or interface configurations, carefully review the routes before making any changes. Your custom image might include configurations that were intentionally set for your environment. Removing or modifying configurations without understanding their purpose might disrupt other network connectivity. Ensure that any changes do not break other intentional network configurations.
   {: important}

2. Run the following command to check if the interface is active:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   The interface with IP address `169.254.169.253` shows the status `Active`.

3. Run the following command to verify that the line description is varied on:

   ```text
   WRKLIND LIND(METADATA)
   ```
   {: pre}

   The line description status shows `VARIED ON`.

4. Run the following command to access the TCP/IP configuration menu:

   ```text
   CFGTCP
   ```
   {: pre}

   Select option 1 (Work with TCP/IP interfaces) and verify that the metadata service interface configuration is correct.

5. If the previous steps do not restore connectivity, configure the metadata service IP address on another `CMN*` device and test connectivity again. The RMC interface that is used by {{site.data.keyword.powerSys_notm}} might not have been configured on your OS, or another `CMN*` device might be available but unconfigured.

If you are still unable to communicate with the metadata service endpoint, open a [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
