---

copyright:
  years: 2019

lastupdated: "2019-07-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Configurando servidores virtuais Power Systems com uma rede privada
{: #cpn-configuring}

É possível usar uma rede privada com o {{site.data.keyword.powerSysFull}} para conectar com segurança seu ambiente local ao ambiente externo do {{site.data.keyword.cloud_notm}}. Em uma rede privada, é possível acessar os recursos do {{site.data.keyword.cloud_notm}} e interconectar-se a outros servidores virtuais.
{:shortdesc}

É possível usar uma das opções a seguir para criar uma rede privada que conecta seu ambiente local ao ambiente do {{site.data.keyword.cloud_notm}}:

1. VPN SSL do **{{site.data.keyword.cloud_notm}} com servidor de salto**
   * É possível usar o serviço de VPN SSL do {{site.data.keyword.cloud_notm}} para se conectar à sua rede existente do {{site.data.keyword.cloud_notm}}. Dentro da rede do {{site.data.keyword.cloud_notm}}, é possível usar uma máquina virtual (VM) do {{site.data.keyword.cloud_notm}} como um servidor de salto para se conectar à sua instância do {{site.data.keyword.powerSys_notm}}.
   * Um servidor de salto deve ser usado porque não é possível usar uma conexão VPN para se conectar diretamente com a instância do {{site.data.keyword.powerSys_notm}}.
   * Essa opção geralmente é usada para gerenciar seus ambientes. Ela não é recomendada para cargas de trabalho de produção.
   * Para obter mais informações sobre como configurar essa opção, consulte [Configurar a VPN SSL](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) e [Solicitando um Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

2. **VPN IPSec do {{site.data.keyword.cloud_notm}} com IBM Cloud Virtual Router Appliance**
   * É possível usar o serviço de VPN IPSec do {{site.data.keyword.cloud_notm}} para se conectar à sua rede existente do {{site.data.keyword.cloud_notm}}. Dentro da rede do {{site.data.keyword.cloud_notm}}, é possível usar o IBM Cloud Virtual Router Appliance (VRA) para se conectar à sua instância do {{site.data.keyword.powerSys_notm}}.
   * Um VRA deve ser usado porque não é possível usar uma conexão VPN para se conectar diretamente à instância do {{site.data.keyword.powerSys_notm}}.
   * Essa opção geralmente é usada para gerenciar seus ambientes. Ela não é recomendada para cargas de trabalho de produção.
   * Para obter mais informações sobre como configurar essa opção, consulte [Configurar a VPN IPSec](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) e [Solicitando um Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

3. **Direct Link Connect com IBM Cloud Virtual Router Appliance**
   * É possível solicitar à IBM o serviço Direct Link Connect, que conecta sua rede local à rede do IBM Cloud usando o IBM Cloud Virtual Router Appliance (VRA).
   * Essa opção fornece um alto desempenho entre a rede local e a rede do IBM Cloud.
   * Para solicitar um Direct Link Connect, conclua as etapas no tópico [Solicitando o IBM Cloud Direct Link Connect por meio do console da IU](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).
   * Há endereços IP específicos que não podem ser utilizados com um serviço Direct Link Connect. Para obter mais informações, consulte [Limitações rigorosas quanto às designações de IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).
