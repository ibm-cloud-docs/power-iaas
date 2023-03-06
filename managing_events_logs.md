---

copyright:
  years: 2019, 2023

lastupdated: "2023-03-06"

keywords: power systems, event logs, events, notifications, view logs, customize notifications

subcollection: power-iaas

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:term: .term}

# Managing Events logs and notifications
{: #manage-event-logs}

The {{site.data.keyword.powerSysFull}} logs all the events and notifications from the IBM cloud console. You can access them from the **Event logs** page in the user interface.
{: shortdesc}

Consider the following for the event logs and notifications:

* The **Event logs** page shows a maximum of 400 latest entries from the current and previous months. For more information, see [Accessing the event logs](/docs/power-iaas?topic=power-iaas-manage-event-logs#access-event-logs).  
* You can choose to enable or disable notifications for events for all workspaces. For more information, see [Customizing the log notification settings](/docs/power-iaas?topic=power-iaas-manage-event-logs#set-event-logs).
* If you have disabled the notifications, you can still access the logs from the **Events logs** page.
* You can also enable or disable notifications from concurrent users within the same workspace. 
* The custom notification settings you choose gets tied to your user account and is applicable for all workspaces.
 
## Accessing the event logs
{: #access-event-logs}

You can access a maximum of 400 events from the current and previous month in the IBM cloud console. To see the events log, perform the following steps:

1.	Log in to the [IBM catalog](https://cloud.ibm.com/catalog){: external} with your credentials.
2.	In the catalog's search box, type **{{site.data.keyword.powerSysFull}}** and click the **Workspace for {{site.data.keyword.powerSysFull}}** tile.
3.	Click **Select workspace** on the left navigation under workspace of the {{site.data.keyword.powerSysFull}} user interface to select from a list of previously created workspaces. 
    If you do not have a workspace, click **Create a workspace**.
4.	Click **Event logs** to see the list of event logs and notifications.

## Customizing the log notification settings
{: #set-event-logs}

You can customize your notifications to stop getting notifications or stop getting notifications from other concurrent users in the same workspace. To customize the log notification settings, perform the following steps:

1.	Access the **Event logs** page from the user interface. For more information, see [Accessing the event logs](/docs/power-iaas?topic=power-iaas-manage-event-logs#access-event-logs).
2.	Click **Log notification settings** on the top right corner of the page.
3.	Toggle the **Show notifications based on the settings below** button to on or off based on your requirement.
    | Toggle notification button status |	Description |
    |-----|------|
    | On	| Shows notification based on other subset parameters that you can choose. |
    | Off | All notifications are disabled |
    {: class="simple-tab-table"}
    {: caption="Table 1. Notification toggle button options" caption-side="top"}
    {: #noti-toggle}
4.	When the **Show notifications based on the settings below** button toggle is set to on, you can further toggle the **Show for events requested by others** button to on or off based on your requirements.
    | Toggle workspace notification button status |	Description |
    |---------|----------|
    | On | Shows notification based on events requested/performed by concurrent users in the same workspace. |
    | Off |	The following condition applies: \n * Shows notifications for events requested/performed by you for the current workspace. \n * Hides notifications based on events requested/performed by concurrent users in the same workspace. |
    {: class="simple-tab-table"}
    {: caption="Workspace notification toglle button options" caption-side="top"}
    {: #workspace-noti-toggle}
5. Click **Save**.