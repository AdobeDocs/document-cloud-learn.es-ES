---
title: Enviar recordatorios mediante la Guía de configuración de Adobe Sign para Salesforce y Marketo
description: Obtenga más información sobre cómo enviar un recordatorio por correo electrónico de Marketo cuando un acuerdo no se ha firmado después de un período de tiempo
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Enviar recordatorios mediante la Guía de configuración de Adobe Sign para Salesforce y Marketo

Obtenga más información sobre cómo enviar un recordatorio por correo electrónico de Marketo cuando un acuerdo permanece sin firmar después de un período de tiempo. Esta integración utiliza Adobe Sign, Adobe Sign para Salesforce, Marketo y Marketo y Salesforce Sync.

## Requisitos previos

1. Instale Marketo Salesforce Sync.

   La información y el plugin más reciente para la sincronización de Salesforce están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instalación de Adobe Sign para Salesforce.

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Buscar el objeto personalizado

Cuando se completan las configuraciones de Marketo Salesforce Sync y Adobe Sign para Salesforce, aparecen varias opciones nuevas en Marketo Admin Terminal.

![Administrador](assets/adminTab.png)

![Sincronización de objetos](assets/salesforceAdmin.png)

1. Haga clic en **Sincronizar esquema** si es la primera vez. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema1.png)

1. Si se está ejecutando la sincronización global, desactívela haciendo clic en **Desactivar sincronización global**.

   ![Desactivar](assets/disableGlobal.png)

1. Haga clic en **Actualizar esquema**.

   ![Actualizar 2](assets/refreshSchema2.png)

## Sincronizar el objeto personalizado

En el lado derecho, consulte Objetos personalizados basados en Candidatos, Contactos y Cuenta.

**Active Sincronizar** los objetos en Candidato si desea enviar un recordatorio cuando un Candidato no haya firmado un acuerdo en Salesforce.

**Active Sincronizar** los objetos en Contacto si desea enviar un recordatorio cuando un Contacto no haya firmado un acuerdo en Salesforce.

**Active Sincronizar** los objetos en Cuenta si desea enviar un recordatorio cuando una cuenta no haya firmado un acuerdo en Salesforce.

1. **Habilite** Sincronizar para el  **** objeto Agreement que se muestra en el elemento principal deseado (Candidato, Contacto o Cuenta). Realice esta acción para cualquier otro objeto personalizado que desee sincronizar.

   ![Objeto Agreement](assets/agreementObject.png)

1. Los siguientes activos muestran cómo **Activar sincronización**.

   ![Sincronización personalizada 1](assets/customObjectSync1.png)

   ![Sincronización personalizada 2](assets/customObjectSync2.png)

## Exponer los campos de objeto personalizados a los activadores

1. Mientras la sincronización global está desactivada, seleccione el objeto personalizado del acuerdo para el que habilitó la sincronización y, a continuación, **Editar campos visibles**.

1. Marque el campo &quot;Nombre del acuerdo&quot; en la columna del activador para mostrarlo a sus activadores de acciones de campaña. Marque cualquier otro campo por el que desee filtrar y, a continuación, **Guardar**.

   ![Editar campos visibles 1](assets/editVisible1.png)

   ![Editar campos visibles 2](assets/editVisible2.png)

1. Cuando termine de activar la sincronización en los objetos personalizados y de exponer los valores del activador, recuerde reactivar la sincronización:

   ![Activar global](assets/enableGlobal.png)

## Crear el programa y el token

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda, seleccione **Nueva carpeta de campaña** y asígnele un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **Nuevo programa** y asígnele un nombre. Deje todo lo demás como predeterminado y, a continuación, haga clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

1. Haga clic en **Mis tokens** y, a continuación, arrastre **Script de correo electrónico** al lienzo.

   ![Script de correo electrónico](assets/emailScript.png)

1. Asigne un nombre y haga clic en **Haga clic para editar**.

   ![Nombre y edición](assets/nameAndSave.png)

1. Expanda **Objetos personalizados** en el lado derecho y, a continuación, expanda el objeto **Acuerdo**. Busque y arrastre el nombre del acuerdo, el estado del acuerdo, la fecha de firma y la dirección URL de firma al lienzo.

