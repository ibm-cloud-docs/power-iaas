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

# Configurazione di Power Systems Virtual Servers con una rete privata
{: #cpn-configuring}

Puoi utilizzare una rete privata con {{site.data.keyword.powerSysFull}} per connetterti in modo sicuro al tuo ambiente in loco con l'ambiente {{site.data.keyword.cloud_notm}} non in loco. In una rete privata, puoi accedere alle risorse {{site.data.keyword.cloud_notm}} ed eseguire l'interconnessione ad altri server virtuali.
{:shortdesc}

Puoi utilizzare una delle seguenti opzioni per creare una rete privata che connette il tuo ambiente in loco all'ambiente {{site.data.keyword.cloud_notm}}:

1. **{{site.data.keyword.cloud_notm}} SSL VPN con un server jump**
   * Puoi utilizzare il servizio {{site.data.keyword.cloud_notm}} SSL VPN per la connessione nella tua rete {{site.data.keyword.cloud_notm}} esistente. Nella rete {{site.data.keyword.cloud_notm}}, puoi utilizzare una macchina virtuale (VM) {{site.data.keyword.cloud_notm}} come un server jump per la connessione alla tua istanza di {{site.data.keyword.powerSys_notm}}.
   * Devi utilizzare un server jump perché non puoi utilizzare una connessione VPN per connetterti direttamente all'istanza di {{site.data.keyword.powerSys_notm}}.
   * Questa opzione viene normalmente utilizzata per gestire i tuoi ambienti. Questa opzione non è consigliata per i carichi di lavoro di produzione.
   * Per ulteriori informazioni su come configurare questa opzione, vedi [Configura la VPN SSL](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) e [Ordinazione di un VRA (Virtual Router Appliance)](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

2. **{{site.data.keyword.cloud_notm}} IPSec VPN con IBM Cloud Virtual Router Appliance**
   * Puoi utilizzare il servizio {{site.data.keyword.cloud_notm}} IPSec VPN per la connessione nella tua rete {{site.data.keyword.cloud_notm}} esistente. Nella rete {{site.data.keyword.cloud_notm}}, puoi utilizzare il IBM Cloud Virtual Router Appliance (VRA) per la connessione alla tua istanza di {{site.data.keyword.powerSys_notm}}.
   * Devi utilizzare un VRA perché non puoi utilizzare una connessione VPN per connetterti direttamente all'istanza di {{site.data.keyword.powerSys_notm}}.
   * Questa opzione viene normalmente utilizzata per gestire i tuoi ambienti. Questa opzione non è consigliata per i carichi di lavoro di produzione.
   * Per ulteriori informazioni su come configurare questa opzione, vedi [Configura la VPN IPSec](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) e [Ordinazione di un VRA (Virtual Router Appliance)](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

3. **Direct Link Connect con IBM Cloud Virtual Router Appliance**
   * Puoi ordinare il servizio Direct Link Connect da IBM il quale connette la tua rete in loco alla rete IBM Cloud tramite IBM Cloud Virtual Router Appliance (VRA).
   * Questa opzione fornisce elevate prestazioni tra la rete in loco e la rete IBM Cloud.
   * Per ordinare un Direct Link Connect, completa la procedura nell'argomento [Ordinazione di IBM Cloud Direct Link Connect dalla console dell'IU](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).
   * Esistono degli indirizzi IP specifici che non puoi utilizzare con un servizio Direct Link Connect. Per ulteriori informazioni, vedi [Limitazioni rigorose sulle assegnazioni IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).
