# Coworking y espacios: brief de diseño

Plantilla `coworking-espacios` creada el 29/10/2026 a partir de `corporativa-clasica` con `php artisan plantillas:nueva`
y rediseñada entera (tanda «ancho completo»). Este fichero se queda en el repo: es lo que lee quien (persona o
agente) rediseñe la plantilla.

## Brief

- **Para quién**: coworkings, oficinas y despachos compartidos, centros de negocios y alquiler de salas por horas
  (`sectores`: coworking, oficinas, espacios, salas, centro-negocios). Quien entra quiere ver cómo es el sitio,
  qué puede alquilar, cuánto cuesta y si el ambiente le encaja.
- **Qué tiene que conseguir**: que pidan una **visita** (botón de la cabecera, del hero y de cada espacio) o que
  llamen / escriban por WhatsApp.
- **Tono y estilo** (`urbano`): industrial, directo, con carácter. Referencia sí: la señalética de un edificio
  rehabilitado (rótulos, números de planta, flechas, planos) y https://losmartesnohayluna.com/ por las bandas a
  sangre. Referencia no: la web de un centro de negocios corporativo con tarjetas blancas y fotos de stock de
  gente sonriendo.
- **Concepto**: «la nave». Bandas a todo el ancho que alternan **carbón** (con retícula de plano), **coral** y
  **blanco roto**; rótulos en monoespaciada con un cuadrado de color (como las placas de una puerta); números de
  orden «01 / 05»; flechas «→» en botones y enlaces; esquinas rectas en todo.
- **Paleta de ejemplo**: primario `#1e1f22` (carbón), acento `#ff6a4d` (coral), fondo `#f5f3ef` (blanco roto),
  texto `#17181a`. El texto sobre el primario y sobre el acento se elige solo (blanco o casi negro) con color
  relativo (`--sobre-primario`, `--sobre-acento`), así que el diseño aguanta cualquier par de colores del cliente.
- **Tipografía**: del sistema. Titulares sans muy pesados (800) y apretados (`letter-spacing: -0.035em`, hero a
  7,5 rem en escritorio y 2,75 rem en móvil); rótulos, fechas, horas y etiquetas en monoespaciada de sistema en
  mayúsculas con interletrado; texto en `system-ui`.
- **Ritmo de bandas** (ejemplo): hero foto a sangre + franja coral → espacios en zigzag 50/50 (claro, blanco y el
  destacado en carbón) → servicios carbón con retícula → comunidad coral (cita enorme + cifras) + personas en
  blanco → eventos carbón → galería en mosaico de borde a borde → visita 50/50 (foto + formulario en blanco) →
  preguntas carbón → contacto coral → pie carbón con el nombre como rótulo gigante.

## Apartados

| id | Qué enseña | Lista propia |
|---|---|---|
| `hero` | Foto a sangre (92svh), velo carbón, título enorme, dos botones, placa con dirección y horario, franja coral | `items` (titulo, texto) |
| `espacios` | Una fila 50/50 a sangre por espacio, alternando lados: número, capacidad, nombre, texto, qué incluye, precio y periodo | `espacios` (nombre, texto, precio, periodo, capacidad, incluye «;», imagen, destacado) |
| `servicios` | Rejilla 4×2 de módulos con icono separados por líneas finas | `items` (titulo, texto, icono) |
| `comunidad` | Cita enorme, cifras gigantes y personas del equipo | `cifras` (titulo, texto), `personas` |
| `eventos` | Agenda como un panel de salidas: día enorme en coral, mes, tipo y hora en mono | `noticias` (fecha, hora, titulo, texto, categoria, url) |
| `galeria` | Mosaico sin márgenes, 2 columnas en móvil y 4 en escritorio, una foto 2×2 cada siete | `galeria` (rutas) |
| `visita` | Foto a sangre + pasos numerados + formulario con día y espacio de interés | `items` (titulo, texto) |
| `preguntas` | Título fijo a la izquierda y acordeón a la derecha | `preguntas` |
| `contacto` | Datos en tipografía grande, llamar y WhatsApp, formulario en bloque carbón | — |
| `texto` | Genérico: 50/50 a sangre con imagen o título + texto a todo el ancho | `items` |

## Fotos

`fotos.json` (14): nave rehabilitada con cerchas de hierro, ladrillo visto y lucernarios; puestos, despacho,
sala de reuniones, sala de eventos, cocina, cabina, bicis, fachada y recepción. Siempre sin personas, sin rótulos
ni texto legible, sin logotipos. Personas del equipo con `/placeholders/persona.svg`.

## Qué no hacer

- Nada de caja centrada estrecha con tarjetas blancas ni esquinas redondeadas: todo son bandas y líneas.
- No usar el coral como color de texto pequeño sobre fondo claro (no llega a AA): en claro, el coral solo en
  cuadrados, líneas, iconos y números grandes.
- No poner precios ni cifras en los componentes: solo en `site.yaml`.
