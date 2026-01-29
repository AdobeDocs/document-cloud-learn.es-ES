---
title: Actualizaciones importantes de productos de Acrobat DC para clientes ETLA
description: Conozca los cambios importantes en los derechos de Acrobat DC incluidos en las ofertas de ETLA (Enterprise Term License Agreement) que comienzan en agosto de 2020 hasta el 20 de noviembre de 2020
feature: Deploy
role: Admin
level: Intermediate
jira: KT-7269
thumbnail: KT-7269.jpg
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: baf36807c1dcf2142d9a8a5502d8d10d5b8d6033
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 2%

---

# Importantes actualizaciones de productos de Acrobat DC para clientes ETLA

[!DNL Adobe Sign Individual] (también conocido como Adobe Sign Pro) se retirará de todas las asignaciones de Acrobat DC incluidas en las ofertas de ETLA (Enterprise Term License Agreement) solo a partir de agosto de 2020 y continuará hasta el 20 de noviembre de 2020. [!DNL Adobe Sign Individual] no proporciona funcionalidad de nivel empresarial y debe reemplazarse por clientes de Adobe Sign Enterprise para empresas. Esto incluye Acrobat DC con licencia como aplicación independiente y Acrobat DC con licencia como parte de Creative Cloud para empresas - Todas las aplicaciones.

El acceso a [!DNL Adobe Sign Individual] está disponible en Acrobat mediante la herramienta **Adobe Sign** o la herramienta **Fill &amp; Sign** ([Solicitar firmas](https://www.adobe.com/es/acrobat/online/request-signature.html){target="_blank"}).

Acceso de ![[!DNL Adobe Sign Individual] en Acrobat DC](../assets/Deploy_SignEntitle1.png)

Si no ha actualizado Acrobat DC a la versión más reciente, es posible que la herramienta tenga la etiqueta &quot;Send for Signature&quot;.

## ¿Por qué estamos desaprovisionando esto?

[En octubre de 2018, lanzamos un nuevo Acrobat DC](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC). Esta última versión incluye nuevas herramientas y funcionalidades para trabajar mejor con PDF de dispositivos móviles, la web y equipos de escritorio, además de las nuevas herramientas de colaboración. Como suscriptor de Acrobat DC, ya deberías tener disponibles estas fantásticas funciones. Otra actualización importante publicada fue nuestra solución de firma electrónica Adobe Sign.

Antes de la versión de octubre de 2018, los usuarios de Acrobat DC podían enviar documentos para firmarlos electrónicamente mediante herramientas de Acrobat con la etiqueta &quot;Fill &amp; Sign&quot; (o &quot;Adobe Sign&quot; o &quot;Send for Signature&quot;) a las que se les había concedido derechos de [!DNL Adobe Sign Individual].

Si bien tener esta opción ha proporcionado una gran forma de capturar firmas electrónicas, estamos retirando el aprovisionamiento de [!DNL Adobe Sign Individual] porque no proporciona la funcionalidad de nivel Enterprise que está disponible a través de Adobe Sign Enterprise, como:

* Capacidad de administrar de forma centralizada los usuarios que tienen permiso para enviar acuerdos o firmar.
* Permitir a los administradores administrar acuerdos que se envían y utilizan en toda la organización
* Ofrecer controles detallados para gestionar las firmas electrónicas en toda la organización

Además, Adobe Sign Enterprise ofrece más funcionalidad en comparación con lo que estaba disponible en el derecho de [!DNL Adobe Sign Individual], lo que incluye, entre otros:

* Administración
   * Inicio de sesión único
   * Delegación de cuentas
* Integraciones
   * Integraciones empresariales prediseñadas con Dropbox, Salesforce, Workday, etc.
   * Adobe Sign es la solución de firma electrónica preferida para todo el catálogo de productos empresariales de [Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html), como Office 365, SharePoint, Dynamics, Teams y Flow
* Personalización y optimización
   * Autenticación de firma electrónica mejorada, verificación avanzada de la identidad del firmante basada en ID, diseñador del flujo de trabajo, compatibilidad avanzada con varios idiomas, etc.

Adobe Sign es la solución líder del sector y reconocida mundialmente para recopilar firmas que cumplen la normativa legal. Adobe Sign se ha creado desde cero para satisfacer cualquiera de las necesidades de firma electrónica de tu organización, con herramientas de administración de TI para garantizar que tú y tus usuarios estáis utilizando firmas electrónicas que cumplen totalmente con las distintas normativas regionales y del sector en torno a las firmas electrónicas. Visita [aquí](https://helpx.adobe.com/es/enterprise/using/adobe-sign-for-enterprise.html) para obtener más información sobre cómo administrar Sign a través de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

Póngase en contacto con su contacto de Adobe para analizar cómo puede seguir proporcionando las capacidades de firma electrónica de su organización a través de nuestra plataforma más amplia de documentos digitales, que incluye Acrobat DC y Adobe Sign Enterprise.

## Acceso a los acuerdos existentes

Los usuarios podrán seguir accediendo a cualquier acuerdo enviado antes de esta acción a través de Adobe Document Cloud iniciando sesión con su Adobe ID en https://documentcloud.adobe.com. Si este usuario está programado para la migración a Sign Enterprise, debe seguir estas [instrucciones](https://helpx.adobe.com/es/sign/kb/how-to-download-signed-documents---adobe-sign.html).

## Experiencia de Acrobat DC sin derechos de [!DNL Sign Individual]

Los usuarios que tengan derechos de Adobe Sign Enterprise pueden enviar acuerdos dentro de Acrobat utilizando Adobe Sign o la herramienta [!UICONTROL Fill &amp; Sign] (Solicitar firmas).
Los usuarios que no tengan derechos de Adobe Sign Enterprise no podrán enviar nuevos acuerdos y recibirán un mensaje de error. En el gráfico siguiente se describen los posibles resultados.

![Mensaje de error para la experiencia de Acrobat DC](../assets/Deploy_SignEntitle2.png)

## Experiencia web de Adobe Document Cloud sin derechos de Sign Individual

Los usuarios podrán iniciar sesión en https://documentcloud.adobe.com/ para acceder y descargar cualquier acuerdo que se haya enviado antes de desaprovisionar los derechos de Adobe Sign Individual.

![Mensaje de error para la experiencia web del Document Cloud](../assets/Deploy_SignEntitle3.png)

## Para obtener más información, visite las siguientes páginas:

* [Iniciar sesión en Adobe Document Cloud](https://helpx.adobe.com/es/document-cloud/help/sign-in.html)
* [Administrar archivos (¿Dónde están mis archivos?)](https://helpx.adobe.com/es/document-cloud/help/manage-files.html)
* [Usando [!UICONTROL Acrobat Customization Wizard] para la configuración](https://www.adobe.com/es/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [Información general del [!UICONTROL Admin Console]](https://helpx.adobe.com/es/enterprise/using/admin-console.html)
* [Administrando Adobe Sign en el [!UICONTROL Admin Console]](https://helpx.adobe.com/es/enterprise/using/adobe-sign-for-enterprise.html)

**Revisiones** 20 de mayo de 2020; publicación original: agosto de 2019
