---

copyright:
  years: 2019, 2026 

lastupdated: "2026-09-29"

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

IAM enables you to securely authenticate users, control access to {{site.data.keyword.powerSysShort}} resources with resource groups, and allow access to specific resources for a set of users with access groups. IAM is the central service for all user and resource management in {{site.data.keyword.cloud_notm}}.
{: shortdesc}




[{{site.data.keyword.on-prem}}]{: tag-red} To display the **Infrastructure capacity** navigation menu for the {{site.data.keyword.on-prem-fname}} when you use a custom role with the `power-iaas.pod-capacity.view` IAM action, ensure that you assign a viewer role in the IAM Access Management service.
{: important}



For more information about IAM, review the following information:

- [Getting started with IAM](/docs/iam?topic=iam-iamoverview)
- [Managing resource groups](/docs/account?topic=account-rgs&interface=ui)
- [Streamlined access management with access groups](/docs/iam?topic=iam-groups&interface=ui)
- [IAM access concepts](/docs/iam?topic=iam-access-management-overview)

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on {{site.data.keyword.cloud_notm}} resources, such as creating users or adding services.

The following table lists the IAM platform access roles and the type of access that each role allows in {{site.data.keyword.powerSys_notm}}:

| Platform access role | Type of access allowed                                                                                                      |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Viewer               | View instances and list instances.                                                                                          |
| Operator             | View instances and manage aliases, bindings ({{site.data.keyword.on-prem-fname}} in client location only), and credentials. |
| Editor               | View instances, list instances, create instances, and delete instances.                                                     |
| Administrator        | View instances, list instances, create instances, delete instances, and assign policies to other users.                     |
{: caption="IAM platform access roles" caption-side="bottom"}

## Service access roles
{: #service-access-roles}

You can use service access roles to define the actions that the users can perform on {{site.data.keyword.powerSys_notm}} resources. The following table lists the IAM service access roles and the corresponding actions that a user can complete in {{site.data.keyword.powerSys_notm}}:

| Service access role | Description of actions                                                                                                                                                                                                               |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Reader              | View all resources, such as SSH keys, storage volumes, and network settings. You cannot modify the resources.                                                                                                                       |
| Manager             | Configure all resources. You can perform the following actions: \n * Create instances \n * Increase storage volume sizes \n * Create SSH keys \n * Modify network settings \n * Create boot images \n * Delete storage volumes |
{: caption="IAM service access roles" caption-side="bottom"}

To see the complete list of actions for each specific role, see the [IAM roles and actions](/docs/iam?topic=iam-iam-service-roles-actions#power-iaas-roles) page in IBM Cloud documentation.



### Resources supported for {{site.data.keyword.powerSys_notm}} IAM access policies
{: #res-supported}

When you assign access to the {{site.data.keyword.powerSys_notm}} service, you can scope access to any of the following resources:
- All resources
- Specific resources, which support the following selections:
    - Resource group
    - Service instance



Access management tags are supported only on {{site.data.keyword.powerSys_notm}} workspaces. The {{site.data.keyword.powerSys_notm}} service ignores the access management tags that are attached to the individual resources in a workspace.



Although you can select a **Resource type** from the **Attribute type** list, {{site.data.keyword.powerSys_notm}} does not support this attribute. Any roles and actions that are assigned to **Resource type** are ignored.
{: note}





## Access role requirements for {{site.data.keyword.powerSys_notm}}
{: #access-roles-requirement}

{{site.data.keyword.powerSys_notm}} requires extra access for features such as Direct Link, Transit Gateway service, and Virtual Private Cloud. You might need this extra access depending on your resource requirements. For example, to create a Cloud connection, you need access to the Direct Link service.

The following table lists the additional access roles that are required for each type of service that {{site.data.keyword.powerSys_notm}} supports:

| Additional access role                                | Resources attributes                                             |
| ----------------------------------------------------- | ---------------------------------------------------------------- |
| Editor, Manager, Operator, Reader, Viewer             | {{site.data.keyword.powerSys_notm}} service                      |
| Editor, Manager, Operator, Reader, Viewer, VPN Client | VPC Infrastructure Services service                              |
| Editor, Operator, Viewer                              | Transit Gateway service                                          |
| Reader, Viewer                                        | All resources in account (Including future IAM enabled services) |
| Editor, Operator, Viewer                              | Direct Link service                                              |
| Viewer                                                | All resource groups                                               |
| Viewer                                                | Satellite service [{{site.data.keyword.on-prem}}]{: tag-red}     |
{: caption="Additional access roles" caption-side="bottom"}

## User access scenarios
{: #user-access-scenarios}

For more information about managing and assigning access by using IAM policies, see [Managing access to resources](/docs/iam?topic=iam-iamusermanpol){: external}.



## Trusted profiles for {{site.data.keyword.powerSys_notm}}
{: #trusted-profiles}

A trusted profile is an IAM identity for a compute resource. IBM Cloud IAM trusts your {{site.data.keyword.powerSys_notm}} VSI as a compute resource, which allows the VSI to call the API endpoints of other IBM Cloud services without storing API keys or credentials on the instance.
{: shortdesc}


### Benefits of using trusted profiles
{: #trusted-profiles-benefits}

Trusted profiles provide the following security benefits for {{site.data.keyword.powerSys_notm}}:

- **Enhanced security**: Eliminates the risk of credential exposure by removing the need to store API keys or passwords on your VSIs.
- **Simplified credential management**: Eliminates the need to rotate, update, or manage static credentials across your VSIs.
- **Dynamic authentication**: Applications in the guest OS can generate tokens on demand based on the VSI identity. Because tokens are short-lived, access credentials are always current and tied to the specific instance.
- **Reduced attack surface**: Prevents compromised VSIs from exposing long-lived credentials to access other resources.
- **Precise access control**: Controls which IBM Cloud services each VSI can access through IAM policies and access groups that are assigned at the individual VSI level.

### Managing trusted profiles
{: #trusted-profiles-management}

You manage trusted profiles through IBM Identity and Access Management (IAM). You can create, configure, and manage trusted profiles from the [IBM Cloud Trusted Profiles UI](https://cloud.ibm.com/iam/trusted-profiles){: external}. You can associate each profile with one or more {{site.data.keyword.powerSys_notm}} VSIs and assign access policies to control which IBM Cloud services and resources the VSIs can access.

### Creating a trusted profile for {{site.data.keyword.powerSys_notm}}
{: #trusted-profiles-create}

To use trusted profiles with your {{site.data.keyword.powerSys_notm}} VSIs, you must create a trusted profile in IAM. You can configure rule-based policies for the VSIs or specify an individual VSI that can use a trusted profile.

For more information about creating and managing a trusted profile, see [Establishing trust with Power Virtual Server compute resources by using the console](/docs/iam?topic=iam-create-trusted-profile&interface=ui#create-profile-powervs){: external}.
