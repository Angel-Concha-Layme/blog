---
autor: Sat Naing
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-12-21T09:12:47.400Z
title: Añadiendo nuevas publicaciones
slug: adding-new-posts-in-astropaper-theme
destacado: true
borrador: false
etiquetas:
  - docs
description: Algunas reglas y recomendaciones para crear o añadir nuevas publicaciones usando el tema AstroPaper.
---

Aquí hay algunas reglas/recomendaciones, consejos y trucos para crear nuevas publicaciones en el tema de blog AstroPaper.

## Tabla de contenidos

## Frontmatter

Frontmatter es el lugar principal para almacenar información importante sobre la publicación del blog (artículo). Frontmatter se encuentra en la parte superior del artículo y está escrito en formato YAML. Lee más sobre frontmatter y su uso en [documentación de astro](https://docs.astro.build/en/guides/markdown-content/).

Aquí está la lista de propiedades de frontmatter para cada publicación.

| Propiedad          | Descripción                                                                                                                 | Observación                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| **_title_**        | Título de la publicación. (h1)                                                                                              | requerido<sup>\*</sup>                            |
| **_description_**  | Descripción de la publicación. Se utiliza en el extracto de la publicación y en la descripción del sitio de la misma.       | requerido<sup>\*</sup>                            |
| **_pubDatetime_**  | Fecha y hora de publicación en formato ISO 8601.                                                                            | requerido<sup>\*</sup>                            |
| **_modDatetime_**  | Fecha y hora de modificación en formato ISO 8601. (solo añadir esta propiedad cuando se modifique una publicación del blog) | opcional                                          |
| **_author_**       | Autor de la publicación.                                                                                                    | por defecto = SITE.author                         |
| **_slug_**         | Slug para la publicación. Este campo es opcional, pero no puede estar vacío. (slug: ""❌)                                   | por defecto = nombre del archivo slugificado      |
| **_featured_**     | Indica si mostrar o no esta publicación en la sección destacada de la página principal.                                     | por defecto = falso                               |
| **_draft_**        | Marca esta publicación como 'no publicada'.                                                                                 | por defecto = falso                               |
| **_tags_**         | Palabras clave relacionadas con esta publicación. Escritas en formato de array yaml.                                        | por defecto = otros                               |
| **_ogImage_**      | Imagen OG de la publicación. Útil para compartir en redes sociales y SEO.                                                   | por defecto = SITE.ogImage o imagen OG generada   |
| **_canonicalURL_** | URL canónica (absoluta), en caso de que el artículo ya exista en otra fuente.                                               | por defecto = `Astro.site` + `Astro.url.pathname` |

> ¡Consejo! Puedes obtener la fecha y hora en formato ISO 8601 ejecutando `new Date().toISOString()` en la consola. Asegúrate de quitar las comillas.

Solo los campos `title`, `description` y `pubDatetime` en el frontmatter deben especificarse.

El título y la descripción (extracto) son importantes para la optimización de motores de búsqueda (SEO) y, por lo tanto, AstroPaper recomienda incluirlos en las publicaciones del blog.

`slug` es el identificador único de la URL. Por lo tanto, `slug` debe ser único y diferente de otras publicaciones. Los espacios en blanco de `slug` deben separarse con `-` o `_`, pero se recomienda `-`. El slug se genera automáticamente utilizando el nombre del archivo de la publicación del blog. Sin embargo, puedes definir tu `slug` como un frontmatter en tu publicación del blog.

Por ejemplo, si el nombre del archivo del blog es `adding-new-post.md` y no especificas el slug en tu frontmatter, Astro creará automáticamente un slug para la publicación del blog utilizando el nombre del archivo. Por lo tanto, el slug será `adding-new-post`. Pero si especificas el `slug` en el frontmatter, esto anulará el slug predeterminado. Puedes leer más sobre esto en [Documentación de Astro](https://docs.astro.build/en/guides/content-collections/#defining-custom-slugs).

Si omites `tags` en una publicación del blog (en otras palabras, si no se especifica ninguna etiqueta), la etiqueta predeterminada `others` se utilizará como etiqueta para esa publicación. Puedes establecer la etiqueta predeterminada en el archivo `/src/content/config.ts`.

```ts
// src/content/config.ts
export const blogSchema = z.object({
  // ---
  draft: z.boolean().optional(),
  tags: z.array(z.string()).default(["others"]), // reemplaza "others" por lo que desees
  // ---
});
```

### Ejemplo de Frontmatter

Aquí está el frontmatter de ejemplo para una publicación.

```yaml
# src/content/blog/sample-post.md
---
title: El título de la publicación
author: tu nombre
pubDatetime: 2022-09-21T05:17:19Z
slug: el-titulo-de-la-publicacion
featured: true
draft: false
tags:
  - algun
  - ejemplo
  - etiquetas
ogImage: ""
description: Esta es la descripción de ejemplo de la publicación de ejemplo.
canonicalURL: https://example.org/my-article-was-already-posted-here
---
```

## Añadir tabla de contenidos

Por defecto, una publicación (artículo) no incluye ninguna tabla de contenidos (toc). Para incluir toc, debes especificarlo de una manera específica.

Escribe `Tabla de contenidos` en formato h2 (## en markdown) y colócalo donde quieras que aparezca en la publicación.

Por ejemplo, si quieres colocar tu tabla de contenidos justo debajo del párrafo introductorio (como suelo hacer), puedes hacerlo de la siguiente manera.

```md
---
# algún frontmatter
---

Aquí hay algunas recomendaciones, consejos y trucos para crear nuevas publicaciones en el tema de blog AstroPaper.

## Tabla de contenidos

<!-- el resto de la publicación -->
```

## Encabezados

Hay algo que debes tener en cuenta acerca de los encabezados. Las publicaciones de blog de AstroPaper utilizan el título (title en el frontmatter) como el encabezado principal de la publicación. Por lo tanto, el resto de los encabezados en la publicación deben usar h2 ~ h6.

Esta regla no es obligatoria, pero se recomienda encarecidamente por motivos visuales, de accesibilidad y SEO.

## Almacenar imágenes para contenido de blo

Aquí hay dos métodos para almacenar imágenes y mostrarlas dentro de un archivo markdown.

> ¡Nota! Si es un requisito estilizar imágenes optimizadas en markdown deberías[usar MDX](https://docs.astro.build/en/guides/images/#images-in-mdx-files).

### Dentro del directorio `src/assets/` (recomendado)

Puedes almacenar imágenes dentro del directorio `src/assets/.` Estas imágenes serán automáticamente optimizadas por Astro a través de [API de Servicio de Imagen](https://docs.astro.build/en/reference/image-service-reference/).

Puedes usar la ruta relativa o la ruta alias (`@assets/`) para servir estas imágenes.

Ejemplo: Supongamos que deseas mostrar `example.jpg` cuya ruta es `/src/assets/images/example.jpg`.

```md
![algo](@assets/images/example.jpg)

<!-- O -->

![algo](../../assets/images/example.jpg)

<!-- Usar etiqueta img o componente Image no funcionará ❌ -->
<img src="@assets/images/example.jpg" alt="algo">
<!-- ^^ Esto es incorrecto -->
```

> Técnicamente, puedes almacenar imágenes dentro de cualquier directorio bajo `src`. Aquí, `src/assets` es solo una recomendación.

### Dentro del directorio `public`

Puedes almacenar imágenes dentro del directorio `public`. Ten en cuenta que las imágenes almacenadas en el directorio `public` permanecen sin tocar por Astro, lo que significa que no estarán optimizadas y necesitarás manejar la optimización de imágenes por ti mismo.

Para estas imágenes, debes usar una ruta absoluta; y estas imágenes pueden mostrarse utilizando [anotación de markdown](https://www.markdownguide.org/basic-syntax/#images-1) o [etiqueta HTML img](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img).

Ejemplo: Supongamos que `example.jpg` está ubicada en `/public/assets/images/example.jpg`.

```md
![algo](/assets/images/example.jpg)

<!-- O -->

<img src="/assets/images/example.jpg" alt="algo">
```

## Bonus

### Compresión de imágenes

Cuando incluyas imágenes en la publicación del blog (especialmente para imágenes bajo el directorio `public`), se recomienda que la imagen esté comprimida. Esto afectará el rendimiento general del sitio web.

Mis recomendaciones para sitios de compresión de imágenes:

- [TinyPng](https://tinypng.com/)
- [TinyJPG](https://tinyjpg.com/)

### Imagen OG

La imagen OG predeterminada se colocará si una publicación no especifica la imagen OG. Aunque no es obligatorio, se debe especificar en el frontmatter una imagen OG relacionada con la publicación. El tamaño recomendado para la imagen OG es **_1200 X 640_** px.

> Desde AstroPaper v1.4.0, las imágenes OG se generarán automáticamente si no se especifican. Consulta [el anuncio](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/).
