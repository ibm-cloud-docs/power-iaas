---

copyright:
  years: 2023, 2024

lastupdated: "2024-07-26"

keywords: preinstallation, checklist, preinstallation checklist, preorder, site-readiness, {{site.data.keyword.powerSys_notm}} as a service, private cloud, network validation, account activation

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Prerequisites for installing the pod
{: #pre_installation_checklist}

---

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

---

Proper planning is essential for the successful setup and use of {{site.data.keyword.powerSysFull}} pods. It ensures that you have everything you need and that you meet all the prerequisites for your pod.
{: shortdesc}

IBM owns the responsibility to install, upgrade, and update the hardware and software for the pod infrastructure. IBM coordinates with you for any dependencies to ensure that your IBM {{site.data.keyword.powerSys_notm}} (On-premises) data center meets all the prerequisites before the pod installation.

IBM provides a pre-installation checklist after you place an order for IBM {{site.data.keyword.powerSys_notm}} (On-premises) and also during the pre-installation stage. You must complete the items in the pre-installation checklist to prepare your IBM {{site.data.keyword.powerSys_notm}} (On-premises) environment for the pod installation. An IBM representative conducts an installation readiness review to ensure that you understand the prerequisites.

## Preorder checklist
{: #pre-order-check}

Before you place the order, you must confirm if the following criteria to install the pod in your data center are met:
*  Identify an IBM Cloud region closest to the physical location of your data center where the pod resides. The network latency between your data center and the selected IBM Cloud region that will run the control plane must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Network latency](/docs/power-iaas?topic=power-iaas-network_latency_main).
*  Confirm that the site and environment requirements to place the pod are met. For more information, see [Site-planning and environmental requirements](/docs/power-iaas?topic=power-iaas-pre_installation_checklist#site-plan-env-req).

## {{site.data.keyword.powerSys_notm}} requirements
{: #power-sys-req}

Before you connect to the IBM Cloud, create a workspace, or perform other pre-installation activities, you must complete the following tasks or keep the following information in hand:
*  You must have an active IBM Cloud account ID. To create an IBM Cloud account ID, see [Setting up your IBM Cloud account](https://cloud.ibm.com/docs/account?topic=account-account-getting-started){: external}.
*  Create a Satellite location associated with an IBM Cloud region. Select the IBM Cloud region that is closest to the physical location of your data center. The network latency between your data center and the selected IBM Cloud region must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Create a Satellite location overview](https://cloud.ibm.com/docs/satellite?topic=satellite-locations){: external}.

## Site-planning and environmental requirements
{: #site-plan-env-req}

Before you place the order, you must prepare your data center site to meet the following site and environmental requirements:
*  The data center can accommodate all the 42U racks in a pod. For example, a small pod contains one 42U rack and a medium pod might contain two or four 42U racks.
*  The floor of the data center is able to withstand the weight of the racks and other equipment. For more information about rack dimensions and weight, see [Site access requirements](/docs/power-iaas?topic=power-iaas-site-access-requirements).
*  Ensure heating, ventilation, and air conditioning (HVAC) setup for front-to-back airflow and humidity control is ready. For more information, see [Environmental requirements](/docs/power-iaas?topic=power-iaas-environmental-requirements).
*  The data center site meets the power source requirements for rack connector and load requirements. For more information, see [Power requirements](/docs/power-iaas?topic=power-iaas-power-requirements).
*  The data center is in a secured location with restricted access. For more information, see [Site readiness](/docs/power-iaas?topic=power-iaas-site-readiness).

The following data center site requirements must be met before the pod is delivered to your data center:
*  Ensure that the IBM site reliability engineering (SRE) operations team has the security and access approval to operationally manage the pod infrastructure.
*  Ensure that the power cables and network cables are routed to the location where the pod will be installed. The power cables must have connectors that are compatible with rack PDU. For more information, see [Supported PDU power cord](https://www.ibm.com/docs/en/power9/0009-ESS?topic=pr-supported-pdu-power-cords){: external}.
*  Identify a network administrator and hire a service provider who can participate in establishing the connections to IBM Direct Link connection or VPN connection and to provide last mile connectivity.

## Networking requirements
{: #network-req}

The following network requirements must be completed before the pod is delivered to your data center:
*  After the order is placed, IBM provides a pre-installation checklist. Complete the pre-installation checklist to provide network-specific information, such as Autonomous system numbers (ASN), Service key, and others. For more information, see [Network requirements](/docs/power-iaas?topic=power-iaas-network-requirements).
*  Review and identify the available network use cases and communicate your requirements to IBM before you proceed with installation. For more information, see [Network use cases](/docs/power-iaas?topic=power-iaas-network_use_cases).

## Network validation and account activation
{: #validation-activation}

You must complete the following steps to validate the network functions and to activate the IBM {{site.data.keyword.powerSys_notm}} (On-premises) account:

* After the physical cabling is completed, provide the initial configuration to set up the data plane network to the IBM site reliability engineering (SREs) team.
* The SRE team configures the network for network validation testing.
    The network validation testing ensures the functionality of the control plane network.
* The SRE team conducts provisioning testing over the control plane by simulating a user request from the IBM Cloud.
    To complete the remaining network connectivity after the installation of the pod, you can contact IBM Support Center through the ticketing system. For more information, see [Getting Support](https://cloud.ibm.com/docs/get-support?topic=get-support-using-avatar&interface=ui){: external}.
* After testing is complete, the SRE team activates the account specifying the period from when the billing starts.
* The SRE team works with you to ensure the visibility of the pod Satellite location in your IBM {{site.data.keyword.powerSys_notm}} (On-premises) account.
* Perform a provisioning test by using the service broker. The provisioning test is successful if the following statements are true:
    * A virtual machine is successfully provisioned.
    * The virtual machine has an IP address that is assigned to it.
    * You can log on to the virtual machine and can run basic commands to inspect the environment settings, such as check memory, CPU, and storage capacity.
