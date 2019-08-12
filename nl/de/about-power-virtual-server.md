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

# Informationen zu Power Systems Virtual Servers
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} verwendet die vorhandene IBM Cloud-Plattform für die Erstellung von Power Systems Virtual Servers, die auch unter der Bezeichnung logische Partitionen (LPAR) bekannt sind und die mit dem PowerVM-Hypervisor auf IBM Power Systems-Hardware ausgeführt werden.
{:shortdesc}

{{site.data.keyword.powerSys_notm}}s sind eine Form von Infrastructure as a Service (IaaS). Mit dem {{site.data.keyword.powerSys_notm}}-Service können Sie schnell einen oder mehrere virtuelle Server erstellen, die entweder unter dem Betriebssystem AIX oder unter IBM i in einer öffentliche Cloud ausgeführt werden. Nachdem Sie den virtuellen Server in der Cloud bereitgestellt haben, sind Sie dafür verantwortlich sicherzustellen, dass das Betriebssystem AIX bzw. IBM i sicher ist.

## Schlüsselfunktionen
{: #apvs-key-features}

Im Folgenden sind einige der Schlüsselfunktionen von {{site.data.keyword.powerSys_notm}} beschrieben.

### Einfache Abrechnung
{: #apvs-billing}

Bei {{site.data.keyword.powerSys_notm}} erfolgt die Abrechnung monatlich und umfasst die Lizenzen für die Betriebssysteme AIX und IBM i. Die monatliche Abrechnung erfolgt anteilig nach Stunden auf Basis der Ressourcen, die in der {{site.data.keyword.powerSys_notm}}-Instanz für den jeweiligen Monat bereitgestellt wurden. Wenn Sie die {{site.data.keyword.powerSys_notm}}-Instanz erstellen, können Sie die Gesamtkosten für Ihre Konfiguration auf Grundlage der von Ihnen angegebenen Optionen anzeigen. Sie können schnell feststellen, welche Konfigurationsoptionen Ihnen die beste Kosten-Nutzen-Relation für Ihre Geschäftsanforderungen bieten. Weitere Informationen finden Sie im Abschnitt [Preisstruktur](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server).

### Hybrid-Cloud-Umgebung
{: #apvs-hybrid}

Sie können {{site.data.keyword.powerSys_notm}}s verwenden, um beliebige AIX- oder IBM i-Workloads Off-Premises von Ihrer vorhandenen Power Systems-Hardwareinfrastruktur auszuführen. Wenn Sie Ihre Workloads in der Public Cloud ausführen, können Sie alle Vorteile der Cloud nutzen, wie z. B. Self-Service, schnelle Bereitstellung, Elastizität und Konnektivität zu anderen IBM Cloud-Services. Auch wenn Ihre AIX- und IBM i-Workloads in der Cloud ausgeführt werden, bleiben dieselben einsatzfähigen, ausfallsicheren und einsatzbereiten Features erhalten, die die Power Systems-Hardware bietet. 

### Infrastrukturanpassung
{: #apvs-customization}

Sie können die folgenden Optionen konfigurieren und anpassen, wenn Sie eine {{site.data.keyword.powerSys_notm}}-Instanz erstellen:
* Anzahl der virtuellen Serverinstanzen
* Anzahl der Kerne
* Speicherkapazität
* Datendatenträgergröße und -typ (HDD oder SSD)
* Privates oder öffentliches Netz

### Eigenes Image verwenden
{: #apvs-own-image}

IBM stellt Ihnen den Bestand der AIX- und IBM i-Betriebssystemimages zur Verfügung, wenn Sie einen {{site.data.keyword.powerSys_notm}} erstellen. Sie können jedoch auch Ihr eigenes angepasstes AIX- oder IBM i-Betriebssystemimage verwenden, das Sie zuvor bereitgestellt und getestet haben. Weitere Informationen finden Sie unter [Angepasstes Image konfigurieren](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Hardwarespezifikationen
{: #apvs-hardware-specifications}

Die folgende IBM Power Systems-Hardware hostet {{site.data.keyword.powerSys_notm}}:

* Datenverarbeitung
  * [Power System E880 (9119-MHE) ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 TB Speicher
    * 8 x 16 Gigabit PCI Express Dual-Port Fibre Channel (FC)
    * 10 x 10 Gigabit Ethernet-SR PCI Express Dual-Port
  * [Power System S922 (9009-22A) ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 GB Speicher
    * 2 x 16 Gigabit PCI Express Dual-Port FC
    * 3 x 10 Gigabit Ethernet-SR PCI Express Dual-Port

* Speicher
  * Storewize V7000F(2076-AF6) Dual Controller
  * Storwize V7000 (2076-624) Dual Controller

* Netz
  * Cisco Nexus9000 93180YC-EX (10G)
  * Cisco Nexus9000 C9348GC-FXP (1G)

## Öffentliche und private Netze
{: #apvs-public-and-private}

Wenn Sie eine {{site.data.keyword.powerSys_notm}}-Instanz erstellen, können Sie eine private Netzschnittstelle oder eine öffentliche Netzschnittstelle auswählen. 

* Öffentliches Netz
  * Einfache und schnelle Methode, um eine Verbindung zu einer {{site.data.keyword.powerSys_notm}}-Instanz herzustellen.
  * IBM konfiguriert die Netzinfrastruktur so, dass eine sichere öffentliche Netzverbindung vom Internet zur {{site.data.keyword.powerSys_notm}}-Instanz hergestellt werden kann.
  * Die Konnektivität wird mithilfe einer IBM Cloud Virtual Router Appliance (VRA) und einer Direct Link Connect-Verbindung implementiert.
  * Schutz durch eine Firewall. Die folgenden sicheren Netzprotokolle werden unterstützt: 
    * SSH
    * HTTPS
    * Ping
    * IBM i 5250 Terminalemulation mit SSL (Port 992)

* Privates Netz
  * Ermöglicht den Ressourcen für Ihre {{site.data.keyword.powerSys_notm}}-Instanz, auf vorhandene {{site.data.keyword.cloud_notm}}-Ressourcen wie Bare-Metal-Server, Kubernetes-Container oder Cloudspeicher zuzugreifen. 
  * Verwendet eine Direct Link Connect-Verbindung, um Ihr IBM Cloud-Kontonetz und Ressourcen zu verbinden. Der Prozess der Erstellung einer Direct Link Connect-Verbindung kann einige Tage in Anspruch nehmen, da IBM Cloud Support den Link konfigurieren muss. 
  * Erforderlich für die Kommunikation zwischen {{site.data.keyword.powerSys_notm}}-Instanzen.

    Weitere Informationen zu verschiedenen Optionen für die Konfiguration eines privaten Netzes finden Sie unter [Privates Netz konfigurieren](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring).
    {: note}

In der folgenden Abbildung wird die Basiskonfiguration für ein öffentliches und privates Netz angezeigt:

![Datenfluss des Netzverkehrs für eine öffentliche oder private Verbindung](/images/power-iaas-network1.svg "Datenfluss des Netzverkehrs für eine öffentliche oder private Verbindung")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
