---

copyright:
  years: 2019

lastupdated: "2019-07-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Solicitud de IBM Cloud Direct Link Connect para servidores virtuales de Power Systems
{: #ordering-direct-link-connect}

Una opción para configurar una red privada con {{site.data.keyword.powerSys_notm}} es utilizar el servicio Direct Link Connect. El servicio Direct Connect Link crea una conexión que permite acceder a los recursos de {{site.data.keyword.cloud}} a partir de la instancia del {{site.data.keyword.powerSys_notm}}. El servicio Direct Link Connect también se utiliza para conectar su red local en la red de IBM Cloud utilizando el dispositivo direccionador virtual (VRA - Virtual Router Appliance) de IBM Cloud.
{:shortdesc}

Puede utilizar la consola de la interfaz de usuario del {{site.data.keyword.cloud_notm}} para solicitar el servicio Direct Link Connect. Direct Link Connect es un servicio independiente del servicio {{site.data.keyword.powerSys_notm}}. Para consultar los cargos de Direct Link Connect, consulte [Precios para IBM Cloud Direct Link](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect).

IBM recomienda que se pida una segunda conexión de Direct Link Connect con fines de copia de seguridad.

## Antes de empezar
{: #before-direct-link-connect}

* Verifique que la cuenta de {{site.data.keyword.cloud}} tenga las autorizaciones correctas para solicitar el servicio Direct Link Connect.
* Entienda los conceptos básicos de la red para el servicio Direct Link Connect consultando los temas siguientes:
    * [Conceptos de Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
    * [Detalles de Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
    * [Limitaciones de Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
    * [Limitaciones estrictas en asignaciones de IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Pasos para solicitar Direct Link Connect
{: #steps-to-order-direct-link-connect}

Para solicitar el servicio Direct Link Connect que crea una conexión con la instancia del {{site.data.keyword.powerSys_notm}}, siga estos pasos:

1. Inicie sesión en el [catálogo de IBM Cloud ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/catalog){: new_window} con las credenciales de su cuenta de IBM Cloud. Su cuenta debe tener la autorización correcta para solicitar el servicio Direct Link Connect.

2. En la sección **Redes**, pulse el mosaico **Direct Link Connect**.
![Muestra el mosaico del catálogo Direct Link](/images/directlink1.png "Muestra el mosaico del catálogo Direct Link")

1. Desde la entrada del catálogo Direct Link Connect, pulse **Crear**.

1. Desde la página de IBM Cloud Direct Link, pulse **Pedir Direct Link Connect**.

1. Desde la página Crear conexión de IBM Cloud Direct Link Connect, complete los campos siguientes.

   A medida que vaya completando los campos siguientes para crear el servicio Direct Link Connect, el precio se va actualizando automáticamente para reflejar sus selecciones.
   {: note}

   <dl>
   <dt><strong>Nombre de instancia de Direct Link</strong><dt>
   <dd>Especifique un nombre que describa la finalidad de Direct Link Connect.</dd>
   <dt><strong>Ubicación</strong><dt>
   <dd>Seleccione la misma ubicación que la de la instancia del {{site.data.keyword.powerSys_notm}}. En la tabla siguiente se identifica la ubicación de la instancia del {{site.data.keyword.powerSys_notm}} así como la opción correspondiente de Direct Link Connection:
   <table>
   <caption>Tabla 1. Opciones de ubicación de Direct Link Connection</caption>
   <tr>
   <th>Ubicación del servidor virtual de Power Systems</th>
   <th>Ubicación de Direct Link Connect</th>
   </tr>
   <tr>
   <td>Dallas, TX EE.UU.</td>
   <td>Dallas 4</td>
   </tr>
   <tr>
   <td>Washington D.C, EE.UU.</td>
   <td>Washington 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Proveedor de red</strong><dt>
   <dd>Debe seleccionar <strong>MEGAPORT</strong> de la lista.</dd>
   <dt><strong>Velocidad de enlace</strong><dt>
   <dd>Seleccione la velocidad de enlace para cumplir los requisitos de carga de trabajo. La selección recomendada de este campo es 1000 Mbps.</dd>
   <dt><strong>Opción de direccionamiento</strong><dt>
   <dd>Seleccione <strong>Direccionamiento local (Libre)</strong> para acceder a todos los centros de datos que están conectados a la ubicación que se ha especificado en el campo <strong>Ubicación</strong>. Seleccione <strong>Direccionamiento global</strong> para acceder a todos los centros de datos de IBM Cloud del mundo. </dd>
   <dt><strong>ASN de BGP</strong><dt>
   <dd>Debe indicar el número ASN de BGP para la ubicación específica de Direct Link Connect en la tabla siguiente.
   <table>
   <caption>Tabla 2. Número ASN de BGP para ubicaciones específicas</caption>
   <tr>
   <th>Ubicación de Direct Link Connect</th>
   <th>Número ASN de BGP</th>
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
   <dt><strong>Selección de VRF</strong><dt>
   <dd>Seleccione la opción de direccionamiento y reenvío virtual para la conexión. Si su cuenta no tiene identificado ningún valor para VRF, este campo no se visualiza. Puede crear el servicio Direct Link Connect igualmente sin seleccionar ningún valor de VRF. La figura siguiente es un ejemplo de los campos de Direct Link Connect.</dd>
   <dd>

   ![Muestra los campos de Direct Link Connect que se han completado](/images/directlink2.png "Muestra los campos de Direct Link Connect que se han completado")
   </dd>
   </dl>
2. Lea el **Acuerdo de servicio maestro** y marque el recuadro de selección. Debe leer y comprender el **Acuerdo de servicio maestro** porque contiene información técnica importante.

3. Pulse **Crear**. El mensaje siguiente se visualiza cuando su solicitud se envía correctamente.
![Muestra el mensaje que indica que Direct Link Connect se ha enviado correctamente](/images/directlink3.png "Muestra el mensaje que indica que Direct Link Connect se ha enviado correctamente")

1. Pulse el enlace **Número de caso** del servicio Direct Link Connect. La información del número de caso se utiliza para identificar la información de Direct Link Connect para conectar la instancia del {{site.data.keyword.powerSys_notm}}.

  El personal de soporte de IBM puede tardar hasta tres días hábiles en crear la conexión de Direct Link Connect.
  {: note}

2. Para crear una conexión a la instancia del {{site.data.keyword.powerSys_notm}} utilizando el servicio Direct Link Connect, abra un [caso nuevo](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support) para el equipo de soporte del {{site.data.keyword.powerSys_notm}}.

      1. En el campo de descripción del caso nuevo, añada el número de caso de Direct Link Connect.
      2. Copie el ID de servicio de IAM del caso {{site.data.keyword.powerSys_notm}} que el sistema ha generado automáticamente.

3. Escriba el ID de servicio de IAM del caso del {{site.data.keyword.powerSys_notm}} en el caso de Direct Link Connect. Cuando se crea la conexión de Direct Link Connect, se cierra el número de caso de Direct Link Connect. A continuación se ofrece un ejemplo de la información de red que se muestra en el caso:

  ```shell
  Velocidad de enlace:         1000 Mbps
  Ubicación:                   Washington 2
  Proveedor de red:            MEGAPORT
  Dirección IP de IBM:         10.254.0.25/30
  Dirección IP de cliente:     10.254.0.26/30
  Clave de servicio:           None
  ASN de BGP:                  64999
  Identificador de red:        1748523-1
  Fecha de creación:           2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. Utilice esta información del número de caso de Direct Link Connect y escriba la siguiente información de red en el caso del {{site.data.keyword.powerSys_notm}}:

  ```shell
  Nombre de cliente:
  ID de cuenta de cliente:
  Subred de Direct Link Connect:
  Dirección IP de red del servidor virtual de Power Systems:
  Dirección IP de IBM Cloud:
  ASN de la red del servidor virtual de Power Systems:
  ASN de IBM Cloud:
  ID de red privada (1):
  ID de red privada (2):
  ID de red privada (3):
  ```
  {: codeblock}

1. El caso del {{site.data.keyword.powerSys_notm}} se cierra cuando se configura la conexión de Direct Link Connect para establecer comunicación con la instancia del {{site.data.keyword.powerSys_notm}}.
