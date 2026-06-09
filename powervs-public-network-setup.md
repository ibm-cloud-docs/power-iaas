---

copyright:
  years: 2026
lastupdated: "2026-06-03"

keywords: power virtual server, public network, outbound connectivity, inbound connectivity, network setup

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Public network connectivity for {{site.data.keyword.powerSys_notm}}
{: #powervs-public-network-setup}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

---

In some {{site.data.keyword.powerSys_notm}} data centers, internet access is provided through alternative networking configurations as you cannot directly attach public subnets to the logical partition (LPAR) or virtual server instance (VSI) in these data centers. In these cases, you can use Virtual Private Cloud (VPC) infrastructure components and a transit gateway connection to provide both outbound and inbound network connectivity.
{: shortdesc}

A transit gateway connects VPCs and {{site.data.keyword.powerSys_notm}} workspaces.

## Configuring the public network for a {{site.data.keyword.powerSys_notm}} instance
{: #setup-public-networking}

Complete the following steps to configure public network access for your LPAR or VSI:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type {{site.data.keyword.powerSys_notm}} and click the {{site.data.keyword.powerSys_notm}} tile.

3. In the navigation panel, click **Workspaces**. The Workspaces page with a list of the existing workspaces is displayed.

4. Click your workspace from the list to open the virtual server instance page.

5. Create a VSI. For instructions, see [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).

6. Configure the outbound networking for the VSI. For instructions, see [Outbound network overview](#outbound-overview).

7. Configure the inbound networking for the VSI. For instructions, see [Inbound network overview](#inbound-overview). You can configure inbound networking only after you configure outbound networking.

You must select the same region and zone as your VSI for all the configurations.
{: note}

## Outbound network overview
{: #outbound-overview}

{{site.data.keyword.powerSys_notm}} instances can access the internet through outbound network connections. The following architecture describes this setup:

1. Connect the {{site.data.keyword.powerSys_notm}} workspace to a transit gateway. The transit gateway provides the connection between the {{site.data.keyword.powerSys_notm}} instance and the VPC infrastructure.
2. Connecnt the transit gateway to a VPC that contains a network load balancer (NLB) that is configured in route mode.
3. Route internet traffic from {{site.data.keyword.powerSys_notm}} instances through a VPC subnet to the internet by using the NLB as a routing gateway. The VPC security groups that are associated with the NLB filter the traffic between the {{site.data.keyword.powerSys_notm}} instance and the internet.
4. Attach the VPC subnet to a public gateway, which provides the actual internet connectivity.

The following diagram illustrates the outbound network architecture to show how traffic flows from {{site.data.keyword.powerSys_notm}} instances through the transit gateway, VPC, and NLB to reach the internet.

![Outbound network architecture diagram](./images/outbound-network-access-architecture.svg "Outbound network architecture"){: caption="Outbound network architecture" caption-side="bottom"}

When an LPAR or VSI in a {{site.data.keyword.powerSys_notm}} workspace sends traffic to the internet, it sends the data packets to the default gateway. The default gateway routes the traffic through the transit gateway to the VPC. The VPC routing table directs traffic to the NLB, which forwards the traffic through the public gateway to the internet. The return traffic follows the same path back to the {{site.data.keyword.powerSys_notm}} instance.

### Considerations for outbound connectivity

Planning the outbound connectivity for your {{site.data.keyword.powerSys_notm}} instance includes the following considerations:

* A workspace with no external connections restricts LPAR and VSI communication to resources within the same Power Virtual Server workspace only.
* A workspace that is connected to a transit gateway links to a VPC with internet access and enables outbound connectivity for the workspace resources.
* Your {{site.data.keyword.powerSys_notm}} instance inherits network connectivity from the workspace configuration. As a result, you need not configure network access for individual LPAR or VSI instances.

## Configuring outbound network access for {{site.data.keyword.powerSys_notm}}
{: #outbound-network}

Complete the following steps to configure outbound network access for {{site.data.keyword.powerSys_notm}}:

Ensure that a VSI is created before you configure outbound network access. For more informaiton see [Configuring public network for {{site.data.keyword.powerSys_notm}} instance](#setup-public-networking).
{: note}

### Step 1: Create the VPC infrastructure.
{: #create-vpc}

1. Create a VPC and subnet. For instructions, see [Creating a VPC and subnet](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console&q=Create+VPC+Infrastructure&tags=vpc#creating-a-vpc-and-subnet){: external}.

    When you create a VPC, set the following values:
    * Select the same region as your {{site.data.keyword.powerSys_notm}} workspace.
    * Ensure that the **Create a default prefix for each zone** checkbox is selected.

    If the **Create a default prefix for each zone** checkbox is selected, IBM Cloud automatically creates default subnets in each available zone. You can use these default subnets for the NLB or create a custom subnet.


2. Record the subnet ID and Classless Inter-Domain Routing (CIDR) range of the subnet. Use the subnet ID and CIDR range when you craete an NLB. For more information, see [Create NLB with routing mode](#create-nlb).

3. Create a public gateway and attach the public gateway to the VPC subnet. For instructions, see [Creating public gateways](/docs/vpc?topic=vpc-create-public-gateways&interface=ui){: external}.

### Step 2: Create a private NLB in route mode.
{: #create-nlb}

1. Create a private NLB in route mode. For instructions, see [Creating a network load balancer with routing mode by using the UI](/docs/vpc?topic=vpc-nlb-vnf&interface=ui#nlb-vnf-ui){: external}.

    When you create the NLB, set the following values:
    * Select the same VPC and VPC subnet that you created in [Step 1: Create VPC infrastructure](#create-vpc).
    * In the details section, select the type as **Private**.
    * Set **Routing mode for VNFs** to **Enabled** to enable the routing mode for virtual network functions (VNFs).
    * Leave the **Back-end pools** and **Front-end listeners** sections empty.
    * In the **Security groups** section, select the VPC default security group.

2. Create a back-end pool for your NLB. For instructions, see [Working with network load balancer pools](/docs/vpc?topic=vpc-nlb-pools){: external}.

    When you create the back-end pool for your NLB, set the following values:
    * Leave the **Instance group** field empty.
    * Select **Bypass** as the failsafe policy.

3. Configure a listener for your NLB. For instructions, see [Working with listeners](/docs/vpc?topic=vpc-nlb-listeners&q=create+a+listener&tags=vpc&offset=10){: external}.

    When you create the listener for your NLB, select the back-end pool for your NLB as the default back-end pool.

### Step 3: Create a transit gateway and connect to {{site.data.keyword.powerSys_notm}}.
{: #create-transit-gateway}

1. Create a transit gateway. For instructions, see [Creating a transit gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui){: external}.

    When you create the transit gateway, set the following values:
    * Select the default resource group.
    * Ensure that **GRE enhanced route propagation** is set to **Disabled**.
    * Select **Local routing** for a single region.
    * Choose a location that matches your {{site.data.keyword.powerSys_notm}} workspace location.
    * Create the transit gateway without adding network connections.

2. Connect the VPC to the transit gateway. For instructions, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections&interface=ui){: external}.

    When you connect the VPC to the transit gateway, set the following values:
    * Select **VPC** as the network connection.
    * Select **Add new connection in this account** as the connection reach.
    * Use the same region, which is the region of the transit gateway.
    * Select your VPC in the **Available connection** section.

3. Connect the {{site.data.keyword.powerSys_notm}} workspace to the transit gateway. For instructions, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections&interface=ui){: external}.

    When you connect the {{site.data.keyword.powerSys_notm}} workspace to the transit gateway, set the following values:
    * Select **Power Systems Virtual Server** as the network connection.
    * Select **Add new connection in this account** as the connection reach.
    * Use the same region, which is the region of the transit gateway.
    * Select your {{site.data.keyword.powerSys_notm}} workspace in the **Available connection** section.

### Step 4: Configure VPC routing.
{: #vpc-routing}

1. Create a custom routing table. For instructions, see [Creating a routing table](/docs/vpc?topic=vpc-create-vpc-routing-table&interface=ui){: external}.

    When you create the routing table, set the following values:
    * Select your VPC.
    * In the **Traffic** section, set **Transit gateway** to on.
    * Set **Advertise to** to **On**.

2. Create a route. For instructions, see [Creating a route](/docs/vpc?topic=vpc-create-vpc-route&interface=ui){: external}.

    When you create the route, set the following values:
    * Select the same zone as your NLB.
    * Set **Destination CIDR** to the following value:

        `0.0.0.0/0`
    * Set **Priority** to **2**, **Action** to **Deliver**, and the **Next hop (IP address)** to the IP address of your NLB.
    * Set **Advertise** to **On**.


### Step 5: Test outbound connectivity.
{: outbound-connectivity}

From the {{site.data.keyword.powerSys_notm}} VSI console, run the following command to test the outbound connectivity:

```text
      ping -c4 <URL>
```
{: codeblock}

If your outbound connectivity is not working, check whether your VPC security group is configured correctly. You must review the rules that allow only the required TCP protocols. For more information about security groups, see [About security groups](/docs/vpc?topic=vpc-using-security-groups){: external}.
{: note}

## Inbound network overview
{: #inbound-overview}

You can enable inbound network connectivity to allow external clients on the internet to initiate connections to your {{site.data.keyword.powerSys_notm}} instances. This inbound network connectivity requires the [outbound network configuration](#outbound-network). The following architecture describes this setup:

1. Allocate and bind a public IP address range to your VPC in the same zone as your NLB.
2. Configure a secondary network interface within the guest operating system on your {{site.data.keyword.powerSys_notm}} instance by using the public IP address.
3. Configure VPC route tables to direct incoming internet traffic for the public IP address to the NLB.
4. Forward internet traffic from the NLB through the transit gateway to your {{site.data.keyword.powerSys_notm}} workspace.
5. Create a custom route in your {{site.data.keyword.powerSys_notm}} workspace to send internet traffic for the public IP address directly to the private IP address of your {{site.data.keyword.powerSys_notm}} instance.

The following diagram illustrates the inbound network architecture to show how internet traffic is routed through the VPC infrastructure to reach your {{site.data.keyword.powerSys_notm}} instances.

![Inbound network architecture diagram](./images/inbound-network-access-architecture.svg "Inbound network architecture"){: caption="Inbound network architecture" caption-side="bottom"}

When a client on the internet sends traffic to your public IP address, the VPC subnet routing table delegates the traffic to the VPC routing table. The VPC routing table forwards the traffic to the private IP address of the NLB. The NLB forwards the traffic through the transit gateway to {{site.data.keyword.powerSys_notm}}. The workspace routes the traffic directly to your {{site.data.keyword.powerSys_notm}} instance by using its private IP address. The {{site.data.keyword.powerSys_notm}} instance receives the traffic on the secondary interface that is configured with the public IP address.

The {{site.data.keyword.powerSys_notm}} instance sends the response from the public IP address on the secondary interface. {{site.data.keyword.powerSys_notm}} routes the response through the transit gateway to the VPC, which routes the response to the NLB. The NLB then forwards the response to the internet.

## Configuring inbound network access for {{site.data.keyword.powerSys_notm}}
{: #inbound-network}

Configure the inbound network by using the same VPC and subnet that is created in [Step 1: Create VPC infrastructure](#create-vpc).

Ensure that a VSI is created and the outbound network access is configured before you configure the inbound network access. For more informaiton see [Configuring public network for {{site.data.keyword.powerSys_notm}} instance](#setup-public-networking).
{: note}

### Step 1: Attach a public address range (Public IP address) to the VPC.
{: #public-add-range}

If you have a public IP address that is attached to your VPC, do not perform this step and go to [Step 2: Locate the NLB IP address](#find-nlb).
{: note}

1. Reserve a public address range and attach it to the VPC. For instructions, see [Creating public address ranges](/docs/vpc?topic=vpc-par-creating&interface=ui){: external}.

    When you create the public address range, set the following values:
    * Set the **Size** to the following value:

        `/32 (1 address)`
    * Retain the default value for **Geography**, **Region**, and **Resource group**.
    * Set **Bind** to on. Select your VPC to attach the public address range.
    * Set **Zone** to the same zone as the NLB that you create in [Step 2: Create NLB](#create-nlb).

2. Record the allocated public IP address. Use this IP address to access your {{site.data.keyword.powerSys_notm}} VSI from the internet.

### Step 2: Locate the NLB IP address.
{: #find-nlb}

Complete the following steps to locate the private IP address of the NLB that you created in [Step 2: Create NLB](#create-nlb).

If you have not created an NLB, create an NLB in route mode. For instructions, see [Step 2: Create NLB](#create-nlb).
{: note}

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. From the **Navigation** menu, click **Infrastructure** > **Network** > **Load balancers**.

3. Select your NLB and record the private IP address.

### Step 3: Configure a VPC routing table for the internet traffic.
{: #vpc-route-tbl-internet}

1. Create a routing table to direct incoming internet traffic for the public IP address to the NLB. For instructions, see [Creating a routing table](/docs/vpc?topic=vpc-create-vpc-routing-table&interface=ui){: external}.

    When you create the routing table, set the following values:
    * Select your VPC.
    * Set **Traffic source** to **Internet**.
    * Set **Advertise to** to **Off**.

2. Create a route. For instructions, see [Creating a route](/docs/vpc?topic=vpc-create-vpc-route&interface=ui){: external}.

    When you create the route, set the following values:
    * Set the **Zone** to the same zone as your NLB.
    * Set **Destination CIDR** to the following value:

        `1.2.3.4/32`
    * Set **Priority** to **2**, **Action** to **Deliver**, and the **Next hop (IP address)** to the IP address of your NLB.
    * Set **Advertise** to **Off**.

### Step 4: Create the transit gateway.
{: #inbound-transit-gateway}

The transit gateway that you created for outbound connectivity already connects the VPC and Power Virtual Server. For more information, see [Step 3: Create transit gateway and connect to {{site.data.keyword.powerSys_notm}}](#create-transit-gateway).

### Step 5: Configure the VPC routing for transit gateway.

The transit gateway is already configured for outbound connectivity. For more information, see [Step 4: Configure VPC routing](#vpc-routing).

### Step 6: Modify the VPC routing table that is mapped with the NLB subnet.
{: #modify-route-table}

Route the incoming traffic for the public IP address to the VPC subnet. Configure the default routing table and create a route for your VPC. For instructions, see [Creating a route](/docs/vpc?topic=vpc-create-vpc-route&interface=ui){: external}.

When you create a route in the default routing table of your VPC, set the following values:
* Set the **Zone** to the same zone as your NLB.
* Set **Destination CIDR** to the following value:

    `1.2.3.4/32`
* Set **Action** to **Delegate-VPC** and **Next hop (IP address)** to the IP address of your NLB.
* Set **Advertise** to **Off**.

Do not modify the routing table that you created in [Step 4: Configure VPC routing](#vpc-routing).
{: important}

### Step 7: Configure a {{site.data.keyword.powerSys_notm}} route.
{: #powervs-route}

Add a static route to your {{site.data.keyword.powerSys_notm}} workspace that points to your VSI. For instructions, see [Creating and managing network routes in IBM Power Virtual Server workspaces](/docs/power-iaas?topic=power-iaas-routes).

When you create the static route, set the following values:
* Set **Destination** to the following value:

    `1.2.3.4/32`
* Set **Next hop** to your VSI IP address.
* Set **Advertise** and **State** to **Enabled**.

This static route configuration routes traffic for the public IP address directly to the VSI.

### Step 8: Configure the VSI network.
{: #vsi-network}

Since {{site.data.keyword.powerSys_notm}} does not support network address translation (NAT), you must configure the public IP address as a secondary interface in the guest operating system of your VSI. Retain the existing private interface for normal {{site.data.keyword.powerSys_notm}} subnet connectivity, and add the public IP address to a secondary interface.

Configure the secondary interface in the guest operating system on your VSI, and not in the {{site.data.keyword.powerSys_notm}} console. Complete this task in the operating system of your VSI that receives the routed internet traffic.

### Step 9: Configure the security groups with the NLB to permit inbound internet traffic.
{: configure-sg}

If the outbound connectivity is configured, the required security groups are already mapped to your NLB. Verify that the security group allows the required inbound ports for your public IP address.

If the security groups that are mapped with your NLB does not permit the inbound internet traffic, configure the security groups to add the rules for inbound internet traffic. For instrauctions, see [Defining security group rules](/docs/vpc?topic=vpc-using-security-groups#defining-security-group-rules){: external}.

For new outbound or inbound connections, map the required security groups with the NLB. You can also adjust the rules to match your security requirements. For more information about security groups, see [About security groups](/docs/vpc?topic=vpc-using-security-groups){: external}.

### Step 10: Test the public IP address
{: test-public-ip}

Test the public IP address from outside the IBM network by using a protocol that is permitted by your network security group.

For example:

```text
      ping -c4 <IP_ADDRESS>
```
{: codeblock}

or

```text
      ssh  <IP_ADDRESS>
```
{: codeblock}

With outbound and inbound network connectivity configured, your {{site.data.keyword.powerSys_notm}} instance can communicate with external networks by using the VPC infrastructure and a transit gateway.
