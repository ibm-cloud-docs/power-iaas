---

copyright:
  years: 2026

lastupdated: "2026-06-09"

keywords: metadata service, troubleshooting, trusted profiles, power virtual server, network connectivity, AIX, Linux, IBM i

subcollection: power-iaas

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting metadata service connectivity
{: #troubleshoot-metadata-service}
{: troubleshoot}

If you experience issues connecting to the metadata service endpoint, use the following troubleshooting procedures for your operating system.
{: shortdesc}

The metadata service uses an internal network configured with the link-local IP address `169.254.169.253`. This network is system-created and should not be modified manually unless required for troubleshooting purposes.
{: note}

## Troubleshooting on AIX
{: #metadata-troubleshooting-aix}

Use the following procedures to troubleshoot and resolve metadata service connectivity issues on AIX VSIs.

### Validating and recovering network connectivity on AIX
{: #metadata-troubleshooting-aix-validate}

If the metadata service endpoint cannot be reached from your AIX VSI, complete the following steps to validate and recover connectivity:

1. Verify whether the IP address `169.254.169.253` is configured on any interface:

   ```sh
   ifconfig -a
   ```
   {: pre}

2. If the IP address is not present, identify an interface that does not have an IP address assigned.

3. Configure the IP address and bring the interface up. In the following example, `en2` is the identified interface:

   ```sh
   chdev -l en2 -a netaddr=169.254.169.253 -a netmask=255.255.0.0 -a state=up
   ```
   {: pre}

4. Ensure that the interface is active:

   ```sh
   ifconfig en2 up
   ```
   {: pre}

5. Validate that the connection is successful by retrieving an instance identity token from within the VSI:

   ```sh
   curl -X PUT "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token" -H "Metadata-Flavor: ibm" -H "Accept: application/json"
   ```
   {: pre}

### Cleaning up network interfaces after disabling the metadata service on AIX
{: #metadata-troubleshooting-aix-cleanup}

When you disable access to the metadata service on your VSI, the network interfaces are not automatically removed. Network interfaces that are left in a "Defined" state must be cleaned up manually.

If you do not perform this cleanup, the unused network interfaces remain in the system configuration and might cause confusion during future network troubleshooting or configuration tasks.
{: note}

Complete the following steps to clean up the interface after disabling the metadata service:

1. List all network adapters:

   ```sh
   lsdev -Cc adapter
   ```
   {: pre}

2. Identify the adapter that is in the "Defined" state.

3. Display the adapter attributes:

   ```sh
   lsattr -El en<X>
   ```
   {: pre}

   Replace `<X>` with the adapter number that you identified.

4. Confirm that the IP address shown is `169.254.169.253`.

5. If confirmed, remove the logical and physical device entries:

   ```sh
   rmdev -dl en<X>
   rmdev -dl ent<X>
   ```
   {: pre}

   Replace `<X>` with the adapter number that you identified earlier.

## Troubleshooting on Linux
{: #metadata-troubleshooting-linux}

Use the following procedures to troubleshoot and resolve metadata service connectivity issues on Linux VSIs.

### Preventing connectivity loss during image capture and restore on Linux
{: #metadata-troubleshooting-linux-prevent}

When you overwrite your Linux VSI's OS disk with a custom image, all network configuration is removed, including the metadata service interface. To prevent the loss of connectivity to the metadata service API endpoint, you can take one of the following preventative measures before you perform the capture.

#### Removing network persistence rules before image capture
{: #metadata-troubleshooting-linux-remove-rules}

Before you capture the image, back up and then delete the contents of the network persistence rules files:

1. Back up the file that contains network persistence rules, including MAC address:

   ```sh
   cp /etc/udev/rules.d/70-persistent-net.rules /home/admin/.
   ```
   {: pre}

   The `admin` user might not exist in your environment. Adjust the path as needed for your environment.
   {: note}

2. Delete the contents of `/etc/udev/rules.d/70-persistent-net.rules` while ensuring that permissions are retained.

3. Repeat for `85-persistent-net-generator.rules`:

   ```sh
   cp /lib/udev/rules.d/85-persistent-net-generator.rules /home/admin/.
   ```
   {: pre}

4. Delete the contents of `/lib/udev/rules.d/85-persistent-net-generator.rules` while ensuring that permissions are retained.

#### Recording the MAC address for manual restoration
{: #metadata-troubleshooting-linux-mac-address}

Alternatively, you can record the MAC address of the metadata service interface before the image overwrite and use it to manually restore the configuration afterward. For more information, see [Reconfiguring the metadata service interface after a custom image overwrite on Linux](#metadata-troubleshooting-linux-reconfigure).

### Reconfiguring the metadata service interface after a custom image overwrite on Linux
{: #metadata-troubleshooting-linux-reconfigure}

If you overwrote your Linux VSI's OS disk with a custom image, you can restore the metadata service network interface by using the MAC address that you recorded before the overwrite.

#### Before overwriting your image
{: #metadata-troubleshooting-linux-before-overwrite}

1. Identify the metadata service interface by running the following command:

   ```sh
   ip addr show | grep -B 2 "169.254.169.253"
   ```
   {: pre}

   Example output:

   ```text
   2: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP
       link/ether fa:16:3e:a1:b2:c3 brd ff:ff:ff:ff:ff:ff
       inet 169.254.169.253/30 brd 169.254.169.255 scope link eth1
   ```
   {: screen}

2. Record the MAC address from the output. In this example: `fa:16:3e:a1:b2:c3`.

   You can also retrieve just the MAC address:

   ```sh
   ip link show eth1 | grep link/ether | awk '{print $2}'
   ```
   {: pre}

3. Save this MAC address. You need it after the image overwrite.

#### After overwriting your image
{: #metadata-troubleshooting-linux-after-overwrite}

1. Identify which interface has the MAC address that you recorded:

   ```sh
   ip link show | grep -B 1 "fa:16:3e:a1:b2:c3"
   ```
   {: pre}

   This command shows the interface name (for example, `eth1`, `ens4`).

2. Configure the interface based on your Linux distribution:

   **For RHEL or CentOS 7 and earlier:**

   a. Create or edit `/etc/sysconfig/network-scripts/ifcfg-eth1` (replace `eth1` with your interface name):

   ```text
   DEVICE=eth1
   BOOTPROTO=none
   ONBOOT=yes
   IPADDR=169.254.169.253
   NETMASK=255.255.255.252
   ```
   {: codeblock}

   b. Restart the network service:

   ```sh
   systemctl restart network
   ```
   {: pre}

   **For RHEL or CentOS 8 and later (using NetworkManager):**

   ```sh
   nmcli connection add type ethernet con-name trusted-profile ifname eth1 ip4 169.254.169.253/30
   nmcli connection up trusted-profile
   ```
   {: pre}

   **For SLES (using wicked):**

   a. Edit `/etc/sysconfig/network/ifcfg-eth1`:

   ```text
   BOOTPROTO='static'
   IPADDR='169.254.169.253/30'
   STARTMODE='auto'
   ```
   {: codeblock}

   b. Restart the network:

   ```sh
   wicked ifup eth1
   ```
   {: pre}

3. Verify the interface configuration:

   ```sh
   ip addr show eth1
   ```
   {: pre}

   The output must include:

   ```text
   inet 169.254.169.253/30 brd 169.254.169.255 scope link eth1
   ```
   {: screen}

4. Ensure that the interface is set to start on boot. For RHEL or CentOS 7 and earlier, verify that `ONBOOT=yes` is set in the interface configuration file. For NetworkManager-based systems, the connection is automatically set to autoconnect.

5. Test connectivity to the metadata service:

   ```sh
   curl -X PUT "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token" -H "Metadata-Flavor: ibm" -H "Accept: application/json"
   ```
   {: pre}

### Validating and recovering network connectivity on Linux
{: #metadata-troubleshooting-linux-validate}

If the metadata service endpoint cannot be reached from your Linux VSI, complete the following steps to validate and recover connectivity:

1. Verify whether the IP address `169.254.169.253` is configured on any interface:

   ```sh
   ip a
   ```
   {: pre}

2. If the IP address is not present, identify an interface that does not have an IP address assigned and configure the IP address on that interface by following the steps in [After overwriting your image](#metadata-troubleshooting-linux-after-overwrite).

3. If the IP address is present but you cannot communicate with the metadata service, complete the following steps:

   a. Verify that the route exists:

   ```sh
   ip route show dev eth1
   ```
   {: pre}

   You should see a route for the `169.254.169.252/30` network.

   b. Check firewall rules:

   For `firewalld`:

   ```sh
   firewall-cmd --list-all
   ```
   {: pre}

   For `iptables`:

   ```sh
   iptables -L -n
   ```
   {: pre}

   If necessary, add a rule to allow traffic to `169.254.169.254`.

   c. Verify that no conflicting routes exist:

   ```sh
   ip route show | grep 169.254
   ```
   {: pre}

   If you see conflicting routes, carefully review them before making any changes. Your custom image might include routes that were intentionally configured for your environment. Removing routes without understanding their purpose might disrupt other network connectivity. Ensure that removing a route does not break any other intentional network configurations before you proceed.
   {: important}

4. If you are still unable to communicate with the metadata service, open a support case for {{site.data.keyword.powerSys_notm}} through the [IBM Cloud Support portal](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

### Cleaning up network interfaces after disabling the metadata service on Linux
{: #metadata-troubleshooting-linux-cleanup}

If you use the `force_disable` flag during a VSI edit, you must clean up the network interface that was used for the metadata service. The tool that is used to configure your interface varies based on what is supported by your distribution. For example, if you're using NetworkManager, use the `nmcli` command to remove the connection.

Complete the following steps to clean up the interface:

1. Identify the interface with the IP address `169.254.169.253`:

   ```sh
   ip a
   ```
   {: pre}

2. Identify the UUID of the connection:

   ```sh
   nmcli con show | grep <interface_name>
   ```
   {: pre}

   Replace `<interface_name>` with the interface name from the previous step.

3. Delete the connection from your OS configuration:

   ```sh
   nmcli con delete <UUID>
   ```
   {: pre}

   Replace `<UUID>` with the UUID from the previous step.

   Ensure that you are not deleting your primary network interface's connection.
   {: important}

## Troubleshooting on IBM i
{: #metadata-troubleshooting-ibmi}

Use the following procedures to troubleshoot and resolve metadata service connectivity issues on IBM i VSIs.

### Configuring the metadata service interface on IBM i
{: #metadata-troubleshooting-ibmi-configure}

When you enable trusted profiles on an IBM i VSI, the metadata service interface is not automatically configured. You must manually create the line description, add the TCP/IP interface, and start the interface to enable trusted profile functionality.

#### Prerequisites
{: #metadata-troubleshooting-ibmi-prereqs}

Before you begin, ensure that you have:

* Access to a 5250 session with sufficient authority (typically `*ALLOBJ` or `*IOSYSCFG` special authority)
* The resource name of an available Ethernet adapter
* Basic familiarity with IBM i TCP/IP configuration

#### Identifying an available Ethernet resource
{: #metadata-troubleshooting-ibmi-identify-resource}

1. From a 5250 session, display available communication resources:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

2. Identify an Ethernet adapter that is not currently in use. Note the resource name (for example, `CMN05`).

3. To verify that the resource is not in use, check existing line descriptions:

   ```text
   WRKCFGSTS *LIN
   ```
   {: pre}

4. Ensure that no line description is using the resource that you selected.

#### Creating the line description
{: #metadata-troubleshooting-ibmi-create-line}

You can create the line description by using either the CFGTCP menu or CL commands.

**Option A: Using CFGTCP menu (recommended):**

1. Enter the following command:

   ```text
   CFGTCP
   ```
   {: pre}

2. Select option 1 (Work with TCP/IP interfaces).

3. Press F6 to add a new interface.

4. Fill in the following fields:

   * **Internet address:** `169.254.169.253`
   * **Subnet mask:** `255.255.255.252`
   * **Line description:** Enter a name (for example, `METADATA`)
   * **Associated local interface:** Leave blank or use `*NONE`

   CIDR notation (such as `/30`) is not accepted. You must use the full subnet mask.
   {: note}

5. Press Enter to continue.

6. When prompted to create the line description, press F10 or select Yes.

7. Fill in the line description parameters:

   * **Resource name:** Enter the resource name that you identified (for example, `CMN05`)
   * **Line type:** `*ELAN`
   * **Vary on:** `*YES`

8. Press Enter to create the line description. The line description is created and automatically varied on.

**Option B: Using CL commands:**

1. Create the line description:

   ```text
   CRTLINETH LIND(METADATA) RSRCNAME(CMN05) LINESPEED(1G) DUPLEX(*FULL)
   ```
   {: pre}

   Replace `CMN05` with your resource name. Adjust `LINESPEED` as appropriate for your hardware (common values: `10M`, `100M`, `1G`, `10G`).

2. Vary on the line:

   ```text
   VRYCFG CFGOBJ(METADATA) CFGTYPE(*LIN) STATUS(*ON)
   ```
   {: pre}

3. Add the TCP/IP interface:

   ```text
   ADDTCPIFC INTNETADR('169.254.169.253') LIND(METADATA) SUBNETMASK('255.255.255.252') AUTOSTART(*YES)
   ```
   {: pre}

#### Starting the TCP/IP interface
{: #metadata-troubleshooting-ibmi-start-interface}

The TCP/IP interface must be explicitly started after creation.

**Using CFGTCP menu:**

1. From the CFGTCP menu, select option 1 (Work with TCP/IP interfaces).

2. Locate the interface with IP address `169.254.169.253`.

3. Enter option 9 (Start) next to the interface.

4. Press Enter. If the interface is already active, the system displays a message indicating that it is running.

**Using CL command:**

```text
STRTCPIFC INTNETADR('169.254.169.253')
```
{: pre}

#### Verifying the configuration
{: #metadata-troubleshooting-ibmi-verify}

1. Check the line description status:

   ```text
   WRKCFGSTS *LIN
   ```
   {: pre}

   The line description (for example, `METADATA`) should show status `VARIED ON`.

2. Verify that the interface is active:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   Look for the interface with IP address `169.254.169.253`. The status should show `Active`.

3. Test connectivity to the metadata service:

   ```text
   PING RMTSYS('169.254.169.254')
   ```
   {: pre}

   You should see successful ping responses. Press F3 to end the ping.

The metadata service network uses the link-local IP range `169.254.169.254/30`. The interface IP address is `169.254.169.253`. No gateway is required for this network.
{: tip}

### Reconfiguring the metadata service interface after a custom image overwrite on IBM i
{: #metadata-troubleshooting-ibmi-reconfigure}

When you overwrite your IBM i VSI's OS disk with a custom image, all network configuration is removed, including the metadata service interface. Before you overwrite your image, record the resource name and hardware address of the metadata service interface. After the overwrite, reconfigure the interface by using the same hardware address.

#### Before overwriting your image
{: #metadata-troubleshooting-ibmi-before-overwrite}

1. From a 5250 session, identify the metadata service interface by running the following command:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

2. Look for the interface with IP address `169.254.169.253`. Note the interface name (for example, `ETH01`, `ETH02`).

3. Display the line description details to get the hardware address:

   ```text
   DSPLIND LIND(ETH01)
   ```
   {: pre}

   Or use:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

   Then select option 5 (Display details) for the Ethernet adapter.

4. Record the following information:

   * Resource name (for example, `CMN05`)
   * Hardware address (MAC address, for example, `FA163EA1B2C3`)

5. Save this information to use it after the image overwrite.

#### After overwriting your image
{: #metadata-troubleshooting-ibmi-after-overwrite}

1. From a 5250 session, identify which resource has the hardware address that you recorded:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

2. Select option 5 (Display details) for each Ethernet adapter until you find the one with the matching hardware address.

3. Create a line description for the metadata service interface:

   **Option A: Using CFGTCP menu (recommended):**

   a. Enter the following command:

   ```text
   CFGTCP
   ```
   {: pre}

   b. Select option 1 (Work with TCP/IP interfaces).

   c. Press F6 to add a new interface.

   d. Fill in the following fields:

   * **Internet address:** `169.254.169.253`
   * **Subnet mask:** `255.255.255.252`
   * **Line description:** Enter a name (for example, `METADATA`)
   * **Associated local interface:** Leave blank or use `*NONE`

   e. Press Enter to continue.

   f. When prompted to create the line description, press F10 or select Yes.

   g. Fill in the line description parameters:

   * **Resource name:** Enter the resource name that you recorded (for example, `CMN05`)
   * **Line type:** `*ELAN`
   * **Vary on:** `*YES`

   h. Press Enter to create the line description. The interface should now be active.

   **Option B: Using CL commands:**

   a. Create the line description:

   ```text
   CRTLINETH LIND(METADATA) RSRCNAME(CMN05) LINESPEED(1G) DUPLEX(*FULL)
   ```
   {: pre}

   Replace `CMN05` with your recorded resource name. Adjust `LINESPEED` as appropriate for your hardware.

   b. Vary on the line:

   ```text
   VRYCFG CFGOBJ(METADATA) CFGTYPE(*LIN) STATUS(*ON)
   ```
   {: pre}

   c. Add the TCP/IP interface:

   ```text
   ADDTCPIFC INTNETADR('169.254.169.253') LIND(METADATA) SUBNETMASK('255.255.255.252') AUTOSTART(*YES)
   ```
   {: pre}

4. Verify the interface configuration:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   Look for the interface with IP address `169.254.169.253`. The status should show as `Active`.

5. Test connectivity to the metadata service:

   ```text
   PING RMTSYS('169.254.169.254')
   ```
   {: pre}

   Press F3 to end the ping after confirming connectivity.

The metadata service network uses the link-local IP range `169.254.169.254/30`. The interface IP address is `169.254.169.253`. No gateway is required for this network.
{: tip}

### Resolving interface activation issues on IBM i
{: #metadata-troubleshooting-ibmi-activation}

If the interface configuration is in place but the interface does not activate, complete the following steps:

1. Check the line description status:

   ```text
   WRKLIND LIND(METADATA)
   ```
   {: pre}

   The status should show `VARIED ON`.

2. If the line is varied off, vary it on:

   ```text
   VRYCFG CFGOBJ(METADATA) CFGTYPE(*LIN) STATUS(*ON)
   ```
   {: pre}

3. Check for error messages in the job log:

   ```text
   DSPJOBLOG
   ```
   {: pre}

   Look for messages that are related to the line description or TCP/IP interface.

4. Verify that the resource name is correct and not in use by another line description:

   ```text
   WRKHDWRSC *CMN
   ```
   {: pre}

   Ensure that the resource is not allocated to another line description.

5. Check if the interface is set to autostart:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   Look at the Auto-Start column. If it shows `NO`, remove and re-add the interface with `AUTOSTART(*YES)`:

   ```text
   RMVTCPIFC INTNETADR('169.254.169.253')
   ADDTCPIFC INTNETADR('169.254.169.253') LIND(METADATA) SUBNETMASK('255.255.255.252') AUTOSTART(*YES)
   ```
   {: pre}

### Validating network connectivity to the metadata service on IBM i
{: #metadata-troubleshooting-ibmi-validate}

If the metadata service interface is configured but you cannot reach `169.254.169.254`, complete the following steps:

1. Verify that the route exists:

   ```text
   NETSTAT *RTE
   ```
   {: pre}

   You should see a route for the `169.254.169.252/30` network associated with your metadata interface.

   If you see conflicting routes or interface configurations, carefully review them before making any changes. Your custom image might include configurations that were intentionally set for your environment. Removing or modifying configurations without understanding their purpose might disrupt other network connectivity. Ensure that any changes do not break other intentional network configurations before you proceed.
   {: important}

2. Check if the interface is active:

   ```text
   NETSTAT *IFC
   ```
   {: pre}

   The interface with IP address `169.254.169.253` should show status `Active`.

3. Verify that the line description is varied on:

   ```text
   WRKLIND LIND(METADATA)
   ```
   {: pre}

4. Check the TCP/IP configuration:

   ```text
   CFGTCP
   ```
   {: pre}

   Select option 1 (Work with TCP/IP interfaces) and verify that the interface configuration is correct.

5. Retry the IP configuration on another `CMN*` device. The RMC interface that is used by {{site.data.keyword.powerSys_notm}} might never have been configured on your OS, or another CMN device might also be unconfigured.

6. If you are still unable to communicate with the metadata service API endpoint, contact [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.
