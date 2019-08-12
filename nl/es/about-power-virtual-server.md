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

# Acerca de los servidores virtuales de Power Systems
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} utiliza la plataforma existente de IBM Cloud para crear servidores virtuales de Power Systems, que también se conocen como particiones lógicas (LPAR), que se ejecutan en el hardware de IBM Power Systems con el hipervisor PowerVM.
{:shortdesc}

Los servidores virtuales de Power Systems son una forma de infraestructura como servicio (IaaS - Infrastructure as a service). Con el servicio {{site.data.keyword.powerSys_notm}}, puede crear y desplegar de forma rápida uno o varios servidores virtuales que están en ejecución en los sistemas operativos AIX o IBM i en una nube pública. Después de suministrar el servidor virtual en la nube, es responsabilidad del usuario asegurarse de que el sistema operativo AIX o IBM i sea seguro.

## Características principales
{: #apvs-key-features}

A continuación encontrará algunas de las características principales del {{site.data.keyword.powerSys_notm}}.

### Facturación directa
{: #apvs-billing}

{{site.data.keyword.powerSys_notm}} utiliza una tarifa de facturación mensual que incluye las licencias de los sistemas operativos AIX e IBM i. La tarifa de facturación mensual se prorratea en horas según los recursos que se hayan desplegado en la instancia del {{site.data.keyword.powerSys_notm}} durante el mes. Cuando se crea la instancia del {{site.data.keyword.powerSys_notm}}, se puede ver el coste total de la configuración en base a las opciones que se hayan especificado.  Es posible identificar rápidamente las opciones de configuración que proporcionan el mejor valor según sus necesidades empresariales. Para obtener más información, consulte [Tarifas](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server).

### Entorno de nube híbrida
{: #apvs-hybrid}

Puede utilizar los servidores virtuales de Power Systems para ejecutar cargas de trabajo de AIX o IBM i fuera de las instalaciones de la infraestructura de hardware de Power Systems. La ejecución de las cargas de trabajo en la nube pública permiten disfrutar de todas las ventajas que ofrece la nube, tales como el autoservicio, la entrega rápida y la conectividad con otros servicios de IBM Cloud. Aunque las cargas de trabajo de AIX e IBM i estén en ejecución en la nube, el usuario sigue conservando las mismas características escalables, resistentes y listas para la producción que proporciona el hardware de Power Systems.

### Personalización de la infraestructura
{: #apvs-customization}

Es posible configurar y personalizar las opciones siguientes cuando se crea un {{site.data.keyword.powerSys_notm}}:
* Número de instancias de servidor virtual
* Número de núcleos
* Cantidad de memoria
* Tamaño y tipo de volumen de datos (HDD o SSD)
* Red pública o privada

### Incorporación de su propia imagen
{: #apvs-own-image}

IBM proporciona una serie de imágenes del sistema operativo AIX e IBM i cuando se crea un {{site.data.keyword.powerSys_notm}}. Sin embargo, el usuario puede incorporar su propia imagen del sistema operativo AIX o IBM i que haya desplegado o comprobado con anterioridad. Para obtener más información, consulte [Configuración de una imagen personalizada](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Especificaciones de hardware
{: #apvs-hardware-specifications}

El siguiente hardware de IBM Power Systems aloja el {{site.data.keyword.powerSys_notm}}:

* Cálculo
  * [Power System E880 (9119-MHE) ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 TB de memoria
    * Canal de fibra (FC) de puerto dual PCI Express de 8 x 16 Gigabits
    * Puerto dual Ethernet-SR PCI Express de 10 x 10 Gigabits
  * [Power System S922 (9009-22A) ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 GB de memoria
    * Canal de fibra de puerto dual PCI Express de 2 x 16 Gigabits
    * Puerto dual Ethernet-SR PCI Express de 3 x 10 Gigabits

* Almacenamiento
  * Controlador dual Storewize V7000F(2076-AF6)
  * Controlador dual Storwize V7000 (2076-624)

* Red
  * Cisco Nexus9000 93180YC-EX (10 G)
  * Cisco Nexus9000 C9348GC-FXP (1 G)

## Redes pública y privada
{: #apvs-public-and-private}

Cuando se crea un {{site.data.keyword.powerSys_notm}}, se puede seleccionar una interfaz de red privada o una interfaz de red pública.

* Red pública
  * Método fácil y rápido para conectarse a una instancia del {{site.data.keyword.powerSys_notm}}.
  * IBM configura la infraestructura de red para habilitar una conexión de red pública segura desde Internet hasta la instancia del {{site.data.keyword.powerSys_notm}}.
  * La conectividad se implementa utilizando un Virtual Router Appliance (VRA) de IBM Cloud y una conexión Direct Link Connect.
  * Está protegido por el cortafuegos y admite los siguientes protocolos de red seguros:
    * SSH
    * HTTPS
    * Ping
    * Emulación de terminal IBM i 5250 con SSL (puerto 992)

* Red privada
  * Permite que los recursos de su instancia del {{site.data.keyword.powerSys_notm}} accedan a los recursos existentes de {{site.data.keyword.cloud_notm}} como, por ejemplo, servidores nativos, contenedores de Kubernetes o almacenamiento en la nube.
  * Utiliza la conexión de Direct Link Connect para conectar su red de cuentas y sus recursos de IBM Cloud. El proceso de creación de una conexión de Direct Link Connect puede tardar unos cuantos días porque el personal de soporte de IBM Cloud debe configurar el enlace.
  * Es necesaria para establecer comunicación entre diversas instancias del {{site.data.keyword.powerSys_notm}}.

    Si desea obtener más información sobre las distintas opciones para configurar una red privada, consulte [Configuración de una red privada](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring).
    {: note}

En la figura siguiente se muestra la configuración básica de una red pública y privada:

![Muestra cómo fluye el tráfico de red para la conexión pública o privada](/images/power-iaas-network1.svg "Muestra cómo fluye el tráfico de red para la conexión pública o privada")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
