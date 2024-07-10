---

copyright:
  years: 2019, 2024

lastupdated: "2024-07-10"

keywords: direct link, order DL, ordering DL

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.dl_short}} Connect for {{site.data.keyword.powerSys_notm}}s
{: #ordering-direct-link-connect}




Use [{{site.data.keyword.cloud}} {{site.data.keyword.dl_short}} (2.0) Connect](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) to configure your private network with {{site.data.keyword.powerSysFull}}. The {{site.data.keyword.dl_short}} (2.0) Connect service creates a seamless connection that allows access to {{site.data.keyword.cloud_notm}} resources from your {{site.data.keyword.powerSys_notm}} instance.
{: shortdesc}

{{site.data.keyword.dl_short}} (2.0) Connect provides the following advantages:

- Support for connections to multiple {{site.data.keyword.cloud_notm}} accounts from a single direct link.
- Support for multiple VPCs (without classic access) from a single direct link within the same account.

## Before you begin
{: #before-you-begin-direct-link-connect}

Before you order {{site.data.keyword.dl_short}} Connect, make sure that you review the following considerations and satisfied the prerequisites:

* Verify that your {{site.data.keyword.cloud_notm}} account has the correct authorization to order the {{site.data.keyword.dl_short}} (2.0) Connect service.
* Review [{{site.data.keyword.dl_short}} prerequisites](/docs/dl?topic=dl-ibm-cloud-dl-prerequisites). Also, review [Routing considerations](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#routing-considerations), and [Setting up high availability](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#ha-availability), as needed for your particular deployment.
* {{site.data.keyword.cloud_notm}} highly recommends that you establish a second, diverse direct link to prevent outages, whether unplanned, or planned due to maintenance.
* A 10 Gbps connection is available only using the {{site.data.keyword.dl_short}} (2.0) Connect offering.
* {{site.data.keyword.dl_short}} (2.0) Connect is available in all current locations.
* Currently, there isn't a migration path from {{site.data.keyword.dl_short}} on Classic (1.0) to {{site.data.keyword.dl_short}} (2.0). You must order a new {{site.data.keyword.dl_short}} (2.0) Connect connection.

## Pricing
{: #direct-link-connect-pricing}

The {{site.data.keyword.powerSys_notm}} offering includes a highly available connection to {{site.data.keyword.cloud_notm}} services at no cost for each customer per data center. You can also select the global routing option for these direct links at no cost.

## Ordering {{site.data.keyword.dl_short}} (2.0) Connect
{: #order-direct-link-connect-2.0}

To order {{site.data.keyword.dl_short}} Connect, complete the following steps:

1. Follow {{site.data.keyword.dl_short}} Connect [ordering instructions](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-connect#instructions-connect) with these exceptions:

   * In the **Gateway** section, select the same location as the {{site.data.keyword.powerSys_notm}} instance. Each location requires its own direct link. For example, if you order a direct link for Frankfurt 04, you cannot establish a connection to the VMs in Frankfurt 05.

      For the list of {{site.data.keyword.dl_short}} Connect PowerVS locations, see [Providers and locations](/docs/dl?topic=dl-locations#connect-locations).
      {: important}

      * For **Routing**, select **Local** to access all of the data centers that are connected at the location that you specified. Select **Global** to access all of the {{site.data.keyword.cloud_notm}} data centers in the world.
      * For **Provider**, select **IBM POWER VS** from the list.
      * For **Speed**, select the link speed to meet your workload requirements. The recommended speed is 1 Gbps.
      * For the list of **Ports**, select a port that has the least number of connections. If you have multiple direct links, you must choose different ports for each connection.

   * In the **Billing** section, select **Unmetered**.
   * In the **BGP** section:

      *  For **BGP peering subnet**, you can select **Auto-select IP** to auto-select an IP address from range `169.254.0.0/16`, or manually enter addresses in a specific range to avoid conflict with an existing connection.
      * For **BGP ASN**, enter `64999` as the BGP ASN number for the {{site.data.keyword.dl_short}} Connect location unless a different ASN number is required as indicated on the provisioning page. For example, the BGP ASN number for the WDC04 location is `64995`. For 10 Gbps ports that are not GRE capable, you must use the BGP ASN number `64997`.
      * Do not try to change the BGP ASN number to **64995**. You must contact the IBM Power support team to handle your request to change the BGP ASN number.

      | Direct Link Connect site | BGP ASN |
      | ---------------------------- | -------------- |
      | Dallas 10 \n Dallas 12 \n Dallas 13 | 4206000072 \n 64999 \n 64999 |
      | Washington 4 | 64995 |
      | Washington 6 | 64999 |
      | Washington 7 | 4206000068 |
      | Frankfurt 4 \n Frankfurt 5 | 64999 |
      | London 6 | 64999 |
      | Toronto 1 | 64999 |
      | Montreal 1 | 64999 |
      | São Paulo 4 | 4206000076 |
      | Chennai 01  | 4206000092 |
      {: caption="Table 1. BGP ASN number for specific Connect sites" caption-side="bottom"}

2. Read and agree to the [{{site.data.keyword.dl_short}} prerequisites](/docs/dl?topic=dl-ibm-cloud-dl-prerequisites), then click **Create**.

   After your {{site.data.keyword.dl_short}} connection order is submitted, go to **Interconnectivity** > **{{site.data.keyword.dl_short}}** to view the status of your order. The **Direct Link** page lists all existing {{site.data.keyword.dl_short}} connections.

3. To [complete your connection](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-connect#complete-connection-connect), submit an [IBM Support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support) to the {{site.data.keyword.powerSys_notm}} team. In the description field, enter the following details.

    ```text
    Customer name:
    Customer account ID:
    Data center details:
    Direct Link Connect subnet:
    IBM Cloud IP address:
     Power Virtual Server network IP address:
    Direct Link Connect VLAN:
    IBM Cloud ASN:
     Power Virtual Server network ASN:
     Power Virtual Server Private Network (subnet) Name (1):
     Power Virtual Server Private Network (subnet) Name (2):
     Power Virtual Server Private Network (subnet) Name (3):
    Direct Link Connect 2.0 Virtual Connections:
    Classic Network Virtual Connection: Yes/No
    VPC Virtual Connection 1: VPC name and ID
    VPC Virtual Connection 2: VPC name and ID
    VPC Virtual Connection 3: VPC name and ID
    ```

    The **{{site.data.keyword.powerSys_notm}} network** autonomous system number (ASN) is the same as your Border Gateway Protocol (BGP) ASN. The {{site.data.keyword.cloud_notm}} network team generates the **{{site.data.keyword.cloud_notm}} ASN** and adds it to the {{site.data.keyword.cloud_notm}} support case. The {{site.data.keyword.cloud_notm}} network team also generates the IP addresses. Your private network name is your {{site.data.keyword.powerSys_notm}} private network subnet name.
    {: important}

    The {{site.data.keyword.powerSys_notm}} support case is closed when the {{site.data.keyword.dl_short}} Connect connection is configured to communicate with your {{site.data.keyword.powerSys_notm}} instance.

## Setting up high availability over {{site.data.keyword.dl_short}} Connect
{: #ha-availability}

Your {{site.data.keyword.dl_short}} connections are location-specific. By default, {{site.data.keyword.cloud_notm}} {{site.data.keyword.dl_short}} is not a redundant service. You must order a separate {{site.data.keyword.dl_short}} Connect instance for redundancy.
{: shortdesc}

To set up a high availability through {{site.data.keyword.dl_short}} Connect, complete the following steps:

1. Order two instances of {{site.data.keyword.dl_short}} Connect. For instructions, see [Ordering {{site.data.keyword.dl_short}} Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0).

   In the **BGP** section, select a port from a separate port group for the redundant {{site.data.keyword.dl_short}} Connect instance. Both {{site.data.keyword.dl_short}} Connect instances must be on separate ports to connect to different {{site.data.keyword.powerSys_notm}} routers, thus, ensuring redundancy.

    The following example shows the {{site.data.keyword.dl_short}} Connect ports for the DAL12 data center. The ports that end with `1-1` and `1-2` belong to one port group, and the ports ending with `2-1` and `2-2` belong to another port group. If you select a port from the first port group, you must select a port from the second port group for the redundant {{site.data.keyword.dl_short}} Connect instance. That is, if you select **-1-1** for the first {{site.data.keyword.dl_short}} Connect instance, you must select **-2-1** or **-2-2** for the second Direct Link Connect instance.

    ![BGP and connections](images/bgp-connections.png){: caption="Figure 1. BGP and connections" caption-side="bottom"}

    Border Gateway Protocol (BGP) sessions are configured for the {{site.data.keyword.dl_short}} Connect service in such a way that when a fault is detected on a {{site.data.keyword.dl_short}} Connect instance, the BGP routes traffic to an alternative {{site.data.keyword.dl_short}} Connect instance. For 10 Gbps connections, use the new ports that are not GRE capable. Ports that are GRE capable can use only up to a 5 Gbps speed.

    Refer to the following table to identify the ports and port groups that you must select for the redundant {{site.data.keyword.dl_short}} Connect instance:

    | Data center | Network provider | Port group 1 | Port group 2 for redundancy |
    | ----------- | ---------------- | ------------ | --------------------------- |
    | LON04 | IBM Power VS | IBM POWER VS-CLOUD EXCHANGE SL-LON04-1-1 \n IBM POWER VS-CLOUD EXCHANGE SL-LON04-1-2 | IBM POWER VS-CLOUD EXCHANGE SL-LON04-2-1 \n IBM POWER VS-CLOUD EXCHANGE SL-LON04-2-2 |
    | LON06 | IBM Power VS | SL-LON06-IBMPOWERLAASLITE-1-1 \n SL-LON06-IBMPOWERLAASLITE-1-2 \n xPowerVS-LON04-10G-NOGRE-1-1[^footnote1] | SL-LON06-IBMPOWERLAASLITE-2-1 \n SL-LON06-IBMPOWERLAASLITE-2-2 \n xPowerVS-LON04-10G-NOGRE-1-2[^footnote2] |
    | FRA05 | IBM Power VS | SL-FRA05-IBMPOWERLAASLITE-1-1 \n SL-FRA05-IBMPOWERLAASLITE-1-2 \n xPowerVS-FRA05-10G-NOGRE-1-1[^footnote3] | SL-FRA05-IBMPOWERLAASLITE-2-1 \n SL-FRA05-IBMPOWERLAASLITE-2-2 \n xPowerVS-FRA05-10G-NOGRE-1-2[^footnote4] |
    | FRA04 | IBM Power VS | SL-FRA04-IBMPOWERLAASLITE-1-1 \n SL-FRA04-IBMPOWERLAASLITE-1-2 \n xPowerVS-FRA04-10G-NOGRE-1-1[^footnote5] | SL-FRA04-IBMPOWERLAASLITE-2-1 \n SL-FRA04-IBMPOWERLAASLITE-2-2 \n xPowerVS-FRA04-10G-NOGRE-1-2[^footnote6] |
    | WDC04 | IBM Power VS | NNI-LINK-SL-WDC04-IBMPOWERLAASLITE-1-2 \n xPowerVS-WDC04-10G-NOGRE-1-1[^footnote7] | NNI-LINK-SL-WDC04-IBMPOWERLAASLITE-2-2 \n xPowerVS-WDC04-10G-NOGRE-1-2[^footnote8] |
    | WDC06 | IBM Power VS | IBM POWER VS-CLOUD EXCHANGE SL-WDC06-1-1 \n IBM POWER VS-CLOUD EXCHANGE SL-WDC06-1-2 | IBM POWER VS-CLOUD EXCHANGE SL-WDC06-2-1 \n IBM POWER VS-CLOUD EXCHANGE SL-WDC06-2-2 |
    | WDC07 | IBM Power VS | SL-WDC07-IBMPOWERLAASLITE-1-1 \n SL-WDC07-IBMPOWERLAASLITE-1-2 | SL-WDC07-IBMPOWERLAASLITE-2-1 \n SL-WDC07-IBMPOWERLAASLITE-2-2 |
    | DAL10 | IBM Power VS | SL-DAL10-IBMPOWERLAASLITE-1-1 \n SL-DAL10-IBMPOWERLAASLITE-1-2 | SL-DAL10-IBMPOWERLAASLITE-2-1 \n SL-DAL10-IBMPOWERLAASLITE-2-2 |
    | DAL12 | IBM Power VS | IBM POWER VS-CLOUD EXCHANGE SL-DAL12-1-1 \n IBM POWER VS-CLOUD EXCHANGE SL-DAL12-1-2 \n xPowerVS-DAL12-10G-NOGRE-1-1[^footnote9] | IBM POWER VS-CLOUD EXCHANGE SL-DAL12-2-1 \n IBM POWER VS-CLOUD EXCHANGE SL-DAL12-2-2 \n xPowerVS-DAL12-10G-NOGRE-1-2[^footnote10] |
    | DAL13 | IBM Power VS | SOFTLAYER-IBMPOWERIAASLITE-1-1 \n SOFTLAYER-IBMPOWERIAASLITE-1-2 \n xPowerVS-DAL13-10G-NOGRE-1-1[^footnote11] | SOFTLAYER-IBMPOWERIAASLITE-2-1 \n SOFTLAYER-IBMPOWERIAASLITE-2-2 \n xPowerVS-DAL13-10G-NOGRE-1-2[^footnote12] |
    | SYD04 | IBM Power VS | SL-SYD04-IBMPOWERLAASLITE-1-1 \n SL-SYD04-IBMPOWERLAASLITE-1-2 \n xPowerVS-SYD04-10G-NOGRE-1-1[^footnote13] | SL-SYD04-IBMPOWERLAASLITE-2-1 \n SL-SYD04-IBMPOWERLAASLITE-2-2 \n xPowerVS-SYD04-10G-NOGRE-1-2[^footnote14] |
    | TOK04 | IBM Power VS | SL-TOK01-ZENLAYER-3-1 \n 01675-TK4-X-I-0002 \n TKY/TKY/LE-275454 | SL-TOK01-ZENLAYER-4-1|
    | OSA21 | IBM Power VS | SL-OSA01-ATTOKYO-1-1 | SL-OSA01-ATTOKYO-2-1 |
    | SAO04 | IBM Power VS | SL-SAO04-POWERVSCX-1-1 \n SL-SAO04-POWERVSCX-1-2 | SL-SAO04-POWERVSCX-2-1 \n SL-SAO04-POWERVSCX-2-2 |
    | CHE01 | IBM Power VS | IBM-CHE01-POWERCX-1-1 \n IBM-CHE01-POWERCX-1-2 | IBM-CHE01-POWERCX-2-1 \n IBM-CHE01-POWERCX-2-2 |
    {: caption="Table 2. Port and Port groups for redundant {{site.data.keyword.dl_short}} instances" caption-side="bottom"}

    [^footnote1]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote2]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote3]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote4]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote5]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote6]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote7]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote8]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote9]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote10]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote11]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote12]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote13]: This port is not GRE capable, but supports a speed of 10 Gbps.
    [^footnote14]: This port is not GRE capable, but supports a speed of 10 Gbps.

2. Select the remaining options and create the {{site.data.keyword.dl_short}} Connect instance as described in [Ordering {{site.data.keyword.dl_short}} (2.0) Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0).

## Routing considerations for VPC
{: #routing-considerations}

If traffic is sent from the {{site.data.keyword.powerSys_notm}} to your private cloud public IP address, and if the virtual server instance has a public floating IP, you might need a special configuration in the VPC. Otherwise, the traffic goes through the virtual machine's public interface instead of a private interface.
{: shortdesc}

For proper VPC configuration, the private cloud IP address must meet the following requirements:

- The IP address range for a private network must be within the following blocks, which are reserved by the Internet Assigned Numbers Authority (IANA):
    - Class A — `10.0.0.0` — `10.255.255.255` (16,777,216 total hosts)
    - Class B — `172.16.0.0` — `172.31.255.255` (1,048,576 total hosts)
    - Class C — `192.168.0.0` — `192.168.255.255` (65,536 total hosts)
- VM instances within the VPC must not have a floating IP.
- Use the **Delegate-VPC** action to create a route to the private cloud public subnet in the VPC default routing table.

For more information, see [Routing considerations for IANA-registered IP assignments](/docs/vpc?topic=vpc-interconnectivity#routing-considerations-iana).
