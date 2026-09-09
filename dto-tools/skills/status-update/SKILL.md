---
name: status-update
description: Use this skill when the user wants to report the status of a project, program or initiative to a senior leader (VP, GM, sponsor, C-level) as a storytelling narrative rather than a detail-heavy report — trigger on phrases like "status update", "quiero contarle a mi jefe cómo vamos", "armame un update para el VP", "necesito reportar el avance del proyecto", "cómo le cuento esto al sponsor", "armá el storytelling del proyecto", "update para leadership", or any request to turn project reality into a short spoken narrative for someone who does not want the detail. Runs a structured interview (and reads transcripts, emails or proposals the user points at), enforces a fact/assumption/recommendation discipline, pushes back when the user's framing oversells what actually happened, and produces a branded Amcor .docx as a spoken talk track — optionally with a private preparation annex.
---

# Status Update — storytelling para liderazgo

Convertís la realidad de un proyecto en un **guion hablado de 3 a 5 minutos** para un líder
senior que no quiere el detalle. El entregable es un `.docx` con branding Amcor donde cada
bloque central es **lo que el usuario dice en voz alta**, entre comillas, listo para leer.

No es un reporte de estado. No es un dashboard. Es un guion.

## Idioma

Español por defecto, siempre — conversación y documento. Solo cambiás a inglés si el usuario
lo pide explícitamente o si nombra una audiencia de liderazgo global.

---

## La estructura narrativa (no la cambies)

Cinco movimientos. Este orden es el producto:

```
1  APERTURA        →  El titular arriba. Qué se movió y qué hay que resolver.
                      Anticipa el problema, no lo esconde para el final.

2  QUÉ SE DESTRABÓ →  Las buenas noticias primero, pero descriptas con precisión.
                      Máximo tres. Cada una nombra a quién y qué dijo.

3  DÓNDE ESTAMOS   →  El estado real: impacto al negocio cuantificado,
                      diseño, inversión, equipo. Cifras con su evidencia al lado.

4  QUÉ FALTA       →  Un solo tema abierto, no una lista. El que puede
                      cambiar el rumbo. Con fecha y dueño.

5  CIERRE          →  Qué sigue, qué NO necesita del líder hoy, y qué
                      dependencia se planta para más adelante.
```

**Por qué este orden.** Un líder senior decide en los primeros treinta segundos si esto es
un problema o un avance. Si el problema aparece en el minuto cuatro, la reacción no es al
problema, es a que se lo escondieron.

**La regla del cierre.** Casi siempre el cierre debe decir "no necesito nada tuyo hoy" y
después plantar la dependencia futura en una sola frase. Eso convierte una charla informativa
en una inversión de capital político. Es el bloque más valioso del documento.

---

## Cómo conducir la sesión

### Paso 1 — Encuadrar antes de preguntar

Averiguá primero, con `AskUserQuestion` cuando haya opciones discretas:

| Qué | Por qué importa |
|---|---|
| Quién es la audiencia y cuál es su rol | Un sponsor ya conoce el contexto: no le expliques su propio programa. Un líder externo al programa necesita dos líneas de encuadre. |
| Cuánto tiempo tiene la charla | Define cuántos bloques entran. 3 min = 4 bloques. 5 min = los 5 completos. 10 min = agregás sub-secciones. |
| Qué quiere que el líder haga al final | Informar / decidir entre escenarios / desbloquear algo. Cambia el cierre entero. |
| Si quiere el anexo privado | Preguntá siempre. Ver más abajo. |

**Si la audiencia es el sponsor del programa, borrá todo el contexto.** El error más común es
explicarle a alguien lo que ya sabe. Va directo a qué se movió.

### Paso 2 — Leer lo que haya

Si el usuario señala transcripts, cadenas de mail, propuestas comerciales o carpetas, leelos
antes de preguntar. Extraé: nombres y roles reales, citas textuales, cifras con su fuente,
compromisos con fecha, y los desacuerdos entre personas. Los desacuerdos son el material más
valioso: casi siempre son el verdadero estado del proyecto.

No barras carpetas enteras sin que te lo pidan.

### Paso 3 — Entrevistar

Preguntá por los cinco movimientos, en ese orden. Preguntas que funcionan:

- "¿Qué se movió desde la última vez que hablaron?"
- "¿Quién lo dijo, y con qué palabras?" — las citas textuales valen más que los resúmenes
- "¿Qué número tenés y de dónde salió?"
- "¿Qué es lo único que podría cambiar el rumbo de esto?"
- "¿Qué querés que haga el líder al terminar la charla?"
- "¿Hay algo que preferirías que no pregunte?" — eso suele ser exactamente el punto 4

### Paso 4 — Hacer pushback (obligatorio)

Antes de escribir nada, contrastá el encuadre del usuario contra las fuentes. Este paso no es
opcional y es la mitad del valor del skill.

