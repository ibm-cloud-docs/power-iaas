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

# Opciones Alta disponibilidad y Recuperación tras desastre en servidores virtuales de Power Systems
{: #ha-dr}

La instancia del {{site.data.keyword.powerSys_notm}} reinicia los servidores virtuales en un sistema host distinto si se produce un error de hardware. Este proceso proporciona prestaciones básicas de Alta disponibilidad (HA) para el servicio {{site.data.keyword.powerSys_notm}}.
{:shortdesc}

Si desea más soluciones de Alta disponibilidad o Recuperación tras desastre (DR), puede desplegar las siguientes aplicaciones en su entorno del {{site.data.keyword.powerSys_notm}}.

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

Puede utilizar un modelo de suscripción mensual cuando adquiera PowerHA SystemMirror for AIX Standard Edition. Para obtener más información, consulte [Opciones de precios mensuales de Standard Edition![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html).

Después de adquirir el software, puede descargarlo de [IBM Entitled Systems Support (ESS) ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/eserver/ess). Puede instalar PowerHA SystemMirror para AIX en el servidor virtual que se está ejecutando en el entorno del {{site.data.keyword.powerSys_notm}}. Para obtener las instrucciones de instalación, consulte [Instalación de PowerHA SystemMirror ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html).

Consulte la información siguiente para implementar PowerHA SystemMirror for AIX en el entorno del {{site.data.keyword.powerSys_notm}}.

* Cuando se crean los servidores virtuales que forman parte del clúster de PowerHA SystemMirror, debe seleccionar **Servidor distinto** en el campo **Reglas de colocalización**. ![Muestra el campo de reglas de colocalización](/images/hadr2.png "Muestra el campo de reglas de colocalización")

* Cuando se crean volúmenes de almacenamiento (discos) para los servidores virtuales que forman parte del clúster de
PowerHA SystemMirror, debe seleccionar **Activado** en el campo **Se puede compartir**.
![Muestra las reglas del campo Se puede compartir](/images/hadr1.png "Muestra el campo Se puede compartir")

* Al utilizar el servicio {{site.data.keyword.powerSys_notm}}, no se dispone de acceso a la HMC, el VIOS y al sistema host. Por lo tanto, las funciones de PowerHA SystemMirror que requieren acceso a estas prestaciones como, por ejemplo Alta disponibilidad optimizada para recursos (ROHA - Resource Optimized High Availability) y Política de parada de nodos activo (ANHP - Active Node Halt Policy), no están disponibles.

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## Continuidad empresarial mediante copia de seguridad y restauración
{: #ha-dr-ha-business}

{{site.data.keyword.cloud}} no realiza copia de seguridad de la configuración ni de los datos del {{site.data.keyword.powerSys_notm}}.

Puede utilizar la interfaz de usuario del {{site.data.keyword.cloud_notm}} para realizar una copia de seguridad del servidor virtual en el Almacenamiento de objetos del {{site.data.keyword.cloud_notm}}. Es posible utilizar este proceso para restaurar el servidor virtual en el caso que se produzca un error grave. Para obtener más información, consulte [Almacenamiento de objetos en la nube ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started).
