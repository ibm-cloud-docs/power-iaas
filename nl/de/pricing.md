---

copyright:
  years: 2019

lastupdated: "2019-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Preisstruktur für Power Systems Virtual Server on IBM Cloud
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} wird in ausgewählten Regionen mit Scale-out-LPARS (LPARS, logische Partitionen) mit bis zu 15 Kernen und 320 GB Speicher angeboten und ebenfalls mit Unternehmens-LPARS mit bis zu 143 Kernen und 8192 GB Speicher. Mit diesen Optionen kann {{site.data.keyword.powerSys_notm}} alle Workloadanforderungen für Ihr Unternehmen erfüllen. Die Leistungen werden monatlich in Rechnung gestellt.
{:shortdesc}

## Monatliche Nutzung
{: #pricing-monthly-usage}

Für {{site.data.keyword.powerSys_notm}}-Instanzen wird eine monatliche Gebühr erhoben, die nach Stundenanteilen berechnet wird. Wenn Sie in der Monatsmitte Ressourcen zu einer LPAR hinzufügen, spiegelt die monatliche Rechnung für die LPAR die Ressourcenänderung und die Gebühr für die LPAR, die nach Stundenanteilen berechnet wird, wider. 

### Beispiel für monatliche Nutzung
{: #pricing-monthly-usage-example}

Im folgenden Beispiel kaufen Sie eine {{site.data.keyword.powerSys_notm}}-Instanz mit 1 Kern und 8 GB Speicher sowie 150 GB Platte und führen diese Instanz auf dem Betriebssystem AIX 7200-03-02 mit einem Grundpreis von 250,57 $ pro Monat (0,343 $ pro Stunde) aus. Im Laufe des Monats fügen Sie mehr Speicher hinzu. Der neue Preis für die LPAR beträgt nun 339,45 $ pro Monat (0,465 $ pro Stunde). Die monatliche Rechnung wird für die einzelnen bereitgestellten Ressourcen anteilmäßig nach Stunden berechnet. 

| Abgelaufene Stunden im Monat   | Gebührenpflichtige Menge |  LPAR-Beschreibung    |
| ----------------------------- | ----------------- | --------------------  |
| 300 Stunden      | 300 Std. x 251 $/Monat = 103$  | 1 Kern, 8 GB Speicher, 150 GB Platte, AIX    |
| 430 Stunden      | 430 Std. x 339 $/Monat = 200$  | 1 Kern, 16 GB Speicher, 150 GB Platte, AIX  |
| 730 Stunden (monatlicher Gesamtbetrag)  | 103 $ + 200 $ = 303 $ (monatlicher Gesamtbetrag)  |   1 Kern, 16 GB Speicher, 150 GB Platte, AIX |
{: caption="Tabelle 1. Beispiel für monatliche LPAR-Gebühren" caption-side="top"}

In diesem Beispiel werden die LPAR-Ressourcen nach Ablauf von 300 Stunden des Monats von 8 GB Speicher auf 16 GB Speicher erhöht. Der monatliche Gesamtpreis für die LPAR (303 $) wird anteilmäßig nach Stunden auf Grundlage des monatlichen Preises für die LPAR berechnet.

## Instanzgrundpreis
{: #pricing-base-instance-prices}

Der Grundpreis für die Instanz hängt von den Optionen wie Maschinentyp, Anzahl der Kerne, Speichermenge usw. ab, die Sie auswählen, wenn Sie die {{site.data.keyword.powerSys_notm}}-Instanz erstellen. Wenn Sie Ihre virtuelle Serverinstanz erstellen, wird der zugehörige monatliche Gebührensatz angezeigt. Weitere Informationen finden Sie unter [{{site.data.keyword.powerSys_notm}} erstellen](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

## Betriebssysteme
{: #pricing-operating-systems}

Im folgenden finden Sie die Images, die IBM Ihnen zur Verfügung stellt: 
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

Sie können Ihr eigenes  angepasstes Image für eine {{site.data.keyword.powerSys_notm}}-Instanz verwenden, es wird jedoch immer noch eine Betriebssystemlizenz für IBM Cloud erworben. Sie können keine vorhandene Lizenz für AIX oder IBM i für LPARs in einer {{site.data.keyword.powerSys_notm}}-Instanz verwenden. Wenn Sie ein angepasstes Image oder ein bereitgestelltes Image verwenden, wird Ihnen derselbe Preis berechnet. Weitere Informationen finden Sie unter [Angepasstes Image konfigurieren](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Ende der Rechnungsstellung
{: #pricing-end-of-billing}

Der monatliche Abrechnungszyklus wird beendet, wenn Sie die LPAR löschen. Wenn Sie Ihre Infrastruktur als Antwort auf die Workloadanforderungen nach oben und unten skalieren, berücksichtigt Ihre Rechnung den Zeitpunkt der Änderung der LPAR-Bereitstellung. Wenn Sie die LPAR stoppen, wird der Abrechnungsvorgang nicht gestoppt (es fallen weiterhin Gebühren an). Sie müssen die LPAR löschen, um den Abrechnungszyklus zu stoppen. 