Los patrones a cazar, con la corrección:

| Lo que el usuario dice | Lo que suele haber pasado | Qué proponer |
|---|---|---|
| "Nos dieron luz verde" | Avalaron una parte — el partner, la factibilidad técnica — no el proyecto | "Validaron X. El proyecto sigue pendiente de Y." Igual de positivo, y exacto. |
| "El problema está resuelto" | Hay una alternativa propuesta que todavía nadie confirmó | Bloque `status_cols`: validado a la izquierda, en definición a la derecha |
| "Estamos a punto de lanzar" | Falta una decisión que no depende del usuario | Nombrar la decisión, la fecha y el dueño |
| "Ya está definido el equipo" | Se propuso un nombre y no está confirmado | "Se propuso a X. Te lo traigo como propuesta, no como decisión." |
| "La restricción es técnica" | La restricción es de alineación organizacional | Decir cuál es y quién la destraba |

Decilo en una o dos frases, directo, con el motivo del riesgo: **si el líder repite el
encuadre optimista y después se cae, el costo lo paga el usuario.** Después ofrecé la versión
exacta, que casi siempre suena igual de fuerte.

Si un desacuerdo interno está sin resolver, no lo resuelvas en el documento. Nombralo, decí
cuándo se dirime y quién está en la mesa.

### Paso 5 — Integridad de la información

Regla dura, sin excepciones:

- **Dato** — verificado en una fuente. Va tal cual, y si es una cita, entre comillas con el autor.
- **Supuesto** — marcado como tal en el texto. "Mi lectura es…", "Sin confirmar".
- **Recomendación** — explícitamente una opinión del usuario.
- **Hueco** — `[COMPLETAR]` visible en el documento. Nunca rellenado con algo plausible.

Nunca inventes cifras, nombres de personas, nombres de sistemas ni fechas. Si una cifra viene
de una fuente con una inconsistencia interna, marcalo en el anexo y no la cites en el guion.

Un `[COMPLETAR]` a la vista es mejor que un número inventado: si el líder lo encuentra, la
respuesta correcta es "está marcado, lo cierro el martes".

### Paso 6 — Escribir las líneas habladas

Cada bloque `say` es texto que el usuario va a leer en voz alta. Por lo tanto:

- Primera persona, dirigiéndose al líder por su nombre en la apertura.
- Frases cortas. Si no se puede decir en una respiración, partila.
- Cifras redondeadas y dichas como se dicen: "440 mil dólares", no "USD 440.000".
- Cero jerga que el líder no use. Si es inevitable, la explicás en la misma frase.
- Una analogía por documento como máximo, y solo si aclara algo. Dos ya es decorativo.
- Nada de "quiero comentarte que" ni "es importante mencionar". Directo.

Longitud objetivo: **2 páginas el guion**. Si se va a 3, sacaste contenido de menos.

### Paso 7 — El anexo privado

Preguntá siempre si lo quiere. Si sí, va después de un `pagebreak` con su propio `subheader`,
y contiene cuatro secciones:

- **A · Si pregunta** — las 5 o 6 preguntas más probables, con la respuesta hablada. Incluí
  siempre la del retorno o el costo si hay cifras en juego.
- **B · Antes de la charla, cerrá** — los `[COMPLETAR]` y todo lo que el líder podría
  preguntar y el usuario no sabe. Con el motivo de por qué importa.
- **C · Lo que no conviene decir** — el detalle técnico, los desacuerdos internos y las
  opiniones de terceros que no suman a esta audiencia. Aclarando que si pregunta, lo tiene.
- **D · Advertencias** — riesgos de posición política: compromisos que el usuario ya tomó por
  escrito, aliados que están saliendo de su rol, encuadres que no puede sostener.

Advertí una vez que el anexo no es compartible tal cual.

### Paso 8 — Renderizar y verificar

Escribís el spec JSON, corrés el renderer, convertís a imágenes y **las mirás**. No entregues
sin ver el resultado.

Las rutas son relativas al directorio de este skill (`<skill_dir>/scripts/`). Depende de
`python-docx`; para la verificación visual, de LibreOffice (`soffice`) y `pdftoppm` (Poppler).

```bash
python3 <skill_dir>/scripts/render_status_update.py spec.json "salida.docx"

# verificación visual — obligatoria
soffice --headless --convert-to pdf "salida.docx" >/dev/null 2>&1
pdftoppm -jpeg -r 100 salida.pdf pg
# copiá los pg-*.jpg al directorio de outputs y leelos con Read
```

Qué revisás en las imágenes:

- El guion cabe en 2 páginas y ninguna sección queda sola al final de una página.
- Ninguna fila de tabla se corta en el salto de página.
- No hay una página con un solo bloque.

Si una sección quedó huérfana: acortá una línea hablada o bajá `pts` en un `spacer`. No
cambies los tamaños de fuente.

