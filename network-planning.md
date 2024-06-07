---

copyright:
  years: 2023


lastupdated: "2023-03-28"

keywords: planning, site-readiness, {{site.data.keyword.powerSys_notm}} as a service, private cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network planning
{: #network-planning}

[On-premises]{: tag-red}

The {{site.data.keyword.powerSys_notm}} network architecture requires connectivity between two entities: IBM Cloud and the pod that is located in your private cloud data center. This connectivity is enabled with the help of Direct Link 2.0 Connect technology or through VPN connection. IBM sets up this connectivity during the initial deployment of the pod. Provide some network-specific information before the pod installation so that the Direct Link 2.0 connection or VPN connection can be established. Information that is required by IBM is included in the checklist that is shared before the installation, such as:
* Autonomous system numbers (ASN)
* Service key
* IP addresses and gateway for the Aggregation Services Router (ASR)
* Network connectivity ports
* Firewall access and permission

As a part of the network planning, you can review the available use cases in the [Network use cases](/docs/power-iaas?topic=power-iaas-network_use_cases) section and identify the use cases that are applicable to you. You can communicate about such requirements before the installation so that you do not have to open separate support tickets to implement those use-cases and configuration.
