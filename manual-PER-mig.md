---

copyright:
  years: 2022, 2026 

lastupdated: "2026-07-16"

keywords: Power edge router migration, PER migration, migration, manual PER migration

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Migrating the existing network configurations to Power Edge Router
{: #migrate-ws-per}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---
Power Edge Router (PER) is enabled for all Power Virtual Server data centers except `CHE01`.

If you configured your workspace network without using a support ticket, you can use self-service automation to complete your PER migration.

You must have access to Direct Link to complete your PER migration. For more information about required access roles, see [Access role requirements for Power Virtual Server](/docs/power-iaas?topic=power-iaas-managing-resources-and-users#access-roles-requirement).
{: note}

You can use the [`ibmcloud pi workspace action`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1) CLI command to automate the migration of an existing network to PER. For more information, see [Migrating to PER](/docs/power-iaas?topic=power-iaas-per#migrate-per).

If you manually configured your subnets and Direct Link through a support ticket, consider migrating your workspace to PER by opening a support ticket. With PER, you can benefit from built-in redundancy and increased bandwidth.



[POWERIAAS-15741-end]{: tag-purple}



## Migrating to PER through a support ticket
{: #migrate-per-ticket}

To migrate your workspace to PER through a support ticket, complete the following steps:



1.	Create a [support case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} in the IBM Cloud Support Center.

2.	Select **{{site.data.keyword.powerSys_notm}}** under **Topic**, and select **Power VS Network Related** under **Subtopic**.

3.	In the **Subject** field, provide a brief description of your migration requirements.

4.	In the **Description** box under additional information, provide the following information and click **Next**:

    1.  The CRN (cloud resource name) of the workspace that you want to migrate.

    2.	The list of subnets configured in the workspace.

    3.	The list of Direct Link connections that the subnets are attached to.

    The {{site.data.keyword.powerSys_notm}} operations team processes the support ticket by configuring PER and other network devices in parallel with the Direct Link configuration. When the PER configuration is complete, the team notifies you through a ticket update that the PER configuration is ready for your validation and testing.

5.	Schedule a maintenance window during which you must provision the Transit Gateway to complete the PER network configuration. For more information, see [PER use cases](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-use-cases). To route the network traffic through PER, complete the following steps:

    1.	In the [IBM Cloud console](https://cloud.ibm.com){: external}, from the navigation menu, select **Infrastructure** > **Network** > **Direct link**.

    2.	Click a Direct Link connection to open the connection details page.

    3.	Click the **BGP** tab and then open the **Route Filter** details.

    4.	Under **Import route filters** and **Export route filters**, select **Deny all import routes** to block the Direct Link routes and route traffic through the PER network.

    Repeat the preceding steps for each Direct Link connection. If you encounter any PER connectivity issues, you can revert to the Direct Link path. To revert, select **Permit all import routes** to unblock the Direct Link routes, and then disconnect the workspace from the Transit Gateway.

6.	After successful testing (for example, a ping test), [delete the Direct Link connections](/docs/dl?topic=dl-delete-direct-link&interface=ui) and notify IBM by updating the ticket.

7.	The {{site.data.keyword.powerSys_notm}} team marks the workspace as **Migrated** and closes the ticket.

After the workspace is migrated to the PER network through the ticketing process, continue to refer to the support ticket for network configuration information, including subnet creation, deletion, and gateway updates. Before you delete the pre-migration workspace, open a support ticket to remove the backend device configuration. Then, you can delete the workspace.
{: important}

## Running a Full Linux Subscription (FLS) on the migrated workspace
{: #fls-migrated-sub}

You can run FLS with the migrated workspace in two ways:

1. FLS works if you update the migrated subnets with DNS IP addresses.

    Update the migrated subnet by adding DNS IP addresses, for example, `161.26.0.10` or `161.26.0.11`.

    Run the following command:

        ```bash
        ibmcloud pi netu <network_id> --dns-servers "127.0.0.1 161.26.0.10 161.26.0.11"
        ```
        {: .codeblock}

2. For existing virtual server instances that are deployed by using migrated subnets, add the following DNS IP addresses, or the specific DNS IP addresses for your environment, to the `/etc/resolv.conf` file:

    * `nameserver 161.26.0.10`
    * `nameserver 161.26.0.11`

## Additional information about PER migration
{: #add-info-per-mig}

If you need to make additional changes after the migration that require backend device configuration, complete the following actions:

- **Create a subnet:** In the {{site.data.keyword.powerSys_notm}} user interface, create the subnet, and then open a support ticket so that the {{site.data.keyword.powerSys_notm}} operations team can configure the subnet on the backend devices.

- **Update or delete a subnet:** First, open a support ticket so that the {{site.data.keyword.powerSys_notm}} operations team can update or remove the configuration on the backend devices. Then, update or delete the subnet in the {{site.data.keyword.powerSys_notm}} user interface.
