# Informe final de unificación

Fecha de cierre: 27 de julio de 2026  
Rama: `fix/taller-01-cumplimiento-guia`

El trabajo quedó listo en la rama indicada. No se hizo push, merge a `main`, force push ni
reescritura de historia.

## Estado inicial

`git branch --show-current` confirmó `fix/taller-01-cumplimiento-guia`.

El árbol no estaba limpio al iniciar porque los documentos recién suministrados por el docente
aparecían sin seguimiento y con sufijos del navegador: `Taller_Practico_01_Guia (1).md`,
`Taller_Practico_01 (1).pdf`, `README (copy 1).md` y una copia raíz de
`Taller_Practico_01.tex`. Se trataron como insumos de esta solicitud, se revisaron antes de
moverlos y no se eliminó contenido único.

## Tarea 1: verificación contra la guía correcta

La revisión anterior sí había quedado incompleta por tomar el `.tex` como fuente normativa. La
lectura completa de `Taller_Practico_01_Guia.md`, incluidas las Tareas 1 a 5 y la sección 6,
reveló estos puntos:

1. El notebook no identificaba literalmente todos los encabezados de las Tareas 1 a 5 de la guía.
2. La Tarea 3 no justificaba de forma explícita el tratamiento de precios y ratings.
3. La Tarea 4 no incluía las tres visualizaciones distintas sobre el resultado de la limpieza
   propia ni las tablas explícitas de frecuencia y proporción solicitadas.
4. La tabla GIGO no tenía primero los encabezados literales exigidos por la guía.
5. El README tenía una fecha de entrega incorrecta y su árbol no reflejaba todos los archivos
   reales.
6. Faltaba dejar explícito que la guía organiza el notebook mientras el `.tex` es el cuestionario
   separado de las partes 1.1 a 3.A.

Se corrigieron esos seis puntos de forma complementaria. El notebook ahora contiene los
encabezados literales Tarea 1 a Tarea 5, conserva las respuestas del cuestionario por separado,
agrega las justificaciones pendientes, dos tablas categóricas y cuatro visualizaciones basadas en
`analisis`. La tabla GIGO del notebook y el CSV quedaron sincronizados en 10 filas y 6 columnas.

La estructura obligatoria quedó confirmada:

```text
README.md
Taller_Practico_01_Guia.md
data/raw/
data/processed/retail_ventas_PROCESADO.csv
notebooks/taller_practico_01_analisis.ipynb
results/figuras/
results/tabla_diagnostico_gigo.csv
taller_practico/Taller_Practico_01.tex
taller_practico/Taller_Practico_01.pdf
docs/declaracion_uso_IA.md
requirements.txt
```

`src/` es opcional según la guía y no se creó porque el proyecto no tiene módulos fuente que
justifiquen esa carpeta. La copia raíz del `.tex` tenía SHA256
`e8301c749dbe17f1276cf351de3567298c871ac7f632b46061da166f03f663e6`, exactamente igual al
archivo ya versionado en `taller_practico/`; se conservó fuera del repositorio en
`/tmp/Taller_Practico_01_raiz_duplicado_e8301c74.tex`. El PDF se preservó junto al `.tex` y la
plantilla del README se preservó como `docs/README_template_docente.md`.

Commit de esta tarea:

```text
22fa356 fix(repo): rehacer verificacion de estructura contra la guia correcta
```

## Tarea 2: revisión completa de `bbcd825`

La salida íntegra, sin truncar ni resumir, quedó guardada en:

* [`/tmp/bbcd825.diff`](/tmp/bbcd825.diff), 682 líneas, 25.141 bytes, SHA256
  `af7743666d80a8ba17bb1b13ac796bf1f7a5225f4081ca8a95de63136e0ab620`.
* [`/tmp/bbcd825.stat`](/tmp/bbcd825.stat), 8 líneas, 335 bytes, SHA256
  `b2c5191da502b0314aefb2d2eb90c252b52ffe050c019bfdde182ed291b13d80`.
* [`/tmp/bbcd825_verificacion.txt`](/tmp/bbcd825_verificacion.txt), recálculo independiente
  completo contra `data/raw/`.

Salida completa de `git show bbcd825 --stat`:

```text
commit bbcd825b001659cbe2e588b67a36981d1adeff22
Author: AndresVelezR <andresvelezr16@gmail.com>
Date:   Mon Jul 27 19:35:36 2026 -0500

    fix(notebook): corregir comparacion y validar cifras finales

 notebooks/taller_practico_01_analisis.ipynb | 379 +++++++++++++++++-----------
 1 file changed, 238 insertions(+), 141 deletions(-)
```

El recálculo valor por valor, alineado por `transaction_id`, produjo:

