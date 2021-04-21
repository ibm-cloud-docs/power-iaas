---

copyright:
<<<<<<< HEAD
  years: 2019, 2020, 2021

lastupdated: "2021-02-25"
=======
  years: 2019, 2021

lastupdated: "2021-04-21"
>>>>>>> draft

keywords: ordering direct link, dirct link location, bgp asn, iam service id, delete direct link, high availability

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Direct Link Connect for Power Systems Virtual Servers
{: #ordering-direct-link-connect}

Direct Link Connect is a separate service from the Power Systems Virtual Server. You must use [Direct Link](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link) to configure your private network with IBM&reg; Power Systems&trade; Virtual Server. The Direct Link Connect 2.0 service creates a seamless connection that allows access to {{site.data.keyword.cloud}} resources from your {{site.data.keyword.powerSys_notm}} instance.
{: shortdesc}

The Direct Link Connect (2.0) provides the following advantages:

- Support for connections to multiple IBM Cloud accounts from a single direct link.
- Support for multiple VPCs (without classic access) from a single direct link within the same account.
- Automated Direct Link 2.0 Configuration in IBM Cloud Classic and VPC.

The Power Systems Virtual Server offering includes a highly available up to 10 Gbps connection to IBM Cloud services at no cost for each customer per data center. If desired, you can select the global routing option for these links at no cost. Over the next few months, the {{site.data.keyword.powerSys_notm}} service plans to continue to evolve its network connectivity capabilities through further automation and integration.

10Gbps connection is available only on the Direct Link Connect 2.0
{: important}

Direcet Link Connect 2.0 is available in all current locations except Toronto 1, Montreal 1, and São Paulo 1. For these locations, you must use [IBM Cloud Direct Link on Classic](/docs/direct-link?topic=direct-link-about-ibm-cloud-direct-link){: new_window}{: external}. Moreover, if you are using Direct Link Connect on Classic in any current location, you can continue to use it with Power Systems Virtual Server. If you want to use Direct Link Connect 2.0, you must order a new Direct Link Connect 2.0 connection.
{: note}

For more information on Direct Link Connect, see [Pricing for IBM Cloud Direct Link](/docs/dl?topic=dl-pricing-for-ibm-cloud-dl) and [IBM Cloud Direct Link Connect on Classic](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-connect).

## Ordering Direct Link Connect 2.0
{: #order-direct-link-connect-2.0}
{: #help}
{: support}

To order the Direct Link Connect 2.0 service that creates a connection to the Power Systems Virtual Server instance, complete the following steps:

Order a second Direct Link Connect connection for backup purposes.
{: tip}

1. Verify that your IBM Cloud account has the correct authorizations to order the Direct Link 2.0 Connect service.

2. Review the following basic Direct Link Connect networking concepts:

   - [Direct Link Connect concepts](/docs/dl?topic=dl-dl-about)
   - [Direct link prerequisites](/docs/dl?topic=dl-ibm-cloud-dl-prerequisites)

3. Log in to your [IBM Cloud](https://cloud.ibm.com/login){: new_window}{: external} account. 

4. Click ![Menu icon](../power-iaas/images/menu.svg "menu icon") icon on the upper left, then click **Interconnectivity**.

5. Click **Order Direct Link** and select the **Direct Link Connect** option.

6. Enter the [configuration parameters](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#direct-link) for your IBM Cloud Direct Link Connect order. As you complete the fields for creating the Direct Link Connect service, the price is automatically updated to reflect your selections.

   The {{site.data.keyword.powerSys_notm}} service offers lower latency direct connectivity to customers. You must select **IBM POWER VIRTUAL SERVER** as the **Network Provider** instead of **MEGAPORT**.
   {: note}

7. Read the *Master Service Agreement* and select the checkbox. You must read and understand the Master Service Agreement as it contains important technical information.

8. Click **Create**. It can take up to several minutes to provision your Direct Link connection request.

9. After your Direct Link connection request is provisioned, go to **Interconnectivity** > **Direct Link**. The **Direct Link** page lists all the existing Direct Link connections.

10. Click the newly provisioned Direct Link connection to identify the following details:

    ![Direct Link Connect 2.0 details](images/dl2-status.png "Direct Link Connect 2.0 details"){: caption="Figure 1. Direct Link Connect 2.0 details" caption-side="bottom"}

11. Create a [new support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support) against the {{site.data.keyword.powerSys_notm}} team. In the new case's description field, enter the following details.

    ```
    Customer name:
    Customer account ID:
    Data center details:
    Direct Link Connect subnet:
    IBM Cloud IP address:
    Power Systems Virtual Server network IP address:
    Direct Link Connect VLAN:
    IBM Cloud ASN:
    Power Systems Virtual Server network ASN:
    Power Systems Virtual Server Private Network (subnet) Name (1):
    Power Systems Virtual Server Private Network (subnet) Name (2):
    Power Systems Virtual Server Private Network (subnet) Name (3):
    Direct Link Connect 2.0 Virtual Connections:
    Classic Network Virtual Connection: Yes/No
    VPC Virtual Connection 1: VPC name and ID
    VPC Virtual Connection 2: VPC name and ID
    VPC Virtual Connection 3: VPC name and ID
    Screen shot of Direct Link 2.0 Connect
    ```

    The **{{site.data.keyword.powerSys_notm}} network** autonomous system number (ASN) is the same as your Border Gateway Protocol (BGP) ASN. The IBM Cloud network team generates the **IBM Cloud ASN** and adds it to the IBM Cloud support ticket. The IBM Cloud network team also generates the IP addresses. Your private network name is your Power Systems Virtual Server private network subnet name.
    {: note}

12. The {{site.data.keyword.powerSys_notm}} support case is closed when the Direct Link Connect connection is configured to communicate with your Power Systems Virtual Server instance.

### Configuration parameters for ordering Direct Link Connect

{: configuration-parameters}

#### Configuration

- **Direct Link Name** - Enter a name for your Direct Link Connect instance.
- **Resource group** - Select the default group.
- **Billing** - Select the Unmetered option.
- **Location** - Select the same location as the {{site.data.keyword.powerSys_notm}} instance. The following table identifies the {{site.data.keyword.powerSys_notm}} instance location and the corresponding Direct Link Connection option:

<table>
      <caption>
        Table 1. Direct Link Connection location options
      </caption>
      <tr>
        <th>Power Systems Virtual Server location</th>
        <th>Direct Link Connect location</th>
        <th>Network provider</th>
      </tr>
      <tr>
        <td>Dallas 13, TX, US</td>
        <td>Dallas 13</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Dallas 12, TX, US</td>
        <td>Dallas 12</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Washington 04, D.C., US</td>
        <td>Washington DC 4</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Frankfurt 04, Germany</td>
        <td>Frankfurt 4</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Frankfurt 05, Germany</td>
        <td>Frankfurt 5</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>London 04, United Kingdom</td>
        <td>London 4</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>London 06, United Kingdom</td>
        <td>London 6</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Sydney 04, Australia</td>
        <td>Sydney 4</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Tokyo 04, Japan</td>
        <td>Tokyo 4</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Osaka 21, Japan</td>
        <td>Osaka 21</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      </table>

  Direct Link 2.0 is available in all current locations except Toronto 1, Montreal 01, and São Paulo 1.</br>
  Each location requires its own Direct Link Connect. For example, if you order a Direct Link for Frankfurt 04, you can not establish connection to the VMs in Frankfurt 05.
  {: note}

- **Routing Option** - Select <strong>Local Routing (Free)</strong> to access all the data centers that are connected at the location that you specified in the <strong>Location</strong> field. Select <strong>Global Routing</strong> to access all the IBM Cloud data centers in the world.
- **Network Provider** - You must select <strong>IBM POWER VIRTUAL SERVER</strong> from the list.
- **Speed** - Select the link speed to meet your workload requirements. The recommended selection for the <strong>Speed</strong> field is 1 Gbps.

#### BGP and connections

- **Ports** - If you have multiple Direct Link connections, you must choose different ports for each connection. Otherwise, you can choose a port that has the least number of connections.
- **BGP peering subnet** - Select **Auto-select IP** for Power Systems Virtual Server to auto-select an IP address from range *169.254.0.0/16*, or manually enter addresses in a specific range to avoid conflict with an existing connection.
- **BGP ASN** - You must enter 64999 as BGP ASN number for Direct Link Connect location unless a different ASN number is required as indicated in the table 3. For example, BGP ASN number for WDC04 location is 64995.

  <!--Do not try to change the BGP ASN number to <strong>64995</strong>. You must contact the IBM Power support team to handle your request to change the BGP ASN number.
  {: important}-->

#### Add connection

Select [Classic or VPC](/docs/cloud-infrastructure?topic=cloud-infrastructure-compare-infrastructure) depending on the type of network reach you want and depending on how you want Direct Link to connect to the IBM Cloud resources. You can create multiple network connections for a Direct Link Connect instance.

Although adding a connection is optional when you are ordering Direct Link Connect, you must add at least one connection later to successfully connect the {{site.data.keyword.powerSys_notm}} instance to the IBM Cloud network. 

Power Systems Virtual Servers Direct Link 2.0 service provides connectivity to IBM Cloud Classic network in addition to VPC network. You can access all of the Classic network locations irrespective of Direct Link 2.0 gateway in local or global routing attribute. You must use the global routing attribute to reach VPC network outside the local region.

## Ordering Direct Link Connect on Classic

{: #steps-to-order-direct-link-connect}

To order the Direct Link Connect on Classic service that creates a connection to the {{site.data.keyword.powerSys_notm}} instance, complete the following steps:

Order a second Direct Link Connect connection for backup purposes.
{: tip}

1. Verify that your {{site.data.keyword.cloud_notm}} account has the correct authorizations to order the Direct Link Connect service.

2. Review the following basic Direct Link Connect networking concepts:

   - [Direct Link Connect on Classic concepts](/docs/direct-link?topic=direct-link-about-ibm-cloud-direct-link)
   - [Direct Link Connect on Classic details](/docs/direct-link?topic=direct-link-about-ibm-cloud-direct-link#direct-link-connect-solution)
   - [Direct Link Connect on Classic limitations](/docs/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
   - [Strict limitations on IP assignments](/docs/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

3. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: new_window}{: external} with your IBM Cloud account credentials.

4. Search for **Direct Link Connect on Classic**.

5. Click **Order Direct Link Connect on Classic** to see the order form.

6. Enter the <a href="#direct-link">configuration parameters</a> for your IBM Cloud Direct Link Connect on Classic order. As you complete the fields for creating the Direct Link Connect service, the price is automatically updated to reflect your selections.

   The {{site.data.keyword.powerSysShort}} service offers lower latency direct connectivity to customers. You must select **IBM POWER VIRTUAL SERVER** as the **Network Provider** instead of **MEGAPORT** to take advantage of this offer.
   {: note}

7. Read the *Master Service Agreement* and select the checkbox. You must read and understand the _Master Service Agreement_ as it contains important technical information.

8. Click **Create**. The following message is displayed when your request is submitted successfully:

   ![Direct Link Connect success message and ticket number](./images/console-direct-link-message.png "Direct Link Connect success message and ticket number"){: caption="Figure 1. Direct Link Connect success message and ticket number" caption-side="bottom"}

9. Click the **Case number** link for the Direct Link Connect service. The information in the case number is used to identify the Direct Link Connect information for connecting your {{site.data.keyword.powerSys_notm}} instance.

   It can take up to three business days to complete the initial setup for the Direct Link connection request.
   {: note}

10. To create a connection to the {{site.data.keyword.powerSys_notm}} instance by using the Direct Link Connect service, create a [new support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support) against the {{site.data.keyword.powerSys_notm}} team. In the new case's description field, add the **Direct Link Connect case number**.

11. When the Direct Link Connect connection is established, the Direct Link Connect case is closed. The following network information is an example of what is displayed:

    ```
    Link Speed:                  1000 Mbps
    Location:                    Washington 4
    Network Provider:            IBM Power Virtual Server
    Direct Link Connect subnet:  10.254.0.24/30
    IBM Cloud IP Address:        10.254.0.25/30
    Customer IP Address:         10.254.0.26/30
    IBM Cloud ASN:               13884
    Customer BGP ASN:            64995
    Network Identifier:          1748523-1
    Date Created:                2019-06-12T14:56:45-06:00
    ```
    {: screen}

12. Use the information from the Direct Link Connect case number to update the **{{site.data.keyword.powerSys_notm}} support case**:

    The **Power Systems Virtual Server network ASN** is the same as your **BGP ASN**. The IBM Cloud network team generates the **IBM Cloud ASN** and adds it to the IBM Cloud support ticket. The IBM Cloud network team also generates the IP addresses. Your private network name is your [Power Systems Virtual Server private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet) name.
    {: note}

    ```
    Customer name:
    Customer account ID:
    Direct Link Connect subnet:
    IBM Cloud IP address:
    Power Systems Virtual Server network IP address:
    IBM Cloud ASN:
    Power Systems Virtual Server network ASN:
    Power Systems Virtual Server Private Network (subnet) Name (1):
    Power Systems Virtual Server Private Network (subnet) Name (2):
    Power Systems Virtual Server Private Network (subnet) Name (3):
    ```
    {: codeblock}

13. The {{site.data.keyword.powerSys_notm}} support case is closed when the Direct Link Connect connection is configured to communicate with your {{site.data.keyword.powerSys_notm}} instance.

<dl id="direct-link">
  <dt><strong>Direct Link Instance Name</strong></dt>
  <dd>Enter a name for your Direct Link Connect instance.</dd>
  <dt><strong>Location</strong></dt>
  <dd>Select the same location as the {{site.data.keyword.powerSys_notm}}instance. Each location requires its own Direct Link Connect. For example, if you order a Direct Link for Frankfurt 04, you can not establish connection to the VMs in Frankfurt 05. </br>
  The following table identifies the {{site.data.keyword.powerSys_notm}} instance location and the corresponding Direct Link Connection option:
    <table>
      <caption>
        Table 2. Direct Link Connection location options
      </caption>
      <tr>
        <th>Power Systems Virtual Server location</th>
        <th>Direct Link Connect location</th>
        <th>Network provider</th>
      </tr>
      <tr>
        <td>Dallas, TX, US</td>
        <td>Dallas 12<br />Dallas 13</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Washington, D.C., US</td>
        <td>Washington 4</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Frankfurt, Germany, EU</td>
        <td>Frankfurt 4<br />Frankfurt 5</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>London, United Kingdom</td>
        <td>London 4<br />London 6</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Toronto, Canada</td>
        <td>Toronto 1</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Montreal, Canada</td>
        <td>Montreal 1</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Sydney, Australia</td>
        <td>Sydney 4</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>São Paulo, Brazil</td>
        <td>São Paulo 1</td>
        <td>IBM Power Virtual Server</td>
      </tr>
    </table>
  </dd>
  <dt><strong>Network Provider</strong></dt>
  <dd>
    You must select <strong>IBM POWER VIRTUAL SERVER</strong> from the list.
  </dd>
  <dt><strong>Link Speed</strong></dt>
  <dd>
    Select the link speed to meet your workload requirements. The recommended
    selection for the <strong>Link Speed</strong> field is 1000 Mbps.
  </dd>
  <dt><strong>Routing Option</strong></dt>
  <dd>
    Select <strong>Local Routing (Free)</strong> to access all of the data centers that
    are connected at the location that you specified in the
    <strong>Location</strong> field. Select <strong>Global Routing</strong> to
    access all of the IBM Cloud data centers in the world.
  </dd>
  <dt><strong>BGP ASN</strong></dt>
  <dd>
    <p>
      You must enter the BGP ASN number for the specific Direct Link Connect
      location.
    </p>
    <p>
      <strong>Important:</strong> Do not try to change the BGP ASN number to
      <strong>64995</strong>. You must contact the IBM Power support team to
      handle your request to change the BGP ASN number.
    </p>
    <table>
      <caption>
        Table 3. BGP ASN number for specific locations
      </caption>
      <tr>
        <th>Direct Link Connect location</th>
        <th>BGP ASN number</th>
      <tr>
        <td>Dallas 12<br />Dallas 13</td>
        <td>64999</td>
      </tr>
      <tr>
        <td>Washington 4</td>
        <td>64995</td>
      </tr>
      <tr>
        <td>Frankfurt 4<br />Frankfurt 5</td>
        <td>64999</td>
      </tr>
      <tr>
        <td>London 6</td>
        <td>64999</td>
      </tr>
      <tr>
        <td>Toronto 1</td>
        <td>64999</td>
      </tr>
      <tr>
        <td>Montreal 1</td>
        <td>64999</td>
      </tr>
    </table>
  </dd>
  <dt><strong>Select VRF</strong></dt>
  <dd>
    Select the virtual routing and forwarding option for the connection. If your
    account does not have a VRF identified, this field is not displayed. You can
    still create the Direct Link Connect service without selecting a VRF.
  </dd>

</dl>

## Deleting your Direct Link Connect on Classic connection

{: deleting-direct-link}

You can remove your Direct Link Connect on Classic connection by [opening a support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support) against the Power Systems Virtual Server support team to remove the appropriate resources.

## Setting up high availability over Direct Link Connect

{: ha-availability}

Your Direct Link connections are location-specific. IBM Cloud Direct Link is not a redundant service by default.  You must order a separate Direct Link Connect instance for redundancy.

To set up a highly available connectivity on the IBM Cloud network by using Direct Link Connect, complete the following steps:

1. Order two instances of Direct Link Connect (2.0) or Direct Link Connect on Classic. For each instance of Direct Link Connect, you can order an additional instance for redundancy. For instructions, see [Ordering Direct Link Connect 2.0](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#help) or [Ordering Direct Link Connect on Classic](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#ordering-direct-link-connect-on-classic).

2. In the **BGP and connections** configuration panel, select a port from a separate port group for the redundant Direct Link Connect instance than the existing instance. Both Direct Link Connect instances must be on separate ports to connect to different Power Systems Virtual Server routers, thus, ensuring redundancy.

  The following example shows the Direct Link Connect ports for the DAL12 data center. The ports ending with 1-1 and 1-2 belong to a port group, and the ports ending with 2-1 and 2-2 belong to another port group. For a Direct Link Connect instance, if you have selected a port from the first port group, you must select a port from the other port group for the redundant Direct Link Connect instance. That is, if you had selected <portname>-1-1 for the first Direct Link Connect instance, you must select <portname>-2-1 or <portname>-2-2 for the second Direct Link Connect instance that you want to use to set up redundancy.

  ![BGP and connections](images/bgp-connections.png){: Caption="Figure 1. BGP and connections" caption-side="bottom"}

  For Direct Link Connect on Classic, you can select the port only when you order a second Direct Link Connect instance for redundancy.
{: note}

  Border Gateway Protocol (BGP) sessions are configured for the Direct Link Connect service in such a way that when a fault is detected on a Direct Link Connect instance, the BGP routes traffic to an alternate Direct Link Connect instance. Refer to the following table to identify the ports and port groups that you must select for the redundant Direct Link Connect instance:

    <table>
      <caption>
        Table 1. Port and Port groups for redundant Direct Link instances
      </caption>
      <tr>
        <th>Data Center</th>
        <th>Network Provider</th>
        <th>Port group 1</th>
        <th>Port group 2 for redundancy</th>
      <tr>
        <td>LON04</td>
        <td>IBM Power VS</td>
        <td>IBM POWER VS-CLOUD EXCHANGE SL-LON04-1-1<br />IBM POWER VS-CLOUD EXCHANGE SL-LON04-1-2</td>
        <td>IBM POWER VS-CLOUD EXCHANGE SL-LON04-2-1<br />IBM POWER VS-CLOUD EXCHANGE SL-LON04-2-2</td>
      </tr>
      <tr>
        <td>LON06</td>
        <td>IBM Power VS</td>
        <td>SL-LON06-IBMPOWERLAASLITE-1-1<br />SL-LON06-IBMPOWERLAASLITE-1-2</td>
        <td>SL-LON06-IBMPOWERLAASLITE-2-1<br />SL-LON06-IBMPOWERLAASLITE-2-2</td>
      </tr>
      <tr>
        <td>FRA05</td>
        <td>IBM Power VS</td>
        <td>SL-FRA05-IBM-PowerIaaSLite-1-1<br />SL-FRA05-IBM-PowerIaaSLite-1-2</td>
        <td>SL-FRA05-IBM-PowerIaaSLite-2-1<br />SL-FRA05-IBM-PowerIaaSLite-2-2</td>
      </tr>
      <tr>
        <td>FRA04</td>
        <td>IBM Power VS</td>
        <td>SL-FRA04-IBMPOWERLAASLITE-1-1<br />SL-FRA04-IBMPOWERLAASLITE-1-2</td>
        <td>SL-FRA04-IBMPOWERLAASLITE-2-1<br />SL-FRA04-IBMPOWERLAASLITE-2-2</td>
      </tr>
      <tr>
        <td>WDC04</td>
        <td>IBM Power VS</td>
        <td>NNI-LINK-SL-WDC04-IBMPOWERLAASLITE-1-2</td>
        <td>NNI-LINK-SL-WDC04-IBMPOWERLAASLITE-2-2</td>
      </tr>
      <tr>
        <td>DAL12</td>
        <td>IBM Power VS</td>
        <td>IBM POWER VS-CLOUD EXCHANGE SL-DAL12-1-1<br />IBM POWER VS-CLOUD EXCHANGE SL-DAL12-1-2</td>
        <td>IBM POWER VS-CLOUD EXCHANGE SL-DAL12-2-1<br />IBM POWER VS-CLOUD EXCHANGE SL-DAL12-2-2</td>
      </tr>
      <tr>
        <td>DAL13</td>
        <td>IBM Power VS</td>
        <td>SOFTLAYER-IBMPOWERIAASLITE-1-1<br />SOFTLAYER-IBMPOWERIAASLITE-1-2</td>
        <td>SOFTLAYER-IBMPOWERIAASLITE-2-1<br />SOFTLAYER-IBMPOWERIAASLITE-2-2</td>
      </tr>
      <tr>
        <td>SYD05</td>
        <td>IBM Power VS</td>
        <td>SL-SYD05-IBMPOWERIAASLITE-1- 1<br />SL-SYD05-IBMPOWERIAASLITE-1- 2</td>
        <td>SL-SYD05-IBMPOWERIAASLITE-2-1<br />SL-SYD05-IBMPOWERIAASLITE-2-2<t/d>
      </tr>
      <tr>
        <td>SYD04</td>
        <td>IBM Power VS</td>
        <td>SL-SYD04-IBMPOWERIAASLITE-1-1<br />SL-SYD04-IBMPOWERIAASLITE-1-2</td>
        <td>SL-SYD04-IBMPOWERIAASLITE-2-1<br />SL-SYD04-IBMPOWERIAASLITE-2-2</td>
      </tr>
      <tr>
        <td>TOK04</td>
        <td>IBM Power VS</td>
        <td>SL-TOK04-POWERIAASLITE-1-1-(ASR1)<br />SL-TOK04-POWERIAASLITE-1-2-(ASR1)</td>
        <td>SL-TOK04-POWERIAASLITE-2-1<br />SL-TOK04-POWERIAASLITE-2-2</td>
      </tr>
    </table>

3. Select the remaining options and create the Direct Link Connect instance as described in [Ordering Direct Link Connect 2.0](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#help) or [Ordering Direct Link Connect on Classic](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#ordering-direct-link-connect-on-classic) (Step 8 onwards).

## Routing considerations for VPC
{: routing-considerations}

If the traffic from Power Systems Virtual Server to your on-premise public IP address and if the virtual server instance has public floating IP, you might need a special configuration in VPC. Otherwise, the traffic goes through the virtual machine's public interface instead of private interface.

For proper VPC configuration, the on-premise IP address must meet the following requirements:

- The IP address range for private network must be with in the following blocks that are reserved by Internet Assigned Numbers Authority (IANA):
  - Class A — 10.0.0.0 — 10.255.255.255 (16,777,216 total hosts)
  - Class B — 172.16.0.0 — 172.31.255.255 (1,048,576 total hosts)
  - Class C — 192.168.0.0 — 192.168.255.255 (65,536 total hosts)
- VM instances within the VPC must not have floating IP.
- You must create a route with the *Delegate-VPC* action in the VPC default routing table to the on-premise public subnet. For more information, see [Routing considerations for IANA-registered IP assignments](/docs/vpc?topic=vpc-interconnectivity#routing-considerations-iana).
