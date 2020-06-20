---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-10"

keywords: getting started, power systems virtual server, configure instance, processor, profile, networking

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

# Creating a Power Systems Virtual Server
{: #creating-power-virtual-server}
{: help}
{: support}

To create and configure a {{site.data.keyword.powerSysFull}}, complete the following steps.
{: shortdesc}

<!-- If you're creating and configuring a {{site.data.keyword.powerSys_notm}} to support an SAP NetWeaver workload, see [Setting up your Power System Virtual Server and Instances](/docs/sap-netweaver-power?topic=sap-netweaver-power-set-up-power-infrastructure). -->

## Creating a Power Systems Virtual Server service
{: #creating-service}

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: new_window}{: external} with your IBM Cloud account credentials.

2. In the catalog's search box, type **Power Systems Virtual Server** and click the {{site.data.keyword.powerSys_notm}} tile.

    <!-- ![The IBM Cloud catalog](./images/catalog-search-bar.png "The IBM Cloud catalog"){: caption="Figure 1. The IBM Cloud catalog" caption-side="bottom"} -->

3. Give your service a name and choose where you'd like to deploy your {{site.data.keyword.powerSys_notm}} instance. See the following table to select the appropriate location for your service.

    <!-- ![Selecting a service and region](./images/power-iaas-service-region.png "Selecting a service and region"){: caption="Figure 2. Selecting a service and region" caption-side="bottom"} -->

| Location               | Region   | Data center |
| ---------------------- | -------- | ----------- |
| Dallas, Texas          | us-south | DAL13       |
| Washington, D.C.       | us-east  | WDC04       |
| Toronto, Canada        | eu-east  | TOR01       |
| Frankfurt, Germany     | eu-de    | FRA04/FRA05 |
| London, United Kingdom | eu-gb    | LON06       |
{: caption="Table 1. Power Systems Virtual Server data centers" caption-side="bottom"}

4. Click **Create**. You are redirected to the **Resource List**.

    <!-- ![Creating a Power Systems Virtual Server service](./images/power-iaas-create-button.png "Creating a Power Systems Virtual Server service"){: caption="Figure 3. Creating a Power Systems Virtual Server service" caption-side="bottom"} -->

5. From the **Resource List**, select your {{site.data.keyword.powerSys_notm}}    service under **Services**.

    ![The IBM Cloud Resource List](./images/power-iaas-resource-list.png "The IBM Cloud Resource List"){: caption="Figure 1. The IBM Cloud Resource List" caption-side="bottom"}

6. Click **New instance** under **Virtual server instances**.

## Configuring a Power Systems Virtual Server instance
{: #configuring-instance}

To begin, complete all of the fields under the **Virtual servers** section. If you select more than one instance, you are presented with additional options.

  The total due per month is dynamically updated in the **Order Summary** based on your selections. You can easily create a cost-effective {{site.data.keyword.powerSys_notm}} instance that satisfies your business needs.
  {: tip}

  ![Creating a power virtual server instance](./images/console-create-virtual-instance.png "Creating a power virtual server instance"){: caption="Figure 2. Creating a Power Systems Virtual Server instance" caption-side="bottom"}

1. Choose an existing SSH key or create one to securely connect to your {{site.data.keyword.powerSys_notm}}.

2. Complete the **Boot image** fields as instructed by your organization. When you select **Boot image**, the {{site.data.keyword.powerSys_notm}} user interface allows you to select from a group of stock images or the list of images in your catalog. You must select a storage type for stock images. Currently, you cannot mix **Tier 1** and **Tier 3** storage types. To see your boot images, go to **Boot images** after you provision the instance.

    If you select IBM i as the boot image, the {{site.data.keyword.powerSys_notm}} user interface generates a list with the following licenses: *IBM i Cloud Storage Solution*, *IBM i Power HA*, and *Rational Dev Studio for IBM i*. Adding a license increases the service's cost.

3. Select your **Machine type**, the number of **Cores**, the amount of **Memory (GB)** and whether you'd like a **Dedicated processor**, **Uncapped shared processor**, or **Capped shared processor**.

    There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. For more information on processor types, see [What's the difference between capped and uncapped shared processor performance? How does they compare to dedicated processor performance?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#processor).
    {: important}

    ![Selecting your processor and system](./images/console-profile.png "Selecting your processor and system"){: caption="Figure 3. Selecting your processor and system" caption-side="bottom"}

    When using an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login appears as being *disabled*. For more information, see [How to create a new AIX VM with SSH keys for root login](/docs/power-iaas?topic=power-iaas-create-vm).

      <!-- ![Defining your volumes](./images/console-volume-network.png "Defining your volumes"){: caption="Figure 8. Defining your volumes" caption-side="bottom"} -->

4. Finally, define your **Network interfaces** by adding a public network, private network, or both. When adding an existing private network, you can choose a specific IP address or have one auto-assigned.

    For an AIX VM, network interface controllers (NICs) are assigned based on the order in which you specify them during creation. To display information about all of the network interfaces after provisioning, open the AIX console and type `ifconfig -a`.
    {: note}

    <!-- ![Defining your network interfaces](./images/console-add-private-network.png "Defining your network interfaces"){: caption="Figure 8. Defining your network interfaces" caption-side="bottom"} -->

5. Accept the **Terms of Use** and click **Create instance** to provision a new {{site.data.keyword.powerSys_notm}}.

Refer to the following table for more information on each {{site.data.keyword.powerSys_notm}} instance field.

<table>
  <caption>
    Table 2. Power Systems Virtual Server instance fields
  </caption>
  <tr>
    <th>Field</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Number of Instances</td>
    <td>
      Specify the number of instances that you want to create for the
      {{site.data.keyword.powerSys_notm}}. If you specify more than one
      instance, you can select the following naming conventions and colo rules:
      <dl>
        <dt><strong>No preference</strong></dt>
        <dd>Select this option if you do not have a hosting preference.</dd>
        <dt><strong>Different Server</strong></dt>
        <dd>
          Select this option to host each instance on a different server. You
          can use this option if you are concerned about a single-server outage
          that might affect all {{site.data.keyword.powerSys_notm}} instances.
        </dd>
        <dt><strong>Numerical refix</strong></dt>
        <dd>
          Select this option to add numbers before the name of the virtual
          server. If, for example, the first {{site.data.keyword.powerSys_notm}}
          name is <em>Austin</em> the next name for the virtual instance is
          <em>1Austin</em>.
        </dd>
        <dt><strong>Numerical postfix</strong></dt>
        <dd>
          Select this option to add numbers after the name of the virtual
          server. If, for example, the first {{site.data.keyword.powerSys_notm}}
          name is <i>Austin</i> the next name for the virtual instance is
          <em>Austin1</em>.
        <dt><strong>VM pinning</strong></dt>
        <dd>
          Select this option to pin your virtual machine. You can choose either a <em>soft</em> or <em>hard</em> pinning policy.<br><a href="https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-power-iaas-faqs#pinning" target="_blank">Learn more</a>
        </dd>
      </dl>
      <p>
        <strong>Note:</strong> When you create multiple instances of the virtual
        server, you must select <strong>On</strong> from the
        <strong>Shareable</strong> field for each data volume that you add. If
        you do not want the data volume to be shareable, you can add the data
        volume after you create the virtual server.
      </p>
    </td>
  </tr>
  <tr>
  </tr>
  <tr>
    <td>Machine type</td>
    <td>
      Specify the machine type. The machine type that you select determines the
      number of cores and memory that is available. For more information about
      hardware specifications, see <a href="https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/5/872/ENUS9119-_h05/index.html&lang=en" target="_blank">E880</a>,
      <a href="https://www.ibm.com/downloads/cas/KQ4BOJ3N" target="_blank">S922</a>, and
      <a href="http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only" target="_blank">E980 (Frankfurt only)</a>.
    </td>
  </tr>
  <tr>
    <td>Cores</td>
    <td>
      There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs.
    </td>
  </tr>
  <tr>
    <td>Memory</td>
    <td>
      Select the amount of memory for the {{site.data.keyword.powerSys_notm}}.
      If you choose to use more than 64 GBs of memory per core, you are charged
      a higher price. For example, when you choose one core with 128 GBs of
      memory, you are charged the regular price for the first 64 GBs. After the
      first 64 GBs (64 - 128 GBs), you are charged a higher price.
    </td>
  </tr>
  <tr>
    <td>Boot image</td>
    <td>
      Select a version of the IBM-provided AIX or IBM i operating system stock
      image.<br>
      <a href="/docs/power-iaas?topic=power-iaas-deploy-custom-image"
        >Learn more</a><p>
        <strong>Important</strong>: When you use an AIX stock image as the boot
        volume, a console session is required for the initial setting of the
        root user password. Without completing this step, SSH login as root
        appears as being <i>disabled</i>.
      </p><p>
        For IBM i operating system licensing information, see
        <a href="/docs/power-iaas?topic=power-iaas-ibmi-lpps">IBM i License Program Products (LPP) and Operating System (OS) feature bundles</a>.
      </p>
    </td>
  </tr>
  <tr>
    <td>Attached volumes</td>
    <td>
      You can either create a new data volume or attach an existing one that you
      defined in your IBM Cloud account.
      <dl>
        <dt><strong>Creating a new data volume</strong></dt>
        <dd>
          Click <strong>Add</strong> to create a new data volume for your
          {{site.data.keyword.powerSys_notm}} instance. If you want to allow
          multiple virtual instances to write data to the same data volume, you
          must click <strong>On</strong> under <strong>Shareable</strong>.
        </dd>
        <dt><strong>Attaching an existing data Volume</strong></dt>
        <dd>
          You can select an existing data volume from the
          <b>Attached volumes</b> list. If a previously used data volume does
          not appear, it might exist under a different IBM Cloud account.
        </dd>
      </dl>
    </td>
  </tr>
  <tr>
    <td>Public Networks</td>
    <td>
      Select this option to use an IBM-provided public network. There is a cost
      that is associated with selecting this option.<br>
      <a href="/docs/power-iaas?topic=power-iaas-about-virtual-server#public-private-networks" target="_blank">Learn more</a>
    </td>
  </tr>
  <tr>
    <td>Private Networks</td>
    <td>
      Click <strong>Add</strong> to identify a new private network for the
      virtual server. If you already added a private network, you can select it
      from the list. For more information, see
      <a href="/docs/power-iaas?topic=power-iaas-configuring-subnet" target="_blank">Configure private network</a>.
    </td>
  </tr>
</table>