```text
store_id            0
comuna              0
date                9
category            0
units_sold         22
unit_price         12
payment_method      0
customer_rating    69
store_lat           6
store_lon           6
```

Por tanto, `customer_rating = 69` es correcto. La diferencia entre el promedio de reseñas y el
promedio de ventas crudas también confirmó:

```text
S01   0.05
S02  -0.18
S03  -0.28
S04  -0.43
S05   0.19
S06   0.08
S07  -0.22
S08   0.13
```

El párrafo actual incluye correctamente S02 entre las tiendas donde las reseñas están por debajo
de ventas y S01 entre aquellas donde están por encima. No se necesitó un commit adicional para
esta tarea.

## Tarea 3: resolución del stash

La salida completa de `git stash show -p stash@{0}` fue vacía. La causa comprobada fue que el
stash contenía únicamente archivos sin seguimiento. La inspección del árbol
`stash@{0}^3` mostró:

```text
241d2a14d592ac1ee6e776bd409421ae0650b936  Taller_Practico_01 (1) (copy 1).tex
241d2a14d592ac1ee6e776bd409421ae0650b936  Taller_Practico_01 (1).tex
241d2a14d592ac1ee6e776bd409421ae0650b936  docs/Taller_Practico_01 (1).tex
46987ba8a6ce6167db15fbd491af5f24ce15b968  notebooks/.ipynb_checkpoints/Copia_de_Retail_01-checkpoint.ipynb
b7b634987dd199f6845082831fa0c4cc340f7e89  notebooks/.ipynb_checkpoints/taller_practico_01_analisis-checkpoint.ipynb
5b18d05fb3c66ee5b06fe281ed18467d9e89b447  notebooks/.~lock.taller_practico_01_analisis.ipynb#
```

Los tres blobs `.tex` son idénticos entre sí y al `.tex` versionado, con SHA256
`e8301c749dbe17f1276cf351de3567298c871ac7f632b46061da166f03f663e6`. Los checkpoints
coinciden exactamente con versiones ya presentes en la historia:

```text
46987ba8a6ce6167db15fbd491af5f24ce15b968  419747b^:notebooks/Copia_de_Retail_01.ipynb
b7b634987dd199f6845082831fa0c4cc340f7e89  8f1f7f6:notebooks/taller_practico_01_analisis.ipynb
```

El archivo de bloqueo tenía 72 bytes y solo contenía metadatos de LibreOffice:

```text
,andres,kali,27.07.2026 17:20,file:///home/andres/.config/libreoffice/4;
```

No había contenido único ni relevante sin versionar. Se ejecutó:

```text
Dropped stash@{0} (1c08dfeb1126671856e0edb95dfc1a1148c672a3)
```

`git stash list` quedó vacío.

## Tarea 4: comparación por contenido desde `origin/main`

El informe íntegro, con la lista de las celdas idénticas, el diff completo de cada celda
modificada y el contenido completo de cada celda nueva, está en
[`/tmp/nb_diff_final.txt`](/tmp/nb_diff_final.txt). Tiene 683 líneas, 43.679 bytes y SHA256
`ea4e5046c80a30ffd5fea1743d02029575ae44f6fd383a3ef12cfe7f7666e54f`.

La comparación usó el par `(tipo de celda, source completo)` como multiconjunto, sin depender del
índice. Los IDs persistentes solo se usaron para enlazar las modificaciones y demostrar que no
hubo eliminaciones.

```text
Celdas originales en origin/main: 53
Celdas actuales: 72
Originales exactamente iguales por contenido: 31
Originales modificadas: 22
Originales eliminadas: 0
Celdas nuevas: 19
Todos los IDs originales persisten: True
```

Desde `a12cf17` se corrigieron la limitación de reseñas y los duplicados, se añadió la comparación
contra la referencia, se documentaron los `review_id` repetidos, se completó la estructura, se
normalizó la redacción, se reescribió la declaración de uso, se corrigió la comparación anulable,
se creó el informe de unificación, se rehízo la revisión contra la guía correcta y se precisó la
afirmación geográfica final. El detalle por commit está al final del informe de `/tmp`.

## Tarea 5: ejecución y verificación final

### Ejecución

El notebook se ejecutó completo y en el sitio con `nbconvert` desde un kernel nuevo:

```text
Celdas de código: 31
Conteos de ejecución: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31
Celdas sin salida: []
Errores: []
```

Todas las cifras de las celdas Markdown se recalcularon sin usar las salidas guardadas. Se
confirmaron, entre otras, 430 filas crudas y 420 eventos finales; 160 reseñas y 157 `review_id`
únicos; 14 ratings de reseñas nulos; 10, 21, 12 y 64 nulos en fecha, unidades, precio y rating de
ventas; 10 pares por `transaction_id`; 2 pares y 4 filas por la llave declarada; 69 diferencias
de `customer_rating`; las frecuencias, proporciones, medidas descriptivas, tabla de contingencia,
ratings por tienda y cifras de la recomendación.

