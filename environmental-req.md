---

copyright:
  years: 2023, 2024


lastupdated: "2024-06-06"

keywords: planning, site-readiness, {{site.data.keyword.powerSys_notm}}, private cloud, environment, environmental requirement

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Environmental requirements
{: #environmental-requirements}

[On-premises]{: tag-red}

Your {{site.data.keyword.powerSysFull}} Private Cloud site must have adequate cooling and humidity control for {{site.data.keyword.powerSysFull}} racks. To know the recommended and allowed values of the required parameters, see Table 1:

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
|-------------------| ------------------------- | ------------------------- |
| Allowable environment (nonoperating) (5)                       | | |
|-------------------| ------------------------- | -------------------------  |
| Temperature       | 5°C - 45°C (41°F - 113°F) |  |
| Relative humidity | 8% to 85% |  |
| Maximum dew point | 27.0°C (80.6°F) |  |
{: caption="Table 1. Recommended and allowed environmental parameter values" caption-side="bottom"}

To set up the operating environment, IBM suggests using the recommended values from Table 1. Over prolonged use, this operating environment becomes reliable and energy-efficient.

To set up a short-term operating environment, you can use the allowable values from Table 1. In an operating system, if you are using the allowable values for the required parameters, use an equipment that is functionally tested.

When allowable values for the required parameters in the operating environment are used for continuous operation, it can overload the equipment.
{: attention}

If you want to use any allowable configurations of ASHRAE A3 to operate at the maximum limits, contact IBM Support.
{: note}

If altitude of the IBM {{site.data.keyword.powerSys_notm}} Private Cloud site exceeds by 900 m (2953 ft), derate the maximum allowable temperature by 1°C (1.8°F) for every 175 m (574 ft). The maximum allowable elevation is 3050 m (10000 ft).

To set the minimum and maximum humidity levels, see the following guidelines:
*  The minimum humidity level is the maximum absolute humidity of the -12°C (10.4°F) dew point and 8% relative humidity. These levels intersect at approximately 25°C (77°F). Based on the temperature, set the minimum humidity level as follows:
   -  If the temperature is less than 25°C (77°F), the dew point (-12°C) represents the minimum humidity level.
   -  If the temperature is greater than 25°C (77°F), the relative humidity (8%) represents the minimum humidity level.
*  The maximum humidity level is the minimum absolute humidity of the -12°C (10.4°F) dew point and 8% relative humidity.

The following minimum requirements apply to data centers that are operated at a low relative humidity:
*  Data centers that lack electrostatic discharge (ESD) floors and permit the use of non-ESD shoes might consider increasing humidity levels. This action is required because the risk of generating 8 kV increases slightly at 8% relative humidity, when compared to 25% relative humidity.
*  All mobile furnishings and equipment must be made of conductive or static dissipative materials and must be bonded to the ground.
*  The maintenance personnel must wear a wrist strap when coming into contact with information technology (IT) equipment during hardware maintenance. The wrist strap must be properly functioning and grounded.

Before installation, the equipment is in the powered-down state when it is removed from the container. The allowable nonoperating environment is provided to define the environmental range that an unpowered system can experience for a short time without sustaining damage.

For more information, see Table 1 - 5 in [Environmental design criteria](https://www.ibm.com/docs/en/power10/9080-HEX?topic=planning-environmental-design-criteria){: external}.
