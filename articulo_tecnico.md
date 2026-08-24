# Segmentación de los municipios de Morelos según condiciones de vivienda, servicios y conectividad mediante KMeans

**Gonzaga Castañeda Cristian Amauri · Chavez Martinez Adrian Uxue · Marquez Bailon Elias Manuel · Portilla Palestina Viridiana**

Grupo 9°A — Ingeniería en Desarrollo y Gestión de Software (IDGS), Universidad Tecnológica de Emiliano Zapata (UTEZ)

## Resumen

Este artículo aplica aprendizaje no supervisado a datos públicos del Censo de Población y Vivienda 2020 para segmentar los 36 municipios de Morelos según sus condiciones de vivienda, acceso a servicios básicos y conectividad digital. Tras expresar los conteos como proporciones municipales, se estandarizaron ocho indicadores y se entrenó KMeans, eligiendo tres grupos con el método del codo y el coeficiente de silueta. Los perfiles resultantes corresponden a niveles alto (9 municipios), intermedio (7) y bajo (20) de equipamiento urbano, con una brecha digital en el acceso a internet que va de 22.9% de las viviendas en Hueyapan a 73.1% en Cuernavaca. Un árbol de decisión de profundidad dos reproduce 97.2% de la asignación de grupos e identifica a la infraestructura hidráulica —drenaje y agua entubada— como el eje discriminante, por encima de la conectividad. La comparación con la marginación municipal 2020 de CONAPO muestra coincidencia parcial: el perfil alto concentra el 100% de los municipios con marginación muy baja, Morelos no registra grados altos o muy altos y las medianas del índice de los perfiles bajo e intermedio son casi idénticas. Los resultados describen patrones territoriales sugerentes para la focalización de políticas públicas, aunque no constituyen categorías oficiales.

**Palabras clave:** clustering, KMeans, municipios, Censo 2020, conectividad, marginación.

## 1. Introducción

Morelos es una entidad compacta —36 municipios— con contrastes territoriales marcados: el corredor urbano Cuernavaca–Jiutepec–Cuautla concentra servicios e infraestructura, mientras las zonas altas del norte y los municipios del oriente y sur conservan localidades rurales. A ello se suma un rasgo institucional reciente: tres municipios de nueva creación (Hueyapan, Xoxocotla y Coatetelco), que desde el Censo 2020 cuentan con estadísticas propias. Entender qué municipios comparten condiciones parecidas de vivienda, servicios y conectividad es útil para diseñar políticas públicas diferenciadas y priorizar inversión.

Este trabajo responde a la pregunta guía: *¿qué municipios de Morelos presentan características similares en sus condiciones de vivienda, acceso a servicios y conectividad?* Para ello se aplicó segmentación con KMeans sobre indicadores censales municipales, se utilizó un árbol de decisión como herramienta de interpretación y se contrastaron los grupos con el índice de marginación municipal de CONAPO. El alcance es deliberadamente acotado —36 observaciones de una sola entidad—, con fuentes oficiales y un flujo de trabajo completamente reproducible (semilla fija y datos separados en crudo y procesados).

## 2. Fuente de datos

La fuente principal es el **ITER 2020** (Principales Resultados por Localidad) del **Censo de Población y Vivienda 2020 de INEGI**, descargado del sitio oficial de datos abiertos. El ITER reporta, para cada municipio, conteos de población y vivienda junto con indicadores de educación, servicios y bienes en el hogar; es una fuente oficial, gratuita y documentada con ficha técnica y diccionario de datos, que trabaja directamente al nivel municipal.

Como fuente complementaria se emplearon los **Índices de Marginación 2020 de CONAPO**, que asignan a cada municipio un índice y un grado de marginación en cinco categorías, utilizados exclusivamente como referencia externa para contrastar los grupos, no como entrada del modelo; el cruce por clave municipal (`17000 + MUN`) verificó población idéntica entre ambas fuentes en los 36 municipios.

## 3. Preparación de datos

Del archivo nacional del ITER se filtraron los registros municipales (localidad `"0000"`) de la entidad 17, excluyendo la fila de total estatal, lo que arroja exactamente **36 municipios**, incluidos los tres de reciente creación, verificado programáticamente. Se revisaron tipos de dato y valores especiales (`*`, N/D) conforme al diccionario oficial, sin valores faltantes en las columnas seleccionadas.

Las proporciones se construyeron dividiendo los conteos de viviendas con cada atributo (`VPH_*`) entre las viviendas particulares habitadas *con características de ocupantes* (`VIVPARH_CV`), denominador que garantiza valores acotados al rango [0, 1], condición verificada programáticamente para los 36 municipios.

