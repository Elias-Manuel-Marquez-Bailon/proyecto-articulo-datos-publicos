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

---

## 20. Registro de avance — cierre de sesión sábado 22 de agosto de 2026

Estado real del proyecto al finalizar la sesión. Las fases 2, 3 y 4 están **COMPLETADAS**.

### Fase 1 — Investigación: ✅ COMPLETADA

Sin cambios respecto a lo descrito arriba.

### Fase 2 — Repositorio y preparación de datos: ✅ COMPLETADA

- Integrantes oficiales registrados en README: Gonzaga Castañeda Cristian Amauri,
  Portilla Palestina Viridiana, Chavez Martinez Adrian Uxue, Marquez Bailon Elias Manuel.
- **Corrección importante:** la URL original del ITER (`iter_2020_csv.zip`) ya no existe.
  La vigente es: https://www.inegi.org.mx/contenidos/programas/ccpv/2020/datosabiertos/iter/iter_00_cpv2020_csv.zip
  (~35 MB comprimidos; ~143 MB el CSV nacional extraído, NO "varios GB").
- Dataset descargado y extraído en `data/raw/iter_00_cpv2020/`.
- Notebook Partes 1–8 ejecutadas sin errores. Encoding correcto: **utf-8-sig** (el CSV trae BOM).
- Filtro municipal verificado con `assert`: `LOC=="0000"` + `ENTIDAD=="15"` excluyendo `MUN=="000"`
  → exactamente **125 municipios**.
- **Hallazgo metodológico clave:** los conteos `VPH_*` deben dividirse entre `VIVPARH_CV`
  ("viviendas particulares habitadas con características"), NO entre `VIVPAR_HAB`.
  Dividir entre `VIVPAR_HAB` produce proporciones > 1 (hasta 1.17). Documentado en Parte 6 del notebook.
- Variables aprobadas por el equipo (dataset limpio): proporciones `p_aguadv`, `p_drenaj`, `p_c_elec`,
  `p_inter`, `p_pc`, `p_cel`, `p_autom` + directas `GRAPROES`, `PROM_OCUP`;
  descriptivas fuera del modelo: `POBTOT`, `TVIVHAB`, `VIVPAR_HAB`, `VIVPARH_CV`, claves/nombres.
- `data/processed/dataset_limpio.csv`: 125 filas × 22 columnas, cero nulos, proporciones en [0, 1].
- `git init` + commit inicial `2bae1ca`.

### Fase 3 — Análisis exploratorio: ✅ COMPLETADA

- Notebook Partes 9–13: estadística descriptiva, distribuciones, municipios extremos,
  escolaridad vs conectividad, matriz de correlaciones.
- Gráficas generadas: `imagenes/grafica_1..5.png` (requisito mínimo de 2 superado).
- Hallazgos: brecha digital extrema en internet (3.8% Ixtapan del Oro → 75.7% Coacalco);
  gradiente educativo paralelo (6.5 vs 12.3 años);
  multicolinealidad alta: `p_inter`~`p_pc` r=0.97, `GRAPROES`~`p_pc` r=0.95, `GRAPROES`~`p_inter` r=0.94.
- Decisión del equipo: **quitar `p_pc` del clustering** (duplicada con `p_inter`);
  `GRAPROES` y `p_inter` se conservan por medir conceptos distintos.
- Commit `deee0af`.

### Fase 4 — KMeans: ✅ COMPLETADA

- Notebook Partes 14–18: variables finales (8), `StandardScaler`, codo + silueta para k=2..10
  (`grafica_6.png`), modelo final, perfiles, exportación (`grafica_7.png`).
- Modelo final: **KMeans k=3**, `random_state=42`, `n_init=10`. Silueta = 0.2694.
- Perfiles (renombrados por conectividad promedio): alto = 59 mun., intermedio = 50, bajo = 16.
- **Decisión justificada de k:** la silueta favorece k=2 (0.39) pero da división casi binaria;
  se eligió k=3 por interpretabilidad (estrato intermedio diferenciado) manteniendo cohesión aceptable.
  Preferencia documentada en el notebook (Parte 15). Caso ilustrativo para defensa:
  Chimalhuacán (metropolitano, ~700 mil hab.) cae en *intermedio*, demostrando que los clusters
  reflejan condiciones y no tamaño poblacional.
