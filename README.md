# Plantilla NoExpertise · Coworking y espacios

Web urbana a todo el ancho para coworkings, oficinas compartidas, centros de negocios y alquiler de salas.
Ejemplo: Nau Trenta Coworking, una nave rehabilitada del Poblenou (Barcelona), negocio ficticio.

- Sectores: coworking, oficinas, espacios, salas, centro-negocios. Estilo: urbano. Plan mínimo: presencia.
- Secciones: hero, espacios, servicios, comunidad, eventos, galeria, visita, preguntas, contacto (y `texto` para apartados nuevos).
- Campos propios:
  - `espacios.espacios[]`: nombre, texto, precio (cadena), periodo, capacidad, incluye («;»), imagen, destacado.
  - `comunidad`: `declaracion`, `firma`, `cifras[]` (titulo = cifra, texto) y `personas[]`.
  - `eventos.noticias[]`: fecha (libre, «13 nov»), hora, titulo, texto, categoria, url.
  - `visita.items[]`: pasos (titulo, texto); `visita.boton` opcional.
  - `hero.items[]`: datos rápidos de la franja de color (titulo, texto).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos a generar en `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de respaldo (`public/placeholders/`) hechas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.espacios.espacios` con `detalle` tiene su página en `/espacios/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