El conjunto de variables quedó integrado por siete proporciones (agua entubada, drenaje, electricidad, internet, computadora, celular y automóvil en la vivienda), la escolaridad promedio (`GRAPROES`, en años) y los ocupantes promedio por vivienda (`PROM_OCUP`). La población total se conservó solo como variable descriptiva, fuera del modelo, para evitar que el tamaño de los municipios dominara el cálculo de similitudes. El resultado fue un dataset procesado de 36 filas por 22 columnas, sin valores nulos.

## 4. Análisis exploratorio

La exploración evidenció dos hechos. Primero, una **brecha digital considerable**: la proporción de viviendas con internet va de 22.9% en Hueyapan a 73.1% en Cuernavaca, poco más de tres veces; la escolaridad promedio acompaña ese gradiente (7.4 frente a 11.4 años aprobados; el mínimo estatal lo registra Coatetelco con 6.9). Segundo, una **multicolinealidad fuerte**: internet y computadora correlacionan r = 0.95, y escolaridad e internet r = 0.87. Dado que internet y computadora miden prácticamente la misma dimensión, se retiró la segunda del modelo; escolaridad e internet se conservaron porque capturan conceptos distintos (educación versus conectividad).

Los servicios básicos aparecen casi universalizados: electricidad (98.9% a 99.8%) y agua entubada en su mayoría alta, aunque con un caso extremo en Tlalnepantla (66.5%). El drenaje conserva la mayor variación útil del bloque hidráulico: de 52.3% en Hueyapan a 99.6% en Cuernavaca.

## 5. Metodología

El flujo fue: estandarización con `StandardScaler` (las variables tienen escalas distintas: proporciones, años y personas por vivienda) y posterior aplicación de **KMeans** con `n_init = 10` y semilla fija (`random_state = 42`) para garantizar reproducibilidad.

El número de grupos se evaluó con dos criterios para k entre 2 y 10: método del codo (inercia) y coeficiente de silueta. La silueta alcanza su máximo en k = 5 (0.303), pero esa solución produce grupos de solo 1 y 2 municipios —uno quedaría integrado únicamente por Hueyapan, aislado por su drenaje extremadamente bajo—, lo que no es interpretable ni útil. Se eligió **k = 3** (silueta = 0.273), donde el codo se flexiona, porque genera grupos interpretables y útiles para el contraste externo; la preferencia de la métrica por k = 5 queda documentada como parte de la decisión.

Como herramienta explicativa se entrenó un `DecisionTreeClassifier` de profundidad máxima 3 y mínimo 5 municipios por hoja, usando la etiqueta de cluster como variable objetivo; no se dividió en entrenamiento y prueba porque el objetivo no es predecir, sino traducir las fronteras internas de KMeans a reglas legibles. La etiqueta proviene de un algoritmo y no representa una categoría oficial.

## 6. Resultados

Los tres perfiles, renombrados por su nivel de conectividad, integran 9 municipios (*alto*), 7 (*intermedio*) y 20 (*bajo*). Sus promedios municipales:

| Perfil | Municipios | Agua entubada | Drenaje | Internet | Celular | Automóvil | Escolaridad |
|---|---|---|---|---|---|---|---|
| Alto | 9 | 97.5% | 99.2% | 58.7% | 90.6% | 42.3% | 10.0 años |
| Intermedio | 7 | 79.8% | 94.1% | 39.1% | 88.2% | 43.0% | 9.2 años |
| Bajo | 20 | 96.0% | 94.2% | 36.2% | 82.8% | 33.7% | 8.6 años |

Electricidad está prácticamente universalizada en los tres grupos (98.9%–99.6%). El perfil *alto* corresponde al corredor urbano (Cuernavaca, Jiutepec, Cuautla, Temixco, Emiliano Zapata, Xochitepec, Yautepec, Zacatepec y Jojutla). El perfil *intermedio* es el más contraintuitivo: agrupa a Tepoztlán, Huitzilac, Tlayacapan, Atlatlahucan, Tlalnepantla, Totolapan y Jantetelco, municipios con buena escolaridad (9.2 años) e internet comparable al del perfil bajo, pero cuyo rasgo distintivo es el menor acceso a agua entubada (79.8%). En el perfil *bajo*, Hueyapan aparece como caso extremo estatal: 52.3% de drenaje y 22.9% de internet. Que municipios prominentes queden fuera del perfil alto confirma que los grupos reflejan condiciones de vivienda y servicios, no tamaño ni reputación.

El árbol de decisión reproduce 97.2% de la asignación (35 de 36 municipios) con profundidad efectiva 2 y tres hojas. Su regla principal separa por drenaje (corte en 98% de las viviendas): por encima, todos los municipios son perfil *alto*; por debajo, un corte de agua entubada en 91% distingue al perfil *intermedio* del *bajo*. Las importancias se concentran en dos variables: drenaje (0.56) y agua entubada (0.44); ninguna variable de conectividad aporta a las fronteras. Solo Xoxocotla queda mal clasificado: su drenaje (98.0%) cae justo en el borde del corte principal.

