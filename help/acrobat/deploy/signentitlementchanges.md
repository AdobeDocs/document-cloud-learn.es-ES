---
title: Actualizaciones importantes de productos de Acrobat DC para clientes ETLA
description: Obtenga más información sobre los cambios importantes en los derechos de Acrobat DC incluidos en las ofertas del ETLA (Enterprise Term License Agreement) desde agosto de 2020 hasta el 20 de noviembre de 2020
role: Admin
product: adobe acrobat
level: Intermediate
thumbnail: KT-7269.jpg
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: 018cbcfd1d1605a8ff175a0cda98f0bfb4d528a8
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 3%

---

# Actualizaciones importantes de productos de Acrobat DC para clientes ETLA

[!DNL Adobe Sign Individual] (también conocido como Adobe Sign Pro) se retirará de todos los derechos de Acrobat DC incluidos en las ofertas de ETLA (Enterprise Term License Agreement) recién a partir de agosto de 2020 y continuará hasta el 20 de noviembre de 2020. [!DNL Adobe Sign Individual] no proporciona funcionalidad de nivel empresarial y debe sustituirse por Adobe Sign Enterprise para clientes empresariales. Esto incluye la licencia de Acrobat DC como aplicación independiente y la licencia de Acrobat DC como parte de Creative Cloud para empresas - Todas las aplicaciones.

El acceso a [!DNL Adobe Sign Individual] está disponible en Acrobat mediante la herramienta **Adobe Sign** o la herramienta **Fill &amp; Sign** (Solicitar firmas).

![[!DNL Adobe Sign Individual] acceso en Acrobat DC](../assets/Deploy_SignEntitle1.png)

Si no ha actualizado Acrobat DC a la versión más reciente, la herramienta puede etiquetarse como &quot;Send for Signature&quot;.

## ¿Por qué estamos desaprovisionando esto?

[En octubre de 2018, lanzamos un nuevo Acrobat DC](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC). Esta última versión incluye nuevas herramientas y funcionalidad para trabajar mejor con archivos PDF en dispositivos móviles, la Web y el escritorio, además de las nuevas herramientas de colaboración. Como suscriptor de Acrobat DC, ya debería tener estas excelentes funciones disponibles. Otra actualización importante que lanzamos fue nuestra solución de firma electrónica Adobe Sign.

Antes de la versión de octubre de 2018, los usuarios de Acrobat DC podían enviar documentos para firmar electrónicamente mediante las herramientas de Acrobat etiquetadas como &quot;Fill &amp; Sign&quot; (o &quot;Adobe Sign&quot; o &quot;Send for Signature&quot;) y aprovisionadas con [!DNL Adobe Sign Individual] derechos.

Si bien esta opción ha proporcionado una buena forma de capturar firmas electrónicas, estamos desaprovisionando [!DNL Adobe Sign Individual] porque no proporciona la funcionalidad de nivel empresarial disponible a través de Adobe Sign Enterprise, como:

* Posibilidad de administrar de forma centralizada los usuarios que tienen permiso para enviar acuerdos o firmar
* Permitir a los administradores administrar los acuerdos que se envían y se utilizan en toda la organización
* Proporcionar controles granulares para administrar las firmas electrónicas en toda la organización

Además, Adobe Sign Enterprise ofrece más funcionalidad en comparación con lo que estaba disponible en la asignación de derechos [!DNL Adobe Sign Individual], lo que incluye, entre otros:

* Administración
   * Inicio de sesión único
   * Delegación de cuenta
* Integraciones
   * Integraciones empresariales prediseñadas con Dropbox, Salesforce, Workday, etc.
   * Adobe Sign es la solución de firma electrónica preferida en toda la cartera empresarial de [Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html), incluidos Office 365, SharePoint, Dynamics, Teams y Flow
* Personalización y optimización
   * Autenticación de firma electrónica mejorada, verificación avanzada de la identidad del firmante basada en ID, diseñador de flujos de trabajo, compatibilidad con idiomas avanzados, etc.

Adobe Sign es la solución mundialmente reconocida líder del sector para capturar firmas que cumplen las normas legales. Adobe Sign se ha creado desde cero para satisfacer cualquiera de las necesidades de firma electrónica de su organización, con herramientas fáciles de administrar de TI para garantizar que usted y sus usuarios usen firmas electrónicas que cumplan completamente las diversas reglamentaciones regionales y del sector relacionadas con las firmas electrónicas. Visite [aquí](https://helpx.adobe.com/es/enterprise/using/adobe-sign-for-enterprise.html) para obtener más información sobre la administración de Sign a través de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

Póngase en contacto con su contacto de Adobe para analizar cómo puede seguir ofreciendo las funciones de firma electrónica de su organización a través de nuestra plataforma de documentos digitales más amplia que incluye Acrobat DC y Adobe Sign Enterprise.

## Acceso a los acuerdos existentes

Los usuarios podrán seguir accediendo a cualquier acuerdo enviado antes de esta acción a través de Adobe Document Cloud iniciando sesión con su Adobe ID en https://documentcloud.adobe.com. Si este usuario está programado para migrar a Sign Enterprise, deberá seguir estas [instrucciones](https://helpx.adobe.com/sign/kb/how-to-download-signed-documents---adobe-sign.html).

## Experiencia de Acrobat DC sin derechos [!DNL Sign Individual]

Los usuarios que tengan derechos de Adobe Sign Enterprise podrán enviar acuerdos dentro de Acrobat mediante la herramienta Adobe Sign o [!UICONTROL Fill &amp; Sign] (Solicitar firmas).
Los usuarios que no tengan derechos de Adobe Sign Enterprise no podrán enviar nuevos acuerdos y recibirán un mensaje de error. El gráfico siguiente describe los posibles resultados.

![Mensaje de error para la experiencia de Acrobat DC](../assets/Deploy_SignEntitle2.png)

## Experiencia web de Adobe Document Cloud sin derechos de Sign Individual

Los usuarios podrán iniciar sesión en https://documentcloud.adobe.com/ para acceder y descargar los acuerdos que se hayan enviado antes de desaprovisionar los derechos de Adobe Sign Individual.

![Mensaje de error para la experiencia web del Document Cloud](../assets/Deploy_SignEntitle3.png)

## Para obtener más información, visite las páginas siguientes:

* [Iniciar sesión en Adobe Document Cloud](https://helpx.adobe.com/document-cloud/help/sign-in.html)
* [Administración de archivos (¿Dónde están mis archivos?)](https://helpx.adobe.com/document-cloud/help/manage-files.html)
* [Uso de  [!UICONTROL Acrobat Customization ] Wizard para la configuración](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [Descripción general del  [!UICONTROL Admin Console]](https://helpx.adobe.com/enterprise/using/admin-console.html)
* [Administración de Adobe Sign en el  [!UICONTROL Admin Console]](https://helpx.adobe.com/enterprise/using/adobe-sign-for-enterprise.html)

**** Revisiones 20 de mayo de 2020; post original - agosto de 2019
