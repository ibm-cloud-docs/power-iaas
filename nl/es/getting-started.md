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

# Iniciación a los servidores virtuales de Power Systems
{: #getting-started}


{{site.data.keyword.powerSysFull}} es una oferta de infraestructura como servicio que el usuario puede utilizar para desplegar un servidor virtual, también se conoce como partición lógica (LPAR), en cuestión de minutos.
{:shortdesc}

Puede desplegar rápidamente los servidores virtuales de Power Systems para satisfacer determinadas necesidades empresariales. Con el {{site.data.keyword.powerSys_notm}} puede crear un entorno de nube híbrida que le permita controlar fácilmente las demandas de carga de trabajo.

Los servidores virtuales de Power Systems pueden ejecutar cargas de trabajo de AIX o de IBM i en diferentes ubicaciones geográficas.

## Terminología
{: #gs-terminology}

Antes de crear un servidor virtual, debe saber cuál es la diferencia terminológica entre un **servicio** {{site.data.keyword.powerSys_notm}} y una **instancia** de {{site.data.keyword.powerSys_notm}}. Piense en el **servicio** {{site.data.keyword.powerSys_notm}} como un contenedor de todas las **instancias** de {{site.data.keyword.powerSys_notm}} en una ubicación geográfica en concreto. El **servicio** {{site.data.keyword.powerSys_notm}} está disponible desde la **Lista de recursos** en la IU de {{site.data.keyword.cloud}}. El servicio puede contener varias **instancias** de {{site.data.keyword.powerSys_notm}}.

Por ejemplo, puede tener dos **servicios** {{site.data.keyword.powerSys_notm}}, uno en Dallas y otro en Washington DC. Cada servicio puede contener varias **instancias** de {{site.data.keyword.powerSys_notm}}.

## Antes de empezar
{: #gs-before-you-begin}

Antes de crear su primer instancia del servidor virtual de Power Systems, consulte los siguientes requisitos previos:

1. {: hide-dashboard} Cree una cuenta de IBM Cloud. Para crear una cuenta de IBM Cloud, consulte [Regístrese en IBM Cloud ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/registration){: new_window}.

2. Cree una clave SSH pública y privada que pueda utilizar para conectarse de forma segura a su {{site.data.keyword.powerSys_notm}}. Para crear una clave SSH pública y privada, consulte [Adición de una clave SSH ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)

3. (Opcional) Si desea utilizar una imagen personalizada para los sistemas operativos AIX o IBM i, debe crear un almacenamiento de objeto de IBM Cloud y cargar la imagen. Para obtener más información, consulte [Configuración de una imagen personalizada](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

4. (Opcional) Si desea utilizar una red privada para conectarse a una instancia de {{site.data.keyword.powerSys_notm}}, debe solicitar el servicio Direct Link Connect. Para obtener más información, consulte [Solicitud de IBM Cloud Direct Link Connect desde la consola de la IU](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## Pasos siguientes
{: #gs-next-steps}

Con una cuenta de IBM Cloud y una clave SSH pública y privada, el usuario ya está listo para [crear el servicio {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).