La auditoría detectó una sola imprecisión residual. El texto decía que había ocho ubicaciones
exactas, aunque existen variaciones de coordenadas entre transacciones. La afirmación correcta es
que el mapa agrupa ventas de las ocho tiendas y todas las coordenadas finales son válidas. Se
corrigió y se volvió a ejecutar todo el notebook.

Commit de esa corrección:

```text
c701b6d fix(notebook): corregir afirmacion geografica detectada en verificacion final
```

### Tabla GIGO

```text
notebook_shape (10, 6)
csv_shape (10, 6)
columnas_identicas True
contenido_identico True
filas_csv_incluyendo_encabezado 11
```

También existen `taller_practico/Taller_Practico_01.tex` y
`docs/declaracion_uso_IA.md`. `notebooks/` contiene un único notebook.

### Salidas literales de los cuatro comandos

Comando:

```zsh
git log main..HEAD --format=%B | grep -iE "co-authored|generated with|claude|codex|🤖|gpt"
```

Salida literal, vacía:

```text
```

Código de salida: `1`, que en `grep` significa que no hubo coincidencias.

Comando:

```zsh
grep -nE '\[copie|\[reformulenla|\[accion concreta|\[\.\.\.\]|Escriba aqui|dd/mm/aaaa' README.md
```

Salida literal, vacía:

```text
```

Código de salida: `1`, que en `grep` significa que no hubo coincidencias.

Comando:

```zsh
git diff main..HEAD -- data/raw/
```

Salida literal, vacía:

```text
```

Código de salida: `0`.

Comando:

```zsh
diff <(python3 -c "import csv;print(len(list(csv.reader(open('results/tabla_diagnostico_gigo.csv')))))") <(echo)
```

Salida literal completa:

```text
1c1
< 11
---
> 
```

Código de salida: `1` porque `11`, las 10 filas más el encabezado, difiere de la línea vacía
producida por `echo`.

## Decisiones ambiguas tomadas

1. Los documentos suministrados tenían sufijos de descarga. Se eligió el nombre canónico
   `Taller_Practico_01_Guia.md`, se preservó la plantilla del docente en `docs/` y se conservó el
   PDF junto al `.tex`.
2. La copia raíz del `.tex` era byte por byte igual a la versionada. En vez de mantener dos copias
   dentro del repositorio, se movió a `/tmp`, donde sigue disponible.
3. No se creó `src/` porque la guía la declara opcional y no existe código modular que trasladar.
4. El stash se eliminó únicamente después de comparar blobs y checksums con la historia y el
   archivo versionado.
5. La frase geográfica se corrigió sin alterar datos ni código, porque ocho corresponde al número
   de tiendas, no al número de pares de coordenadas exactos.

## Commits nuevos de esta sesión

```text
22fa356 fix(repo): rehacer verificacion de estructura contra la guia correcta
c701b6d fix(notebook): corregir afirmacion geografica detectada en verificacion final
```

El commit que versiona este informe usa el mensaje
`docs: actualizar informe final de unificacion`; su hash se muestra en el log final entregado al
usuario.

## Pendientes

No quedó ningún hallazgo sin resolver. Los artefactos extensos requeridos permanecen en `/tmp`,
el árbol queda limpio y no se hizo push ni merge.

## Ampliación de trazabilidad solicitada

Esta ampliación responde la revisión cruzada posterior. La auditoría anterior, tanto en
`62cb2fd` como en `a12cf17`, tenía 45 de las 53 celdas originales exactamente iguales a
`origin/main`. El estado actual tiene 31 idénticas. Las 14 que cambiaron se identificaron por el
ID persistente de la celda y se compararon por su `source` completo.

La clasificación comprobada es:

```text
Solo sustitución del guion largo del encabezado por un punto: 9 celdas
Cambio adicional de contenido, rotulación o argumento: 5 celdas
Contenido o argumento eliminado: 0 celdas
```

Las nueve celdas con cambio exclusivo de puntuación son:
`61057651`, `11834b64`, `be8a4685`, `00f6fc48`, `086907da`, `c2e8ba8d`,
`2ed6e702`, `7513f43a` y `77811297`.

Las cinco con cambios adicionales son:

1. `3c92c61a`: añade que la Parte 1 pertenece al cuestionario.
2. `8f5a5f8d`: la rotula como Tarea 2 de la guía y explica su relación con la Parte 2.
3. `58df97ac`: reorganiza y amplía la tabla GIGO con los encabezados de la guía, pilares,
   evidencia y tres hallazgos del JSON.
4. `ecb1b266`: la rotula como Tarea 3 y explicita que la limpieza es reproducible.
5. `7c4ba11a`: aclara que la Parte 3 pertenece al cuestionario.

