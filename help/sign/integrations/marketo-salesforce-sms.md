---
title: Envío de notificaciones mediante Adobe Sign para Salesforce y Marketo
description: Obtenga más información sobre cómo enviar un mensaje de texto, un correo electrónico o una notificación de inserción para que el firmante sepa que un acuerdo está en camino
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Envío de notificaciones mediante Adobe Sign para Salesforce y Marketo

Obtenga más información sobre cómo enviar un mensaje de texto, un correo electrónico o una notificación push para que el firmante sepa que un acuerdo está en camino mediante Adobe Sign, Adobe Sign para Salesforce, Marketo y Marketo Salesforce Sync. Para enviar notificaciones desde Marketo, primero debe adquirir o configurar una función de administración de SMS de Marketo. Este tutorial utiliza [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), pero hay otras soluciones SMS de Marketo disponibles.

## Requisitos previos

1. Instale Marketo Salesforce Sync.

   La información y el plugin más reciente para la sincronización de Salesforce están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instalación de Adobe Sign para Salesforce.

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Marketo Salesforce Sync y Adobe Sign para Salesforce, aparecen varias opciones nuevas en Marketo Admin Terminal.

![Administrador](assets/adminTab.png)

![Sincronización de objetos](assets/salesforceAdmin.png)

1. Haga clic en **Sincronizar esquema** si es la primera vez. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema1.png)

1. Si se está ejecutando la sincronización global, desactívela haciendo clic en **Desactivar sincronización global**.

   ![Desactivar](assets/disableGlobal.png)

1. Haga clic en **Actualizar esquema**.

   ![Actualizar 2](assets/refreshSchema2.png)

## Sincronizar los objetos personalizados

En el lado derecho, consulte Objetos personalizados basados en Candidatos, Contactos y Cuenta.

**Habilite** Sincronizar para los objetos en Candidato si desea activarlo cuando se añada un Candidato a un acuerdo en Salesforce.

**Habilite** Sincronizar para los objetos en Contacto si desea activarlo cuando se añada un Contacto a un acuerdo en Salesforce.

**Habilite** Sincronizar para los objetos en Cuenta si desea activarlo cuando se añada una cuenta a un acuerdo en Salesforce.

1. **Habilite** Sincronizar para los objetos personalizados que se muestran en el elemento principal deseado (Candidato, Contacto o Cuenta).

   ![Objetos personalizados](assets/customObjects.png)

1. Los siguientes activos muestran cómo **Activar sincronización**.

   ![Sincronización personalizada 1](assets/customObjectSync1.png)

   ![Sincronización personalizada 2](assets/customObjectSync2.png)

1. Cuando termine de activar la sincronización en los objetos personalizados, reactive la sincronización.

   ![Activar global](assets/enableGlobal.png)

## Crear el programa

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda, seleccione **Nueva carpeta de campaña** y asígnele un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **Nuevo programa** y asígnele un nombre. Deje todo lo demás como predeterminado y, a continuación, haga clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

## Configurar Twilio SMS

En primer lugar, asegúrese de que tiene una cuenta activa de Twilio y ha adquirido las funciones de SMS que necesita.

La configuración del webhook Marketo - Twilio SMS requiere tres parámetros Twilio de tu cuenta.

- SID de cuenta
- Token de cuenta
- Número de teléfono de Twilio

Recupere estos parámetros de su cuenta y abra su instancia de Marketo.

1. Haga clic en **Administrador** en la parte superior derecha.

   ![Administrador](assets/adminTab.png)

1. Haga clic en **Webhooks**, luego **Nuevo Webhook**.

   ![Webhooks](assets/webhooks.png)

1. Introduzca un **Nombre de Webhook** y **Descripción**.

1. Introduzca la siguiente URL y asegúrese de reemplazar las credenciales de **[ACCOUNT_SID]** y **[AUTH_TOKEN]** por las credenciales de Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Seleccione **POST** como tipo de solicitud.

1. Introduzca la siguiente **Plantilla** y asegúrese de reemplazar **[MY_TWILIO_NUMBER]** por el número de teléfono de Twilio y **[YOUR_MESSAGE]** por un mensaje de su elección.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Establezca la codificación del token de solicitud en Formulario/URL.

1. Establezca el tipo de respuesta en JSON y, a continuación, haga clic en **Guardar**.

## Configuración del activador de la campaña inteligente

1. En la sección Actividades de marketing, haga clic con el botón derecho en el programa que ha creado y, a continuación, seleccione **Nueva campaña inteligente**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asígnele un nombre y haga clic en **Crear**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Si la configuración de la sincronización de objetos personalizados se ha realizado correctamente, debería ver los siguientes activadores disponibles para su uso en la carpeta Salesforce.

1. Haga clic y arrastre Agregado al acuerdo a la lista inteligente. Añada las restricciones que desee tener en el activador.

   ![Añadido al acuerdo 2](assets/addedToAgreement2.png)

## Configuración del flujo de campaña inteligente

1. Haga clic en la ficha **Flow** en Smart Campaign. Busque y arrastre el flujo **Llamar a Webhook** al lienzo y seleccione el webhook que creó en la sección anterior.

   ![Llamar a Webhook](assets/callWebhook.png)

1. Ya está configurada tu campaña de notificación SMS para los posibles clientes que se añaden a un acuerdo.

>[!TIP]
>
>Este tutorial forma parte del curso [Acelerar los ciclos de ventas con Adobe Sign para Salesforce y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1), que está disponible de forma gratuita para el Experience League.