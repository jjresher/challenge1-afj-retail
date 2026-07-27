# Taller Práctico 01 — afj

**Curso:** Fundamentos en Ciencia de Datos — Maestría en Ciencia de Datos y Analítica, EAFIT

**Conjunto de datos elegido:** A - Retail

**Fecha límite de entrega:** Lunes 27 de julio de 2026

**Fecha de entrega real:** Lunes 27 de julio de 2026

**Integrantes del equipo:**

| Nombre completo | Cédula         |
| --------------- | -------------- |
| Juan Jose Restrepo      | 1193082063 |
| Luis Felipe Quesada      | 1005755239 |
| Andrés Vélez Rendón      | 1001371042 |

---

## 1. Resumen ejecutivo (máx. 8 líneas)

> El equipo analizó 420 transacciones de venta en 8 tiendas de Medellín para identificar qué
> categoría y qué tienda concentran mayor riesgo de perder ventas por falta de inventario o mal
> servicio. Tras limpiar duplicados, fechas mixtas, categorías inconsistentes, precios con error
> de digitación y coordenadas fuera de rango, y cruzar las ventas con las reseñas de clientes
> (JSON), encontramos que `Pan` tiene la mayor rotación por transacción, pero las tiendas S07
> (Aranjuez) y S05 (Envigado) tienen el rating promedio más bajo, con "el local estaba
> desordenado" como la queja más repetida en S07. Recomendamos un piloto de reposición frecuente
> de Pan en S07 y S05 junto con una revisión operativa del servicio, sin descuidar el
> abastecimiento de `Pasteles` por ser la categoría de mayor ingreso total.

## 2. Pregunta de negocio

- **Pregunta ancla del conjunto de datos:** ¿Qué categoría de producto y qué tienda presentan
  mayor riesgo de perder ventas o clientes por falta de inventario o servicio deficiente?
- **Pregunta específica que el equipo decidió responder:** dado el rating promedio y la queja más
  frecuente de cada tienda, ¿cuál tienda tiene mayor probabilidad de estar perdiendo clientes por
  un problema operativo (no de inventario), y por lo tanto debería intervenirse primero?

## 3. Estructura del repositorio

```
.
├── README.md
├── data/
│   ├── raw/                  # datos originales (sin modificar)
│   └── processed/            # datos ya limpios, generados por el notebook
├── notebooks/
│   └── taller_practico_01_analisis.ipynb
├── src/                      # funciones auxiliares (opcional)
├── results/
│   ├── figuras/
│   └── tabla_diagnostico_gigo.csv
├── taller_practico/
│   └── Taller_Practico_01.tex   # enunciado recibido (respuestas dentro del notebook)
└── docs/
    └── declaracion_uso_IA.md
```

## 4. Cómo reproducir el análisis (Solamente vía terminal)

```bash
# 1. Clonar el repositorio
git clone https://github.com/jjresher/challenge1-afj-retail.git
cd challenge1-afj-retail

# 2. Crear entorno e instalar dependencias
pip install -r requirements.txt

# 3. Ejecutar el notebook de inicio a fin
jupyter notebook notebooks/taller_practico_01_analisis.ipynb
```

## 5. Principales hallazgos

| #   | Hallazgo | Evidencia (tabla/figura) |
| --- | -------- | ------------------------ |
| 1   | `Pan` es la categoría de mayor rotación (4,08 unidades/transacción), pero `Pasteles` genera el mayor ingreso total | `resumen_categoria`, Tarea 4 / `results/figuras/resumen_categoria_tienda.jpg` |
| 2   | S07 (Aranjuez) y S05 (Envigado) tienen el rating promedio más bajo (3,77 y 3,82) | `resumen_tienda`, Tarea 4 / `results/figuras/resumen_categoria_tienda.jpg` |
| 3   | El rating de las reseñas y el de las ventas no siempre coinciden por tienda (hasta 0,43 de diferencia); en S07 la queja más común es "el local estaba desordenado" (5 de 27 reseñas) | Cruce `reseñas_clientes.json` × ventas por `store_id`, Tarea 1 |

## 6. Problemas de calidad de datos encontrados (resumen GIGO)

| Problema | Estrategia de corrección | Justificación |
| -------- | ------------------------ | ------------- |
| Duplicados de evento de negocio | Conservar la fila más completa y usar `transaction_id` como llave práctica | La contaminación alteró justamente los campos de la llave de negocio declarada en 2.6 |
| Formatos de fecha mixtos (ISO/US/texto) | `pd.to_datetime` con parsing condicional y `errors="coerce"` | Evita detener el proceso; lo no interpretable queda nulo en vez de adivinarse |
| Precios con dos ceros de más | Dividir entre 100 solo si el resultado cae en rango comercial | Corrige el error de digitación sin alterar precios que ya eran válidos |

*(Tabla completa en `results/tabla_diagnostico_gigo.csv`)*

## 7. Decisión recomendada

- **Recomendación:** piloto de reposición frecuente de Pan en S07 y S05, junto con una revisión
  operativa del servicio (orden, limpieza, atención) en esas dos tiendas.
- **Costo de un Falso Positivo:** intervenir o aumentar inventario donde no era necesario genera
  costo operativo, capital inmovilizado y merma.
- **Costo de un Falso Negativo:** no intervenir donde sí existe el problema causa quiebres, ventas
  perdidas y deterioro de la experiencia del cliente.
- **Limitación principal de los datos que persiste tras la limpieza:** no hay costo, margen,
  inventario disponible ni hora de la venta; el texto de las reseñas ayuda a explicar el rating,
  pero solo cubre 160 reseñas repartidas de forma desigual entre tiendas.

## 8. Declaración de uso de Inteligencia Artificial

Ver `docs/declaracion_uso_IA.md`. Resumen: se usó IA generativa para la organización inicial del
notebook y la sintaxis de pandas/matplotlib; la elección de estrategias de imputación, la llave de
deduplicación y la interpretación de los resultados fueron realizadas y validadas por el equipo.
