---

copyright:
  years: 2023, 2024

lastupdated: "2025-07-17"

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