- Exportados: `outputs/resultados_modelo.csv` y `outputs/resumen_resultados.csv`.
- Commit `6b45b76`.

### Siguiente fase

**Fase 5 — Decision Tree explicativo:** usar `perfil`/`cluster` como variable objetivo,
obtener reglas legibles y variables que separan los grupos. Después Fase 6 (validación CONAPO).

### Recordatorios pendientes (apuntados por el alumno)

1. **Crear el repositorio remoto en GitHub**: <https://github.com/new>, nombre sugerido
   `proyecto-articulo-datos-publicos`, vacío (sin README/.gitignore/licencia), y pasar la URL
   para conectar con `git remote add origin <URL>` + push de los commits locales existentes.
   El alumno indicará además cómo configurar el repo correctamente (nota: este entorno CLI
   no puede visualizar imágenes; en Desktop sí).
2. **Falta el grupo** en el README (integrantes ya están).
3. **Encender/iniciar el servicio de Grafana** antes de la Fase 7 (dashboard); no dejarlo
   para el último momento.
4. Publicación Medium/Hashnode y PDF del artículo siguen pendientes (Fases 8–9).

---

## 21. Registro de avance — sesión domingo 23 de agosto de 2026

### Repositorio remoto configurado ✅

- Repo **público** creado manualmente por el alumno y conectado:
  https://github.com/Elias-Manuel-Marquez-Bailon/proyecto-articulo-datos-publicos
- Rama local renombrada `master` → `main` (queda trackeando `origin/main`; pushes simples con `git push`).
- Push inicial: 5 commits locales + 1 nuevo.
- README actualizado: grupo **9°A — IDGS (Ingeniería en Desarrollo y Gestión de Software)**,
  resultados principales de Fase 4, e instrucciones corregidas (ITER ~35 MB, extraer ZIP en
  `data/raw/`, queda `data/raw/iter_00_cpv2020/`; se corrigió el dato viejo de "varios GB").

### Fase 5 — Decision Tree explicativo: ✅ COMPLETADA

- Notebook Partes 19–20 agregadas (52 celdas totales), ejecutado completo de arriba a abajo
  con nbconvert usando Anaconda (`C:\Users\corey\anaconda3\python.exe -m nbconvert --execute`).
- `DecisionTreeClassifier(max_depth=3, min_samples_leaf=5, random_state=42)` sobre las mismas
  8 variables, objetivo = `perfil`. Sin train/test a propósito: fin interpretativo, no predictivo
  (justificado en el markdown de la Parte 19).
- Precisión reproduciendo los clusters: **0.952** (bajo 16/16, intermedio 48/50, alto 55/59).
  Se documenta que la coincidencia alta es esperable (mismas variables que KMeans):
  el árbol interpreta, NO valida; la validación externa es la Fase 6 con CONAPO.
- Regla principal del árbol: `p_cel <= 0.86` separa bajo/intermedio vs alto; dentro del ramal
  bajo, `p_inter <= 0.19` aísla el estrato bajo (con `p_drenaj <= 0.89` como refino).
- Importancias: p_cel 0.54, p_inter 0.20, p_drenaj 0.19, p_c_elec 0.06; el resto en 0.
- Gráficas nuevas: `imagenes/grafica_8.png` (diagrama del árbol) y `imagenes/grafica_9.png`
  (importancia de variables).
- Import ampliado en Parte 1: `from sklearn.tree import DecisionTreeClassifier, export_text, plot_tree`.

### Siguiente fase

**Fase 6 — Validación externa con CONAPO:** descargar marginación municipal 2020,
cruzar por clave de municipio (clave INEGI `MUN` vs clave CONAPO), analizar la distribución
de grados de marginación por cluster. Sin lenguaje causal; presentar como comparación.

### Recordatorios vigentes

1. ~~Crear repo remoto~~ ✅ hecho (sección 21). 
2. ~~Grupo en README~~ ✅ puesto (9°A — IDGS).
3. **Grafana:** encender/iniciar el servicio antes de la Fase 7; no dejarlo al final.
4. Publicación Medium/Hashnode y PDF del artículo (Fases 8–9) siguen pendientes.
5. Celdas "Lectura del equipo" del notebook siguen como prompts para redactar por el equipo
   (Partes 9, 10, 11, 13, 17, 18, 19 y 20); conviene llenarlas antes de la entrega.

