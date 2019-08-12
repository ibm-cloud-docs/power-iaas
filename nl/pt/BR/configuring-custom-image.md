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

# Configurando uma imagem customizada com um servidor virtual Power Systems
{: #configuring-custom-image}

É possível trazer sua própria imagem customizada do sistema operacional AIX ou IBM i para implementar um {{site.data.keyword.powerSysFull}}.
{:shortdesc}

Não é possível transferir uma licença de sistema operacional de um sistema local para um {{site.data.keyword.powerSys_notm}} em execução no ambiente de nuvem. O custo de licença é integrado à taxa de faturamento por hora geral.
{: note}

## Antes de começar
{: #cci-before-you-begin}

Antes de usar uma imagem customizada como o volume de inicialização, revise as informações a seguir:

* Deve-se verificar se o nível de tecnologia do sistema operacional AIX ou IBM i é suportado no hardware do Power Systems selecionado no campo **Tipo de máquina**. Para ver uma lista dos níveis de tecnologia dos sistemas operacionais AIX e IBM i suportados e o hardware do Power Systems, consulte [Mapas do software do sistema ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).
* Deve-se ter um entendimento básico dos conceitos do **IBM Cloud Object Storage**. Para obter mais informações, consulte [Sobre o IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage).
* Se não tiver uma imagem existente do AIX ou do IBM i, será possível usar o IBM® PowerVC™ para capturar e exportar uma imagem a ser usada com um {{site.data.keyword.powerSys_notm}}. Para obter mais informações, consulte [Capturando uma máquina virtual ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} e [Exportando imagens ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}.

## Fazendo upload de uma imagem customizada como um objeto
{: #cci-uploading}

1. Crie um objeto do IBM Cloud Storage e faça upload de sua imagem. Para obter mais informações, consulte [Fazer upload de dados](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload).
2. Gere as chaves de acesso e secreta com o Hash-based Message Authentication Code (HMAC). É possível gerar essas chaves ao criar as credenciais de serviço para o objeto do IBM Cloud Storage. Para criar as credenciais de serviço, deve-se ter acesso `Writer` ao depósito do **Object Storage**. Para obter mais informações, consulte [Credenciais de serviço](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) e [Permissões de depósito](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).
3. No [catálogo do IBM Cloud ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/catalog){: new_window}, clique no quadro Servidor virtual Power para incluir a imagem. Se você já criou a instância de servidor virtual, selecione **Ícone Menu ![Ícone Menu](../icons/icon_hamburger.svg "Ícone Menu") > Lista de recursos > Dispositivos** e selecione seu servidor virtual existente.

 Preencha os campos a seguir para criar seu {{site.data.keyword.powerSys_notm}} e clique em **Imagem customizada do AIX** ou em **Imagem customizada do IBM i**.

| Campo | Descrição |
| ------| ------------|
| Nome do depósito do Cloud Object Storage | Para identificar o nome de seu depósito, selecione **Ícone Menu ![Ícone Menu](../icons/icon_hamburger.svg "Ícone Menu") > Lista de recursos > Armazenamento > Nome do Cloud Storage Object > Depósitos**. |
| Chave de acesso do Cloud Object Storage | Para identificar sua chave de acesso, selecione **Ícone Menu ![Ícone Menu](../icons/icon_hamburger.svg "Ícone Menu") > Lista de recursos > Armazenamento > Nome do Cloud Storage Object > Credenciais de serviço > Visualizar credenciais**. Copie o valor `access_key_id` e cole-o nesse campo. |
| Chave secreta do Cloud Object Storage | Para identificar sua chave secreta, selecione **Ícone Menu ![Ícone Menu](../icons/icon_hamburger.svg "Ícone Menu") > Lista de recursos > Armazenamento > Nome do Cloud Storage Object > Credenciais de serviço > Visualizar credenciais**. Copie o valor `secret_access_key` e cole-o nesse campo. |
| Caminho da imagem | Insira o caminho completo do arquivo de imagem. O caminho completo deve estar no formato `endpoint/bucket_name/file_name`. Deve-se usar o domínio do terminal privado. Por exemplo, `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`. É possível identificar o domínio do terminal, o nome do depósito e o nome do arquivo selecionando **Ícone Menu ![Ícone Menu](../icons/icon_hamburger.svg "Ícone Menu") > Lista de recursos > Armazenamento > Cloud Storage Object**.
