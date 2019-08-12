---

copyright:
  years: 2019

lastupdated: "2019-08-1"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:table: .aria-labeledby="caption"}

# Power Systems Virtual Server erstellen
{: #creating-power-virtual-server}

Führen Sie die folgenden Schritte aus, um einen {{site.data.keyword.powerSysFull}} zu erstellen und zu konfigurieren: 

1. Melden Sie sich beim [IBM Cloud-Katalog ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog){: new_window} mit Ihren Kontoberechtigungsnachweisen für IBM Cloud an. 
2. Geben Sie im Suchfeld des Katalogs **Power Systems Virtual Server** ein und klicken Sie auf die Kachel {{site.data.keyword.powerSys_notm}}.

    ![IBM Cloud-Katalog](./images/catalog-search-bar.png "IBM Cloud-Katalog")

3. Geben Sie Ihrem Service einen Namen und wählen Sie aus, wo Sie Ihre {{site.data.keyword.powerSys_notm}}-Instanz bereitstellen möchten. 

    ![Service und Regionsauswahl](./images/power-iaas-service-region.png "Service und Regionsauswahl")

4. Klicken Sie auf die Schaltfläche **Erstellen** unten auf der Webseite. 

    ![Schaltfläche 'Erstellen'](./images/power-iaas-create-button.png "Schaltfläche 'Erstellen'")

5. Nachdem Sie auf die Schaltfläche **Erstellen** geklickt haben, werden Sie zur Anzeige **Ressourcenliste** weitergeleitet.
6. Wählen Sie in der **Ressourcenliste** Ihren Service unter **Services** aus, um zur Anzeige **Verwalten** zu gelangen.

    ![IBM Cloud Ressourcenliste](./images/power-iaas-resource-list.png "IBM Cloud Ressourcenliste")

7. Klicken Sie von hier aus auf die Schaltfläche **Neu bereitstellen** .

    ![Bereitstellung eines neuen virtuellen Servers](./images/power-iaas-provision-new.png "Bereitstellung eines neuen virtuellen Servers")

8. Füllen Sie alle erforderlichen Felder aus, um eine neue Instanz erfolgreich zu erstellen:

     Der Preis wird im Abschnitt **Auftragsübersicht** dynamisch aktualisiert, wenn Sie die Felder ausfüllen, um eine {{site.data.keyword.powerSys_notm}}-Instanz zu erstellen. So können Sie auf einfache Weise eine kosteneffiziente {{site.data.keyword.powerSys_notm}}-Instanz erstellen, die Ihre Geschäftsanforderungen erfüllt.
{: tip}

    1. Füllen Sie alle Felder im Abschnitt **Virtuelle Server** aus. Wenn Sie mehrere Instanzen auswählen, werden Ihnen zusätzliche Optionen angezeigt.

      ![Erstellung einer neuen Power Virtual Server-Instanz](./images/console-virtual-instance.png "Erstellung einer neuen Power Virtual Server-Instanz")

    1. Wählen Sie aus, welchen Prozessor Sie verwenden möchten: **Dedizierter Prozessor** oder **Gemeinsam genutzter Prozessor**. Denken Sie daran, den gewünschten **Maschinentyp**, die Anzahl der Kerne und die Speicherkapazität durch Klicken auszuwählen. 

      ![Auswahl von Prozessor und System](./images/console-profile.png "Auswahl von Prozessor und System")

    1. Schließlich füllen Sie die Felder **Bootdatenträger**, **Angehängte Datenträger** und **Netzschnittstellen** so aus, wie von Ihrer Organisation vorgegeben. 

      ![Definition Ihrer Datenträger und Netzschnittstellen](./images/console-volume-network.png "Definition Ihrer Datenträger und Netzschnittstellen")

9. Akzeptieren Sie die **Nutzungsbedingungen** und klicken Sie auf die Schaltfläche **Erstellen**, um eine neue {{site.data.keyword.powerSys_notm}}-Instanz zu erstellen.

Die folgende Tabelle enthält Informationen zu den Felder von **Virtuelle Serverinstanz**:

<table>
<caption>Tabelle 1. Felder für neue Power Virtual Server-Instanz</caption>
<tr>
<th>Feld</th>
<th>Beschreibung</th>
</tr>
<tr>
<td>Anzahl der Instanzen</td>
<td>Geben Sie die Anzahl der Instanzen an, die für {{site.data.keyword.powerSys_notm}} erstellt werden sollen. Wenn Sie mehr als eine Instanz angeben, können Sie die folgenden Namenskonventionen und Zusammenstellungsregeln auswählen:
  <dl>
    <dt><strong>Keine Vorgabe</strong></dt>
  <dd>Wählen Sie diese Option aus, wenn Sie über keine Hostingvorgabe verfügen. </dd>
    <dt><strong>Anderer Server</strong></dt>
  <dd>Wählen Sie diese Option aus, wenn jede Instanz auf einem anderen Server gehostet werden soll. Sie können diese Option verwenden, wenn es sich um einen Einzelserverausfall handelt, der sich auf alle {{site.data.keyword.powerSys_notm}}-Instanzen auswirken kann. </dd>
  <dt><strong>Numerisches Präfix</strong></dt>
  <dd>Wählen Sie diese Option aus, um vor dem Namen des virtuellen Servers Ziffern hinzuzufügen. Wenn beispielsweise der erste {{site.data.keyword.powerSys_notm}}-Name <kbd>Austin</kbd> lautet, so ist der nächste Name der virtuellen Instanz <kbd>1Austin</kbd>.</dd>
  <dt><strong>Numerisches Postfix</strong></dt>
  <dd>Wählen Sie diese Option aus, um nach dem Namen des virtuellen Servers Ziffern hinzuzufügen. Wenn beispielsweise der erste {{site.data.keyword.powerSys_notm}}-Name <kbd>Rochester</kbd> lautet, so ist der nächste Name der virtuellen Instanz <kbd>Rochester1</kbd>.</dd>
  </dl>
  <p>
  <strong>Anmerkung:</strong> Wenn Sie mehrere Instanzen des virtuellen Servers erstellen, müssen Sie im Feld <strong>Gemeinsam nutzbar</strong> die Option <strong>Ein</strong> für jeden Datenträger auswählen, den Sie hinzufügen. Wenn Sie den Datenträger nicht gemeinsam nutzbar machen wollen, können Sie den Datenträger hinzufügen, nachdem Sie den virtuellen Server erstellt haben.
  </p>
   </td>
</tr>
<tr>
<td>Virtuelle Maschine fest verknüpfen</td>
<td>Wählen Sie <strong>Ein</strong> aus, um {{site.data.keyword.powerSys_notm}} fest mit einem Hostsystem zu verknüpfen. Wenn Sie <strong>Ein</strong> auswählen, kann der virtuelle Server nicht auf einen anderen Host verschoben werden. Durch die Auswahl von <strong>Ein</strong> kommt es dann beispielsweise bei einer Wartung des Hosts zu einer Betriebsunterbrechung. </td>
</tr>
<tr>
<td>Maschinentyp</td>
<td>Geben Sie den Maschinentyp an. Der von Ihnen ausgewählte Maschinentyp legt die Anzahl der Kerne und den verfügbaren Speicher fest. Weitere Informationen zu Hardwarespezifikationen finden Sie zum Beispiel unter <a href="https://www.ibm.com/downloads/cas/KQ4BOJ3N" target="_blank">S922</a> und <a href="https://www.ibm.com/downloads/cas/EE476WAP" target="_blank">E880</a>.</td>
</tr>
<tr>
<td>Kerne</td>
<td>Wählen Sie die Anzahl der Kerne für {{site.data.keyword.powerSys_notm}} aus. Wenn Sie <strong>Gemeinsam genutzter Prozessoren</strong> ausgewählt haben, können Sie die Anzahl der Kerne mit Inkrementen von 0,25 angeben. Gültige Werte für die Anzahl der Kerne sind beispielsweise 0,5, 1,25 und 2,75. Eine virtuelle CPU wird für alle 0,25 Nutzungsrechte zugeordnet. 

Wenn Sie Leistungsprobleme befürchten, können Sie <strong>Dedizierter Prozessor</strong> auswählen, weil der Prozessor dann Ihrem virtuellen Server dediziert zugeordnet ist und nicht gemeinsam genutzt genutzt wird. Weitere Informationen finden Sie im Leistungsvergleich von gemeinsam genutzten und dedizierten Prozessoren unter <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">How does Shared Processor Performance Compare to Dedicated Processors</a>.</td>
</tr>
<tr>
<td>Speicher</td>
<td>Wählen Sie die Speicherkapazität für {{site.data.keyword.powerSys_notm}} aus. Die Speicherkapazität, die Sie auswählen können, hängt von der Anzahl der ausgewählten Kerne ab. Für jeden von Ihnen ausgewählten Kern können Sie bis zu 64 GB zuordnen. Wenn Sie zum Beispiel vier Kerne auswählen, können Sie bis zu 256 GB Speicher zuordnen. </td>
</tr>
<tr>
<td>Bootdatenträger erstellen</td>
<td>Wählen Sie eine Version des Betriebssystemimage von AIX oder IBM i aus, das für Sie bereitgestellt wird, oder wählen Sie ein angepasstes Betriebssystemimage von AIX oder IBM i aus, das Sie zuvor On-Premises bereitgestellt haben. Lizenzinformationen zum Betriebssystem finden Sie bei IBM unter <a href="https://www-03.ibm.com/software/sla/sladb.nsf" target="_blank">Dokumente zu Lizenzinformationen</a>.

Wenn Sie Ihr eigenes angepasstes Image verwenden möchten, müssen Sie ein unterstütztes Technology Level des Betriebssystemimages von AIX oder IBM i für die Power Systems-Hardware verwenden, die Sie im Feld <strong>Maschinentyp</strong> ausgewählt haben. Weitere Informationen finden Sie unter <a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">Angepasstes Image konfigurieren</a>.</td>
</tr>
<tr>
<td>Angehängte Datenträger</td>
<td>Sie können entweder einen neuen Datenträger erstellen oder einen vorhandenen Datenträger anhängen, der bereits in Ihrem IBM Cloud-Konto definiert ist.
<dl>
  <dt><strong>Datenträger erstellen</strong></dt>
  <dd>Klicken Sie auf <strong>Hinzufügen</strong>, um einen neuen Datenträger zu erstellen, der verwendet werden kann, um mehr Speicher für Ihre {{site.data.keyword.powerSys_notm}}-Instanz zur Verfügung zu stellen. Wenn Sie mehreren Instanzen von {{site.data.keyword.powerSys_notm}} erlauben möchten, Daten auf denselben Datenträger zu speichern, müssen Sie im Feld <strong>Gemeinsam nutzbar</strong> die Option <strong>Ein</strong> auswählen.</dd>
  <dt><strong>Vorhandenen Datenträger anhängen</strong></dt>
  <dd>Wählen Sie einen vorhandenen Datenträger aus, um mehr Speicher für Ihre {{site.data.keyword.powerSys_notm}}-Instanz zur Verfügung zu stellen. Wenn die Liste keinen Datenträger anzeigt, den Sie zuvor verwendet haben, kann dies daran liegen, dass der Datenträger mit einem anderen IBM Cloud-Konto erstellt wurde. </dd>
</dl>
</td>
</tr>
<tr>
<td>Öffentliche Netze</td>
<td>Wählen Sie diese Option aus, um ein von IBM bereitgestelltes öffentliches Netz zu verwenden. Mit der Auswahl dieser Option sind Kosten verbunden. Weitere Informationen finden Sie unter <a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">Öffentliche und private Netze</a>.
</td>
</tr>
<tr>
<td>Private Netze</td>
<td>Klicken Sie auf <strong>Hinzufügen</strong>, um ein neues privates Netz für den virtuellen Server zu ermitteln. Wenn Sie bereits ein privates Netz hinzugefügt haben, können Sie es aus der Liste auswählen. Weitere Informationen finden Sie unter <a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">Privates Netz konfigurieren</a>.</td>
</tr></table>
