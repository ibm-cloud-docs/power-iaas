---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-06"

keywords: port forwarding, ibm i virtual machine, putty session, tcp servers

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Connecting to an IBM i virtual machine (VM)
{: #connect-ibmi}


Learn how to connect to an IBM i VM after configuring your system. Make sure to review [Configuring your IBM i virtual machine (VM)](/docs/power-iaas?topic=power-iaas-configuring-ibmi) before connecting to an IBM i VM.
{: shortdesc}

For a complete list of firewall ports that are available for IBM i VMs, see [Network security](/docs/power-iaas?topic=power-iaas-network-security). If you plan on ordering [Direct Link Connect on Classic](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect) or already have it, port forwarding is not needed.
{: important}

## Installing and configuring IBM i Access Client Solutions (ACS)
{: #installing-acs}

Before you begin, see [Install IBM i Access Client Solutions](https://www.ibm.com/support/pages/ibm-i-access-client-solutions){: external}.

## Using SSH tunneling to allow ACS to connect over the public IP
{: #ssh-tunneling}

The public IP address blocks most ports. As a result, you need to use SSH tunneling or configure your certificates and use SSL to allow ACS to connect over public IP.

Before you use an SSH tunnel, you must create a user profile with `USRCLS(*SECOFR)` specified or enable the `QSECOFR` user profile. To enable the `QSECOFR` user profile, edit the `/QOpenSys/QIBM/ProdData/SC1/OpenSSH/etc/sshd_config` configuration file, and uncomment `PermitRootLogin yes`.

After the `QSECOFR` user profile is enabled, start the SSHD server on the VM:

```text
endtcpsvr server(*SSHD)instance(*all)
strtcpsvr server(*SSHD)
```
{: pre}

On a Linux&reg; or Mac system, you would run a command similar to the following example:

```text
ssh -L 50000:localhost:23 -L 2001:localhost:2001  -L 449:localhost:449 -L 8470:localhost:8470 -L 8471:localhost:8471 -L 8472:localhost:8472 -L 2007:localhost:2007 -L 8473:localhost:8473 -L 8474:localhost:8474 -L 8475:localhost:8475 -L 8476:localhost:8476 -L 2003:localhost:2003 -L 2002:localhost:2002 -L 2006:localhost:2006 -L 2300:localhost:2300 -L 2323:localhost:2323 -L 3001:localhost:3001 -L 3002:localhost:3002 -L 2005:localhost:2005  -o ExitOnForwardFailure=yes -o ServerAliveInterval=15 -o ServerAliveCountMax=3 <myuser>@<myIPaddress>
```
{: pre}

You might have to type  `sudo` in front of the `ssh` command if the system denies you permission.
{: note}

For further information on information and mapping, see [TCP/IP Ports Required for IBM i Access and Related Functions](https://www.ibm.com/support/pages/node/644775){: external} and also [Port Assignments with Operations Console](https://www.ibm.com/support/pages/ibm-iseries-port-assignments-operations-console){: external}.

If you are on a Windows&reg; system, continue with [Setting up and configuring PuTTY on a Windows system](#configure-putty), otherwise see [Starting TCP servers](#start-tcp-servers).

## Setting up and configuring PuTTY on a Windows system
{: #configure-putty}

Install [PuTTY](https://www.putty.org/){: external} onto your system. PuTTY is used for the SSH tunnel on a Windows system.

1. Open **Session** under **Category:**.

2. Enter your system's **IP address** and select **SSH** as the **Connection type**.

3. Enter **22** as the port number.

4. Under the **Connection** category, select **Connection**>**SSH**>**Tunnels**.

5. Add your **Source port** number and **Destination**. For example, you can chose 50000 as the source port number.

    Do not change the source port numbers. When telnetting, avoid making the source port the same as the destination.
    {: tip}

6. Click **Add** to add your source port to the forwarded port list.

    You need to repeat step **3** to step **6** to add all of the following ports: 23, 449, 8470, 8471, 8472, 8473, 8474, 8475, 8476, 2003, 2002, 2006, 2300, 2323, 3001, 3002, and 2005.
    {: important}

7. After you add all of the necessary port numbers, check your populated list.

8. Click back on the **Session** category and give your session a name under **Saved Sessions**. Click **Save**.

9. Your saved session appears under **Saved Sessions** after you click **Save**. Select your session and click **Open** to start a PuTTY session to your system.

    ![Seeing your list of saved sessions](./images/putty-load-sesson.png "Seeing your list of saved sessions"){: caption="Figure 4. Seeing your list of saved sessions" caption-side="bottom"}

10. You are prompted to accept a key on first use, and then presented with a log-in prompt. Use your IBM i session profile and password.

11. Configure you ACS client or **IBM i Access for Windows Client** to use the SSH tunnel. In both clients, you must select **Configure** from the **Communications** menu.

12. Change the IP address to *127.0.0.1* on **port 23**.

13. Press **OK** to save the changes. The client restarts and connects.

## Starting the TCP servers
{: #start-tcp-servers}

Start the required TCP servers on your IBM i operating system by completing the following tasks:

1. To allow SSH connections, enter the following command:

    ```text
    strtcpsvr server(*SSHD)
    ```
    {: pre}

2. To start the IBM Navigator for i (iNav) and Digital Certificate Manager (DCM) GUIs, enter the following command:

    ```text
    strtcpsvr server(*HTTP) httpsvr(*ADMIN)
    ```
    {: pre}

3. To get a 5250 console from ACS, start Telnet:

    ```text
    strtcpsvr server(*TELNET)
    ```
    {: pre}

## Starting a 5250 session on your IBM i VM from ACS
{: #starting-session}

To get a 5250 session on your IBM i VM from ACS, you need to either configure
your virtual devices or enable _autoconfig_. To enable _autoconfig_, complete the following steps by using the IBM i VM:

 1. Enter the `cfgtcp` command.

 2. Select option **20** (Configure TCP/IP applications).

 3. Select option **11** (Configure TELNET).

 4. Select option **10** (Autoconfigure virtual devices).

 5. Select `QAUTOVRT` with option **2** (Change).

 6. Change the value from **0** to the number of auto-configured consoles that you want to be able to connect concurrently.

 7. Go to the IBM i VM and start the telnet server for the console:

    ```text
    strtcpsvr server(*TELNET)
    ```
    {: pre}

After you complete these steps, you can get to a console from ACS. Additionally, you can get to _iNav/DM_ by pointing your browser to the following address:


```text
https://127.0.0.1:2005/ibm/console/login.do?action=secure
```
{: pre}

To enable ICC to use an SSL connection to IBM Cloud Object Storage (COS), which IBM COS requires, see [Configuring Cloud Storage Solutions file transfer encryption](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_72/icc/topics/iccutsk_config_ssl.htm){: external}.

### Configuring ACS
{: #configuring-acs}

After starting ACS, create a system configuration (*sysconfig*).

1. Configure a server for *localhost*. For example, **port 50000** is forwarding to **port 23**. Go into the 5250 session configuration and change the port from **23** to **50000**.

2. Return to the IBM i terminal and enter your credentials, including *System*, *User*, and *Password*.
