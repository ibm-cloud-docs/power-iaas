---

copyright:
  years: 2023

lastupdated: "2023-04-27"

keywords: AIX and IBM i development, test, use case, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology, video, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# AIX and IBM i development and test
{: #use-case-dev-test}

IBM i is not supported for private cloud.
{: note}

{{site.data.keyword.powerSysFull}} is a great solution if you want to create a temporary sandbox environment to perform testing and as a step before you deploy production applications.
{: shortdesc}

For example:
    - You need a remote environment to test the software or hardware updates.
    - You need some system resources temporarily.
    - You need to evaluate, plan, and test next-generation hardware or operating system (OS) versions.
    - You want a temporary and isolated infrastructure for application testing.
    - You want to test hardware before a refresh.


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

- {{site.data.keyword.powerSysFull}}
- Direct Link Connect for optional connectivity into full {{site.data.keyword.cloud_notm}} or from  a private cloud environment
- VPN and Direct Link Dedicated for private cloud connectivity
- Cloud Object Storage for optional backup and custom image hosting or migration
