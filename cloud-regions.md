---

copyright:
  years: 2023, 2025

lastupdated: "2025-08-06"

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










| Location      | VPC Region | {{site.data.keyword.powerSys_notm}} region | VPC Zone                                 | {{site.data.keyword.powerSys_notm}} zone                                    | Classic infrastructure    |
| ------------- | ---------- | ------------------------------------------ | ---------------------------------------- | --------------------------------------------------------------------------- | ------------------------- |
| Dallas        | us-south   | us-south                                   | us-south-1  \n us-south-2  \n us-south-3 | dal10  \n dal12  \n us-south  \n dal14 | dal10  \n dal12  \n dal13 |
| Sao Paulo     | br-sao     | sao                                        | br-sao-1  \n br-sao-2  \n br-sao-3       | sao01  \n sao04  \n x                                                       | sao01  \n sao04  \n sao05     |
| Toronto       | ca-tor     | tor, mon                                   | ca-tor-1  \n ca-tor-2  \n ca-tor-3       | tor01 [^2]  \n mon01  \n x                                                  | tor01  \n mon01  \n x     |
| Washington DC | us-east    | us-east                                    | us-east-1  \n us-east-2  \n us-east-3    | us-east  \n wdc06  \n wdc07                                                 | wdc04  \n wdc06  \n wdc07 |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="{{site.data.keyword.powerSys_notm}} regions and zones in Americas" caption-side="top"}
{: #Americas}
{: tab-title="Americas"}

[^2]: This is a single data center for the location.


| Location  | VPC Region | {{site.data.keyword.powerSys_notm}} region | VPC Zone                        | {{site.data.keyword.powerSys_notm}} zone | Classic infrastructure |
| --------- | ---------- | ------------------------------------------ | ------------------------------- | ---------------------------------------- | ---------------------- |
| Frankfurt | eu-de      | eu-de                                      | eu-de-1  \n eu-de-2  \n eu-de-3 | x  \n eu-de-1  \n eu-de-2                | x  \n fra04  \n fra05  |
| London    | eu-gb      | lon                                        | eu-gb-1  \n eu-gb-2  \n eu-gb-3 | lon04  \n x  \n lon06                    | lon04  \n x  \n lon06  |
| Madrid    | eu-es      | mad                                        | eu-es-1  \n eu-es-2  \n eu-es-3 | mad02  \n mad04  \n x                    | mad02  \n mad04  \n x  |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="{{site.data.keyword.powerSys_notm}} regions and zones in Europe" caption-side="top"}
{: #europe}
{: tab-title="Europe"}



| Location | VPC Region | {{site.data.keyword.powerSys_notm}} region | VPC Zone                           | {{site.data.keyword.powerSys_notm}} zone | Classic infrastructure |
| -------- | ---------- | ------------------------------------------ | ---------------------------------- | ---------------------------------------- | ---------------------- |
| Sydney   | au-syd     | syd                                        | au-syd-1  \n au-syd-2  \n au-syd-3 | x  \n syd04  \n syd05                    | x  \n syd04  \n syd05  |
| Tokyo    | jp-tok     | tok                                        | jp-tok-1  \n jp-tok-2  \n jp-tok-3 | x  \n tok04  \n x                        | x  \n tok04  \n x      |
| Osaka    | jp-osa     | osa                                        | jp-osa-1  \n jp-osa-2  \n jp-osa-3 | osa21  \n x  \n x                        | osa21  \n x  \n x      |
| Chennai  | x          | in-che          | x                                  | che01 [^5]                               | che01                  |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="{{site.data.keyword.powerSys_notm}} regions and zones in Asia Pacific" caption-side="top"}
{: #asia-pacific}
{: tab-title="Asia Pacific"}

**x - Not available**

[^5]: This is a single data center for the location.










{{_include-segments/workspace-note.md}}
