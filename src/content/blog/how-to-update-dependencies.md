---
title: Cómo actualizar las dependencias de AstroPaper
author: Sat Naing
pubDatetime: 2023-07-20T15:33:05.569Z
slug: how-to-update-dependencies
featured: false
draft: false
ogImage: /assets/forrest-gump-quote.webp
tags:
  - FAQ
description: Cómo actualizar las dependencias del proyecto y la plantilla AstroPaper.
---

Actualizar las dependencias de un proyecto puede ser tedioso. Sin embargo, descuidar la actualización de las dependencias de un proyecto tampoco es una buena idea 😬. En este post, compartiré cómo suelo actualizar mis proyectos, centrándome en AstroPaper como ejemplo. No obstante, estos pasos pueden aplicarse también a otros proyectos js/node.


![Forrest Gump Fake Quote](/assets/forrest-gump-quote.webp)

## Tabla de contenidos

## Actualización de las dependencias del proyecto

Hay varias formas de actualizar las dependencias, y he probado varios métodos para encontrar el camino más fácil. Una forma de hacerlo es actualizar manualmente cada paquete usando `npm install package-name@latest`. Este método es la forma más sencilla de actualizar. Sin embargo, puede que no sea la opción más eficiente.

Mi forma recomendada de actualizar las dependencias es utilizando el paquete [npm-check-updates](https://www.npmjs.com/package/npm-check-updates). Hay un buen [artículo](https://www.freecodecamp.org/news/how-to-update-npm-dependencies/) de freeCodeCamp sobre eso, así que no voy a explicar los detalles de lo que es y cómo usar ese paquete. En su lugar, te mostraré mi enfoque típico.


Primero, instala el paquete `npm-check-updates` globalmente.


```bash
npm install -g npm-check-updates
```

Después de instalar el paquete, ejecuta el siguiente comando para actualizar todas las dependencias a la última versión.

```bash
ncu
```
La mayoría de las veces, las dependencias de los parches pueden actualizarse sin afectar en absoluto al proyecto. Por lo tanto, suelo actualizar las dependencias de los parches ejecutando `ncu -i --target patch` o `ncu -u --target patch`. La diferencia es que `ncu -u --target patch` actualizará todos los parches, mientras que `ncu -i --target patch` dará la opción de elegir qué paquete actualizar. Tú decides qué enfoque adoptar.

La siguiente parte consiste en actualizar las dependencias menores. Las actualizaciones de paquetes menores no suelen romper el proyecto, pero siempre es bueno comprobar las notas de la versión de los respectivos paquetes. Estas actualizaciones menores a menudo incluyen algunas características interesantes que se pueden aplicar a nuestros proyectos.


```bash
ncu -i --target minor
```


Por último, pero no menos importante, es posible que haya algunas actualizaciones importantes de paquetes en las dependencias. Por lo tanto, compruebe el resto de las actualizaciones de dependencias ejecutando

```bash
ncu -i
```

Si hay alguna actualización mayor (o algunas actualizaciones que aún tenga que hacer), el comando anterior mostrará los paquetes restantes. Si el paquete es una actualización de versión mayor, tiene que tener mucho cuidado ya que esto probablemente romperá todo el proyecto. Por lo tanto, por favor, lea la nota de lanzamiento respectiva (o) docs muy cuidadosamente y haga los cambios en consecuencia.

Si ejecuta `ncu -i` y no encuentra más paquetes que actualizar, _**Congrats!!!**_ ha actualizado con éxito todas las dependencias de su proyecto.


## Actualización de AstroPaper

Al igual que otros proyectos de código abierto, AstroPaper está evolucionando con correcciones de errores, actualizaciones de características, y así sucesivamente. Así que si eres alguien que utiliza AstroPaper como plantilla, es posible que también quieras actualizar la plantilla cuando haya una nueva versión.

El caso es que puede que ya hayas actualizado la plantilla según tu gusto. Por lo tanto, no puedo mostrar exactamente **"la manera perfecta para todos (the one-size-fits-all perfect way) "** de actualizar la plantilla a la versión más reciente. Sin embargo, aquí hay algunos consejos para actualizar la plantilla sin romper su repo. Tenga en cuenta que, la mayoría de las veces, la actualización de las dependencias del paquete puede ser suficiente para usted.




### Archivos y directorios a tener en cuenta

En la mayoría de los casos, los archivos y directorios que es posible que no desee anular (ya que es probable que haya actualizado esos archivos) son `src/content/blog/`, `src/config.ts`, `src/pages/about.md`, y otros activos y estilos como `public/` y `src/styles/base.css`.

Si eres alguien que sólo actualiza lo mínimo de la plantilla, no debería haber problema en sustituir todo por la última AstroPaper excepto los archivos y directorios mencionados. Es como el sistema operativo Android puro y otros sistemas operativos específicos de proveedores como OneUI. Cuanto menos modifiques la base, menos tendrás que actualizar.

Puedes reemplazar manualmente cada archivo uno por uno, o puedes utilizar la magia de git para actualizar todo. No te voy a mostrar el proceso de sustitución manual, ya que es muy sencillo. Si no te interesa ese método tan directo e ineficiente, ten paciencia conmigo 🐻.

### Actualización de AstroPaper usando Git

**¡¡IMPORTANTE!!!**

> Sólo haz lo siguiente si sabes cómo resolver conflictos de fusión. Si no, mejor reemplaza los archivos manualmente o actualiza sólo las dependencias.

En primer lugar, añade astro-paper como mando a distancia en tu proyecto.

```bash
git remote add astro-paper https://github.com/satnaing/astro-paper.git
```

Haz checkout a una nueva rama para actualizar la plantilla. Si sabes lo que estás haciendo y estás seguro de tu habilidad con git, puedes omitir este paso.

```bash
git checkout -b build/update-astro-paper
```

A continuación, extraiga los cambios de astro-paper ejecutando

```bash
git pull astro-paper main
```

Si te encuentras con el error `fatal: refusing to merge unrelated histories`, puedes resolverlo ejecutando el siguiente comando

```bash
git pull astro-paper main --allow-unrelated-histories
```

Tras ejecutar el comando anterior, es probable que encuentres conflictos en tu proyecto. Tendrás que resolver estos conflictos manualmente y hacer los ajustes necesarios según tus necesidades.

Después de resolver los conflictos, prueba tu blog a fondo para asegurarte de que todo funciona como se espera. Comprueba tus artículos, componentes y cualquier personalización que hayas realizado.

Una vez que estés satisfecho con el resultado, es hora de fusionar la rama de actualización con tu rama principal (sólo si estás actualizando la plantilla en otra rama). ¡Enhorabuena! Has actualizado con éxito tu plantilla a la última versión. ¡Tu blog ya está actualizado y listo para brillar! 🎉

## Conclusión

En este artículo he compartido algunas de mis ideas y procesos para actualizar las dependencias y la plantilla AstroPaper. Espero sinceramente que este artículo te resulte valioso y te ayude a gestionar tus proyectos de forma más eficiente.

Si tienes algún enfoque alternativo o mejorado para actualizar las dependencias/AstroPaper, me encantaría que me lo comunicaras. No dudes en iniciar un debate en el repositorio, enviarme un correo electrónico o abrir una incidencia. Tus aportaciones e ideas son muy apreciadas.

Por favor, comprenda que mi agenda está bastante ocupada estos días, y puede que no sea capaz de responder rápidamente. Sin embargo, prometo responderte lo antes posible. 😬

Gracias por tomarte el tiempo de leer este artículo, ¡y te deseo lo mejor con tus proyectos!
