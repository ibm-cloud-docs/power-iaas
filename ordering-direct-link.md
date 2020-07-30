---

copyright:
  years: 2019, 2020

lastupdated: "2020-06-10"

keywords: ordering direct link, dirct link location, bgp asn, iam service id, delete direct link

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

You must use [Direct Link](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link) to configure your private network with a IBM&reg; Power Systems&trade; Virtual Server. The Direct Link Connect service creates a connection that allows access to {{site.data.keyword.cloud}} resources from your {{site.data.keyword.powerSys_notm}} instance. The Direct Link Connect service is also used to connect your on-premises network to the IBM Cloud network by using the IBM Cloud Virtual Router Appliance (VRA). Direct Link Connect is a separate service from the {{site.data.keyword.powerSys_notm}} service. For more information on Direct Link Connect, see [Pricing for IBM Cloud Direct Link](/docs/direct-link?topic=direct-link-pricing-for-ibm-cloud-direct-link) and [IBM Cloud Direct Link Connect on Classic](/docs/direct-link?topic=direct-link-how-to-order-ibm-cloud-direct-link-connect-classic).
{: shortdesc}

The {{site.data.keyword.powerSys_notm}} offering now includes a highly available 5 Gbps connection to IBM public cloud services. The 5 Gbps connection is set up in a high availability (HA) configuration at **$0 for each customer per datacenter**. If desired, you can select the global routing option for these links at no cost. This change allows you to set up connectivity between the {{site.data.keyword.powerSys_notm}} service and other IBM Cloud resources without adding any additional costs. Over the next few months, the {{site.data.keyword.powerSys_notm}} service plans to continue to evolve its network connectivity capabilities through further automation and integration. To learn more about this offer, see [Getting started with IBM Cloud Direct Link on Classic](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link){: new_window}{: external}.

## Ordering Direct Link Connect on Classic
{: #steps-to-order-direct-link-connect}
{: help}
{: support}

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
  <dt></dt>
  <dd>Enter a name for your Direct Link Connect instance.</dd>
  <dt><strong>Location</strong></dt>
  <dt></dt>
  <dd>
    Select the same location as the {{site.data.keyword.powerSys_notm}}
    instance. The following table identifies the
    {{site.data.keyword.powerSys_notm}} instance location and the corresponding
    Direct Link Connection option:
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
        <td>Dallas, TX, US</td>
        <td>Dallas 13</td>
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
        <td>London 6</td>
        <td>IBM Power Virtual Server</td>
      </tr>
      <tr>
        <td>Toronto, Canada</td>
        <td>Toronto 1</td>
        <td>IBM Power Virtual Server</td>
      </tr>
    </table>
  </dd>
  <dt><strong>Network Provider</strong></dt>
  <dt></dt>
  <dd>
    You must select <strong>IBM POWER VIRTUAL SERVER</strong> from the list.
  </dd>
  <dt><strong>Link Speed</strong></dt>
  <dt></dt>
  <dd>
    Select the link speed to meet your workload requirements. The recommended
    selection for the <strong>Link Speed</strong> field is 1000 Mbps.
  </dd>
  <dt><strong>Routing Option</strong></dt>
  <dt></dt>
  <dd>
    Select <strong>Local Routing (Free)</strong> to access all of the data centers that
    are connected at the location that you specified in the
    <strong>Location</strong> field. Select <strong>Global Routing</strong> to
    access all of the IBM Cloud data centers in the world.
  </dd>
  <dt><strong>BGP ASN</strong></dt>
  <dt></dt>
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
        Table 2. BGP ASN number for specific locations
      </caption>
      <tr>
        <th>Direct Link Connect location</th>
        <th>BGP ASN number</th>
      <tr>
        <td>Dallas 13</td>
        <td>64999</td>
      </tr>
      <tr>
        <td>Washington 4</td>
        <td>64995</td>
      </tr>
      <tr>
        <td>Frankfurt 4<br/>Frankfurt 5</td>
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
    </table>
  </dd>
  <dt><strong>Select VRF</strong></dt>
  <dt></dt>
  <dd>
    Select the virtual routing and forwarding option for the connection. If your
    account does not have a VRF identified, this field is not displayed. You can
    still create the Direct Link Connect service without selecting a VRF.
  </dd>
  <dd></dd>
</dl>

## Deleting your Direct Link Connect on Classic connection
{: deleting-direct-link}

You can remove your Direct Link Connect on Classic connection by [opening a support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support) against the Power Systems Virtual Server support team to remove the appropriate resources.
