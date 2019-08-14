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

# Création d'une instance Power Systems Virtual Server
{: #creating-power-virtual-server}

Pour créer et configurer une instance {{site.data.keyword.powerSysFull}}, procédez comme suit :

1. Connectez-vous au [catalogue d'IBM Cloud ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/catalog){: new_window} avec vos informations d'authentification au compte IBM Cloud. 
2. Dans la zone de recherche du catalogue, entrez **Power Systems Virtual Server** et cliquez sur la vignette {{site.data.keyword.powerSys_notm}}.

    ![Catalogue IBM Cloud](./images/catalog-search-bar.png "Catalogue IBM Cloud")

3. Indiquez un nom pour votre service et choisissez l'emplacement où déployer votre instance {{site.data.keyword.powerSys_notm}}.

    ![Service et sélection d'une région](./images/power-iaas-service-region.png "Service et sélection d'une région")

4. Cliquez sur le bouton **Créer** au bas de la page Web.

    ![Bouton Créer](./images/power-iaas-create-button.png "Bouton Créer")

5. Après avoir cliqué sur le bouton **Créer**, vous êtes redirigé vers le panneau **Liste de ressources**.
6. Dans la **liste de ressources**, sélectionnez votre service dans **Services** pour accéder au panneau **Gérer**.

    ![Liste de ressources d'IBM Cloud](./images/power-iaas-resource-list.png "Liste de ressources d'IBM Cloud")

7. Dans cette liste, cliquez sur le bouton de **mise à disposition d'un nouvel élément**.

    ![Mise à disposition d'un nouveau serveur virtuel](./images/power-iaas-provision-new.png "Mise à disposition d'un nouveau serveur virtuel")

8. Renseignez toutes les zones obligatoires pour réussir à créer une nouvelle instance :

     Le tarif est mis à jour de manière dynamique dans la section **Récapitulatif de la commande** à mesure que vous renseignez les zones pour créer une instance {{site.data.keyword.powerSys_notm}}. Cela vous permet de créer facilement une instance {{site.data.keyword.powerSys_notm}} pour répondre à vos besoins métier.
     {: tip}

    1. Remplissez toutes les zones de la section **Serveurs virtuels**. Si vous sélectionnez plusieurs instances, de nouvelles options sont disponibles.

      ![Création d'une nouvelle instance Power Systems Virtual Server](./images/console-virtual-instance.png "Création d'une nouvelle instance Power Systems Virtual Server")

    1. Sélectionnez si vous souhaitez un **processeur dédié** ou un **processeur partagé**. N'oubliez pas de cliquez sur le **type de machine** ainsi que sur le nombre de coeurs et la quantité de mémoire désirés.

      ![Sélection du processeur et du système](./images/console-profile.png "Sélection du processeur et du système")

    1. Et enfin, complétez les zones **Volume d'amorçage**, **Volumes connectés** et **Interfaces réseau** suivant les instructions fournies par votre organisation.

      ![Définition de vos volumes et interfaces réseau](./images/console-volume-network.png "Définition de vos volumes et interfaces réseau")

9. Acceptez les **conditions d'utilisation** et cliquez sur le bouton **Créer** pour mettre à disposition une nouvelle instance {{site.data.keyword.powerSys_notm}}.

Le tableau suivant fournit des informations sur les zones **Instance de serveur virtuel** :

<table>
<caption>Tableau 1. Zones de la nouvelle instance Power Virtual Server</caption>
<tr>
<th>Zone</th>
<th>Description</th>
</tr>
<tr>
<td>Nombre d'instances</td>
<td>Indiquez le nombre d'instances que vous souhaitez créer pour le service {{site.data.keyword.powerSys_notm}}. Si vous indiquez plusieurs instances, vous pouvez sélectionner les règles de colocalisation et de convention de dénomination suivantes :
  <dl>
    <dt><strong>Aucune préférence</strong></dt>
  <dd>Sélectionnez cette option si vous n'avez pas de préférence d'hébergement.</dd>
    <dt><strong>Serveur différent</strong></dt>
  <dd>Sélectionnez cette option pour que chaque instance soit hébergée sur un serveur distinct.  Vous pouvez utiliser cette option si vous craignez l'éventualité d'une panne de serveur unique pouvant affecter toutes vos instances {{site.data.keyword.powerSys_notm}}. </dd>
  <dt><strong>Préfixe numérique</strong></dt>
  <dd>Sélectionnez cette option pour ajouter des numéros avant le nom du serveur virtuel. Par exemple, si le nom de la première instance {{site.data.keyword.powerSys_notm}} est <kbd>Austin</kbd>, le nom de l'instance virtuelle suivante sera <kbd>1Austin</kbd></dd>
  <dt><strong>Suffixe numérique</strong></dt>
  <dd>Sélectionnez cette option pour ajouter des numéros après le nom du serveur virtuel. Par exemple, si le nom de la première instance {{site.data.keyword.powerSys_notm}} est <kbd>Rochester</kbd>, le nom de l'instance virtuelle suivante sera <kbd>Rochester1</kbd>.</dd>
  </dl>
  <p>
  <strong>Remarque :</strong> lorsque vous créez plusieurs instances du serveur virtuel, vous devez sélectionner <strong>Activé</strong> dans la zone <strong>Partageable</strong> de chaque volume de données que vous ajoutez. Si vous ne souhaitez pas que votre volume de données puisse être partagé, vous pouvez ajouter le volume de données après avoir créé le serveur virtuel.
  </p>
   </td>
</tr>
<tr>
<td>Serveur virtuel PIN</td>
<td>Sélectionnez <strong>Activé</strong> pour verrouiller l'instance {{site.data.keyword.powerSys_notm}} sur un système hôte. Si vous cliquez sur <strong>Activé</strong>, le serveur virtuel ne peut pas être déplacé sur un autre hôte. Par exemple, en sélectionnant <strong>Activé</strong>, vous pourriez obtenir une panne lors de la maintenance de l'hôte.</td>
</tr>
<tr>
<td>Type machine</td>
<td>Spécifiez le type de machine. Le type de machine que vous sélectionnez détermine le nombre de coeurs et la quantité de mémoire disponible. Pour plus d'informations sur les spécifications matérielles, voir <a href="https://www.ibm.com/downloads/cas/KQ4BOJ3N" target="_blank">S922</a> et <a href="https://www.ibm.com/downloads/cas/EE476WAP" target="_blank">E880</a>.</td>
</tr>
<tr>
<td>Coeurs</td>
<td>Sélectionnez le nombre de coeurs pour {{site.data.keyword.powerSys_notm}}. Si vous avez sélectionné <strong>Processeur partagé</strong>, vous pouvez spécifier le nombre de coeurs par incréments de 0,25. Par exemple, les valeurs de coeur valides sont : 0,5, 1,25 et 2,75. Une UC virtuelle est allouée à chaque incrément de 0,25.

Si vous craignez d'éventuels problèmes liés aux performances, vous pouvez sélectionner <strong>Processeur dédié</strong> car le processeur est dédié à votre serveur virtuel sans être partagé. Pour plus d'informations, voir <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">How does Shared Processor Performance Compare to Dedicated Processors</a>.</td>
</tr>
<tr>
<td>Mémoire</td>
<td>Sélectionnez la quantité de mémoire pour l'instance {{site.data.keyword.powerSys_notm}}. La quantité de mémoire que vous pouvez sélectionner dépend du nombre de coeurs que vous avez sélectionnés. Vous pouvez allouer jusqu'à 64 Go à chaque coeur que vous sélectionnez. Par exemple, si vous avez sélectionné quatre coeurs, vous êtes autorisé à sélectionner jusqu'à 256 Go de mémoire. </td>
</tr>
<tr>
<td>Créer un volume d'amorçage</td>
<td>Sélectionnez une version parmi le stock d'images de système d'exploitation AIX ou IBM i fournies pour vous ou sélectionnez une image personnalisée de système d'exploitation AIX ou IBM i que vous avez déjà déployée sur site. Pour obtenir des informations sur les licences des systèmes d'exploitation, voir la documentation IBM <a href="https://www-03.ibm.com/software/sla/sladb.nsf" target="_blank">License Information documents</a>.

Si vous voulez fournir votre propre image personnalisée, vous devez utiliser un niveau de technologie compatible de l'image de système d'exploitation AIX ou IBM i pour le matériel Power Systems que vous avez sélectionné dans la zone <strong>Type machine</strong>. Pour plus d'informations, voir <a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">Configuration d'une image personnalisée</a>.</td>
</tr>
<tr>
<td>Volumes de données connectés</td>
<td>Vous pouvez créer un nouveau volume de données ou connecter un volume de données existant déjà défini dans votre compte IBM Cloud.
<dl>
  <dt><strong>Créer un volume de données</strong></dt>
  <dd>Cliquez sur <strong>Ajouter</strong> pour créer un nouveau volume de données pouvant être utilisé pour obtenir du stockage supplémentaire pour votre instance {{site.data.keyword.powerSys_notm}}. Pour autoriser plusieurs instances de {{site.data.keyword.powerSys_notm}} à écrire des données dans le même volume de données, vous devez sélectionner <strong>Activé</strong> dans la zone <strong>Partageable</strong>. </dd>
  <dt><strong>Connecter un volume de données existant</strong></dt>
  <dd>Sélectionnez un volume de données existant pour obtenir du stockage supplémentaire pour votre instance {{site.data.keyword.powerSys_notm}}. Si dans la liste vous ne trouvez pas un volume de données que vous avez déjà utilisé, il est possible que ce volume de données ait été créé avec un autre compte IBM Cloud.</dd>
</dl>
</td>
</tr>
<tr>
<td>Réseaux publics</td>
<td>Sélectionnez cette option pour utiliser un réseau public fourni par IBM. La sélection de cette option a un coût. Pour plus d'informations, voir <a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">Réseau public et réseau privé</a>.
</td>
</tr>
<tr>
<td>Réseaux privés</td>
<td>Cliquez sur <strong>Ajouter</strong> pour identifier un nouveau réseau privé pour le serveur virtuel. Si vous avez déjà ajouté un réseau privé, vous pouvez le sélectionner dans la liste. Pour plus d'informations, voir la rubrique sur la <a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">configuration d'un réseau privé</a>.</td>
</tr></table>