---

## 22. Registro de avance — Fase 6: ✅ COMPLETADA (domingo 23 de agosto de 2026)

### Descarga y preparación

- Base oficial CONAPO descargada de `conapo.segob.gob.mx` → `data/raw/IMM_2020.xls` (~1.6 MB,
  NO se sube al repo por política de raw; instrucciones en `data/raw/README_raw.md`).
- Hoja usada: `IMM_2020` (header en fila 0; la hoja "Base de marginación 2020" trae títulos).
- Requirió `xlrd>=2.0.1` instalado en Anaconda base para leer `.xls`; agregado a `requirements.txt`.
- Cruce por clave entera: `CVE_MUN_CONAPO == 15000 + MUN`. Control de calidad: población
  idéntica al 100% entre ambas fuentes tras el cruce (`assert` implícito, dif. relativa máx = 0.0).

### Resultados del cruce (Partes 21–23 del notebook, 60 celdas totales)

- Distribución oficial estatal GM_2020: Muy bajo 73, Bajo 26, Medio 14, Alto 12, Muy alto 0.
- **Gradiente perfectamente compatible con KMeans:**
  - perfil *bajo* (16): 68.8% marginación Alto + 31.2% Medio; cero municipios en grados bajos.
  - perfil *intermedio* (50): 52% Bajo + 28% Muy bajo + 18% Medio + 2% Alto.
  - perfil *alto* (59): **100% Muy bajo**.
- Mediana IM_2020 monótona: 52.13 (*bajo*) < 55.78 (*intermedio*) < 58.60 (*alto*).
  OJO para defensa: en esta base, MAYOR IM_2020 = MENOR marginación (escala invertida);
  aclararlo al presentar la mediana.
- Cero casos discordantes extremos (ningún *alto* con marginación alta, ningún *bajo*
  con marginación baja). Mencionar como matiz que ambas fuentes provienen del Censo 2020
  y comparten dimensiones conceptuales, por lo que la coincidencia fuerte era esperable;
  el valor está en el gradiente limpio y monotónico, no en "validar" circularmente.
- Gráfica nueva: `imagenes/grafica_10.png` (barras apiladas 100% grado de marginación por perfil).
- Export nuevo: `outputs/cruce_conapo_perfiles.csv` (MUN, NOM_MUN, perfil, IM_2020, GM_2020).
- README actualizado: resultados principales incluyen árbol y validación CONAPO;
  instrucciones de ejecución mencionan descargar IMM_2020.xls.

### Siguiente fase

**Fase 7 — Visualización / dashboard:** prioridad a gráficas ya existentes (10) y resultados
exportados; mapa de clusters si es viable; Grafana SOLO si se implementa rápido y estable
(recordatorio: encender el servicio con anticipación).

### Estado global del proyecto

Fases 1–6 completadas. Pendientes: Fase 7 (dashboard opcional), Fase 8 (artículo ~4,000
caracteres para Hypatia + PDF), Fase 9 (Medium/Hashnode, presentación 5–7 min), y llenar las
celdas "Lectura del equipo" del notebook con las interpretaciones del equipo.

---

## 23. Registro de avance — Fase 8: borradores v1 de ambos artículos (domingo 23 de agosto de 2026)

### Artículo técnico (`articulo_tecnico.md`)

- Borrador completo con la estructura exigida por el profesor (Resumen → Referencias).
- **1,647 palabras** sin contar URLs ni referencias (meta 1200–1800 ✅).
- Todos los números tomados de los resultados reales del notebook/outputs:
  silueta k=2 vs k=3, composición 59/50/16, brecha digital 3.8%–75.7%, hallazgo del
  denominador `VIVPARH_CV`, precisión del árbol 95.2%, regla `p_cel <= 0.86`,
  importancias 0.54/0.20/0.19/0.06, gradiente CONAPO completo y caso Chimalhuacán.
- Tabla resumen de perfiles incluida en Resultados.
- 7 referencias numeradas (INEGI x3, CONAPO x2, scikit-learn x2), dentro de la meta 7–9.
- Incluye limitaciones condensadas de la sección 13 y lectura cautelosa de la coincidencia
  con CONAPO (mismo censo de origen; no validación circular).

