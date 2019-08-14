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

# Creación de un servidor virtual de Power Systems
{: #creating-power-virtual-server}

Para crear y configurar un {{site.data.keyword.powerSysFull}}, siga estos pasos:

1. Inicie sesión en el [catálogo de IBM Cloud ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/catalog){: new_window} con las credenciales de su cuenta de IBM Cloud.
2. En el recuadro de búsqueda del catálogo, escriba **Servidor virtual de Power Systems** y pulse el mosaico del  {{site.data.keyword.powerSys_notm}}.

    ![Catálogo de IBM Cloud](./images/catalog-search-bar.png "Catálogo de IBM Cloud")

3. Proporcione un nombre a su servicio y decida dónde desea desplegar la instancia del {{site.data.keyword.powerSys_notm}}.

    ![Selección de servicio y zona](./images/power-iaas-service-region.png "Selección de servicio y zona")

4. Pulse el botón **Crear** en la parte inferior de la página web.

    ![Botón Crear](./images/power-iaas-create-button.png "Botón Crear")

5. Después de pulsar el botón **Crear**, se le redirigirá al panel **Lista de recursos**.
6. Desde la **Lista de recursos**, seleccione el servicio en **Servicios** para ir al panel **Gestionar**.

    ![Lista de recursos de IBM Cloud](./images/power-iaas-resource-list.png "Lista de recursos de IBM Cloud")

7. Desde aquí, pulse el botón **Suministrar nuevo**.

    ![Suministro de un servidor virtual nuevo](./images/power-iaas-provision-new.png "Suministro de un servidor virtual nuevo")

8. Complete todos los campos necesarios para crear una instancia nueva correctamente:

     El precio se actualiza dinámicamente en la sección **Resumen del pedido** a medida que se van completando los campos para crear un {{site.data.keyword.powerSys_notm}}. De esta forma puede crear fácilmente un {{site.data.keyword.powerSys_notm}} rentable que satisfaga sus necesidades empresariales.
     {: tip}

    1. Complete todos los campos de la sección **Servidores virtuales**. Si selecciona más de una instancia, se le presentarán opciones adicionales.

      ![Creación de una instancia nueva de un servidor virtual de Power](./images/console-virtual-instance.png "Creación de una instancia nueva del servidor virtual de Power")

    1. Seleccione si desea un **Procesador dedicado** o un **Procesador compartido**. Recuerde pulsar el **Tipo de máquina** que desee, el número de núcleos así como la cantidad de memoria.

      ![Selección de su procesador y sistema](./images/console-profile.png "Selección de su procesador y sistema")

    1. Por último, complete los campos **Volumen de arranque**, **Volúmenes adjuntos** e
**Interfaces de red** tal como se le indique desde su organización.

      ![Definición de sus volúmenes e interfaces de red](./images/console-volume-network.png "Definición de sus volúmenes e interfaces de red")

9. Acepte las **Condiciones de uso** y pulse el botón **Crear** para suministrar un {{site.data.keyword.powerSys_notm}}.

En la tabla siguiente se proporciona información sobre los campos **Instancia de servidor virtual**:

<table>
<caption>Tabla 1. Nuevos campos de instancia de servidor virtual de Power</caption>
<tr>
<th>Campo</th>
<th>Descripción</th>
</tr>
<tr>
<td>Número de instancias</td>
<td>Especifique el número de instancia que desee crear para el {{site.data.keyword.powerSys_notm}}. Si especifica más de una instancia, puede seleccionar las siguientes convenciones de nomenclatura y reglas de colocalización:
  <dl>
    <dt><strong>Sin preferencias</strong></dt>
  <dd>Seleccione esta opción si no tiene ninguna preferencia de alojamiento.</dd>
    <dt><strong>Servidor distinto</strong></dt>
  <dd>Seleccione esta opción para alojar cada instancia en un servidor distinto.  Puede utilizar esta opción si le preocupa que se produzca una parada de un solo servidor que pudiera afectar a todas las instancias del {{site.data.keyword.powerSys_notm}}. </dd>
  <dt><strong>Prefijo numérico</strong></dt>
  <dd>Seleccione esta opción para añadir números antes del nombre del servidor virtual. Por ejemplo, si el primer nombre del {{site.data.keyword.powerSys_notm}} es <kbd>Austin</kbd>, el siguiente nombre de la instancia virtual será <kbd>1Austin</kbd></dd>
  <dt><strong>Postfijo numérico</strong></dt>
  <dd>Seleccione esta opción para añadir números después del nombre del servidor virtual. Por ejemplo, si el primer nombre del {{site.data.keyword.powerSys_notm}} es <kbd>Rochester</kbd>, el siguiente nombre de la instancia virtual será <kbd>Rochester1</kbd>.</dd>
  </dl>
  <p>
  <strong>Nota:</strong> Cuando se crean varias instancias del servidor virtual, se debe seleccionar <strong>Activado</strong> en el campo <strong>Se puede compartir</strong> de cada volumen de datos que se añada. Si no desea que el volumen de datos se pueda compartir, puede añadirlo después de crear el servidor virtual.
  </p>
   </td>
</tr>
<tr>
<td>Máquina virtual de pin</td>
<td>Seleccione <strong>Activado</strong> para bloquear el {{site.data.keyword.powerSys_notm}} en un sistema host. Si selecciona <strong>Activado</strong>, el servidor virtual no se podrá mover a otro host. Por ejemplo, si se selecciona <strong>Activado</strong> detectará una parada durante el mantenimiento del host.</td>
</tr>
<tr>
<td>Tipo de máquina</td>
<td>Especifique el tipo de máquina. El tipo de máquina que seleccione determina el número de núcleos y la memoria que está disponible. Para obtener más información sobre las especificaciones de hardware, consulte <a href="https://www.ibm.com/downloads/cas/KQ4BOJ3N" target="_blank">S922</a> y <a href="https://www.ibm.com/downloads/cas/EE476WAP" target="_blank">E880</a>.</td>
</tr>
<tr>
<td>Núcleos</td>
<td>Seleccione el número de núcleos para el {{site.data.keyword.powerSys_notm}}. Si ha seleccionado <strong>Procesadores compartidos</strong>, puede especificar el número de núcleos en incrementos de 0,25. Por ejemplo, los valores válidos de núcleo son 0,5, 1,25 y 2,75. Se asigna una CPU virtual para cada titularidad de 0,25.

Si le preocupan los problemas de rendimiento, puede seleccionar <strong>Procesador dedicado</strong> porque el proceso está dedicado a su servidor virtual y no se comparte. Para obtener más información, consulte <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">Cómo se compara el rendimiento de procesador compartido con los procesadores dedicados</a>.</td>
</tr>
<tr>
<td>Memoria</td>
<td>Seleccione la cantidad de memoria del {{site.data.keyword.powerSys_notm}}. La cantidad de memoria que se puede seleccionar depende del número de núcleos que se hayan seleccionado. Para cada núcleo que seleccione, puede asignar hasta 64 GB. Por ejemplo, si ha seleccionado cuatro núcleos, podrá seleccionar hasta 256 GB de memoria. </td>
</tr>
<tr>
<td>Creación de un volumen de arranque</td>
<td>Seleccione una versión de la imagen en stock del sistema operativo AIX o IBM i que se proporcionan, o seleccione una imagen personalizada del sistema operativo AIX o IBM i que haya desplegado localmente con anterioridad. Para obtener información sobre las licencias de los sistemas operativos, consulte los <a href="https://www-03.ibm.com/software/sla/sladb.nsf" target="_blank">Documentos de información de licencias</a> de IBM.

Si desea incorporar su propia imagen personalizada, deberá utilizar un nivel de tecnología admitido de la imagen de los sistemas operativos AIX o IBM i para el hardware de Power Systems que haya seleccionado en el campo <strong>Tipo de máquina</strong>. Para obtener más información, consulte <a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">Configuración de una imagen personalizada</a>.</td>
</tr>
<tr>
<td>Volúmenes de datos adjuntos</td>
<td>Puede crear un volumen de datos nuevo o adjuntar un volumen de datos existente que ya se haya definido en su cuenta de IBM Cloud.
<dl>
  <dt><strong>Creación de un volumen de datos</strong></dt>
  <dd>Pulse <strong>Añadir</strong> para crear un volumen de datos nuevo que se pueda utilizar para más poder almacenar más datos en su instancia del
{{site.data.keyword.powerSys_notm}}. Si desea permitir que varias instancias del {{site.data.keyword.powerSys_notm}} escriban datos en el mismo volumen de datos, deberá seleccionar <strong>Activado</strong> en el campo <strong>Se puede compartir</strong>. </dd>
  <dt><strong>Conexión de un volumen de datos existente</strong></dt>
  <dd>Seleccione un volumen de datos existente para disponer de más almacenamiento para su instancia del {{site.data.keyword.powerSys_notm}}. Si la lista no muestra ningún volumen de datos que haya utilizado anteriormente, puede que se deba a que se ha creado ese volumen de datos con una cuenta de IBM Cloud distinta.</dd>
</dl>
</td>
</tr>
<tr>
<td>Redes públicas</td>
<td>Seleccione esta opción para utilizar una red pública proporcionada por IBM. Hay un coste asociado a la selección de esta opción. Para obtener más información, consulte <a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">Redes públicas y privadas</a>.
</td>
</tr>
<tr>
<td>Redes privadas</td>
<td>Pulse <strong>Añadir</strong> para identificar una nueva red privada para el servidor virtual. Si ya ha añadido una red privada, puede seleccionarla de la lista. Para obtener más información, consulte <a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">Configuración de una red privada</a>.</td>
</tr></table>
