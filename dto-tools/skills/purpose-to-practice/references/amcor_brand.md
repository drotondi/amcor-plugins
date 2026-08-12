# Amcor brand spec — PDFs de la sesión de propósito

Fuente de verdad: la skill `amcor-design` (no `amcor-theme`, deprecada). Los valores de abajo son el extracto necesario para estos dos PDFs — usarlos exactamente, sin inventar colores ni ajustar la paleta.

## Colores (hex)

| Rol | Hex | Uso |
|---|---|---|
| Amcor Dark Blue | `#00395A` | Dominante. Masthead, títulos de sección, encabezados de tabla, banda del propósito. |
| Amcor White | `#FFFFFF` | Fondo de página, texto sobre oscuro. |
| Amcor Light Blue | `#00A1DE` | Acento — etiquetas de campo, filetes finos, encabezados de tabla secundarios. |
| Amcor Green | `#00A551` | Acento puntual — solo para marcar tests de calidad aprobados. |
| Negro (funcional) | `#000000` | Solo texto de cuerpo. Nunca como color de marca. |

Dark Blue domina el layout. Light Blue y Green son acentos: un filete, una etiqueta, una banda chica de encabezado — nunca una sección entera.

## Tipografía

- **Arial** (Bold para títulos, Regular para cuerpo) — fallback digital aprobado y seguro para reportlab.
- Títulos: Arial Bold, Dark Blue (o White si van sobre banda Dark Blue).
- Cuerpo: Arial Regular, negro o Dark Blue, 10-11 pt.
- Etiquetas de campo: Arial Bold, sentence case, Light Blue o Dark Blue.
- Sentence case en todo. ALL CAPS solo en encabezados de tabla muy cortos.
- Sin emoji en los PDFs (regla de marca), aunque el usuario los use en el chat.

---

## PDF 1 — Guía de facilitación

Documento operativo: el facilitador lo tiene en la mano durante la sesión. Prioridad a la legibilidad rápida sobre la densidad. Multipágina esperada.

1. **Masthead** (página 1, fondo blanco, filete Dark Blue debajo): wordmark "AMCOR" bold Dark Blue arriba a la izquierda. Subtítulo: "Digital Transformation Office". Debajo, en bold: "Guía de facilitación — Sesión de propósito: [Programa]".
2. **Grid de contexto**: tabla bordeada 2×3, borde Dark Blue fino, etiqueta (Dark Blue Arial Bold, chica) sobre valor (negro Regular):
   - Fila 1: Programa | Duración total
   - Fila 2: Participantes (cantidad y perfil) | Formato (presencial/virtual/híbrido)
   - Fila 3: Facilitador | Fecha
3. **Banda de método**: tabla de una sola celda, fondo Dark Blue, texto blanco. Una línea: "Método: Purpose-to-Practice (Liberating Structures) — Nine Whys, Remember the Future, anti-propósito, 1-2-4-All."
4. **Flujo de la sesión**: tabla de 5 filas, columnas "Paso", "Formato", "Tiempo". Encabezado con fondo Light Blue y texto blanco bold. Es el mapa de una mirada — mantenerla en la página 1.
5. **Un bloque por paso** (5 bloques, uno por paso del flujo): encabezado de sección Arial Bold Dark Blue con el número y nombre del paso, y debajo una tabla bordeada de 3 filas con etiquetas en Light Blue:
   - "Instrucción a leer" — el guion literal que el facilitador dice en voz alta.
   - "Preguntas a proyectar" — lista con `<br/>` entre preguntas, en negrita.
   - "Qué mirar" — la señal de alerta de ese paso.
6. **Reglas de la sala**: sección con tabla bordeada de una celda, 2-4 bullets.
7. **Test de calidad**: tabla numerada de 4 filas con las cuatro preguntas, encabezado Light Blue.
8. **Cuando algo se rompe**: tabla de 2 columnas ("Síntoma", "Intervención"), tomada de la reference de facilitación, filtrada a los 4-6 casos relevantes según formato y tamaño del grupo. No pegar la tabla entera si no aplica.
9. **Materiales**: lista corta al final.
10. **Footer** en todas las páginas: filete Dark Blue fino, "Amcor — Digital Transformation Office" + fecha de generación, texto chico Dark Blue.

