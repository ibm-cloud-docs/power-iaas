---

copyright:
  years: 2025

lastupdated: "2025-09-22"

keywords: cloud carbon calculator, carbon calculator, carbon emission, greenhouse gas

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Using carbon calculator with {{site.data.keyword.powerSys_notm}}
{: #carbon-cal}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}





---

The IBM Cloud&reg; carbon calculator is a dashboard to track, analyze, and manage greenhouse gas (GHG) emissions that is associated with your IBM Cloud services. Carbon emission data is available on IBM Power10 or later systems. To view and export GHG emissions data for an account, you must be able to access the billing service for that account. To access the billing service, you must be the account owner, account administrator, a user with a viewer role, or a user with higher permissions.
{: shortdesc}

A carbon calculator can perform the following functions:
- Display the GHG emission data for an account.
- Monitor the electricity consumption for services, resources, and the location and efficiency of your data centers.
- Track the GHG emissions that are associated with your account to manage and mitigate your carbon footprint over time.

For more information about carbon calculator, see [Working with IBM Cloud's carbon calculator](https://cloud.ibm.com/docs/account?topic=account-what-is-cloud-calc){: external}.


## IBM Cloud and sustainability
{: #sustainability}

As organizations and users work together to achieve better outcomes for their business and for the environment, digital technologies are a growing source of GHG emissions. The four areas that are the main source for GHG emissions are: data centers, extensive data analytics, security, and internet usage. For more information about sustainability, see [IT sustainability beyond the data center](https://www.ibm.com/thought-leadership/institute-business-value/report/it-sustainability){: external}.

For more information about environmental, social, and governance (ESG) initiatives, see [IBM Releases 2023 Impact Report](https://newsroom.ibm.com/2023-04-11-IBM-Releases-2023-Impact-Report){: external}. For more information about how different geographical areas address sustainability challenges, see [The State of Sustainability 2024 report](https://www.ibm.com/think/insights/state-of-sustainability-geo-data){: external}.


## FAQs about carbon calculator
{: #faq-ccc}

### What is GHG?
{: ghg}
{: #faq-ccc}

GHG is a gaseous substance that has a warming effect on the Earth when released to the atmosphere. For more information, see [FAQ for IBM Cloud Carbon Calculator](https://cloud.ibm.com/docs/account?topic=account-carboncalcfaqs){: external}.

### How is GHG measured in IBM Cloud?
{: ghg-how}
{: #faq-ccc}

IBM Cloud plays a critical role in achieving IBM’s energy conservation, renewable electricity procurement, and GHG emissions reduction targets. IBM Cloud is improving the estimation approach by introducing the carbon calculator, which gives you a detailed view of your cloud electricity consumption and associated GHG emissions. For more information, see [FAQ for IBM Cloud Carbon Calculator](https://cloud.ibm.com/docs/account?topic=account-carboncalcfaqs){: external}.


### What methodology does IBM Cloud carbon calculator use?
{: ghg-what-meth}
{: #faq-ccc}

IBM Cloud carbon calculator uses data from electricity consumption, measurement of the usage of server resources, server and process lifecycle events, and service usage data. Based on the data, the tool estimates the electricity consumption and GHG emission from each account and service offerings, according to the location, time period, and resource groups. For more information, see [FAQ for IBM Cloud Carbon Calculator](https://cloud.ibm.com/docs/account?topic=account-carboncalcfaqs){: external}.


### Who can view the carbon calculator data?
{: ghg-who}
{: #faq-ccc}

To view and export GHG emissions data for an account, you must be able to access the billing service for that account. To access the billing service, you must be the account owner, account administrator, a user with a viewer role, or a user with higher permissions. You must have an account or have a billing administrator role to grant other users access to the billing service. For more information, see [FAQ for IBM Cloud Carbon Calculator](https://cloud.ibm.com/docs/account?topic=account-carboncalcfaqs){: external}.


### How to view the Power Virtual Server GHG emissions data on carbon calculator?
{: ghg-how-id}
{: #faq-ccc}

On the [IBM Cloud carbon calculator](https://cloud.ibm.com/billing/carbon-calculator) GUI, select the **Power Virtual Server** option from the **Filter by server** list.


### Why is the data for my workspace not displayed in the carbon calculator?
{: ghg-why}
{: #faq-ccc}

The data for your workspace is not displayed in the carbon calculator or you are not be able to see the data for your workspace because of the following reasons:
- Only the data from your workspaces on IBM Power10 or later systems is used to calculate the carbon emissions. If your workspace is on IBM Power9 or previous generations, the carbon emissions data is not available.
- You must have the required permissions or roles to view the data on the carbon calculator. For more information about assigning access, see [Assigning access to account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=api#billing-acct-mgmt-api){: external}.
- The Power Usage Effectiveness (PUE) and Carbon Efficiency Factor (CEF) for your workspace location is set to zero. For more information about PUE and CEF, see [Energy and carbon quantification methodology](https://cloud.ibm.com/media/docs/downloads/account/carbon-calc-method-v4.pdf){: external}.


### How to view and export GHG emissions for an account in the carbon calculator?
{: ghg-howtrack}
{: #faq-ccc}

To view and export GHG emissions data for an account, you must be able to access the billing service for that account. To access the billing service, you must be the account owner, account administrator, a user with a viewer role, or a user with higher permissions. For more information, see [Tracking account emissions with carbon calculator](https://cloud.ibm.com/docs/account?topic=account-tracking-emissions-account){: external}.


### How to extract GHG emissions data by using API?
{: ghg-howextract}
{: #faq-ccc}

You can use APIs to extract GHG emissions data. For more information, see [Carbon Calculator API](https://cloud.ibm.com/apidocs/carbon-calculator){: external}.
