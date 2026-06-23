---

copyright:
  years: 2026

lastupdated: "2026-06-23"

keywords: metadata service, troubleshooting, configuration, trusted profiles, power virtual server, network connectivity, AIX, Linux, IBM i

subcollection: power-iaas

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Configuring and troubleshooting metadata service connectivity
{: #troubleshoot-metadata-service}

Learn how to configure the metadata service network interface on your virtual server instance (VSI) and troubleshoot connectivity issues.
{: shortdesc}

The metadata service uses a link-local network with IP address 169.254.169.253 on your VSI and connects to the metadata service endpoint at 169.254.169.254. This network is system-created and must not be modified unless required to correct connectivity issues or as a cleanup activity, as described in this topic.

You must perform the following procedures while you are logged in to the operating system (OS) on your VSI. You can log in by using SSH or by accessing the OS through the {{site.data.keyword.powerSys_notm}} console.
{: requirement}

## Reconfiguring the metadata service interface on IBM i after an OS disk overwrite
{: #reconfigure-ibmi-after-capture}

Learn how to restore the metadata service network interface on an IBM i VSI after you overwrite the operating system (OS) disk with a backup image.

### Reconfiguring the metadata service interface after an OS disk overwrite
{: #reconfigure-ibmi-after-os-or}

When you overwrite the OS disk of an IBM i VSI, the network configuration, including the metadata service interface, might be lost. Before you overwrite the disk, record the resource name and hardware address of the metadata service interface. After the overwrite, reconfigure the metadata service interface by using the same hardware address.

### Before overwriting your image
{: #reconfigure-ibmi-before}

To record the resource name and hardware address, complete the following steps:

1. From a 5250 session, run the following command to identify the metadata service interface:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

2. Look for the interface with IP address `169.254.169.253`. Record the metadata service interface name (for example, `ETH01`, `ETH02`).

3. Run the following command to display the line description details. Record the hardware address from the line description details.

   ```text
   DSPLIND LIND(ETH01)
   ```
   {: pre}

   Alternatively, you can use the following command:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

   Then select option 5 (Display details) for the Ethernet adapter.

4. Record the following information:

   * Resource name (for example, `CMN05`)
   * Hardware address (MAC address, for example, `FA163EA1B2C3`)

5. Save this information to use it after the image overwrite.

### After overwriting your image
{: #reconfigure-ibmi-after}

To reconfigure the metadata service interface by using the information that you recorded, complete the following steps:

1. From a 5250 session, run the following command to display the hardware resources:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

2. Select option 5 (Display details) for each Ethernet adapter to identify which resource has the hardware address that you recorded.

3. Run the following command to create a line description for the metadata service interface:

   ```text
   CRTLINETH LIND(METADATA) RSRCNAME(CMN05) LINESPEED(1G) DUPLEX(*FULL)
   ```
   {: pre}

   Replace `CMN05` with the resource name that you recorded. Set the `LINESPEED` value to match your the speed of your Ethernet adapter.

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

### Verifying the metadata service interface configuration
{: #reconfigure-ibmi-verify}

To verify that the metadata service interface is configured correctly and active, complete the following steps:

1. Run the following command to verify the metadata interface configuration:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   Look for the metadata service interface with IP address `169.254.169.253`. The status of the metadata service interface must be `Active`.

2. Run the following command to test connectivity to the metadata service interface:

   ```text
   PING RMTSYS('169.254.169.254')
   ```
   {: pre}

   Press F3 to end the ping after confirming connectivity.

The metadata service network uses the link-local IP range `169.254.169.254/30`. The metadata service interface IP address is `169.254.169.253`. No gateway is required for this network.
{: tip}

## Reconfiguring the metadata service interface on Linux after an OS disk overwrite
{: #reconfigure-linux-after-capture}

When you overwrite the OS disk of a Linux VSI with a previously created disk image, the network configuration, including the metadata service interface, might be removed. You can take preventative measures before you capture the image or use the MAC address to restore the configuration afterward.

### Preventing network configuration loss
{: #reconfigure-linux-prevent}

You can take one of the following preventative measures to avoid losing connectivity to the metadata service endpoint:

* Remove the network persistence rules before you perform the capture
* Note the MAC address of the interface to restore the configuration

#### Removing network persistence rules before capture
{: #reconfigure-linux-remove-rules}

To prevent network configuration loss by removing network persistence rules before you capture the image, complete the following steps:

1. Run the following command to back up the file that contains network persistence rules, including the MAC address:

   ```bash
   cp /etc/udev/rules.d/70-persistent-net.rules /home/admin/.
   ```
   {: pre}

   The `admin` user might not exist in your environment. Adjust the path as needed for your environment.
   {: note}

2. Delete the contents of the `/etc/udev/rules.d/70-persistent-net.rules` file. Ensure that file permissions are retained.

3. Run the following command to back up the file that generates network persistence rules:

   ```bash
   cp /lib/udev/rules.d/85-persistent-net-generator.rules /home/admin/.
   ```
   {: pre}

4. Delete the contents of the `/lib/udev/rules.d/85-persistent-net-generator.rules` file. Ensure that file permissions are retained.

### Before overwriting your image
{: #reconfigure-linux-before}

If you prefer to keep the network persistence rules in place, record the MAC address of the interface that communicates with the metadata service endpoint. After you overwrite the boot disk of your VSI with the saved image, you can reconfigure the interface by using the MAC address.

To record the MAC address before you overwrite your image, complete the following steps:

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

2. Record the MAC address from the output. In this example: `fa:16:3e:a1:b2:c3`.

   Alternatively, run the following command to retrieve only the MAC address:

   ```bash
   ip link show eth1 | grep link/ether | awk '{print $2}'
   ```
   {: pre}

   Replace `eth1` with the interface name from the output in step 1.

3. Save this MAC address to use it after the image overwrite.

### After overwriting your image
{: #reconfigure-linux-after}

If you removed the network persistence rules before the image capture, no further configuration is required. If you kept the network persistence rules in place and recorded the MAC address, complete the following steps to reconfigure the metadata service interface:

1. Run the following command to identify the interface that has the MAC address that you recorded:

   ```bash
   ip link show | grep -B 1 "fa:16:3e:a1:b2:c3"
   ```
   {: pre}

   Replace `fa:16:3e:a1:b2:c3` with the MAC address that you recorded in step 2 of the [Before overwriting your image](#reconfigure-linux-before) section.

   The output shows the metadata service interface name (for example, `eth1`, `ens4`).

2. Configure the interface by using the following procedures for your Linux distribution.

#### For RHEL or CentOS 7 and earlier
{: #reconfigure-linux-rhel7}

To configure the metadata service interface on RHEL or CentOS 7 and earlier, complete the following steps:

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

#### For RHEL or CentOS 8 and later (using NetworkManager)
{: #reconfigure-linux-rhel8}

To configure the metadata service interface on RHEL or CentOS 8 and later with NetworkManager, run the following commands:

```bash
nmcli connection add type ethernet con-name trusted-profile ifname eth1 ip4 169.254.169.253/30
nmcli connection up trusted-profile
```
{: pre}

Replace `eth1` with your metadata service interface name.

#### For SLES (using wicked)
{: #reconfigure-linux-sles}

To configure the metadata service interface on SLES by using wicked, complete the following steps:

1. Edit the `/etc/sysconfig/network/ifcfg-eth1` file with the following content:

   ```text
   BOOTPROTO='static'
   IPADDR='169.254.169.253/30'
   STARTMODE='auto'
   ```
   {: codeblock}

   Replace `eth1` with your metadata service interface name.

2. Run the following command to restart the network:

   ```bash
   wicked ifup eth1
   ```
   {: pre}

   Replace `eth1` with your metadata service interface name.

### Verifying the metadata service interface configuration
{: #reconfigure-linux-verify}

To verify that the metadata service interface is configured correctly and active, complete the following steps:

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

2. Verify that the metadata service interface is configured to start automatically on boot:

   * For RHEL or CentOS 7 and earlier: Verify that the `ONBOOT` parameter is set to `yes` in the interface configuration file.

   * For NetworkManager-based systems: NetworkManager configures the connection to start automatically on boot.

3. Run the following command to verify that the VSI can reach the metadata service and request an identity token:

   ```bash
   curl -X PUT "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token" -H "Metadata-Flavor: ibm" -H "Accept: application/json"
   ```
   {: pre}

## Steps to perform within AIX after disabling access to the metadata service endpoint
{: #aix-metadata-interface-removal}

When you disable access to the metadata service on an AIX VSI, the network interfaces are not automatically removed. Network interfaces that are left in a "Defined" state require cleanup.

To clean up the metadata service network interfaces, complete the following steps:

1. Run the following command to list all network adapters:

   ```bash
   lsdev -Cc adapter
   ```
   {: pre}

2. From the output, identify the adapter that is in the "Defined" state.

3. Run the following command to display the adapter attributes:

   ```bash
   lsattr -El en<X>
   ```
   {: pre}

   Replace `<X>` with the adapter number that you identified in step 2.

4. Verify that the IP address shown in the output is `169.254.169.253`.

5. Run the following commands to remove the logical and physical device entries:

   ```bash
   rmdev -dl en<X>
   rmdev -dl ent<X>
   ```
   {: pre}

   Replace `<X>` with the adapter number from step 2.

## Cleaning up network interfaces after disabling the metadata service on Linux
{: #cleanup-linux}

If you use the `force_disable` flag during a VSI edit, you must clean up the network interface that the metadata service used. The tool that configures the metadata service interface varies based on the Linux distribution. The following example uses NetworkManager and the `nmcli` command to remove the connection.

To clean up the metadata service network interface, complete the following steps:

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

   The output displays connection information in columns:

   ```text
   NAME                UUID                                  TYPE      DEVICE
   trusted-profile     1875ae2a-0235-48de-b451-777154597ea9  ethernet  eth1
   lo                  fc819d11-25f8-456a-a026-a926639ba021  loopback  lo
   ```
   {: screen}

   Locate the connection that uses the interface name from step 1, and record the UUID (the second column).

   Alternatively, you can filter the output by using the interface name:

   ```bash
   nmcli con show | grep <interface_name>
   ```
   {: pre}

   Replace `<interface_name>` with the interface name from step 1. Record the UUID from the second column of the output.

3. Run the following command to delete the connection from your OS configuration:

   ```bash
   nmcli con delete <UUID>
   ```
   {: pre}

   Replace `<UUID>` with the UUID that you recorded from step 2.

   Ensure that you do not delete the connection for your primary network interface.
   {: important}

## Troubleshooting metadata service connectivity on AIX
{: #troubleshoot-aix}
{: troubleshoot}

If your AIX VSI cannot reach the metadata service endpoint, complete the following steps to validate and restore connectivity
{: shortdesc}

### Validating and restoring network connectivity
{: #troubleshoot-aix-validate}

To validate and restore network connectivity to the metadata service endpoint, complete the following steps:

1. Run the following command to verify whether the IP address `169.254.169.253` is configured on any interface:

   ```bash
   ifconfig -a
   ```
   {: pre}

2. If the IP address is not present in the output, identify an interface that does not have an IP address assigned.

3. Run the following command to configure the IP address and bring the interface up:

   ```bash
   chdev -l en2 -a netaddr=169.254.169.253 -a netmask=255.255.0.0 -a state=up
   ```
   {: pre}

   Replace `en2` with the interface name that you identified in step 2.

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

   This command retrieves an instance identity token from the metadata service.

If you still cannot communicate with the metadata service endpoint, contact [IBM Support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## Troubleshooting metadata service connectivity on Linux
{: #troubleshoot-linux}
{: troubleshoot}

If your Linux VSI cannot reach the metadata service endpoint, complete the following steps to validate and restore connectivity.
{: shortdesc}

### Validating the network configuration
{: #troubleshoot-linux-validate}

To validate the metadata service network configuration, complete the following steps:

1. Run the following command to verify whether the IP address `169.254.169.253` is configured on any interface:

   ```bash
   ip a
   ```
   {: pre}

2. If the IP address is not present in the output, identify an interface that does not have an IP address assigned. Then, configure the IP address on that interface by following the steps in [After overwriting your image](#reconfigure-linux-after).

### Troubleshooting when the interface is configured but unreachable
{: #troubleshoot-linux-unreachable}

If the metadata service interface is configured but you cannot reach the metadata service endpoint at `169.254.169.254`, complete the following steps:

1. Run the following command to verify that the route exists:

   ```bash
   ip route show dev eth1
   ```
   {: pre}

   Replace `eth1` with your metadata service interface name.

   The output should show a route for the `169.254.169.252/30` network.

2. Run the following commands to check firewall rules:

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

   If necessary, add a rule to allow traffic to IP address `169.254.169.254`.

3. Run the following command to verify that no conflicting routes exist:

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

   The status should show `VARIED ON`.

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

   The output should show a route for the `169.254.169.252/30` network associated with your metadata interface.

   If you see conflicting routes or interface configurations, carefully review the routes before making any changes. Your custom image might include configurations that were intentionally set for your environment. Removing or modifying configurations without understanding their purpose might disrupt other network connectivity. Ensure that any changes do not break other intentional network configurations.
   {: important}

2. Run the following command to check if the interface is active:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   The interface with IP address `169.254.169.253` should show status `Active`.

3. Run the following command to verify that the line description is varied on:

   ```text
   WRKLIND LIND(METADATA)
   ```
   {: pre}

   The line description status should show `VARIED ON`.

4. Run the following command to access the TCP/IP configuration menu:

   ```text
   CFGTCP
   ```
   {: pre}

   Select option 1 (Work with TCP/IP interfaces) and verify that the metadata service interface configuration is correct.

5. If the previous steps do not restore connectivity, configure the metadata service IP address on another `CMN*` device and test connectivity again. The RMC interface that is used by {{site.data.keyword.powerSys_notm}} might not have been configured on your operating system, or another `CMN*` device might be available but unconfigured.

If you are still unable to communicate with the metadata service endpoint, contact [IBM Support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