### Anexo A: diff completo de las 14 celdas

El siguiente bloque es la salida completa, sin truncar, de la comparación antes y después.

```diff
DIFF COMPLETO DE LAS 14 CELDAS
Referencia anterior: a12cf17 y 62cb2fd, ambos con 45/53 celdas originales idénticas.
Referencia normativa de contenido original: origin/main (88f7b83).
Estado actual: HEAD, con 31/53 idénticas, 22 modificadas, 0 eliminadas y 19 nuevas.
Las 14 listadas eran idénticas a origin/main en a12cf17 y ahora difieren.

========================================================================================
1. ID 3c92c61a | CAMBIO ADICIONAL
Además de quitar guiones de puntuación, añade "del cuestionario" y cambia la rotulación de Parte 1.
sha256 antes: 4516bcbb1854f8904d34ead452314d278dd51ffa798c41d1a7ed8bd527d2ab1c
sha256 después: b2bd95f558e20c645450d58aec903153eea7c039322626f04d2b74cafe838da9
----------------------------------------------------------------------------------------
--- origin/main:3c92c61a (ANTES)
+++ HEAD:3c92c61a (DESPUÉS)
@@ -1,7 +1,7 @@
 ---
-## Parte 1 — Análisis estadístico general
+## Parte 1 del cuestionario: Análisis estadístico general
 
-### 1.1 — Taxonomía
+### 1.1. Taxonomía
 
 Se clasifican cinco variables según el significado del dato, no solamente según el tipo que muestra
 Python.

========================================================================================
2. ID 61057651 | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: da670be93e46e3912939d47633c0a71126cfaafe5c4d950e5ecc70d48a52def4
sha256 después: 4f6e0b24dfa67aad77c7481f61f8d7f13c8745df0a607a9faf30c7d973084dcf
----------------------------------------------------------------------------------------
--- origin/main:61057651 (ANTES)
+++ HEAD:61057651 (DESPUÉS)
@@ -1 +1 @@
-### 1.2 — Medidas de tendencia central y dispersión
+### 1.2. Medidas de tendencia central y dispersión

========================================================================================
3. ID 11834b64 | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: ecee97da8f7db0776b022b4177f42735f5abc0757e5202dadd945499a2058d57
sha256 después: 7785369675bb8979b6c285326779f4d13244cc9460ab2e5a7250b4860fdbdffe
----------------------------------------------------------------------------------------
--- origin/main:11834b64 (ANTES)
+++ HEAD:11834b64 (DESPUÉS)
@@ -1 +1 @@
-### 1.3 — Variable cualitativa: categoría
+### 1.3. Variable cualitativa: categoría

========================================================================================
4. ID be8a4685 | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: 7654b28bf66fd5b2c3740921dd12c985bf50692b4a28ab112fad435623e55431
sha256 después: c46b778349db2c898c0fb96d8f5016cdc06a1f81739745426adfd36984b0dc0d
----------------------------------------------------------------------------------------
--- origin/main:be8a4685 (ANTES)
+++ HEAD:be8a4685 (DESPUÉS)
@@ -1 +1 @@
-### 1.4 — Forma de la distribución y valores atípicos
+### 1.4. Forma de la distribución y valores atípicos

========================================================================================
5. ID 00f6fc48 | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: 011d4434dd3cb84481f808d63803058a14a4b21b229d7a39e50dc80c0bd4ffd9
sha256 después: 7f96665893984233f8bb12903416ac695b4bd6825e6ba44de1527c40535a76a2
----------------------------------------------------------------------------------------
--- origin/main:00f6fc48 (ANTES)
+++ HEAD:00f6fc48 (DESPUÉS)
@@ -1 +1 @@
-### 1.5 — ¿Por qué la misma media puede exigir decisiones distintas?
+### 1.5. ¿Por qué la misma media puede exigir decisiones distintas?

========================================================================================
6. ID 8f5a5f8d | CAMBIO ADICIONAL
Renombra la sección como Tarea 2 de la guía y explica que también responde la Parte 2 del cuestionario.
sha256 antes: 1b70b17fee1f3ee932b6eb5ca91f127a095db14367132c8628259f99a19c2ea0
sha256 después: 79ee2218da2e1993d34cfb0b0f6eacc5df0d6db5f3b98f6da7383fc8cd45f594
----------------------------------------------------------------------------------------
--- origin/main:8f5a5f8d (ANTES)
+++ HEAD:8f5a5f8d (DESPUÉS)
@@ -1,4 +1,5 @@
 ---
-## Parte 2 — Diagnóstico y transformación del archivo contaminado
+## Tarea 2: Diagnóstico GIGO sobre el archivo contaminado
 
-Primero se diagnostica; todavía no se corrigen los datos.
+Esta sección también responde la Parte 2 del cuestionario `.tex`. Primero se diagnostica; todavía
+no se corrigen los datos.

========================================================================================
7. ID 58df97ac | CAMBIO ADICIONAL
Amplía y reorganiza la tabla GIGO: encabezados de la guía, pilares, evidencia y tres hallazgos del JSON.
sha256 antes: 2979508a545e73e2dfa9505de91d2e97a3226900ce74eb55a9ab4696eb0a0a13
sha256 después: 0c754baf0c056209567766d71cc04197907af59f63a57a331a67e240dffd9a2c
----------------------------------------------------------------------------------------
--- origin/main:58df97ac (ANTES)
+++ HEAD:58df97ac (DESPUÉS)
@@ -1,13 +1,16 @@
-### 2.1 — Diagnóstico de calidad
+### 2.1. Diagnóstico de calidad
 
-| Problema detectado | Columnas | Detección con pandas | Riesgo para el negocio |
-|---|---|---|---|
-| Faltantes: 10 fechas, 21 unidades, 12 precios y 64 ratings | `date`, `units_sold`, `unit_price`, `customer_rating` | `isna().sum()` | Subestima ventas, ingresos o insatisfacción. |
-| 1 duplicado exacto adicional y 10 IDs repetidos | `transaction_id` y demás columnas | `duplicated()` y `duplicated(subset=...)` | Infla rotación e ingresos. |
-| 19 textos para 4 categorías reales | `category` | `unique()` / `value_counts()` | Fragmenta una categoría en grupos falsos. |
-| Fechas ISO, con `/`, con `-`, texto y nulos | `date` | patrones de texto y `to_datetime(..., errors="coerce")` | Asigna ventas al día o mes equivocado. |
-| 8 cantidades negativas y 6 ratings fuera de 1–5 | `units_sold`, `customer_rating` | `between()` y comparaciones | Distorsiona demanda y satisfacción. |
-| 5 precios con dos ceros adicionales | `unit_price` | regla comercial y revisión por categoría | Infla el ingreso y la dispersión. |
-| 6 coordenadas en cero o fuera de Medellín | `store_lat`, `store_lon` | `between()` para latitud y longitud | Ubica tiendas en zonas incorrectas. |
+| Problema detectado | Columna(s) afectada(s) | Método de detección en pandas | ¿Por qué es un riesgo para la decisión de negocio? | Pilar GIGO | Evidencia |
+|---|---|---|---|---|---|
+| Valores faltantes | date, units_sold, unit_price, customer_rating | df.isnull().sum() | Subestima ventas, ingresos o insatisfaccion. | Completitud | date:10, units_sold:21, unit_price:12, customer_rating:64 nulos |
+| Duplicados de evento de negocio | transaction_id y demas columnas | df['transaction_id'].duplicated().sum() | Infla rotacion e ingresos. | Unicidad | 10 transaction_id repetidos + 1 fila duplicada exacta |
+| Etiquetas categoricas inconsistentes | category | df['category'].unique() | Fragmenta una categoria en grupos falsos. | Consistencia | 19 valores unicos en 'category' para 4 categorias reales |
+| Formatos de fecha mixtos | date | patrones de texto y to_datetime(..., errors='coerce') | Asigna ventas al dia o mes equivocado. | Consistencia | date mezcla ISO, con '/', con '-', texto y nulos |
+| Valores imposibles | units_sold, customer_rating | between() y comparaciones | Distorsiona demanda y satisfaccion. | Validez | 8 cantidades negativas y 6 ratings fuera de 1-5 |
+| Precios inflados por error de digitacion | unit_price | regla comercial y revision por categoria | Infla el ingreso y la dispersion. | Validez | 5 precios con dos ceros adicionales (>= 100.000 COP) |
+| Georreferenciacion fuera de rango | store_lat, store_lon | between() para latitud y longitud | Ubica tiendas en zonas incorrectas. | Georreferenciacion | 6 coordenadas en cero o fuera de Medellin |
+| Columna sentiment 100% nula | sentiment | df_resenas['sentiment'].isna().sum() | Columna inservible tal como esta: no aporta analisis de sentimiento sin procesar el texto. | Completitud | 160/160 valores nulos en df_resenas['sentiment'] |
+| Rating de resenas con nulos | rating | df_resenas['rating'].isna().sum() | Sesga el rating promedio por tienda si se ignoran sin marcarlos. | Completitud | 14/160 resenas sin rating numerico |
+| review_id repetido con contenido distinto | review_id | duplicated() sobre review_id | dos resenas distintas comparten identificador; agregarlas por review_id fusionaria eventos que no son el mismo | Unicidad | 160 registros y 157 review_id unicos; R0057, R0098 y R0150 aparecen dos veces con tienda, fecha y texto distintos |
 
 El diagnóstico cubre completitud, unicidad y consistencia antes de modificar el archivo.

========================================================================================
8. ID 086907da | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: e33a366caf944d767a92abe1f030c507e3d259ee3681a61f861aef47dc7def1a
sha256 después: 9ed3510b046488df1c13f010819e2231987af2751b2ca02c3c33adadcb75e880
----------------------------------------------------------------------------------------
--- origin/main:086907da (ANTES)
+++ HEAD:086907da (DESPUÉS)
@@ -1 +1 @@
-### 2.2 — Conversión de fechas
+### 2.2. Conversión de fechas

========================================================================================
9. ID c2e8ba8d | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: 14e43b38700c1910c5602557370bc714cc5c58902faf4912f7b921836bcff009
sha256 después: 4636e5f2ff82a20501d37c4e5d799ea42eb584a036dfca45bf2f3b610fd72d99
----------------------------------------------------------------------------------------
--- origin/main:c2e8ba8d (ANTES)
+++ HEAD:c2e8ba8d (DESPUÉS)
@@ -1 +1 @@
-### 2.3 — Estandarización de la categoría
+### 2.3. Estandarización de la categoría

========================================================================================
10. ID 2ed6e702 | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: df5c193c8c9dbc3ac09aacb4580a4511ac318c8a79f32a846b87e88fa4bb70fa
sha256 después: 34f7884f0674c599059f7cdab306a087b2b4126f4f7092f59ea1d32a6aea5830
----------------------------------------------------------------------------------------
--- origin/main:2ed6e702 (ANTES)
+++ HEAD:2ed6e702 (DESPUÉS)
@@ -1 +1 @@
-### 2.4 — Georreferenciación
+### 2.4. Georreferenciación

========================================================================================
11. ID 7513f43a | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: 24d6ef2508a5b2115fb8ca28a27fc4849588a51d51fbf7fa23ad29f75e3cf6b4
sha256 después: 93dbc2200df4b45f46a7d2219a35c2f60dfb740cbc5ff795c7f743b7391af0dc
----------------------------------------------------------------------------------------
--- origin/main:7513f43a (ANTES)
+++ HEAD:7513f43a (DESPUÉS)
@@ -1 +1 @@
-### 2.5 — Imputación y valores imposibles
+### 2.5. Imputación y valores imposibles

========================================================================================
12. ID 77811297 | SOLO PUNTUACIÓN
Sustituye el guion largo del encabezado por punto.
sha256 antes: 547444ca2ee590d7993ea5fbb2a035f983bde9b000d735b77887fd1670970c1b
sha256 después: 78c20b5d19ca9c07acbc8ead3d21538f3d882b6312eb88b8d561d51c94f1b75a
----------------------------------------------------------------------------------------
--- origin/main:77811297 (ANTES)
+++ HEAD:77811297 (DESPUÉS)
@@ -1 +1 @@
-### 2.6 — Duplicados y llave de negocio
+### 2.6. Duplicados y llave de negocio

========================================================================================
13. ID ecb1b266 | CAMBIO ADICIONAL
Renombra la sección como Tarea 3 de la guía y añade que el bloque es reproducible.
sha256 antes: b1a7f3d673166856118a3fd999138c9571bbb8f38610b931379e9f76e2aa5385
sha256 después: a86cb6d7a5c9533dac2fe6c6eabfeec970d79fe6a2253418b6d62e9b0f79b361
----------------------------------------------------------------------------------------
--- origin/main:ecb1b266 (ANTES)
+++ HEAD:ecb1b266 (DESPUÉS)
@@ -1,5 +1,5 @@
 ---
-## 3. Limpieza reproducible
+## Tarea 3: Transformación y limpieza con pandas
 
-El siguiente bloque reúne las decisiones anteriores. El archivo limpio de referencia no se usa para
-rellenar valores; solamente se contrasta al final.
+El siguiente bloque reúne las decisiones anteriores de forma reproducible. El archivo limpio de
+referencia no se usa para rellenar valores; solamente se contrasta al final.

========================================================================================
14. ID 7c4ba11a | CAMBIO ADICIONAL
Además de quitar el guion, aclara que Parte 3 pertenece al cuestionario.
sha256 antes: 718d34916303e5f72e7e3d479145375882e0364a4ff576814af7e039b647f14b
sha256 después: 70561fb43fa96b85e92d658956ad2175eb23e71751c68140753906cd03b88dbe
----------------------------------------------------------------------------------------
--- origin/main:7c4ba11a (ANTES)
+++ HEAD:7c4ba11a (DESPUÉS)
@@ -1,4 +1,4 @@
 ---
-## Parte 3 — Interpretación y decisión para Retail
+## Parte 3 del cuestionario: Interpretación y decisión para Retail
 
 ### Resumen por categoría

========================================================================================
RESUMEN DE CLASIFICACIÓN
Solo puntuación: 9
Cambio adicional: 5
Contenido o argumento eliminado: 0
```

