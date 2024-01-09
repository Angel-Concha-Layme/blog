---
author: Sat Naing
pubDatetime: 2022-09-23T04:58:53Z
title: Cómo configurar el tema de AstroPaper
slug: how-to-configure-astropaper-theme
featured: true
draft: false
tags:
  - configuration
  - docs
description: Cómo puedes hacer que el tema AstroPaper sea absolutamente tuyo.
---

AstroPaper es un tema de blog Astro altamente personalizable. Con AstroPaper, puede personalizar todo de acuerdo a su gusto personal. Este artículo explicará cómo puedes hacer algunas personalizaciones fácilmente en el archivo de configuración.

## Tabla de contenidos

## Configurando SITE

Las configuraciones importantes se encuentran en el archivo `src/config.ts`. Dentro de ese archivo, verás el objeto `SITE` donde puedes especificar las principales configuraciones de tu sitio web.

Durante el desarrollo, está bien dejar `SITE.website` vacío. Pero en el modo de producción, debe especificar su url desplegado en `SITE.website` opción ya que esto se utilizará para la URL canónica, URL tarjeta social, etc., que son importantes para SEO.

```js
// file: src/config.ts
export const SITE = {
  website: "https://astro-paper.pages.dev/",
  author: "Sat Naing",
  desc: "Un tema para blog Astro minimalista, responsivo y SEO-friendly.",
  title: "AstroPaper",
  ogImage: "astropaper-og.jpg",
  lightAndDarkMode: true,
  postPerPage: 3,
};
```



| Options            | Description                                                                                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `website`          | Tu URL del sitio web desplegado
url                                                                                                                                    |
| `author`           | Tu nombre                                                                                                                                                |
| `desc`             | Descripción de tu sitio. Útil para SEO y compartir en redes sociales.                                                                                      |
| `title`            | Nombre de tu sitio                                                                                                                                       |
| `ogImage`          | Tu imagen OG predeterminada para el sitio. Útil para compartir en redes sociales. Las imágenes OG pueden ser una URL de imagen externa o pueden colocarse bajo el directorio /public.|
| `lightAndDarkMode` | Habilitar o deshabilitar el `modo claro y oscuro` para el sitio web. Si se deshabilita, se usará el esquema de color primario. Esta opción está habilitada por defecto.    |
| `postPerPage`      | Puedes especificar cuántas publicaciones se mostrarán en cada página de publicaciones. (ej: si configuras SITE.postsPerPage a 3, cada página mostrará solo 3 publicaciones por página)      |






## Configurar la configuración regional

Puede configurar la configuración regional por defecto utilizada para la construcción (por ejemplo, el formato de fecha en la página de entrada), y para la representación en los navegadores (por ejemplo, el formato de fecha en la página de búsqueda)

```js
// file: src/config.ts
export const LOCALE = {
  lang: "en", // código html lang. Establecer este vacío y por defecto será "en"
  langTag: ["en-EN"], // BCP 47 Etiquetas de idioma. Establecer este vacío [] para utilizar el entorno por defecto
} as const;
```

Se utilizará `LOCALE.lang` como código de idioma HTML ISO en `<html lang="en">`. Si no lo especifica, se utilizará `en` por defecto.
`LOCALE.langTag` se utiliza como [datetime locale](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString#locales). Para ello, puede especificar una matriz de configuraciones regionales para los idiomas alternativos. Deje `LOCALE.langTag` vacío `[]` para usar el entorno por defecto en _build-_ y _run-time_.



## Configurar logo o título

Puede especificar el título del sitio o la imagen del logo en el archivo `src/config.ts`.

![Una flecha apuntando al logo del sitio web](https://res.cloudinary.com/noezectz/v1663911318/astro-paper/AstroPaper-logo-config_goff5l.png)


```js
// file: src/config.ts
export const LOGO_IMAGE = {
  enable: false,
  svg: true,
  width: 216,
  height: 46,
};
```

Si especifica `LOGO_IMAGE.enable` => `false`, AstroPaper convertirá automáticamente `SITE.title` en el logo de texto principal del sitio.

Si especifica `LOGO_IMAGE.enable` => `true`, AstroPaper usará la imagen del logo como logo principal del sitio.

Debe especificar `logo.png` o `logo.svg` en el directorio `/public/assets`. Actualmente, sólo se admiten los formatos de archivo de imagen svg y png. (**_¡Importante!_** _el nombre del logo debe ser logo.png o logo.svg)_)

Si la imagen de su logotipo tiene formato png, debe configurar `LOGO_IMAGE.svg` => `false`.

Se recomienda especificar la anchura y la altura de la imagen del logotipo. Puede hacerlo estableciendo `LOGO_IMAGE.width` _y_ `LOGO_IMAGE.height`.



## Configuración de enlaces sociales

Puedes configurar tus propios enlaces sociales junto con sus iconos.


![Una flecha señalando los iconos de los enlaces sociales](https://res.cloudinary.com/noezectz/v1663914759/astro-paper/astro-paper-socials_tkcjgq.png)

Actualmente se soportan 20 iconos sociales. (Github, LinkedIn, Facebook etc.)


Puede especificar y habilitar determinados enlaces sociales en la sección hero y en el pie de página. Para ello, vaya a `/src/config.ts` y entonces usted encontrará `SOCIALS` matriz de objetos.



```js
// file: src/config.ts
export const SOCIALS: SocialObjects = [
  {
    name: "Github",
    href: "https://github.com/satnaing/astro-paper",
    linkTitle: ` ${SITE.title} on Github`,
    active: true,
  },
  {
    name: "Facebook",
    href: "https://github.com/satnaing/astro-paper",
    linkTitle: `${SITE.title} on Facebook`,
    active: true,
  },
  {
    name: "Instagram",
    href: "https://github.com/satnaing/astro-paper",
    linkTitle: `${SITE.title} on Instagram`,
    active: true,
  },
  ...
]
```

Usted tiene que establecer enlace social específico a `active: true` con el fin de mostrar sus enlaces sociales en el héroe y la sección de pie de página. A continuación, también tiene que especificar su enlace social en `href` propiedad.

Por ejemplo, si quiero hacer aparecer mi Github, lo haré así.

```js
export const SOCIALS: SocialObjects = [
  {
    name: "Github",
    href: "https://github.com/satnaing", // actualizar enlace de cuenta
    linkTitle: `${SITE.title} on Github`, // este texto aparecerá al pasar el ratón por encima y VoiceOver
    active: true, // asegúrese de establecer activo a true
  }
  ...
]
```

Otra cosa a tener en cuenta es que se puede especificar el `linkTitle` en el objeto. Este texto se mostrará al pasar el ratón sobre el enlace del icono social. Además, esto mejorará la accesibilidad y el SEO. AstroPaper proporciona valores predeterminados para el título del enlace, pero puedes sustituirlos por tus propios textos.

Por ejemplo,

```js
linkTitle: `${SITE.title} on Twitter`,
```

a 

```js
linkTitle: `Follow ${SITE.title} on Twitter`;
```

## Conclusión

Esta es la breve especificación de cómo se puede personalizar este tema. Usted puede personalizar más si usted sabe algo de codificación. Para personalizar los estilos, por favor lea [este artículo](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/). Gracias por leer.✌🏻