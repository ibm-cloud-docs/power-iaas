---

copyright:
  years: 2025

lastupdated: "2025-11-24"

keywords: cloud carbon calculator, carbon calculator, carbon emission, greenhouse gas

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}




# Using carbon calculator on {{site.data.keyword.powerSys_notm}}
{: #carbon-cal}





---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}





---

You can use the IBM Cloud&reg; carbon calculator to view and export carbon emission data on {{site.data.keyword.powerSys_notm}}. The carbon calculator is a dashboard to track, analyze, and manage greenhouse gas (GHG) emissions that is associated with your IBM Cloud services. Carbon emission data is available for IBM Power10 or later systems. To view and export GHG emissions data for an account, you must have account owner, administrator, or viewer level access on the billing service.
{: shortdesc}








The IBM Cloud carbon calculator performs the following functions:

- Displays the GHG emission data for an account. The GHG emission data is classified based on total energy consumption by an account, region, location, or service.
- Reports the overall energy consumption of an account and the efficiency of data centers.
- Tracks the GHG emissions that are associated with an account.
- Identifies **hot-spots** such as services, locations, or resource groups that reports the highest emissions to mitigate the carbon footprint.



For more information about carbon calculator, see [Working with IBM Cloud's carbon calculator](https://cloud.ibm.com/docs/account?topic=account-what-is-cloud-calc){: external}.


## IBM Cloud and sustainability
{: #sustainability}

As organizations and users work together to achieve better outcomes for their business and for the environment, digital technologies are a growing source of GHG emissions. The four areas that are the main source for GHG emissions are: data centers, extensive data analytics, security, and internet usage. For more information about sustainability, see [IT sustainability beyond the data center](https://www.ibm.com/thought-leadership/institute-business-value/report/it-sustainability){: external}.






For more information about environmental, social, and governance (ESG) initiatives of IBM, see [IBM Releases 2023 Impact Report](https://newsroom.ibm.com/2023-04-11-IBM-Releases-2023-Impact-Report){: external}. For more information about how different geographical areas address sustainability challenges, see [The State of Sustainability 2024 report](https://www.ibm.com/think/insights/state-of-sustainability-geo-data){: external}.



## FAQs for carbon calculator on {{site.data.keyword.powerSys_notm}}
{: #faq-ccc}

### What is GHG emission?
{: ghg}
{: #faq-ccc}

GHG emission stands for greenhouse gas emission. For more information, see [Carbon calculator terminology](https://cloud.ibm.com/docs/account?topic=account-carbon-calc-terms){: external} and [What are greenhouse gas (GHG) emissions?](https://www.ibm.com/think/topics/greenhouse-gas-emissions){: external}.




### How is GHG measured in IBM Cloud?
{: ghg-how}
{: #faq-ccc}








You can use the IBM Cloud carbon calculator for a detailed view of your cloud GHG emissions. For more information, see [FAQ for IBM Cloud Carbon Calculator](https://cloud.ibm.com/docs/account?topic=account-carboncalcfaqs){: external}.



### What methodology does IBM Cloud carbon calculator use?
{: ghg-what-meth}
{: #faq-ccc}






IBM Cloud carbon calculator uses a calculation methodology that conforms to the GHG protocol. For more information, see [IBM Cloud carbon calculator methodology](https://cloud.ibm.com/docs/account?topic=account-what-is-cloud-calc#carbon-methodology){: external}.




### Who can view the carbon calculator data?
{: ghg-who}
{: #faq-ccc}

To view and export GHG emissions data for an account, you must have account owner, administrator, or viewer level access on the billing service. You must be an account holder or have a billing administrator role to grant access to other users to the billing service. For more information, see [FAQ for IBM Cloud Carbon Calculator](https://cloud.ibm.com/docs/account?topic=account-carboncalcfaqs){: external}.


### How to view the Power Virtual Server GHG emissions data on carbon calculator?
{: ghg-how-id}
{: #faq-ccc}

On the [IBM Cloud carbon calculator](https://cloud.ibm.com/billing/carbon-calculator) GUI, select the **Power Virtual Server** option from the **Filter by server** list.



For {{site.data.keyword.powerSys_notm}}, GHG emissions are not distinguished for individual services. It is a combined report of GHG emissions for workloads that run on {{site.data.keyword.powerSys_notm}} instances (VSIs).

You can create a resource group and add the {{site.data.keyword.powerSys_notm}} VSIs for a specific workload to the resource group. View the **Emissions by resource group** widget on the carbon calculator GUI to view the carbon emissions for the resource group that you created. For more information about creating a resource group, see [Managing resource groups](https://cloud.ibm.com/docs/account?topic=account-rgs&interface=ui){: external}.






### Why no data is displayed in the carbon calculator?
{: ghg-why}
{: #faq-ccc}

The data for your workspace is not displayed in the carbon calculator or you are not be able to see the data for your workspace because of the following reasons:

- Only the data from your workspaces on IBM Power10 or later systems is used to calculate the carbon emissions. If your workspace is on IBM Power9 or previous generations, the carbon emissions data is not available.

- You must have the required permissions or roles to view the data on the carbon calculator. For more information about assigning access, see [Assigning access to account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=api#billing-acct-mgmt-api){: external}.

- If you run workloads in a zero emission data center, emissions that are calculated by using the market-based methodology are set to zero and no data is displayed. To view emissions that are calculated by using the location-based methodology, check the **Display unadjusted emissions** checkbox on the [IBM Cloud carbon calculator](https://cloud.ibm.com/billing/carbon-calculator) dashboard. For more information about the market-based and location-based methodology, see [Market-based and location-based methodology](https://cloud.ibm.com/docs/account?topic=account-what-is-cloud-calc#market-location-methodology){: external}.








### How to view and export GHG emissions for an account in the carbon calculator?
{: ghg-howtrack}
{: #faq-ccc}

To view and export GHG emissions data for an account, you must have account owner, administrator, or viewer level access on the billing service. For more information, see [Tracking account emissions with carbon calculator](https://cloud.ibm.com/docs/account?topic=account-tracking-emissions-account){: external}.


### How to extract GHG emissions data by using API?
{: ghg-howextract}
{: #faq-ccc}

You can use APIs related to the carbon calculator to extract GHG emissions data. For more information, see [Carbon Calculator API](https://cloud.ibm.com/apidocs/carbon-calculator){: external}.
