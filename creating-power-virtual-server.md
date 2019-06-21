---

copyright:
  years: 2019

lastupdated: "2019-05-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:table: .aria-labeledby="caption"}

# Creating a Power Systems Virtual Server
{: #creating-power-virtual-server}

To create and configure a {{site.data.keyword.powerSysFull}}, complete the following steps:

1. Log in to the [IBM Cloud catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog){: new_window} with your IBM Cloud account credentials.
1. From the Catalog, select **Compute**, and under the **Infrastructure** heading click the **Power Systems Virtual Server** tile.
1. From the Power Systems Virtual Server catalog entry, select the location you want to deploy your {{site.data.keyword.powerSys_notm}} in and click **Create**.
1. From the Resource List, click **Manage > Virtual Instances > Provision New**.
1. Complete all fields and click **Create** to create the {{site.data.keyword.powerSys_notm}}. The following table provides information about the fields that you might have trouble completing.

    As you complete the fields to create a {{site.data.keyword.powerSys_notm}} the price is dynamically updated in the **Order Summary** section. You can easily see what each options cost and create a cost-effective {{site.data.keyword.powerSys_notm}} for your business needs.
    {:tip}

<table>
<caption>Table 1. New Power Virtual Server Instance fields</caption>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
<tr>
<td>Number of Instances</td>
<td>Specify the number of instances that you want to create for the {{site.data.keyword.powerSys_notm}}. If you specify more than one instance, you can select the following naming conventions and collocation rules:
  <dl>
    <dt><strong>Same Server</strong></dt>
  <dd>Select this option to have all instances hosted on the same server. You can use this option if you want fast communication between each {{site.data.keyword.powerSys_notm}} instance.</dd>
    <dt><strong>Different  Server</strong></dt>
  <dd>Select this option to have each instance hosted on a different server.  You can use this option if you are concerned about a single-server outage occurring that could affect all {{site.data.keyword.powerSys_notm}} instances. </dd>
  <dt><strong>Numerical Prefix</strong></dt>
  <dd>Select this option to add numbers before the name of the virtual server. For example, if the first {{site.data.keyword.powerSys_notm}} name is <tt>Austin</tt> the next name for the virtual instance is <tt>1Austin</tt></dd>
  <dt><strong>Numerical Postfix</strong></dt>
  <dd>Select this option to add numbers after the name of the virtual server. For example, if the first {{site.data.keyword.powerSys_notm}} name is <tt>Rochester</tt> the next name for the virtual instance is <tt>Rochester1</tt>.</dd>
  </dl>
  <p>
  <b>Note:</b> When you create multiple instances of the virtual server, you must select On from the Shareable field for each data volume that you add. If you do not want the data volume to be shareable, you can add the data volume after you create the virtual server.
  </p>
   </td>
</tr>
<tr>
<td>Pin Virtual Machine</td>
<td>Select <b>On</b> to lock the {{site.data.keyword.powerSys_notm}} onto a host system. If you select <b>On</b>, the virtual server cannot be moved to a different host. For example, by selecting <b>On</b> you would experience an outage during host maintenance.</td>
</tr>
<tr>
<td>Machine Type</td>
<td>Specify the machine type. The machine type that you select determines the number of cores and memory that is available. For more information about hardware specifications, see <a href="https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm" target="_blank">S922</a> and <a href="https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm" target="_blank">E880</a>.</td>
</tr>
<tr>
<td>Cores</td>
<td>Select the number of cores for the {{site.data.keyword.powerSys_notm}}. If you selected <b>Shared Processors</b>, you can specify the number of cores by 0.25 increments. For example, valid core values are 0.5, 1.25, and 2.75. A virtual CPU is allocated for every 0.25 entitlement. If you are concerned about performance issues, you can select <b>Dedicated Processor</b> because the process is dedicated to your virtual server and is not shared. For more information, see <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">How does Shared Processor Performance Compare to Dedicated Processors</a>.</td>
</tr>
<tr>
<td>Memory</td>
<td>Select the amount of memory for the {{site.data.keyword.powerSys_notm}}. The amount of memory that you can select depends on the number of cores you selected. For each core that you select, you can allocate up to 64 GB. For example, if you selected four cores you are allowed to select up to 256 GB of memory. </td>
</tr>
<tr>
<td>Create Boot Volume</td>
<td>Select a version of the AIX or IBM i operating system stock image that are provided for you, or select a custom AIX or IBM i operating system image that you previously deployed on-premises.
<p>
The following are the stock images that are provided to you by IBM:
<ul>
<li><b>AIX</b>
  <ul>
  <li>7200-03-02</li>
  <li>7100-05-03</li>
  </ul>
</li>
<li><b>IBM i</b>
  <ul>
  <li>7.3 TR5</li>
  <li>7.2 TR9</li>
  </ul>
</li>
</ul>
</p>
<p>
If you want to bring your own custom image, you must use a supported technology level of the AIX or IBM i operating system image for the Power Systems hardware that you selected in the <b>Machine Type</b> field. For more information, see <a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">Configuring a custom image</a>.
</p>
</td>
</tr>
<tr>
<td>Attached Data Volumes</td>
<td>You can either create a new data volume or attach an existing data volume that is already defined in your IBM Cloud account.
<dl>
  <dt><strong>Create Data Volume</strong></dt>
  <dd>Click <b>Add</b> to create a new data volume that can be used for more storage for your {{site.data.keyword.powerSys_notm}} instance. If you want to allow multiple instances of {{site.data.keyword.powerSys_notm}} to write data to the same data volume, you must select <b>On</b> from the <b>Shareable</b> field. </dd>
  <dt><strong>Attach Existing Data Volume</strong></dt>
  <dd>Select an existing data volume from the list that can be used for more storage for your {{site.data.keyword.powerSys_notm}} instance. If the list does not display a data volume that you have previously used, it is most likely because that data volume was created with a different IBM Cloud account. </dd>
</dl>
</td>
</tr>
<tr>
<td>Public Networks</td>
<td>Select this option use a public network that IBM provides. There is a cost that is associated with selecting this option. For more information, see <a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">Public and private networks</a>.
</td>
</tr>
<tr>
<td>Private Networks</td>
<td>Click <b>Add</b> to identify a new private network for the virtual server. If you already added a private network, you can select it from the list. For more information, see <a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">Configure private network</a>.</td>
</tr>
</table>
