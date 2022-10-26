---
title: "Actualizando enrutamiento de correos"
date: 2022-01-05T00:00:00-03:00
lastmod: 2022-01-05T00:00:00-03:00
weight: 1
draft: false
keywords:
    [
        "enrutamiento",
        "routing",
        "gmail",
        "cuentas",
        "correos",
        "email",
        "redirigir",
    ]
mantained_by:
    - manu.reyes
---

# Introducción

A continuación, se muestra lo necesario para que los correos (emails) que llegan a una determinada cuenta, alias o grupo de correos en Gmail (cuenta empresa) se redirigan (o enruten) hacia otro correo de interés.

**Como ejemplo a seguir**, se presenta el siguiente caso:

El equipo de Obtención de Talento TI (Equipo Valhalla), necesita que los correos que lleguen a la cuenta _"talento@23people.io"_, se redirijan al correo 23people de un miembro nuevo en su equipo (e.g Nicolas Vergara, *nicolas.vergara@23people.io*).

# Precondiciones

El procedimiento a continuación, asume que el usuario que lo hará, **tiene permisos administrativos** para hacer esto.

# Procedimiento

Para referencia, la documentación de Google para esto, se puede acceder en [este link](https://apps.google.com/supportwidget/articlehome?hl=en&article_url=https%3A%2F%2Fsupport.google.com%2Fa%2Fanswer%2F4524505%3Fhl%3Den&product_context=4524505&product_name=UnuFlow&trigger_context=a).

A continuación, la guia paso a paso:

1. Ir a la consola de administración de google ([admin.google.com](https://admin.google.com/)) y autenticarse.
   ![admin-google-image](../images/admin-console.png)
2. Ir a [Apps > Google Workspace > Gmail > Routing](https://admin.google.com/ac/apps/gmail/routing)
   ![routing-image](../images/routing-main.png)
3. Bajar en la pagina y llegar a la sección **Recipient address map** y presionar **edit** en el mapeo de enrutamiento de correos de interés (en este ejemplo, _Mapping Mail Obtencion Talento TI_)
   ![routing-section-image](../images/routing-section.png)
4. En la ventana "Edit Setting" que apareció desde el paso anterior, bajar hasta la sección **"For the above types of messages, rewrite the recipients:"**
   ![routing-edit-image](../images/routing-edit.png)
5. Presionar el boton **ADD** para añadir una nueva linea de mapeo de enrutamiento de correos
   ![edit-adding-route-image](../images/edit-adding-route.png)
6. Completar los datos de origen ("address") y destino del mapeo de correos (**"Map to adress"**) y presionar el boton **"SAVE"**
   ![edit-route-saving-image](../images/edit-route-saving.png)
7. Esperar a que guarde y se cierre la ventana.

Con estos pasos, se espera que los correos que lleguen al correo objetivo, se redirijan al correo de destino.
