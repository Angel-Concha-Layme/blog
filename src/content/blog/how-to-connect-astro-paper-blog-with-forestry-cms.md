---
title: Cómo conectar el blog AstroPaper con el CMS Forestry
author: Sat Naing
pubDatetime: 2022-09-21T05:17:19Z
slug: how-to-connect-astro-paper-blog-with-forestry-cms
featured: false
draft: false
tags:
  - docs
  - forestry-cms
  - astro-paper
ogImage: https://res.cloudinary.com/noezectz/v1663745737/astro-paper/astropaper-x-forestry-og_kqfwp0.png
description:
  Proceso paso a paso para conectar el tema de blog Astro-Paper con Forestry Headless CMS.
---


> ¡¡¡Importante!!! La silvicultura dejará de funcionar el 22 de abril de 2023. Puedes [leer su anuncio](https://forestry.io/blog/forestry.io-end-of-life/) para más información.

En este artículo, voy a explicar paso a paso el proceso de conectar el tema AstroPaper con el CMS headless Forestry. Así que, vamos a empezar 🎉


## Tabla de contenidos

## ¿Qué es Forestry?

[Forestry](https://forestry.io/ "Forestry Website") es un CMS headless basado en git y podemos gestionar nuestros contenidos markdown fácilmente usándolo. Aunque no es un CMS de código abierto, tiene un buen plan gratuito por el cual podemos importar hasta 3 sitios (3 repositorios). En este artículo, voy a demostrar cómo podemos utilizar Forestry como CMS basado en git de nuestro tema de blog AstroPaper.


## Iniciar sesión / Registrar una cuenta en Forestry.io

En primer lugar, tienes que crear una cuenta en [Forestry website](https://app.forestry.io/login "Forestry Login Page"). Yo suelo registrarme con mi cuenta de Github.

![Página de inicio de sesión de Forestry](https://res.cloudinary.com/noezectz/v1663739096/astro-paper/Forestry-io_hk5yzv.png)

## Importar el sitio AstroPaper (repositorio)


Esta parte es importar el repositorio a Forestry y un poco de proceso de configuración.

### Añadir sitio

Después de iniciar sesión/registrar una cuenta, importe su sitio AstroPaper haciendo clic en el botón "Añadir sitio".

[Página 'Mis sitios' de Forestry](https://res.cloudinary.com/noezectz/v1663739752/astro-paper/Forestry-io_1_z1bdyd.png)

### Seleccionar SSG

En este caso, simplemente seleccione "Otros

![Seleccionar 'Otros' como generador de sitios](https://res.cloudinary.com/noezectz/v1663740872/astro-paper/Forestry-io_2_blrrw2.png)


### Select Git Provider

Mi proveedor de git es Github y supongo que el tuyo es el mismo. Así que elige "Github".

![Seleccionar Github como proveedor de git](https://res.cloudinary.com/noezectz/v1663740922/astro-paper/Forestry-io_3_pj1v8v.png)



Después de esto, se realiza el proceso de importación del sitio (repo).


## ## Configurar la barra lateral (sidebar)

La siguiente fase después de importar el sitio es configurar el menú lateral. Puedes agregar tantos menús laterales como quieras. Sin embargo, solo agregaré un menú lateral en este caso.

Navega a "Finalizar proceso de configuración" > "Configurar menú lateral" y haz clic en "Configurar menú lateral"

![Pantalla de bienvenida de Forestry](https://res.cloudinary.com/noezectz/v1663740974/astro-paper/forestry-io_4_j35uk9.png)

Luego, haz clic en el botón "Agregar sección".

![Haciendo clic en 'Agregar sección' para el menú lateral](https://res.cloudinary.com/noezectz/v1663741011/astro-paper/forestry-io_5_sxtgvx.png)

Después de eso, elige DIRECTORIO para el Tipo de Sección.

![Eligiendo 'DIRECTORIO' como el Tipo de Selección](https://res.cloudinary.com/noezectz/v1663741052/astro-paper/forestry-io_6_lddmkx.png)

Luego, configura la sección del directorio. Puedes seguir mi configuración.

![Configurando la Sección del Directorio](https://res.cloudinary.com/noezectz/v1663741105/astro-paper/forestry-io_7_jkwgi1.png)

Después de este paso, deberías ver un menú lateral "Publicaciones del Blog" y algunas publicaciones del blog.

## Configuración de Importación de Medios

En Forestry CMS, puedes configurar diferentes opciones para los medios (también conocidos como activos) tales como Cloudinary, commit de medios en git, etc. Usualmente almaceno mis activos en [Cloudinary](https://cloudinary.com/). Para configurar la importación de medios, ve a Configuración > Medios. Luego selecciona tu proveedor de almacenamiento de imágenes. (Yo elegí Cloudinary).

![Configurando 'Cloudinary' como la importación de medios](https://res.cloudinary.com/noezectz/v1663741636/astro-paper/forestry-io-media-import_1_f8i4lm.png)

Puedes ver los detalles de la configuración de Cloudinary en Forestry en [documentación de Forestry](https://forestry.io/docs/media/cloudinary/).

## Configuración de la Plantilla de Front Matter

Después de configurar todo, puedes configurar la plantilla de front matter para tus futuras publicaciones en el blog. Para configurar la plantilla de front matter, navega al menú "Front Matter" en la barra lateral.

Luego, haz clic en el botón "Agregar Plantilla" en la esquina superior derecha.

![Página de Plantillas de Front Matter](https://res.cloudinary.com/noezectz/v1663742060/astro-paper/forestry-io-frontmatter_yskfvn.png)

Selecciona una nueva plantilla basada en un documento existente.

![Creando una nueva plantilla basada en un documento existente](https://res.cloudinary.com/noezectz/v1663742179/astro-paper/forestry-io-existing-doc_bwcb9q.png)

Luego, añade el nombre de la plantilla y elige una de mis páginas de documento como plantilla.

Como configuración final, realiza algunos ajustes en los ajustes del campo de front matter.

![Realizando algunos ajustes en la configuración de un campo de front matter](https://res.cloudinary.com/noezectz/v1663742450/astro-paper/forestry-io-fm-config_jqmgwz.png)

Aquí hay algunos ajustes que tienes que hacer.

**_title_**

- Validación => REQUERIDO => true

**_author_**

- Predeterminado => tu nombre

**_datetime_**

- Predeterminado => USAR "AHORA" COMO PREDETERMINADO

**_description_**

- Validación => REQUERIDO => true

## Conclusión

Ahora puedes publicar tus artículos y escribir lo que desees.


