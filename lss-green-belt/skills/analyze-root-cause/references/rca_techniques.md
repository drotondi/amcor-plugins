# Root cause analysis techniques — guidance

## Cuándo usar cada técnica

- **Ishikawa (causa-efecto / espina de pescado)**: cuando todavía no hay hipótesis claras y hace falta generar un abanico amplio de causas potenciales antes de priorizar. Buen punto de partida cuando el efecto es claro pero las causas no.
- **Pareto**: cuando hay datos de frecuencia o impacto por categoría (tipos de defecto, motivos de reclamo, causas de downtime) y hace falta priorizar dónde enfocar el esfuerzo — el 80/20: pocas categorías explican la mayoría del efecto.
- **5 Whys**: cuando ya hay una causa candidata (de Ishikawa, Pareto, o intuición del equipo) y hace falta profundizar de "qué pasa" a "por qué pasa realmente" hasta algo accionable. No es un punto de partida cuando el campo de causas todavía es amplio — sirve para profundizar, no para explorar.

**Combinación típica y recomendada**: Ishikawa para generar causas → Pareto (si hay datos) para priorizar cuáles atacar primero → 5 Whys sobre las causas priorizadas para llegar a algo accionable → validación estadística de la causa raíz candidata con los datos.

## Ishikawa — las 6M

Categorías estándar para organizar causas potenciales:
- **Método**: procedimientos, instrucciones de trabajo, falta de estandarización.
- **Mano de obra**: entrenamiento, experiencia, fatiga, rotación.
- **Máquina**: equipos, mantenimiento, calibración, desgaste.
- **Material**: calidad de insumos, variabilidad de proveedor, especificaciones.
- **Medición**: exactitud/precisión del sistema de medición, falta de validación (Gage R&R).
- **Medio ambiente**: temperatura, humedad, layout, condiciones del lugar de trabajo.

No todas las categorías aplican siempre — está bien que 2-3 categorías queden vacías si el equipo genuinamente no identifica causas ahí.

## 5 Whys — reglas prácticas

- Cada "por qué" debe responder con un hecho verificable, no con otra opinión o suposición sin base.
- Parar quiere decir: llegaste a algo que (a) es accionable con una solución concreta, y (b) si se corrige, el efecto original razonablemente desaparece.
- Si en algún "por qué" la respuesta es "no sé" o "porque sí", eso es una señal de que hace falta ir a los datos antes de seguir preguntando — no inventar una respuesta para completar las 5 rondas.
- 5 es una guía, no una regla rígida: a veces la causa raíz aparece en el 3er "por qué", a veces hacen falta 6-7. Lo importante es el criterio de parada, no el conteo.

## Pareto — cómo interpretarlo

- Ordenar las categorías de mayor a menor frecuencia/impacto, calcular el % de cada una sobre el total, y el % acumulado.
- Las categorías cuyo % acumulado llega hasta ~80% son los "pocos vitales" — ahí va el foco del proyecto.
- Si el Pareto sale "plano" (todas las categorías con % similar, sin pocos vitales claros), es una señal en sí misma: puede que la categorización esté mal definida, o que el problema tenga causas verdaderamente dispersas y haga falta otro enfoque (ej. Ishikawa más profundo, o estratificar los datos de otra forma).
