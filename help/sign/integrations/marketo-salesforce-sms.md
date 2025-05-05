---
title: Enviar notificaciones con Acrobat Sign para Salesforce y Marketo
description: Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Enviar notificaciones mediante Acrobat Sign para [!DNL Salesforce] y [!DNL Marketo]

Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino mediante Acrobat Sign, Acrobat Sign para Salesforce, Marketo y Marketo Salesforce Sync. Para enviar notificaciones desde Marketo, primero debe adquirir o configurar una función de administración de SMS de Marketo. Este tutorial utiliza [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), pero hay disponibles otras soluciones de SMS de Marketo.

## Requisitos previos

1. Instale Marketo Salesforce Sync.

   La información y el complemento más reciente para la sincronización de Salesforce están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html?lang=es)

1. Instale Acrobat Sign para Salesforce.

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Sincronización de Marketo Salesforce y Acrobat Sign para Salesforce, aparecen varias opciones nuevas en el Terminal de administración de Marketo.

![Administrador](assets/adminTab.png)

![Sincronización de objetos](assets/salesforceAdmin.png)

1. Haga clic en **Sincronizar esquema** si es la primera vez que lo hace. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema1.png)

1. Si se está ejecutando la sincronización global, deshabilítela haciendo clic en **Deshabilitar sincronización global**.

   ![Deshabilitar](assets/disableGlobal.png)

1. Haga clic en **Actualizar esquema**.

   ![Actualizar 2](assets/refreshSchema2.png)

## Sincronizar los objetos personalizados

En el lado derecho, consulte Objetos personalizados basados en clientes potenciales, contactos y cuentas.

**Habilite la sincronización** para los objetos en Candidato si desea activarla cuando se agregue un Candidato a un acuerdo en Salesforce.

**Habilite la sincronización** para los objetos en Contacto si desea activarla cuando se agregue un contacto a un acuerdo en Salesforce.

**Habilite la sincronización** para los objetos de Account si desea activarla cuando se agregue una cuenta a un acuerdo en Salesforce.

1. **Habilite la sincronización** para los objetos personalizados que se muestran bajo el elemento principal deseado (Candidato, Contacto o Cuenta).

   ![Objetos personalizados](assets/customObjects.png)

1. Los siguientes activos muestran cómo **Habilitar sincronización**.

   ![Sincronización personalizada 1](assets/customObjectSync1.png)

   ![Sincronización personalizada 2](assets/customObjectSync2.png)

1. Cuando haya terminado de activar la sincronización en los objetos personalizados, vuelva a activar la sincronización.

   ![Habilitar global](assets/enableGlobal.png)

## Crear el programa

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda, seleccione **Nueva carpeta de campaña** y asígnele un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **Nuevo programa** y asígnele un nombre. Deja todo lo demás como predeterminado y luego haz clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

## Configurar Twilio SMS

Primero asegúrese de tener una cuenta activa de Twilio y compró las características de SMS que necesita.

La configuración del webhook Marketo - Twilio SMS requiere tres parámetros de Twilio de su cuenta.

- SID de cuenta
- Token de cuenta
- Número de teléfono Twilio

Recupere estos parámetros de su cuenta y abra su instancia de Marketo.

1. Haz clic en **Administrador** en la parte superior derecha.

   ![Administrador](assets/adminTab.png)

1. Haz clic en **Webhooks** y, a continuación, en **New Webhook**.

   ![Webhooks](assets/webhooks.png)

1. Escriba un **Nombre de webhook** y una **Descripción**.

1. Introduzca la siguiente URL y asegúrese de reemplazar **[ACCOUNT_SID]** y **[AUTH_TOKEN]** por sus credenciales de Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecciona **POST** como tu tipo de solicitud.

1. Introduce la siguiente **plantilla** y asegúrate de reemplazar **[MY_TWILIO_NUMBER]** por tu número de teléfono Twilio y **[YOUR_MESSAGE]** por un mensaje de tu elección.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Establezca Codificación del token de solicitud en Formulario/URL.

1. Establezca el tipo de respuesta en JSON y, a continuación, haga clic en **Guardar**.

## Configurar el activador inteligente de la campaña

1. En la sección Actividades de marketing, haz clic con el botón derecho en el programa que has creado y, a continuación, selecciona **Nueva campaña inteligente**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asígnele un nombre y, a continuación, haga clic en **Crear**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Si la configuración de la sincronización de objetos personalizados se ha realizado correctamente, debería ver los siguientes desencadenadores disponibles para su uso en la carpeta Salesforce.

1. Haga clic en Añadir al acuerdo y arrástrelo a la lista inteligente. Añada las restricciones que desee tener en el activador.

   ![Agregado al acuerdo 2](assets/addedToAgreement2.png)

## Configurar el flujo de campaña inteligente

1. Haz clic en la pestaña **Flujo** en Smart Campaign. Busque y arrastre el flujo **Call Webhook** al lienzo y seleccione el webhook que creó en la sección anterior.

   ![Llamar a webhook](assets/callWebhook.png)

1. La campaña de avisos por SMS para clientes potenciales añadidos a un acuerdo ya está configurada.
