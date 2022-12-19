---
title: "Editar el manual localmente"
date: 2021-11-25T00:00:00-03:00
lastmod: 2021-12-13T00:00:00-03:00
weight: 1
draft: false
keywords: ["handbok", "manual", "local"]
mantained_by:
    - patricia.munoz
---

# Introducción

En esta página, se mostrará el como realizar cambios, añadir nuevas páginas o temas mas avanzados de edición del proyecto, mediante modificaciones en tu ambiente local.

DRAFT:

# Prerequisitos

-   Tener una cuenta en Github
-   Tener conocimientos minimos de git
-   Tener una llave SSH
-   Subir la llave a la cuenta personal en Github
-   Instalar Hugo en el ambiente local

# Pasos

## Instalación del ambiente

Esto es para Mac

[Instalar Hugo](https://gohugo.io/getting-started/installing/#homebrew-macos)

## ¿Cómo se suben los últimos cambios realizados en el manual?

Para que los cambios se puedan compartir y visualizar en nuestra página principal es necesario realizar un merge request.
Estos se pueden realizar por el terminal o directamente desde el Visual Stude Code.

-   Terminal:

    1.- Guardar los cambios realizados

    2.- Ir a la terminal y escribir los siguientes comandos:

    2.1.- En caso de tener ejecutando el servidor Hugo se debe bajar la consola con control + c

    2.2.- git status (Para saber el estado del repositorio)

    2.3.- git add . (Para que se consideren los cambios)

    2.4.- git commit -m "Mensaje commit" ( -m. Anuncia un mensaje, entre “”)

    2.5.- git push (Para que suba la información)

    3.- Hacer el Pull Request (PR) en github

    4.- Esperar que te aprueben el cambio.

-   VS Code:

    1.- Guardar los cambios

    2.- Realizar commit en tu rama para guardar los cambios nuevos.

    3.- Actualizar la rama desde el origen. (pull)

    4.- Hacer un push desde tu rama.

    5.- Hacer el PR en githubb

    6.- Esperar que te aprueben el cambio.

# Problemas y soluciones conocidas

## ¿Qué pasa si al subir un cambio nos llega un mail con la nota Failed jobs?

Podemos ingresar al número de Pipeline que te lleva directamente a la página para revisar cuál es el motivo del fallo.

## Al actualizar la rama desde el mail dejó de funcionar mi servidor local. Me da el siguiente error al iniciar el servidor

Al intentar subir el servidor (hugo server --disableFastRender --gc --buildDrafts) envía el siguiente mensaje:

**Error building site: "/Users/patriciamunoz/23people/handbok/content/company/the-handbok/\_index.es.md:1:1": plain HTML documents not supported**
Posterior a esto mata la sesión.

Esto puede ser porque al intentar subir el código git deja algunas líneas de comentarios en algunas páginas. Estos comentarios deben ser eliminados.

## Otro tipo de errores

**Error Validate branches Another open merge request already exists for this source branch: !20**
Este error se produce cuando existe pendiente de merge la misma rama.
