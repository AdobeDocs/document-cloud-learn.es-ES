---
title: Actualizaciones importantes de productos de Acrobat DC para clientes ETLA
description: Conozca los cambios importantes en los derechos de Acrobat DC incluidos en las ofertas de ETLA (Enterprise Term License Agreement) desde agosto de 2020 hasta el 20 de noviembre de 2020
role: Admin
product: adobe acrobat
level: Intermediate
thumbnail: KT-7269.jpg
jira: KT-7269
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: 2b47655370d52405e5773f0358c71aa65fdecdef
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 6%

---

# Importantes actualizaciones de productos de Acrobat DC para clientes ETLA

[!DNL Adobe Sign Individual] (también conocido como Adobe Sign Pro) se retirará de todas las asignaciones de Acrobat DC incluidas en las ofertas de ETLA (Enterprise Term License Agreement) solo a partir de agosto de 2020 y continuará hasta el 20 de noviembre de 2020. [!DNL Adobe Sign Individual] no proporciona funciones de nivel empresarial y debe sustituirse por clientes de Adobe Sign Enterprise para empresas. Esto incluye Acrobat DC con licencia como aplicación independiente y Acrobat DC con licencia como parte de Creative Cloud para empresas - Todas las aplicaciones.

Acceso a [!DNL Adobe Sign Individual] está disponible en Acrobat a través del **Adobe Sign** o la **Fill &amp; Sign** herramienta ([Solicitar firmas](https://www.adobe.com/es/acrobat/online/request-signature.html){target="_blank"}).

![[!DNL Adobe Sign Individual] acceso en Acrobat DC](../assets/Deploy_SignEntitle1.png)

Si no ha actualizado Acrobat DC a la versión más reciente, es posible que la herramienta tenga la etiqueta &quot;Send for Signature&quot;.

## ¿Por qué estamos desaprovisionando esto?

[En octubre de 2018, lanzamos un nuevo Acrobat DC](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC). Esta última versión incluye nuevas herramientas y funcionalidades para trabajar mejor con PDF de dispositivos móviles, la web y equipos de escritorio, además de las nuevas herramientas de colaboración. Como suscriptor de Acrobat DC, ya deberías tener disponibles estas fantásticas funciones. Otra actualización importante que lanzamos fue nuestra solución de firma electrónica Adobe Sign.

Antes de la versión de octubre de 2018, los usuarios de Acrobat DC podían enviar documentos para firmarlos electrónicamente mediante herramientas de Acrobat con la etiqueta &quot;Fill &amp; Sign&quot; (o &quot;Adobe Sign&quot; o &quot;Send for Signature&quot;), que se suministraban con [!DNL Adobe Sign Individual] derecho.

Si bien disponer de esta opción ha proporcionado una excelente forma de capturar firmas electrónicas, estamos retirando el aprovisionamiento [!DNL Adobe Sign Individual] porque no proporciona la funcionalidad de nivel Enterprise que está disponible en Adobe Sign Enterprise, como:

* Capacidad de administrar de forma centralizada los usuarios que tienen permiso para enviar acuerdos o firmar
* Permitir a los administradores administrar acuerdos que se envían y utilizan en toda la organización
* Ofrecer controles detallados para gestionar las firmas electrónicas en toda la organización

Además, Adobe Sign Enterprise ofrece más funcionalidades en comparación con lo que estaba disponible en el [!DNL Adobe Sign Individual] derechos, incluidos, entre otros:

* Administración
   * Inicio de sesión único
   * Delegación de cuentas
* Integraciones
   * Integraciones empresariales prediseñadas con Dropbox, Salesforce, Workday, etc.
   * Adobe Sign es la solución de firma electrónica preferida en todo el [Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html) portafolio empresarial, que incluye Office 365, SharePoint, Dynamics, Teams y Flow
* Personalización y optimización
   * Autenticación de firma electrónica mejorada, verificación avanzada de la identidad del firmante basada en ID, diseñador del flujo de trabajo, compatibilidad avanzada con varios idiomas, etc.

Adobe Sign es la solución líder del sector y reconocida mundialmente para recopilar firmas que cumplen la normativa legal. Adobe Sign se ha creado desde cero para satisfacer cualquiera de las necesidades de firma electrónica de tu organización, con herramientas de administración de TI para garantizar que tú y tus usuarios estáis utilizando firmas electrónicas que cumplen totalmente con las distintas normativas regionales y del sector en torno a las firmas electrónicas. Visite [aquí](https://helpx.adobe.com/es/enterprise/using/adobe-sign-for-enterprise.html) para obtener más información sobre la administración de Sign mediante [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

Póngase en contacto con su contacto de Adobe para analizar cómo puede seguir proporcionando las capacidades de firma electrónica de su organización a través de nuestra plataforma más amplia de documentos digitales, que incluye Acrobat DC y Adobe Sign Enterprise.

## Acceso a los acuerdos existentes

Los usuarios podrán seguir accediendo a cualquier acuerdo enviado antes de esta acción a través de Adobe Document Cloud iniciando sesión con su Adobe ID en https://documentcloud.adobe.com. Si se ha programado la migración de este usuario a Sign Enterprise, deberá seguir estos pasos [instrucciones](https://helpx.adobe.com/es/sign/kb/how-to-download-signed-documents---adobe-sign.html).

## Experiencia de Acrobat DC sin [!DNL Sign Individual] derecho

Los usuarios que tengan derechos de Adobe Sign Enterprise podrán enviar acuerdos dentro de Acrobat utilizando Adobe Sign o [!UICONTROL Fill &amp; Sign] (Solicitar firmas).
Los usuarios que no tengan derechos de Adobe Sign Enterprise no podrán enviar nuevos acuerdos y recibirán un mensaje de error. El gráfico siguiente describe los posibles resultados.

![Mensaje de error de Acrobat DC Experience](../assets/Deploy_SignEntitle2.png)

## Experiencia web de Adobe Document Cloud sin derechos de Sign Individual

Los usuarios podrán iniciar sesión en https://documentcloud.adobe.com/ para acceder y descargar cualquier acuerdo que se haya enviado antes de retirar los derechos de Adobe Sign Individual.

![Mensaje de error de Document Cloud Web Experience](../assets/Deploy_SignEntitle3.png)

## Para obtener más información, visite las siguientes páginas:

* [Iniciar sesión en Adobe Document Cloud](https://helpx.adobe.com/document-cloud/help/sign-in.html)
* [Administrar archivos (¿Dónde están mis archivos?)](https://helpx.adobe.com/document-cloud/help/manage-files.html)
* [Uso [!UICONTROL Acrobat Customization Wizard] para la configuración](https://www.adobe.com/es/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [Descripción general de [!UICONTROL Admin Console]](https://helpx.adobe.com/es/enterprise/using/admin-console.html)
* [Gestión de Adobe Sign en el [!UICONTROL Admin Console]](https://helpx.adobe.com/es/enterprise/using/adobe-sign-for-enterprise.html)

**Revisiones** 20 de mayo de 2020; original post - agosto 2019
