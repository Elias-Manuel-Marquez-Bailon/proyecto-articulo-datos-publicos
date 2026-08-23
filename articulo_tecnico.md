# Segmentación de los municipios del Estado de México según condiciones de vivienda, servicios y conectividad mediante KMeans

**Gonzaga Castañeda Cristian Amauri · Chavez Martinez Adrian Uxue · Marquez Bailon Elias Manuel · Portilla Palestina Viridiana**

Grupo 9°A — Ingeniería en Desarrollo y Gestión de Software (IDGS), Universidad Tecnológica de Emiliano Zapata (UTEZ)

## Resumen

Este artículo aplica aprendizaje no supervisado a datos públicos del Censo de Población y Vivienda 2020 para segmentar los 125 municipios del Estado de México según sus condiciones de vivienda, acceso a servicios básicos y conectividad digital. Después de expresar los conteos censales como proporciones municipales, se estandarizaron ocho indicadores y se entrenó un modelo KMeans, eligiendo tres grupos mediante el método del codo y el coeficiente de silueta. Los perfiles resultantes corresponden a niveles alto (59 municipios), intermedio (50) y bajo (16) de equipamiento urbano, con una brecha digital notable en el acceso a internet, que va de 3.8% a 75.7% de las viviendas según el municipio. Un árbol de decisión de profundidad tres reproduce 95.2% de la asignación de grupos e identifica la disponibilidad de celular en la vivienda como la principal variable discriminante. La comparación con los grados de marginación municipales 2020 de CONAPO muestra un patrón compatible: el perfil alto concentra el 100% de los municipios con marginación muy baja, mientras que el perfil bajo se reparte entre marginación alta y media. Los resultados describen patrones territoriales sugerentes para la focalización de políticas públicas, aunque no constituyen categorías oficiales.

**Palabras clave:** clustering, KMeans, municipios, Censo 2020, conectividad, marginación.

## 1. Introducción

El Estado de México es la entidad más poblada de México y presenta contrastes territoriales profundos: municipios metropolitanos densamente urbanizados conviven con demarcaciones rurales y semirurales. Entender qué municipios comparten condiciones parecidas de vivienda, servicios y conectividad es útil para diseñar políticas públicas diferenciadas, priorizar inversión y dar seguimiento a las desigualdades internas de la entidad.

Este trabajo responde a la pregunta guía: *¿qué municipios del Estado de México presentan características similares en sus condiciones de vivienda, acceso a servicios y conectividad?* Para ello se aplicó segmentación con KMeans sobre indicadores censales municipales, se utilizó un árbol de decisión como herramienta de interpretación y se contrastaron los grupos con el índice de marginación municipal de CONAPO. El alcance es deliberadamente acotado —125 observaciones de una sola entidad—, con fuentes públicas oficiales y un flujo de trabajo completamente reproducible (semilla aleatoria fija y datos separados en crudo y procesados).

## 2. Fuente de datos

La fuente principal es el **ITER 2020** (Principales Resultados por Localidad) del **Censo de Población y Vivienda 2020 de INEGI**, descargado del sitio oficial de datos abiertos. El ITER reporta, para cada municipio, conteos de población y vivienda junto con indicadores de educación, servicios y bienes en el hogar. Se seleccionó esta fuente porque es oficial, gratuita, está documentada mediante ficha técnica y diccionario de datos, y permite trabajar directamente al nivel municipal.

Como fuente complementaria se emplearon los **Índices de Marginación 2020 de CONAPO**, que asignan a cada municipio un índice y un grado de marginación en cinco categorías. Esta base se utilizó exclusivamente como referencia externa para contrastar los grupos obtenidos, no como entrada del modelo.

## 3. Preparación de datos

Del archivo nacional del ITER se filtraron los registros municipales (localidad `"0000"`) de la entidad 15, obteniendo exactamente **125 municipios**, verificado programáticamente. Se revisaron tipos de dato y valores especiales del censo (`*`, N/D) conforme al diccionario oficial.

