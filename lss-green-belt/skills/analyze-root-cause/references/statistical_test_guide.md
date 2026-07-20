# Guía de selección de test estadístico

Árbol de decisión para recomendar qué test usar para validar (o descartar) una causa raíz candidata con datos, según el tipo de dato y la pregunta que se quiere responder. El objetivo es sugerir el test correcto, no ejecutarlo — el usuario corre el test en Minitab/Excel/Python y trae el resultado (p-value) de vuelta para interpretarlo.

## Paso 1 — ¿qué pregunta querés responder?

1. **Comparar el promedio/mediana de una variable numérica entre 2 grupos** (ej. turno A vs turno B, antes vs después) → ir a Paso 2A.
2. **Comparar el promedio/mediana de una variable numérica entre 3 o más grupos** (ej. 3 líneas, 4 proveedores) → ir a Paso 2B.
3. **Ver si dos variables categóricas están relacionadas** (ej. tipo de defecto vs turno) → **Chi-cuadrado de independencia**.
4. **Ver la relación/asociación entre dos variables numéricas continuas** (ej. temperatura vs % de scrap) → ir a Paso 2C.
5. **Ver si la variabilidad (no el promedio) difiere entre grupos** (ej. ¿un proveedor es más inconsistente que otro?) → **Test de Levene** (o F-test de 2 varianzas si son solo 2 grupos y los datos son normales).
6. **No estoy seguro / es otra cosa** → repreguntar con ejemplos concretos de sus datos hasta ubicarlo en una de las anteriores.

## Paso 2A — 2 grupos, variable numérica

- ¿Los mismos elementos/personas fueron medidos antes y después (datos pareados)?
  - **Sí, pareados** + datos aprox. normales → **t-test pareado**.
  - **Sí, pareados** + datos no normales o muestra chica → **Wilcoxon signed-rank**.
  - **No, son grupos independientes** + datos aprox. normales → **t-test de 2 muestras (independent samples)**.
  - **No, son grupos independientes** + datos no normales o con outliers fuertes → **Mann-Whitney U**.

## Paso 2B — 3+ grupos, variable numérica

- Datos aprox. normales y varianzas razonablemente similares entre grupos → **ANOVA de un factor (one-way ANOVA)**, seguido de **Tukey HSD** como post-hoc si el ANOVA da significativo, para ver qué pares de grupos difieren.
- Datos no normales, o varianzas muy distintas entre grupos, o muestras chicas → **Kruskal-Wallis**, seguido de comparaciones por pares (ej. Dunn) si da significativo.

## Paso 2C — relación entre dos variables numéricas

- Relación aparentemente lineal y datos aprox. normales → **Correlación de Pearson** (+ regresión lineal simple si además se quiere predecir/cuantificar el efecto).
- Relación no lineal, datos con outliers, o no normales → **Correlación de Spearman**.

## Cómo saber si los datos son "aproximadamente normales"

- Con el interfaz gráfico de Minitab/Excel: un histograma o un normal probability plot que no muestre sesgo marcado ni colas muy pesadas es suficiente para un análisis de Green Belt — no hace falta un test formal de normalidad para decidir esto en la mayoría de los casos.
- Si hace falta ser más riguroso (muestra chica, decisión de alto impacto): **Anderson-Darling** o **Shapiro-Wilk**, con p-value > 0.05 como indicio razonable de normalidad (aclarar siempre que un p-value alto no "prueba" normalidad, solo no la contradice).
- Con muestras grandes (n > 30 por grupo), el Teorema Central del Límite hace que el t-test/ANOVA sean razonablemente robustos aunque los datos no sean perfectamente normales — no hace falta ser purista en ese caso.

## Interpretación del resultado (para todos los tests)

- **p-value < 0.05** (o el umbral de significancia que el equipo use): hay evidencia estadística de diferencia/asociación — la causa candidata gana soporte, pero confirmar que la diferencia también sea **prácticamente relevante** (una diferencia estadísticamente significativa pero mínima en magnitud puede no justificar una acción).
- **p-value ≥ 0.05**: no hay evidencia suficiente para afirmar diferencia/asociación con estos datos — no equivale a "confirmar que no hay diferencia"; puede ser una causa real con muestra insuficiente, o efectivamente no ser la causa. Sugerir aumentar la muestra si hay dudas antes de descartar la hipótesis por completo.
- Nunca declarar una causa raíz como "confirmada" solo por lógica o intuición del equipo si hay datos disponibles para testearla — y nunca declararla "confirmada" solo por un p-value bajo sin que la relación tenga sentido de negocio/proceso.
