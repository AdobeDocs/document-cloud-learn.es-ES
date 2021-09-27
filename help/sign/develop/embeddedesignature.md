---
title: Creación de experiencias de firma electrónica y documento incrustadas
description: Aprenda a utilizar las API de Adobe Sign para incrustar experiencias de firma electrónica y documentos en las plataformas web y los sistemas de gestión de contenido y documentos
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: f015bd7ea1a25772a12cd0852d452d120f205a5c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Crear experiencias de firma electrónica y documento incrustadas

Aprenda a utilizar las API de Adobe Sign para incrustar experiencias de firma electrónica y documentos en sus plataformas web y sistemas de administración de contenido y documentos. Este tutorial práctico consta de cuatro partes y se describe en los vínculos siguientes:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="embeddedesignature.md#part1">
        <img alt="Lo que necesitarás" src="assets/embeddedesignature/EmbedPart1_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part1"><strong>Parte 1: Lo que necesitarás</strong></a>
    </div>
  </td>
  <td>
    <a href="embeddedesignature.md#part2">
        <img alt="Parte 2: Código bajo/sin — el poder de los formularios web" src="assets/embeddedesignature/EmbedPart2_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part2"><strong>Parte 2: Código bajo/sin — el poder de los formularios web</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part3">
      <img alt="Parte 3: Enviar acuerdo con un formulario, combinar datos" src="assets/embeddedesignature/EmbedPart3_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part3"><strong>Parte 3: Enviar un acuerdo con un formulario y combinar datos</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part4">
      <img alt="Parte 4: Incrustar experiencia de firma, redirecciones y mucho más" src="assets/embeddedesignature/EmbedPart4_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part4"><strong>Parte 4: Incrustar experiencia de firma, redirecciones y mucho más</strong></a>
    </div>
  </td>
</tr>
</table>

## Parte 1: Lo que necesitarás {#part1}

En la primera parte, aprenderás a empezar con todo lo que necesitas para las partes 2 y 4. Comencemos por obtener las credenciales de API.

