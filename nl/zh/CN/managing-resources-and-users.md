---

copyright:
  years: 2019

lastupdated: "2019-07-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}

# 管理 {{site.data.keyword.powerSys_notm}} 资源和用户
{: #managing-resources-and-users}

{{site.data.keyword.powerSysFull}} 的授权和资源管理实践通过 IBM Cloud Identity and Access Management (IAM) 服务进行协调。通过 IAM，您能够安全地认证用户，通过资源组控制对 {{site.data.keyword.powerSys_notm}} 资源的访问权，并通过访问组允许一组用户访问特定资源。换句话说，IAM 是一站式服务点，用于 {{site.data.keyword.cloud_notm}} 中的所有用户和资源管理。
{: shortdesc}

您可以根据以下条件来分配 IAM 授权：

* 单个用户
* 访问组（用户组）
* 特定类型的资源
* 资源组

有关 IAM 的更多信息，请查看以下信息：

* [IAM 入门](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [IAM 概念](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [管理资源组](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [设置访问组](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## 平台访问角色
{: #platform-access-roles}

可以使用平台访问角色来支持用户在 {{site.data.keyword.cloud_notm}} 资源上完成任务，例如创建用户或添加服务。

下表显示了 IAM 平台访问角色以及 {{site.data.keyword.powerSys_notm}} 允许的相应控制类型：

|平台访问角色|允许的访问类型|
|-----------|-------------------------|
|查看者|查看实例和列出实例。|
|操作员|查看实例和列出实例。|
|编辑者|查看实例、列出实例、创建实例和删除实例。|
|管理员|查看实例、列出实例、创建实例、删除实例以及将策略分配给其他用户。|

## 服务访问角色
{: #service-access-roles}

可以使用服务访问角色来定义哪些用户可以使用 {{site.data.keyword.powerSys_notm}} 服务功能。

下表显示了 IAM 服务访问角色以及用户可以通过 {{site.data.keyword.powerSys_notm}} 完成的相应操作：

|服务访问角色 |操作描述|
|-----------|-------------------------|
|读取者|查看所有资源，例如 SSH 密钥、存储卷和网络设置。无法对资源进行任何更改。|
|管理者|可以配置所有资源。下面是可以执行的一些操作：<ul><li>创建实例</li><li>增大存储卷大小</li><li>创建 SSH 密钥</li><li>修改网络设置</li><li>创建引导映像</li><li>删除存储卷</li>
</ul>

## 用户访问场景
{: #user-access-scenarios}

以下访问场景涵盖添加新用户和修改现有用户许可权所需的步骤。

### 邀请新用户查看 {{site.data.keyword.powerSys_notm}} 资源
{: #inviting-a-new-user-to-create-or-manage-resources}

您必须邀请 IBM Cloud 用户加入帐户，并向其授予查看 {{site.data.keyword.powerSys_notm}} 资源的访问权。请记住，服务访问角色用于确定用户对 {{site.data.keyword.powerSys_notm}} 资源具有的访问级别。

在 IAM 中完成以下步骤，以支持用户查看 {{site.data.keyword.powerSys_notm}} 资源：

1. 导航至 IBM Cloud 控制台中的 [IAM 用户 UI ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/iam/users){: new_window}，然后单击**邀请用户**。

      ![显示 IAM UI 中的“邀请用户”图标](/images/invite_users.png "在 IAM UI 中邀请用户")

2. 在**用户**部分下的**电子邮件地址**字段中，输入所需的用户电子邮件地址。
3. 接下来，从**分配对以下对象的访问权**字段中，选择**资源**，然后在**服务**字段中，选择 **{{site.data.keyword.powerSys_notm}}**。

    ![显示服务字段](/images/invite_users2.png "在 IAM UI 中为新用户选择 {{site.data.keyword.powerSys_notm}} 服务")

4. 选择要分配给用户的平台访问角色。在此场景中，用户只能查看 {{site.data.keyword.cloud_notm}} 和 {{site.data.keyword.powerSys_notm}} 资源。

    ![显示用于 IAM 角色的 UI](/images/invite_users3.png "在 IAM UI 中为新用户选择角色")

5. 单击**邀请用户**。用户必须接受邀请，才能被添加到帐户。如果成功发送了邀请，那么会显示一条消息。

    ![显示成功邀请的消息](/images/invite_users4.png "成功邀请消息")

### 授予现有用户管理 {{site.data.keyword.powerSys_notm}} 资源的许可权
{: #giving-an-existing-user-permission-to-manage-resources}

要为帐户中的现有用户提供配置 {{site.data.keyword.powerSys_notm}} 资源的许可权，请完成以下步骤。

1. 导航至 IBM Cloud 控制台中的 [IAM 用户 UI ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/iam/users){: new_window}。
2. 从用户列表中，选择要更改其授权的用户。
3. 单击**访问策略**，然后单击用户的当前角色。在此场景中，请单击**查看者和读取者**。

    ![显示如何更改现有用户的许可权](/images/existing_user1.png "在 IAM UI 中更改用户的许可权")

4. 在**选择角色**字段中，单击**管理者**。可以将**读取者**角色保持选中。

    ![显示为现有用户添加管理者角色](/images/existing_user2.png "在 IAM UI 中选择管理者角色")

5. 单击**保存**。

   现在，用户有权配置 {{site.data.keyword.powerSys_notm}} 资源。但是，此用户无法管理特定于 {{site.data.keyword.cloud_notm}} 平台的服务和资源。例如，该用户无法添加新用户。
   {: note}
