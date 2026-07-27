# Declaración de uso de Inteligencia Artificial

**Curso:** Fundamentos en Ciencia de Datos — Maestría en Ciencia de Datos y Analítica, EAFIT
**Taller:** Taller Práctico 01 (Dataset A: Retail)
**Equipo:** Juan José Restrepo, Luis Felipe Quesada, Andrés Vélez Rendón

Este taller se resolvió con apoyo de asistentes de IA generativa, según lo permite y espera el
Pacto Pedagógico. La división del trabajo fue explícita: **el criterio analítico es del equipo;
la ejecución operativa se apoyó en IA.** Declaramos ambas partes con el mismo detalle.

## 1. Lo que decidió el equipo (criterio)

Ninguna de estas decisiones fue delegada. Son las que sostenemos frente al docente:

- La elección del conjunto de datos y la pregunta de negocio que decidimos responder.
- Qué cuenta como problema de calidad en este archivo y por qué cada uno es un riesgo para la
  decisión (columna `riesgo_para_decision` de la tabla GIGO).
- Las reglas de validación: rango geográfico de Medellín (lat 6,1–6,4; lon −75,7 a −75,4), rango
  comercial de precios (1.000–9.000 COP) y `units_sold` como entero mayor que cero.
- Las estrategias de imputación: mediana por categoría para unidades y precio, mediana geográfica
  por `store_id` para coordenadas, y la decisión de **no** imputar `customer_rating` (no se
  fabrica satisfacción) ni las fechas no convertibles.
- La llave de deduplicación y su excepción: argumentamos en 2.6 que la llave de negocio es
  `store_id + date + category + unit_price`, y documentamos por qué en este archivo concreto
  `transaction_id` resultó ser el campo más confiable.
- La lectura de la discrepancia entre el rating de las reseñas y el de las ventas: son dos
  instrumentos distintos, no un error de carga.
- La recomendación final, el costo del falso positivo y del falso negativo, y las limitaciones
  que persisten después de la limpieza.

## 2. Lo que se apoyó en IA (ejecución)

- Sintaxis de `pandas`, `matplotlib` y `seaborn` en las celdas de carga, limpieza, agregación y
  graficación.
- La estructura y el orden de las secciones del notebook.
- La **redacción** de las celdas Markdown a partir de los argumentos que el equipo definió
  previamente. El texto es asistido; el argumento no.
- El código de integración y aplanado del archivo `reseñas_clientes.json`.
- Una revisión de cumplimiento del entregable contra la guía del taller, y la organización de los
  commits del repositorio.

## 3. Cómo se validó

- El notebook se ejecutó completo de principio a fin (reinicio de kernel + ejecución secuencial),
  sin errores y con todas las celdas produciendo salida.
- Cada cifra citada en el notebook y en el README se contrastó contra los datos reales antes de
  aceptarse. Corregimos manualmente las que el asistente había redondeado o arrastrado de una
  versión anterior del análisis.
- `retail_ventas_LIMPIO.csv` se usó únicamente como verificación final, nunca como fuente para
  rellenar valores durante la limpieza.

## 4. Herramientas

Claude (Anthropic), vía interfaz de chat y vía Claude Code en terminal.