El cruce con CONAPO mostró coincidencia parcial. Morelos no registra municipios con marginación *alta* ni *muy alta* (12 *muy baja*, 19 *baja*, 5 *media*). El perfil *alto* concentra el 100% de marginación *muy baja*; el *intermedio* se compone de *baja* (71.4%) y *media* (28.6%); y el *bajo* integra *muy baja* (15%), *baja* (70%) y *media* (15%). Sin embargo, la mediana del índice no es monotónica entre los dos perfiles inferiores (bajo 55.74 ≈ intermedio 55.39, frente a 57.96 del alto), y 17 de los 20 municipios del perfil *bajo* se ubican en grados oficiales bajos: la lectura de KMeans (equipamiento de la vivienda) y la de CONAPO (educación, ingresos, ocupación) coinciden en los extremos pero divergen en la franja media del estado.

## 7. Interpretación

Los resultados dibujan tres configuraciones municipales coexistentes en el territorio, cuyo eje diferenciador principal es la **infraestructura hidráulica** —drenaje primero, agua entubada después— y no la conectividad, pese a que el gradiente interno de internet acompaña a la escolaridad (r = 0.87). La conectividad ordena el espectro municipal; las fronteras entre grupos las marcan los servicios básicos aún no universalizados. Que un árbol de dos niveles explique 97% de los grupos indica que la segmentación descansa en diferencias simples y comunicables.

La comparación con la clasificación oficial de marginación debe leerse con cautela: ambas fuentes provienen del mismo censo y comparten dimensiones conceptuales, y la coincidencia es parcial: ilustra patrones compatibles, no constituye una validación independiente ni implica que KMeans mida marginación.

## 8. Limitaciones

Los datos corresponden a un corte temporal único (Censo 2020) y están agregados por municipio, por lo que ocultan heterogeneidad interna (colonias, localidades rurales). Los resultados dependen de las variables seleccionadas, del número de grupos elegido, de la estandarización y de la conversión de conteos a proporciones; decisiones distintas producirían segmentaciones distintas. Con solo 36 observaciones, los clusters son particularmente sensibles a casos extremos como Hueyapan. La variable objetivo del árbol es una etiqueta generada por el propio KMeans, de modo que su precisión mide legibilidad, no validez externa. Los grupos no son categorías oficiales de calidad de vida, la comparación con CONAPO no establece causalidad y pueden existir variables relevantes no incluidas; los hallazgos deben interpretarse como patrones sugeridos por los datos.

## 9. Conclusiones

Con datos públicos oficiales y métodos estándar de aprendizaje no supervisado fue posible ordenar los 36 municipios de Morelos en tres perfiles comprensibles, cuantificar una brecha digital considerable (23% a 73% de viviendas con internet) y expresar la segmentación en reglas sencillas centradas en la infraestructura hidráulica. La concordancia parcial con los grados de marginación de CONAPO respalda la plausibilidad de los grupos en sus extremos y advierte sobre la franja media, donde equipamiento urbano y marginación oficial cuentan historias distintas. Como trabajo futuro se proponen cartografiar los perfiles, incorporar series intercensales —que permitirán observar la trayectoria de los municipios de nueva creación— y extender el análisis a otras entidades. El notebook, los datasets procesados y todos los resultados son públicos y reproducibles en el repositorio del proyecto.

## Referencias

1. INEGI (2020). *Censo de Población y Vivienda 2020*. https://www.inegi.org.mx/programas/ccpv/2020/default.html
2. INEGI (2020). *Principales resultados por localidad (ITER), datos abiertos*. https://www.inegi.org.mx/contenidos/programas/ccpv/2020/datosabiertos/iter/iter_00_cpv2020_csv.zip
3. INEGI (2020). *Ficha técnica de datos del ITER del Censo de Población y Vivienda 2020*. https://www.inegi.org.mx/contenidos/programas/ccpv/2020/doc/fd_iter_cpv2020.pdf
4. CONAPO (2020). *Índices de marginación 2020*. https://www.gob.mx/conapo/documentos/indices-de-marginacion-2020-284372
5. CONAPO (2020). *Índice de marginación por entidad federativa y municipio 2020, base de datos municipal*. https://conapo.segob.gob.mx/work/models/CONAPO/Datos_Abiertos/Municipio/IMM_2020.xls
6. Pedregosa, F., et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research, 12*, 2825–2830. https://scikit-learn.org/stable/
7. Scikit-learn (2024). Documentación oficial: KMeans, StandardScaler, silhouette_score y DecisionTreeClassifier. https://scikit-learn.org/stable/modules/clustering.html