### Anexo B: corrección geográfica `c701b6d`

El `git show c701b6d` completo también está en
[`/tmp/c701b6d.diff`](/tmp/c701b6d.diff), con 484 líneas, 19.382 bytes y SHA256
`3accf9faca22c603764dd2359c404e19b196a1df2b2b9b961acfb991009e6c3a`.

El diff semántico exacto y la verificación independiente son:

```text
DIFF SEMÁNTICO EXACTO DE c701b6d
Celda 69, ID dbd9e0d5, tipo markdown
--- c701b6d^ (ANTES)
+++ c701b6d (DESPUÉS)
@@ -1,7 +1,7 @@
 **Conclusiones de las visualizaciones.** La barra por categoría confirma que `Pan` tiene la mayor
 rotación promedio. La barra por tienda muestra que S07 y S05 tienen los ratings promedio más bajos.
 El histograma confirma la asimetría positiva del precio unitario, por lo que la mediana es el centro
-más representativo. El mapa de puntos agrupa las ventas en ocho ubicaciones válidas de Medellín y
+más representativo. El mapa de puntos agrupa las ventas de las ocho tiendas con coordenadas válidas de Medellín y
 permite comprobar que no permanecen coordenadas en cero o fuera del rango definido.
 
 **Nota de coherencia con la Prioridad 2.** Esta sección usa `df` (el resultado propio de la Tarea 3),

VERIFICACIÓN INDEPENDIENTE CONTRA data/raw/

CONTAMINADO CRUDO
filas: 430
store_id únicos: 8
store_id: S01,S02,S03,S04,S05,S06,S07,S08
pares de coordenadas exactos únicos: 418
filas con coordenadas inválidas: 6
pares exactos únicos por tienda:
store_id
S01    51
S02    48
S03    57
S04    45
S05    55
S06    54
S07    40
S08    70

PROCESADO POR EL NOTEBOOK
filas: 420
store_id únicos: 8
store_id: S01,S02,S03,S04,S05,S06,S07,S08
pares de coordenadas exactos únicos: 419
filas con coordenadas inválidas: 0
pares exactos únicos por tienda:
store_id
S01    51
S02    48
S03    57
S04    44
S05    55
S06    54
S07    40
S08    70

CONCLUSIÓN
La frase anterior era falsa si "ubicaciones" significaba pares exactos de coordenadas: hay 418 pares crudos y 419 procesados, no 8.
La frase nueva es correcta: hay exactamente 8 tiendas y, después del proceso del notebook, 0 filas con coordenadas inválidas.
```

