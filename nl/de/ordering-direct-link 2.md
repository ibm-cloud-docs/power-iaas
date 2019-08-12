---

copyright:
  years: 2019

lastupdated: "2019-06-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}


# IBM Cloud Direct Link Connect für Power Systems Virtual Servers bestellen
{: #ordering-direct-link-connect}

Eine Option für die Konfiguration eines privaten Netzes mit {{site.data.keyword.powerSys_notm}} ist die Verwendung des Direct Link Connect-Service. Der Direct Connect Link-Service stellt eine Verbindung her, die von Ihrer {{site.data.keyword.powerSys_notm}}-Instanz aus Zugriff auf {{site.data.keyword.cloud}}-Ressourcen ermöglicht. Der Direct Link Connect-Service wird auch verwendet, um Ihr On-Premises-Netz mit dem IBM Cloud-Netz zu verbinden, indem die Virtual Router Appliance (VRA) der IBM Cloud verwendet wird.


Sie können auch die Konsole der Benutzerschnittstelle von {{site.data.keyword.cloud_notm}} verwenden, um den Direct Link Connect-Service zu bestellen. Um eine Verbindung zu Ihrer {{site.data.keyword.powerSys_notm}}-Umgebung herzustellen, sollten Sie zwei direkte Verbindungsverbindungsverbindungen bestellen. Direct Link Connect ist ein separater Service des {{site.data.keyword.powerSys_notm}}-Service. Die Kosten für Direct Link Connect finden Sie unter [Preisstruktur für IBM Cloud Direct Link](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect){: new_window}.

## Vorbereitende Schritte
{: #before-direct-link-connect}

* Überprüfen Sie, dass Ihr {{site.data.keyword.cloud}}-Konto über die richtigen Berechtigungen verfügt, um den Direct Link Connect-Service zu bestellen. 
* Lesen Sie die folgenden Themen, um ein grundlegendes Verständnis des Konzepts des Direct Link Connect-Service zu erlangen: 
  * [Konzepte von Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
  * [Details zu Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
  * [Einschränkungen bei Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
  * [Strikte Einschränkungen bei IP-Zuweisungen](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Schritte bei der Bestellung von Direct Link Connect
{: #steps-to-order-direct-link-connect}

Führen Sie die folgenden Schritte aus, um den Direct Link Connect-Service zu bestellen, der eine Verbindung zur {{site.data.keyword.powerSys_notm}}-Instanz erstellt:

1. Melden Sie sich beim [IBM Cloud-Katalog ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog){: new_window} mit Ihren Kontoberechtigungsnachweisen für IBM Cloud an. Ihr Konto muss über die richtigen Berechtigungen zum Bestellen des Direct Link Connect-Service verfügen. 

1. Klicken Sie im Abschnitt **Netzbetrieb** auf die Kachel **Direct Link Connect**.
![Katalogkachel für Direct Link](/images/directlink1.png "Katalogkachel für Direct Link ")

1. Klicken Sie im Katalogeintrag für Direct Link Connect auf **Erstellen**.

1. Klicken Sie auf der Seite von IBM Cloud Direct Link auf **Direct Link Connect bestellen**.

1. Füllen Sie auf der Seite zum Erstellen der IBM Cloud Direct Link Connect-Verbindung die folgenden Felder aus. 

   Wenn Sie die folgenden Felder zum Erstellen des Direct Link Connect-Service ausfüllen, wird der Preis automatisch aktualisiert, um Ihre Auswahlen widerzuspiegeln. {:note}

   <dl>
   <dt><strong>Direct Link-Instanzname</strong><dt>
   <dd>Geben Sie den Namen ein, der den Zweck der Direct Link Connect beschreibt.</dd>
   <dt><strong>Standort</strong><dt>
   <dd>Wählen Sie denselben Standort wie für die {{site.data.keyword.powerSys_notm}}-Instanz aus. Die folgende Tabelle gibt den Standort der {{site.data.keyword.powerSys_notm}}-Instanz und die entsprechende Direct Link Connection-Option an:
   <table>
   <caption>Tabelle 1. Standortoptionen für Direct Link Connection</caption>
   <tr>
   <th>Standort von Power Systems Virtual Server</th>
   <th>Standort von Direct Link Connect</th>
   </tr>
   <tr>
   <td>Dallas, TX US</td>
   <td>Dallas 4</td>
   </tr>
   <tr>
   <td>Washington D.C, US</td>
   <td>Washington 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Netzbetreiber</strong><dt>
   <dd>Sie müssen <strong>MEGAPORT</strong> aus der Liste auswählen. </dd>
   <dt><strong>Verbindungsgeschwindigkeit</strong><dt>
   <dd>Wählen Sie die Verbindungsgeschwindigkeit aus, die Ihren Workloadanforderungen entspricht. Die empfohlene Auswahl für dieses Feld ist 1000 MB/s. </dd>
   <dt><strong>Routing-Option</strong><dt>
   <dd>Wählen Sie <b>Lokales Routing (Kostenlos)</b> aus, um auf alle Datenzentren zuzugreifen, die mit dem Standort verbunden sind, den Sie im Feld <b>Standort</b> eingegeben haben. Wählen Sie <b>Globales Routing</b> aus, um auf alle IBM Cloud-Rechenzentren weltweit zuzugreifen. </dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>Sie müssen die BGP ASN-Nummer für den jeweiligen Standort von Direct Link Connect in die folgenden Tabelle eingeben. <table>
   <caption>Tabelle 2. BGP ASN-Nummer für jeweiligen Standort</caption>
   <tr>
   <th>Standort von Direct Link Connect</th>
   <th>BGP ASN-Nummer</th>
   </tr>
   <tr>
   <td>Dallas 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>Washington 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>VRF auswählen</strong><dt>
   <dd>Wählen Sie die Option für virtuelle Routenwahl und Weiterleitung (VRF) für die Verbindung aus. Wenn für Ihr Konto kein VRF angegeben ist, wird dieses Feld nicht angezeigt. Sie können weiterhin den Direct Link Connect-Service ohne Auswahl von VRF erstellen.</dd>
   <dd>
    Die folgende Abbildung ist ein Beispiel für die Felder von Direct Link Connect.
   ![Zeigt die ausgefüllten Felder von Direct Link](/images/directlink2.png "Zeigt die ausgefüllten Felder von Direct Link")
   </dd>
   </dl>
1. Lesen Sie die Rahmenvereinbarung und wählen Sie das Kontrollkästchen aus. Sie müssen die Rahmenvereinbarung lesen, da sie wichtige technische Informationen enthält, die Sie verstanden haben müssen, bevor Sie fortfahren. 

1. Klicken Sie auf **Erstellen**. Die folgende Nachricht wird angezeigt, wenn Ihre Anforderung erfolgreich übergeben wurde.![Zeigt die Nachricht über die erfolgreiche Übergabe der Direct Link Connect-Anforderung.](/images/directlink3.png "Zeigt die Nachricht über die erfolgreiche Übergabe der Direct Link Connect-Anforderung.")

1. Klicken Sie auf den Link **Fallnummer** für den Direct Link Connect-Service. Die Informationen in der Fallnummer werden verwendet, um die Direct Link Connect-Daten zum Erstellen einer Verbindung zu Ihrer {{site.data.keyword.powerSys_notm}}-Instanz zu ermitteln.

  Das Team von IBM Cloud Support benötigt bis zu drei Werktage, um die Direct Link Connect-Verbindung zu erstellen.
  {: note}

1. Öffnen Sie einen neuen Fall für das Support-Team von {{site.data.keyword.powerSys_notm}}, um eine Verbindung zur {{site.data.keyword.powerSys_notm}}-Instanz mithilfe des Direct Link Connect-Service zu erstellen. Geben Sie im {{site.data.keyword.powerSys_notm}}-Fall die Direct Link Connect-Fallnummer an. Der {{site.data.keyword.powerSys_notm}}-Fall wird mit einer Service-ID aktualisiert. Informationen zum Öffnen des Falls finden Sie unter [Hilfe und Unterstützung anfordern](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support).

1. Geben Sie die Service-ID aus der {{site.data.keyword.powerSys_notm}}-Fallnummer in die Direct Link Connect-Fallnummer ein. Wenn die Direct Link Connect-Verbindung erstellt wird, wird die Direct Link Connect-Fallnummer geschlossen. Es folgt ein Beispiel für die Netzinformationen, die im Fall angezeigt werden:


  ```
  Link Speed:                  1000 Mbps
  Location:                    Washington 2
  Network Provider:            MEGAPORT
  IBM IP Address:              10.254.0.25/30
  Customer IP Address:         10.254.0.26/30
  Service Key:                 None
  BGP ASN:                     64999
  Network Identifier:          1748523-1
  Date Created:                2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. Verwenden Sie diese Informationen aus der Direct Link Connect-Fallnummer und geben Sie die folgenden Netzinformationen in den {{site.data.keyword.powerSys_notm}}-Fall ein:


  ```
  Customer name:
  Customer account ID:
  Direct Link Connect subnet:
  Power Systems Virtual Server network IP address:
  IBM Cloud IP address:
  Power Systems Virtual Server network ASN:
  IBM Cloud ASN:
  Private Network ID (1):
  Private Network ID (2):
  Private Network ID (3):
  ```
  {: codeblock}

1. Der {{site.data.keyword.powerSys_notm}}-Fall wird geschlossen, wenn die Direct Link Connect-Verbindung so konfiguriert wurde, dass sie mit Ihrer {{site.data.keyword.powerSys_notm}}-Instanz kommuniziert. 
