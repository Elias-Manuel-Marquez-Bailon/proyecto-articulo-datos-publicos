# data/raw — Datos originales (no modificables)

Este directorio debe contener el archivo original del ITER 2020 y la base municipal de
marginación de CONAPO 2020.

## 1) ITER 2020 (INEGI) — fuente principal

Opción A (enlace directo, ~35 MB comprimidos; se extrae un CSV nacional de ~143 MB):
https://www.inegi.org.mx/contenidos/programas/ccpv/2020/datosabiertos/iter/iter_00_cpv2020_csv.zip

Opción B: desde la página oficial del Censo 2020 → "Datos abiertos":
https://www.inegi.org.mx/programas/ccpv/2020/default.html

## Contenido esperado

- `iter_00_cpv2020_csv.zip`: descarga original del ITER 2020 (no modificable).
- `iter_00_cpv2020/`: contenido extraído del zip:
  - `conjunto_de_datos/conjunto_de_datos_iter_00CSV20.csv` (datos nacionales, encoding UTF-8 con BOM);
  - `diccionario_datos/diccionario_datos_iter_00CSV20.csv`;
  - `metadatos/metadatos_iter_00_cpv2020.txt`.
- `IMM_2020.xls`: base municipal del Índice de Marginación 2020 (CONAPO), usada en la Parte 21
  como fuente externa de comparación (~1.6 MB). Descarga directa:
  https://conapo.segob.gob.mx/work/models/CONAPO/Datos_Abiertos/Municipio/IMM_2020.xls
  (página oficial: https://www.gob.mx/conapo/documentos/indices-de-marginacion-2020-284372)
- Este contenido NO se sube al repositorio. Ver `.gitignore`.

Regla del proyecto: nunca modificar los archivos de `data/raw/`; las transformaciones se guardan en `data/processed/`.
