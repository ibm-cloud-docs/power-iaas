---

copyright:
  years: 2019, 2026 

lastupdated: "2026-06-24"

keywords: identity, access management, iam, managing virtual servers, platform access roles, user access scenarios

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing identity and access management (IAM) for {{site.data.keyword.powerSysFull}}s
{: #managing-resources-and-users}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

IAM enables you to securely authenticate users, control access to {{site.data.keyword.powerSysShort}} resources with resource groups, and allow access to specific resources for a set of users with access groups. IAM is your one-stop shop for all user and resource management in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}




[{{site.data.keyword.on-prem}}]{: tag-red} To display the **Infrastructure capacity** navigation menu for the {{site.data.keyword.on-prem-fname}} when you use a custom role with the `power-iaas.pod-capacity.view` IAM action, ensure that you have a `Viewer` role that is assigned in the IAM Access Management service.
{: important}



For more information about IAM, review the following information:

- [Getting started with IAM](/docs/iam?topic=iam-iamoverview)
- [Managing resource groups](/docs/account?topic=account-rgs&interface=ui)
- [Streamlined access management with access groups](/docs/iam?topic=iam-groups&interface=ui)
- [IAM access concepts](/docs/iam?topic=iam-access-management-overview)

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on {{site.data.keyword.cloud_notm}} resources, such as creating users or adding services.

The following table displays the IAM platform access roles and the corresponding type of control that is allowed by the {{site.data.keyword.powerSys_notm}}:

| Platform access role | Type of access allowed                                                                                  |
| -------------------- | ------------------------------------------------------------------------------------------------------- |
| Viewer               | View instances and list instances.                                                                      |
| Operator             | View instances and manage aliases, bindings ({{site.data.keyword.on-prem-fname}} in client location only), and credentials.                     |
| Editor               | View instances, list instances, create instances, and delete instances.                                 |
| Administrator        | View instances, list instances, create instances, delete instances, and assign policies to other users. |
{: caption="IAM platform access roles" caption-side="bottom"}

## Service access roles
{: #service-access-roles}

You can use the service access roles to define the actions that the users can perform on {{site.data.keyword.powerSys_notm}} resources. The following table displays the IAM service access roles and the corresponding actions that a user can complete by using the {{site.data.keyword.powerSys_notm}}:

| Service access role | Description of actions |
|-----------|-------------------------|
| Reader | View all resources (such as SSH keys, storage volumes, and network settings). You cannot modify the resources. |
| Manager | Configure all resources. You can perform the following actions:  \n * Create instances  \n * Increase storage volume sizes  \n * Create SSH keys  \n * Modify network settings  \n * Create boot images  \n * Delete storage volumes |
{: caption="IAM service access roles" caption-side="bottom"}

To see the complete list of actions for each specific role, see the [IAM roles and actions](/docs/iam?topic=iam-iam-service-roles-actions#power-iaas-roles) page in IBM Cloud documentation.

### Resources supported for {{site.data.keyword.powerSys_notm}} IAM access policies
{: #res-supported}

When you assign access to the {{site.data.keyword.powerSys_notm}} service, you can scope access to any of the following resources:
- All resources
- Specific resources, which support the following selections:
    - Resource group
    - Service instance



The access management tags are supported only on {{site.data.keyword.powerSys_notm}} workspaces. The {{site.data.keyword.powerSys_notm}} service ignores the access management tags that are attached to the individual resources in a workspace.



Although you can select a **Resource type** from the **Attribute type** list, it is not supported. Any roles and actions that are assigned to the **Resource type** are ignored.
{: note}


## Access role requirements for {{site.data.keyword.powerSys_notm}}
{: #access-roles-requirement}

{{site.data.keyword.powerSys_notm}} requires extra access for features such as Direct Link, Transit Gateway service, and Virtual Private Cloud. You might require these extra access based on your resource requirements. For example, to create a Cloud connection, you need `access`to the Direct Link service.

The following table displays the additional access roles that are required for the corresponding type of services that are allowed by {{site.data.keyword.powerSys_notm}}:

| Additional access role | Resources Attributes                                                                                  |
| ---------------------- | ----------------------------------------------------------------------------------------------------- |
| Editor, Manager, Operator, Reader, Viewer               | {{site.data.keyword.powerSys_notm}} service                          |
| Editor, Manager, Operator, Reader, Viewer, VPN Client   | VPC Infrastructure Services service                                  |
| Editor, Operator, Viewer                                | Transit Gateway service                                              |
| Reader, Viewer                                          | All resources in account (Including future IAM enabled services)     |
| Editor, Operator, Viewer                                | Direct Link service                                                  |
| Viewer                                                  | All resource group                                                   |
| Viewer                                                  | Satellite service [{{site.data.keyword.on-prem}}]{: tag-red}                           |
{: caption="Additional access roles" caption-side="bottom"}

## User access scenarios
{: #user-access-scenarios}

For more information about managing and assigning access by using IAM policies, see [Managing access to resources](/docs/iam?topic=iam-iamusermanpoll).



## Understanding trusted profiles for {{site.data.keyword.powerSys_notm}}
{: #trusted-profiles}

A trusted profile is a security mechanism that eliminates the need to store static secrets, such as IBM Cloud API keys, in potentially vulnerable environments like virtual server instances (VSIs). An {{site.data.keyword.cloud_notm}} instance is trusted by IBM Cloud IAM as a type of compute resource. As a result, trusted profiles can be used to grant {{site.data.keyword.powerSys_notm}} VSIs secure access to call other service API endpoints without storing credentials within the instance.
{: shortdesc}


### Benefits of using trusted profiles
{: #trusted-profiles-benefits}

Using trusted profiles with {{site.data.keyword.powerSys_notm}} provides several security and operational advantages:

Enhanced security
:   Eliminates the risk of credential exposure by removing the need to store API keys or passwords on your VSIs.

Simplified credential management
:   Eliminates the need to rotate, update, or manage static credentials across your VSI fleet.

Dynamic authentication
:   Applications in the guest OS can generate tokens on demand based on the VSI identity, ensuring that access is always current and tied to the specific instance.

Reduced attack surface
:   Without stored credentials, compromised VSIs cannot expose long-lived secrets that can be used to access other resources.

Granular access control
:   You can assign specific access rights to individual VSIs through IAM policies and access groups.

### Managing trusted profiles
{: #trusted-profiles-management}

You manage trusted profiles through IBM Identity and Access Management (IAM). You can create, configure, and manage trusted profiles from the [IBM Cloud Trusted Profiles UI](https://cloud.ibm.com/iam/trusted-profiles){: external}. You can associate each profile with one or more {{site.data.keyword.powerSys_notm}} VSIs, and you can assign access policies to control which IBM Cloud services and resources the VSIs can access.

### Creating a trusted profile for {{site.data.keyword.powerSys_notm}}
{: #trusted-profiles-create}

To use trusted profiles with your {{site.data.keyword.powerSys_notm}} VSIs, you must first create a trusted profile in IAM. You can configure rule-based policies for the VSIs or specify an individual VSI that can use a trusted profile. All configuration is done from within an individual trusted profile.

For more information about creating and managing a trusted profile, see [Establishing trust with compute resources in the console](/docs/iam?topic=iam-create-trusted-profile&interface=ui#create-profile-compute){: external}.
