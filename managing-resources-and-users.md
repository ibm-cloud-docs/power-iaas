---

copyright:
  years: 2019, 2023

lastupdated: "2022-11-27"

keywords: identity, access management, iam, managing virtual servers, platform access roles, user access scenarios

subcollection: power-iaas

---


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

- [Getting started with IAM](/docs/account?topic=account-access-getstarted)
- [Managing resource groups](/docs/account?topic=account-rgs)
- [Setting up access groups](/docs/account?topic=account-groups)
- [IAM concepts](/docs/account?topic=account-iamoverview)

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
{: caption="Table 1. IAM platform access roles" caption-side="bottom"}

## Service access roles
{: #service-access-roles}

You can use the service access roles to define what users can do with {{site.data.keyword.powerSys_notm}} functions. The following table displays the IAM service access roles and the corresponding actions a user can complete with {{site.data.keyword.powerSys_notm}}:

| Service access role | Description of actions |
|-----------|-------------------------|
| Reader | View all resources (such as SSH keys, storage volumes, and network settings). You cannot make any changes to the resources. |
| Manager | You can configure all resources. The following are some of the actions you can perform: \n * Create instances \n * Increase storage volume sizes \n * Create SSH keys \n * Modify network settings \n * Create boot images \n * Delete storage volumes |
{: caption="Table 2. IAM service access roles" caption-side="bottom"}

To see the complete list of actions for each specific role, see the [Manage authorizations](https://cloud.ibm.com/iam/authorizations){: external} page in IBM Cloud.

## Access roles requirements for Power System Virtual Server
{: #access-roles-requirement}

{{site.data.keyword.powerSys_notm}} requires additional access for features such as Direct Link, Transit Gateway service, Virtual Private Cloud, and so on. You may require additional access based on your resource requirements. For example, to create a Cloud connection you will need Editor access to Direct Link service.

The following table displays the additional access roles required for the corresponding type of services that is allowed by {{site.data.keyword.powerSys_notm}}:

| Additional access role | Resources Attributes                                                                                  |
| ---------------------- | ----------------------------------------------------------------------------------------------------- |
| Editor, Manager, Operator, Reader, Viewer               | {{site.data.keyword.powerSys_notm}} service                          |
| Editor, Manager, Operator, Reader, Viewer, VPN Client   | VPC Infrastructure Services service                                  |
| Editor, Operator, Viewer                                | Transit Gateway service                                              |
| Reader, Viewer                                          | All resources in account (Including future IAM enabled services)                    |
| Editor, Operator, Viewer                                | Direct Link service                                                  |
| Viewer                                                  | All resource group                                                   |
{: caption="Table 3. Additional access roles" caption-side="bottom"}
## User access scenarios
{: #user-access-scenarios}

See [Managing access to resources](/docs/iam?topic=iam-iammanidaccser) for information on how to manage or assign access by using IAM policies.