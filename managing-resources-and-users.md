---

copyright:
  years: 2019, 2022

lastupdated: "2022-09-15"

keywords: identity, access management, iam, managing virtual servers, platform access roles, user access scenarios

subcollection: power-iaas

---


{{site.data.keyword.attribute-definition-list}}

# Managing IBM {{site.data.keyword.powerSys_notm}} (IAM)
{: #managing-resources-and-users}

Identity and Access Management (IAM) enables you to securely authenticate users, control access to {{site.data.keyword.powerSysFull}} resources with resource groups, and allow access to specific resources for a set of users with access groups. IAM is your one-stop shop for all user and resource management in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

<!--You can assign IAM authorizations based on the following criteria:

- Individual users
- Access groups
- Specific types of resources
- Resource groups-->

For more information about IAM, review the following information:

- [Getting started with IAM](/docs/account?topic=account-access-getstarted)
- [Managing resource groups](/docs/account?topic=account-rgs)
- [Setting up access groups](/docs/account?topic=account-groups)
- [IAM concepts](/docs/account?topic=account-iamoverview)


## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on {{site.data.keyword.cloud_notm}} resources, such as creating users.

The following table displays the IAM platform access roles and the corresponding type of control that is allowed by {{site.data.keyword.powerSys_notm}}:

| Platform access role | Type of access allowed                                                                                  |
| -------------------- | ------------------------------------------------------------------------------------------------------- |
| Viewer               | View and list instances.                                                                      |
| Operator             | View instances and manage aliases, bindings (private cloud only), and credentials.          |
| Editor               | View, list, create, and delete instances.                                 |
| Administrator        | View, list, create, and delete instances as well as assign policies to other users. |
{: caption="Table 1. IAM platform access roles" caption-side="bottom"}

## Service access roles
{: #service-access-roles}

You can use the service access roles to define what actions users can perform on {{site.data.keyword.powerSys_notm}} resources. The following table displays the IAM service access roles and the corresponding actions a user can perform on {{site.data.keyword.powerSys_notm}}:

| Service access role | Description of actions |
|-----------|-------------------------|
| Reader | View all resources (such as SSH keys, storage volumes, and network settings). You cannot make any changes to the resources. |
| Manager | You can configure all resources. The following are some of the actions you can perform on {{site.data.keyword.powerSys_notm}}: \n * Create instances \n * Increase storage volume sizes \n * Create SSH keys \n * Modify network settings \n * Create boot images \n * Delete storage volumes |
{: caption="Table 2. IAM service access roles" caption-side="bottom"}

[Private Cloud]{: tag-red}
To view the storage pool and system pool capacities of your private cloud location that is satellite-enabled, you must have the privileges associated with a `Manager`-type service access role.
{: note}

To see the complete list of actions for each specific role, see the [Manage authorizations](https://cloud.ibm.com/iam/authorizations){: external} page in IBM Cloud.

### Resources supported for IAM access policies on {{site.data.keyword.powerSys_notm}}
{: #res-supported}

When you assign access to the {{site.data.keyword.powerSys_notm}} service, you can set the scope of the access policy to any of the following resources:

* All resources
* Specific resources, which supports the following selections:
    * Resource group
    * Service instance

    You can select a **Resource type** option from the **Attribute type** drop-down list but it is not supported. Any roles and actions that are assigned to the **Resource type** option are ignored.
    {: note}


## Access roles requirements for {{site.data.keyword.powerSys_notm}}
{: #access-roles-requirement}

{{site.data.keyword.powerSys_notm}} requires additional access for features such as Direct Link, Transit Gateway service, Virtual Private Cloud, and so on. You may require additional access based on your resource requirements. For example, to create a Cloud connection you will need an Editor access to Direct Link service.

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

See [Managing access to resources](https://cloud.ibm.com/docs/account?topic=account-assign-access-resources&interface=ui){: external} for information on how to manage or assign access by using IAM policies.
