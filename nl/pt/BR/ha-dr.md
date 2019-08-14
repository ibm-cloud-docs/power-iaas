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
{:important: .important}
{:tip: .tip}
{:note: .note}

# Opções de alta disponibilidade e recuperação de desastre nos servidores virtuais Power Systems
{: #ha-dr}

A instância do {{site.data.keyword.powerSys_notm}} reiniciará os servidores virtuais em um sistema host diferente se uma falha de hardware ocorrer. Esse processo fornece recursos básicos de alta disponibilidade (HA) ao serviço {{site.data.keyword.powerSys_notm}}.
{:shortdesc}

Para obter soluções de HA ou DR (recuperação de desastre) mais avançadas, implemente os aplicativos a seguir em seu ambiente do {{site.data.keyword.powerSys_notm}}.

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

É possível usar um modelo de assinatura mensal ao comprar o PowerHA SystemMirror for AIX Standard Edition. Para obter mais informações, consulte [Opções de precificação mensal da Standard Edition ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html).

Depois de comprar, é possível fazer download do software no [IBM Entitled Systems Support (ESS) ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/eserver/ess). É possível instalar o PowerHA SystemMirror for AIX no servidor virtual que está em execução em seu ambiente do {{site.data.keyword.powerSys_notm}}. Para obter instruções de instalação, consulte [Instalando o PowerHA SystemMirror ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html).

Revise as informações a seguir para implementar o PowerHA SystemMirror for AIX em seu ambiente do {{site.data.keyword.powerSys_notm}}.

* Ao criar os servidores virtuais que fazem parte do cluster do PowerHA SystemMirror, deve-se selecionar **Servidor diferente** no campo **Regras de colocação**.
![Exibe o campo de regras de colocação](/images/hadr2.png "Exibe o campo de regras de colocação")

* Ao criar volumes de armazenamento (discos) para os severos virtuais que fazem parte do cluster do PowerHA SystemMirror, deve-se selecionar **Ligado** no campo **Compartilhável**.
![Exibe o campo de regras compartilháveis](/images/hadr1.png "Exibe o campo Compartilhável")

* Usando o serviço {{site.data.keyword.powerSys_notm}}, você não tem acesso ao HMC, ao VIOS e ao sistema host. Portanto, quaisquer funções do PowerHA SystemMirror que requerem acesso a esses recursos, como o Resource Optimized High Availability (ROHA) e o Active Node Halt Policy (ANHP), não estão disponíveis.

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## Continuidade de negócios por meio de backup e restauração
{: #ha-dr-ha-business}

A configuração e os dados do seu {{site.data.keyword.powerSys_notm}} não são submetidos a backup pelo {{site.data.keyword.cloud}}.

É possível usar a IU do {{site.data.keyword.cloud_notm}} para fazer backup de seu servidor virtual no {{site.data.keyword.cloud_notm}} Object Storage. É possível usar esse processo para restaurar seu servidor virtual no caso de uma falha crítica. Para obter mais informações, consulte [Cloud Object Storage ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started).
