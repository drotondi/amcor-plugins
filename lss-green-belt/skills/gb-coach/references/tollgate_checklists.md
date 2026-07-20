# Tollgate checklists por fase DMAIC

Preguntas de revisión que un Master Black Belt (MBB) usaría en una revisión de tollgate real. Cada pregunta se presenta como botón Sí / Parcial / No. Un "No" o "Parcial" sin justificación sólida es una señal de gap, no un fallo automático — el objetivo es que el candidato entienda el gap, no que apruebe un examen.

## Define

1. ¿El problema está redactado como un hecho observable y medible, sin causa ni solución incluida?
2. ¿Hay evidencia cuantitativa (datos, no solo percepción) que respalde que el problema existe?
3. ¿El alcance del proyecto está explícitamente delimitado (qué incluye y qué NO incluye)?
4. ¿Se identificó claramente quién es el cliente (interno o externo) afectado por el problema?
5. ¿Existe al menos un CTQ (Critical to Quality) derivado de una necesidad real del cliente (VOC)?
6. ¿El SIPOC cubre el proceso de punta a punta sin saltarse pasos intermedios relevantes?
7. ¿El business case cuantifica el impacto (costo, tiempo, calidad, riesgo) en términos concretos?
8. ¿El equipo del proyecto tiene sponsor, champion/MBB y Green Belt claramente asignados?

**Pitfalls comunes en Define:** confundir el problema con la solución ("necesitamos un dashboard"); un alcance tan amplio que el proyecto nunca cierra; un CTQ inventado sin conectarlo a una voz de cliente real.

## Measure

1. ¿Existe un plan de recolección de datos (qué, cómo, quién, cuándo) antes de salir a medir?
2. ¿La métrica clave (Y) está operacionalmente definida sin ambigüedad (todos medirían lo mismo)?
3. ¿Se validó el sistema de medición (Gage R&R o equivalente) antes de confiar en los datos?
4. ¿El tamaño de muestra recolectado es representativo del proceso (no solo un día bueno o malo)?
5. ¿Se estableció la línea base (baseline) del proceso con datos reales, no con supuestos?
6. ¿Se calculó la capacidad del proceso (Cp/Cpk o Z-score) cuando aplica a datos continuos?
7. ¿Los datos fueron estratificados por las variables sospechosas (turno, línea, operador, producto)?

**Pitfalls comunes en Measure:** medir sin definir operacionalmente la métrica; saltar la validación del sistema de medición; recolectar datos convenientes en vez de representativos.

## Analyze

1. ¿Se generaron múltiples causas potenciales (Ishikawa, brainstorming) antes de fijarse en una sola?
2. ¿Las causas potenciales se priorizaron con datos (Pareto, frecuencia, impacto) en vez de opinión?
3. ¿Se aplicó al menos una técnica de causa raíz (5 Whys u otra) hasta llegar a algo accionable?
4. ¿Las causas raíz candidatas fueron validadas estadísticamente con los datos (no solo lógica)?
5. ¿Se eligió el test estadístico correcto según el tipo de dato (continuo/discreto, número de grupos)?
6. ¿El resultado del test se interpretó correctamente (p-value, significancia práctica vs. estadística)?
7. ¿Se descartaron explícitamente las causas que los datos no soportaron, en vez de ignorarlas?

**Pitfalls comunes en Analyze:** parar en la primera causa "obvia" sin validarla con datos; confundir correlación con causalidad; elegir un test estadístico por costumbre en vez de por el tipo de dato.

## Improve

1. ¿Las soluciones propuestas atacan directamente la(s) causa(s) raíz validada(s) en Analyze?
2. ¿Se generaron y compararon múltiples alternativas de solución antes de elegir una?
3. ¿Se corrió un piloto o prueba a pequeña escala antes de un rollout completo?
4. ¿Los resultados del piloto se midieron con la misma métrica (Y) definida en Measure?
5. ¿Se evaluaron riesgos o efectos secundarios no deseados de la solución (FMEA o equivalente)?
6. ¿Existe un plan de implementación con responsables y fechas, no solo la idea de la solución?

**Pitfalls comunes en Improve:** implementar una solución sin pilotearla; elegir la primera idea sin comparar alternativas; no volver a medir con la misma métrica de Measure, perdiendo la comparación antes/después.

## Control

1. ¿Existe un plan de control documentado (qué se monitorea, con qué frecuencia, quién reacciona)?
2. ¿Se definieron límites de control o umbrales claros para detectar que el proceso se sale de rango?
3. ¿Los procedimientos/documentos del proceso se actualizaron para reflejar el nuevo estándar?
4. ¿El equipo/operación fue entrenado en el nuevo proceso, no solo informado por email?
5. ¿Se definió un plan de reacción (reaction plan) ante una señal de que el proceso se degrada?
6. ¿Se programó una revisión de sostenibilidad a mediano plazo (30/60/90 días) del resultado?

**Pitfalls comunes en Control:** entregar la mejora sin un plan de control formal; no entrenar a quienes operan el proceso día a día; declarar victoria sin una revisión de sostenibilidad posterior.

## Criterio de Go / No-Go

- **Go**: todas las preguntas de la fase son "Sí", o los "Parcial" tienen un plan concreto y de corto plazo para cerrarse.
- **Go con condiciones**: 1-2 preguntas en "No" o "Parcial" sin plan, pero ninguna es bloqueante para empezar la siguiente fase en paralelo. Listar explícitamente qué queda pendiente y para cuándo.
- **No-Go**: 3+ preguntas en "No", o cualquier pregunta fundacional (ej. problema mal definido en Define, sistema de medición no validado en Measure, causa raíz no validada con datos en Analyze) sin resolver. Explicar puntualmente qué falta y sugerir qué hacer antes de volver a intentar el tollgate.