Un hallazgo metodológico relevante fue la elección del denominador de las proporciones: los conteos de viviendas con cada atributo (`VPH_*`) se dividieron entre las viviendas particulares habitadas *con características de ocupantes* (`VIVPARH_CV`). Dividir entre el total de viviendas habitadas producía proporciones mayores a 1 en algunos municipios, lo cual es inválido; con el denominador correcto todas quedaron en el rango [0, 1].

El conjunto de variables quedó integrado por siete proporciones (agua entubada, drenaje, electricidad, internet, computadora, celular y automóvil en la vivienda), la escolaridad promedio (`GRAPROES`, en años) y los ocupantes promedio por vivienda (`PROM_OCUP`). La población total se conservó solo como variable descriptiva, fuera del modelo, para evitar que el tamaño de los municipios dominara el cálculo de similitudes. El resultado fue un dataset procesado de 125 filas por 22 columnas, sin valores nulos.

## 4. Análisis exploratorio

La exploración evidenció dos hechos. Primero, una **brecha digital extrema**: la proporción de viviendas con internet va de 3.8% en Ixtapan del Oro a 75.7% en Coacalco de Berriozábal, casi veinte veces más; la escolaridad promedio acompaña ese gradiente (6.5 frente a 12.3 años aprobados). Segundo, una **multicolinealidad fuerte**: internet y computadora correlacionan r = 0.97, y escolaridad e internet r = 0.94. Dado que internet y computadora miden prácticamente la misma dimensión, se retiró la segunda del modelo para no sobrerrepresentarla en las distancias; escolaridad e internet se conservaron porque capturan conceptos distintos (educación versus conectividad). Las proporciones de agua entubada, drenaje y electricidad resultaron altas en casi todo el estado, aunque el drenaje conserva variación útil (79% a 99%).

## 5. Metodología

El flujo fue: estandarización con `StandardScaler` (las variables tienen escalas distintas: proporciones, años y personas por vivienda) y posterior aplicación de **KMeans** con `n_init = 10` y semilla fija (`random_state = 42`) para garantizar reproducibilidad.

El número de grupos se evaluó con dos criterios para k entre 2 y 10: método del codo (inercia) y coeficiente de silueta. La silueta alcanza su máximo en k = 2 (0.39), pero esa solución divide el estado casi en dos bloques y diluye un estrato intermedio amplio y reconocible. Se eligió **k = 3** (silueta ≈ 0.27), donde el codo se flexiona, porque produce grupos interpretables y útiles para el contraste externo; la preferencia de la métrica por k = 2 se documenta como parte de la decisión, no se oculta.

Como herramienta explicativa se entrenó un `DecisionTreeClassifier` de profundidad máxima 3 y mínimo 5 municipios por hoja, usando la etiqueta de cluster como variable objetivo. No se dividió en entrenamiento y prueba porque el objetivo no es predecir, sino traducir las fronteras internas de KMeans a reglas legibles. La etiqueta objetivo proviene de un algoritmo y no representa una categoría oficial.

## 6. Resultados

Los tres perfiles, renombrados por su nivel de conectividad, integran 59 municipios (*alto*), 50 (*intermedio*) y 16 (*bajo*). Sus promedios municipales:

| Perfil | Municipios | Internet | Drenaje | Celular | Automóvil | Escolaridad |
|---|---|---|---|---|---|---|
| Alto | 59 | 54.4% | 98.9% | 89.6% | 44.9% | 10.2 años |
| Intermedio | 50 | 29.9% | 93.2% | 82.6% | 38.9% | 8.7 años |
| Bajo | 16 | 12.8% | 79.0% | 73.6% | 31.3% | 7.4 años |

Agua entubada y electricidad están prácticamente universalizadas en los tres grupos (98%–100%). Un caso ilustrativo: Chimalhuacán, con alrededor de 700 mil habitantes, queda en el perfil *intermedio*, lo que confirma que los grupos reflejan condiciones de vivienda y servicios, no tamaño de población.

El árbol de decisión reproduce 95.2% de la asignación. Su regla principal separa por posesión de celular (corte en 86% de las viviendas); dentro de la rama con menos celulares, un corte de internet ≤ 19% aísla casi limpiamente al estrato bajo. Las importancias concentran 93% del poder discriminatorio en cuatro variables: celular (0.54), internet (0.20), drenaje (0.19) y electricidad (0.06).

