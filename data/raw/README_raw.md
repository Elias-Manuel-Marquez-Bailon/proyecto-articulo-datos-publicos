# data/raw — Datos originales (no modificables)

Este directorio debe contener el archivo original del ITER 2020.

## Cómo descargarlo

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
- Este contenido NO se sube al repositorio. Ver `.gitignore`.

Regla del proyecto: nunca modificar los archivos de `data/raw/`; las transformaciones se guardan en `data/processed/`.
