---
title: Crear firmas electrónicas incrustadas y experiencias con documentos
description: Aprende a utilizar las API de Acrobat Sign para insertar firmas electrónicas y experiencias con documentos en tus plataformas web y sistemas de gestión de contenidos y documentos
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Crea firmas electrónicas incrustadas y experiencias con documentos

Aprende a utilizar las API de Acrobat Sign para insertar firmas electrónicas y experiencias de documentos en tus plataformas web y sistemas de gestión de contenidos y documentos. Este tutorial práctico consta de cuatro partes que se describen en los vínculos siguientes:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="embeddedesignature.md#part1">
        <img alt="Lo que va a necesitar" src="assets/embeddedesignature/EmbedPart1_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part1"><strong>Parte 1: Lo que va a necesitar</strong></a>
    </div>
  </td>
  <td>
    <a href="embeddedesignature.md#part2">
        <img alt="Parte 2: Código bajo/sin: el poder de los formularios web" src="assets/embeddedesignature/EmbedPart2_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part2"><strong>Parte 2: Código bajo/sin: el poder de los formularios web</strong></a>
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
      <img alt="Parte 4: Incrusta la experiencia de firma, las redirecciones y mucho más" src="assets/embeddedesignature/EmbedPart4_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part4"><strong>Parte 4: Incrusta la experiencia de firma, las redirecciones y mucho más</strong></a>
    </div>
  </td>
</tr>
</table>

## Parte 1: Lo que va a necesitar {#part1}

En la parte 1, aprenderás a empezar con todo lo que necesitas para las partes 2-4. Vamos a empezar a obtener credenciales de API.

