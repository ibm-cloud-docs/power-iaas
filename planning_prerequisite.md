---

copyright:
  years: 2023, 2024

lastupdated: "2024-06-07"

keywords: planning, prerequisites, environment, site access, site requirement, power, power requirement, network, network requirement, system calculator, site-readiness, {{site.data.keyword.powerSys_notm}}, private cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Planning and prerequisites
{: #planning_prerequisite}

[On-premises]{: tag-red}

Proper planning is essential for the successful setup and use of your IBM {{site.data.keyword.powerSys_notm}} Private Cloud pods. It ensures that you have everything you need and that you meet all the prerequisites for your pod.
{: shortdesc}

IBM owns the responsibility to install, upgrade, and update the hardware and software for the pod infrastructure. However, IBM coordinates with you for any dependencies and to ensure that your IBM {{site.data.keyword.powerSys_notm}} Private Cloud data center meets all the prerequisites before the pod installation.

IBM provides a checklist during the pre-installation stage so that your IBM {{site.data.keyword.powerSys_notm}} Private Cloud environment is ready for the pod installation and other associated activities. An IBM representative conducts the installation readiness review to ensure that you understand the prerequisites clearly.

Review the following guidelines to prepare your data center for the {{site.data.keyword.powerSys_notm}}.

## Site access requirements
{: #site-access-requirements}

Site planners can use this information to assess the physical site and operational requirements that are necessary to prepare your site for new IBM {{site.data.keyword.powerSys_notm}} racks. Work with the IBM representative to ensure that these prerequisites are completed before the pods are delivered to your data center. The information in this document includes specifications for servers and expansion units, plugs and receptacles, cables, power-distribution units, and uninterruptible power supplies.

Review the following requirements that your IBM {{site.data.keyword.powerSys_notm}} Private Cloud site must fulfill:
* Accommodate a fully configured 42U rack that is 7 ft tall
* Provide secured and controlled access to the {{site.data.keyword.powerSys_notm}} racks in your IBM {{site.data.keyword.powerSys_notm}} Private Cloud site
* Provide the flooring that supports the weight of the {{site.data.keyword.powerSys_notm}} racks.

Refer the following tables for rack dimensions and weight details:

| Rack  |  Width             |  Depth  |  Height |  Weight(Empty)  |
| -----  | ------------------ | -------| -------|  -------------- |
| Rack only  | 600 mm (23.6 in.) | 1070 mm (42.1 in.) | 2020 mm (79.5 in.) | 166 kg (365 lb) |
| Rack with two standard doors     |  600 mm (23.6 in.) | 1132 mm (44.6 in)  |  2020 mm (79.5 in.) | 177 kg (391 lb) |
| Rack with rear door, heat exchanger (dry), and standard doors |  600 mm (23.6 in.) | 1231 mm (48.5 in.) |  2020 mm (79.5 in.) | 210 kg (463 lb) |
| Rack with high-end appearance front door and rear door        |  600 mm (23.6 in.) | 1210 mm (47.3 in.) |  2020 mm (79.5 in.) | 181 kg (398 lb) |
{: caption="Table 1. Rack dimensions and weight" caption-side="bottom"}


| Characteristics   | Maximum weight    | EIA unit capacity             |
| ------------------| ----------------- | ----------------------------- |
| Dynamic (rolling) | 1134 kg (2500 lb) | 18 kg (40 lb) or EIA average  |
| Static            | 1678 kg (3700 lb) | 32 kg (70 lb) or EIA average  |
| Seismic certified | 1170 mm (2580 lb) | 20 kg (45 lb) or EIA maximum  |
| EIA: Energy Information Administration |
{: caption="Table 2. Rack characteristics and capacity" caption-side="bottom"}


For generic prerequisites and planning guidelines for Power10 processor-based systems, see the following topics:

* [Site preparation and physical planning](https://www.ibm.com/docs/en/power10/9080-HEX?topic=e1080-planning-system){: external}
* [IBM Power as Rack Specification](https://www.ibm.com/docs/en/power10/9080-HEX?topic=rack-model-7965-s42-specifications){: external}

## Environmental requirements
{: #environmental-requirements}

Your IBM {{site.data.keyword.powerSys_notm}} Private Cloud site must have adequate cooling and humidity control for {{site.data.keyword.powerSys_notm}} racks. See the following table for recommended and allowed values of the required parameters:

| Environment (operating) (1)                                           | | |
|---------------------------------------------------------------------- | --- | --- |
| Properties        | Recommended    | Allowable (2,3,4)   |
| ------------------| -------------- | ------------------- |
| ASHRAE class      |                | A3 (Fourth edition) |
| Airflow direction | Front-to-back  |                     |
| Temperature       | 18.0°C – 27.0°C (64.4°F – 80.6°F) | 5.0°C – 40.0°C (41.0°F – 104.0°F) |
| Low-end moisture  | -9.0°C (15.8°F) dew point | -12.0°C (10.4°F) dew point and 8% relative humidity|
| High-end moisture | 60% relative humidity and 15°C (59°F) dew point | 85% relative humidity and 24.0°C (75.2°F) dew point |
| Maximum altitude  |                           | 3050 m (10,000 ft) |
| Allowable environment (nonoperating) (5) |
| Temperature       | 5°C - 45°C (41°F - 113°F) |  |
| Relative humidity | 8% to 85% |  |
| Maximum dew point | 27.0°C (80.6°F) |  |
{: caption="Table 3. Recommended and allowed environmental parameter values" caption-side="bottom"}

IBM recommended operating environment is a long-term operating environment that can result in the greatest reliability and energy efficiency. The allowable operating environment represents the environment in which the equipment is tested to verify its functions. Due to the stresses that operating in the allowable envelope can place on the equipment, these envelopes must be used for short-term operation, not continuous operation. A few configurations must not operate at the maximum limits of the ASHRAE A3 allowable range. Consult your IBM technical specialist for additional information.

If altitude of the IBM {{site.data.keyword.powerSys_notm}} Private Cloud site exceeds by 900 m (2,953 ft), derate the maximum allowable temperature by 1°C (1.8°F) for every 175 m (574 ft). The maximum allowable elevation is 3,050 m (10,000 ft).

Refer to the following considerations to set the minimum and maximum humidity levels:
*  The minimum humidity level is the maximum absolute humidity of the -12°C (10.4°F) dew point and 8% relative humidity. These levels intersect at approximately 25°C (77°F). Based on the temperature, set the minimum humidity level:
   -  if the temperature is less than 25°C (77°F), the dew point (-12°C) represents the minimum humidity level.
   -  if the temperature is greater than 25°C (77°F), the relative humidity (8%) represents the minimum humidity level.
*  The maximum humidity level is the minimum absolute humidity of the -12°C (10.4°F) dew point and 8% relative humidity.

The following minimum requirements apply to data centers that are operated at low relative humidity:
*  Data centers that do not have ESD floors and where people are allowed to wear non-ESD shoes might consider increasing humidity. This action is required because the risk of generating 8 kV increases slightly at 8% relative humidity, when compared to 25% relative humidity.
*  All mobile furnishings and equipment must be made of conductive or static dissipative materials and be bonded to the ground.
*  During maintenance of any hardware, if the maintenance personnel are coming in contact with information technology (IT) equipment, they must wear a wrist strap that is properly functioning and grounded.

Before installation, the equipment is in the powered down state when it is removed from the container. The allowable nonoperating environment is provided to define the environmental range that an unpowered system can experience for a short time without being damaged.

For more information, see Table 1 - 5 in [Environmental design criteria](https://www.ibm.com/docs/en/power10/9080-HEX?topic=planning-environmental-design-criteria){: external}.

## Power requirements
{: #power-requirements}

Your IBM {{site.data.keyword.powerSys_notm}} Private Cloud site must be provisioned with dual power cords that meets the PowerVS rack connector and load requirements. See the following table for rack connector and load requirements:


| Rack Line Cord Feature Code | Wall plug      | Rated voltage (V AC) | Phase   | Rated amperage | Geography |
| -- | -- | -- | -- | -- | -- |
| #6492 | IEC 309, 2P+G,60 A  | 200 - 208, 240 |   1   | 48 amps          | US, Canada, Latin America(LA), and Japan |
| #6491 | IEC 309,P+N+G, 63 A | 230            |   1   | 63 amps          | EMEA |
| #6657 | PDL                 | 230-240        |   1   | 32 amps          | Australia and New Zealand |
| #6658 | Korean Plug         | 220            |   1   | 30 amps          | North and South Korea |
| #6489 | IEC309,3P+N+G, 32 A | 230            |   3   | 32 amps perphase | Europe, Middle East, and Asia, (EMEA) |
| #6667 | PDL                 | 380 - 415      |   3   | 32 amps perphase | Australia and New Zealand |
{: caption="Table 4. Rack connectors with load capacity requirements" caption-side="bottom"}


See the following table for the single-phase rack power requirements:

| Specification                           | North America                                        | EMEA |
| -- | -- | -- |
| Input normal voltage                    | 200 - 208 V ac                                        | 220 - 240 V ac |
| Frequency                               | 50 or 60 Hz plus or minus 3 Hz                       | 50 or 60 Hz plus or minus 3 Hz |
| Line load current                       | 60 A plug (48 A derated)                             | 63A |
| Power connection (from the rack's PDUs) | IEC 60309 2P+E (60 A plug (48 A derated)) \n **(IBM 6491)** | IEC 309, P+N+G \n **(IBM 6492)** |
| PDUs/Power Circuits                     | Four (two redundant pairs)                           | Four (two redundant pairs) |
| Power requirement at site               | * Four single-phase circuits \n * Each rack requires four drops. | |
| Power cord length                       | 14 ft                                                 | 4.3 m |
{: caption="Table 5. Single-phase rack power requirements" caption-side="bottom"}


See the following table for the three-phase rack power requirements:

| Specification                           | North America                                        | EMEA |
| -- | -- | -- |
| Input normal voltage                    | 200 - 208 V ac                                        | 415 V ac |
| Frequency                               | 50 or 60 Hz plus or minus 3 Hz                       | 50 or 60 Hz plus or minus 3 Hz |
| Line load current                       | 60 A                                                 | 32A |
| Power connection (from the rack's PDUs) | IEC 309 3P+G (60 A plug (48 A derated)) \n **(IBM (ECJ7/EPTP/EPTL))** | IEC 309, 3P+N+G \n **(IBM 6489)** |
| PDUs/Power Circuits                     | Four (two redundant pairs)                           | Four (two redundant pairs) |
| Power requirement at site               | * Four single-phase circuits.   \n * Each rack requires four drops. | |
| Power cord length                       | 14 ft                                                 | 4.3 m |
{: caption="Table 6. Three-phase rack power requirements" caption-side="bottom"}

For more information about IBM power cord, see [Supported PDU power cord](https://www.ibm.com/docs/en/power9/0009-ESS?topic=pr-supported-pdu-power-cords){: external}.

## IBM Cloud specific requirements
{: #ibm-cloud-specific-requirements}

Keep the following cloud-specific requirements ready:
* An active IBM Cloud account ID
        You can create an IBM Cloud account or use an existing account ID. For more information, see [Setting up your IBM Cloud account](https://cloud.ibm.com/docs/account?topic=account-account-getting-started&mhsrc=ibmsearch_a&mhq=IBM+cloud+account&_gl=1*1s6v863*_ga*NzQ0MjA1OTk5LjE2ODkxODA1Njk.*_ga_FYECCCS21D*MTY4OTU3NDAwNC44LjEuMTY4OTU3NDQ4Ni4wLjAuMA..){: external}.
* A Satellite Location ID for each {{site.data.keyword.powerSys_notm}} infrastructure deployment
        A Satellite location is a representation of an environment in your infrastructure provider, such as an IBM {{site.data.keyword.powerSys_notm}} Private Cloud data center or cloud. You must select an IBM Cloud region that is closest to the physical location of the data center where the pod will be installed. For more information, see [Creating a Satellite location](https://cloud.ibm.com/docs/satellite?topic=satellite-locations){: external}.
* A Satellite Connector for providing a secure connection between your Satellite location and IBM Cloud. For more information, see [Creating a Connector](https://cloud.ibm.com/docs/satellite?topic=satellite-create-connector){: external}
        **Note:** The default value of the Connector name is connector. However, while creating a Connector, specify a unique name such that the connector name represents your pod location. For example, if your pod is located in a data center in the Raleigh, North Carolina region, the name of the connector can be “Raleigh North Data Center pod”.
* A secure access for IBM specialists or operations team to remotely manage the {{site.data.keyword.powerSys_notm}} infrastructure from the IBM Cloud.

## Network requirements
{: #network-requirements}

Review the following network requirements to facilitate the pod infrastructure connectivity:
* The site must provide network cables to connect the IBM {{site.data.keyword.powerSys_notm}} Private Cloud network infrastructure and the data network at the site.
* Site must provide two uplink cables that to connect the IBM {{site.data.keyword.powerSys_notm}} Private Cloud network infrastructure to the IBM Cloud region through IBM Direct Link connections or through VPN connections.
* Hire a service provider to
    * Provide redundant connections to the IBM Direct Link connection or VPN connection
    * Provide the last mile connection from the point-of-presence (PoP) of your service provider to the customer data center  

For network architecture diagrams, see [Network architecture diagrams](/docs/power-iaas?topic=power-iaas-network_overview-on-premises&interface=api#netwok-architecture-diagrams){: external}.

Setting up of a network has two parts:
* [Control plane network](#control-plane-network) - for communication between IBM Cloud and the pod
* [Data plane network](#data-plane-network) - for accessing virtual servers

### Control plane network
{: #control-plane-network}

The IBM {{site.data.keyword.powerSys_notm}} Private Cloud network architecture requires connectivity between two entities, IBM Cloud and the pod that is located in your IBM {{site.data.keyword.powerSys_notm}} Private Cloud data center. This connectivity is the main communication channel and is known as a control plane network. For more information, see [Control plane network](/docs/power-iaas?topic=power-iaas-network_overview-on-premises&interface=api#control-plane-network){: external}.

Direct Link 2.0 Connect can be viewed as an alternative to a traditional site-to-site VPN solution that can provide security and privacy, consistent, and higher-throughput connectivity between a remote network and IBM Cloud environments. For more information about Direct Link Connect, see [Getting started with IBM Cloud Direct Link](https://cloud.ibm.com/docs/dl?topic=dl-get-started-with-ibm-cloud-dl){: external}

A VPN connection can be established by using one of the following methods:
* [Site-to-site VPN Connectivity](/docs/power-iaas?topic=power-iaas-network-private-cloud&interface=api#vpn)
* [Connectivity by using IBM Cloud classic environment](/docs/power-iaas?topic=power-iaas-network-private-cloud&interface=api#vpn)

Provide the required network-specific information before the pod installation so that either the Direct Link 2.0 connection or VPN connection can be established. For example,

* Autonomous system numbers (ASN)
* Service key
* IP addresses and gateway for the Aggregation Services Router (ASR)
* Network connectivity ports
* Firewall access and permission

### Data plane network
{: #data-plane-network}

The Data Plane Network is enabled when the pods in your data center are connected to your IBM {{site.data.keyword.powerSys_notm}} Private Cloud network infrastructure. Using this connectivity that you can access the virtual servers (logical partitions) in the pod through your network instead of IBM Cloud. As part of the network planning, you can review the [Network overview](/docs/power-iaas?topic=power-iaas-network-private-cloud) and available use cases in the [Network use cases](/docs/power-iaas?topic=power-iaas-network_use_cases) sections and identify the use cases that are applicable to you. You can communicate about such requirements before the installation so that you do not have to open separate support tickets to implement those use-cases and configuration.

## Site readiness
{: #site-readiness}

Determine whether a new site must be constructed or alterations to an existing site is to be made. The electric power and communication facilities must be available in the adequate quantities for operation. If these facilities are inadequate, contact the utility company to determine whether more services can be made available.

Ensure that the {{site.data.keyword.powerSys_notm}} pod is installed in a restricted access location. Only skilled and instructed persons with proper authorization must be able to access this area.

Refer [Site preparation and physical planning](https://www.ibm.com/docs/en/power10?topic=system-site-preparation-physical-planning){: external} for prerequisites and planning guidelines.

## Network planning
{: #network-planning}

The {{site.data.keyword.powerSys_notm}} network architecture requires connectivity between two entities: IBM Cloud and the pod that is located in your IBM {{site.data.keyword.powerSys_notm}} Private Cloud data center. This connectivity is enabled with the help of Direct Link 2.0 Connect technology or through VPN connection. IBM sets up this connectivity during the initial deployment of the pod. Provide some network-specific information before the pod installation so that the Direct Link 2.0 connection or VPN connection can be established. Information that is required by IBM is included in the checklist that is shared before the installation, such as:
* Autonomous system numbers (ASN)
* Service key
* IP addresses and gateway for the Aggregation Services Router (ASR)
* Network connectivity ports
* Firewall access and permission

As a part of the network planning, you can review the available use cases in the [Network use cases](/docs/power-iaas?topic=power-iaas-network_use_cases) section and identify the use cases that are applicable to you. You can communicate about such requirements before the installation so that you do not have to open separate support tickets to implement those use-cases and configuration.

## System calculators
{: #system-calculators}

You can use system calculators to determine the system power load or the distributed floor load for your system.
* **Power calculators**: The [IBM Systems energy estimator](https://see.c8f8f055.public.multi-containers.ibm.com/see/EnergyEstimator){: external} is a web-based tool for estimating power requirements for IBM systems. This tool estimates typical power requirements (watts) for a specific system configuration under normal operating conditions.
* **Floor load calculator**: Use [Floor load calculator](http://www-01.ibm.com/support/knowledgecenter/v1/content/POWER6/iphdl/floorloadcalc.htm){: external} to determine the distributed load that a server, expansion unit, or migration tower places on a subfloor (for example, in a data center with a raised floor) or on an above-ground or nonraised floor structure.
* **Workload estimator**: The [IBM Workload estimator](https://ibm.biz/workload-estimator){: external} is a web-based sizing tool for IBM systems. You can use this tool to size a new system to size an upgrade to an existing system, or to size a consolidation of several systems. For European power distributions that cannot support 30 amps single-phase, a 16 amps 3-Phase PDU power cord is substituted.
