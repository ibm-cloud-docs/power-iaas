---

copyright:
  years: 2019

lastupdated: "2019-7-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}

# Introdução aos servidores virtuais Power Systems
{: #getting-started}


O {{site.data.keyword.powerSysFull}} é uma oferta de infraestrutura como serviço que pode ser usada para implementar um servidor virtual, também conhecido como partição lógica (LPAR), em questão de minutos.
{:shortdesc}

É possível implementar rapidamente os {{site.data.keyword.powerSys_notm}}s para atender às suas necessidades de negócios específicas. Com o {{site.data.keyword.powerSys_notm}}, é possível criar um ambiente de nuvem híbrida que permite o controle fácil de suas demandas de carga de trabalho.

Os {{site.data.keyword.powerSys_notm}}s podem executar cargas de trabalho do AIX ou do IBM i em diferentes locais geográficos.

## Terminologia
{: #gs-terminology}

Antes de criar um servidor virtual, deve-se entender a diferença de terminologia entre um **serviço** {{site.data.keyword.powerSys_notm}} e uma **instância** do {{site.data.keyword.powerSys_notm}}. Pense no **serviço** {{site.data.keyword.powerSys_notm}} como um contêiner para todas as **instâncias** do {{site.data.keyword.powerSys_notm}} em um local geográfico específico. O **serviço** {{site.data.keyword.powerSys_notm}} está disponível na **Lista de recursos** da IU do {{site.data.keyword.cloud}}. Ele pode conter diversas **instâncias** do {{site.data.keyword.powerSys_notm}}.

Por exemplo, é possível ter dois **serviços** {{site.data.keyword.powerSys_notm}}, um em Dallas e outro em Washington DC. Cada um pode conter diversas **instâncias** do {{site.data.keyword.powerSys_notm}}.

## Antes de começar
{: #gs-before-you-begin}

Antes de criar sua primeira instância de servidor virtual Power Systems, revise os pré-requisitos a seguir:

1. {: hide-dashboard} Crie uma conta do IBM Cloud. Para isso, consulte [Inscrever-se no IBM Cloud ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/registration){: new_window}.

2. Crie uma chave SSH pública e privada que possa ser usada para se conectar com segurança ao seu {{site.data.keyword.powerSys_notm}}. Para isso, consulte [Incluindo uma chave SSH ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)

3. (Opcional) Se desejar usar uma imagem customizada para o sistema operacional AIX ou IBM i, um IBM Cloud Object Storage deverá ser criado e o upload da imagem deverá ser realizado. Para obter mais informações, consulte [Configurando uma imagem customizada](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

4. (Opcional) Se desejar usar uma rede privada para se conectar a uma instância do {{site.data.keyword.powerSys_notm}}, o serviço Direct Link Connect deverá ser solicitado. Para obter mais informações, consulte [Solicitando o IBM Cloud Direct Link Connect por meio do console da IU](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## Próximos passos
{: #gs-next-steps}

Agora, com uma conta do IBM Cloud e uma chave SSH privada e pública, você está pronto para [Criar o serviço {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).
