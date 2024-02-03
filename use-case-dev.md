---

copyright:
  years: 2019, 2020

lastupdated: "2019-04-10"

keywords: use case, client needs, solution components, hybrid cloud journey, sandbox environment

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# AIX and IBM i development and test
{: #use-case-dev-test}

The client wants to create a temporary sandbox environment to perform testing and as a step before they deploy production applications in the IBM {{site.data.keyword.powerSys_notm}}.
{: shortdesc}

## Client needs
{: #use-case-dev-needs}

- Requires a remote environment to test updates
- Temporary need for system resource resources (consumption model)
- Evaluate, plan, and test next-generation hardware or operating system (OS) versions

## Examples
{: #use-case-dev-examples}

- An initial step in the *Hybrid Cloud Journey*
- Testing complicated or large architecture changes without the need to procure the capital (for example, evaluating a scale-up E980 system deployment if the client's needs grow beyond scale-out image limits)
- Looking for a temporary and isolated infrastructure for application testing
- Wants to test hardware before a refresh

## Technical solution
{: #use-case-dev-solutions}

- IBM&reg; Power Systems&trade; Virtual Server
- Direct Link Connect for optional connectivity into full {{site.data.keyword.cloud_notm}} or from  an on-premises environment
- VPN and Direct Link Dedicated for on-premises connectivity
- Cloud Object Storage for optional backup and custom image hosting or migration