El cruce con CONAPO mostró un gradiente compatible: el perfil *alto* concentra el 100% de municipios con marginación *muy baja*; el *intermedio* se reparte entre *muy baja* (28%), *baja* (52%) y *media* (18%); y el *bajo* se integra por marginación *alta* (68.8%) y *media* (31.2%), sin ningún municipio en grados bajos. La mediana del índice es monotónica a través de los perfiles y no existe ningún caso contradictorio extremo (ningún municipio del perfil *alto* con marginación alta, ni del perfil *bajo* con marginación baja).

## 7. Interpretación

Los resultados dibujan tres configuraciones municipales coexistentes en el territorio estatal, cuyo eje diferenciador principal es la **conectividad digital junto con el drenaje**, y no el acceso a agua o electricidad, hoy casi universales. Que un árbol de pocas reglas explique 95% de los grupos indica que la segmentación descansa en diferencias simples y comunicables: cuántas viviendas tienen celular e internet define en gran medida el lugar del municipio en el mapa de condiciones.

La coincidencia con la clasificación oficial de marginación aporta consistencia externa al ejercicio, aunque debe leerse con cautela: ambas fuentes provienen del mismo censo y comparten dimensiones conceptuales, por lo que la comparación ilustra patrones compatibles y no constituye una validación independiente en sentido estricto, ni implica que KMeans mida marginación.

## 8. Limitaciones

Los datos corresponden a un corte temporal único (Censo 2020) y están agregados por municipio, por lo que ocultan heterogeneidad interna (colonias, localidades rurales). Los resultados dependen de las variables seleccionadas, del número de grupos elegido, de la estandarización y de la conversión de conteos a proporciones; decisiones distintas producirían segmentaciones distintas. La variable objetivo del árbol es una etiqueta generada por el propio KMeans, de modo que su precisión mide legibilidad, no validez externa. Los grupos no son categorías oficiales de calidad de vida, la comparación con CONAPO no establece causalidad y pueden existir variables relevantes no incluidas. Los hallazgos deben interpretarse como patrones sugeridos por los datos.

## 9. Conclusiones

Con datos públicos oficiales y métodos estándar de aprendizaje no supervisado fue posible ordenar los 125 municipios del Estado de México en tres perfiles comprensibles, cuantificar una brecha digital de gran magnitud y expresar la segmentación en reglas sencillas centradas en conectividad. La concordancia con los grados de marginación de CONAPO respalda la plausibilidad de los grupos. Como trabajo futuro se proponen la cartografía de los perfiles, la incorporación de series intercensales para observar trayectorias y la extensión del análisis a otras entidades. El notebook, los datasets procesados y todos los resultados son públicos y reproducibles en el repositorio del proyecto.

## Referencias

1. INEGI (2020). *Censo de Población y Vivienda 2020*. https://www.inegi.org.mx/programas/ccpv/2020/default.html
2. INEGI (2020). *Principales resultados por localidad (ITER), datos abiertos*. https://www.inegi.org.mx/contenidos/programas/ccpv/2020/datosabiertos/iter/iter_00_cpv2020_csv.zip
3. INEGI (2020). *Ficha técnica de datos del ITER del Censo de Población y Vivienda 2020*. https://www.inegi.org.mx/contenidos/programas/ccpv/2020/doc/fd_iter_cpv2020.pdf
4. CONAPO (2020). *Índices de marginación 2020*. https://www.gob.mx/conapo/documentos/indices-de-marginacion-2020-284372
5. CONAPO (2020). *Índice de marginación por entidad federativa y municipio 2020, base de datos municipal*. https://conapo.segob.gob.mx/work/models/CONAPO/Datos_Abiertos/Municipio/IMM_2020.xls
6. Pedregosa, F., et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research, 12*, 2825–2830. https://scikit-learn.org/stable/
7. Scikit-learn (2024). Documentación oficial: KMeans, StandardScaler, silhouette_score y DecisionTreeClassifier. https://scikit-learn.org/stable/modules/clustering.html
