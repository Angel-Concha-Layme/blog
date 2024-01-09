---
title: Cómo desarrollar mi sitio web y mi blog
author: Sat Naing
pubDatetime: 2022-03-25T16:55:12.000+00:00
slug: how-do-i-develop-my-portfolio-and-blog
featured: false
draft: false
tags:
  - NextJS
  - TailwindCSS
  - HeadlessCMS
  - Blog
description:
  " EJEMPLO DE POST: Mi experiencia sobre el desarrollo de mi primera web de portfolio y un blog usando NextJS y un CMS headless"
---


> Este artículo es originalmente de mi [blog post](https://satnaing.dev/blog/posts/how-do-i-develop-my-portfolio-and-blog). Puse este artículo para demostrar cómo se puede escribir entradas de blog / artículos utilizando AstroPaper.

Mi experiencia sobre el desarrollo de mi primer sitio web de portafolio y un blog usando NextJS y un CMS headless.


![Building portfolio](https://satnaing.dev/_ipx/w_2048,q_75/https%3A%2F%2Fres.cloudinary.com%2Fnoezectz%2Fimage%2Fupload%2Fv1653050141%2FSatNaing%2Fblog_at_cafe_ei1wf4.jpg?url=https%3A%2F%2Fres.cloudinary.com%2Fnoezectz%2Fimage%2Fupload%2Fv1653050141%2FSatNaing%2Fblog_at_cafe_ei1wf4.jpg&w=2048&q=75)

## Motivación

Siempre he estado pensando en lanzar mi propio sitio web con mi nombre de dominio personalizado (**satnaing.dev**) desde mi vida de estudiante universitario. Pero eso nunca sucedió hasta este proyecto. He hecho varios proyectos y trabajos sobre desarrollo de aplicaciones web pero no me había esforzado en hacer esto.

Entonces, "¿qué pasa con el blog?" te preguntarás. Sí, blog también ha estado en mi lista de proyectos desde hace algún tiempo. Siempre quise hacer un proyecto de blog utilizando algunas de las últimas tecnologías. Sin embargo, he estado ocupado con mis trabajos y otros proyectos por lo que ese proyecto de blog nunca se ha iniciado.

En estos días, tiendo a desarrollar mis propios proyectos con el foco en la buena calidad más que en la cantidad. Después de que el proyecto está hecho, suelo poner un archivo readme adecuado en el repositorio de Github. Pero Github repo readme sólo es adecuado para los aspectos técnicos (esto es sólo mi pensamiento). Quiero escribir mis experiencias y desafíos. Por lo tanto, decidí hacer mi propio blog. Además, en este momento, tengo experiencias decentes y confianza para desarrollar este proyecto.

## Tech Stack

Para el front-end, quería usar [React](https://reactjs.org/ "React Official Website"). Pero React por sí solo no es lo suficientemente bueno para SEO; y tuve que considerar muchos factores como enrutamiento, optimización de imágenes, etc. Así que elegí [NextJS](https://nextjs.org/ "NextJS Official Website") como mi principal pila de front-end. Y por supuesto TypeScript para la comprobación de tipos. (Se dice que te encantará TypeScript cuando te acostumbres a él 😉)

Para el styling, uso [TailwindCSS](https://tailwindcss.com/ "Tailwind CSS Official Website"). Esto es porque me encanta la experiencia de desarrollador que da Tailwind y tiene muchas flexibilidades en comparación con otras librerías de componentes UI como MUI o React Bootstrap.

Todos los contenidos de este proyecto residen en el repositorio de GitHub. Todas las entradas de mi blog (incluyendo esta) están escritas en formato Markdown ya que estoy muy acostumbrado a ello. Pero para escribir Markdown junto con su frontmatter sin esfuerzo, utilizo [Forestry](https://forestry.io/ "Forestry Official Website") headless CMS. Es un CMS basado en git que puede servir Markdown y otros contenidos. Debido a esto, puedo escribir mis contenidos ya sea usando Markdown o editor wysiwyg. Además, escribir frontmatters con esto es una brisa.

Las imágenes y los activos se cargan y almacenan en [Cloudinary](https://cloudinary.com/ "Cloudinary Official Website"). Conecto Cloudinary a través de Forestry y los gestiono directamente en el panel de control.


En conclusión, estos son los stack tecnológicos que he utilizado para este proyecto.

- Front-end: NextJS (TypeScript)
- Estilización: TailwindCSS
- Animaciones: GSAP
- CMS: Silvicultura Headless CMS
- Despliegue: Vercel


## Características

Las siguientes son algunas de las características de mi portafolio y blog

### SEO Friendly

Todo el proyecto está desarrollado con el enfoque SEO en mente. He utilizado etiquetas meta adecuadas, descripciones y alineaciones de encabezado. Este sitio web está indexado por Google.

> Puede buscar este sitio web en Google utilizando palabras clave como 'sat naing dev'.

![searching satnaing.dev on google](https://res.cloudinary.com/noezectz/image/upload/v1648231400/SatNaing/satnaing-on-google_asflq6.png "satnaing.dev is indexed")

Además, este sitio web se mostrará bien cuando se comparta en las redes sociales gracias al uso correcto de las metaetiquetas.

![satnaing.dev card layout when shared to Facebook](https://res.cloudinary.com/noezectz/image/upload/v1653106955/SatNaing/satnaing-dev-share-on-facebook_1_zjoehx.png "Card layout when shared to Facebook")
### Sitemap dinámico

Sitemap juega un papel importante en SEO. Debido a esto, cada página de este sitio debe ser incluido en sitemap.xml. Hice un mapa del sitio generado automáticamente en mi sitio web cada vez que creo un nuevo contenido o etiquetas o categorías.

### Temas claros y oscuros

Debido a la tendencia de temas oscuros en los últimos años, muchos sitios web incluyen tema oscuro fuera de la caja hoy en día. Ciertamente, mi sitio web también es compatible con la luz y temas oscuros.

### Totalmente Accesible

Este sitio web es totalmente accesible. Usted puede navegar por sólo con el teclado. Puse todas las mejores prácticas de mejora a11y como incluir texto alt en todas las imágenes, no saltarse los encabezados, usar etiquetas HTML semánticas, usar aria-attributes correctamente.

### Cuadro de búsqueda, categorías y etiquetas

Todos los contenidos del blog se pueden buscar mediante el cuadro de búsqueda. Además, los contenidos pueden filtrarse por categorías y etiquetas. De esta manera, los lectores del blog pueden buscar y leer lo que realmente quieren.

### Rendimiento y puntuación Lighthouse

Este sitio web obtuvo muy buen rendimiento y puntuación lighthouse gracias a un desarrollo adecuado y a las mejores prácticas. Esta es la puntuación Lighthouse de este sitio web.

![satnaing.dev Lighthouse score](https://user-images.githubusercontent.com/53733092/159957822-7082e459-11e9-4616-8f1e-49d0881f7cbb.png "satnaing.dev Lighthouse score")

### Animaciones

Inicialmente utilicé [Framer Motion](https://www.framer.com/motion/ "Framer Motion") para añadir animaciones y micro interacciones para este sitio web. Sin embargo, cuando intenté utilizar algunas animaciones complejas y efectos de paralaje, me resultó incómodo integrarme con Framer Motion (quizás no soy muy bueno ni estoy acostumbrado a trabajar con él). Por lo tanto, decidí utilizar [GSAP](https://greensock.com/ "GSAP Animation Library") para todas mis animaciones. Es una de las librerías de animación más populares y es capaz de hacer animaciones complejas y avanzadas. Puedes ver animaciones y micro interacciones en casi todas las páginas de este sitio web.



![animations at satnaing.dev](https://res.cloudinary.com/noezectz/image/upload/v1653108324/SatNaing/ezgif.com-gif-maker_2_hehtlm.gif "satnaing.dev website")

## Outro

En conclusión, este proyecto me da mucha experiencia y confianza sobre el desarrollo de sitio de blog (SSG). Ahora, he adquirido conocimientos de CMS basado en git y cómo interactúa con NextJS. También he aprendido sobre SEO, generación de sitemap dinámico e indexación de procedimientos de Google. Haré mejores proyectos en el futuro. Así que, ¡estén atentos! ✌🏻

Y... por último, pero no menos importante, me gustaría dar las 'gracias' a mi amigo [Swann Fevian Kyaw](https://www.facebook.com/bon.zai.3910 "Swann Fevian Kyaw's Facebook Account") (@[ToonHa](https://www.facebook.com/ToonHa-102639465752883 "ToonHa Facebook Page")) que ha dibujado una preciosa ilustración para mi sección hero del sitio web.

## Enlaces del proyecto

- Página web: [https://satnaing.dev/](https://satnaing.dev/ "https://satnaing.dev/")
- Blog: [https://satnaing.dev/blog](https://satnaing.dev/blog "https://satnaing.dev/blog")
- Repo: [https://github.com/satnaing/my-portfolio](https://github.com/satnaing/my-portfolio "https://github.com/satnaing/my-portfolio")