1. Escriba una secuencia de comandos Velocity utilizando estos distintivos para mostrar la dirección URL del acuerdo de un acuerdo sin firmar durante una semana. A continuación se muestra un ejemplo que compara la fecha actual con la fecha de envío:

   ```
   #foreach($agreement in $echosign_dev1__SIGN_Agreement__cList)
       #if($agreement.echosign_dev1__Status__c == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.echosign_dev1__DateSent__c)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.Name)
               #set($agreementURL = $agreement.echosign_dev1__Signing_URL__c.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. Haga clic en **Guardar**.

## Crear el recordatorio y añadir personalización

Algunos ejemplos de personalización son: el nombre del firmante, el nombre del acuerdo, un vínculo al acuerdo, etc.

1. Haga clic con el botón derecho en el programa que creó y haga clic en **Nuevo activo local** y, a continuación, seleccione **Correo electrónico**.

   ![Nuevo correo electrónico](assets/createNewEmail.png)

1. En la nueva ficha, introduzca un **Nombre** y una **Descripción** para el correo electrónico y seleccione una plantilla del selector de plantillas. Haga clic en **Crear**.

   ![Selector de plantilla](assets/templatePicker.png)

1. Establezca los valores **Desde nombre** y **Desde dirección**.

   ![Correo electrónico recordatorio](assets/reminderEmail.png)

1. Haga clic en el cuerpo del mensaje para activar el editor. Haga clic en el botón **Insertar token**, busque el token de URL de acuerdo personalizado que creó y, a continuación, haga clic en **Insertar**. Termine de personalizar su correo electrónico y haga clic en **Guardar**.

   ![Insertar token](assets/insertToken.png)

1. Vista previa mediante un perfil que tenga asignado un acuerdo. Debe ver un vínculo a la URL con el nombre del acuerdo como etiqueta.

   ![Vínculo de correo electrónico](assets/emailLink.png)

## Configuración del filtro de campaña inteligente

1. Haga clic con el botón derecho en el programa que creó y, a continuación, haga clic en **Nueva campaña inteligente**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asigne un nombre a su elección y, a continuación, haga clic en **Crear**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Busque y, a continuación, haga clic y arrastre **Tiene acuerdo** a la lista inteligente.

   ![Tiene acuerdo](assets/hasAgreement.png)

1. Los campos que expuso al activador ahora deben estar disponibles en **Agregar restricción**. Seleccione **Estado del acuerdo** y cualquier otro campo por el que desee filtrar. Para cada campo agregado, defina los valores por los que filtrar. En este caso, solo se activará cuando el **Estado del acuerdo** esté Enviado para firmar y **Fecha de envío** esté en el pasado antes de 7 días.

   ![Estado del acuerdo](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d un identificador único para las restricciones, como **Nombre del acuerdo**, si desea que esta campaña se ejecute solo para determinados acuerdos.

1. Confirme la audiencia de la campaña y vea quién calificará en la ficha Programación.

   ![Calificadores](assets/qualifiers.png)

## Configuración del flujo de campaña inteligente

Dado que se utilizó el filtro de campaña **Días sin firmar**, puede utilizar una periodicidad programada para la campaña.

1. Haga clic en la ficha **Flow** en Smart Campaign. Busque y arrastre el flujo **Enviar correo electrónico** al lienzo y seleccione el correo electrónico de recordatorio que creó en la sección anterior.

   ![Enviar correo electrónico](assets/sendEmail.png)

1. Haga clic en la ficha **Programar** en la campaña inteligente. Asegúrese de que el flujo de campaña esté limitado a ejecutarse solo una vez por persona en la **Configuración de campaña inteligente**. A continuación, haga clic en la ficha **Programar repetición**.

   ![Pestaña Programar](assets/scheduleTab.png)

1. Establezca el **Programa** en Diario, elija un día y una hora de inicio y una fecha de finalización para la campaña si es necesario.

   ![Configuración de programación](assets/scheduleSettings.png)

>[!TIP]
>
>Este tutorial forma parte del curso [Acelerar los ciclos de ventas con Adobe Sign para Salesforce y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1), que está disponible de forma gratuita para el Experience League.
