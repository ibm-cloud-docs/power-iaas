---

copyright:
  years: 2023, 2025

lastupdated: "2025-12-08"

keywords: power systems, cloud regions

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud&reg; regions
{: #ibm-cloud-reg}

---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---

The following table displays the appropriate region for your workspace:






The network round-trip latency, also known as round-trip time (RTT), is approximately 0.4 milliseconds when your workloads are running in Power Virtual Server and IBM Cloud Virtual Private Cloud (VPC), which are colocated in the same zone and connected through IBM Cloud Transit Gateway. RTT statistics might vary and are intended to help you plan the optimal placement of your cloud deployment.








| Location      | VPC region[^6] | {{site.data.keyword.powerSys_notm}} region | VPC zone                                 | {{site.data.keyword.powerSys_notm}} zone                                    | Classic infrastructure[^1]    |
| ------------- | ---------- | ------------------------------------------ | ---------------------------------------- | --------------------------------------------------------------------------- | ------------------------- |
| Dallas        | us-south   | us-south                                   | us-south-1  \n us-south-2  \n us-south-3 | dal10  \n dal12  \n us-south  \n dal14 | dal08[^9] \n dal09  \n dal10  \n dal12  \n dal13 \n dal14 |
| Montreal       | ca-mon     | mon                                   | x       |  mon01                                                  | mon01  |
| San Jose      | x          | x                                          | x                                        | x                                      | sjc03  \n sjc04     |
| Sao Paulo     | br-sao     | sao                                        | br-sao-1  \n br-sao-2  \n br-sao-3       | sao01  \n sao04  \n sao05                                                       | sao01  \n sao04  \n sao05     |
| Toronto       | ca-tor     | tor                                   | ca-tor-1  \n ca-tor-2  \n ca-tor-3       | tor01[^2]  \n tor04  \n tor05                                                   | tor01  \n tor04  \n tor05  |
| Washington DC | us-east    | us-east                                    | us-east-1  \n us-east-2  \n us-east-3    | us-east  \n wdc06  \n wdc07                                                 | wdc03[^9a]  \n wdc04  \n wdc06  \n wdc07 |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="{{site.data.keyword.powerSys_notm}} regions and zones in Americas" caption-side="top"}
{: #Americas}
{: tab-title="Americas"}

[^1]: For more information about the list of classic data centers in IBM Cloud, see [Classic data centers](/docs/overview?topic=overview-locations#data-centers){: external}.
[^2]: This is a single data center for the location.
[^6]: For more information about the IBM Cloud regions that support VPC, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region&interface=cli){: external}.
[^9]: IBM Cloud for government. [Learn more](https://www.ibm.com/cloud/government){: external}.
[^9a]: IBM Cloud for government. [Learn more](https://www.ibm.com/cloud/government){: external}.

| Location  | VPC region[^7] | {{site.data.keyword.powerSys_notm}} region | VPC zone                        | {{site.data.keyword.powerSys_notm}} zone | Classic infrastructure[^3] |
| --------- | ---------- | ------------------------------------------ | ------------------------------- | ---------------------------------------- | ---------------------- |
| Amsterdam | x          | x    | x    | x   | ams03  |
| Frankfurt | eu-de      | eu-de                                      | eu-de-1  \n eu-de-2  \n eu-de-3 | x  \n eu-de-1  \n eu-de-2                | fra02  \n fra04  \n fra05  |
| London    | eu-gb      | lon                                        | eu-gb-1  \n eu-gb-2  \n eu-gb-3 | lon04  \n x  \n lon06                    | lon02 \n lon04  \n lon05  \n lon06  |
| Madrid    | eu-es      | mad                                        | eu-es-1  \n eu-es-2  \n eu-es-3 | mad02  \n mad04  \n x                    | mad02  \n mad04  \n mad05  |
| Milan | x | x   | x   | x  | mil01  |
| Paris | x | x   | x   | x  | par01  |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="{{site.data.keyword.powerSys_notm}} regions and zones in Europe" caption-side="top"}
{: #europe}
{: tab-title="Europe"}

[^3]: For more information about the list of classic data centers in IBM Cloud, see [Classic data centers](/docs/overview?topic=overview-locations#data-centers){: external}.
[^7]: For more information about the IBM Cloud regions that support VPC, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region&interface=cli){: external}.



| Location | VPC region[^8] | {{site.data.keyword.powerSys_notm}} region | VPC zone                           | {{site.data.keyword.powerSys_notm}} zone | Classic infrastructure[^4] |
| -------- | ---------- | ------------------------------------------ | ---------------------------------- | ---------------------------------------- | ---------------------- |
| Chennai  | x          | in-che          | x                                  | che01 [^5]                               | che01                  |
| Osaka    | jp-osa     | osa                                        | jp-osa-1  \n jp-osa-2  \n jp-osa-3 | osa21  \n x  \n x                        | osa21  \n osa22  \n osa23      |
| Singapore | x | x   | x   | x  | sng01  |
| Sydney   | au-syd     | syd                                        | au-syd-1  \n au-syd-2  \n au-syd-3 | x  \n syd04  \n syd05                    | syd01  \n syd04  \n syd05  |
| Tokyo    | jp-tok     | tok                                        | jp-tok-1  \n jp-tok-2  \n jp-tok-3 | x  \n tok04  \n x                        | tok02  \n tok04  \n tok05      |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="{{site.data.keyword.powerSys_notm}} regions and zones in Asia Pacific" caption-side="top"}
{: #asia-pacific}
{: tab-title="Asia Pacific"}

**x - Not available**

[^4]: For more information about the list of classic data centers in IBM Cloud, see [Classic data centers](/docs/overview?topic=overview-locations#data-centers){: external}.

[^5]: This is a single data center for the location.
[^8]: For more information about the IBM Cloud regions that support VPC, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region&interface=cli){: external}.









{{_include-segments/workspace-note.md}}
