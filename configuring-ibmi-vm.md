---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-1"

keywords: license keys, system service tools, dedicated service tools, network configuration, ibm i, ssh tunneling

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

# Configuring your IBM i virtual machine (VM)
{: #configuring-ibmi}

Complete the following instructions to configure your IBM i virtual machine (VM).
{: shortdesc}

## Licenses and configuring your network
{: #license-network}

You must install the following program temporary fixes (PTFs) on your IBM i VM in order for the {{site.data.keyword.cloud}} to inject licenses:

- IBM i 7.2 - 5770SS1 SI71091 (prereqs SLIC PTFs: MF66395, MF66394, MF66391)
- IBM i 7.3 - MF99207 (TR7) and SI69686
- IBM i 7.4 - MF99301 (TR1) and SI70544

If you are bringing your own IBM i custom image, you must install the PTFs previously mentioned and the software required for `cloud-init`. For more information, see [Cloud-Init Support for IBM i](https://www.ibm.com/support/pages/node/1166194){: new_window}{: external}.

After you deploy an IBM i VM and and install the proper PTFs, you need to accept the license agreements. To accept the license agreements from the console, you must press **5** to display the agreement and **F18** to accept it. When using **F** keys above **F12** on the console (such as **F18**), you must use the buttons on the console screen and not your keyboard. After you accept the license agreements, `cloud-init` configures your network and injects your license keys.

The `cloud-init` configuration process can take up to 5 minutes. **Do not restart your system** while `cloud-init` is running. If you restart your system during this time, you must call IBM support to manually configure your network and license keys.
{: important}

To verify that `cloud-init` configured your IP addresses correctly, check your VM's attributes. In the following example, you can see three IP addresses. Two of IP addresses are internal and one is external.

![Verifying your VM IP addresses](./images/console-ibmi-ip.png "Verifying your VM IP addresses"){: caption="Figure 1. Verifying your VM IP addresses" caption-side="bottom"}

Under the **Subnet** tab in your dashboard, you can see a single subnet. There is an additional internal IP address that represents the external IP address. Configuration information for the external IP address does not exist when you check the VM. The network forwards traffic from the internal IP address to the external IP address.

![Checking your VM subnet](./images/console-ibmi-subnet.png "Checking your VM subnet"){: caption="Figure 2. Checking your VM subnet" caption-side="bottom"}

Next, check to see whether the two internal IP addresses are configured correctly. To do this, enter the `CFGTCP` command and choose option `1`.

![Using the CFGTCP command](./images/terminal-ibmi-cfgtcp.png "Using the CFGTCP command"){: caption="Figure 3. Using the CFGTCP command" caption-side="bottom"}

If the two IP addresses match the internal IP addresses of your VM, the `cloud-init` configuration ran successfully.

Lastly, enter the `DSPLICKEY` command to verify that the `cloud-init` injected the license keys correctly. After you verify your network and license key configuration, you can initial program load (IPL) the LPAR.

![Using the DSPLICKEY command](./images/terminal-ibmi-dsplickey.png "DSPLICKEY command"){: caption="Figure 4. Using the DSPLICKEY command" caption-side="bottom"}

## Changing the System Service Tools (SST) and Dedicated Service Tools (DST) passwords
{: #sst-dst}

By default, the SST and DST passwords are expired. Complete the following tasks to get into SST, change your passwords, and configure the newly attached disk. Configuring a newly attached disk is required.

![Changing the system value](./images/terminal-ibmi-ipl.png "Changing the system value"){: caption="Figure 5. Changing the system value" caption-side="bottom"}

For more information on user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: new_window}{: external}.
{: note}

1. Enter the  `wrksysval qipltype` command and change the value to **1**. The `wrksysval qipltype` command changes the `sysval QIPLTYPE` value.

2. Enter the `pwrdwnsys` command twith the `RESTART` paramater to restart the IBM i operating system (OS).

3. At the DST console on restart, enter `QSECOFR/QSECOFR` and change the password.

4. Enter the `wrksysval qipltype` command and change the value to **0**.

5. Reenter the `pwrdwnsys` command with the `RESTART` parameter to restart the IBM i OS again.

You can now log in, run `STRSST`, and manage the newly attached disk as the password is manageable.

## Using SSH tunneling to allow ACS to connect over the public IP
{: #ssh-tunneling}

The public IP address blocks most ports. As a result, you need to use SSH tunneling or configure your certificates and use SSL.

1. Start the **SSHD** server on the VM:

    ```shell
    strtcpsvr server(*SSHD)
    ```
    {: pre}

    On a Linux or Mac system, you would run a command similar to the following example:

    ```shell
    ssh -L 50000:localhost:23 -L 2001:localhost:2001 -L 2005:localhost:2005 -L 449:localhost:449 -L 8470:localhost:8470 -L 8471:localhost:8471 -L 8472:localhost:8472 -L 8473:localhost:8473 -L 8474:localhost:8474 -L 8475:localhost:8475 -L 8476:localhost:8476 -o ExitOnForwardFailure=yes -o ServerAliveInterval=15 -o ServerAliveCountMax=3 <myuser>@<myIPaddress>
    ```
    {: pre}

    If the system is denying you permission, you might have to use `sudo` in front of the `ssh` command.
    {: note}

2. To get a 5250 session on your IBM i VM from ACS, you need either to configure your virtual devices or enable _autoconfig_. To enable _autoconfig_, complete the following steps by using the IBM i VM:
    1. Enter the `cfgtcp` command.

    2. Select option **20** (Configure TCP/IP applications).

    3. Select option **11** (configure TELNET).

    4. Select option **10** (autoconfigure virtual devices).

    5. Select `QAUTOVRT` with option **2** (change).

    6. Change the value from **0** to the number of auto-configured consoles you want to be able to connect concurrently.

3. Go to the IBM i VM and start the telnet server for the console:

    ```shell
    strtcpsvr server(*TELNET)
    ```
    {: pre}

For ACS, you need to configure a server for _localhost_. In this example, **port 50000** is forwarding to **port 23**. Go into the 5250 session configuration and change the port from **23** to **50000**.

![Changing the port number](./images/system-ibmi-localhost.png "Changing the port number"){: caption="Figure 6. Changing the port number" caption-side="bottom"}