---

## PDF 2 — Acta de propósito

Documento de registro: se comparte después y se cita meses más tarde. Prioridad a la trazabilidad de la decisión.

1. **Masthead** igual al PDF 1, con título: "Acta de propósito — [Programa]".
2. **Banda del propósito**: tabla de una sola celda a ancho completo, fondo Dark Blue, texto blanco, la frase acordada centrada en cuerpo grande (14-16 pt, Arial Bold). Es el elemento visual dominante de la página 1 — nada compite con él.
3. **Grid de contexto**: tabla bordeada 2×2 — Fecha de la sesión | Cantidad de participantes; Facilitador | Áreas representadas.
4. **Alternativas consideradas**: sección con tabla de 2 columnas ("Redacción alternativa", "Por qué se dejó de lado"), una fila por draft descartado (típicamente 2-3). No omitir esta sección aunque el acta quede más larga: es la que evita reabrir la discusión seis meses después.
5. **Anti-propósito**: sección "Lo que este programa NO es", tabla bordeada de una celda con los ítems como bullets (`Paragraph` con `<br/>`), en las palabras textuales del grupo, sin suavizar.
6. **Test de calidad**: tabla de 3 columnas ("Criterio", "Resultado", "Evidencia / ejemplo dado"). Los resultados aprobados en Amcor Green bold; los que quedaron con reservas, en Dark Blue con la reserva explicitada en la tercera columna. Nunca marcar todo como aprobado si el grupo tuvo dudas.
7. **Participantes**: tabla de 2 columnas ("Nombre", "Área / rol").
8. **Próximos pasos**: tabla de 3 columnas ("Acción", "Responsable", "Fecha").
9. **Footer** igual al PDF 1.

---

## Notas de reportlab

- **Logo:** usar `/mnt/skills/user/amcor-design/assets/logo-amcor-footer.png` (marca + wordmark en azul oscuro, 156×47 px) para el masthead sobre fondo blanco, a ~34 mm de ancho. No usar `logo-amcor-color.png`: su wordmark es blanco y desaparece sobre la página. Copiar el asset al directorio de trabajo antes de referenciarlo, ya que `/mnt/skills` es de solo lectura.
- **Celdas con etiqueta sobre valor:** armarlas como un único `Paragraph` con la etiqueta inline, no como una tabla anidada dentro de la celda — las tablas anidadas se superponen con el valor al renderizar. Patrón: `Paragraph(f'<font size="7.5" color="#00395A"><b>{LABEL}</b></font><br/>{value}', estilo_valor)`.
- Usar `platypus` (`SimpleDocTemplate`, `Paragraph`, `Table`, `Spacer`, `TableStyle`), no canvas crudo, para que las tablas fluyan entre páginas y las celdas se ajusten al contenido.
- Envolver cada bloque de paso (encabezado + tabla) en `KeepTogether` para que no se parta entre páginas: el facilitador lee un paso completo de una sola mirada.
- Colores con `from reportlab.lib.colors import HexColor` — reusar `HexColor("#00395A")`, `HexColor("#00A1DE")`, `HexColor("#00A551")`.
- Toda celda con más de unas pocas palabras debe ser un `Paragraph`, no un string crudo, para que el texto largo haga wrap en vez de desbordar.
- `TableStyle` con `GRID` (Dark Blue, 0.5 pt), `VALIGN` top, ~6 pt de padding en todas las tablas bordeadas. Encabezados con `BACKGROUND` Light Blue y texto blanco bold.
- La banda del propósito y la banda de método son `Table` de una sola celda con `BACKGROUND` Dark Blue a ancho completo.
- Guardar el archivo en el directorio de outputs y presentarlo con `present_files`.
