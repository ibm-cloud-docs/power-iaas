---

copyright:
  years: 2019, 2026 

lastupdated: "2026-10-27"

keywords: license keys, system service tools, dedicated service tools, network configuration, ibm i, ssh tunneling

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring your IBM i VSI
{: #configuring-ibmi}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Use these instructions to start and configure your IBM i-based virtual server instance (VSI).
{: shortdesc}

IBM i 7.3 or later stock images support up to 127 storage volumes per VSI by default. To support up to 508 storage volumes, configure the VSI settings.
{: note}

## First boot of IBM i
{: #first-boot}

When you use IBM i 7.5 or later stock OS image on an {{site.data.keyword.powerSysFull}}, you must first reset the dedicated service tools (DST) password for the IBM i standard user `QSECOFR` through the console. Complete this step within an hour of VSI deployment for TCP configuration to complete.

The IBM i standard user `QSECOFR` is set to the password `QSECOFR`. You must change it to a 15-character password (no blank spaces) through the VSI console. For tips on working with the IBM i console, see [Tips for working with the IBM i console](/docs/power-iaas?topic=power-iaas-configuring-ibmi#tips-ibmi).

For steps on changing the DST password, see [Changing the DST password](#first-boot-change-dst-password).
{: note}



### Accessing the VSI console
{: #first-boot-access-vsi-console}

To open the VSI console on the first boot, complete the following steps:

1. Go to the **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and select your IBM i-based VSI. The Virtual server instance details page appears.
2. Click **VM actions** and select **Open console** from the drop-down list. The Console Setting dialog appears.
3. Select **037 English** from the **Console language** drop-down list.
4. Click **Open console**. The IBM i console opens in a new window. Ensure that your browser settings allow pop-up windows.

    The idle timeout for the VSI console is 2 hours.
    {: important}




To disconnect from the VSI console session, close the web browser window that is titled 'noVNC'.

If you lose internet connectivity, your VSI console session (provided through noVNC) displays an error and does not auto-connect when internet connectivity is restored.

To restore the VSI console session, complete the following steps:

1. Return to the IBM Power Virtual instance.
2. Click **VM actions** in the Virtual server details page and select **Open console** from the drop-down list. The session is restored and the 'Connected (encrypted)' message appears.

Alternatively, if you have multiple IBM i-based VSIs you can use the IBM Cloud CLI to return the VSI console session URL, such as using a shell command loop:

```shell
ibmcloud pi workspace list
ibmcloud pi workspace target <<IBM_POWER_VS_WORKSPACE_CRN>>
for i in $(ibmcloud pi instance list --json | jq -r '.pvmInstances.[] | select(.operatingSystem.type=="ibmi").id'); do echo "" && ibmcloud pi instance console get "$i"; done
```

### Changing the DST password
{: #first-boot-change-dst-password}

When the VSI console is loading and the IBM i console screen appears (IBM i 7.5 or later), complete the following steps to reset the password of the IBM i standard user:

For releases before IBM i 7.5, the System Sign-on screen appears first, where you must reset the `QSECOFR` password.
{: note}

1. In the VSI console window, when the IBM i VSI waits on the **Dedicated Service Tools (DST) Sign On** screen, type `QSECOFR` and then click **PF5** to open the change password screen.
2. When the **Change Service Tools User Password** screen loads, place the cursor on `Current password . . . .` and enter `QSECOFR`.
3. Press the TAB key to move the cursor to the `New password . . . .` field and enter a 15 character password (no blanks).
4. Repeat the step on the `New password (to verify) . . . .` field and enter the new password again.
5. Press ENTER to continue. If you enter the password incorrectly, try again. If a warning message about locking the user appears, click **PF3** and start again.
6. The **IPL or Install the System** screen appears.



If the DST sign-on screen displays the message `ATTENTION: This device can become the console`, press **F18** to bypass the screen and continue. This message appears if the console session is interrupted and reconnected during deployment.
{: note}



You can now configure the IBM i VSI. Select whether to perform an Initial Program Load (IPL), install the OS, or perform an automated OS install.

Option 1 (**Perform an IPL**) is selected by default.

### Reviewing software agreements
{: #first-boot-review-software-licenses}

When the installation is complete, the **System Sign-On** screen appears. Follow the [Changing the DST password](#first-boot-change-dst-password) procedure to change the `QSECOFR` password. After the system sign-on is complete, accept the Licensed Program Software Agreements.

1. After you log in, the system displays the **Software Agreements** screen.
2. To accept the license agreements from the console, press **5=Display** for each license agreement and press ENTER.
3. Press **F14** to accept each agreement.
4. After you accept all agreements, press ENTER. The IBM i main menu appears.
5. After the IBM i main menu appears, cloud-init configures the network and inject the license keys. This process can take up to 5 minutes.
6. Confirm that the system has the [Minimum PTF levels for IBM i](/docs/power-iaas?topic=power-iaas-minimum-levels).


## Tips for working with the IBM i console
{: #tips-ibmi}

- The standard IBM i user/password is `QSECOFR/QSECOFR`.
- IBM i uses function keys extensively. In the console, you can see **PF1** through **PF12**. To get to **PF13** to **PF24**, click the **Next...** button.
- If you see a red **X** in the console during the configuration process, use your keyboard's **CONTROL** button to exit.
- You can use **CONTROL+W** to end a hung session. If this error occurs, you must perform a bypass by clicking **PF18** and logging on again.
- Shut down the system before you restart it.
- If you are using a Mac computer, the **Page Down** key is the same as **FN + Down Arrow**.
- `CRTUSRPRF` and `CHGUSRPRF` use the same new security rules as `QSECOFR`, requiring at least a 15 character password.


## Verifying licenses and network configuration
{: #verify-licences-and-network-configuration}


To resolve an issue with expired operating system licenses when you deploy IBM i images, complete the following steps on the IBM {{site.data.keyword.powerSys_notm}} console:

1. After you change the default login password for the OS in an IBM i VSI, the Operating System License Information screen appears. If you see the error message `No operating system licenses are available at this time.`, wait 15 minutes.
2. Press **F5** to retry license verification and to continue with the sign-on process.
3. Accept Software Agreements.
4. Run IBM i command `STRSBS QBASE` or `STRSBS QCTL` to exit restricted state.
5. Run IBM i command `CFGTCP` to verify whether the TCP/IP configuration is complete.

If the stock image is deployed without displaying the Operating System License Information screen, run the `STRSBS QBASE` command within one hour of the VSI deployment. For more information, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support-pvs).




To verify that `cloud-init` configured your IP addresses correctly, on the **IBM i main menu** screen type the `cfgtcp` command in the console window (on line Selection or command ===>), press ENTER, choose `1`, and press ENTER again.

Verify that one or more IP addresses with **Line Description** `CLOUDINIT<<0..n>>` appear and match the network interfaces for the attached IBM Power VS network subnets that appear in the IBM Power Virtual Server workspace. If the IP addresses match, the `cloud-init` configuration completed successfully.

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

For external IP addresses, if you do not see the external IP address in the **Work with TCP/IP Interfaces** screen, wait approximately 10 minutes, open another terminal, and ping the external IP address. The external address must match what appears in the {{site.data.keyword.powerSys_notm}} user interface on your instance's **Server details** page. If the ping returns no response, contact support or delete and reprovision your IBM i VSI.


Finally, on the **IBM i main menu** screen, type the `WRKLICINF` command in the console window (on line **Selection or command ===>**), press ENTER, and then click **PF11** to display the usage information. The Usage Limit, Usage Count, and Peak Usage values must be populated for each license.

After you verify your network and license key configuration, perform an IPL on the LPAR.

If license keys for the operating system or any IBM i licensed program Products (LPP) are not applied, follow instructions in the [PowerVS license key issues](https://www.ibm.com/support/pages/mustgather-powervs-license-key-issues){: external} document.

If this system is an upgrade that previously contained license keys, allow a weekend (Saturday–Sunday) to process the updated keys before you collect the [PowerVS license key issues](https://www.ibm.com/support/pages/mustgather-powervs-license-key-issues){: external} information.

Updating the IBM i VSI license and memory at the same time might cause a timeout error.
{: note}



## Changing the system service tools (SST) and DST passwords
{: #sst-dst}

The SST and DST passwords are expired by default. Complete the following steps to access SST and change the passwords.

To change the SST and DST passwords, complete the following steps:

1. Go to the **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VSI. The Virtual server instance details page appears.
2. Click **VM actions** in the Virtual server details page and select **IBM i operations** from the drop-down list. The IBM i operations dialog appears.
3. Select **(21) Active dedicated service tools** option from the list displayed on the **Control Panel functions** tab.
4. Click **Run action**.


For more information about user ID types, see [Managing service tools user IDs](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzamh/rzamhmanageuserids.htm){: external}.
{: note}

## Managing the IBM i VSI instance
{: #manage-IBMi-VM}

You can use the **IBM i operations** option to run control panel functions and configure VSI boot operations. Complete the following steps:

1. Go to the **IBM Power Virtual Server** instance in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VSI. The Virtual server instance details page appears.
2. Click **VM actions** in the Virtual server details page and select **IBM i operations** from the drop-down list. The IBM i operations dialog appears.

The **IBM i operations** option is available only for the IBM i VSIs.
{: note}

3. In the IBM i operations dialog, select one of the following actions from the **Control panel functions** tab based on your requirements:

   Job operations:

     - **(21) Activate dedicated service tools** – Activates DST and makes it available on the system console display. You can use DST from the system console display to work with Licensed Internal Code (LIC), disk units, configuration and resources, and to verify devices and communications.

     - **(34) Retry Dump** – Retries a failed main storage dump (MSD) operation. You can run this function when the VSI is hung during the MSD operation or when you want to reattempt the initial program load (IPL) operation without losing the original dump information.

     - **(66) Enable remote service** - Activates the communications port that is used by a remote service session or operations console.

     - **(67) Disk unit IOP reset/reload** - Initiates an I/O processor (IOP) dump operation and a disk unit IOP reset or reload operation. This function is available only when specific system reference codes (SRCs) appear on the control page and the associated IOP supports a reset or reload operation. This function is not available for all system types.

     - **(70) IOP Control storage dump** - Saves the contents of the service processor control storage into a nonvolatile storage for potential use from an error log file.

     - **(22) Dump restart** - Copies main storage data and processor data to the disk. Run this function only when an MSD operation is necessary, for example, after a suspended (system hang) condition or after an operating system failure.

      You must not shut down the system before the MSD operation. This action can cause data loss.
      {: note}

4. In the IBM i operations dialog, select one of the following options from the **Boot operations** tab based on your requirements:

    Server boot mode
    :   - **A-** Perform an IPL operation from a disk by using the copy A of the system LIC.
        - **B-** Perform an IPL operation from a disk by using the copy B of the system LIC.
        - **C-** Reserved for IBM lab use only.
        - **D-** Perform an IPL operation from a media other than the load-source disk. Perform an alternative IPL operation for code installation support.

    Server operating mode
    :   - **Normal** - Allows you to access the operating system and perform an unattended IPL operation. After the system power-on, operating the system in **Normal** (unattended) mode requires no operator intervention during the IPL operation. When you turn on the system in **Normal** mode, the system performs the IPL operation and presents the **Sign On** display on all available display stations. The operator cannot change the internal system environment during the IPL operation. Dedicated service tools (DST) and the operating system do not present any menus or options during this IPL operation.
        - **Manual** - Allows you to access DST and perform an attended IPL operation. After the system power-on, operating the system in Manual (attended) mode means that an operator uses the **Operation** page or the control page to direct the system for special needs. During the IPL operation in **Manual** mode, DST and the operating system present menus and prompts you to change the internal system environment. These modifications can include entering debug mode for service representatives to diagnose difficult problems. For more information, see [Operating mode of an IPL](https://www.ibm.com/docs/en/i/7.6.0?topic=panel-operating-mode-ipl){: external}.

5. Click **Run Action**.




## IBM i language support
{: #ibmi-language-support}

By default, the IBM i VSI console uses English and supports the following languages:

- IBM i stock OS images support English (2924) or English DBCS (2984). You can install secondary languages and change the primary language on an IBM i VSI.

- The VSI console also supports Japanese if it is installed as a primary or secondary language.

    If you select Japanese as the language in the Console Setting dialog before you start the IBM i VSI console, selecting this language option does not install Japanese on the VSI. Installing Japanese as a primary or secondary language is a separate task that you must perform on the IBM i VSI.
    {: note}




- To change the service tools language of your IBM i system, see [Changing the service tools language of your system or logical partition](https://www.ibm.com/docs/en/i/7.6.0?topic=mst-changing-service-tools-language-your-system-logical-partition){: external}.



- Use the COR stock OS image to deploy a second IBM i VSI. The deployed IBM i VSI contains the language media that you can use to install primary and secondary languages on other IBM i VSIs.

For more information about IBM i network and software installation, see:

- [Setting up an IBM i network install server](/docs/power-iaas?topic=power-iaas-preparing-install-server){: external}
- [Globalization and IBM i software installation](https://www.ibm.com/docs/en/i/7.6.0?topic=installation-globalization-i-software#rzahcglobalconsider){: external}



## Considerations for IBM i and Global Replication Services
{: #ibmi-grs-io}

If you plan to use Global Replication Services to replicate your IBM i VSI volumes, review the recommended volume group limits and their impact on I/O response times. For more information, see [Performance and I/O considerations for GRS](/docs/power-iaas?topic=power-iaas-getting-started-GRS#performance-IO-time).
