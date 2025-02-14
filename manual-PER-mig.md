---

copyright:
  years: 2022, 2024

lastupdated: "2025-02-14"

keywords: Power edge router migration, PER migration, migration, manual PER migration

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Migrating the existing network configurations to Power Edge Router
{: #migrate-ws-per}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---


All the IBM {{site.data.keyword.powerSys_notm}} data centers are PER-enabled, except `CHE01` and `MON01`.

If you have manually configured the network configurations in your workspace without customizations through a support ticket, you can use self-service automation to complete your PER migration.




You must have access to Direct Link to complete your PER migration. For more information about roles with access rights, see [Access role requirements for Power Virtual Server](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-managing-resources-and-users#access-roles-requirement).
{: note}





The automation to migrate an existing network to PER is supported via CLI. Use [ibmcloud pi workspace action](https://cloud.ibm.com/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1){: external} command. For more information, see [Migrating to PER](/docs/power-iaas?topic=power-iaas-per#migrate-per).

If you have manually configured the subnets and Direct Link through a support ticket, consider migrating your workspace to Power Edge Router (PER) through a support ticket. With PER, you can use the built-in redundancy and higher bandwidth.


To migrate your workspace to PER through a support ticket, complete the following steps:



1.	Create a [case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} from the **Support Center** of IBM Cloud.
2.	Select **Workspace for {{site.data.keyword.powerSys_notm}}**under **Topic** and **Power VS Network Related** under **Subtopic**.
3.	Provide a short description of your migration requirements in the **Subject**.
4.	In the **Description** box under additional information, provide the following information and click **Next**:
    1.  The CRN (Cloud Resource Name) of your workspace that you want to upgrade.
    2.	The list of subnets configured in the workspace.
    3.	The list of Direct Link connections to which the subnets are attached.

    The IBM {{site.data.keyword.powerSys_notm}} operation team processes the support ticket by configuring the PER and other network devices in parallel to the Direct Link configuration. When the PER configuration is complete, you are notified through a ticket update that the PER configuration is ready for your validation and testing.

5.	Schedule a maintenance window, during which you need to provision the Transit Gateway to conclude the PER network construction. See the [PER use cases](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-use-cases) for more information. To force the network to go through the PER network, complete the following steps:
    1.	From the IBM Cloud catalog, browse your provisioned Direct Link connections.
    2.	Click a Direct Link connection to open the connection details page.
    3.	Click the **BGP** tab and then open the **Route Filter** details.
    4.	Under **Import route filters** and **Export route filters**, select **Deny all import routes** to block the Direct Link routes and force the traffic to go through the PER network.

    Repeat the preceding steps for each of the Direct Link connections. If you face any PER connectivity problem, you can revert to the Direct Link path. To revert, select **Permit all import routes** to unblock the Direct Link routes and disconnect the workspace from the Transit Gateway.

6.	Upon successful testing, for example, through a ping test, [delete the Direct Link connections](/docs/dl?topic=dl-delete-direct-link-gateway&interface=ui) and notify IBM by updating the ticket.
7.	The {{site.data.keyword.powerSys_notm}} team marks the workspace as `Migrated` and closes the ticket.

After the workspace is migrated to the PER network through the ticketing process, continue to refer to the support ticket for network configuration information (subnet create, delete, and update gateway). Before you delete your old migrated workspace, open a support ticket to remove the configuration of the backend devices. Then, you can delete the workspace.
{: important}

## Running a Full Linux Subscription (FLS) on the migrated workspace
{: #fls-migrated-sub}

Following are the two ways to run the FLS with the migrated workspace.

1. FLS works if you update the migrated subnets with DNS IP addresses.

    Update the migrated subnet by adding DNS IP addresses such as `161.26.0.10` or `161.26.0.11`.

    Use the command-line to run the following command in your terminal:

    `ibmcloud pi netu Network_ID --dns-servers "127.0.0.1 161.26.0.10 161.26.0.11`

2. For existing virtual server instances that are deployed by using migrated subnets, add the following two DNS IP's or specific DNS IP addresses of your environment to `/etc/resolv.conf` file:

    * `nameserver 161.26.0.10`
    * `nameserver 161.26.0.11`

## Additional information on PER migration
{: #add-info-per-mig}

If you need to make extra changes after you complete the migration to configure the backend devices, complete the following actions:
- Create a subnet: Create the subnet in the {{site.data.keyword.powerSys_notm}} UI and then open a support ticket for the {{site.data.keyword.powerSys_notm}} operations team to configure the subnet on the backend devices.
- Update or delete a subnet: First, open a support ticket so that the {{site.data.keyword.powerSys_notm}} operations team can update or delete the changes in the backend devices. You can then update or delete the subnet from the {{site.data.keyword.powerSys_notm}} UI.
