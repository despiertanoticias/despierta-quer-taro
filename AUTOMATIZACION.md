# Publicación automática — instrucciones para la tarea programada

Esta tarea corre dos veces al día (mañana y tarde, hora del centro de México) y publica en despiertaqueretaro.com.

## 1. Buscar las noticias
- Busca en la web las noticias más importantes de las últimas 12 horas en Querétaro (capital y los 18 municipios), en México y en el mundo.
- Prioridad: Querétaro > Nacional > Política > Economía > Internacional > Deportes > Entretenimiento > Tecnología > Educación.
- Medios locales: Diario de Querétaro, AM Querétaro, El Universal Querétaro, Quadratín Querétaro, Plaza de Armas, Noticias de Querétaro, Código Qro, Telediario Querétaro, Rotativo. Nacionales: Uno TV, Infobae México, Milenio, El Universal, La Jornada, Reforma, Excélsior, El Financiero, Expansión, Proceso. Abre las notas para confirmar los datos.
- Antes de escribir, lee los títulos de `content/notas/` de los últimos 2 días y **no repitas** una nota que ya existe. Si un tema avanzó, escribe una nota nueva con el dato nuevo.

## 2. Escribir 20 notas
Crea **exactamente 20** archivos nuevos en `content/notas/`, uno por nota, con nombre `AAAA-MM-DD-titular-en-minusculas-con-guiones.json` (máximo 70 caracteres después de la fecha) y este formato:

```json
{
  "titulo": "Titular claro, en tus palabras",
  "seccion": "queretaro",
  "fecha": "2026-10-23T06:20",
  "resumen": "Dos o tres frases con los hechos: qué pasó, dónde, cifras y quién lo dijo.",
  "cuerpo": "",
  "imagen_tema": "acueducto",
  "imagen": "",
  "credito": "",
  "fuentes": [{ "medio": "Diario de Querétaro", "enlace": "https://..." }],
  "destacada": false,
  "autor": "Redacción"
}
```

Reglas:
- `seccion`: queretaro, nacional, politica, economia, internacional, entretenimiento, tecnologia, educacion o deportes. Al menos 8 de las 20 deben ser de `queretaro`. Notas de política o educación locales (Legislatura, UAQ, USEBEQ) pueden ir en `politica` o `educacion`.
- `fecha`: la hora de la ejecución (hora del centro). Usa minutos distintos para conservar el orden de importancia (la más importante con la hora más reciente).
- Marca `"destacada": true` en las 4 más importantes; de preferencia, al menos 2 de Querétaro.
- `imagen_tema`: una de las claves de `assets/imagenes.js` que corresponda al tema o lugar (por ejemplo `uaq`, `sanjuan`, `corregidora` para Gallos Blancos, `industria` para inversiones, `trafico` para accidentes y movilidad, `gobierno` para el Gobierno del Estado o la Legislatura). Si ninguna encaja, usa `centro` para Querétaro o `zocalo` para el país.
- **Redacta todo con tus propias palabras.** No copies frases de los medios; como máximo, una cita breve (menos de 15 palabras) entre comillas si la frase exacta importa.
- **No inventes datos.** Cada cifra, nombre o fecha debe estar en la fuente enlazada. Si una fuente solo da el titular, escribe una nota breve con eso.
- Cada nota lleva al menos una fuente con su enlace real.
- Temas delicados (violencia, salud, política): tono neutral, sin adjetivos ni opiniones.

## 3. Actualizar los datos del día
Edita `content/hoy.json` (mismo formato que ya tiene):
- `fecha` ("Viernes 23 de octubre de 2026") y `actualizado` (hora).
- `clima`: máxima, mínima, pronóstico, probabilidad de lluvia y viento de Santiago de Querétaro (SMN / Conagua; Telediario publica el pronóstico por municipio). `ahora` solo si tienes la temperatura actual de una fuente.
- `municipios`: 5 o 6 municipios (San Juan del Río, Corregidora, El Marqués, Tequisquiapan, Amealco, Jalpan de Serra).
- `vialidades`: estado de la autopista México-Querétaro (Capufe / Guardia Nacional), carretera 57, Paseo de la República, 5 de Febrero, Bernardo Quintana y Qrobús, solo con reportes confirmados.
- `avisos`: cortes de agua de la CEA, obras, alertas de Protección Civil o trámites con fecha límite.
- `agenda`: eventos, ferias y manifestaciones anunciadas para el día.
Si no encuentras un dato, quita esa fila o deja el anterior; no lo inventes.

## 4. Revisar y publicar
1. Ejecuta `node scripts/build.mjs`. Si marca errores, corrígelos.
2. Confirma que hay 20 archivos nuevos y que ninguno repite una nota anterior.
3. Haz commit en `main` con el mensaje `Noticias del AAAA-MM-DD (mañana|tarde)` y push. Netlify publica solo.
4. Envía al usuario un mensaje corto: cuántas notas se publicaron, los 4 titulares destacados y cualquier problema.
