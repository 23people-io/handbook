---
title: "Historias de Usuario"
date: 2022-04-12T00:00:00-03:00
lastmod: 2022-04-12T00:00:00-03:00
weight: 3
description: "¿Cuál es la definición de terminado que utilizamos en nuestros proyectos?"
draft: false
keywords: ["HU", "historias", "Gherkin", "usuario"]
mantained_by:
    - patricia.munoz
---

![img-user-stories](../img-user-stories.png)

### ¿Qué son las Historias de Usuario?

Si esto se lo consultamos a google nos indicará: _"Las historias de usuario son descripciones cortas y simples de una funcionalidad, escritas desde la perspectiva de la persona que necesita una nueva capacidad de un sistema, por lo general el usuario, área de negocio o cliente"_.

Algunas de las características que debemos tener en cuenta:

1. Deben ser peticiones pequeñas, que idealmente no impliquen largos períodos de trabajo.
1. Deben ser creadas por el cliente (PO) y puede ser conversada con el equipo.
1. Deben ser pensadas en la finalidad del producto.

### ¿Qué estructura de Historias de Usuario utilizamos en 23people?

-   #### TITULO

**Como** Donde se especifique el tipo de usuario para quién se hace la funcionalidad.

**Deseo** Aclarando cuales son los objetivos a los que tenemos que enfrentarnos.

**Tal que** Definiendo el motivo del lado de negocio por el cual se ha creado la historia.

-   #### CRITERIOS DE ACEPTACION

Para establecer criterios de aceptación utilizamos los escenarios de Gherkin.

**Y qué o quién es Gherkin?**

Gherkin es un Lenguaje Específico de Dominio (DSL), que son lenguajes diseñados en concreto para resolver un problema muy específico. Y, en este caso, el problema que quiere solucionar Gherkin es un problema de comunicación entre los perfiles de negocio y los perfiles técnicos.
Gherkin está compuesto por varios elementos que permiten esta comunicación entre perfiles de negocio y técnicos de forma sencilla.

**Los elementos más utilizados**
Podemos tener uno o varios escenarios. Es recomendado comenzar por los positivos.

**Escenario:** todas las acciones que un usuario podría realizar (incluida la entrada incorrecta)

**DADO:** (Escrito en pasado) Son las precondiciones para que se puedan ejecutar x acciones. Es un elemento de tipo acción. Establece el contexto. ¿En qué página estamos y en qué estado estamos? ¿El usuario es administrador? ¿Registrado? ¿Ha creado una campaña?

**CUÁNDO:** (Escrito en presente) Se trata de las condiciones de las acciones que se van a ejecutar y es un elemento de tipo acción. ¿Qué acciones está realizando el usuario?. ¿Qué evento ocurrió?

**ENTONCES:** (Escrito en futuro) Se trata del resultado esperado de las acciones ejecutadas, también es un elemento de tipo acción. ¿Qué debe hacer el sistema en respuesta? ¿Cuál es el resultado esperado?

Revisemoslo con un ejemplo simple:

**HU:** inicio de sesión en la tienda online.

**Escenario:** inicio de sesión mediante usuario y contraseña.

**Dado** que el usuario ha de introducir de forma correcta su usuario y su contraseña, que ha registrado previamente.

**Cuando** el usuario hace click sobre el botón de iniciar sesión

**Entonces** el usuario puede iniciar sesión de forma correcta.

-   #### FUENTES DE DATOS

En este punto nos referimos desde donde tomamos los datos, el origen de los datos, para trabajar en esta Historia de Usuario.

-   #### AMBIENTE DE DESPLIEGUE

¿En que ambiente debemos ejecutar esta Historia de Usuario?

-   #### EXPECTATIVAS NO FUNCIONALES

Es lo que se espera en relación a puntos técnicos como por ejemplo de qué color será nuestra página, de qué tipo será el archivo que se debe adjuntar, cómo será la estructura de la página,

-   #### COMO HACER EL DEMO

Aquí debemos indicar de qué forma podemos mostrar que nuestra Historia de Usuario ya se ha realizado según lo solicitado.

-   #### DEFINICION DE TERMINADO

En el siguiente link podemos encontrar la [**Definición de Terminado**](http://localhost:1313/engineering/how-we-work/definition-of-done/)
