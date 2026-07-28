# Declaración de uso de Inteligencia Artificial

**Curso:** Fundamentos en Ciencia de Datos de la Maestría en Ciencia de Datos y Analítica, EAFIT
**Taller:** Taller Práctico 01 (Dataset A: Retail)
**Equipo:** Juan José Restrepo, Luis Felipe Quesada, Andrés Vélez Rendón

El equipo utilizó apoyo de IA generativa dentro de los límites definidos por el Pacto Pedagógico.
Los tres integrantes revisaron el contenido analítico, comprenden las decisiones adoptadas y
pueden defender tanto los métodos como las conclusiones.

## Análisis e interpretación

Las siguientes decisiones y conclusiones corresponden al análisis del equipo:

- La pregunta de negocio busca identificar qué categoría y qué tienda presentan mayor riesgo de
  perder ventas o clientes por falta de inventario o por un servicio deficiente.
- Los criterios de calidad abarcan completitud, unicidad, consistencia y validez. El equipo
  comprobó fechas convertibles, categorías reconocidas, unidades enteras mayores que cero,
  ratings entre 1 y 5, precios dentro del rango comercial y coordenadas compatibles con Medellín.
- La estrategia de imputación usa la mediana de la categoría para `units_sold` y `unit_price`, y
  la mediana de cada `store_id` para las coordenadas. Las fechas sin evidencia y los valores
  faltantes de `customer_rating` se conservan como nulos para no inventar información.
- La llave de negocio propuesta es `store_id + date + category + unit_price`. En el archivo crudo,
  esa llave detecta 2 pares y `transaction_id` detecta 10. Como la contaminación modificó fechas,
  categorías o precios dentro de ocho pares, el equipo eligió `transaction_id` como llave práctica
  para este conjunto de datos y conservó la fila más completa de cada duplicado.
- La reflexión de la Tarea 1 concluye que convertir y agregar una fuente semiestructurada puede
  conservar el promedio numérico, pero pierde la causa cualitativa que vive en `text`. Las reseñas
  permiten formular hipótesis por tienda, aunque no están vinculadas con una venta específica.
- La discrepancia entre el rating de las reseñas y el rating de las ventas no es un error de
  carga. Son instrumentos distintos y pueden medir momentos diferentes de la experiencia del
  cliente, por lo que toda conclusión debe identificar la fuente utilizada.
- La tabla de contingencia muestra que la distribución del rating cambia según la categoría. En
  `Pan`, `Pasteles` y `Snacks` predomina el rating 4, mientras `Bebidas` concentra su mayor
  proporción en el rating 5. Un solo promedio por tienda oculta estas diferencias.
- El análisis descriptivo recupera 420 eventos únicos. `Pan` presenta la mayor rotación promedio,
  con 4,08 unidades por transacción, y `Pasteles` aporta el mayor ingreso total. S07 y S05 tienen
  los ratings promedio más bajos, con 3,77 y 3,82 respectivamente, aunque la diferencia entre
  ambas tiendas es pequeña y exige revisar las dos.
- La hipótesis revisada sobre S07 se apoya en el texto de las reseñas. La queja más frecuente es
  que el local estaba desordenado, con 5 menciones entre 27 reseñas. Por eso el equipo interpreta
  que existe un problema operativo de orden, limpieza o atención y no solamente un posible
  problema de inventario.
- La recomendación final es realizar un piloto de reposición frecuente de `Pan` en S07 y S05,
  acompañado de una revisión operativa del servicio, y proteger el abastecimiento de `Pasteles`
  por su aporte al ingreso. El seguimiento debe medir quiebres, merma y ratings durante cuatro
  semanas.

## Apoyo operativo de IA

El apoyo de IA se limitó a tareas mecánicas:

- Consulta de sintaxis de `pandas`, `matplotlib` y `seaborn`.
- Organización de secciones y celdas del notebook.
- Formato inicial de tablas y visualizaciones.
- Redacción inicial de párrafos a partir de argumentos definidos previamente por el equipo.

## Validación

El notebook se ejecuta de principio a fin tras reiniciar el kernel, sin errores. Todas las cifras
citadas se contrastaron contra los datos crudos, y el archivo limpio de referencia se utilizó
solamente para verificar el resultado propio.