Guardás en la carpeta del proyecto que corresponda, nombre en minúsculas con guiones
(`status-update-<proyecto>-<aaaa-mm-dd>.docx`), y lo compartís con `present_files`.

**Si falta una dependencia** (`python-docx`, `soffice` o `pdftoppm`), construís el `.docx`
igual con `python-docx` y respetás el sistema de diseño de abajo a mano: Arial, hoja Letter,
márgenes 0.75", y el bloque hablado como tabla de una celda con fondo `#F2F7FA` y filete
izquierdo de 3pt en `#00A1DE`, texto en cursiva `#00395A` entre comillas tipográficas. Si no
podés renderizar a imagen, decíselo al usuario en vez de entregar sin verificar.

---

## Diseño

Sistema Amcor, ya implementado en el renderer. No lo toques.

- **Dark Blue `#00395A`** dominante: títulos, texto hablado, etiquetas.
- **Light Blue `#00A1DE`** acentos: numeración de secciones, filete del bloque hablado, viñetas.
- **Green `#00A551`** oportunidad, beneficio, lo validado.
- **Orange `#E98300`** exposición y riesgo, nada más. Si todo es naranja, nada es naranja.
- **Arial** — tipografía secundaria aprobada de Amcor para documentos internos y digitales.

---

## Spec JSON — referencia de bloques

```json
{
  "header": {
    "eyebrow": ["BUSINESS UPDATE", "NOMBRE DEL PROGRAMA · UNIDAD"],
    "title": "Guion de conversación — <Nombre del líder>",
    "subtitle": "Estado del programa X  ·  <alcance>  ·  ~5 minutos",
    "meta": "<fecha>   ·   Borrador — <autor>"
  },
  "sections": [ /* bloques, en orden */ ]
}
```

Un segmento de texto enriquecido es `"texto plano"` o una lista mezclando strings y
`{"t": "texto", "b": true, "i": true, "color": "dark|lblue|green|orange|grey"}`.

| Bloque | Forma | Cuándo |
|---|---|---|
| `h1` | `{"type":"h1","num":"1","text":"Apertura"}` | Cada uno de los cinco movimientos |
| `h2` | `{"type":"h2","text":"3.1   Impacto al negocio"}` | Sub-secciones dentro de "Dónde estamos" |
| `lead` | `{"type":"lead","text":"..."}` | Una línea gris de encuadre bajo un título |
| `say` | `{"type":"say","lines":["...","..."]}` | **El bloque central.** Lo que se dice en voz alta |
| `bullets` | `{"type":"bullets","items":[{"label":"Título.","text":"..."}]}` | Las tres cosas que se destrabaron |
| `kpis` | `{"type":"kpis","items":[{"value":"$3.0M+","label":"...","color":"green"}]}` | 2 a 4 cifras titulares. Nunca más de 4 |
| `evidence` | `{"type":"evidence","header":[...],"rows":[{"impact":"...","evidence":"...","value":"$36.5M","note":"...","color":"orange"}]}` | Cifras con la prueba al lado. Sin `color` la cifra se ve chica y neutra — usalo para `[COMPLETAR]` |
| `status_cols` | `{"type":"status_cols","left":{"title":"Validado","items":[...]},"right":{"title":"En definición","items":[...]}}` | **Bloque de honestidad.** Cuando algo puede confundirse con una decisión ya tomada |
| `qa` | `{"type":"qa","items":[{"q":"¿...?","a":"..."}]}` | Solo en el anexo |
| `note` | `{"type":"note","text":[...]}` | Una línea de cierre o énfasis fuera de un bloque hablado |
| `pagebreak` | `{"type":"pagebreak"}` | Antes del anexo |
| `subheader` | `{"type":"subheader","eyebrow":"ANEXO — SOLO PARA VOS","title":"Preparación y respuestas"}` | Portada del anexo |
| `spacer` | `{"type":"spacer","pts":6}` | Ajuste fino de paginado |

`scripts/example-spec.json` es un spec completo y funcional. Leelo antes de escribir el primero.

---

## Errores que arruinan el entregable

1. **Explicarle el contexto al sponsor.** Si conoce el programa, el bloque 1 sobra.
2. **Aceptar el encuadre optimista del usuario.** El paso 4 no es opcional.
3. **Meter cinco temas en "Qué falta".** Uno. El que puede cambiar el rumbo.
4. **Una cifra sin su evidencia.** Todo número grande va en `evidence` o en un `say` que
   nombre de dónde salió.
5. **Rellenar un hueco con algo plausible.** `[COMPLETAR]`, visible.
6. **Pedirle una decisión cuando el usuario dijo que solo quería informar.** Y al revés.
7. **Entregar sin mirar el PDF renderizado.**
8. **Tres páginas de guion.** Es señal de que no se editó.
