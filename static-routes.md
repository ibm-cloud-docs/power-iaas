---

copyright:
  year: 2025

lastupdated: "2025-07-24"

keywords: Network routes, static routes, custom route, route table, routes for high availability (ha) and disaster recovery (da)

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating and managing network routes in IBM {{site.data.keyword.powerSys_notm}} workspaces
{: #routes}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

---

A network route is a defined path that data packets follow to travel from a source to a destination across a network. You can use the routes feature in the {{site.data.keyword.powerSysFull}} to view implicit network routes and to create or manage static routes within your {{site.data.keyword.powerSys_notm}} workspaces. Static routes are custom routes that control where the network packets are sent, depending on the destination Classless Inter-Domain Routing (CIDR) and the specified next hop address. The next hop is the IP address to which you want to route the network packet.
{: shortdesc}

With static routes, you can build an overlay network by using CIDRs that are not associated with subnets in your {{site.data.keyword.powerSys_notm}} workspace to implement high availability (HA) and disaster recovery (DR) strategies. You can also view external network routes to identify which external destinations are accessible from your {{site.data.keyword.powerSys_notm}} workspace.

The routes feature is available only on the PER-enabled {{site.data.keyword.powerSys_notm}} workspaces. For more information, see [Getting started with the Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
{: note}

## Creating static routes
{: #creating-routes}

To create a static route in your {{site.data.keyword.powerSys_notm}} workspace, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Click **Workspaces** in the left navigation menu.
3. Select a workspace in which you want to create the static route. The "Workspace details" panel is displayed.
4. Click **View virtual servers**.
5. In the navigation pane, click **Networking** > **Routes**. The Routes page is displayed with a list of any existing static routes on the **Static routes** tab.
6. Click **Create static route** to create a static route. The "Create static route" panel is displayed.
7. Enter a name in the **Name** field.
8. Optional: Enter user tags in the **User tags (optional)** field.
9. Enter the destination IP address in the **Destination** field and the next hop IP address in the **Next hop** field.
10. Set one of the following values for **Advertise**:
    - **Enabled**: Default. If **Advertise** is set to **Enabled**, the static route is advertised to the external connections.
    - **Disabled**: If **Advertise** is set to **Disabled**, the static route is not advertised to the external connections.
11. Set one of the following values for **Status**:
    - **Enabled**: Default. If **Status** is set to **Enabled**, the static route is enabled within the network fabric.
    - **Disabled**: If **Status** is set to **Disabled**, the static route is disabled within the network fabric.

    If you set **Status** to **Disabled**, the static route is not advertised to the external connections, even if **Advertise** is set to **Enabled**.
    {: important}

12.	Click **Create route**.

The static route destination is currently limited to a single IP address (/32 CIDR) and must not overlap with the local subnet or any subnets that are derived from it.
{: note}

The static route that you created is displayed on the **Static routes** tab. The State column indicates one of the following operational statuses of each static route:

- **Deployed**: Indicates that the static route is active and the next hop IP address exists within a subnet that is defined in the {{site.data.keyword.powerSys_notm}} workspace. Routes in the deployed state are advertised externally when **Advertise** is set to **Enabled**.

- **Defined**: Indicates that the static route is configured but not yet deployed or active. A static route might be in the defined state when the specified next hop IP address does not currently exist in any subnet within the {{site.data.keyword.powerSys_notm}} workspace.

  Routes in the defined state are not used for forwarding network traffic and is not advertised externally even if **Advertise** is set to **Enabled**. However, after a subnet that includes the next hop IP address is created, the static route automatically becomes active and the status is changed to **Deployed**.

- **Disabled**: Indicates that the static route is manually disabled by setting **Status** to **Disabled**. Routes in the disabled state are not used for forwarding traffic and are not advertised externally.


## Modifying static routes
{: #modifying-routes}

You can edit an existing static route to modify its name, destination IP address, next hop IP address, and the advertise and status options. To modify a static route in your {{site.data.keyword.powerSys_notm}} workspace, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Click **Workspaces** in the left navigation menu.
3. Select a workspace in which you want to create the static route. The "Workspace details" panel is displayed.
4. Click **View virtual servers**.
5. In the navigation pane, click **Networking** > **Routes**. The Routes page is displayed with a list of any existing static routes on the **Static routes** tab.
6. Click the overflow menu (icon with 3 vertical dots) on the static route entry that you want to modify and select **Edit**. The "Edit static route" panel is displayed.
7. Modify the route details and click **Edit route**.

You can modify the static routes by using the GUI, API, CLI, and Terraform interfaces.
{: note}

## Deleting static routes
{: #deleting-routes}

To delete a static route in your {{site.data.keyword.powerSys_notm}} workspace, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Click **Workspaces** in the left navigation menu.
3. Select a workspace in which you want to create the static route. The "Workspace details" panel is displayed.
4. Click **View virtual servers**.
5. In the navigation pane, click **Networking** > **Routes**. The Routes page is displayed with a list of any existing static routes on the **Static routes** tab.
6. Click the overflow menu (icon with 3 vertical dots) on the static route entry that you want to delete and select **Delete**. The "Delete static route" dialog is displayed.
7. Click **Delete** to delete the static route.

You cannot recover a static route after it is deleted.
{: important}

When you delete a workspace, all the static routes that were created within that workspace are also deleted.
{: important}

## Viewing external routes
{: #external-routes}

The external routes tab displays all external networks and subnets with which your {{site.data.keyword.powerSys_notm}} workspace can communicate through the connected infrastructure, such as IBM Cloud Transit Gateway. The external routes are learned from external sources, such as other {{site.data.keyword.powerSys_notm}} workspaces, VPCs, or other on-premises networks. You can use the external routes information to identify the external destinations that are accessible from your {{site.data.keyword.powerSys_notm}} workspace.

To view the external routes, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Click **Workspaces** in the left navigation menu.
3. Select a workspace in which you want to create the static route. The "Workspace details" panel is displayed.
4. Click **View virtual servers**.
5. In the navigation pane, click **Networking** > **Routes**. The Routes page is displayed with a list of any existing static routes on the **Static routes** tab.
6. Click the **External routes** tab. The available external routes are displayed.
