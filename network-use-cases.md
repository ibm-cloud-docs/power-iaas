---

copyright:
  years: 2023, 2024

lastupdated: "2025-07-24"

keywords: network, network use cases, {{site.data.keyword.powerSys_notm}}, private cloud, terminology, architecture, how-to, outbound-only, bidirectional, BGP, DHCP, full linux

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network use cases
{: #network_use_cases}

---



{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Review the common network use cases within the network architecture of {{site.data.keyword.powerSysFull}}.
{: shortdesc}

## Use case 1: Private network within a pod
{: #connect_lpars_within_pod}

With this use case, you can establish a private network within a pod that allows communication between the applications that are located in the pod. You can establish a private network within the pod by using the IP address allocation method, Classless Inter-Domain Routing (CIDR).

You can deploy virtual machines in a pod that has a default configuration by using one of the following patterns:
* **Affinity**: In this pattern, virtual machines are deployed on the same physical host. Therefore, the virtual machines can communicate with each other on the same host through the attached Ethernet switch.
* **Anti-affinity**: In this pattern, virtual machines are deployed on different physical hosts. A custom configuration is required on the externally connected Ethernet switch to enable communication between virtual machines that are deployed on different physical hosts.

### Example
{: #pri-example}

You have a database server and a web server that need to communicate exclusively with each other. You can connect both servers to the same private network to enable communication between them.

Figure 1 describes the private network within a pod type of network setup.
![Private network within a pod](./figures/connect_lpars_within_pod.png "Private network within a pod"){: caption="Private network within a pod" caption-side="bottom"}







## Use case 2: Multiple external connections
{: #static-l3}

With this use case, you can access the external connectivity to and from the virtual machines in a subnet. 

To access the external connectivity, you must create peer interfaces and establish an external subnet in a workspace. The VMs deployed on the workspace can access the external environment.

To access the external connectivity, complete the following steps:

**Step 1: Create a peer interface**

To create a peer interface, complete the following steps:

1. Create a workspace.
2. Open a [support ticket](https://cloud.ibm.com/docs/get-support?topic=get-support-using-avatar&interface=ui){: external} to create a peer interface. The support team sets up a peer interface with one of the following combinations:
   - Layer 2
   - Layer 2 and Layer 3 with BGP route
   - Layer 2 and Layer 3 with static route
   - Layer 3 BGP route
   - Layer 3 static route

    The peer interface combination is based on the type of data network cabling in your infrastructure. If you need a specific combination of peer interface, you must specify the combination in the ticket.


**Step 2: Create an external subnet**

To create an external subnet, use one of the peer interfaces configured in `Step 1`.



**Step 3: Deploy VMs to access external connectivity**

To configure your workspace, open a [support ticket](https://cloud.ibm.com/docs/get-support?topic=get-support-using-avatar&interface=ui){: external}.

You can deploy VMs on your workspace after you receive the confirmation from the support team about the completion of configuring your workspace.



### Bidirectional external connectivity through BGP
{: #bi-dir-ext-conn-bgp}

With this use case, you can establish a network that allows communication between the applications within the pod and with the destination points on the external network. By setting up the Layer 3 Firewall rules, you can allow both inbound and outbound connections. Configure the BGP manually between the pod router and the corporate network. By using the BGP configuration, establish a connection between the private network and the corporate network. To configure BGP manually, contact the Support Center. For more information, see [Getting support](https://cloud.ibm.com/docs/get-support?topic=get-support-using-avatar&interface=ui){: external} section.

#### Example
{: #BGP-example}

 You have a database server that is running inside the pod. You need to access the database server from another application that resides outside the pod but within your corporate network. Layer 3 inbound access, you can route the traffic and apply your corporate firewall or routing rules to access the database server. The corporate network can access the pod subnets by using a BGP connection.

Figure 3 describes the bidirectional external connectivity through BGP type of network setup.
![Bidirectional external connectivity through BGP](./figures/bi-dir-ext-conn-bgp.png "Bidirectional external connectivity through BGP"){: caption="Bidirectional external connectivity through BGP" caption-side="bottom"}

### Bidirectional external connectivity through static routes
{: #bi-dir-ext-conn-static-routes}

With this use case, you can establish a network that allows communication between applications within the pod and with destination points on the external network. Layer 3 firewall rules, you can allow both inbound and outbound connections. Establish a static route between edge routers that are within the pod and to the next hop router that is within the corporate network. The static route establishes a connection between the pod subnet and the corporate network. To establish the static route connectivity manually, contact the Support Center. For more information, see [Getting support](https://cloud.ibm.com/docs/get-support?topic=get-support-using-avatar&interface=ui){: external} section.

#### Example
{: #static-example}

You have a database server that is running inside the pod. You need to access the database server from another application that resides outside the pod but within your corporate network. Layer 3 inbound access, you can route the traffic and apply your corporate firewall or routing rules to access the database server. Your corporate network can access the pod subnets through a static route connection.

Figure 4 describes the bidirectional external connectivity through static routes type of network setup.
![Bidirectional external connectivity through static routes](./figures/static-route.png "Bidirectional external connectivity through static routes"){: caption="Bidirectional external connectivity through static routes" caption-side="bottom"}

### Bidirectional external connectivity - Layer 2
{: #bi-dir-ext-conn-L2out}

With this use case, you can create a network that allows communication between applications within the pod and with destination points on the external network. Integrate a Layer 2 firewall with one of your existing corporate networks to allow the outbound connections. In this type of network, bidirectional external connectivity bypasses the router and connect to the IBM {{site.data.keyword.powerSys_notm}} network fabric. You can establish this type of connectivity when you want the same IP address space on both internal and external networks. All other external networks involve two distinct subnets.

Figure 5 describes the bidirectional external connectivity by using Layer 2 firewall type of network setup.
![Bidirectional external connectivity through L2Out](./figures/bi-dir-ext-conn-ACI-L2out.png "Bidirectional external connectivity through L2Out"){: caption="Bidirectional external connectivity through L2Out" caption-side="bottom"}

## Use case 3: Network connectivity for full Linux subscription
{: #net-conn-full-linux-sub}

With this use case, you can establish a network between a virtual machine in the pod and the Red Hat Satellite server on IBM Cloud. The virtual machine has the stock image of Red Hat Enterprise Linux (RHEL) with full Linux subscription.

Connect the virtual machine in the pod to a proxy network in the corporate network environment. Connect the proxy network to the Red Hat Satellite server on IBM Cloud by using either Direct Link or VPN connection. The virtual machine in the pod can access the Linux&reg; satellite server to retrieve software fixes and other artifacts.

The network connectivity for full Linux subscription can be established by providing the network requirements before the installation of the pod. For more information, see [Network requirement](/docs/power-iaas?topic=power-iaas-pre_installation_checklist#network-req). Once the pod is installed, you can configure the network connectivity for full Linux subscription by using the Support Center ticketing system. For more information about full Linux subscription, see [Full Linux subscription for Power Virtual Server Private Cloud](/docs/power-iaas?topic=power-iaas-full-linux-sub). For more information about contacting the Support Center, see [Getting support](https://cloud.ibm.com/docs/get-support?topic=get-support-using-avatar&interface=ui){: external} section.

Figure 6 describes the network connectivity between a virtual machine and a Red Hat Satellite server on IBM Cloud setup.

![Network connectivity for full Linux subscription](./figures/net-conn-full-linux-sub.png "Network connectivity for full Linux subscription"){: caption="Network connectivity for full Linux subscription" caption-side="bottom"}
