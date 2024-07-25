---

copyright:
  years: 2023

lastupdated: "2024-07-24"

keywords: creating workspace resources, {{site.data.keyword.powerSys_notm}}, private cloud, workspace

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}



# Creating a workspace for IBM {{site.data.keyword.powerSys_notm}} Private Cloud
{: #creating-workspace-private-cloud}





IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

A workspace is a container of {{site.data.keyword.powerSys_notm}} resources at a specific geographic location (region). Compute (for example, images and virtual server instances), networking (for example, subnets and VPN connections), and storage (for example, volumes and snapshots) resources are deployed within a specific workspace and cannot be moved or shared between workspaces.
{: shortdesc}

You can create a workspace once the pod setup at your data center is complete and a satellite location is created. Within each location, you can create multiple workspaces. For example, you can create two workspaces in the Dallas location: a workspace for production workloads and another workspace for development tests. Workspaces are a means of grouping and managing related resources that are deployed in a single location. Billing is done on components of the workspace.


You must have the necessary platform roles and "Read" access to the Satellite location instance to create and modify the workspace instances. A client-side administrator can control the access policies by assigning the necessary roles to users. An administrator can also control the access policies to view, create, and modify resources within a workspace.

{{site.data.keyword.powerSys_notm}} provides a default workspace that is associated to your Satellite location instance. Complete the following steps to create workspaces based on your requirements:

You can create a workspace only if the pod setup at your data center is complete and a satellite location is created.
{: Note}

1. Log in to the [IBM catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the catalog's search box, type **{{site.data.keyword.powerSys_notm}}** and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Create a workspace**.

4. Select the **Location type** as On-premises.

5. Select the **Sattelite location** that you created for the IBM Cloud region that is closest to the physical location of your data center.

6. Select the details such as name and resource group that is listed under **Details**.

7. Click **Create**.
   When the workspace is created, you are redirected to the **Workspaces** page where you can select the workspace that you created.
