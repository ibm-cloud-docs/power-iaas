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

# Einführung in Power Systems Virtual Servers
{: #getting-started}


{{site.data.keyword.powerSysFull}} ist ein Angebot für eine Infrastructure as a Service, die Sie verwenden können, um einen virtuellen Server, auch unter dem Namen logische Partition (LPAR) bekannt, in wenigen Minuten bereitzustellen.
{:shortdesc}

Sie können {{site.data.keyword.powerSys_notm}}s schnell bereitstellen, um Ihren Geschäftsanforderungen gerecht zu werden. Mit {{site.data.keyword.powerSys_notm}} können Sie eine Hybrid-Cloud-Umgebung erstellen, die eine einfache Steuerung des Workloadbedarfs ermöglicht. 

{{site.data.keyword.powerSys_notm}}s können AIX- oder IBM i-Workloads an verschiedenen Standorten ausführen. 

## Terminologie
{: #gs-terminology}

Bevor Sie einen virtuellen Server erstellen, müssen Sie den Unterschied in der Terminologie von einem {{site.data.keyword.powerSys_notm}}-**Service** und einer {{site.data.keyword.powerSys_notm}}-**Instanz** verstanden haben. Stellen Sie sich den {{site.data.keyword.powerSys_notm}}-**Service** als einen Container für alle {{site.data.keyword.powerSys_notm}}-**Instanzen** an einem bestimmten Standort vor. Der {{site.data.keyword.powerSys_notm}}-**Service** ist in der **Ressourcenliste** in der Benutzerschnittstelle von{{site.data.keyword.cloud}} verfügbar. Der Service kann mehrere {{site.data.keyword.powerSys_notm}}-**Instanzen** enthalten.

Sie können beispielsweise über zwei {{site.data.keyword.powerSys_notm}}-**Services** verfügen, wobei sich einer in Dallas und ein anderer in Washington DC befindet. Jeder Service kann mehrere {{site.data.keyword.powerSys_notm}}-**Instanzen** enthalten.

## Vorbereitende Schritte
{: #gs-before-you-begin}

Bevor Sie Ihre erste Power Systems Virtual Server-Instanz erstellen, prüfen Sie die folgenden Voraussetzungen: 

1. {: hide-dashboard} Erstellen Sie ein IBM Cloud-Konto. Informationen dazu, wie Sie ein IBM Cloud-Konto erstellen, finden Sie unter [Für IBM Cloud anmelden ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/registration){: new_window}.

2. Erstellen Sie einen öffentlichen und privaten SSH-Schlüssel, den Sie verwenden können, um eine sichere Verbindung zu Ihrem {{site.data.keyword.powerSys_notm}} herzustellen. Informationen zum Erstellen eines öffentlichen und privaten SSH-Schlüssels finden Sie unter [SSH-Schlüssel hinzufügen![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)

3. (Optional) Wenn Sie ein angepasstes Image für die Betriebssysteme AIX oder IBM i verwenden möchten, müssen Sie einen IBM Cloud Object Storage erstellen und das Image hochladen. Weitere Informationen finden Sie unter [Angepasstes Image konfigurieren](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

4. (Optional) Wenn Sie ein privates Netz verwenden möchten, um eine Verbindung zu einer {{site.data.keyword.powerSys_notm}}-Instanz herzustellen, müssen Sie den Direct Link Connect-Service bestellen. Weitere Informationen finden Sie unter [Ordering IBM Cloud Direct Link Connect from the UI Console](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## Nächste Schritte
{: #gs-next-steps}

Mit einem IBM Cloud-Konto und einem privaten und öffentlichen SSH-Schlüssel können Sie nun damit beginnen, dass Sie den [{{site.data.keyword.powerSys_notm}}-Service erstellen](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).
