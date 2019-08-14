---

copyright:
  years: 2016, 2019
lastupdated: "2019-05-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:note: .note}

# {{site.data.keyword.powerSys_notm}} Activity Tracker 事件
{: #at_events}

作为安全主管、审计员或管理员，您可以使用 Activity Tracker 服务来跟踪用户和应用程序如何与 {{site.data.keyword.cloud}} 中的 {{site.data.keyword.powerSys_notm}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.at_full_notm}} 会记录用户发起的会更改 {{site.data.keyword.cloud_notm}} 中服务状态的活动。您可以使用此服务来调查异常活动和关键操作，并符合监管审计需求。此外，可以在发生操作时收到相关警报。收集的事件符合 Cloud Auditing Data Federation (CADF) 标准。
[了解更多](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started)。

## 事件列表：读取
{: #at_actions_read}

以下事件用于读取 {{site.data.keyword.powerSys_notm}} 实例。

|操作|描述|
|:---------------------------|:--------------------------------|
|pcloud.cloud-instance.read|读取 Power Cloud 实例|


## 事件列表：映像
{: #at_actions_images}

以下事件与使用 {{site.data.keyword.powerSys_notm}} 实例中的映像相关。

|操作|描述|
|:---------------------------|:--------------------------------|
|pcloud.image.read|读取一个映像或所有映像|
|pcloud.image.creat|创建新映像|
|pcloud.image.update|更新映像|
|pcloud.image.delete|删除映像|
|pcloud.image.capture|导出映像|


## 事件列表：网络
{: #at_actions_networks}

以下事件与使用 {{site.data.keyword.powerSys_notm}} 实例中的网络相关。

|操作|描述|
|:---------------------------|:--------------------------------------|
|pcloud.network.read|读取一个网络或所有网络|
|pcloud.network.create|创建新网络（公用/专用）|
|pcloud.network.update|更新网络|
|pcloud.network.delete|删除网络|
{: caption="表 3. 生成事件的操作" caption-side="top"}

## 事件列表：{{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

以下事件与使用 {{site.data.keyword.powerSys_notm}} 实例中的各个虚拟服务器相关。

|操作|描述|
|:------------------------------|:-------------------------------------|
|pcloud.pvm-instance.read|读取 Power 虚拟服务器实例|
|pcloud.pvm-instance.create|创建 Power 虚拟服务器实例|
|pcloud.pvm-instance.update|更新 Power 虚拟服务器实例|
|pcloud.pvm-instance.delete|删除 Power 虚拟服务器实例|
|pcloud.pvm-instance.start|启动 Power 虚拟服务器实例|
|pcloud.pvm-instance.stop|停止 Power 虚拟服务器实例|
|pcloud.pvm-instance.renew|重新引导 Power 虚拟服务器实例|
|pcloud.pvm-instance.unknown|对 Power 虚拟服务器实例执行的未知操作|
|pcloud.pvm-instance.monitor|通过控制台访问 Power 虚拟服务器实例|
|pcloud.pvm-instance.capture|将 Power 虚拟服务器实例捕获为映像|

## 事件列表：SSH 密钥
{: #at_actions_ssh_keys}

以下事件与使用 {{site.data.keyword.powerSys_notm}} 实例中的帐户和 SSH 密钥相关。

|操作|描述|
|:-------------------------|:----------------------------|
|pcloud.tenant.read|读取租户信息|
|pcloud.ssh-key.read|读取 SSHKey（即 SSH 密钥）|
|pcloud.ssh-key.create|创建 SSH 密钥|
|pcloud.ssh-key.update|更新 SSH 密钥|
|pcloud.ssh-key.delete|删除 SSH 密钥|

## 事件列表：数据卷
{: #at_actions_data_volumes}

以下事件与使用 {{site.data.keyword.powerSys_notm}} 实例中的数据卷相关。

|操作|描述|
|:-------------------------|:----------------------------|
|pcloud.volume.read|读取卷|
|pcloud.volume.create|创建卷|
|pcloud.volume.update|更新卷|
|pcloud.volume.delete|删除卷|
|pcloud.volume.configure|连接或拆离卷|

## 查看事件
{: #at_ui}

事件在**达拉斯**位置中提供。

{{site.data.keyword.at_full_notm}} 在每个位置只能有一个实例。要查看事件，必须在 `us-south` 位置访问 {{site.data.keyword.at_full_notm}} 服务的 Web UI。[了解更多](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2)。
