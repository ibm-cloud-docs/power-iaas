---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-07"

keywords: power, power systems, event logs, events, notifications, view logs, customize notifications

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing events logs and notifications
{: #manage-event-logs}

The {{site.data.keyword.powerSysFull}} logs all the events and notifications from the IBM Cloud console. You can access these events and notifications in the **Event logs** page.
{: shortdesc}

Consider the following points when you are working with the event logs and notifications:

* The **Event logs** page shows a maximum of 400 entries from the current and previous months.
* You can choose to enable or disable notifications for events on all workspaces. For more information, see [Customizing the log notification settings](/docs/power-iaas?topic=power-iaas-manage-event-logs#set-event-logs).
* If you disable the notifications, you can still access the logs from the **Event logs** page.
* You can customize notifications; for example, you can enable or disable notifications from concurrent users within the same workspace.
* Your changes to the notification settings are associated with your user account and apply to all workspaces.
* Your every action or operation does not create a log that you can view in the Event logs page.

## Accessing the event logs
{: #access-event-logs}

You can access a maximum of 400 events for the current and previous months in the IBM Cloud console. To see the event logs, complete the following steps:

1.	Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.
2.	In the catalog's search box, type **{{site.data.keyword.powerSysFull}}**, and click the **Workspace for {{site.data.keyword.powerSysFull}}** tile.
3.	Click **Select workspace** on the left navigation under workspace of the {{site.data.keyword.powerSysFull}} user interface to select from a list of previously created workspaces.
    If you do not have a workspace, click **Create a workspace**.
4.	Click **Event logs** to see the list of event logs and notifications.

## Customizing the log notification settings
{: #set-event-logs}

You can stop the notifications or stop getting notifications from other concurrent users in the same workspace. To customize the log notification settings, complete the following steps:

1.	Access the **Event logs** page from the user interface. For more information, see [Accessing the event logs](/docs/power-iaas?topic=power-iaas-manage-event-logs#access-event-logs).
2.	Click **Log notification settings**.
3.	Toggle the **Show notifications based on the settings below** button to on or off based on your requirement.
    | Toggle notification button status |	Description |
    |-----|------|
    | On	| Shows notification based on other subset parameters that you can choose. |
    | Off | All notifications are disabled. |
    {: caption="Table 1. Notification toggle button options" caption-side="top"}
    {: #noti-toggle}

4.	When the **Show notifications based on the settings below** button toggle is set to on, you can further toggle the **Show for events requested by others** button to on or off based on your requirements.
    | Toggle workspace notification button status |	Description |
    |---------|----------|
    | On | Shows notification based on events that are requested or performed by concurrent users in the same workspace. |
    | Off |	Shows notifications for events that are requested or performed by you for the current workspace. It also hides notifications based on events that are requested or performed by concurrent users in the same workspace. |
    {: caption="Table 2. Workspace notification toglle button options" caption-side="top"}
    {: #workspace-noti-toggle}

5. Click **Save**.
