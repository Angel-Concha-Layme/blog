---
title: Cómo añadir un tiempo estimado de lectura en AstroPaper
author: Sat Naing
pubDatetime: 2023-07-21T10:11:06.130Z
modDatetime: 2023-12-26T08:39:25.181Z
slug: how-to-add-estimated-reading-time
featured: false
draft: false
tags:
  - FAQ
description: Cómo puedes añadir un 'Tiempo de lectura' en las entradas de tu blog de AstroPaper.
---

Como dicen los [Astro docs](https://docs.astro.build/en/recipes/reading-time/), se puede usar remark plugin para añadir una propiedad de tiempo de lectura en nuestro frontmatter. Sin embargo, por alguna razón, no podemos añadir esta característica siguiendo lo indicado en los documentos de Astro. Por lo tanto, para lograr esto, tenemos que ajustar un poco. Este post demostrará cómo podemos hacerlo.

## Índice

## Añadir tiempo de lectura en PostDetails

Paso (1) Instalar las dependencias necesarias.

```bash
npm install reading-time mdast-util-to-string
```

Paso (2) Crear el archivo  `remark-reading-time.mjs` en el directorio `utils`

```js
import getReadingTime from "reading-time";
import { toString } from "mdast-util-to-string";

export function remarkReadingTime() {
  return function (tree, { data }) {
    const textOnPage = toString(tree);
    const readingTime = getReadingTime(textOnPage);
    data.astro.frontmatter.readingTime = readingTime.text;
  };
}
```
Paso (3) Añade el plugin a `astro.config.ts`.


```js
import { remarkReadingTime } from "./src/utils/remark-reading-time.mjs"; // asegúrese de que su ruta relativa es correcta

// https://astro.build/config
export default defineConfig({
  site: SITE.website,
  integrations: [
    // other integrations
  ],
  markdown: {
    remarkPlugins: [
      remarkToc,
      remarkReadingTime, // 👈🏻 nuestro plugin
      [
        remarkCollapse,
        {
          test: "Table of contents",
        },
      ],
    ],
    // other config
  },
  // other config
});
```

Paso (4) Añadir `readingTime` al esquema del blog (`src/content/config.ts`)

```ts
import { SITE } from "@config";
import { defineCollection, z } from "astro:content";

const blog = defineCollection({
  type: "content",
  schema: ({ image }) =>
    z.object({
      // others...
      canonicalURL: z.string().optional(),
      readingTime: z.string().optional(), // 👈🏻 readingTime frontmatter
    }),
});

export const collections = { blog };
```

Paso (5) Crear un nuevo fichero llamado `getPostsWithRT.ts` en el directorio `src/utils`.

```ts
import type { MarkdownInstance } from "astro";
import type { CollectionEntry } from "astro:content";
import { slugifyStr } from "./slugify";

export const getReadingTime = async () => {
  // Obtener todos los posts usando glob. Esto es para obtener el frontmatter actualizado
  const globPosts = import.meta.glob("../content/blog/*.md") as Promise<
    CollectionEntry<"blog">["data"][]
  >;

  // A continuación, establezca los valores frontmatter en un JS Map con el par clave-valor
  const mapFrontmatter = new Map();
  const globPostsValues = Object.values(globPosts);
  await Promise.all(
    globPostsValues.map(async globPost => {
      const { frontmatter } = await globPost();
      mapFrontmatter.set(
        slugifyStr(frontmatter.title),
        frontmatter.readingTime
      );
    })
  );

  return mapFrontmatter;
};

const getPostsWithRT = async (posts: CollectionEntry<"blog">[]) => {
  const mapFrontmatter = await getReadingTime();
  return posts.map(post => {
    post.data.readingTime = mapFrontmatter.get(slugifyStr(post.data.title));
    return post;
  });
};

export default getPostsWithRT;
```

Paso (6) Refactorizar `getStaticPaths` de `/src/pages/posts/[slug].astro` como sigue

```ts
---
// other imports
import getPostsWithRT from "@utils/getPostsWithRT";

export interface Props {
  post: CollectionEntry<"blog">;
}

export async function getStaticPaths() {
  const posts = await getCollection("blog", ({ data }) => !data.draft);

  const postsWithRT = await getPostsWithRT(posts); // reemplaza la lógica del tiempo de lectura con esta func

   const postResult = postsWithRT.map(post => ({ // asegúrese de sustituir posts por postsWithRT
    params: { slug: post.slug },
    props: { post },
  }));

// other codes
```

Paso (7) Refactorizar `PostDetails.astro` así. Ahora puedes acceder y mostrar `readingTime` en `PostDetails.astro`.

```ts
---
// imports

export interface Props {
  post: CollectionEntry<"blog">;
}

const { post } = Astro.props;

const {
  title,
  author,
  description,
  ogImage,
  readingTime, // ahora podemos acceder directamente a readingTime desde frontmatter
  pubDatetime,
  modDatetime,
  tags } = post.data;

// other codes
---
```

## Acceder al tiempo de lectura fuera de PostDetails (opcional)

Siguiendo los pasos anteriores, ahora puede acceder a la propiedad frontmatter `readingTime` en su página de detalles del post. A veces, esto es exactamente lo que quieres. Si es así, puede pasar a la siguiente sección. Sin embargo, si quiere mostrar el "tiempo estimado de lectura" en el índice, en las entradas, y técnicamente en todas partes, necesita realizar los siguientes pasos adicionales.

Paso (1) Actualice `utils/getSortedPosts.ts` como sigue

```ts
import type { CollectionEntry } from "astro:content";
import getPostsWithRT from "./getPostsWithRT";

const getSortedPosts = async (posts: CollectionEntry<"blog">[]) => {
  // asegúrate de que esta función es asíncrona
  const postsWithRT = await getPostsWithRT(posts); // add reading time
  return postsWithRT
    .filter(({ data }) => !data.draft)
    .sort(
      (a, b) =>
        Math.floor(
          new Date(b.data.modDatetime ?? b.data.pubDatetime).getTime() / 1000
        ) -
        Math.floor(
          new Date(a.data.modDatetime ?? a.data.pubDatetime).getTime() / 1000
        )
    );
};

export default getSortedPosts;
```

Paso (2) Asegúrese de refactorizar cada archivo que utiliza la función `getSortedPosts`. Puedes simplemente añadir la palabra clave `await` delante de la función `getSortedPosts`.

Los archivos que utilizan la función `getSortedPosts` son los siguientes

- src/pages/index.astro
- src/pages/posts/index.astro
- src/pages/rss.xml.ts
- src/pages/posts/[slug].astro

Todo lo que tiene que hacer es lo siguiente


```ts
const sortedPosts = getSortedPosts(posts); // old code ❌
const sortedPosts = await getSortedPosts(posts); // new code ✅
```

Ahora puedes acceder a `readingTime` en otros lugares además de `PostDetails`.

## Mostrar el tiempo de lectura (opcional)

Como ahora puedes acceder a `readingTime` en los detalles de tu post (o en cualquier sitio si haces lo de la sección anterior), depende de ti mostrar `readingTime` donde quieras.

Pero en esta sección, voy a mostrarte cómo mostraría `readingTime` en mis componentes. Esto es opcional. Puedes ignorar esta sección si quieres.

Paso (1) Actualizar el componente `Datetime` para mostrar `readingTime


```tsx
import { LOCALE } from "@config";

export interface Props {
  datetime: string | Date;
  size?: "sm" | "lg";
  className?: string;
  readingTime?: string; // new type
}

export default function Datetime({
  datetime,
  size = "sm",
  className,
  readingTime, // new prop
}: Props) {
  return (
    // other codes
    <span className={`italic ${size === "sm" ? "text-sm" : "text-base"}`}>
      <FormattedDatetime pubDatetime={pubDatetime} modDatetime={modDatetime} />
      <span> ({readingTime})</span> {/* display reading time */}
    </span>
    // other codes
  );
}
```

Paso (2) A continuación, pasar `readingTime` props de su componente padre.

archivo: Card.tsx

```ts
export default function Card({ href, frontmatter, secHeading = true }: Props) {
  const { title, pubDatetime, modDatetime description, readingTime } = frontmatter;
  return (
    ...
    <Datetime
      pubDatetime={pubDatetime}
      modDatetime={modDatetime}
      readingTime={readingTime}
    />
    ...
  );
}
```

archivo: PostDetails.tsx

```jsx
// Other Codes
<main id="main-content">
  <h1 class="post-title">{title}</h1>
  <Datetime
    pubDatetime={pubDatetime}
    modDatetime={modDatetime}
    size="lg"
    className="my-2"
    readingTime={readingTime}
  />
  {/* Other Codes */}
</main>
// Other Codes
```

## Conclusión

Siguiendo los pasos y ajustes indicados, ya puedes incorporar esta útil función a tu contenido. Espero que este post te ayude a añadir `readingTime` en tu blog. AstroPaper podría incluir el tiempo de lectura por defecto en futuras versiones. 🤷🏻‍♂️
