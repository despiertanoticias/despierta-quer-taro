# Despierta Querétaro

Sitio de noticias de Querétaro y del país, publicado en Netlify en **https://despiertaqueretaro.com**. Es la misma plataforma que Despierta Ciudad de México, con la marca, las secciones y el panel lateral adaptados a Querétaro.

## Cómo publicar una nota (panel)
1. Entra a **https://despiertaqueretaro.com/admin**.
2. Inicia sesión con GitHub.
3. En **Notas → Nueva nota**, llena titular, sección, resumen y, si quieres, el texto completo y una foto.
4. Pulsa **Guardar / Publicar**. En uno o dos minutos aparece en el sitio.

Desde el mismo panel puedes editar o borrar notas y cambiar los **Datos del día** (clima de la capital y por municipio, vialidades y Qrobús, avisos y agenda).

> El panel guarda en el repositorio `despiertanoticias/despierta-quer-taro`. Si el repositorio tiene otro nombre, cámbialo en `admin/config.yml` (línea `repo:`).

## Publicación automática
Las instrucciones para la tarea programada que agrega noticias dos veces al día están en `AUTOMATIZACION.md`.

## Estructura
- `content/notas/*.json` — una nota por archivo
- `content/hoy.json` — clima, vialidades, avisos y agenda del día
- `scripts/build.mjs` — junta todo en `assets/datos.js` (Netlify lo ejecuta en cada publicación)
- `assets/imagenes.js` — fotos de archivo de Wikimedia Commons por tema (Querétaro, nacional e internacional)
- `assets/logo.webp`, `assets/logo.png`, `assets/og.png`, `assets/favicon.svg` — identidad
- `admin/` — panel de publicación
- `img/subidas/` — fotos que subes desde el panel

## Netlify
- Comando de build: `node scripts/build.mjs` · Carpeta publicada: `.` (ya configurado en `netlify.toml`).
- Dominio: `despiertaqueretaro.com`, con redirección de `www` al dominio principal.

## Lo que publicas desde /admin no gasta créditos de Netlify
Netlify cobra 15 créditos por cada publicación del sitio. Para que lo que subes desde el panel no cueste:
- `scripts/omitir-build.sh` le dice a Netlify que **no** publique cuando el cambio viene del panel (notas nuevas, ediciones, borrados, fotos o datos del día).
- `assets/en-vivo.js` hace que el sitio lea esos cambios directo de GitHub y los muestre de inmediato (la nota abre en `nota.html?id=...`).
- La siguiente publicación automática (o cualquier cambio de diseño) sí publica el sitio completo y la nota recibe su página fija y su lugar en el sitemap.
