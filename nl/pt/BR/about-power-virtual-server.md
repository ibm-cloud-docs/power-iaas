---

copyright:
  years: 2019

lastupdated: "2019-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Sobre os servidores virtuais Power Systems
{: #about-power-virtual-server}

O {{site.data.keyword.powerSysFull}} usa a plataforma existente do IBM Cloud para criar servidores virtuais Power Systems, também conhecidos como partições lógicas (LPAR), que são executados no hardware do IBM Power Systems com o hypervisor PowerVM.
{:shortdesc}

Os {{site.data.keyword.powerSys_notm}}s são um tipo de infraestrutura como serviço (IaaS). Com o serviço {{site.data.keyword.powerSys_notm}}, é possível criar e implementar rapidamente um ou diversos servidores virtuais que executem os sistemas operacionais AIX ou IBM i em uma nuvem pública. Depois de provisionar o servidor virtual na nuvem, é de sua responsabilidade certificar-se de que o sistema operacional AIX ou IBM i esteja seguro.

## Recursos-chave
{: #apvs-key-features}

Consulte a seguir alguns dos recursos importantes para o {{site.data.keyword.powerSys_notm}}.

### Faturamento direto
{: #apvs-billing}

O {{site.data.keyword.powerSys_notm}} usa uma taxa de faturamento mensal que inclui as licenças para os sistemas operacionais AIX e IBM i. A taxa de faturamento mensal é rateada por hora com base nos recursos implementados na instância do {{site.data.keyword.powerSys_notm}} para o mês. Ao criar a instância do {{site.data.keyword.powerSys_notm}}, é possível ver o custo total para sua configuração com base nas opções especificadas. É possível identificar rapidamente quais opções de configuração fornecem a você o melhor valor para suas necessidades de negócios. Para obter mais informações, consulte  [ Precificação ](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server).

### Ambiente de nuvem híbrida
{: #apvs-hybrid}

É possível usar os {{site.data.keyword.powerSys_notm}}s para executar qualquer carga de trabalho do AIX ou do IBM i fora de sua infraestrutura de hardware existente do Power Systems. Executar suas cargas de trabalho na nuvem pública permite que você aproveite todas as vantagens que a nuvem tem para oferecer, como o autoatendimento, a entrega rápida, a elasticidade e a conectividade com outros serviços do IBM Cloud. Embora suas cargas de trabalho do AIX e do IBM i estejam em execução na nuvem, você ainda mantém os mesmos recursos escaláveis, resilientes e prontos para produção fornecidos pelo hardware do Power Systems.

### Customização de infraestrutura
{: #apvs-customization}

É possível configurar e customizar as opções a seguir ao criar um {{site.data.keyword.powerSys_notm}}:
* Número de instâncias de servidor virtual
* Número de núcleos
* Quantidade de memória
* Tamanho e tipo do volume de dados (HDD ou SSD)
* Rede privada ou pública

### Traga sua própria imagem
{: #apvs-own-image}

A IBM fornece a você as imagens de estoque dos sistemas operacionais AIX e IBM i na criação de um {{site.data.keyword.powerSys_notm}}. No entanto, é possível trazer sua própria imagem customizada do sistema operacional AIX ou IBM i implementada e testada anteriormente. Para obter mais informações, consulte [Configurando uma imagem customizada](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Especificações de hardware
{: #apvs-hardware-specifications}

O hardware do IBM Power Systems a seguir hospeda o {{site.data.keyword.powerSys_notm}}:

* Cálculo
  * [Power System E880 (9119-MHE) ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 TB de memória
    * 8 x 16 Gigabit PCI Express de porta dupla Fibre Channel (FC)
    * 10 x 10 Gigabit Ethernet-SR PCI Express de porta dupla
  * [Power System S922 (9009-22A) ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 GB de memória
    * 2 x 16 Gigabit PCI Express de porta dupla FC
    * 3 x 10 Gigabit Ethernet-SR PCI Express de porta dupla

* Storage
  * Storewize V7000F(2076-AF6) Dual Controller
  * Storwize V7000 (2076-624) Dual Controller

* Rede
  * Cisco Nexus9000 93180YC-EX (10G)
  * Cisco Nexus9000 C9348GC-FXP (1G)

## Redes públicas e privadas
{: #apvs-public-and-private}

Ao criar um {{site.data.keyword.powerSys_notm}}, é possível selecionar uma interface de rede privada ou pública.

* Rede pública
  * Um método rápido e fácil para se conectar a uma instância do {{site.data.keyword.powerSys_notm}}.
  * A IBM configura a infraestrutura de rede para ativar uma conexão de rede pública segura da Internet com a instância do {{site.data.keyword.powerSys_notm}}.
  * A conectividade é implementada usando uma conexão do IBM Cloud Virtual Router Appliance (VRA) e uma do Direct Link Connect.
  * Com proteção de firewall, suporta os protocolos de rede segura a seguir:
    * SSH
    * HTTPS
    * Ping
    * Emulação de terminal do IBM i 5250 com SSL (porta 992)

* Rede Privada
  * Permite que os recursos de sua instância do {{site.data.keyword.powerSys_notm}} acessem recursos existentes do {{site.data.keyword.cloud_notm}}, como servidores bare metal, contêineres Kubernetes ou armazenamento em nuvem.
  * Usa uma conexão do Direct Link Connect para se conectar à rede e aos recursos de sua conta do IBM Cloud. O processo de criação de uma conexão do Direct Link Connect pode demorar alguns dias porque o suporte do IBM Cloud precisa configurar o link.
  * Necessário para a comunicação entre diferentes instâncias do {{site.data.keyword.powerSys_notm}}.

    Para obter mais informações sobre as diferentes opções de configuração de uma rede privada, consulte [Configurar uma rede privada](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring).
    {: note}

A figura a seguir exibe a configuração básica para uma rede pública e privada:

![Exibe como o tráfego de rede flui para a conexão pública ou privada](/images/power-iaas-network1.svg "Exibe como o tráfego de rede flui para a conexão pública ou privada")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
