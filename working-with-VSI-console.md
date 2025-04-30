---

copyright:
  year: 2025

lastupdated: "2025-04-30"

keywords: VSI console, Power virtual server instance console, AIX console, IBM i console, PowerVS console, VTERM, vterm

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Working with the VSI console
{: #vsi-console}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

The Virtual Server Instance (VSI) console in the {{site.data.keyword.powerSysFull}} environment, also known as VTERM, is an important utility that you can use to interact with the AIX, IBM i, and Linux-based Power virtual servers. The VSI console performs several management and troubleshooting activities. The VSI console provides the following benefits:

- Provides access to the AIX, IBM i, and Linux-based VMs (Linux, SAP HANA, and SAP NetWeaver) to perform various OS-related tasks such as installation, configuration, troubleshooting, and recovery
- Debugs VM boot issues
- Resets the Dedicated Service Tools (DST) password for the IBM i standard user

## Starting the VSI console for a {{site.data.keyword.powerSys_notm}} instance
{: #opening-vsi-console}

To start the VSI console of a {{site.data.keyword.powerSys_notm}} instance from the IBM Cloud UI after you [create the instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server){: external}, complete the following steps:

1. Open the [{{site.data.keyword.powerSys_notm}} user interface](https://cloud.ibm.com/power/overview) and log in with your credentials.

2. Click **Virtual server instances** from the left navigation pane in the {{site.data.keyword.powerSys_notm}} user interface. The Virtual server instances page is displayed. A list of the existing virtual server instances that are associated with the selected workspace is displayed on the **Servers** tab.

3. Select a virtual server instance to open the Virtual server instance details page.

4. Click **VM actions** in the Virtual server details page and select **Open console** from the drop-down list. The VSI console opens in a new browser window. Ensure that your browser settings allow pop-up windows.

  When you open the console for an IBM i-based {{site.data.keyword.powerSys_notm}} instance through the IBM Cloud UI, the Console Setting dialog is displayed. You can optionally select a language other than English and click **Open console** to open the VSI console. To change the language, see [Changing the VSI console language](#changing-vsi-console-lang).
  {: note}

To open the VSI console of a {{site.data.keyword.powerSys_notm}} instance by using the IBM Cloud CLI, complete the following steps:

1. To get the URL that you can use to open the VSI console, use the [`ibmcloud pi instance console`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-get) IBM Cloud CLI command. The `INSTANCE_ID` in the following command is the unique identifier or name of the instance and must be replaced with the actual ID of your VSI.

    ```sh
    ibmcloud pi instance console get INSTANCE_ID
    ```
    {: pre}

2. Copy the URL that is generated in the previous step and paste it into the address bar of a web browser. The console window for the VSI is displayed.

## Closing a VSI console session
{: #closing-vsi-console}

To close a VSI console session for a {{site.data.keyword.powerSys_notm}} instance, close the browser window or the tab.

## Changing the VSI console language
{: #changing-vsi-console-lang}

When you open the VSI console of a {{site.data.keyword.powerSys_notm}} instance that is running IBM i as the boot image, you can change the console language from English to another language. To change the language from the IBM Cloud UI, complete the following steps:

1. Open the [{{site.data.keyword.powerSys_notm}} user interface](https://cloud.ibm.com/power/overview) and log in with your credentials.

2. Click **Virtual server instances** from the left navigation pane in the {{site.data.keyword.powerSys_notm}} user interface. The Virtual server instances page is displayed. A list of the existing virtual server instances that are associated with the selected workspace is displayed on the **Servers** tab.

3. Select an IBM i-based virtual server instance to open the Virtual server instance details page.

4. Click **VM actions** in the Virtual server details page and select **Open console** from the drop-down list. The Console Setting dialog is displayed.

5. Select a language from the **Console language** drop-down list.

6. Click **Open console** to open the console using the language that you selected in the previous step.

To change the VSI console language, you can use the [`ibmcloud pi instance console update`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-console-update) IBM Cloud CLI command. The `INSTANCE_ID` and `CODE` in the following command must be replaced with the ID of your VSI and the associated language code:

```sh
ibmcloud pi instance console update INSTANCE_ID --code CODE
```
{: pre}

To view the languages available for an IBM i-based {{site.data.keyword.powerSys_notm}} instance, you can use the following IBM Cloud CLI command:

```sh
ibmcloud pi instance console list
```
{: pre}

Changing the VSI console language on an IBM i-based {{site.data.keyword.powerSys_notm}} instance terminates any open console sessions before a new console session is started.
{: note}

## Sharing the VSI console session
{: #sharing-console-session}

When multiple users open the VSI console for the same {{site.data.keyword.powerSys_notm}} instance, the same VSI console (VTERM) session is shared among all users. When the last user closes the VSI console, the underlying console session is terminated. Reopening the VSI console creates a new VTERM and establishes a new console connection to the VSI on the host.

## VSI console considerations
{: #vsi-console-considerations}

To use the VSI console, consider the following factors:

- {{site.data.keyword.powerSys_notm}} attempts to keep the browser window for the VSI console active and open for up to 2 hours. After the VSI console is idle for 2 hours, the console connection is terminated.

- The connection to the VSI console can be interrupted or disconnected for various reasons, including a disruption in the network connectivity between your workstation and the {{site.data.keyword.powerSys_notm}} host.

- If multiple users connect to the same IBM i-based {{site.data.keyword.powerSys_notm}} instance and one of the users changes the console language and opens the VSI console, the console that is in use by the other users is terminated and requires the console to be reopened.

For more information about how to use the VSI console with IBM i, see [Tips for working with the IBM i console](/docs/en/power-virtual-server?topic=i-configuring-your-virtual-machine-vm#tips-ibmi).
