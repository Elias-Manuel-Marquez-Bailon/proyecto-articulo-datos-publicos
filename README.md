# Segmentación de los municipios del Estado de México según condiciones de vivienda, servicios y conectividad mediante KMeans

Proyecto final de la materia **Extracción de Conocimiento en Bases de Datos**: análisis no supervisado con datos públicos reales (INEGI Censo 2020 / ITER) para agrupar municipios con condiciones semejantes.

## Integrantes

- Gonzaga Castañeda Cristian Amauri
- Portilla Palestina Viridiana
- Chavez Martinez Adrian Uxue
- Marquez Bailon Elias Manuel

**Grupo:** 9°A — IDGS (Ingeniería en Desarrollo y Gestión de Software)

## Pregunta guía

¿Qué municipios del Estado de México presentan características similares en sus condiciones de vivienda, acceso a servicios y conectividad?

## Fuente de datos

- **Principal:** INEGI — Censo de Población y Vivienda 2020, Principales Resultados por Localidad (ITER). <https://www.inegi.org.mx/programas/ccpv/2020/default.html>
- **Validación externa:** CONAPO — Índices de Marginación 2020. <https://www.gob.mx/conapo/documentos/indices-de-marginacion-2020-284372>

## Descripción del dataset

El ITER 2020 contiene indicadores de población y vivienda por localidad y municipio. Se filtran los registros municipales del Estado de México (`LOC == "0000"`), obteniendo **125 observaciones** (una por municipio).

Variables consideradas (proporciones respecto a viviendas particulares habitadas): agua entubada, drenaje, electricidad, internet, computadora, celular, automóvil; además de escolaridad promedio (GRAPROES) y ocupación de la vivienda.

## Técnicas utilizadas

- Limpieza y preparación de datos con Pandas.
- Análisis exploratorio con Pandas/Matplotlib.
- Estandarización con `StandardScaler`.
- Clustering con `KMeans` (método del codo + coeficiente de silueta).
- Árbol de decisión (`DecisionTreeClassifier`) como herramienta explicativa.
- Comparación externa con marginación municipal CONAPO 2020.

## Resultados principales

- KMeans con **k = 3** (`random_state=42`, `n_init=10`), elegido con método del codo y coeficiente de silueta (silueta = 0.27).
- Tres perfiles municipales por conectividad y servicios: **alto** (59 municipios), **intermedio** (50) y **bajo** (16).
- Brecha digital marcada en internet: de 3.8% de viviendas conectadas en el municipio menos conectado a 75.7% en el más conectado.
- El clustering refleja condiciones de vivienda/servicios, no tamaño poblacional.

*Se actualizará al completar las Fases 5–6 (árbol explicativo y validación CONAPO).*

## Limitaciones

- Datos del Censo 2020: representan un periodo específico.
- Datos agregados por municipio, no individuos.
- El resultado depende de las variables seleccionadas y del número de clusters (`k`).
- Los clusters son resultado del análisis, no categorías oficiales.
- La comparación con CONAPO es validación externa; no implica causalidad.

Detalle completo en el notebook y el artículo.

## Instrucciones de ejecución

1. Instalar Python 3.11+ o Anaconda.
2. Instalar dependencias: `pip install -r requirements.txt`
3. Descargar el ITER 2020 (~35 MB) desde `referencias/fuentes_datos.txt` y extraer el ZIP en `data/raw/` (debe quedar la carpeta `data/raw/iter_00_cpv2020/`).
4. Abrir y ejecutar `notebook/analisis_datos_publicos.ipynb` (debe quedar ejecutado en orden).

Nota: por tamaño, el dataset crudo nacional del ITER **no** está incluido en el repositorio; solo se incluye `data/processed/dataset_limpio.csv` (125 municipios).

## Enlace al artículo

- Artículo técnico: [`articulo_tecnico.md`](articulo_tecnico.md)
- Versión de divulgación (Revista Hypatia) y PDF: pendientes.