La frase anterior era incorrecta si “ubicaciones” significaba pares exactos de coordenadas:
el archivo contaminado contiene 418 pares exactos distintos y el procesado 419. La frase nueva
es correcta porque existen exactamente ocho `store_id` y, después de aplicar el proceso del
notebook, ninguna fila conserva coordenadas fuera del rango válido.

### Anexo C: salidas literales verificables de la Tarea 5

Se guardó `stdout` por separado para evitar que una salida vacía vuelva a confundirse con una
autoevaluación. Los resultados binarios son:

```text
0 bytes  e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855  /tmp/task5_cmd1.stdout
0 bytes  e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855  /tmp/task5_cmd2.stdout
0 bytes  e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855  /tmp/task5_cmd3.stdout
16 bytes 4fcf212679bf1a7012596b8f13ebf39e2ab9a2dc7ef3cb910ab90ee266d0c9b6  /tmp/task5_cmd4.stdout
```

Transcripción textual literal:

```text
$ git log main..HEAD --format=%B | grep -iE "co-authored|generated with|claude|codex|🤖|gpt"
$
```

No existe ninguna línea entre ambos prompts. Código de salida: `1`.

```text
$ grep -nE '\[copie|\[reformulenla|\[accion concreta|\[\.\.\.\]|Escriba aqui|dd/mm/aaaa' README.md
$
```

