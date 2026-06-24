---

copyright:
  years: 2019, 2026 

lastupdated: "2026-06-24"

keywords: managing placement groups, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology, video, how-to, placement groups, add placement group, delete placement group

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing server placement groups
{: #managing-placement-groups}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Server placement groups provide you with control over the host or server on which a new virtual server instance (VSI) is placed. By using server placement groups, you can build high availability within a data center.
{: shortdesc}

You can apply an affinity or anti-affinity policy to each VSI within a server placement group. After you create a placement group, you can provision a new VSI in the placement group. When you set a placement group with an affinity policy, all VSIs in the placement group are provisioned on the same server. When you set a placement group with an anti-affinity policy, all VSIs in the placement group are provisioned on different servers.



You can use the user interface for placement groups only when the total number of VSIs in your account is less than 100. If your account has more than 100 VSIs, you must use the CLI or API to create placement groups.
{: important}

## Creating server placement groups by using the {{site.data.keyword.powerSys_notm}} user interface
{: #creating-placement-groups}


You can create server placement groups to provision VSIs with an affinity or anti-affinity policy. Each placement group that you create must have a unique name. You can create a maximum of 25 placement groups. If you need to create more than 25 placement groups, raise a support ticket to increase the maximum limit. Use the following API to create a placement group: [Create a server placement group](/apidocs/power-cloud#pcloud-placementgroups-post).

You can add or remove VSIs within the placement group. You cannot change the policy or name of a placement group after you create it.

To create a placement group, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. From the Workspaces page, select a workspace in which you want to create a server placement group. The Virtual server instances page is displayed.

5. Click the **Server placement groups** tab. The Server placement groups page is displayed with a list of existing placement groups.

6. Click **Create group**. The New placement group panel is displayed.

7. Enter a name for the placement group in the **Name** field.

8. Optionally, add user tags in the **User tags (optional)** field.

9. Select a **Colocation policy**:
   - **Same server**: All VSIs in the placement group are provisioned on the same server (affinity policy).
   - **Different server**: All VSIs in the placement group are provisioned on different servers (anti-affinity policy).

10. Click **Done**.

The new placement group is displayed in the Server placement groups table. The table shows the placement group name, the number of VSIs in the group, and the colocation policy.


## Server placement group APIs
{: #all-placement-groups}

You can use the following APIs for managing server placement groups:

- [Get all server placement groups](/apidocs/power-cloud#pcloud-placementgroups-getall): Displays all existing server placement groups.
- [Get server placement group details](/apidocs/power-cloud#pcloud-cloud-placementgroups-get): Displays details about a specific server placement group.
- [Delete server placement group](/apidocs/power-cloud#pcloud-placementgroups-delete): Deletes server placement groups even if they contain member instances.
- [Remove server from placement group](/apidocs/power-cloud#pcloud-placementgroups-members-delete): Removes a virtual server instance from a server placement group.

## Adding VSIs to a server placement group by using the {{site.data.keyword.powerSys_notm}} user interface
{: #add-server-pgroup}



You can add VSIs to a server placement group.  You cannot add a VSI to a server placement group that contains a VSI in the **Build** state.  You must wait until the VSI changes to the **Active** state before adding another VSI to the server placement group. Use the following API to add a server to a placement group: [Add server to placement group](/apidocs/power-cloud#pcloud-placementgroups-members-post).


When you add a VSI to the server placement group, the request might fail due to a conflict (409) with the affinity policy. In this case, you might need to open a DLPAR operations support ticket. To open a support ticket, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
{: note}

To add a VSI to a placement group, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. From the Workspaces page, select a workspace. The Virtual server instances page is displayed.

5. Click the **Server placement groups** tab. The Server placement groups page is displayed with a list of existing placement groups.

6. From the placement group table, click the placement group name. The placement group details page is displayed.

7. In the **Virtual server instances in placement group** section, you can create a new VSI or add an existing VSI:

   - To create a new VSI, click **Create new** and follow the steps in [Creating a Power Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).

   - To add an existing VSI, click **Add existing**. The Add existing virtual server instance panel is displayed with a list of available VSIs. Select one or more VSIs from the table, and click **Add**.

VSIs that you select must be on the same server or different server based on the colocation policy of the placement group. A VSI can belong to only one placement group, and VSIs that are already placed in a different placement group are disabled in the table.
{: note}
