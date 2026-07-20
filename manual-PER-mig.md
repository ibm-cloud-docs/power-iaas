---

copyright:
  years: 2022, 2026 

lastupdated: "2026-07-20"

keywords: Power edge router migration, PER migration, migration, manual PER migration

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Migrating the existing network configurations to Power Edge Router
{: #migrate-ws-per}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---
Power Edge Router (PER) is enabled for all {{site.data.keyword.powerSys_notm}} data centers except `CHE01`. Two migration paths are available depending on how your workspace network was originally configured: self-service automation or a support ticket.
{: shortdesc}

## Before you begin
{: #per-mig-prereqs}

You must have access to Direct Link to complete your PER migration. For more information about required access roles, see [Access role requirements for Power Virtual Server](/docs/power-iaas?topic=power-iaas-managing-resources-and-users#access-roles-requirement).

- If you configured your workspace network without using a support ticket, use the [`ibmcloud pi workspace action`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1) CLI command to automate the migration. For more information, see [Migrating to PER](/docs/power-iaas?topic=power-iaas-per#migrate-per).

- If you manually configured your subnets and Direct Link through a support ticket, migrate your workspace to PER by opening a support ticket. See [Migrating to PER through a support ticket](#migrate-per-ticket).

## Determining your Direct Link configuration method
{: #determine-dl-config}

If you are unsure whether you manually configured subnets and Direct Link for your workspace, complete the following steps to verify your configuration method.

### Identifying automatically configured Cloud connections
{: #identify-cloud-connections}

To confirm that you have an automatically configured Cloud connection, check the following two conditions:

1. The connection appears on the **Cloud connections** page in the {{site.data.keyword.powerSys_notm}} workspace. To verify, complete the following steps:

   1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external}.

   2. In the search box, type **Power Virtual Server**, and click the **Power Virtual Server** tile.

   3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

   4. From the Workspaces page, select your workspace.

   5. Click **Cloud connections** in the left navigation panel. The Cloud connections page is displayed.

        If the **Cloud connections** option does not appear, your workspace is already PER-enabled, and this procedure does not apply to you. If your connections are listed here, continue to the next condition.

2. The Direct Link details page displays the message "This Direct Link is read-only". To verify, complete the following steps:

   1. Log in to the [IBM Cloud console](https://cloud.ibm.com){: external}.

   2. From the navigation menu, select **Infrastructure** > **Network** > **Direct link**. The Direct Link page is displayed.

   3. Click the Direct Link connection that has the same name as your Cloud connection.

   4. In the **Details** section, check for the read-only message.

If both conditions are met, your Direct Link connection was automatically configured through Cloud connections. Use the self-service automation to migrate to PER.

### Identifying manually configured Direct Link 2.0
{: #identify-manual-dl}

To confirm that you have a manually configured Direct Link 2.0, check the following conditions:

1. The connection does not appear on the **Cloud connections** page in the {{site.data.keyword.powerSys_notm}} workspace. To verify, complete the following steps:

   1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external}.

   2. In the search box, type **Power Virtual Server**, and click the **Power Virtual Server** tile.

   3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

   4. From the Workspaces page, select your workspace.

   5. Click **Cloud connections** in the left navigation panel. The Cloud connections page is displayed.

        If the **Cloud connections** option does not appear, your workspace is already PER-enabled. If no connections are listed or your Direct Link is not shown here, your Direct Link might be manually configured.

2. The Direct Link details page does not display the message "This Direct Link is read-only". To verify, complete the following steps:

   1. Log in to the [IBM Cloud console](https://cloud.ibm.com){: external}.

   2. From the navigation menu, select **Infrastructure** > **Network** > **Direct link**.

   3. Click the Direct Link connection.

   4. In the **Details** section, verify that the read-only message is not displayed.

If both conditions are met, your Direct Link connection was manually configured through a support ticket. In this case, you must also migrate to PER by opening a support ticket.



## Migrating to PER through a support ticket
{: #migrate-per-ticket}

To migrate your workspace to PER through a support ticket, complete the following steps:



1.	Create a [support case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} in the IBM Cloud Support Center.

2.	Select **{{site.data.keyword.powerSys_notm}}** under **Topic**, and select **Power VS Network Related** under **Subtopic**.

3.	In the **Subject** field, provide a brief description of your migration requirements.

4.	In the **Description** box under additional information, provide the following information:

    - The CRN (cloud resource name) of the workspace that you want to migrate

    - The subnet configuration details for the workspace

    - The Direct Link connection details associated with the workspace subnets

    The {{site.data.keyword.powerSys_notm}} operations team processes the support ticket by configuring PER and other network devices in parallel with the Direct Link configuration. When the PER configuration is complete, the team notifies you through a ticket update that the PER configuration is ready for your validation and testing.

5. Click **Next**.

6.	Schedule a maintenance window during which you must provision the Transit Gateway to complete the PER network configuration. For more information, see [PER use cases](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-use-cases). To route the network traffic through PER, complete the following steps:

    1.	In the [IBM Cloud console](https://cloud.ibm.com){: external}, from the navigation menu, select **Infrastructure** > **Network** > **Direct link**.

    2.	Click a Direct Link connection to open the connection details page.

    3.	Click the **BGP** tab and then open the **Route Filter** details.

    4.	Under **Import route filters** and **Export route filters**, select **Deny all import routes** to block the Direct Link routes and route traffic through the PER network.

    Repeat the preceding steps for each Direct Link connection.

7.	Verify that the network connection is working correctly, for example, by running a ping test.

    If you encounter any PER connectivity issues, revert to the Direct Link path by selecting **Permit all import routes** to unblock the Direct Link routes, and then disconnect the workspace from the Transit Gateway.

8.	After successful verification, follow the steps in [Deleting a Direct Link](/docs/dl?topic=dl-delete-direct-link&interface=ui) to remove the Direct Link connections, and then notify IBM by updating the ticket.

9.	The {{site.data.keyword.powerSys_notm}} team marks the workspace as **Migrated** and closes the ticket.

10.	Open a support ticket to remove the backend device configuration, and then delete the pre-migration workspace.

Before you delete the pre-migration workspace, you must open a support ticket to remove the backend device configuration first.
{: important}

After migration, if you need to make additional network configuration changes that require backend device configuration, complete the following actions:
{: #add-info-per-mig}

- **Create a subnet:** In the {{site.data.keyword.powerSys_notm}} user interface, create the subnet, and then open a support ticket so that the {{site.data.keyword.powerSys_notm}} operations team can configure the subnet on the backend devices.

- **Update or delete a subnet:** First, open a support ticket so that the {{site.data.keyword.powerSys_notm}} operations team can update or remove the configuration on the backend devices. Then, update or delete the subnet in the {{site.data.keyword.powerSys_notm}} user interface.

## Configuring FLS after migration
{: #fls-migrated-sub}

If you run Full Linux Subscription (FLS) on virtual server instances (VSIs) in the migrated workspace, you must update the DNS configuration after migration. FLS requires IBM DNS IP addresses to function correctly.

You can update the DNS configuration in two ways:

1. FLS works if you update the migrated subnets with DNS IP addresses.

    Update the migrated subnet by adding DNS IP addresses, for example, `161.26.0.10` or `161.26.0.11`.

    Run the following command:

        ```bash
        ibmcloud pi netu <network_id> --dns-servers "127.0.0.1 161.26.0.10 161.26.0.11"
        ```
        {: .codeblock}

    Where `127.0.0.1` refers to the local stub resolver on the VSI.

2. For existing VSIs that are deployed by using migrated subnets, add the following DNS IP addresses, or the specific DNS IP addresses for your environment, to the `/etc/resolv.conf` file:

    * `nameserver 161.26.0.10`
    * `nameserver 161.26.0.11`
