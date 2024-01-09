---
author: Sat Naing
pubDatetime: 2022-09-25T15:20:35Z
title: Personalización de los esquemas de color del tema AstroPaper
featured: false
draft: false
tags:
  - color-schemes
  - docs
description: Cómo puedes habilitar/deshabilitar el modo claro y oscuro; y personalice los esquemas de color.
---

Esta publicación explicará cómo puedes activar o desactivar el modo claro y oscuro para el sitio web. Además, aprenderás cómo puedes personalizar los esquemas de colores de todo el sitio web.

## Tabla de contenidos

## Activar/desactivar el modo claro y oscuro

El tema AstroPaper incluirá por defecto el modo claro y oscuro. En otras palabras, habrá dos esquemas de colores: uno para el modo claro y otro para el modo oscuro. Este comportamiento predeterminado se puede desactivar en el objeto de configuración del SITIO del archivo `src/config.ts`.

```js
// archivo: src/config.ts
export const SITE = {
  website: "https://astro-paper.pages.dev/",
  author: "Sat Naing",
  desc: "Un tema de blog Astro minimalista, adaptable y amigable con SEO.",
  title: "AstroPaper",
  ogImage: "astropaper-og.jpg",
  lightAndDarkMode: true, // verdadero por defecto
  postPerPage: 3,
};
```

Para desactivar el `light & dark mode` establece `SITE.lightAndDarkMode` en `false`.

## Elegir esquema de color primario

Por defecto, si desactivamos `SITE.lightAndDarkMode`, solo obtendremos el esquema de colores preferido por el sistema.

Por lo tanto, para elegir un esquema de color primario en lugar del esquema de colores preferido por el sistema, debemos establecer el esquema de colores en la variable primaryColorScheme dentro de `public/toggle-theme.js`.

```js
/* archivo: public/toggle-theme.js */
const primaryColorScheme = ""; // establecer "light" o "dark" aquí

// Obtener los datos del tema del almacenamiento local
const currentTheme = localStorage.getItem("theme");

// otros códigos etc...
```

La variable **primaryColorScheme** puede contener dos valores: `light`, `dark`. Puedes dejar la cadena vacía (predeterminado) si no quieres especificar el esquema de color primario.

- `""` - el sistema prefiere el esquema de color. (predeterminado)
- `"light"` - utiliza el modo claro como esquema de color primario.
- `"dark"` - utiliza el modo oscuro como esquema de color primario.

<details><summary>¿Por qué 'primaryColorScheme' no está dentro de config.ts?</summary>

> Para evitar el parpadeo de colores al recargar la página, tenemos que colocar los códigos de JavaScript del interruptor de cambio tan pronto como sea posible cuando la página se carga. Esto soluciona el problema del parpadeo, pero como compensación, ya no podemos usar importaciones de ESM.

[Click here](https://docs.astro.build/en/reference/directives-reference/#isinline) Para saber más sobre el script `is:inline` de Astro.

</details>

## Personalizar esquemas de colores

Ambos esquemas de colores, claro y oscuro, del tema AstroPaper pueden personalizarse. Puedes hacer esto en el archivo `src/styles/base.css`.

```css
/* file: src/styles/base.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root,
  html[data-theme="light"] {
    --color-fill: 251, 254, 251;
    --color-text-base: 40, 39, 40;
    --color-accent: 0, 108, 172;
    --color-card: 230, 230, 230;
    --color-card-muted: 205, 205, 205;
    --color-border: 236, 233, 233;
  }
  html[data-theme="dark"] {
    --color-fill: 47, 55, 65;
    --color-text-base: 230, 230, 230;
    --color-accent: 26, 217, 217;
    --color-card: 63, 75, 90;
    --color-card-muted: 89, 107, 129;
    --color-border: 59, 70, 85;
  }
  /* other styles */
}
```

En el tema AstroPaper, se utilizan los selectores `:root` y `html[data-theme="light"]` como el esquema de color claro y `html[data-theme="dark"]` se utiliza el esquema de color oscuro. Si quieres personalizar tu esquema de color personalizado, debes especificar tu esquema de color claro dentro de `:root`,`html[data-theme="light"]` y el esquema de color oscuro dentro de `html[data-theme="dark"]`.

Los colores se declaran en la notación de propiedad personalizada CSS (variable CSS). Los valores de las propiedades de color se escriben en valores rgb. (Nota: en lugar de `rgb(40, 39, 40)`, solo especifica `40, 39, 40`)

Aquí está la explicación detallada de las propiedades de color.

| Propiedad de color   | Definición y Uso                                                                                 |
| -------------------- | ------------------------------------------------------------------------------------------------ |
| `--color-fill`       | Color principal del sitio web. Generalmente el fondo principal.                                  |
| `--color-text-base`  | Color secundario del sitio web. Generalmente el color del texto.                                 |
|                      |
| `--color-accent`     | Color de acento del sitio web. (link color, hover color, etc.)                                   |
|                      |
| `--color-card`       | Card, scrollbar and code background color (like `this`).                                         |
| `--color-card-muted` | Color de fondo de la tarjeta y la barra de desplazamiento para el estado de desplazamiento, etc. |
| `--color-border`     | Color del borde. Especialmente utilizado en fila horizontal (hr)                                 |



A continuación se muestra un ejemplo de cambio del esquema de color claro.




```css
@layer base {
  /* lobster color scheme */
  :root,
  html[data-theme="light"] {
    --color-fill: 246, 238, 225;
    --color-text-base: 1, 44, 86;
    --color-accent: 225, 74, 57;
    --color-card: 220, 152, 145;
    --color-card-muted: 233, 119, 106;
    --color-border: 220, 152, 145;
  }
}
```

> Consulta algunos [esquemas de color predefinidos](https://astro-paper.pages.dev/posts/predefined-color-schemes/) que AstroPaper ya ha creado para ti.

