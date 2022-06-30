---

copyright:
  years: 2019, 2022

lastupdated: "2022-06-30"

keywords: license keys, system service tools, dedicated service tools, network configuration, ibm i, ssh tunneling

subcollection: power-iaas

---

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

IBM i 7.1 VMs support only 64 storage volumes per VM. IBM i 7.2, and later, VMs support up to 127 storage volumes per VM.
{: note}

## Working with the IBM i console
{: #opening-console}

To open the IBM i console, complete the following steps:

1. Go to **Virtual server instance** in the {{site.data.keyword.powerSys_notm}} user interface and click your IBM i VM instance.
2. Click **VM actions** in the server details pane and select **Open console** from the drop-down list.

    IBM i console opens as a popup window. Ensure that your browser setting does not block this popup window.
    {: note}

    ![IBM i console](./images/ibm-i-console.png "IBM i console"){: caption="Figure 2. IBM i console" caption-side="bottom"}

## Tips for working with the IBM i console
{: #tips-ibmi}

- The standard IBM i user is `QSECOFR/QSECOFR`.
- IBM i uses function keys extensively. At the bottom of the console, you can see **PF1** through **PF12**. To get to **PF13** to **PF24**, click the **Next...** button.
- If you see a red **X** in the console during the configuration process, use your keyboard's **CONTROL** button to exit.
- You can use **CONTROL+W** to end a hung session. If this happens, you must perform a bypass by clicking **PF18** and logging on again.
- It's best to first shut down the system before you restart it.
- **Do not restart the system until the `cloud-init` process is finished and you've configured the local IP address**. If you restart the system during the `cloud-init` process, you must call support or delete and reprovision your IBM i VM instance.
- If you are using a Mac computer, the **Page Down** key is the same as **FN + Down Arrow**.
- Change the password on the **Dedicated Service Tools (DST) Sign On** screen. Use **PF5** to change the DST password.
- On the next screen, select **Option 1** to **Perform an IPL**. The sign-on screen appears after the IPL completes. Change the system `QSECOFR` ID password. New security rules require at least a 15-character password.
- `CRTUSRPRF` and `CHGUSRPRF` will also use these new security rules. 

## Licenses and configuring your network
{: #license-network}

You must install the [minimum program temporary fix (PTFs) levels](/docs/power-iaas?topic=power-iaas-minimum-levels) on your IBM i VM.

After you deploy an IBM i VM and install the proper PTFs, you need to accept the license agreements. To accept the license agreements from the console, you must press **5** on each license agreement to display them. Click **PF14** to accept each agreement. Click **Next...** and **PF15** to show more items. After you accept the license agreements, press **PF3** and wait until `cloud-init` configures your network and injects your license keys.

The `cloud-init` configuration process can take up to 5 minutes. **Do not restart your system** while `cloud-init` is running. If you restart your system during this time, you must call IBM support to manually configure your network and license keys.
{: important}

To verify that `cloud-init` configured your IP addresses correctly, type the `cfgtcp` command in the IBM i console window and choose `1`. If the two IP addresses match the internal IP addresses of your VM, the `cloud-init` configuration ran successfully.

![Verifying the cloud-init configuration](./images/terminal-ibmi-cfgtcp.png "Verifying the cloud-init configuration"){: caption="Figure 3. Verifying the cloud-init configuration" caption-side="bottom"}

If you do not see the external IP address in the **Work with TCP/IP Interfaces** window, wait approximately 10 minutes, open another terminal and ping the external IP address. The external address must match what is shown in the {{site.data.keyword.powerSys_notm}} user interface within your instance's **Server details** pane. Contact support or delete and reprovision your IBM i VM if the ping doesn't return anything.

Lastly, enter the `WRKLICINF` command and F11 to display the usage information to verify that the `cloud-init` injected the license keys correctly. After you verify your network and license key configuration, you can initial program load (IPL) the LPAR.

If License Keys for the operating system or any IBM i Licensed Program Products (LPP) have not been applied, follow instructions in the [PowerVS license key issues](https://www.ibm.com/support/pages/mustgather-powervs-license-key-issues){: external} document.

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

1. Enter the  `wrksysval qipltype` command and change the value to **1**. The `wrksysval qipltype` command changes the `sysval QIPLTYPE` value.

2. Enter the `pwrdwnsys` command with the `RESTART` parameter to restart the IBM i operating system (OS).

3. At the DST console on restart, enter `QSECOFR/QSECOFR` and change the password.

4. Enter the `wrksysval qipltype` command and change the value to **0**.

5. Reenter the `pwrdwnsys` command with the `RESTART` parameter to restart the IBM i OS again. You can now log in, run `STRSST`, and manage the newly attached disk as the password is manageable.

6. Proceed to [Connect to an IBM i virtual machine (VM)](/docs/power-iaas?topic=power-iaas-connect-ibmi) to connect to your IBM i Cloud VM. -->

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
  