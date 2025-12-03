---

copyright:
  years: 2019, 2025

lastupdated: "2025-12-03"

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

VMs running the IBM i 7.2 or later stock OS images support up to 127 storage volumes per VM by default and can be configured to support up to 508 storage volumes per VM.
{: note}

## First boot of IBM i
{: #first-boot}

When you use IBM i 7.5 or later stock OS image on an {{site.data.keyword.powerSysFull}}, you must first reset the Dedicated Service Tools (DST) password for the IBM i standard user `QSECOFR` through the console. This step needs to be completed within an hour of VM deployment for the TCP configuration to finish.

The IBM i standard user `QSECOFR` is set to the password `QSECOFR`, and must be changed to a password with 15 characters (no blank spaces) through the Virtual Server Instance (VSI) console. For a refresh of VSI console usage with IBM i, see [Tips for working with the IBM i console](/docs/power-iaas?topic=power-iaas-configuring-ibmi#tips-ibmi).

For steps on changing the DST password, see [Changing the DST password](#first-boot-change-dst-password).
{: note}



### Accessing the VSI console
{: #first-boot-access-vsi-console}

To open the VSI console on the first boot, complete the following steps:

1. Go to the **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VM instance. The Virtual server instance details page is displayed.
2. Click **VM actions** in the Virtual server details page and select **Open console** from the drop-down list. The Console Setting dialog is displayed.
3. Select **037 English** from the **Console language** drop-down list.
4. Click **Open console**. The IBM i console opens in a new window. Ensure that your browser settings allow pop-up windows.

    The idle timeout for the VSI console is 2 hours.
    {: important}




To disconnect from the VSI console session, close the web browser window that is titled 'noVNC'.

If you lose internet connectivity, your VSI console session (provided through noVNC) displays the "Server disconnected (code: 1006)" message and will not auto-connect when internet connectivity is restored.

To restore the VSI console session, complete the following steps:

1. Return to the IBM Power Virtual instance.
2. Click **VM actions** in the Virtual server details page and select **Open console** from the drop-down list. The session is restored and the 'Connected (encrypted)' message is displayed

Alternatively, if you have many IBM i virtual machines you can use the IBM Cloud CLI to return the VSI console session URL, such as using a shell command loop:

```shell
ibmcloud pi service-list
ibmcloud pi service-target <<IBM_POWER_VS_WORKSPACE_CRN>>
for i in $(ibmcloud pi instances --json | jq -r '.pvmInstances.[] | select(.osType=="ibmi").serverName'); do echo "" && ibmcloud pi instance-get-console "$i"; done
```

### Changing the DST password
{: #first-boot-change-dst-password}

When the VSI console loads and the IBM i console screen is shown (IBM i 7.5 or later), complete the following steps to reset the password of the IBM i standard user:

Releases before IBM i 7.5 is presented on the System Sign-on screen first, where the `QSECOFR` password needs to be reset.
{: note}

1. In the VSI console window, the IBM i virtual machine waits on **Dedicated Service Tools (DST) Sign On** screen, type `QSECOFR` followed by clicking **PF5** at the end of the console window to open the change password screen for the IBM i standard user.
2. The **Change Service Tools User Password** screen loads, and the cursor is on `Current password . . . .`, enter `QSECOFR`.
3. Press the TAB key to move the cursor to the `New password . . . .` field and enter a 15 character password (no blanks).
4. Repeat the step on the `New password (to verify) . . . .` field and enter the new password again.
5. Press ENTER to continue.
6. The **IPL or Install the System** screen is shown.

Multiple attempts are permitted, if the warning message is shown about locking the user then click **PF3** at the bottom of the console window and start again.
{: note}

The IBM i virtual machine is now ready to be configured and a prompt will be given whether to perform an Initial Program Load (IPL), Install the OS, or Perform an Automated Install of the OS.

The default is to select Option 1 'Perform an IPL'.

### Reviewing software agreements
{: #first-boot-review-software-licenses}

When the installation is complete, the **System Sign-On** screen is displayed. Follow the [Changing the DST password](#first-boot-change-dst-password) procedure to change `QSECOFR` password. After the system sign-on is complete, accept the Licensed Program Software Agreements.

1. After you login, the screen automatically changes to the work with **Software Agreements** screen.
2. To accept the license agreements from the console, press **5=display** each license agreement and press ENTER.
3. Press **F14** to accept each agreement.
4. Once you accept all agreements press ENTER, the IBM i main menu is displayed.
5. When the IBM i main menu is shown, the cloud-init configuration of the network and injection of the license keys begin. The cloud-init configuration process can take up to 5 minutes.
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


## Verifying licenses and network configuration
{: #verify-licences-and-network-configuration}


To resolve an issue with operating system licenses that are expired when you deploy IBM i images, perform the following steps on the IBM {{site.data.keyword.powerSys_notm}} console:

1. After you change the default login password for OS in an IBM i VSI, the Operating System License Information screen is displayed. If you see the error message, `No operating system licenses are available at this time.` wait for 15 min.
2. Press **F5** to retry license verification and to continue with the sign-on process.
3. Accept Software Agreements.
4. Run IBM i command `STRSBS QBASE` or `STRSBS QCTL` to exit restricted state.
5. Run IBM i command `CFGTCP` to verify whether the TCP/IP configuration is complete.

If the stock image is deployed without displaying the Operating System License Information screen, run the `STRSBS QBASE` command within one hour of the VSI deployment. For additional help, contact the support team. For more information, see [Getting Help and Support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).




To verify that `cloud-init` configured your IP addresses correctly, on the **IBM i main menu** screen type the `cfgtcp` command in the console window (on line "Selection or command ===>"), press ENTER, choose `1` and press ENTER again.

One or more IP addresses with "Line Description" as `CLOUDINIT<<0..n>>` should be shown and match the network interfaces for the attached IBM Power VS network subnets that are shown in the IBM Power Virtual Server workspace. If the IP addresses match, then `cloud-init` configuration ran successfully.

See the following example of the `cloud-init` configuration verification:

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

The SST and DST passwords are expired by default. Complete the following tasks to get into SST and change the passwords.

For more information on user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: external}.
{: note}

To change the System Service Tools (SST) and Dedicated Service Tools (DST) passwords, complete the following steps:

1. Go to the **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VM instance. The Virtual server instance details page is displayed.
2. Click **VM actions** in the Virtual server details page and select **IBM i operations** from the drop-down list. The IBM i operations dialog is displayed.
3. Select **(21) Active dedicated service tools** option from the list displayed on the **Control Panel funstions** tab.
4. Click **Run action**.


For more information on user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: external}.
{: note}

## Managing the IBM i VM instance
{: #manage-IBMi-VM}

You can use the **IBM i operations** option to manage advanced VM operations and configuration. To run the control panel functions or boot operations, complete the following steps:

1. Go to the **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VM instance. The Virtual server instance details page is displayed.
2. Click **VM actions** in the Virtual server details page and select **IBM i operations** from the drop-down list. The IBM i operations dialog is displayed.

The **IBM i operations** option is available only for the IBM i VM instances.
{: note}

3. In the IBM i operations dialog, select one of the following actions listed on the **Control panel functions** as per your requirements:

   Job operations:

     - **(21) Activate dedicated service tools** – Activates dedicated service tools (DST) and makes it available on the system console display. You can use DST from the system console display to work with Licensed Internal Code (LIC), disk units, configuration and resources, and to verify devices and communications.

     - **(34) Retry Dump** – Retries a failed main storage dump (MSD) operation. You can run this function when the VM instance is hung during the MSD operation or when you want to reattempt the initial program load (IPL) operation without losing the original dump information.

     - **(66) Enable remote service** - Activates the communications port that is used by a remote service session or operations console.

     - **(67) Disk unit IOP reset/reload** - Initiates an I/O processor (IOP) dump operation and a disk unit IOP reset or reload operation. The function is enabled only when specific system reference codes (SRCs) are displayed on the control page and the associated IOP supports a reset or reload operation. This function is not available for all system types.

     - **(70) IOP Control storage dump** - Saves the contents of the service processor control storage into a nonvolatile storage for potential use from an error log file.

     - **(22) Dump restart** - Copies main storage data and processor data to the disk. Run this function only when an MSD operation is necessary, for example, after a suspended (system hang) condition or after an operating system failure.

      You must not shut down the system before the MSD operation. This action can cause data loss.
      {: note}

4. In the IBM i operations dialog, configure one of the following options listed on the **Boot operations** tab as per your requirements:

   Boot operations:

     - **Server boot mode**
         - **A-** Perform an IPL operation from a disk by using the copy A of the system LIC.
         - **B-** Perform an IPL operation from a disk by using the copy B of the system LIC.
         - **C-** Reserved for IBM lab use only.
         - **D-** Perform an IPL operation from a media other than the load-source disk. Perform an alternative IPL operation for code installation support.

     - **Server operating mode**
         - **Normal** - Allows you to access the operating system and perform an unattended IPL operation. After the system power-on, operating the system in **Normal** (unattended) mode requires no operator intervention during the IPL operation. When you turn on the system in **Normal** mode, the system performs the IPL operation and presents the **Sign On** display on all available display stations. The operator cannot change the internal system environment during the IPL operation. Dedicated service tools (DST) and the operating system do not present any menus or options during this IPL operation.
         - **Manual** - Allows you to access DST and perform an attended IPL operation. After the system power-on, operating the system in Manual (attended) mode means that an operator uses the **Operation** page or the control page to direct the system for special needs. During the IPL operation in **Manual** mode, DST and the operating system present menus and prompts you to change the internal system environment. These modifications can include entering debug mode for service representatives to diagnose difficult problems. For more information, see [Operating mode of an IPL](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzal2/rzal2ipliplmodeco.htm){: external}.

5. Click **Run Action**.




## IBM i language support
{: #ibmi-language-support}

The VSI console of an IBM i virtual machine supports English language by default and provides the following additional language support:

- IBM i stock OS images support English (2924) or English DBCS (2984). You can install additional secondary languages and  change the primary language on an IBM i virtual machine.

- The VSI console also supports Japanese if it is installed as a primary or secondary language.

  If you select Japanese as the language in the Console Setting dialog before you start the IBM i VSI console, the system does not install the Japanese language. Installing Japanese as a primary or secondary language is a separate task that you must perform on an IBM i virtual machine.
  {: note}



- To change the service tools language of your IBM i system, see [Changing the service tools language of your system or logical partition](https://www.ibm.com/docs/en/i/7.6.0?topic=mst-changing-service-tools-language-your-system-logical-partition){: external}.



- The COR stock OS image can be used to deploy a second IBM i virtual machine. The second IBM i virtual machine that is deployed contains the language media that can be used to install primary and secondary languages on other IBM i virtual machines.

For more information about IBM i network and software installation, see:

- [Setting up an IBM i network install server](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-preparing-install-server){: external}
- [Globalization and IBM i software installation](https://www.ibm.com/docs/en/i/7.6.0?topic=installation-globalization-i-software#rzahcglobalconsider){: external}
