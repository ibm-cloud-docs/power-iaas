---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-05"

keywords: license keys, system service tools, dedicated service tools, network configuration, ibm i, ssh tunneling

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring your IBM i virtual machine (VM)
{: #configuring-ibmi}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

The following instructions describe the first boot and usage of your IBM i virtual machine (VM).
{: shortdesc}

IBM i 7.2, and later, VMs support up to 127 storage volumes per VM.
{: note}

## First boot of IBM i
{: #first-boot}

When you use IBM i 7.5 stock OS Image on an {{site.data.keyword.powerSysFull}}, you must first reset the Dedicated Service Tools (DST) password for the IBM i standard user `QSECOFR` through the console. This step needs to be completed within an hour of VM deployment for the TCP configuration to finish.

The IBM i standard user `QSECOFR` is set to the password `QSECOFR`, and must be changed to a password with 15 characters (no blank spaces) through the VNC Console. For a refresh of VNC Console usage with IBM i, see [Tips for working with the IBM i console](/docs/power-iaas?topic=power-iaas-configuring-ibmi#tips-ibmi).

For steps on changing the DST password, see [First boot change password](#first-boot-change-password).
{: note}


### First boot VNC Console access
{: #first-boot-vnc-console-access}

To begin your first boot, open the VNC Console:

1. Go to the **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VM instance.
2. Click **VM actions** in the server details page and select **Open console** from the drop-down list. On the console setting page, select the language and click **Open console**.

    IBM i console opens as a new window. Ensure that your browser setting does not block any pop-up window.
    {: note}

    The Idle timeout for the VNC console is 30 minutes.
    {: important}

To disconnect from the VNC Console session, close the web browser window that is titled 'noVNC'.

If you lose internet connectivity, your VNC Console session (provided through noVNC) shows as "Server disconnected (code: 1006)" and will not auto-connect when internet connectivity is restored.

To restore the VNC Console session, return to the IBM Power Virtual Instance, and again click **VM actions** in the server details page and select **Open console** from the drop-down list. Your session is restored and shows 'Connected (encrypted)'.

Alternatively, if you have many IBM i virtual machines you can use the IBM Cloud CLI to return the VNC Console session URL, such as using a shell command loop:

```shell
ibmcloud pi service-list
ibmcloud pi service-target <<IBM_POWER_VS_WORKSPACE_CRN>>
for i in $(ibmcloud pi instances --json | jq -r '.pvmInstances.[] | select(.osType=="ibmi").serverName'); do echo "" && ibmcloud pi instance-get-console "$i"; done
```

### First boot change password
{: #first-boot-change-password}

When the VNC Console loads and the IBM i console screen is shown (IBM i 7.5), complete the following steps to reset the password of the IBM i standard user:

Releases prior to IBM i 7.5 will be presented the System Sign-on screen first, where the QSECOFR password needs to be reset.
{: note}

1. In the VNC Console window, the IBM i virtual machine waits on **Dedicated Service Tools (DST) Sign On** screen, type `QSECOFR` followed by clicking **PF5** at the end of the console window to open the change password screen for the IBM i standard user.
2. The **Change Service Tools User Password** screen loads, and the cursor will be on `Current password . . . .`, enter `QSECOFR`.
3. Press the TAB key to move the cursor to the `New password . . . .` field and enter a 15 character password (no blanks).
4. Repeat the step on the `New password (to verify) . . . .` field and enter the new password again.
5. Press ENTER to continue.
6. The **IPL or Install the System** screen is shown. See more steps documented on this page.

Multiple attempts are permitted, if the warning message is shown about locking the user then click **PF3** at the bottom of the console window and start again.
{: note}

After this, the IBM i virtual machine is ready to be configured and a prompt will be given whether to perform an Initial Program Load (IPL), Install the OS, or Perform an Automated Install of the OS.

The default is to select Option 1 'Perform an IPL'.

### First boot license choice
{: #first-boot-license-choice}

When the installation is complete, the **System Sign-On** screen is presented. Follow the similar steps from [First boot change password](#first-boot-change-password) to change `QSECOFR` password. After the System sign-on is complete, accept the Licensed Program Software Agreements.

1. Following login, the screen will automatically change to the work with **Software Agreements** screen.
2. To accept the license agreements from the console, press **5=display** each license agreement and press ENTER.
3. Use **F14** to accept each agreement.
4. After all are accepted, press ENTER to continue to the IBM i main menu.
5. When the IBM i main menu is shown, the cloud-init configuration of the network and injection of the license keys begin. The cloud-init configuration process ran and can take up to 5 minutes.
6. Confirm that the system has the [Minimum PTF levels for IBM i](/docs/power-iaas?topic=power-iaas-minimum-levels).


## Tips for working with the IBM i console
{: #tips-ibmi}

- The standard IBM i user/password is `QSECOFR/QSECOFR`.
- IBM i uses function keys extensively. At the bottom of the console, you can see **PF1** through **PF12**. To get to **PF13** to **PF24**, click the **Next...** button.
- If you see a red **X** in the console during the configuration process, use your keyboard's **CONTROL** button to exit.
- You can use **CONTROL+W** to end a hung session. If this happens, you must perform a bypass by clicking **PF18** and logging on again.
- It is recommended to first shut down the system before you restart it.
- If you are using a Mac computer, the **Page Down** key is the same as **FN + Down Arrow**.
- `CRTUSRPRF` and `CHGUSRPRF` use the same new security rules as `QSECOFR`, requiring at least a 15 character password.


## Verify licenses and network configuration
{: #verify-licences-and-network-configuration}

To verify that `cloud-init` configured your IP addresses correctly, on the **IBM i main menu** screen type the `cfgtcp` command in the console window (on line "Selection or command ===>"), press ENTER, choose `1` and press ENTER again.

One or more IP addresses with "Line Description" as `CLOUDINIT<<0..n>>` should be shown and match the network interfaces for the attached IBM Power VS network subnets that are shown in the IBM Power Virtual Server workspace. If the IP addresses match, then `cloud-init` configuration ran successfully.

See an example below of the `cloud-init` configuration verification:

```screen
                    Work with TCP/IP Interfaces
                                                                      System: KCW73A
Type options, press Enter.
  1=Add   2=Change    4=Remove    5=Display   9=Start   10=End

          Internet          Subnet            Line                Line
Opt       Address           Mask              Description         Type
___       127.0.0.1         255.0.0.0         *LOOPBACK           *NONE
___       10.1.1.5          255.255.255.192   CLOUDINIT1          *ELAN
___       192.168.128.138   255.255.255.248   CLOUDINIT2          *ELAN

                                                                              Bottom
F3=Exit       F5=Refresh      F6 Print list     F11-Display interface status
F12=Cancel    F17=Top         F18=Bottom
```

For external IP addresses, if you do not see the external IP address in the **Work with TCP/IP Interfaces** screen, wait approximately 10 minutes, open another terminal and ping the external IP address. The external address must match what is shown in the {{site.data.keyword.powerSys_notm}} user interface within your instance's **Server details** page. Contact support or delete and reprovision your IBM i VM if the ping doesn't return anything.


Lastly, on the **IBM i main menu** screen type the `WRKLICINF` command in the console window (on line "Selection or command ===>"), press ENTER, then click **PF11** at the bottom of the console window to display the usage information. The Usage Limit, Usage Count and Peak Usage values should be populated for each license.

When you have verified your network and license key configuration, you can initial program load (IPL) the LPAR.

If license keys for the operating system or any IBM i licensed program Products (LPP) are not applied, follow instructions in the [PowerVS license key issues](https://www.ibm.com/support/pages/mustgather-powervs-license-key-issues){: external} document.

If this is an upgraded system that contained license Keys before, allow a weekend (Saturday-Sunday) to process the updated keys before collecting the [PowerVS license key issues](https://www.ibm.com/support/pages/mustgather-powervs-license-key-issues){: external} information.

The IBM i virtual machine might result in a timeout error, if you update the IBM i virtual machine license and memory together.
{: note}



## Changing the System Service Tools (SST) and Dedicated Service Tools (DST) passwords
{: #sst-dst}

By default, the SST, and DST passwords are expired. Complete the following tasks to get into SST, change your passwords, and configure the newly attached disk. Configuring a newly attached disk is required and must be done if other disks are attached.

For more information on user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: external}.
{: note}

To change the System Service Tools (SST) and Dedicated Service Tools (DST) passwords complete the following steps:

1. Click the VM instance to view the **Server details** page and click **Operations**.
2. Choose **(21) Active dedicated service tools** option from the displayed list under the **Job operations**.
3. Click **Run action**.


For more information on user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: external}.
{: note}

## Managing the IBM i VM instance
{: #manage-IBMi-VM}

You can use the **Operations** page to manage advanced VM operations and configuration. To open the **Operations** page and to run job operations or boot operations, complete the following steps:

1. Click the VM instance to view the **Server details** page.
2. Click **Operations**. The **Operations** button is available only for the IBM i VM instances.
3. In the **Operations** page, in the **Job operations** tab, click one of the following actions as per your requirements:

   Job operations:

     - **(21) Activate dedicated service tools** – Activates dedicated service tools (DST) and makes it available on the system console display. You can use DST from the system console display to work with Licensed Internal Code (LIC), disk units, configuration and resources, and to verify devices and communications.

     - **(34) Retry Dump** – Retries a failed main storage dump (MSD) operation. You can run this function when the VM instance is hung during the MSD operation or when you want to reattempt the initial program load (IPL) operation without losing the original dump information.

     - **(66) Enable remote service** - Activates the communications port that is used by a remote service session or operations console.

     - **(67) Disk unit IOP reset/reload** - Initiates an I/O processor (IOP) dump operation and a disk unit IOP reset or reload operation. The function is enabled only when specific system reference codes (SRCs) are displayed on the control page and the associated IOP supports a reset or reload operation. This function is not available for all system types.

     - **(70) IOP Control storage dump** - Saves the contents of the service processor control storage into a nonvolatile storage for potential use from an error log file.

     - **(22) Dump restart** - Copies main storage data and processor data to the disk. Run this function only when an MSD operation is necessary, for example, after a suspended (system hang) condition or after an operating system failure.

      You must not shut down the system before the MSD operation. This action can cause data loss.
      {: note}

4. In the **Operations** page, in the **Boot operations** tab, configure one of the following options according to your requirements:

   Boot operations:

     - **Server boot mode**
         - **A-** Perform an IPL operation from a disk by using the copy A of the system LIC.
         - **B-** Perform an IPL operation from a disk by using the copy B of the system LIC.
         - **C-** Reserved for hardware service use only.
         - **D-** Perform an IPL operation from a media other than the load-source disk. Perform an alternative IPL operation for code installation support.

     - **Server operating mode**
         - **Normal** - Allows you to access the operating system and perform an unattended IPL operation. After the system power-on, operating the system in **Normal** (unattended) mode requires no operator intervention during the IPL operation. When you turn on the system in **Normal** mode, the system performs the IPL operation and presents the **Sign On** display on all available display stations. The operator cannot change the internal system environment during the IPL operation. Dedicated service tools (DST) and the operating system do not present any menus or options during this IPL operation.
         - **Manual** - Allows you to access DST and perform an attended IPL operation. After the system power-on, operating the system in Manual (attended) mode means that an operator uses the **Operation** page or the control page to direct the system for special needs. During the IPL operation in **Manual** mode, DST and the operating system present menus and prompts you to change the internal system environment. These modifications can include entering debug mode for service representatives to diagnose difficult problems. For more information, see [Operating mode of an IPL](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzal2/rzal2ipliplmodeco.htm){: external}.

5. Click **Run Action**.
