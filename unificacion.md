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
