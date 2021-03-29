---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-10"

keywords: identity, access management, iam, managing virtual servers, platform access roles, user access scenarios

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Managing Power Systems Virtual Servers (IAM)
{: #managing-resources-and-users}

Identity and access management (IAM) enables you to securely authenticate users, control access to {{site.data.keyword.powerSysShort}} resources with resource groups, and allow access to specific resources for a set of users with access groups. IAM is your one-stop shop for all user and resource management in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

You can assign IAM authorizations based on the following criteria:

- Individual users
- Access groups
- Specific types of resources
- Resource groups

For more information about IAM, review the following information:

- [Getting started with IAM](/docs/iam?topic=iam-getstarted#getstarted)
- [Managing resource groups](/docs/resources?topic=resources-rgs)
- [Setting up access groups](/docs/iam?topic=iam-groups)
- [IAM concepts](/docs/iam?topic=iam-iamoverview)

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on {{site.data.keyword.cloud_notm}} resources, such as creating users or adding services.

The following table displays the IAM platform access roles and the corresponding type of control that is allowed by {{site.data.keyword.powerSys_notm}}:

| Platform access role | Type of access allowed                                                                                  |
| -------------------- | ------------------------------------------------------------------------------------------------------- |
| Viewer               | View instances and list instances.                                                                      |
| Operator             | View instances and list instances.                                                                      |
| Editor               | View instances, list instances, create instances, and delete instances.                                 |
| Administrator        | View instances, list instances, create instances, delete instances, and assign policies to other users. |

## Service access roles
{: #service-access-roles}

You can use the service access roles to define what users can do with {{site.data.keyword.powerSys_notm}} service functions. The following table displays the IAM service access roles and the corresponding actions a user can complete with {{site.data.keyword.powerSys_notm}}:

| Service access role | Description of actions |
|-----------|-------------------------|
| Reader | View all resources (such as SSH keys, storage volumes, and network settings). You cannot make any changes to the resources. |
| Manager | You can configure all resources. The following are some of the actions you can perform:<ul><li>Create instances</li><li>Increase storage volume sizes</li><li>Create SSH keys</li><li>Modify network settings</li><li>Create boot images</li><li>Delete storage volumes</li>
</ul>

## User access scenarios
{: #user-access-scenarios}

See [Managing access to resources](/docs/account?topic=account-assign-access-resources) for information on how to manage or assign access by using IAM policies.