* [Cuenta de desarrollador de Adobe Sign](https://acrobat.adobe.com/es/es/sign/developer-form.html)
* [Código de inicio](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [Código VS (o editor de su elección)](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebrew
   * Linux — Instalador integrado
   * Windows — Chocolatey
   * Todo — https://www.python.org/downloads/

## Parte 2: Código bajo/sin — el poder de los formularios web {#part2}

En la segunda parte, explorarás la opción de bajo o sin código al usar formularios web. Siempre es buena idea ver si puedes evitar escribir código al principio.

1. Acceda a Adobe Sign con su cuenta de desarrollador.
1. Haga clic en **Publicar un formulario web** en la página principal.

   ![Captura de pantalla de la página de inicio de Adobe Sign](assets/embeddedesignature/embed_1.png)

1. Cree su acuerdo.

   ![Captura de pantalla de cómo crear un formulario web](assets/embeddedesignature/embed_2.png)

1. Incruste el acuerdo en una página HTML plana.
1. Experimente con la adición dinámica de parámetros de consulta.

   ![Captura de pantalla de adición de parámetros de consulta](assets/embeddedesignature/embed_3.png)

## Parte 3: Enviar un acuerdo con un formulario y combinar datos {#part3}

En la tercera parte, crearás acuerdos de forma dinámica.

Primero, tendrás que establecer el acceso. Con Adobe Sign, existen dos formas de conectarse mediante API. Tokens de OAuth y claves de integración. A menos que tenga una razón muy específica para usar OAuth con su aplicación, primero querrá explorar las claves de integración.

1. Seleccione **Clave de integración** en el menú **Información de API** en la ficha **Cuenta** de Adobe Sign.

   ![Captura de pantalla de dónde encontrar la clave de integración](assets/embeddedesignature/embed_4.png)

Ahora que tiene acceso e interactúa con la API, consulte lo que puede hacer con la API.

1. Vaya a [Métodos de la versión 6 de la API REST de Adobe Sign](http://adobesign.com/public/docs/restapi/v6).

   ![Captura de pantalla de cómo navegar por los métodos de la versión 6 de la API REST de Adobe Sign](assets/embeddedesignature/embed_5.png)

1. Utilice el token como valor &quot;portador&quot;.

   ![Captura de pantalla del valor del portador](assets/embeddedesignature/embed_6.png)

Para enviar su primer acuerdo, es mejor entender cómo utilizar la API.

1. Cree un documento transitorio y envíelo.

>[!NOTE]
>
>Las llamadas de solicitud basadas en JSON tienen la opción &quot;Modelo&quot; y &quot;Esquema de modelo mínimo&quot;. Esto proporciona especificaciones y un conjunto mínimo de carga.

![Captura de pantalla de creación de un documento transitorio](assets/embeddedesignature/embed_7.png)

Después de enviar un acuerdo por primera vez, ya puede añadir la lógica. Siempre es buena idea establecer algunos ayudantes para minimizar la repetición. A continuación se ofrecen algunos ejemplos:

**Validación**

![Captura de pantalla de la lógica de validación](assets/embeddedesignature/embed_8.png)

**Encabezados/autenticación**

![Captura de pantalla de los encabezados/lógica de autenticación](assets/embeddedesignature/embed_9.png)

**URI base**

![Captura de pantalla de la lógica URI base](assets/embeddedesignature/embed_10.png)

Tenga en cuenta dónde aterrizan los documentos transitorios dentro del gran esquema del ecosistema de Sign.
Transición -> Acuerdo
Transición -> Plantilla -> Acuerdo
Transitorio -> Widget -> Acuerdo

En este ejemplo se utiliza una plantilla como origen del documento. Normalmente, esta es la mejor ruta, a menos que tenga una razón sólida para generar dinámicamente documentos para firmar (por ejemplo, generación de código heredado o de documento).

El código es bastante sencillo; utiliza un documento de biblioteca (plantilla) para el origen del documento. Los firmantes primero y segundo se asignan de forma dinámica. El estado `IN_PROCESS` significa que el documento se envía inmediatamente. Además, `mergeFieldInfo` se aprovecha para rellenar campos de forma dinámica.

![Captura de pantalla del código para añadir firmas dinámicamente](assets/embeddedesignature/embed_11.png)

## Parte 4: Incrustar experiencia de firma, redirecciones y mucho más {#part4}

En muchos casos, es posible que desee permitir que el participante desencadenante firme inmediatamente un acuerdo. Esto resulta útil para aplicaciones y quioscos orientados al cliente.

Si no desea que se active el primer envío de correo electrónico, una forma sencilla es administrar el comportamiento mediante una modificación de la llamada de API.

![Captura de pantalla del código para no activar el envío de correo electrónico](assets/embeddedesignature/embed_12.png)

A continuación se explica cómo controlar la redirección posterior a la firma:

![Captura de pantalla del código para controlar la redirección posterior a la firma](assets/embeddedesignature/embed_13.png)

Después de actualizar el proceso de creación del acuerdo, el paso final es generar la URL de firma. Esta llamada también es bastante sencilla y genera una URL que un firmante puede utilizar para acceder a su parte del proceso de firma.

![Captura de pantalla del código para generar una URL de firmante](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Tenga en cuenta que la llamada de creación del acuerdo es técnicamente asíncrona. Esto significa que se puede realizar una llamada al acuerdo &quot;POST&quot;, pero el acuerdo aún no está listo. La práctica recomendada es establecer un bucle de reintento. Use un reintento o lo que sea la práctica recomendada para su entorno.

![Captura de pantalla que indica que se recomienda establecer un bucle de reintento](assets/embeddedesignature/embed_15.png)

Cuando todo está unido, la solución es bastante sencilla. Está realizando un acuerdo y, a continuación, generando una URL de firma para que el firmante haga clic en y comience el ritual de firma.

### Temas adicionales

* [Eventos de JS](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Eventos de Webhook
   * [API REST](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks en Adobe Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Reactivar correos electrónicos de solicitud (con eventos)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Reemplazar tiempo de espera por un reintento](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)

   <br> 
* Recordatorios personalizados
   * Con la creación inicial

      ![Captura de pantalla de la navegación a Power Automate](assets/embeddedesignature/embed_16.png)

   * O bien, añada una [en vuelo](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)

## Recursos adicionales

http://bit.ly/Summit21-T126

Incluye:
* Cuenta de desarrollador de Adobe Sign
* Documentos de la API de Adobe Sign
* Código de muestra
* Código de Visual Studio
* Python
