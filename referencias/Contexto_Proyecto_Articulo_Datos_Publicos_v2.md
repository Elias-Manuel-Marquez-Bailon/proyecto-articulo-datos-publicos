# Contexto maestro v2 — Proyecto final: Artículo técnico con datos públicos

## 1. Objetivo de este archivo

Este documento sustituye al contexto inicial del proyecto y debe utilizarse como contexto maestro para continuar el trabajo en otro chat sin tener que explicar nuevamente el proyecto.

El objetivo es desarrollar un artículo técnico aplicado, reproducible y defendible, usando datos públicos reales, con un análisis de segmentación de municipios mediante KMeans y un árbol de decisión como herramienta explicativa.

**Fecha límite del proyecto:** lunes.  
**Forma de trabajo:** Jupyter Notebook / Anaconda, Python y Markdown en español.

---

## 2. Perfil y forma de trabajo del alumno

- Alumno de Ingeniería de Software.
- Materia: Extracción de Conocimiento en Bases de Datos.
- Trabaja principalmente con Anaconda Jupyter Notebook.
- Prefiere notebooks sencillos y ordenados.
- Estilo habitual:
  - celdas Markdown con encabezados `## Parte X ...`;
  - código separado por etapas;
  - imports → carga → revisión → limpieza → análisis → modelo → resultados;
  - interpretaciones escritas en Markdown por el alumno.
- El proyecto es por equipo, pero todos deben poder explicar lo realizado.
- Se debe priorizar un proyecto sólido y comprensible sobre el uso excesivo de tecnologías.

---

## 3. Requisitos del profesor

El proyecto debe desarrollar un **artículo técnico aplicado usando datos públicos reales**, integrando:

- búsqueda y selección de datos;
- revisión y preparación;
- limpieza básica;
- análisis exploratorio;
- al menos un modelo supervisado o no supervisado;
- interpretación de resultados;
- limitaciones;
- publicación en repositorio.

El artículo debe tener aproximadamente **1200–1800 palabras** y debe leerse como artículo técnico, no solamente como explicación de código.

### Fuentes de datos permitidas

- INEGI;
- API del Banco de Indicadores de INEGI;
- Portal de datos abiertos de México;
- datos abiertos de gobiernos estatales/municipales e instituciones públicas con fuente clara.

No utilizar:

- datos personales sensibles;
- bases filtradas de redes sociales;
- datasets sin fuente;
- sitios dudosos.

### Modelos permitidos/relevantes

- Supervisado: creación de variable objetivo + `DecisionTreeClassifier`.
- No supervisado: variables numéricas + escalado + `KMeans` + análisis de clusters.

### Requisitos del repositorio

```text
proyecto-articulo-datos-publicos/
├── README.md
├── articulo_tecnico.md
├── notebook/
│   └── analisis_datos_publicos.ipynb
├── data/
│   ├── raw/
│   │   └── dataset_original.csv
│   └── processed/
│       └── dataset_limpio.csv
├── outputs/
│   ├── resultados_modelo.csv
│   └── resumen_resultados.csv
├── imagenes/
│   ├── grafica_1.png
│   └── grafica_2.png
├── referencias/
│   └── fuentes_datos.txt
└── requirements.txt
```

El notebook debe quedar **ejecutado**.

El README debe incluir título, integrantes, grupo, materia, pregunta guía, fuente de datos, descripción del dataset, técnicas, resultados principales, limitaciones, instrucciones de ejecución y enlace al artículo.

El artículo debe incluir:

- Título
- Resumen
- Introducción
- Fuente de datos
- Preparación de datos
- Análisis exploratorio
- Metodología
- Resultados
- Interpretación
- Limitaciones
- Conclusiones
- Referencias

También se necesita:

- PDF del artículo;
- GitHub;
- publicación en Medium o Hashnode;
- presentación/defensa oral de 5–7 minutos;
- dashboard, preferentemente Grafana, si el tiempo lo permite.

---

## 4. Tema definitivo propuesto

### Título de trabajo

**Segmentación de los municipios del Estado de México según condiciones de vivienda, servicios y conectividad mediante KMeans**

### Pregunta guía

