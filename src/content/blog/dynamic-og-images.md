---
author: Sat Naing
pubDatetime: 2022-12-28T04:59:04.866Z
title: Generación dinámica de imágenes OG en las entradas de blog de AstroPaper
slug: dynamic-og-image-generation-in-astropaper-blog-posts
featured: false
draft: false
tags:
  - docs
  - release
description: Nueva función en AstroPaper v1.4.0, que introduce la generación dinámica de imágenes OG para las entradas del blog.
---

Nueva función en AstroPaper v1.4.0, que introduce la generación dinámica de imágenes OG para las entradas del blog.


## Índice

## Introducción

Las imágenes OG (también conocidas como imágenes sociales) desempeñan un papel importante en la participación en las redes sociales. En caso de que no sepas lo que significa imagen OG, es una imagen que se muestra cada vez que compartimos la URL de nuestro sitio web en medios sociales como Facebook, Discord, etc.

> La Imagen Social utilizada para Twitter técnicamente no se llama imagen OG. Sin embargo, en este post, voy a utilizar el término imagen OG para todos los tipos de Imágenes Sociales.


## Default/Static OG image (la vieja forma)

AstroPaper ya proporciona una forma de añadir una imagen OG a una entrada de blog. El autor puede especificar la imagen OG en el frontmatter `ogImage`. Incluso cuando el autor no define la imagen OG en el frontmatter, la imagen OG por defecto se utilizará como un fallback (en este caso `public/astropaper-og.jpg`). Pero el problema es que la imagen OG por defecto es estática, lo que significa que cada entrada del blog que no incluya una imagen OG en el frontmatter utilizará siempre la misma imagen OG por defecto a pesar de que el título/contenido de cada entrada sea diferente de los demás.

## Imagen OG dinámica

Generar una imagen OG dinámica para cada entrada permite al autor evitar especificar una imagen OG para cada entrada del blog. Además, esto evitará que la imagen OG fallback sea idéntica para todas las entradas del blog.

En AstroPaper v1.4.0, se utiliza el paquete [Satori](https://github.com/vercel/satori) de Vercel para la generación de imágenes OG dinámicas.


Las imágenes OG dinámicas se generarán en tiempo de compilación para las entradas de blog que


- no incluyan una imagen OG en el frontmatter
- no estén marcados como borrador.



## Anatomía de la imagen OG dinámica de AstroPaper

La imagen OG dinámica de AstroPaper incluye _the blog post title_, _author name_ y _site title_. El nombre del autor y el título del sitio se obtendrán a través de `SITE.author` y `SITE.title` del archivo **"src/config.ts "**. El título se genera a partir del `title` de la entrada del blog.  
![Example Dynamic OG Image link](https://user-images.githubusercontent.com/53733092/209704501-e9c2236a-3f4d-4c67-bab3-025aebd63382.png)



## Limitaciones

En el momento de escribir esto, [Satori](https://github.com/vercel/satori) es bastante nuevo y aún no ha alcanzado la versión principal. Por lo tanto, todavía hay algunas limitaciones a esta característica dinámica de imagen OG.


- Si tienes entradas de blog con títulos que no están en inglés, tienes que configurar la opción `embedFonts` a `false` (archivo: `src/utils/generateOgImage.tsx`). Incluso después de esto, la imagen OG podría no mostrarse muy bien.
- Además, los idiomas RTL aún no están soportados.
-[Usar emoji](https://github.com/vercel/satori#emojis) en el título puede ser un poco complicado.
