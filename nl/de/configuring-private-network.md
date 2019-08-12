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

# Power Systems Virtual Servers mit einem privaten Netz konfigurieren
{: #cpn-configuring}

Sie können ein privates Netz mit {{site.data.keyword.powerSysFull}} verwenden, um eine sichere Verbindung Ihrer On-Premises-Umgebung mit der Off-Premises-{{site.data.keyword.cloud_notm}}-Umgebung herzustellen. In einem privaten Netz können Sie auf {{site.data.keyword.cloud_notm}}-Ressourcen  zugreifen und sich mit anderen virtuellen Servern verbinden.
{:shortdesc}

Sie können eine der folgenden Optionen verwenden, um ein privates Netz zu erstellen, das Ihre On-Premises-Umgebung mit der {{site.data.keyword.cloud_notm}}-Umgebung verbindet:

1. **{{site.data.keyword.cloud_notm}}-SSL-VPN mit Jump-Server**
   * Sie können den {{site.data.keyword.cloud_notm}}-SSL-VPN-Service verwenden, um eine Verbindung in Ihr vorhandenes {{site.data.keyword.cloud_notm}}-Netz herzustellen. Innerhalb des {{site.data.keyword.cloud_notm}}-Netzes können Sie eine {{site.data.keyword.cloud_notm}}-VM (Virtual Machine) als Jump-Server verwenden, um eine Verbindung zu Ihrer {{site.data.keyword.powerSys_notm}}-Instanz herzustellen. 
   * Sie müssen einen Jump-Server verwenden, da Sie keine VPN-Verbindung verwenden können, um eine direkte Verbindung zur {{site.data.keyword.powerSys_notm}}-Instanz herzustellen. 
   * Diese Option wird in der Regel verwendet, um Ihre Umgebungen zu verwalten. Diese Option wird nicht für den Produktionsbetrieb empfohlen. 
   * Weitere Informationen dazu, wie Sie diese Option konfigurieren, finden Sie unter [SSL-VPN einrichten](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) und [Eine Virtual Router Appliance bestellen](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

2. **{{site.data.keyword.cloud_notm}}-IPSec-VPN mit IBM Cloud Virtual Router Appliance**
   * Sie können den {{site.data.keyword.cloud_notm}}-IPSec-VPN-Service verwenden, um eine Verbindung in Ihr vorhandenes {{site.data.keyword.cloud_notm}}-Netz herzustellen. Innerhalb des {{site.data.keyword.cloud_notm}}-Netzes können Sie die IBM Cloud Virtual Router Appliance (VRA) verwenden, um eine Verbindung zu Ihrer {{site.data.keyword.powerSys_notm}}-Instanz herzustellen. 
   * Sie müssen eine VRA verwenden, da Sie keine VPN-Verbindung verwenden können, um eine direkte Verbindung zur {{site.data.keyword.powerSys_notm}}-Instanz herzustellen. 
   * Diese Option wird in der Regel verwendet, um Ihre Umgebungen zu verwalten. Diese Option wird nicht für den Produktionsbetrieb empfohlen. 
   * Weitere Informationen dazu, wie Sie diese Option konfigurieren, finden Sie unter [IPSec-VPN einrichten](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) und [Eine Virtual Router Appliance bestellen](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

3. **Direct Link Connect mit IBM Cloud Virtual Router Appliance**
   * Sie können den Direct Link Connect-Service von IBM bestellen, mit dem Sie Ihr On-Premises-Netz mit dem Netz der IBM Cloud verbinden können, indem Sie die IBM Cloud Virtual Router Appliance (VRA) verwenden.
   * Diese Option bietet eine hohe Leistung zwischen dem On-Premises-Netz und dem Netz der IBM Cloud.
   * Um Direct Link Connect zu bestellen, führen Sie die Schritte aus, die im Abschnitt [IBM Cloud Direct Link Connect von der Konsole der Benutzerschnittstelle aus bestellen](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect) beschrieben sind.
   * Es gibt bestimmte IP-Adressen, die Sie nicht mit einem Direct Link Connect-Service verwenden können. Weitere Informationen finden Sie im Abschnitt [Strikte Einschränkungen bei IP-Zuweisungen](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).
