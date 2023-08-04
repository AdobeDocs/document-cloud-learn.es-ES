---
title: Recopilación de documentos de gran volumen mediante GigaSign
description: Gigasign le permite enviar, recopilar y realizar el seguimiento de documentos para su firma a miles de personas al mismo tiempo
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 5%

---

# Recopilación de documentos de gran volumen mediante GigaSign

Gigasign le permite enviar, recopilar y realizar el seguimiento de documentos para su firma a miles de personas al mismo tiempo. Se ha diseñado para comunicaciones de gran volumen con sus empleados y clientes, y ofrece asistencia a un máximo de 2500 destinatarios con cada envío masivo. GigaSign utiliza la API de Acrobat Sign para proporcionar la misma funcionalidad que MegaSign e incluye compatibilidad con varios firmantes, grupos de destinatarios, funciones de destinatarios, nombres de acuerdos, copia de seguridad y mucho más.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Descargar e instalar la aplicación GigaSign

[Descargar archivo Zip de GigaSign](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Vínculo de descarga de Java 1.8 (solo si es necesario)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[Direcciones IP a lista blanca (solo si es necesario)](https://helpx.adobe.com/es/sign/system-requirements.html#IPs){target="_blank"}

## Instrucciones básicas de configuración

1. Inicie sesión en la cuenta de Acrobat Sign.

1. Haga clic en **[!UICONTROL Grupo]** o **[!UICONTROL Cuenta]**, lo que se vea en la parte superior.

1. Escriba &quot;Tokens de acceso&quot; en el campo de búsqueda en la parte izquierda de la pantalla.

1. Presione el icono &quot;+&quot; en el lado derecho.

1. Cree una clave con los ámbitos necesarios (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Haga doble clic en la tecla que ha creado y copie el texto completo (se sale de la pantalla a la derecha, así que asegúrese de que lo obtiene todo).

1. Abra GigaSign.

1. Haga clic en **[!UICONTROL Configuración]** en la parte superior derecha.

1. Pegue la clave de integración en la primera línea.

1. Introduzca la dirección de correo electrónico de la cuenta utilizada para crear esa clave en la segunda línea.

1. Haga clic en **[!UICONTROL Enviar]**.