**¿Qué municipios del Estado de México presentan características similares en sus condiciones de vivienda, acceso a servicios y conectividad?**

### Alcance geográfico

Trabajar inicialmente con los **125 municipios del Estado de México**.

Se eligió este alcance porque:

- hace el problema concreto;
- permite una explicación clara;
- facilita las visualizaciones;
- reduce complejidad;
- mantiene suficiente cantidad de observaciones para KMeans;
- coincide con la recomendación de evitar temas demasiado generales.

No se analizarán inicialmente los aproximadamente 2,400 municipios del país.

---

## 5. Fuente principal de datos

### INEGI — Censo de Población y Vivienda 2020 / ITER

El Censo 2020 contiene información sobre población, vivienda, servicios, educación y otras características, con desagregación geográfica que permite trabajar a nivel municipal.

El ITER y su diccionario de datos serán la referencia principal para seleccionar y comprender las variables.

Fuente oficial:
https://www.inegi.org.mx/programas/ccpv/2020/default.html

Documentación del ITER:
https://www.inegi.org.mx/contenidos/programas/ccpv/2020/doc/fd_iter_cpv2020.pdf

La propuesta inicial identificó la descarga del ITER 2020 para Estados Unidos Mexicanos y el filtro de municipios mediante los registros correspondientes a `Total del Municipio` / `LOC == "0000"`.

**Importante:** antes de fijar las variables definitivas, revisar el diccionario oficial y comprobar:
- significado;
- unidad;
- denominador;
- cobertura;
- valores especiales;
- posibles valores nulos;
- si conviene convertir conteos a proporciones.

---

## 6. Fuente complementaria principal

### CONAPO — Índices de Marginación 2020

Se utilizará como posible **validación externa** de los clusters.

Página oficial:
https://www.gob.mx/conapo/documentos/indices-de-marginacion-2020-284372

Existe información de marginación a nivel de entidad federativa y municipio, además de bases de datos y documentación metodológica.

La intención NO es afirmar que KMeans calcula o mide la marginación.

La comparación debe plantearse como:

> Los clusters obtenidos mediante KMeans se compararon con los indicadores/grados de marginación municipal publicados por CONAPO para observar si existían patrones compatibles o diferencias.

No debe utilizarse lenguaje causal ni afirmaciones absolutas.

---

## 7. Fuentes metodológicas y académicas

Además de las fuentes de datos proporcionadas por el profesor, se pueden utilizar fuentes externas confiables para fundamentar la metodología.

Tipos de fuentes deseados:

1. Artículos académicos sobre:
   - análisis municipal;
   - desigualdad territorial;
   - indicadores socioeconómicos;
   - clustering o segmentación territorial.

2. Documentación oficial de Scikit-learn:
   - KMeans;
   - `StandardScaler`;
   - coeficiente de silueta;
   - `DecisionTreeClassifier`.

3. Documentación metodológica de INEGI y CONAPO.

No se debe llenar la bibliografía con fuentes innecesarias. Objetivo aproximado: **7–9 fuentes bien justificadas**, incluyendo fuentes de datos y metodológicas.

---

## 8. Fuentes proporcionadas originalmente por el profesor

1. INEGI:
https://www.inegi.org.mx/

2. API del Banco de Indicadores:
https://www.inegi.org.mx/servicios/api_indicadores.html

3. Portal de datos abiertos de México:
https://www.datos.gob.mx/

Estas fuentes siguen siendo válidas y deben conservarse como parte del contexto original del proyecto.

---

## 9. Decisiones importantes

### Sí utilizar

- INEGI Censo 2020 / ITER.
- CONAPO Marginación 2020.
- Python.
- Jupyter / Anaconda.
- Pandas.
- NumPy.
- Matplotlib.
- Scikit-learn.
- KMeans.
- StandardScaler.
- Silhouette Score.
- DecisionTreeClassifier como modelo explicativo.
- Grafana si puede implementarse sin poner en riesgo el proyecto.

### No agregar por ahora

No incorporar DENUE, AWS, TensorFlow, PyTorch, Spark, APIs adicionales, Docker u otras tecnologías solamente para hacer el proyecto más grande.

La prioridad es:

