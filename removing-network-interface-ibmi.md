---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-07"

keywords: network interface, tcp/ip address, ibm i vm, external ip address, dns, lind, cfgtcp command

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# How to add or remove a network interface from an IBM i virtual machine (VM)
{: #managing-network-interface-ibmi}


Since IBM PowerVC Version 1.2.2, IBM PowerVC can dynamically add a network interface controller (NIC) to a VM or remove a NIC from a VM. IBM PowerVC does not set the IP address for new network interfaces that are created after the machine deployment. Any removal of a NIC results in freeing the IP address that was set on it. You must remove and readd the IBM i VM network interface if you choose to disconnect the {{site.data.keyword.powerSys_notm}} IBM i VM from a public network.
{: shortdesc}

When you toggle a public network off and then on, the {{site.data.keyword.powerSysFull}} user interface regenerates new internal and external IP addresses. You need to check the {{site.data.keyword.powerSys_notm}} user interface for the new internal IP address to complete this procedure.
{: note}

## Removing a network interface from an IBM i VM
{: #remove-nic-ibmi}

Learn how to change the TCP/IP address of your IBM i VM. You can change your system's TCP/IP address while the TCP/IP is active. However, you must deactivate the TCP/IP interface. For a complete set of instructions, see [Changing the TCP/IP Address of the IBM i System](https://www.ibm.com/support/pages/node/641015){: external}.

1. Before you change a TCP/IP address, determine whether it has any associated routes. Choose **Option 8** from the **NETSTAT \*IFC** screen.
    It's a good idea to select **Option 5** to display the details of the route. Remember to press **F6** to print the details for reference for when the route must be readded. This step should be done for all of the **non-\*DIRECT** routes that are listed on the screen.
    {: tip}

2. Run the `CFGTCP` command, and select **Option 2** to work with your TCP/IP routes. Select **Option 4** next to the routes you need to remove. All of that communication that is going over the route is terminated after you remove it.
3. To make the actual changes, you must deactivate and remove the interface before you add it. Select **Option 10** next to the interface you need to deactivate on the **NETSTAT \*IFC** screen.
4. To remove the interface after deactivation, run the `CFGTCP` command and select **Option 1** from that menu. Select **Option 4** next to the interface you need to remove.
    Removing a network interface:

    ```
                        Work with TCP/IP Interfaces
                                                                        System: RCHASSLH
    Type options, press Enter.
    1=Add   2=Change    4=Remove    5=Display   9=Start   10=End

              Internet          Subnet            Line                Line
    Opt       Address           Mask              Description         Type
    ___       9.5.186.23        255.255.255.0     SITETRN             *TRLAN
    ___       9.5.186.222       255.255.255.0     SITETRN             *TRLAN
    _4_       10.10.10.1        255.255.255.0     SITETRN             *TRLAN
    ___       127.0.0.1         255.0.0.0         *LOOPBACK           *NONE





                                                                                  Bottom
    F3=Exit       F5=Refresh      F6 Print list     F11-Display interface status
    F12=Cancel    F17=Top         F18=Bottom
    ```

5. You must vary off the Line description (LIND) after you remove the interface.

## Adding a network interface to an IBM i VM
{: #add-nic-ibmi}

When you toggle a public network off and then on, the {{site.data.keyword.powerSys_notm}} user interface regenerates new internal and external IP addresses. You need to check the {{site.data.keyword.powerSys_notm}} user interface for the new internal IP address (that maps to the external IP address). Point the new interface at the new internal IP address.

1. After you remove the routes and interfaces, create the new configuration in the reverse order. To get to the **ADDTCPIFC** screen, run the `CFGTCP` command and select **Option 1**.
    Most configurations require you to update only the first three fields.
    {: note}

2. Add the new internal IP address that you obtained from the {{site.data.keyword.powerSys_notm}} user interface (you can type over the quotation marks) to the **Internet address** field.
3. Add the new subnet mask to the **Subnet mask** field.
4. Complete the remaining fields by using your reference printout. The LIND must be the same as the LIND defined on the removed interface.
5. After you add the interface, activate it from the **NETSTAT \*IFC** screen by selecting **Option 9**.
6. To verify that the new interface is active, ping the address from the command line. If the ping responds, the interface is working correctly.
7. Finally, add the new routes that use this interface (if any). You can add new routes by selecting **Option 2** from the `CFGTCP` menu. Type **1** in the **Opt** column to add a new route, and press the **Enter** key.

Adding a network interface:

    ```
                                Add TCP/IP Interface (ADDTCPIFC)

    Type choices, press Enter

    Internet address.   .   .   .   .   .   .   .   .   . > .   .
    Line description.   .   .   .   .   .   .   .   .   .   ____________    Name, *LOOPBACK..
    Subnet mask .   .   .   .   .   .   .   .   .   .   .   ____________
    Associated local interface. .   .   .   .   .   .   .   *NONE
    Type of service.    .   .   .   .   .   .   .   .   .   *NORMAL         *MINDELAY, *MAXTHRPUT..
    Maximum transmission unit.  .   .   .   .   .   .   .   *LIND           576-16388, *LIND
    Autostart.  .   .   .   .   .   .   .   .   .   .   .   *YES            *YES,   *NO
    PVC logical channel identifier. .   .   .   .   .   .   ____________    001-FFF
                                 + for more values          ____________
    X.25 idle circuit timeout.  .   .   .   .   .   .   .   60              1-600
    X.25 maximum virtual circuits.  .   .   .   .   .   .   64              0-64
    X.25 DDN interface. .   .   .   .   .   .   .   .   .   *NO             *YES,   *NO
    TRLAN bit sequencing.   .   .   .   .   .   .   .   .   *MSB            *MSB,   *LSB
    ```