No existe ninguna línea entre ambos prompts. Código de salida: `1`.

```text
$ git diff main..HEAD -- data/raw/
$
```

No existe ninguna línea entre ambos prompts. Código de salida: `0`.

```text
$ diff <(python3 -c "import csv;print(len(list(csv.reader(open('results/tabla_diagnostico_gigo.csv')))))") <(echo)
1c1
< 11
---
> 
$
```

Código de salida: `1`. La representación hexadecimal exacta de esa salida es:

```text
00000000: 31 63 31 0a 3c 20 31 31 0a 2d 2d 2d 0a 3e 20 0a  1c1.< 11.---.> .
```

### Anexo D: evidencia recuperable del stash

El drop quitó la referencia de `git stash list`, pero el objeto
`1c08dfeb1126671856e0edb95dfc1a1148c672a3` aún es direccionable directamente. Por tanto, la
decisión todavía puede comprobarse de forma independiente. La evidencia completa es:

```text
EVIDENCIA RECUPERABLE DEL STASH DESCARTADO
Objeto: 1c08dfeb1126671856e0edb95dfc1a1148c672a3
Aunque git stash list está vacío, el objeto todavía es direccionable por hash.

1. git stash list

2. git cat-file -t 1c08dfeb1126671856e0edb95dfc1a1148c672a3
commit

3. git show -s --format=fuller 1c08dfeb1126671856e0edb95dfc1a1148c672a3
commit 1c08dfeb1126671856e0edb95dfc1a1148c672a3
Merge: 62cb2fd 33fa8c6 6e3bb2f
Author:     AndresVelezR <andresvelezr16@gmail.com>
AuthorDate: Mon Jul 27 18:49:27 2026 -0500
Commit:     AndresVelezR <andresvelezr16@gmail.com>
CommitDate: Mon Jul 27 18:49:27 2026 -0500

    On fix/taller-01-cumplimiento-guia: respaldo archivos sin seguimiento previos a taller 01

4. git stash show -p 1c08dfeb1126671856e0edb95dfc1a1148c672a3
<<<INICIO_SALIDA_LITERAL>>>
<<<FIN_SALIDA_LITERAL>>> (vacía; el stash no modificaba archivos rastreados)

5. git ls-tree -r 1c08dfeb1126671856e0edb95dfc1a1148c672a3^3
100644 blob 241d2a14d592ac1ee6e776bd409421ae0650b936	Taller_Practico_01 (1) (copy 1).tex
100644 blob 241d2a14d592ac1ee6e776bd409421ae0650b936	Taller_Practico_01 (1).tex
100644 blob 241d2a14d592ac1ee6e776bd409421ae0650b936	docs/Taller_Practico_01 (1).tex
100644 blob 46987ba8a6ce6167db15fbd491af5f24ce15b968	notebooks/.ipynb_checkpoints/Copia_de_Retail_01-checkpoint.ipynb
100644 blob b7b634987dd199f6845082831fa0c4cc340f7e89	notebooks/.ipynb_checkpoints/taller_practico_01_analisis-checkpoint.ipynb
100644 blob 5b18d05fb3c66ee5b06fe281ed18467d9e89b447	notebooks/.~lock.taller_practico_01_analisis.ipynb#

6. SHA256 de los tres .tex del stash y del .tex versionado
e8301c749dbe17f1276cf351de3567298c871ac7f632b46061da166f03f663e6  Taller_Practico_01 (1) (copy 1).tex
e8301c749dbe17f1276cf351de3567298c871ac7f632b46061da166f03f663e6  Taller_Practico_01 (1).tex
e8301c749dbe17f1276cf351de3567298c871ac7f632b46061da166f03f663e6  docs/Taller_Practico_01 (1).tex
e8301c749dbe17f1276cf351de3567298c871ac7f632b46061da166f03f663e6  taller_practico/Taller_Practico_01.tex

7. Identidad de blobs de checkpoints con versiones ya registradas
46987ba8a6ce6167db15fbd491af5f24ce15b968  stash checkpoint Copia_de_Retail_01
46987ba8a6ce6167db15fbd491af5f24ce15b968  historia 419747b^:notebooks/Copia_de_Retail_01.ipynb
b7b634987dd199f6845082831fa0c4cc340f7e89  stash checkpoint taller_practico_01_analisis
b7b634987dd199f6845082831fa0c4cc340f7e89  historia 8f1f7f6:notebooks/taller_practico_01_analisis.ipynb

8. Tamaño y contenido literal hexadecimal del archivo de bloqueo
72
00000000: 2c 61 6e 64 72 65 73 2c 6b 61 6c 69 2c 32 37 2e  ,andres,kali,27.
00000010: 30 37 2e 32 30 32 36 20 31 37 3a 32 30 2c 66 69  07.2026 17:20,fi
00000020: 6c 65 3a 2f 2f 2f 68 6f 6d 65 2f 61 6e 64 72 65  le:///home/andre
00000030: 73 2f 2e 63 6f 6e 66 69 67 2f 6c 69 62 72 65 6f  s/.config/libreo
00000040: 66 66 69 63 65 2f 34 3b                          ffice/4;

CONCLUSIÓN
Los .tex eran copias byte por byte del archivo versionado; ambos notebooks eran checkpoints byte por byte de versiones ya registradas; el último archivo era solo un bloqueo de LibreOffice de 72 bytes. No había contenido único.
```