### Versión Hypatia (`articulo_hypatia.md`, archivo nuevo)

- Borrador de divulgación conforme a REGLAS_ARTICULO_HYPATIA.md:
  **4,056 caracteres con espacios** (meta ~4,000 ✅), inicio gancho cotidiano,
  desarrollo y cierre; sin citas ni referencias; términos explicados entre paréntesis
  (KMeans = ordenar frutas, árbol = lista de preguntas); subtítulos mínimos;
  instituciones mencionadas (INEGI, CONAPO, UTEZ); fidelidad a los números reales.
- Datos de autores: nombres + grupo 9°A + UTEZ + correos institucionales.
- **Decisión de privacidad:** los teléfonos NO se suben al repo público; van únicamente en el
  documento Word final que se envíe a hypatia@morelos.gob.mx (asunto = título).
  Pendiente confirmar "último grado académico" de cada autor para la versión final.

### Pendientes derivados

1. Revisión y ajuste de ambos borradores por el equipo (voz propia del equipo).
2. Generar PDF del artículo técnico (pandoc o Word) una vez aprobado.
3. Formatear Hypatia a Word: Arial 11, subtítulos Arial 12 negritas, interlineado sencillo,
   agregar teléfonos, nombre de archivo con palabras clave del tema.
4. Publicación Medium/Hashnode (puede reutilizar el artículo técnico).
5. Fase 7 opcional: Grafana (login: probar admin/admin; si se olvidó la contraseña,
   resetear con `grafana-cli admin reset-admin-password <nueva>`).

---

## 24. Cierre de sesión — domingo 23 de agosto de 2026 (resumen para revisión del alumno)

Todo lo de esta sesión quedó guardado y publicado en GitHub (commits `9a585bd` → `ad60d79`).

### Qué se completó hoy

1. **Repo remoto configurado** — creado manualmente por el alumno y conectado; rama `master`
   renombrada a `main`; todo sincronizado con `git push`.
   https://github.com/Elias-Manuel-Marquez-Bailon/proyecto-articulo-datos-publicos
2. **README completo** — grupo 9°A IDGS agregado; resultados principales actualizados hasta
   Fase 6; instrucciones corregidas (ITER ~35 MB + IMM_2020.xls).
3. **Fase 5 ✅** — árbol de decisión explicativo (Partes 19–20): precisión 0.952,
   regla principal `p_cel <= 0.86`, importancias p_cel/p_inter/p_drenaj;
   `grafica_8.png` y `grafica_9.png`.
4. **Fase 6 ✅** — validación externa CONAPO (Partes 21–23): descarga oficial de
   `IMM_2020.xls`, cruce por `15000 + MUN` verificado con población idéntica al 100%,
   gradiente compatible (alto = 100% Muy bajo; bajo = Alto/Medio sin excepciones),
   `grafica_10.png` y `outputs/cruce_conapo_perfiles.csv`. Requirió `xlrd` en requirements.
5. **Fase 8 (borradores v1)** — `articulo_tecnico.md` (1,647 palabras, estructura completa,
   7 referencias) y `articulo_hypatia.md` (4,056 caracteres, divulgación sin citas).
   Teléfonos de autores NO subidos al repo público (solo al Word final de la revista).

### Qué debe revisar el equipo sobre los borradores

- Voz y estilo: ajustar frases a su manera de escribir (los borradores son base de trabajo).
- Confirmar "último grado académico" de cada autor para Hypatia (¿Estudiante/Pasante/TSU?).
- Verificar que todos se sientan representados en la autoría y el orden de los nombres.

### Estado global al cerrar la sesión

| Fase | Estado |
|---|---|
| 1–4 | ✅ Completadas (sesión sábado 22) |
| 5 Decision Tree | ✅ Completada |
| 6 Validación CONAPO | ✅ Completada |
| 7 Dashboard/Grafana | ⏸ Opcional; probar login admin/admin o resetear contraseña |
| 8 Artículos | 🟡 Borradores v1 listos, falta revisión del equipo |
| 8 PDF / Word Hypatia | ⬜ Tras aprobar textos |
| 9 Medium/Hashnode + presentación | ⬜ Pendiente |

Pendiente transversal: llenar las celdas "Lectura del equipo" del notebook antes de entregar.
