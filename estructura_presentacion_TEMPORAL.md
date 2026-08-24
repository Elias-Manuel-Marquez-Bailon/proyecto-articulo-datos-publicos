# Estructura inicial de la presentación (TEMPORAL)

> Archivo de trabajo para armar la presentación de defensa (5–7 min). Se puede eliminar cuando las diapositivas estén terminadas.

**Regla general:** máximo 6 líneas de texto por diapositiva; las cifras hablan solas; quien expone complementa.

---

## Diapositiva 1 — Portada (30 s)

- Título: Segmentación de los municipios de Morelos según condiciones de vivienda, servicios y conectividad mediante KMeans
- Materia: Extracción de Conocimiento en Bases de Datos
- Grupo 9°A IDGS · UTEZ
- Integrantes: Gonzaga Castañeda Cristian Amauri · Chavez Martinez Adrian Uxue · Marquez Bailon Elias Manuel · Portilla Palestina Viridiana

## Diapositiva 2 — Pregunta guía y objetivo (45 s)

- ¿Qué municipios de Morelos se parecen en vivienda, servicios y conectividad?
- Objetivo: agrupar los 36 municipios con datos públicos reales, sin etiquetas previas

## Diapositiva 3 — Datos (45 s)

- Fuente principal: INEGI, Censo 2020 (ITER) → 36 municipios, incluidos Hueyapan, Xoxocotla y Coatetelco (de nueva creación)
- Validación externa: marginación CONAPO 2020
- Variables: % de viviendas con agua entubada, drenaje, luz, internet, celular, automóvil + escolaridad promedio y ocupantes por vivienda

## Diapositiva 4 — Método (60 s)

- Conteos convertidos a proporciones → estandarización (StandardScaler)
- KMeans con semilla fija 42 (reproducible)
- Elección de k = 3: codo + silueta (k = 5 daba grupos de 1–2 municipios, inservible)
- Imagen: `imagenes/grafica_6.png`

## Diapositiva 5 — Resultado: los tres perfiles (75 s) ⭐ diapositiva clave

- Alto: 9 · Intermedio: 7 · Bajo: 20
- Sorpresa: Tepoztlán/Huitzilac/Tlayacapan en intermedio por menor acceso a agua entubada (79.8%) pese a buena escolaridad
- Imagen: `imagenes/grafica_7.png` (incluye los nombres de todos los municipios)

## Diapositiva 6 — Brecha digital (45 s)

- Internet: de 22.9% (Hueyapan) a 73.1% (Cuernavaca)
- Escolaridad acompaña el gradiente (r = 0.87)
- Imagen: `imagenes/grafica_3.png` o `grafica_4.png`

## Diapositiva 7 — El hallazgo: el árbol explicativo (75 s)

- Árbol de decisión de 2 niveles reproduce 97.2% de los grupos
- Regla principal: drenaje > 98% → perfil alto; si no, agua entubada ≤ 91% separa intermedio de bajo
- Mensaje clave: **en Morelos distingue la plomería, no el celular** (drenaje 0.56 y agua 0.44 de importancia; conectividad en 0)
- Imagen: `imagenes/grafica_9.png`

## Diapositiva 8 — Validación CONAPO (60 s)

- Morelos no registra municipios con marginación Alta ni Muy alta (12 Muy baja, 19 Baja, 5 Media)
- Perfil alto = 100% marginación muy baja, pero coincidencia PARCIAL en la franja media (medianas: alto 57.96 ≳ bajo 55.74 ≈ intermedio 55.39)
- Honestidad científica: coincidencia parcial ≠ validación absoluta
- Imagen: `imagenes/grafica_10.png`

## Diapositiva 9 — Limitaciones y cierre (45 s)

- Fotografía de 2020; datos por municipio (ocultan colonias/localidades); sensible a casos extremos como Hueyapan
- Los grupos no son categorías oficiales
- Cierre: "Todo es reproducible: notebook público con datos, código y resultados"

---

## Reparto sugerido (4 integrantes)

| Integrante | Diapositivas |
|---|---|
| A | 1–3 |
| B | 4–5 |
| C | 6–7 |
| D | 8–9 |

## Cifras fuertes para memorizar

1. **36** municipios (entidad 17)
2. **k = 3** (silueta 0.273; se descartó k = 5 aunque maximizaba la silueta)
3. Brecha digital: **22.9% → 73.1%**
4. Árbol: profundidad **2**, precisión **97.2%**
5. Eje diferenciador: **drenaje/agua > conectividad**

Todas las imágenes están en `imagenes/` del repositorio.