**calidad > cantidad de tecnologías.**

DENUE podría reconsiderarse solamente si durante el desarrollo aparece una razón clara y si no compromete el tiempo de entrega.

---

## 10. Metodología definitiva propuesta

### Fase 1 — Investigación

Estado: **prácticamente completada**.

Se revisaron:

- requisitos del profesor;
- INEGI;
- Censo 2020;
- ITER;
- CONAPO Marginación 2020;
- posibilidades de fuentes académicas/metodológicas;
- Scikit-learn;
- alcance geográfico.

### Fase 2 — Preparación e implementación inicial

Siguiente fase.

1. Crear repositorio.
2. Crear estructura de carpetas.
3. Crear entorno / `requirements.txt`.
4. Descargar ITER.
5. Guardar dataset original en `data/raw/`.
6. Explorar estructura.
7. Filtrar los municipios del Estado de México.
8. Revisar nombres de variables y diccionario.
9. Seleccionar variables.
10. Limpiar valores especiales.
11. Convertir variables a formato numérico cuando corresponda.
12. Crear proporciones cuando sea metodológicamente apropiado.
13. Guardar dataset procesado.

### Fase 3 — Análisis exploratorio

Realizar:

- revisión de tipos;
- nulos;
- estadísticas descriptivas;
- distribuciones;
- comparación entre municipios;
- correlaciones.

Objetivo aproximado: 4–6 visualizaciones útiles, aunque el requisito mínimo es 2.

### Fase 4 — KMeans

1. Seleccionar variables numéricas finales.
2. Estandarizar con `StandardScaler`.
3. Probar diferentes valores de `k`.
4. Utilizar método del codo.
5. Utilizar coeficiente de silueta.
6. Elegir un `k` justificable.
7. Entrenar KMeans con semilla fija.
8. Asignar cluster a cada municipio.
9. Analizar perfiles promedio de cada cluster.
10. Exportar resultados.

No escoger el número de clusters solamente porque visualmente parezca conveniente.

### Fase 5 — Interpretación mediante Decision Tree

Usar el cluster generado por KMeans como variable objetivo para un `DecisionTreeClassifier`.

Objetivo:

- encontrar reglas legibles;
- identificar qué variables separan los clusters;
- complementar la interpretación de KMeans.

Debe explicarse claramente que el cluster es una etiqueta creada por el algoritmo y **no una verdad oficial**.

### Fase 6 — Validación externa con CONAPO

Cruzar los municipios con la información de marginación 2020.

Analizar:

- distribución de grados de marginación por cluster;
- promedios o indicadores relevantes;
- coincidencias;
- diferencias;
- posibles patrones.

No afirmar causalidad.

### Fase 7 — Visualización / dashboard

Prioridad:

1. gráficas del notebook;
2. resultados exportados;
3. mapa de clusters si es viable;
4. Grafana si puede implementarse rápidamente y de forma estable.

Grafana es complemento, no debe poner en riesgo el notebook ni el artículo.

### Fase 8 — Artículo

Redactar 1200–1800 palabras.

### Fase 9 — Entregables

- Notebook ejecutado.
- Dataset raw.
- Dataset procesado.
- CSV de resultados.
- Gráficas.
- README.
- Artículo Markdown.
- PDF.
- Repositorio GitHub.
- Publicación Medium/Hashnode.
- Presentación/defensa.

---

## 11. Variables: decisión pendiente

No fijar todavía las variables finales.

Posibles variables candidatas identificadas inicialmente:

- `POBTOT`
- `GRAPROES`
- viviendas particulares habitadas;
- viviendas con agua;
- viviendas con drenaje;
- viviendas con electricidad;
- viviendas con internet;
- viviendas con computadora;
- viviendas con celular;
- viviendas con automóvil;
- ocupantes por vivienda.

La selección final debe hacerse después de revisar el diccionario del ITER.

### Consideración importante

Evitar que variables absolutas de tamaño, especialmente población total, dominen el clustering.

Cuando sea apropiado, convertir conteos de viviendas a proporciones o porcentajes respecto del denominador correspondiente.

`POBTOT` puede mantenerse como variable descriptiva o utilizarse de forma controlada si la evidencia exploratoria justifica incluirla.

