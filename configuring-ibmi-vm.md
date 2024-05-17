---

copyright:
  years: 2019, 2024

lastupdated: "2024-05-16"

keywords: license keys, system service tools, dedicated service tools, network configuration, ibm i, ssh tunneling

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring your IBM i virtual machine (VM)
{: #configuring-ibmi}

[On Cloud]{: tag-blue}


The following instructions describe the first boot and usage of your IBM i virtual machine (VM).
{: shortdesc}

IBM i 7.2, and later, VMs support up to 127 storage volumes per VM.
{: note}

## First boot of IBM i
{: #first-boot}

When an IBM Power Virtual Server is started using a Stock OS Image of IBM i, the console must first be used to reset the password of the IBM i standard user `QSECOFR`.

The IBM i standard user `QSECOFR` is set to the password `QSECOFR`, and must be changed to a password with 17 characters (no blank spaces) by using the VNC Console. For a refresh of VNC Console usage with IBM i, please see the following [Tips for working with the IBM i console](/docs/power-iaas?topic=power-iaas-configuring-ibmi#tips-ibmi).

The first boot steps below may have minor differences for stock OS Images prior to IBM i 7.5.


### First boot VNC Console access
{: #first-boot-vnc-console-access}

To begin your first boot, open the VNC Console:

1. Go to **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VM instance.
2. Click **VM actions** in the server details pane and select **Open console** from the drop-down list; the console setting will prompt for the language and click open console.

    IBM i console opens as a popup window. Ensure that your browser setting does not block this popup window.
    {: note}
To disconnect form the VNC Console session, close the web browser window (i.e. close the web broswer pop-up window titled 'noVNC').

If you lose internet connectivity, your VNC Console session (provided via noVNC) will show as "Server disconnected (code: 1006)" and will not auto-connect when internet connectivity is restored.

To restore the VNC Console session, return to the IBM Power Virtual Instance, and again click **VM actions** in the server details pane and select **Open console** from the drop-down list. Your session will be restored and show 'Connected (encrypted)'.

Alternatively, if you have many IBM i virtual machines you can use the IBM Cloud CLI to return the VNC Console session URL, such as using a shell command loop:
```shell
ibmcloud pi service-list
ibmcloud pi service-target <<IBM_POWER_VS_WORKSPACE_CRN>>
for i in $(ibmcloud pi instances --json | jq -r '.pvmInstances.[] | select(.osType=="ibmi").serverName'); do echo "" && ibmcloud pi instance-get-console "$i"; done
```
### First boot change password
{: #first-boot-change-password}
Once the VNC Console has loaded and the IBM i console screen is shown, follow the following steps to reset the password of the IBM i standard user.
3. In the VNC Console window, the IBM i virtual machine will wait on **Dedicated Service Tools (DST) Sign On** screen, type `QSECOFR` followed by clicking **PF5** at the bottom of the console window to open the change password screen for the IBM i standard user.
4. The **Change Service Tools User Password** screen will load, and the cursor will be on `Current password . . . .`, enter `QSECOFR`.
5. Press your keyboard TAB key multiple times until the cursor is next to the `New password . . . .` and enter a 17 character password (no blanks).
6. Repeat, use TAB key multiple times until the cursor is next to the `New password (to verify) . . . .` and enter the new password again.
7. Press your keyboard ENTER key, and the password will change.
8. The **IPL or Install the System** screen will be shown. See further steps below.
    Multiple attempts are permitted, if the warning message is shown about locking the user then click **PF3** at the bottom of the console window and start again.
    {: note}
### First boot configuration choice
{: #first-boot-configuration-choice}
After this, the IBM i virtual machine is ready to be configured and a prompt will be given whether to perform an Initial Program Load (IPL), Install the OS, or Perform an Automated Install of the OS.
The default is to select Option 1 'Perform an IPL'.
However, the minimum Program Temporary Fix (PTFs) levels depend on the IBM i version that has been provisioned and will impact `cloud-init` successful execution; only IBM i 7.5 requires no PTF installation or other tasks. Please see [Minimum PTF levels for IBM i](/docs/power-iaas?topic=power-iaas-minimum-levels) for more information for IBM i 7.1 - 7.4, and to instead peform the OS Install first, then PTFs, then the IPL.
If the PTFs are incomplete this will cause `cloud-init` to not complete (executed after IPL / OS Install and Licensed Program Software Agreements), which will cause the local IP Address configuration to not be saved upon restart of the system. If you restart your system during before `cloud-init` is successful, you must call IBM support to manually configure your network and license keys, or delete and reprovision your IBM i virtual machine instance to start again.
{: important}
9. In the **IPL or Install the System** screen, the cursor will be on `Selection`. The default as described previously, is 'Perform an IPL' therefore enter `1` and then press your keyboard ENTER key, which will begin the installation automatically. This process can take more than 10 minutes, each screen in the first text block will show `Current step / total . . . . :` with the number of steps completed (e.g. `20  49` being 20 of 49 steps).
10. During the installation, you will first be shown the **Licensed Internal Code IPL in Progress** screen, then the **Operating System IPL in Progress** screen. During the installation a blank screen with a cursor will be shown for a few minutes, the cursor will disappear and a full blank screen will be shown while the host completes for a further few minutes before returning to the **Operating System IPL in Progress** screen.
Use your keyboard CTRL+W to return to the **Dedicated Service Tools (DST) Sign On** screen at any time (this can be useful if you experience a console session hang).
{: note}
### First boot license choice
{: #first-boot-license-choice}
After installation is completed, the Licensed Program Software Agreements must be accepted.
11. Once installation is completed, the **Sign On** screen will be shown. Enter the `QSECOFR` user, press your keyboard TAB key to move to the next line, and then enter the password chosen previously. Press your keyboard ENTER key to login. In rare occurances if the password was reset during installation, use default password `QSECOFR` again and follow prompts to change your password again.
12. Upon login, the screen will automatically change to the **Work with Software Agreements** screen.
13. On the **Work with Software Agreements** screen, click **PF12** at the bottom of the console window to show the descriptions for each license (e.g. DB2 Multisystem).
14. On the **Work with Software Agreements** screen, for each Licensed Program enter `5` as the "Opt" to display the agreement to accept. Press your keyboard ENTER key to begin.
15. The **Software Agreement** screen will appear for each Licensed Program. Click **PF15** at the bottom of the console window to Accept All for this Licensed Program. The **Confirm Acceptance of Software Agreement** screen will appear for each Licensed Program. Press your keyboard ENTER key to confirm acceptance.
16. The **Work with Software Agreements** screen will appear again, showing "More..." in the bottom right corner. Click **PF11** at the bottom of the console window to show the "Accept Status" which should appear as 'Yes'. Press your keyboard ENTER key, this will force a check of the agreements.
17. The force check of the agreements will then show the **Software Agreements Not Accepted** screen. Click **PF12** at the bottom of the console window to return to the **Work with Software Agreements** screen where the Licensed Program list will have been updated.
18. Repeat steps 14 to 17. There will be 4 repeats until all Licensed Program Software Agreements have been accepted.
19. When all Licensed Program Software Agreements in the list are completed, the **IBM i Main Menu** screen is shown and `cloud-init` configuration of network and injection of license keys will begin. The `cloud-init` configuration process is executed after all, and can take up to 5 minutes.

## Tips for working with the IBM i console
{: #tips-ibmi}

- The standard IBM i user/password is `QSECOFR/QSECOFR`.
- IBM i uses function keys extensively. At the bottom of the console, you can see **PF1** through **PF12**. To get to **PF13** to **PF24**, click the **Next...** button.
- If you see a red **X** in the console during the configuration process, use your keyboard's **CONTROL** button to exit.
- You can use **CONTROL+W** to end a hung session. If this happens, you must perform a bypass by clicking **PF18** and logging on again.
- It's best to first shut down the system before you restart it.
- If you are using a Mac computer, the **Page Down** key is the same as **FN + Down Arrow**.
- `CRTUSRPRF` and `CHGUSRPRF` will use the same new security rules as `QSECOFR`, requiring at least a 17 character password.

## Verify licences and network configuration
{: #verify-licences-and-network-configuration}

To verify that `cloud-init` configured your IP addresses correctly, on the **IBM i Main Menu** screen type the `cfgtcp` command in the console window (on line "Selection or command ===>"), press ENTER, choose `1` and press ENTER again.

One or more IP Addresses with "Line Description" as `CLOUDINIT<<0..n>>` should be shown and match the network interfaces for the attached IBM Power VS network subnets shown in the IBM Power VS Workspace. If the IP Address/es match, then `cloud-init` configuration ran successfully.

See an example below of the `cloud-init` configuration verification:

```
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

For external IP Addresses, if you do not see the external IP address in the **Work with TCP/IP Interfaces** screen, wait approximately 10 minutes, open another terminal and ping the external IP address. The external address must match what is shown in the {{site.data.keyword.powerSys_notm}} user interface within your instance's **Server details** pane. Contact support or delete and reprovision your IBM i VM if the ping doesn't return anything.


Lastly, on the **IBM i Main Menu** screen type the `WRKLICINF` command in the console window (on line "Selection or command ===>"), press ENTER, then click **PF11** at the bottom of the console window to display the usage information. The Usage Limit, Usage Count and Peak Usage values should be populated for each License.

After you verify your network and license key configuration, you can initial program load (IPL) the LPAR.

If License Keys for the operating system or any IBM i Licensed Program Products (LPP) have not been applied, follow instructions in the [PowerVS license key issues](https://www.ibm.com/support/pages/mustgather-powervs-license-key-issues){: external} document.

If this is an upgraded system that contained License Keys before, please allow a weekend (Saturday-Sunday) to process the updated keys before collecting the [PowerVS license key issues](https://www.ibm.com/support/pages/mustgather-powervs-license-key-issues){: external} information.


## Changing the System Service Tools (SST) and Dedicated Service Tools (DST) passwords
{: #sst-dst}

By default, the SST and DST passwords are expired. Complete the following tasks to get into SST, change your passwords, and configure the newly attached disk. Configuring a newly attached disk is required and must be done if other disks are attached.

For more information on user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: external}.
{: note}

To change the System Service Tools (SST) and Dedicated Service Tools (DST) passwords complete the following steps:

1. Click the VM instance to view the **Server details** pane and click **Operations**.
2. Choose **(21) Active dedicated service tools** option from the displayed list under the **Job operations**.
3. Click **Run action**.


For more information on user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: external}.
{: note}

## Managing the IBM i VM instance
{: #manage-IBMi-VM}

You can use the **Operations** panel to manage advanced VM operations and configuration. To open the **Operations** panel and to run job operations or boot operations, complete the following steps:

1. Click the VM instance to view the **Server details** pane.
2. Click **Operations**. The **Operations** button is available only for the IBM i VM instances.
3. In the **Operations** panel, in the **Job operations** tab, click one of the following actions as per your requirements:

   Job operations:

     - **(21) Activate dedicated service tools** – Activates dedicated service tools (DST) and makes it available on the system console display. You can use DST from the system console display to work with Licensed Internal Code (LIC), disk units, configuration and resources, and to verify devices and communications.

     - **(34) Retry Dump** – Retries a failed main storage dump (MSD) operation. You can run this function when the VM instance is hung during the MSD operation or when you want to reattempt the initial program load (IPL) operation without losing the original dump information.

     - **(66) Enable remote service** - Activates the communications port that is used by a remote service session or operations console.

     - **(67) Disk unit IOP reset/reload** - Initiates an I/O processor (IOP) dump operation and a disk unit IOP reset or reload operation. The function is enabled only when specific system reference codes (SRCs) are displayed on the control panel and the associated IOP supports a reset or reload operation. This function is not available for all system types.

     - **(70) IOP Control storage dump** - Saves the contents of the service processor control storage into a non-volatile storage for potential use from an error log file.

     - **(22) Dump restart** - Copies main storage data and processor data to the disk. Run this function only when a MSD operation is necessary, for example, after a suspended (system hang) condition or after an operating system failure.

      You must not shut down the system before the MSD operation. This action can cause data loss.
      {: note}

4. In the **Operations** pane, in the **Boot operations** tab, configure one of the following options according to your requirements:

   Boot operations:

     - **Server boot mode**
         - **A-** Perform an IPL operation from a disk by using the copy A of the system LIC.
         - **B-** Perform an IPL operation from a disk by using the copy B of the system LIC.
         - **C-** Reserved for hardware service use only.
         - **D-** Perform an IPL operation from a media other than the load-source disk. perform an alternate IPL operation for code installation support.

     - **Server operating mode**
         - **Normal** - Allows you to access the operating system and perform an unattended IPL operation. After the system power-on, operating the system in **Normal** (unattended) mode requires no operator intervention during the IPL operation. When you turn on the system in **Normal** mode, the system performs the IPL operation and presents the **Sign On** display on all available display stations. The operator cannot change the internal system environment during the IPL operation. Dedicated service tools (DST) and the operating system do not present any menus or options during this IPL operation.
         - **Manual** - Allows you to access DST and perform an attended IPL operation. After the system power-on, operating the system in Manual (attended) mode means that an operator uses the **Operation** panel or the control panel to direct the system for special needs. During the IPL operation in **Manual** mode, DST and the operating system present menus and prompts you to make changes to the internal system environment. These modifications can include entering debug mode for service representatives to diagnose difficult problems. For more information, see [Operating mode of an IPL](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzal2/rzal2ipliplmodeco.htm){: external}.

5. Click **Run Action**.
