---

copyright:
  years: 2023

lastupdated: "2023-03-28"

keywords: planning, site-readiness, {{site.data.keyword.powerSys_notm}} as a service, private cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Site access requirements
{: #site-access-requirements}

[Private Cloud]{: tag-red}

Site planners can use this information to assess the physical site and operational requirements that are necessary to prepare your site for new {{site.data.keyword.powerSysFull}} racks. Work with the IBM representative to ensure that these prerequisites are complete before the pods are delivered to your data center.

Review the following requirements that your private cloud site must fulfill:
* Accommodate a fully configured 42U rack that is 7 ft tall.
* Provide secured and controlled access to the {{site.data.keyword.powerSys_notm}} racks in your private cloud site.
* Provide the flooring that supports the weight of the {{site.data.keyword.powerSys_notm}} racks.

Refer Table 1 to understand rack dimensions and weight.

| Rack  |  Width             |  Depth  |  Height |  Weight(Empty)  |
| -----  | ------------------ | -------| -------|  -------------- |
| Rack only  | 600 mm (23.6 in.) | 1070 mm (42.1 in.) | 2020 mm (79.5 in.) | 166 kg (365 lb) |
| Rack with two standard doors     |  600 mm (23.6 in.) | 1132 mm (44.6 in)  |  2020 mm (79.5 in.) | 177 kg (391 lb) |
| Rack with rear door, heat exchanger (dry), and standard doors |  600 mm (23.6 in.) | 1231 mm (48.5 in.) |  2020 mm (79.5 in.) | 210 kg (463 lb) |
| Rack with high-end appearance front door and rear door        |  600 mm (23.6 in.) | 1210 mm (47.3 in.) |  2020 mm (79.5 in.) | 181 kg (398 lb) |
{: caption="Table 1. Rack dimensions and weight" caption-side="bottom"}


Refer Table 2 to understand rack characteristics and capacity.

| Characteristics   | Maximum weight    | EIA unit capacity             |
| ------------------| ----------------- | ----------------------------- |
| Dynamic (rolling) | 1134 kg (2500 lb) | 18 kg (40 lb) or EIA average  |
| Static            | 1678 kg (3700 lb) | 32 kg (70 lb) or EIA average  |
| Seismic certified | 1170 mm (2580 lb) | 20 kg (45 lb) or EIA maximum  |
| EIA: Energy Information Administration |
{: caption="Table 2. Rack characteristics and capacity" caption-side="bottom"}


**Floor load calculator**: You can use [Floor load calculator](http://www-01.ibm.com/support/knowledgecenter/v1/content/POWER6/iphdl/floorloadcalc.htm){: external} to determine the distributed load that a server, expansion unit, or migration tower places on a subfloor (for example, in a data center with a raised floor) or on an above-ground or nonraised floor structure.

For generic prerequisites and planning guidelines for Power10 processor-based systems, see the following topics:

* [Site preparation and physical planning](https://www.ibm.com/docs/en/power10/9080-HEX?topic=e1080-planning-system){: external}
* [IBM Power as Rack Specification](https://www.ibm.com/docs/en/power10/9080-HEX?topic=rack-model-7965-s42-specifications){: external}
