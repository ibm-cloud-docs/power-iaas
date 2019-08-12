---

copyright:
  years: 2019

lastupdated: "2019-7-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# 配置定制映像以用于 Power Systems Virtual Server
{: #configuring-custom-image}

您可以使用自带定制 AIX 或 IBM i 操作系统映像来部署 {{site.data.keyword.powerSysFull}}。
{:shortdesc}

不能将操作系统许可证从内部部署系统传输到在云环境中运行的 {{site.data.keyword.powerSys_notm}}。许可证成本已计入总体每小时计费费率中。
{: note}

## 开始之前
{: #cci-before-you-begin}

要能够将定制映像用作引导卷，请首先查看以下信息：

* 必须验证 AIX 或 IBM i 操作系统技术级别在**机器类型**字段中选择的 Power Systems 硬件上是否受支持。要查看支持的 AIX 和 IBM i 操作系统技术级别以及 Power System 硬件的列表，请参阅 [System software maps ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps)。
* 您必须对 **IBM Cloud Object Storage** 概念有基本的了解。有关更多信息，请参阅[关于 IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage)。
* 如果您没有现有的 AIX 或 IBM i 映像，那么可以使用 IBM® PowerVC™ 来捕获和导出映像，以用于 {{site.data.keyword.powerSys_notm}}。有关更多信息，请参阅 [Capturing a virtual machine ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} 和 [Exporting images ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}。

## 将定制映像作为对象上传
{: #cci-uploading}

1. 创建 IBM Cloud Storage 对象并上传映像。有关更多信息，请参阅[上传数据](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload)。
2. 使用基于散列的消息认证代码 (HMAC) 生成私钥和访问密钥。您可以在为 IBM Cloud Storage 对象创建服务凭证时生成这些密钥。要创建服务凭证，您必须对 **Object Storage** 存储区具有`写入者`访问权。有关更多信息，请参阅[服务凭证](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials)和[存储区许可权](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions)。
3. 在 [IBM Cloud 目录 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/catalog){: new_window} 中，单击 Power Virtual Server 磁贴以添加映像。如果已创建虚拟服务器实例，请选择**“菜单”图标 ![“菜单”图标](../icons/icon_hamburger.svg "“菜单”图标") > 资源列表 > 设备**，然后选择现有虚拟服务器。

 填写以下字段以创建 {{site.data.keyword.powerSys_notm}}，然后单击**定制 AIX 映像**或**定制 IBM i 映像**。

|字段|描述|
| ------| ------------|
|Cloud Object Storage 存储区名称|要识别存储区名称，请选择**“菜单”图标 ![“菜单”图标](../icons/icon_hamburger.svg "“菜单”图标") > 资源列表 > 存储 > Cloud Storage 对象名称 > 存储区**。|
|Cloud Object Storage 访问密钥|要识别访问密钥，请选择**“菜单”图标 ![“菜单”图标](../icons/icon_hamburger.svg "“菜单”图标") > 资源列表 > 存储 > Cloud Storage 对象名称 > 服务凭证 > 查看凭证**。复制 `access_key_id` 值并将其粘贴到此字段中。|
|Cloud Object Storage 私钥|要识别私钥，请选择**“菜单”图标 ![“菜单”图标](../icons/icon_hamburger.svg "“菜单”图标") > 资源列表 > 存储 > Cloud Storage 对象名称 > 服务凭证 > 查看凭证**。复制 `secret_access_key` 值并将其粘贴到此字段中。|
|映像路径|输入映像文件的标准路径。标准路径的格式必须为 `endpoint/bucket_name/file_name`。您必须使用专用端点域。例如，`s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`。您可以通过选择**“菜单”图标 ![“菜单”图标](../icons/icon_hamburger.svg "“菜单”图标") > 资源列表 > 存储 > Cloud Storage 对象**来识别端点域、存储区名称和文件名。
