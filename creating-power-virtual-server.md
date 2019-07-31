---

copyright:
  years: 2019

lastupdated: "2019-07-25"

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
2. In the catalog's search box, type **Power Systems Virtual Server** and click on the  {{site.data.keyword.powerSys_notm}} tile.

    ![IBM Cloud catalog](./images/catalog-search-bar.png "IBM Cloud catalog"){: caption="Figure 1. IBM Cloud catalog" caption-side="bottom"}

3. Give your service a name and choose where you'd like to deploy your {{site.data.keyword.powerSys_notm}} instance.

    ![Service and region selection](./images/power-iaas-service-region.png "Service and region selection"){: caption="Figure 2. Service and region selection" caption-side="bottom"}

4. Click the **Create** button at the bottom of the webpage.

    ![Create button](./images/power-iaas-create-button.png "Create Button"){: caption="Figure 3. Create button" caption-side="bottom"}

5. After you click the **Create** button, you are redirected to the **Resource List** panel.
6. From the **Resource List**, select your service under **Services** to go to the **Manage** panel.

    ![IBM Cloud Resource List](./images/power-iaas-resource-list.png "IBM Cloud Resource List"){: caption="Figure 3. IBM Cloud Resource List" caption-side="bottom"}

7. From here, click the **provision new** button and complete all of the required fields.

     The price is dynamically updated in the **Order Summary** section as you complete the fields to create a {{site.data.keyword.powerSys_notm}}. This allows you to easily create a cost-effective {{site.data.keyword.powerSys_notm}} that satisfies your business needs.
     {: tip}

    ![Provisioning a new virtual server](./images/power-iaas-provision-new.png "Provisioning a new virtual server"){: caption="Figure 4. Provisioning a new virtual server" caption-side="bottom"}

8. Accept the **Terms of Use** and click the **Create** button to provision a {{site.data.keyword.powerSys_notm}}.

The following table provides information about the **Virtual server instance** fields:

<table>
<caption>Table 1. New Power Virtual Server Instance fields</caption>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
<tr>
<td>Number of Instances</td>
<td>Specify the number of instances that you want to create for the {{site.data.keyword.powerSys_notm}}. If you specify more than one instance, you can select the following naming conventions and colocation rules:
  <dl>
    <dt><strong>Same Server</strong></dt>
  <dd>Select this option to have all instances hosted on the same server. You can use this option if you want fast communication between each {{site.data.keyword.powerSys_notm}} instance.</dd>
    <dt><strong>Different  Server</strong></dt>
  <dd>Select this option to have each instance hosted on a different server.  You can use this option if you are concerned about a single-server outage occurring that might affect all {{site.data.keyword.powerSys_notm}} instances. </dd>
  <dt><strong>Numerical Prefix</strong></dt>
  <dd>Select this option to add numbers before the name of the virtual server. For example, if the first {{site.data.keyword.powerSys_notm}} name is <kbd>Austin</kbd> the next name for the virtual instance is <kbd>1Austin</kbd></dd>
  <dt><strong>Numerical Postfix</strong></dt>
  <dd>Select this option to add numbers after the name of the virtual server. For example, if the first {{site.data.keyword.powerSys_notm}} name is <kbd>Rochester</kbd> the next name for the virtual instance is <kbd>Rochester1</kbd>.</dd>
  </dl>
  <p>
  <strong>Note:</strong> When you create multiple instances of the virtual server, you must select <strong>On</strong> from the <strong>Shareable</strong> field for each data volume that you add. If you do not want the data volume to be shareable, you can add the data volume after you create the virtual server.
  </p>
   </td>
</tr>
<tr>
<td>Pin Virtual Machine</td>
<td>Select <strong>On</strong> to lock the {{site.data.keyword.powerSys_notm}} onto a host system. If you select <strong>On</strong>, the virtual server cannot be moved to a different host. For example, by selecting <strong>On</strong> you would experience an outage during host maintenance.</td>
</tr>
<tr>
<td>Machine Type</td>
<td>Specify the machine type. The machine type that you select determines the number of cores and memory that is available. For more information about hardware specifications, see <a href="https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/1/760/ENUS9009-_h01/index.html&lang=en&request_locale=en" target="_blank">S922</a> and <a href="https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/5/872/ENUS9119-_h05/index.html&lang=en&request_locale=en" target="_blank">E880</a>.</td>
</tr>
<tr>
<td>Cores</td>
<td>Select the number of cores for the {{site.data.keyword.powerSys_notm}}. If you selected <strong>Shared Processors</strong>, you can specify the number of cores by 0.25 increments. For example, valid core values are 0.5, 1.25, and 2.75. A virtual CPU is allocated for every 0.25 entitlement. If you are concerned about performance issues, you can select <strong>Dedicated Processor</strong> because the process is dedicated to your virtual server and is not shared. For more information, see <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">How does Shared Processor Performance Compare to Dedicated Processors</a>.</td>
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
<li><strong>AIX</strong>
  <ul>
  <li>7200-03-02</li>
  <li>7100-05-03</li>
  </ul>
</li>
<li><strong>IBM i</strong>
  <ul>
  <li>7.3 TR5</li>
  <li>7.2 TR9</li>
  </ul>
</li>
</ul>
</p>
<p>
If you want to bring your own custom image, you must use a supported technology level of the AIX or IBM i operating system image for the Power Systems hardware that you selected in the <strong>Machine Type</strong> field. For more information, see <a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">Configuring a custom image</a>.
</p>
</td>
</tr>
<tr>
<td>Attached Data Volumes</td>
<td>You can either create a new data volume or attach an existing data volume that is already defined in your IBM Cloud account.
<dl>
  <dt><strong>Create Data Volume</strong></dt>
  <dd>Click <strong>Add</strong> to create a new data volume that can be used for more storage for your {{site.data.keyword.powerSys_notm}} instance. If you want to allow multiple instances of {{site.data.keyword.powerSys_notm}} to write data to the same data volume, you must select <strong>On</strong> from the <strong>Shareable</strong> field. </dd>
  <dt><strong>Attach Existing Data Volume</strong></dt>
  <dd>Select an existing data volume for more storage for your {{site.data.keyword.powerSys_notm}} instance. If the list does not display a data volume that you have previously used, it might be because that data volume was created with a different IBM Cloud account.</dd>
</dl>
</td>
</tr>
<tr>
<td>Public Networks</td>
<td>Select this option to use an IBM-provided public network. There is a cost that is associated with selecting this option. For more information, see <a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">Public and private networks</a>.
</td>
</tr>
<tr>
<td>Private Networks</td>
<td>Click <strong>Add</strong> to identify a new private network for the virtual server. If you already added a private network, you can select it from the list. For more information, see <a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">Configure private network</a>.</td>
</tr></table>
