---

copyright:
  years: 2023


lastupdated: "2023-03-28"

keywords: planning, site-readiness, {{site.data.keyword.powerSys_notm}}, private cloud, power requirement, power

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Power requirements
{: #power-requirements}

[On-Premises]{: tag-red}

Your {{site.data.keyword.powerSysFull}} Private Cloud site must be provisioned with with A-side and B side power redundancy that meets the {{site.data.keyword.powerSys_notm}} rack connector and load requirements. Table 1 shows the rack connector and load requirements.

Be sure to read all caution and danger statements provided in the Safety notices before you perform the procedures. For more information about safety notices containing the the caution and danger information, see [Safety notices](/docs/power-iaas?topic=power-iaas-safety-notices). Read any additional safety information that comes with your system or optional device before you install the device.


| Corresponding PDU| Rack line cord feature code | Wall plug      | Rated voltage (V AC) line to line | Phase   | Rated amperage | Location |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| ECJJ (C19) and ECJN (C13) | #6492 | IEC 60309, 2P+G, 60 A  | 200 - 240 V |   1   | 48 A          | US, Canada, Latin America(LA), and Japan |
|         | #6491 | IEC 60309, P+N+G, 63 A | 230 V           |   1   | 63 A          | EMEA |
|         | #6489 | IEC 60309, 3P+N+G, 32 A | 380 – 415 V    |   3 Wye   | 32 A per phase | Europe, Middle East, and Asia (EMEA) |
|         | #6667 | PDL                 | 380 – 415 V      |   3 Wye   | 32 A per phase | Australia and New Zealand |
|         | #6653 | IEC 60309, 3P+N+G   | 380 - 415 V    | 3 Wye | 16 A per phase     | Switzerland |
|         | #ELC2 | IEC 60309, 3P+N+G, 30 A | 380 - 415 V   | 3 Wye | 30 A (derated to 24 A) per phase | United States, Canada, Mexico, and Japan (European Style Power for US type countries) |
| ECJL (C19) and ECJQ (C13) | #ECJ6 | CS8365C | 200 - 240 V | 3 Delta | 50 A or line (40 A derated) | United States, Canada |
|         | #ECJ7 | IEC 60309, 3P+G | 200 - 240 V | 3 Delta | 60 A or line (48 A derated) | United States, Canada, Latin America, and Japan |
{: caption="Table 1. Rack connectors with load capacity requirements" caption-side="bottom"}


<!--Table 2 shows the single-phase rack power requirements.

| Specification                           | North America                                        | EMEA |
| Input normal voltage                    | 200 - 208, 240 V ac                                        | 220 - 240 V ac |
| Frequency                               | 50 or 60 Hz plus or minus 3 Hz                       | 50 or 60 Hz plus or minus 3 Hz |
| Line load current                       | 60 A plug (48 A derated) \n #6492                             | 63A  \n #6491|
| Power connection (from the PDU of the rack) | IEC 60309 2P+E (60 A plug (48 A derated)) \n **(IBM 6491)** | IEC 60309, P+N+G \n **(IBM 6492)** |
| PDUs/Power Circuits                     | Four to six (two to three redundant pairs)                           | Four to six (two to three redundant pairs) |
| Power requirement at site               | * Four to six single-phase circuits \n * Each rack requires four to six drops. | * Four or six single-phase circuits \n * Each rack requires four or six drops. |
| Power cord length                       | 14 ft                                                 | 4.3 m |-->


<!--{: caption="Table 2. Single-phase rack power requirements" caption-side="bottom"}-->


<!--Table 3 shows the three-phase rack power requirements.

| Specification                           | North America                                        | EMEA |
| Input normal voltage  (line-to-line)                    | 200 - 208, 240 V ac                                        | 380 - 415 V ac |
| Frequency                               | 50 or 60 Hz plus or minus 3 Hz                       | 50 or 60 Hz plus or minus 3 Hz |
| Line load current                       | 50 or 60 A (three-phase delta) \n #ECJ6 or #ECJ7 \n 30A (three-phase wye) \n #ELC2                                                  | 16A \n #6653 \n 32A \n #6489 or #6667 |
| Power connection (from the PDU of the rack) | IEC 60309 3P+G (60 A plug (48 A derated)) \n **(IBM  (ECJ7/EPTP/EPTL))** | IEC 60309, 3P+N+G \n **(IBM 6489)** |
| PDUs/Power Circuits                     | Four or six (two redundant pairs)                           | Four or six (two redundant pairs) |
| Power requirement at site               | * Four or six single-phase circuits.   \n * Each rack requires four or six drops. | * Four or six single-phase circuits.   \n  * Each rack requires four or six drops. |
| Power cord length                       | 14 ft                                                 | 4.3 m |-->


<!--{: caption="Table 3. Three-phase rack power requirements" caption-side="bottom"}-->



Table 2 shows the number of PDUs and the corresponding power cords that are required for different configurations.

If you have selected the configuration with 4 PDUs, you can include 6 power drops in the facility plan to increase the number of PDUs in future.
{: note}

| Rack type | PDU feature codes | Number of PDUs | Number of Power S1022 servers | Number of Power E1050 servers | Number of Power S1022 and E1050 servers | Number of Power E1080 servers \n (no mixing) |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| ESMP (Small) | ECNJ or ECJQ** \n (Default) | 4 | 8 x S1022 (includes management server)  | N/A   | N/A | N/A  |
|   |  | 6 | 3 extra S1022 |  (C19 PDUs are required) | N/A |  N/A |
|   |  ECJJ or ECJL** | 4  | 1 (management server)  | 3  | N/A | N/A |
|   |   |  6  | 2 x S1022 which is equivalent to 1 MRX. (optional) |  5 | 2 x S1022 which is equivalent to 1 MRX. | N/A |
| EMPD + 4651 or 4652 \n (Medium rack 1 or 2) | ECJJ or ECJL** | 4  | 6  | 3  | 2 x S1022 which is equivalent to 1 MRX. | 1x2 enclosures |
|   |   | 6 | 8 |  4 | 2 x S1022 which is equivalent to 1 MRX. | N/A |
| EMPD + 4653 or 54 \n (Medium rack 1 or 2) |  | 4  | 8  | 3  | N/A | 1x2 enclosures  |
|  |  | 6 |  12 |  4 | N/A |  2x2 enclosures |
{: caption="Table 2. PDUs and power drops requirements" caption-side="bottom"}

** You can place an order for ECJJ or ECJL PDUs only if there is an order with ER3E identifier (specifies 9043-MRX) or EN31 identifier (specifies 4983-AH8).
{: note}

For more information about IBM power cords, see [Supported PDU power cord](https://www.ibm.com/docs/en/power9/0009-ESS?topic=pr-supported-pdu-power-cords){: external}.


**Power calculators**: The [IBM Systems energy estimator](https://see.c8f8f055.public.multi-containers.ibm.com){: external} is a web-based tool for estimating power requirements for IBM systems. This tool estimates typical power requirements (watts) for a specific system configuration under normal operating conditions.
