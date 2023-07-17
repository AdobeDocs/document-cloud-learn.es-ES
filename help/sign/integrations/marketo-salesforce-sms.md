---
title: Enviar notificaciones con Acrobat Sign para Salesforce y Marketo
description: Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: aa8fd589d214879f2bfcb6bc54576c707532fd6f
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Enviar notificaciones con Acrobat Sign para [!DNL Salesforce] y [!DNL Marketo]

Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino mediante Acrobat Sign, Acrobat Sign para Salesforce, Marketo y Marketo Salesforce Sync. Para enviar notificaciones desde Marketo, primero debe adquirir o configurar una función de administración de SMS de Marketo. Este tutorial utiliza [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), pero hay otras soluciones SMS de Marketo disponibles.

## Requisitos previos

1. Instale Marketo Salesforce Sync.

   Dispone de información y del plugin más reciente para Salesforce Sync [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instalación de Acrobat Sign para Salesforce.

   Información sobre este plugin está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Sincronización de Marketo Salesforce y Acrobat Sign para Salesforce, aparecen varias opciones nuevas en el Terminal de administración de Marketo.

![Administrador](assets/adminTab.png)

![Sincronización de objetos](assets/salesforceAdmin.png)

1. Haga clic en **Sincronizar esquema** si es tu primera vez. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema1.png)

1. Si se está ejecutando la sincronización global, deshabilite haciendo clic en **Deshabilitar la sincronización global**.

   ![Desactivar](assets/disableGlobal.png)

1. Haga clic en **Actualizar esquema**.

   ![Actualizar 2](assets/refreshSchema2.png)

## Sincronizar los objetos personalizados

En el lado derecho, consulte Objetos personalizados basados en clientes potenciales, contactos y cuentas.

**Habilitar sincronización** para los objetos en Candidato si desea activar cuando se añade un Candidato a un acuerdo en Salesforce.

**Habilitar sincronización** para los objetos de Contacto si desea activar cuando se agrega un Contacto a un acuerdo en Salesforce.

**Habilitar sincronización** para los objetos de Account si desea activar cuando se agrega una cuenta a un acuerdo en Salesforce.

1. **Habilitar sincronización** para los objetos personalizados mostrados bajo el padre deseado (Candidato, Contacto o Cuenta).

   ![Objetos personalizados](assets/customObjects.png)

1. Los siguientes activos muestran cómo **Habilitar sincronización**.

   ![Sincronización personalizada 1](assets/customObjectSync1.png)

   ![Sincronización personalizada 2](assets/customObjectSync2.png)

1. Cuando haya terminado de activar la sincronización en los objetos personalizados, vuelva a activar la sincronización.

   ![Habilitar global](assets/enableGlobal.png)

## Crear el programa

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda, seleccione **Nueva carpeta de campaña** y ponle un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada y seleccione **Nuevo programa** y ponle un nombre. Deje todo lo demás como predeterminado y, a continuación, haga clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

## Configurar Twilio SMS

Primero asegúrese de tener una cuenta activa de Twilio y compró las características de SMS que necesita.

La configuración del webhook Marketo - Twilio SMS requiere tres parámetros de Twilio de su cuenta.

- SID de cuenta
- Token de cuenta
- Número de teléfono Twilio

Recupere estos parámetros de su cuenta y abra su instancia de Marketo.

1. Haga clic en **Administrador** en la parte superior derecha.

   ![Administrador](assets/adminTab.png)

1. Haga clic en **Webhooks**, entonces **Nuevo webhook**.

   ![Webhooks](assets/webhooks.png)

1. Introduzca un **Nombre de webhook** y **Descripción**.

1. Introduzca la siguiente dirección URL y asegúrese de reemplazar la **[ACCOUNT_SID]** y **[AUTH_TOKEN]** con sus credenciales de Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Seleccionar **POST** como tipo de solicitud.

1. Introduzca lo siguiente **Plantilla** y asegúrese de reemplazar **[MY_TWILIO_NUMBER]** con tu número de teléfono Twilio y **[YOUR_MESSAGE]** con un mensaje de su elección.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Establezca Codificación del token de solicitud en Formulario/URL.

1. Establezca el Tipo de respuesta en JSON y, a continuación, haga clic en **Guardar**.

## Configurar el activador inteligente de campañas

1. En la sección Actividades de marketing, haga clic con el botón derecho en el programa que ha creado y, a continuación, seleccione **Nueva campaña inteligente**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asígnele un nombre y, a continuación, haga clic en **Crear**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Si la configuración de la sincronización de objetos personalizados se ha realizado correctamente, debería ver los siguientes desencadenadores disponibles para su uso en la carpeta Salesforce.

1. Haga clic y arrastre Agregado al acuerdo a la lista inteligente. Añada las restricciones que desee tener en el activador.

   ![Añadido al acuerdo 2](assets/addedToAgreement2.png)

## Configurar el flujo de campaña inteligente

1. Haga clic en el **Flujo** de la Campaña inteligente. Busque y arrastre el **Llamar a webhook** en el lienzo y seleccione el webhook creado en la sección anterior.

   ![Llamar a webhook](assets/callWebhook.png)

1. La campaña de avisos por SMS para clientes potenciales añadidos a un acuerdo ya está configurada.

>[!TIP]
>
>Este tutorial forma parte del curso [Agiliza los ciclos de ventas con Acrobat Sign para Salesforce y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponible de forma gratuita en el Experience League!