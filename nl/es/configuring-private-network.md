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

# Configuración de los servidores virtuales de Power Systems con un red privada
{: #cpn-configuring}

Puede utilizar una red privada con el {{site.data.keyword.powerSysFull}} para conectar de forma segura su entorno local con el entorno no local del {{site.data.keyword.cloud_notm}}. En una red privada, puede acceder a los recursos de {{site.data.keyword.cloud_notm}} e interconectarlos con otros servidores virtuales.
{:shortdesc}

Puede utilizar una de las opciones siguientes para crear una red privada que conecte su entorno local con el entorno de {{site.data.keyword.cloud_notm}}:

1. La VPN con SSL de **{{site.data.keyword.cloud_notm}} con el servidor puente**
   * Puede utilizar el servicio VPN con SSL de {{site.data.keyword.cloud_notm}} para establecer una conexión con la red existente de su {{site.data.keyword.cloud_notm}}. Dentro de la red de {{site.data.keyword.cloud_notm}}, puede utilizar una máquina virtual de {{site.data.keyword.cloud_notm}} como servidor puente para conectarla con la instancia del {{site.data.keyword.powerSys_notm}}.
   * Debe utilizar un servidor puente porque no se puede utilizar una conexión VPN para establecer una conexión directamente con la instancia del {{site.data.keyword.powerSys_notm}}.
   * Esta opción se suele utilizar para gestionar sus entornos. Esta opción no se recomienda para las cargas de trabajo de producción.
   * Para obtener más información sobre cómo configurar esta opción, consulte [Configuración de la VPN con SSL](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) y [Petición de un dispositivo direccionador virtual](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

2. VPN de IPSec de **{{site.data.keyword.cloud_notm}} con el dispositivo direccionador virtual (VRA - Virtual Router Appliance) de IBM Cloud**
   * Puede utilizar el servicio VPN con IPSec de {{site.data.keyword.cloud_notm}} para establecer una conexión con la red existente de su {{site.data.keyword.cloud_notm}}. Dentro de la red de {{site.data.keyword.cloud_notm}}, puede utilizar el VRA de IBM Cloud para conectarse a su instancia del {{site.data.keyword.powerSys_notm}}.
   * Debe utilizar un VRA porque no se puede utilizar una conexión VPN para establecer una conexión directamente con la instancia del {{site.data.keyword.powerSys_notm}}.
   * Esta opción se suele utilizar para gestionar sus entornos. Esta opción no se recomienda para las cargas de trabajo de producción.
   * Para obtener más información sobre cómo configurar esta opción, consulte [Configuración de la VPN con IPSec](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) y [Petición de un dispositivo direccionador virtual](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

3. **Direct Link Connect con el dispositivo direccionador virtual (VRA) de IBM Cloud**
   * Puede solicitar el servicio Direct Link Connect de IBM que conecta su red local a la red de IBM Cloud utilizando el dispositivo direccionador virtual (VRA - Virtual Router Appliance) de IBM Cloud.
   * Esta opción proporciona un alto rendimiento entre la red local y la red de IBM Cloud.
   * Para realizar el pedido de Direct Link Connect, complete los pasos del tema [Solicitud de IBM Cloud Direct Link Connect desde la consola de la IU](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).
   * Hay ciertas direcciones IP que no puede utilizar con el servicio Direct Link Connect. Para obtener más información, consulte [Limitaciones estrictas en asignaciones de IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).
