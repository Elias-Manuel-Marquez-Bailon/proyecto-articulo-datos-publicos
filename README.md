# Segmentación de los municipios de Morelos según condiciones de vivienda, servicios y conectividad mediante KMeans

Proyecto final de la materia **Extracción de Conocimiento en Bases de Datos**: análisis no supervisado con datos públicos reales (INEGI Censo 2020 / ITER) para agrupar municipios con condiciones semejantes.

## Integrantes

- Gonzaga Castañeda Cristian Amauri
- Portilla Palestina Viridiana
- Chavez Martinez Adrian Uxue
- Marquez Bailon Elias Manuel

**Grupo:** 9°A — IDGS (Ingeniería en Desarrollo y Gestión de Software)

## Pregunta guía

¿Qué municipios de Morelos presentan características similares en sus condiciones de vivienda, acceso a servicios y conectividad?

## Fuente de datos

- **Principal:** INEGI — Censo de Población y Vivienda 2020, Principales Resultados por Localidad (ITER). <https://www.inegi.org.mx/programas/ccpv/2020/default.html>
- **Validación externa:** CONAPO — Índices de Marginación 2020. <https://www.gob.mx/conapo/documentos/indices-de-marginacion-2020-284372>

## Descripción del dataset

El ITER 2020 contiene indicadores de población y vivienda por localidad y municipio. Se filtran los registros municipales de Morelos (entidad 17, `LOC == "0000"`), obteniendo **36 observaciones** (una por municipio).

Variables consideradas (proporciones respecto a viviendas particulares habitadas): agua entubada, drenaje, electricidad, internet, computadora, celular, automóvil; además de escolaridad promedio (GRAPROES) y ocupación de la vivienda.

## Técnicas utilizadas

- Limpieza y preparación de datos con Pandas.
- Análisis exploratorio con Pandas/Matplotlib.
- Estandarización con `StandardScaler`.
- Clustering con `KMeans` (método del codo + coeficiente de silueta).
- Árbol de decisión (`DecisionTreeClassifier`) como herramienta explicativa.
- Comparación externa con marginación municipal CONAPO 2020.

## Resultados principales

- KMeans con **k = 3** (`random_state=42`, `n_init=10`), elegido con método del codo y coeficiente de silueta (silueta = 0.273; la métrica favorece k = 5, pero produce grupos de 1–2 municipios, decisión documentada en el notebook).
- Tres perfiles municipales: **alto** (9 municipios), **intermedio** (7) y **bajo** (20).
- Brecha digital: de 23% de viviendas con internet en Hueyapan a 73% en Cuernavaca.
- En Morelos el eje diferenciador combina conectividad e infraestructura hidráulica: el perfil *intermedio* agrupa municipios con menor acceso a agua entubada pese a buena escolaridad (Tepoztlán, Huitzilac, Tlayacapan).
- **Árbol explicativo:** un `DecisionTreeClassifier` de profundidad 2 reproduce el 97.2% de los clusters; regla principal `drenaje > 98%` separa al perfil alto; importancias: drenaje 0.56 y agua entubada 0.44.
- **Validación externa CONAPO:** Morelos no registra municipios con marginación Alta o Muy alta (12 Muy baja, 19 Baja, 5 Media). El perfil *alto* concentra 100% de marginación "Muy baja"; entre los perfiles *bajo* e *intermedio* las medianas del índice son casi iguales (55.7 vs 55.4), coincidencia parcial que se discute como limitación.

## Limitaciones

- Datos del Censo 2020: representan un periodo específico.
- Datos agregados por municipio, no individuos.
- Muestra municipal pequeña (36 municipios): los clusters son sensibles a las variables elegidas y al número de grupos (`k`).
- Los clusters son resultado del análisis, no categorías oficiales.
- La comparación con CONAPO es validación externa; no implica causalidad.

Detalle completo en el notebook y el artículo.

## Instrucciones de ejecución

1. Instalar Python 3.11+ o Anaconda.
2. Instalar dependencias: `pip install -r requirements.txt`
3. Descargar los datos originales en `data/raw/` (ver `data/raw/README_raw.md`): el ZIP del ITER 2020 (~35 MB, extraer en `data/raw/`) y la base municipal de CONAPO `IMM_2020.xls`.
4. Abrir y ejecutar `notebook/analisis_datos_publicos.ipynb` (debe quedar ejecutado en orden).

Nota: por tamaño, el dataset crudo nacional del ITER **no** está incluido en el repositorio; solo se incluye `data/processed/dataset_limpio.csv` (36 municipios de Morelos).

## Enlace al artículo

- Artículo técnico: [`articulo_tecnico.md`](articulo_tecnico.md)
- Versión de divulgación (Revista Hypatia): [`articulo_hypatia.md`](articulo_hypatia.md)
- PDF: pendiente de generar una vez aprobado el texto.
