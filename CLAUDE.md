# Plantilla «Coworking y espacios» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **urbano**
(señalética de edificio industrial, a todo el ancho). El brief de diseño está en `DISEÑO.md`.
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa (también las listas propias `espacios` y `cifras`); no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = carbón de las bandas oscuras, acento = coral de las bandas de color y los botones, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…). El color del texto sobre el primario y sobre el acento se calcula solo (`--sobre-primario`, `--sobre-acento` en `src/styles/global.css`): aguanta cualquier color del cliente.
- **Tipografías y aspecto general**: `src/styles/global.css` (titulares sans de sistema muy pesados, rótulos en monoespaciada con un cuadrado del acento `.rotulo`, bandas `.banda--oscura|acento|clara|blanca`, retícula `.plano`, botones `.btn`/`.btn-sec` con flecha, cabecera `.cabecera--urbana` y pie `.pie--urbano`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos del ejemplo van en `public/fotos/` (se generan a partir de `fotos.json`); las de respaldo, en `public/placeholders/` (`Imagen.astro` las muestra si una foto falta). En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Personas: `/placeholders/persona.svg` hasta que el cliente suba la suya.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en un cuadrado del acento + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas son bandas a todo el ancho.
- `hero` → `hero.astro`: foto a sangre casi a pantalla completa con velo, título enorme, dos botones, placa con dirección y horario (escritorio) y franja de color con `items` (titulo, texto). La cabecera es transparente sobre ella hasta hacer scroll.
- `espacios` → `espacios.astro`: zigzag 50/50 a sangre, una fila por espacio. Lista `espacios` (nombre, texto, precio, periodo, capacidad, incluye con «;», imagen, destacado). El destacado lleva la ficha en carbón. `cta` = enlace de cada fila.
- `servicios` → `servicios.astro`: banda carbón con retícula y rejilla de 4 columnas con líneas finas. `items` (titulo, texto, icono). `imagen` opcional: franja de foto a sangre debajo.
- `comunidad` → `comunidad.astro`: banda de acento con título, cita grande (`declaracion` + `firma`) y cifras (`cifras`: titulo = cifra, texto = etiqueta); banda clara con `personas` (nombre, cargo, foto, texto).
- `eventos` → `eventos.astro`: agenda en filas a todo el ancho. Lista `noticias` (fecha libre «13 nov», hora, titulo, texto, categoria, url). Sin eventos no se pinta.
- `galeria` → `galeria.astro`: mosaico de borde a borde sin márgenes (`galeria`: rutas).
- `visita` → `visita.astro`: foto a sangre + pasos (`items`: titulo, texto) y formulario de visita con día y espacio (las opciones salen de los espacios). `boton` opcional = texto del botón.
- `preguntas` → `preguntas.astro`: acordeón `details/summary` en banda carbón; sin preguntas no se pinta.
- `contacto` → `contacto.astro`: banda de acento con los datos en grande, botones de llamar y WhatsApp y formulario en bloque carbón.
- `texto` → `texto.astro`: apartado genérico (con imagen, 50/50 a sangre; sin imagen, título y texto a todo el ancho).

Iconos disponibles (`items[].icono`): wifi, taza, llave, buzon, impresora, telefono, taquilla, bici, sala, enchufe, planta, usuarios, calendario, reloj, mapa, correo, mensaje, escudo, estrella, check (`src/components/ui/Icono.astro`).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre como cadena (`"240 €"`, `"Consultar"`).
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Varios valores en un campo: cadena con «;» (`incluye: "Wifi; Café; Taquilla"`). Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: crea `src/components/secciones/<id>.astro` (copia la estructura de una existente: `seccion(id)`, una banda `banda--…` a todo el ancho y `.contenedor` dentro) y añade `secciones.<id>` en `site.yaml`. `src/pages/index.astro` la recoge sola.
7. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida y respaldo), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto en móvil (`.contenedor`), sin scroll horizontal, botones de 44 px de alto como mínimo. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el nombre de la ficha); las decorativas, `alt=""`.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.espacios.espacios` → `/espacios/<slug>/` (espacio).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/espacios/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).