---

## 12. Flujo conceptual

```text
INEGI Censo 2020 / ITER
          |
          v
Filtrar municipios Estado de México
          |
          v
Revisión + limpieza
          |
          v
Selección de variables
          |
          v
Proporciones / transformaciones
          |
          v
EDA
          |
          v
StandardScaler
          |
          v
KMeans
          |
          v
Clusters
     /          \
    v            v
Decision Tree   CONAPO 2020
explicativo     validación externa
     \          /
      v        v
       Interpretación
             |
             v
        Resultados
             |
     +-------+-------+
     |       |       |
    CSV   Gráficas Dashboard
     |
     v
Artículo + PDF + GitHub
```

---

## 13. Limitaciones que deben aparecer en el artículo

Como mínimo:

- Los datos corresponden al Censo 2020 y representan un periodo específico.
- Se trabaja con datos agregados por municipio, no con individuos.
- KMeans depende de las variables seleccionadas.
- El resultado depende del número de clusters (`k`).
- La estandarización y transformación de variables influyen en el resultado.
- El Decision Tree utiliza como objetivo una etiqueta generada por KMeans.
- Los clusters no representan categorías oficiales de calidad de vida.
- La comparación con CONAPO es una validación/comparación externa, no una prueba causal.
- El análisis no permite establecer causalidad.
- Puede haber variables relevantes no incluidas.
- Los resultados deben interpretarse como patrones sugeridos por los datos.

---

## 14. Principios para todo el proyecto

1. No complicar el proyecto innecesariamente.
2. Cada tecnología debe tener una función clara.
3. Cada variable debe tener una justificación.
4. Cada fuente debe utilizarse realmente.
5. No hacer afirmaciones causales.
6. No presentar un cluster como una categoría oficial.
7. Explicar las decisiones en Markdown.
8. Mantener reproducibilidad mediante semilla fija.
9. Guardar datos originales separados de datos procesados.
10. No modificar el dataset original.
11. Evitar datos personales.
12. Priorizar fuentes oficiales y literatura académica confiable.
13. El proyecto debe poder ser explicado por el alumno durante una defensa de 5–7 minutos.

---

## 15. Estado actual

### Ya decidido

- Tema: segmentación municipal.
- Estado: Estado de México.
- Observaciones esperadas: 125 municipios.
- Fuente principal: INEGI Censo 2020 / ITER.
- Modelo principal: KMeans.
- Modelo complementario: Decision Tree explicativo.
- Validación externa: CONAPO Marginación 2020.
- Python + Jupyter.
- Grafana como complemento si el tiempo lo permite.
- No incorporar tecnologías innecesarias.

### Pendiente inmediato

1. Crear repositorio.
2. Crear estructura.
3. Descargar ITER.
4. Explorar dataset.
5. Revisar diccionario.
6. Seleccionar variables definitivas.
7. Limpiar y procesar.

---

## 16. Fuentes investigadas hasta ahora

### INEGI — Censo de Población y Vivienda 2020
https://www.inegi.org.mx/programas/ccpv/2020/default.html

Sirve como fuente principal y contiene documentación metodológica, resultados, metadatos y herramientas del Censo.

### INEGI — Diccionario / documentación ITER
https://www.inegi.org.mx/contenidos/programas/ccpv/2020/doc/fd_iter_cpv2020.pdf

Sirve para interpretar correctamente las variables del ITER.

### CONAPO — Índices de Marginación 2020
https://www.gob.mx/conapo/documentos/indices-de-marginacion-2020-284372

Sirve como fuente complementaria y para la posible validación externa de los clusters.

### CONAPO — Índice de marginación por entidad federativa y municipio 2020
https://www.gob.mx/conapo/es/articulos/indice-de-marginacion-por-entidad-federativa-y-municipio-2020-271404

Sirve para consultar resultados de marginación municipal 2020.

### Scikit-learn
Utilizar la documentación oficial para fundamentar KMeans, StandardScaler, silhouette y DecisionTreeClassifier.

---

## 17. Instrucciones para el siguiente chat

El siguiente asistente debe asumir que:

