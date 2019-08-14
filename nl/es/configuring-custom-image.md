---

copyright:
  years: 2019

lastupdated: "2019-7-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Configuración de una imagen personalizada con un servidor virtual de Power Systems
{: #configuring-custom-image}

Puede incorporar su propia imagen personalizada del sistema operativo AIX o IBM i para desplegar un {{site.data.keyword.powerSysFull}}.
{:shortdesc}

No puede transferir una licencia de sistema operativo de un sistema local a un {{site.data.keyword.powerSys_notm}} que se esté ejecutando en el entorno en nube. El coste de la licencia se repercute en la tarifa de facturación por horas global.
{: note}

## Antes de empezar
{: #cci-before-you-begin}

Antes de utilizar una imagen personalizada como volumen de arranque, consulte la siguiente información:

* Debe comprobar que el nivel de tecnología del sistema operativo AIX o IBM i lo admita el hardware de Power Systems que haya seleccionado en el campo **Tipo de máquina**. Si desea ver una lista de los niveles de tecnología y del hardware Power System que se admiten con los sistemas operativos AIX e IBM i, consulte [Correlaciones del software del sistema ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).
* Debe tener un conocimiento básico de los conceptos de **Almacenamiento de objetos de IBM Cloud**. Para obtener más información, consulte [Acerca del almacenamiento de objetos de IBM Cloud](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage).
* Si no tiene ninguna imagen existente de AIX o IBM i, puede utilizar IBM® PowerVC™ para capturar y exportar una imagen que se utilizará con el {{site.data.keyword.powerSys_notm}}. Para obtener más información, consulte [Captura de una máquina virtual![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} y [Exportación de imágenes![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}.

## Carga de una imagen personalizada como objeto
{: #cci-uploading}

1. Cree un objeto de almacenamiento de IBM Cloud y cargue su imagen. Para obtener más información, consulte [Cargar datos](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload).
2. Genere claves de secreto y acceso con el código de autenticación de mensajes basado en Hash (HMAC - Hash-based Message Authentication Code). Puede generar estas claves cuando cree las credenciales de servicio para el objeto de almacenamiento de IBM Cloud. Para crear las credenciales de servicio, debe disponer de acceso de `Escritor` para el grupo **Almacenamiento de objetos**. Para obtener más información, consulte [Credenciales de servicio](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) y [Permisos de grupo](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).
3. Desde el [catálogo de IBM Cloud ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/catalog){: new_window}, pulse el mosaico del servidor de Power Virtual para añadir la imagen. Si ya ha creado la instancia del servidor virtual, seleccione **icono de Menú ![icono de Menú](../icons/icon_hamburger.svg "icono de Menú") > Lista de recursos > Dispositivos** y seleccione su servidor virtual existente.

 Complete los campos siguientes para crear su {{site.data.keyword.powerSys_notm}} y pulse **Imagen de AIX personalizada** o **Imagen de IBM i personalizada**.

| Campo | Descripción |
| ------| ------------|
| Nombre de grupo de almacenamiento de objetos en la nube | Para identificar el nombre de grupo, seleccione **icono de Menú ![icono de Menú](../icons/icon_hamburger.svg "icono de Menú") > Lista de recursos > Almacenamiento > Nombre de objeto de almacenamiento en la nube > Grupos**. |
| Clave de acceso de almacenamiento de objetos en la nube | Para identificar su clave de acceso, seleccione **icono de Menú ![icono de Menú](../icons/icon_hamburger.svg "icono de Menú") > Lista de recursos > Almacenamiento > Nombre de objeto de almacenamiento en la nube > Credenciales de servicio > Ver credenciales**. Copie el valor de `access_key_id` y péguelo en este campo. |
| Clave secreta de almacenamiento de objetos en la nube | Para identificar su clave secreta, seleccione **icono de Menú ![icono de Menú](../icons/icon_hamburger.svg "icono de Menú") > Lista de recursos > Almacenamiento > Nombre de objeto de almacenamiento en la nube > Credenciales de servicio > Ver credenciales**. Copie el valor de `secret_access_key` y péguelo en este campo. |
| Vía de acceso de la imagen | Escriba la vía de acceso completa del archivo de la imagen. La vía de acceso completa debe tener este formato: `endpoint/bucket_name/file_name`. Debe utiliza el dominio de punto final privado. Por ejemplo, `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`. Puede identificar el dominio de punto final, el nombre de grupo y el nombre de archivo seleccionando **icono de Menú ![icono de Menú](../icons/icon_hamburger.svg "icono de Menú") > Lista de recursos > Almacenamiento > Objeto de almacenamiento en la nube**.
