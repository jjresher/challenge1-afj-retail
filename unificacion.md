# Informe de unificación

Trabajo terminado en `fix/taller-01-cumplimiento-guia`. Árbol limpio, sin push ni merge a `main`.

## Commits nuevos

```text
a12cf17 fix(notebook): confirmar correccion de limitacion de resenas y conteo de duplicados
979a356 feat(notebook): agregar comparacion columna por columna contra el archivo limpio de referencia
235dde6 feat(notebook): documentar duplicados de review_id en reseñas_clientes.json
b217d81 fix(repo): completar estructura y placeholders pendientes
e8e8431 docs(redaccion): eliminar guiones usados como puntuacion en celdas markdown y documentos
61b700d docs: reescribir declaracion de uso de IA distinguiendo analisis del equipo y apoyo operativo
bbcd825 fix(notebook): corregir comparacion y validar cifras finales
```

## Verificación de la Tarea 7

1. `notebooks/taller_practico_01_analisis.ipynb` fue ejecutado desde un kernel nuevo:

   - 31 celdas de código ejecutadas secuencialmente.
   - Ninguna celda sin ejecutar.
   - Todas produjeron salida.
   - Cero errores.

2. La auditoría independiente contra `data/raw/` fue aprobada:

   - Se corrigió el conteo de la llave declarada: 2 pares frente a 10 por `transaction_id`.
   - Se corrigió la comparación anulable: `customer_rating` tiene 69 diferencias, no cero.
   - El párrafo de ratings ahora incluye correctamente S02 y S01.
   - No se encontraron otras discrepancias numéricas.

3. Verificaciones textuales:

   - La búsqueda de atribuciones prohibidas en commits produjo una salida vacía.
   - La búsqueda de placeholders en el README produjo una salida vacía.
   - El diff de `data/raw/` frente a `main` está vacío.
   - Las cuatro coincidencias restantes de la búsqueda de guiones son operadores matemáticos en código.

4. `results/tabla_diagnostico_gigo.csv` y la tabla del notebook:

   - Tienen 10 filas y 6 columnas.
   - Tienen el mismo orden de columnas.
   - Tienen contenido idéntico.

5. Existencia confirmada:

   - `taller_practico/Taller_Practico_01.tex`
   - `docs/declaracion_uso_IA.md`

## Decisiones tomadas

- El árbol comenzó con copias `.tex`, checkpoints y un archivo de bloqueo sin seguimiento. Eran copias exactas del `.tex` ya versionado. Se preservaron reversiblemente en `stash@{0}` con el nombre `respaldo archivos sin seguimiento previos a taller 01`.
- `Taller_Practico_01_Guia.md` no existe en el repositorio. Se usó el `.tex` original versionado como fuente de la guía.
- Las tablas GIGO estaban previamente desalineadas. Se conservó toda la información correcta, se añadió `columnas` y se sincronizaron ambos artefactos sin eliminar hallazgos.
- En `customer_rating`, la limpieza propia conserva nulos y no afirma una imputación inexistente. La interpretación explica la diferencia frente al archivo de referencia.

## Pendientes

No quedó nada sin resolver. No se hizo push ni merge a `main`.
