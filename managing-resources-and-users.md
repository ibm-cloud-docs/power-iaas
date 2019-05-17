---

copyright:
  years: 2019

lastupdated: "2019-05-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Managing {{site.data.keyword.powerSys_notm}} resources and users
{: #managing-resources-and-users}

The {{site.data.keyword.powerSysFull}} authorization and resource management practices coordinate with the IBM Cloud Identity and Access Management (IAM) services. IAM enables you to securely authenticate users, control access to {{site.data.keyword.powerSys_notm}} resources with resource groups, and allow access to specific resources for a set of users with access groups. In other words, IAM is your one stop shop for all user and resource management in {{site.data.keyword.cloud_notm}}.

For more information about IAM, review the following information:

* [IAM concepts](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [Getting started with IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [Managing resource groups](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [Setting up access groups](https://cloud.ibm.com/docs/iam?topic=iam-groups)

You can assign IAM authorizations based on the follow criteria:

* Individual users
* Access groups (groups of users)
* Specific types of resources
* Resource groups

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on {{site.data.keyword.cloud_notm}} resources, such as creating users or adding services.

The following table displays the IAM platform access roles and the corresponding type of control allowed by {{site.data.keyword.powerSys_notm}}:

| Platform access role | Type of access allowed |
|-----------|-------------------------|
| Viewer | View instances and list instances. |
| Operator | View instances and list instances. |
| Editor | View instances, list instances, create instances, and delete instances.  |
| Administrator | View instances, View instances, list instances, create instances, delete instances, and assign policies to other users. |

## Service access roles
{: #service-access-roles}

You can use the service access roles to define what users can specifically do with the functions for the {{site.data.keyword.powerSys_notm}} service.

The following table displays the IAM service access roles and the corresponding actions a users can complete with {{site.data.keyword.powerSys_notm}}:

| Service access role | Description of actions |
|-----------|-------------------------|
| Reader | View all resources, such as SSH keys, storage volumes, and network settings. You cannot make any changes to the resources. |
| Manager | You can configure all resources. The following are some of the actions you can perform:<ul><li>Create instances</li><li>Increase storage volume sizes</li><li>Create SSH keys</li><li>Modify network settings</li><li>Create boot images</li><li>Delete storage volumes</li>
</ul> |

## User access scenarios
{: #user-access-scenarios}

The following scenarios covers the basic steps that are required to add a new user and modify an existing user's permissions.

### Inviting a new user to view {{site.data.keyword.powerSys_notm}} resources
{: #inviting-a-new-user-to-create-or-manage-resources}

You must invite an IBM Cloud user to your account and give them access to view {{site.data.keyword.powerSys_notm}} resources. Remember, the service access role determines the access level that a user has for {{site.data.keyword.powerSys_notm}} resources.

Complete the following steps in IAM to enable a user to view {{site.data.keyword.powerSys_notm}} resources:

1. Navigate to the [IAM Users UI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/iam/users){: new_window} in the IBM Cloud Console, and click **Invite users**.

      ![Displays the invite users icon from the IAM UI](/images/invite_users.png "Invite users from the IAM UI")

1. On the **Invite users** page, in the **Users** section, enter the email addresses of the users that you want to invite in the **Email address** field.
1. In the **Services** section, select **Resources** from the **Assign access to** field.
1. From the **Services** field, select **{{site.data.keyword.powerSys_notm}}**.

    ![Displays the service fields](/images/invite_users2.png "Selecting the {{site.data.keyword.powerSys_notm}} service for a new user from the IAM UI")

1. Select the platform access role that you want to assign to the users. In this scenario, the user can only view {{site.data.keyword.cloud_notm}} and {{site.data.keyword.powerSys_notm}} resources.

    ![Displays the UI for IAM roles](/images/invite_users3.png "Selecting roles for a new user from the IAM UI")

1. Click **Invite users**. The user must accept the invite to be added to the if the invitation is sent successfully, a message is displayed.

    ![Displays message for successful invitation](/images/invite_users4.png "Successfully invitation message")

### Giving an existing user permission to manage {{site.data.keyword.powerSys_notm}} resources
{: #giving-an-existing-user-permission-to-manage-resources}

Complete the following steps to provide an existing user in your account permission to configure {{site.data.keyword.powerSys_notm}} resources.

1. Navigate to the [IAM Users UI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/iam/users){: new_window} in the IBM Cloud Console.
1. From the list of users, select the user whose authorization you want to change.
1. Click **Access policies** and click the current roles for the users. In this scenario, click **Viewer, Reader**.

    ![Displays how to change the permissions for an existing user](/images/existing_user1.png "Changing the permissions for a user from the IAM UI")

1. From the **Select Roles** field, click **Manager**. You can leave the **Reader** role selected.
    ![Displays adding the manager role for an existing user](/images/existing_user2.png "Selecting the manager role from the IAM UI")

1. Click **Save**.

   The user is now authorized to configure {{site.data.keyword.powerSys_notm}} resources. However, this user cannot manage services and resources that are specific to the {{site.data.keyword.cloud_notm}} platform. For example, they cannot add new users.