- este documento ya contiene el contexto del proyecto;
- la Fase 1 de investigación ya fue realizada;
- no debe volver a preguntar desde cero qué proyecto se está haciendo;
- debe continuar con la Fase 2;
- debe respetar las decisiones establecidas aquí;
- debe ser crítico si encuentra un problema metodológico;
- debe priorizar una solución sencilla, reproducible y defendible;
- no debe agregar tecnologías innecesarias.

### Primer objetivo del siguiente chat

Comenzar con:

**Fase 2 — Construcción del repositorio y preparación de datos.**

Orden recomendado:

1. Confirmar la estructura del repositorio.
2. Crear las carpetas y archivos iniciales.
3. Preparar `requirements.txt`.
4. Descargar el ITER 2020.
5. Guardarlo en `data/raw/`.
6. Crear/abrir el notebook.
7. Explorar columnas y registros.
8. Revisar el diccionario.
9. Filtrar los 125 municipios del Estado de México.
10. Seleccionar las variables definitivas con justificación.

No saltar directamente a KMeans sin comprobar primero la calidad y significado de las variables.

---

## 18. Regla general del proyecto

La meta no es entregar el proyecto más grande.

La meta es entregar un proyecto que pueda defenderse diciendo:

> "Utilicé una fuente pública oficial, preparé los datos, seleccioné variables justificadas, exploré los patrones, apliqué KMeans de forma reproducible, evalué la separación de los grupos, interpreté los clusters mediante un árbol de decisión y comparé los resultados con una fuente oficial externa."

Si todo eso está correctamente realizado, el proyecto será técnicamente sólido incluso sin incorporar muchas tecnologías.

---

## 19. Plan aprobado — Fase 2 (registro de trabajo)

Plan aprobado por el equipo y en ejecución. Fecha de registro: sábado 22 de agosto de 2026.

### Decisiones confirmadas

- El repositorio vive en la carpeta local existente: `C:\Users\corey\OneDrive\Desktop\Proyecto-Articulo`.
- El profesor no exige un nombre de repositorio; solo la estructura interna. Nombre sugerido para GitHub: `proyecto-articulo-datos-publicos`.
- Se hará `git init` local; el repositorio remoto en GitHub lo crea el alumno manualmente y después se conecta con `git remote add origin <URL>`.
- Python a utilizar: Anaconda base instalado en `C:\Users\corey\anaconda3` (Python 3.13.9) con pandas 2.3.3, scikit-learn 1.7.2 y matplotlib ya disponibles.
- La descarga del ITER la realiza el asistente automáticamente.
- Extensión del artículo para Hypatia: ~4,000 caracteres con espacios (sustituye las 1200–1800 palabras del contexto original).

### Pasos aprobados

1. Guardar este plan al final de este documento y copiar los dos MDs de contexto dentro del repositorio (`referencias/`).
2. Crear estructura de carpetas: README.md inicial, articulo_tecnico.md (placeholder), notebook/, data/raw/, data/processed/, outputs/, imagenes/, referencias/, requirements.txt, .gitignore.
3. Descargar `iter_2020_csv.zip` desde INEGI a `data/raw/`, inspeccionar el zip y extraer lo necesario.
4. Crear notebook `analisis_datos_publicos.ipynb` con esqueleto "## Parte X": imports → carga → revisión → filtro Edomex → limpieza → variables → proporciones → guardado.
5. Exploración inicial: cargar CSV (encoding latin), revisar columnas, filtrar `LOC == "0000"` + Estado de México, verificar 125 municipios.
6. Descargar diccionario oficial a `referencias/` y proponer lista definitiva de variables con justificación (aprobación del alumno antes de limpiar).
7. Limpieza y procesado: tipos numéricos, valores especiales (`*`, N/D), proporciones, guardar `data/processed/dataset_limpio.csv`.
8. `git init` + `.gitignore` + primer commit con la estructura.

### Decisión sobre datos pesados

- El CSV completo nacional del ITER pesa varios GB y GitHub no acepta archivos mayores a 100 MB.
- No se subirá el raw nacional al repo: queda local en `data/raw/` con instrucciones de descarga en el README.
- Solo se sube `dataset_limpio.csv` (125 filas).