* [Cuenta de desarrollador de Acrobat Sign](https://acrobat.adobe.com/es/es/sign/developer-form.html)
* [Código de inicio](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS Code (o editor de su elección)](https://code.visualstudio.com)
* Python 3.x
   * Mac: Homebrew
   * Linux: instalador incorporado
   * Windows: Chocolatey
   * Todos: https://www.python.org/downloads/

## Parte 2: Código bajo/sin: el poder de los formularios web {#part2}

En la parte 2, explorarás la opción de bajo/sin código al usar formularios web. Siempre es una buena idea comprobar si puedes evitar escribir código al principio.

1. Accede a Acrobat Sign con tu cuenta de desarrollador.
1. Haga clic en **Publicar un formulario web** en la página principal.

   ![Captura de pantalla de la página principal de Acrobat Sign](assets/embeddedesignature/embed_1.png)

1. Cree su acuerdo.

   ![Captura de pantalla de cómo crear un formulario web](assets/embeddedesignature/embed_2.png)

1. Incruste el acuerdo en una página plana del HTML.
1. Experimente con la adición dinámica de parámetros de consulta.

   ![Captura de pantalla de adición de parámetros de consulta](assets/embeddedesignature/embed_3.png)

## Parte 3: Enviar un acuerdo con un formulario y combinar datos {#part3}

En la parte 3, creará acuerdos dinámicamente.

En primer lugar, deberá establecer el acceso. Con Acrobat Sign, hay dos formas de conectarse mediante API. Tokens de OAuth y claves de integración. A menos que tenga una razón muy específica para utilizar OAuth con la aplicación, es conveniente explorar primero las claves de integración.

1. Seleccionar **Clave de integración** en la **Información de API** bajo el menú **Cuenta** en Acrobat Sign.

   ![Captura de pantalla de dónde encontrar la clave de integración](assets/embeddedesignature/embed_4.png)

Ahora que tiene acceso a la API y puede interactuar con ella, consulte lo que puede hacer con ella.

1. Vaya a la [Métodos de la versión 6 de la API REST de Acrobat Sign](http://adobesign.com/public/docs/restapi/v6).

   ![Captura de pantalla de navegación por los métodos de la API REST versión 6 de Acrobat Sign](assets/embeddedesignature/embed_5.png)

1. Utilice el token como valor &quot;portador&quot;.

   ![Captura de pantalla del valor al portador](assets/embeddedesignature/embed_6.png)

Para enviar su primer acuerdo, lo mejor es saber cómo utilizar la API.

1. Cree un documento transitorio y envíelo.

>[!NOTE]
>
>Las llamadas de solicitud basadas en JSON tienen las opciones &quot;Modelo&quot; y &quot;Esquema de modelo mínimo&quot;. Esto proporciona especificaciones y un conjunto mínimo de carga útil.

![Captura de pantalla de creación de un documento transitorio](assets/embeddedesignature/embed_7.png)

Después de enviar un acuerdo por primera vez, ya puede añadir la lógica. Siempre es una buena idea establecer algunos ayudantes para minimizar la repetición. A continuación se ofrecen algunos ejemplos:

**Validación**

![Captura de pantalla de la lógica de validación](assets/embeddedesignature/embed_8.png)

**Encabezados/autenticación**

![Captura de pantalla de encabezados/lógica de autenticación](assets/embeddedesignature/embed_9.png)

**URI base**

![Captura de pantalla de lógica de URI base](assets/embeddedesignature/embed_10.png)

Tenga en cuenta dónde se incluyen los documentos transitorios en el esquema general del ecosistema de Sign.
Transient -> Agreement Transient -> Template -> Agreement Transient -> Widget -> Agreement

En este ejemplo se utiliza una plantilla como origen de documento. Esta suele ser la mejor opción, a menos que tenga una razón sólida para generar dinámicamente documentos para su firma (por ejemplo, código heredado o generación de documentos).

El código es bastante sencillo; utiliza un documento de biblioteca (plantilla) para el origen del documento. El primer y el segundo firmante se asignan dinámicamente. La `IN_PROCESS` estado significa que el documento se envía inmediatamente. Además, `mergeFieldInfo` se aprovecha para rellenar campos de forma dinámica.

![Captura de pantalla de código para añadir firmas dinámicamente](assets/embeddedesignature/embed_11.png)

## Parte 4: Incrusta la experiencia de firma, las redirecciones y mucho más {#part4}

En muchos casos, es posible que desee permitir que el participante que realiza la activación firme inmediatamente un acuerdo. Esto resulta útil para aplicaciones y quioscos orientados al cliente.

Si no desea que se active el primer envío de correo electrónico, una forma sencilla es administrar el comportamiento mediante una modificación de la llamada de la API.

![Captura de pantalla de código para no activar el envío de correo electrónico](assets/embeddedesignature/embed_12.png)

A continuación se indica cómo controlar la redirección posterior a la firma:

![Captura de pantalla del código para controlar la redirección posterior a la firma](assets/embeddedesignature/embed_13.png)

Después de actualizar el proceso de creación del acuerdo, el paso final es generar la URL de firma. Esta llamada también es bastante sencilla y genera una dirección URL que un firmante puede utilizar para acceder a su parte del proceso de firma.

![Captura de pantalla de código para generar una URL de firmante](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Tenga en cuenta que la llamada de creación del acuerdo es técnicamente asincrónica. Esto significa que se puede realizar una llamada al acuerdo &quot;POST&quot;, pero el acuerdo aún no está listo. La práctica recomendada es establecer un bucle de reintento. Utilice un reintento o lo que sea la práctica recomendada para su entorno.

![Captura de pantalla que indica que es recomendable establecer un bucle de reintento](assets/embeddedesignature/embed_15.png)

Cuando todo se junta, la solución es bastante sencilla. Está realizando un acuerdo y, a continuación, generando una URL de firma para que el firmante haga clic en él y comience el ritual de firma.

### Temas adicionales

* [Eventos de JS](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Eventos de webhook
   * [API REST](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks en Acrobat Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Reactivar correos electrónicos de solicitud (con eventos)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Reemplazar el tiempo de espera con un reintento](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)

   <br> 
* Recordatorios personalizados
   * Con la creación inicial

      ![Captura de pantalla de la navegación a Power Automate](assets/embeddedesignature/embed_16.png)

   * O añade uno [en vuelo](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)

## Recursos adicionales

http://bit.ly/Summit21-T126

Incluye:
* Cuenta de desarrollador de Acrobat Sign
* Documentos de API de Acrobat Sign
* Código de ejemplo
* Visual Studio Code
* Python
