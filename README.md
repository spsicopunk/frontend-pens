# Fury Frontend Mantra v2.0
[![nodo](https://img.shields.io/badge/Fury-Client-111)](https://furydocs.io/client)
[![styles](https://img.shields.io/badge/Styles-sass-ff69b4)](https://sass-lang.com/)
[![Andes](https://img.shields.io/badge/Webkit-Andes-3483fa)](https://andes.adminml.com)
[![Odin](https://img.shields.io/badge/Navigation-Odin-42b983)](https://furydocs.io/frontend-odin/)
[![Nordic](https://img.shields.io/badge/Frontend-Nordic-fff)](https://nordic.adminml.com/)
[![Odin](https://img.shields.io/badge/Test-Jest-6b2e85)](https://furydocs.io/frontend-odin/)
![nodo](https://img.shields.io/badge/node-v14-blue)
[![soporte](https://img.shields.io/badge/Soporte-Help_Mantra%40-green.svg)](https://meli.slack.com/archives/C016GDSQAHG)

### Tabla de contenido
- [Descripción](#descripción)
- [Requerimientos Básicos](#descripción)
- [Instalando entorno de desarrollo](#Instalando-entorno-de-desarrollo)
- [Donde empiezo?](#Donde-empiezo?)
- [Un poco de contexto](#Un-poco-de-contexto)
- [Componentes](#Componentes)
- [Contribuyendo](#contribuyendo)
- [Versionamiento](#Versionamiento)
- [Desarrollo](#Desarrollo)
- [Despliegue](#Despliegue)
- [Publicación](#Publicación)
- [Changelog](#Changelog)
- [Roadmap](#Roadmap)

## Descripción

Mantra es una herramienta para gestionar la calidad de las diferentes aplicaciones pertenecientes a los equipos y unidades de negocio.

Esta gestión de calidad se realiza a través de una serie de kpis (Indicadores de rendimiento), los cuales se utilizan para sintetizar información sobre la eficacia, productividad y previsibilidad de las acciones que se lleven a cabo en los equipos y unidades de negocio, con el fin de poder tomar decisiones y determinar aquellas que han sido más efectivas a la hora de cumplir con los objetivos marcados.

Este frontend tiene como proposito ser la guia visual de los indicadores de rendimiento de todos los equipos de Mercadolibre y se debera usar de sabiamente siguiendo las pautas de diseño y stack tecnologico [Andes](https://andes.adminml.com), [Nordic](https://nordic.adminml.com/) y [Odin](https://furydocs.io/frontend-odin/).

### Requerimientos Basicos
  - Node v14 no mayor
  - Agregar a /etc/hosts -> 127.0.0.1 local-mantra.adminml.com

### Instalando entorno de desarrollo
```sh
  $ cd fury_frontend-mantra
  $ npm install
 ```
### Donde empiezo?
  - ```npm run build```: comando usado para compilar el artefacto por primera vez 
  - ```npm run watch:``` es usado para ejecutar el comando build en todo momento 
  - **(En otro tab de la terminal ejecutar):** ``` npm run start-dev```: usado para correr el servidor de pruebas
  - **Navega en tu browser** a https://local-mantra.adminml.com:8443

### Un poco de contexto
  - Este proyecto esta construido con [React js](https://es.reactjs.org/docs/react-component.html) basado en componentes de clase
  - En el directorio ``` /api ``` se encuentra todo lo relacionado al consumo desde front al [Backend Mantra](https://github.com/mercadolibre/fury_backend-mantra) con [Goland](https://go.dev/)
  - Funcionalidades de JS, no componentes de la interfaz de usuario. En la mayoría de los casos es un código del lado del servidor, pero algunas funcionalidades están destinadas a funcionar en el lado del cliente (seguimiento, URL, constantes, etc.)

### Componentes

* ``` AlertCustomThreshold ``` componente encargado de mostrar alertas al guardar cambios en las notificaciones
* ``` Behavior ``` componente que visualiza en el home el total de aplicaciones en **Above** o **Below**

### Contribuyendo

Para informar un error o contribuir a la biblioteca, le recomendamos que se comunique con nosotros en **mantra@mercadolibre.com**.

Sin embargo, si ve algo que no está bien o necesita una nueva función, siga estos pasos para ayudar a resolverlo.
* [Crear un Problema en el repositorio](https://github.com/mercadolibre/fury_frontend-mantra/issues/new) correspondiente describiendo el problema
* Cuéntanoslo con un correo electrónico indicando su prioridad (esto es importante ya que tal vez la función que necesitas tiene una razón para no existir o tal vez alguien más ya está trabajando en ella). Puede enviar un correo electrónico a mantra@mercadolibre.com
* Si eres colaborador del equipo te recomendamos saltar al apartado de [Desarollo](#Desarollar)

### Versionamiento

Si estas colaborando el proyecto frontend mantra debes seguir los lineamiento del [Libflow](https://furydocs.io/release-proess/4.9.0/guide/#/lang-es/workflows/04_libflow) para el control de versiones en este proyecto.

### Desarrollo

Para desarrollar una nueva función, debe

* Para las nuevas funciones, le recomendamos que haga el trabajo RFC antes. Las opciones son un borrador de PR, un documento que describe o al menos una reunión con un colaborador
* Crear una rama con la nomenclatura indicada en [Versionamiento](#versionamiento) según el tipo de ajuste ejm: `feature/mantra-432-notifications` osea `feature/Mantra-(Numero de Historia)-(Nombre descriptivo)`
* Seguido a crear la rama, haz el trabajo
* Para correr los test unitarios localmente (puede usar `npm run test:unit`)
* Para correr los test slint localmente (puede usar `npm run lint`)
* Seguido se debe actualizar la versión [CHANGELOG.MD](CHANGELOG.md) con los ajustes y tipo de ajuste correspondiente con Nomenclatura de [versionamiento semántico](https://semver.org/lang/es/)
* Actualice su versión `package.json` de igual manera con [versionamiento semántico](https://semver.org/lang/es/) teniendo en cuenta la ultima versión del [CHANGELOG.MD](CHANGELOG.md)
* Una vez hecho los pasos anteriores ejecuta `fury create-version` (comprueba en fury que la versión se está creando correctamente) 
* Cuando se termine de generar la versión es aconsejable desplegar con una estrategia de despliegue [Blue Green en fury](https://web.furycloud.io/frontend-mantra/deployments-new) con los parametros de Block size = 100 & Swap Interval = 10
* Pruébelo en un ambiente dedicado a Mantra (Ya sea [Test](https://test-mantra.adminml.com/) o [Stage](https://staging-mantra.adminml.com/)) y esta prohibido desplegar en scope de Producción sino es rama Release o Master.

**NOTA**: No olvide agregar una descripción de registro de cambios para cada paquete (siga los ejemplos actuales)

### Desplegue
Teniendo en cuenta que los cambios sean correctos se debe:

* Crear un pull request desde la rama modificada con base de **Develop** y pedir la aprobación de algún colaborador del proyecto
* Si todo el pipeline es exitoso y se mezclan los cambios a **Develop** se aconseja eliminar la rama Feature y crear una nueva rama release/2.20.4 (Esta nomenclatura puede variar y se recomienda ver cual es la versión más actual en el repositorio para continuar con el versionamiento) 
* Teniendo el ejemplo de la version release/2.20.4 se debe hacer un Pull Request con base Master
* Si todo esta tal cual se subio a la rama Develop no hay necesidad de pedir un **Review de los cambios**, pero si se hacen ajustes en la rama **Release** se debe pedir Review nuevamente.
* Una vez mezclado con Master y develop se debe eliminar las ramas con nomenclatura backport

### Publicación

* Finalmente se debe anunciar la nueva característica en una nota de workplace ([Un ejemplo de publicación](https://meli.workplace.com/notes/161486316270466/)) y esa publicación notificarla en [Help Mantra](https://meli.slack.com/archives/C016GDSQAHG) en el caso que sea una caracteristica nueva. 

### Roadmap

Breve o especie de hoja de ruta 
* Mantra v2.0 [Presentación]([https://docs.google.com/presentation/d/1R87rG1bxliJW1nlM4XRMxSdf90mg3qKMeaLDpMTxcr0/edit#slide=id.g71959900f1_0_159).

### Changelog

Mantenemos los cambios en nuestro código base [aquí](CHANGELOG.md)

***
**©Copyright - Equipo SRE - Shipping Tech**
