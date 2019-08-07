---

copyright:
  years: 2019

lastupdated: "2019-08-7"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Ordering IBM Cloud Direct Link Connect for Power Systems Virtual Servers
{: #ordering-direct-link-connect}

One option for configuring a private network with {{site.data.keyword.powerSys_notm}} is to use the Direct Link Connect service. The Direct Connect Link service creates a connection that allows access to {{site.data.keyword.cloud}} resources from you {{site.data.keyword.powerSys_notm}} instance. The Direct Link Connect service is also used to connect your on-premises network to the IBM Cloud network by using the IBM Cloud Virtual Router Appliance (VRA).
{:shortdesc}

You can use the {{site.data.keyword.cloud_notm}} UI console to order the Direct Link Connect service. Direct Link Connect is a separate service from the {{site.data.keyword.powerSys_notm}} service. To review the charges for Direct Link Connect, see [Pricing for IBM Cloud Direct Link](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-ibm-cloud-direct-link.

IBM recommends that you order a second Direct Link Connect connection for backup purposes.

## Before you begin
{: #before-direct-link-connect}

* Verify your {{site.data.keyword.cloud}} account has the correct authorizations to order the Direct Link Connect service.
* Understand the basic networking concepts for the Direct Link Connect service by reviewing the following topics:
    * [Direct Link Connect concepts](/docs/infrastructure/direct-link?topic=direct-link-about-ibm-cloud-direct-link)
    * [Direct Link Connect details](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
    * [Direct Link Connect limitations](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
    * [Strict limitations on IP assignments](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Steps to order Direct Link Connect
{: #steps-to-order-direct-link-connect}

To order the Direct Link Connect service that creates a connection to the {{site.data.keyword.powerSys_notm}} instance, complete the following steps:

1. Log in to the [IBM Cloud catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog){: new_window} with your IBM Cloud account credentials. Your account must have correct authorization to order the Direct Link Connect service.

1. In the **Networking** section, click the **Direct Link Connect** tile.
![Displays the Direct Link catalog tile](./images/directlink1.png "Displays the Direct Link catalog tile"){: caption="Figure 1. Direct Link Connect tile from the IBM Cloud catalog." caption-side="bottom"}

1. From the Direct Link Connect catalog entry, click **Create**.

1. From the IBM Cloud Direct Link page, click **Order Direct Link Connect**.

1. From the Create IBM Cloud Direct Link Connect Connection page, complete the following fields.

   As you complete the following fields for creating the Direct Link Connect service, the price is automatically updated to reflect your selections.
   {: note}

   <dl>
   <dt><strong>Direct Link Instance Name</strong><dt>
   <dd>Enter a name that describes the purpose of the Direct Link Connect.</dd>
   <dt><strong>Location</strong><dt>
   <dd>Select the same location as the {{site.data.keyword.powerSys_notm}} instance. The following table identifies the {{site.data.keyword.powerSys_notm}} instance location and the corresponding Direct Link Connection option:
   <table>
   <caption>Table 1. Direct Link Connection location options</caption>
   <tr>
   <th>Power Systems Virtual Server location</th>
   <th>Direct Link Connect location</th>
   </tr>
   <tr>
   <td>Dallas, TX US</td>
   <td>Dallas 4</td>
   </tr>
   <tr>
   <td>Washington D.C, US</td>
   <td>Washington 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Network Provider</strong><dt>
   <dd>You must select <strong>MEGAPORT</strong> from the list.</dd>
   <dt><strong>Link Speed</strong><dt>
   <dd>Select the link speed to meet your workload requirements. The recommended selection for  this field is 1000 Mbps.</dd>
   <dt><strong>Routing Option</strong><dt>
   <dd>Select <strong>Local Routing (Free)</strong> to access all data centers that are connected at the location that you specified in the <strong>Location</strong> field. Select <strong>Global Routing</strong> to access all IBM Cloud data centers in the world. </dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>You must enter the BGP ASN number for the specific Direct Link Connect location in the following table.
   <table>
   <caption>Table 2. BGP ASN number for specific locations</caption>
   <tr>
   <th>Direct Link Connect location</th>
   <th>BGP ASN number</th>
   </tr>
   <tr>
   <td>Dallas 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>Washington 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Select VRF</strong><dt>
   <dd>Select the virtual routing and forwarding option for the connection. If your account does not have a VRF identified, this field is not displayed. You can still create the Direct Link Connect service without selecting a VRF.The following figure is an example of the Direct Link Connect fields.</dd>
   <dd>

   ![Displays the Direct Link Connect fields that are completed](./images/directlink2.png "Displays the Direct Link Connect fields that are completed"){: caption="Figure 2. Direct Link Connect fields." caption-side="bottom"}
   </dd>
   </dl>
1. Read the **Master Service Agreement** and select the check box. You must read and understand the **Master Service Agreement** as it contains important technical information.

1. Click **Create**. The following message is displayed when your request is submitted successfully.
![Displays the Direct Link Connect submitted successfully message](./images/directlink3.png "Displays the Direct Link Connect submitted successfully message"){: caption="Figure 3. Direct Link Connect success message." caption-side="bottom"}

1. Click the **Case number** link for the Direct Link Connect service. The information in the case number is used to identify the Direct Link Connect information for connecting your {{site.data.keyword.powerSys_notm}} instance.

    It can take IBM Cloud support up to three business days to create the Direct Link Connect connection.
    {: note}

1. To create a connection to the {{site.data.keyword.powerSys_notm}} instance by using the Direct Link Connect service, open a [new case](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support) for the {{site.data.keyword.powerSys_notm}} support team.

    1. In the new case's description field, add the Direct Link Connect case number.
    2. Copy the {{site.data.keyword.powerSys_notm}} case IAM Service ID that the system automtically generated.

1. Enter the IAM Service ID from the {{site.data.keyword.powerSys_notm}} case into the Direct Link Connect case. When the Direct Link Connect connection is created, the Direct Link Connect case number is closed. The following is an example of the network information that is displayed in the case:

  ```shell
  Link Speed:                  1000 Mbps
  Location:                    Washington 2
  Network Provider:            MEGAPORT
  IBM IP Address:              10.254.0.25/30
  Customer IP Address:         10.254.0.26/30
  Service Key:                 None
  BGP ASN:                     64999
  Network Identifier:          1748523-1
  Date Created:                2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. Use this information from the Direct Link Connect case number and enter the following network information into the {{site.data.keyword.powerSys_notm}} case:

  ```shell
  Customer name:
  Customer account ID:
  Direct Link Connect subnet:
  Power Systems Virtual Server network IP address:
  IBM Cloud IP address:
  Power Systems Virtual Server network ASN:
  IBM Cloud ASN:
  Private Network ID (1):
  Private Network ID (2):
  Private Network ID (3):
  ```
  {: codeblock}

1. The {{site.data.keyword.powerSys_notm}} case is closed when the Direct Link Connect connection is configured to communicate with your {{site.data.keyword.powerSys_notm}} instance.
