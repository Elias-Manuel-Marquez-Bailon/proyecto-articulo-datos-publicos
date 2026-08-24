# ¿Qué municipios de Morelos se parecen entre sí? Una mirada con datos públicos

**Elias Manuel Marquez Bailon · Adrián Uxue Chavez Martínez · Cristian Amauri Gonzaga Castañeda · Viridiana Portilla Palestina**

Estudiantes de Ingeniería en Desarrollo y Gestión de Software, grupo 9°A.
Universidad Tecnológica de Emiliano Zapata (UTEZ).
Contacto: 20233tn068@utez.edu.mx · 20233tn093@utez.edu.mx · 20233tn102@utez.edu.mx · 20233tn092@utez.edu.mx
*(Los teléfonos de contacto se incluyen únicamente en el documento enviado a la revista.)*

Casi todos hemos hecho un viaje corto donde, al cruzar un límite municipal, el paisaje cambia de golpe: llega el pavimento, llegan las tiendas, llega el internet del celular… o todo eso desaparece. En Morelos ese contraste cabe en media hora de carretera: del corredor Cuernavaca–Jiutepec–Cuautla a las laderas del oriente o a los municipios altos del norte. Esa sensación cotidiana tiene respaldo en los números. Nosotros nos preguntamos: si miramos los datos oficiales de vivienda, servicios y conectividad, ¿qué municipios de Morelos se parecen realmente entre sí?

Para responderlo usamos información pública del Censo de Población y Vivienda 2020 del INEGI, que entrevista a los hogares de todo el país. De ahí tomamos, para cada uno de los 36 municipios del estado —incluidos los tres de nueva creación: Hueyapan, Xoxocotla y Coatetelco—, datos sencillos pero reveladores: qué porcentaje de viviendas tiene agua entubada, drenaje, luz eléctrica, internet, computadora, celular o automóvil, además de los años de escuela promedio de sus habitantes.

Con esa tabla llena de porcentajes aplicamos una técnica llamada KMeans (un método que agrupa cosas parecidas). Funciona como ordenar frutas sin leer etiquetas: sin que nadie le diga cuáles son "las manzanas", junta a los elementos que más se parecen. Antes de agrupar igualamos la escala de todas las variables para que ninguna dominara la comparación.

Probamos varias cantidades de grupos y elegimos tres, porque era la división más clara de explicar. El resultado fueron tres "Morelos" municipales conviviendo en un solo estado:

1. **Perfil alto (9 municipios):** el corredor urbano —Cuernavaca, Jiutepec, Cuautla, Temixco y compañía—, con casi seis de cada diez viviendas conectadas a internet y drenaje prácticamente universal.
2. **Perfil intermedio (7):** una sorpresa. Ahí aparecen Tepoztlán, Huitzilac y Tlayacapan, municipios con buena escuela (más de nueve años en promedio) pero donde solo ocho de cada diez viviendas tienen agua entubada, el nivel más bajo del estado.
3. **Perfil bajo (20):** poco más de un tercio de las viviendas con internet, y aquí se encuentra el caso extremo estatal: Hueyapan, donde apenas la mitad de las viviendas tiene drenaje.

La cifra más llamativa es la brecha digital: en Hueyapan solo 23 de cada 100 viviendas tienen internet; en Cuernavaca son 73 de cada 100. Tres veces más oportunidades de estudiar, trabajar o tramitar en línea según el municipio donde se nazca.

Luego pedimos ayuda a otra herramienta, un árbol de decisión (una especie de lista de preguntas tipo "¿el drenaje llega a casi todas las viviendas?"). Este árbol reprodujo 97% de los grupos con dos preguntas sencillas: primero el drenaje, después el agua entubada. La conectividad ordena el gradiente entre municipios, pero lo que separa unos grupos de otros son los servicios básicos que todavía no llegan a todos. Es decir, hoy la plomería —no el celular— distingue mejor a los municipios de Morelos.

Finalmente contrastamos nuestros grupos con los grados de marginación que calcula el CONAPO, un organismo oficial con su propia metodología. La coincidencia fue parcial e interesante: todos los municipios de nuestro perfil alto están en el grado de marginación muy baja, y Morelos no registra ningún municipio con marginación alta o muy alta; sin embargo, buena parte del perfil bajo también figura oficialmente en grados bajos. Dos miradas contaron historias parecidas en los extremos, pero distintas en la franja media del estado.

¿Qué significa esto? Los grupos no son categorías oficiales ni calificaciones morales a los municipios: son patrones sugeridos por los datos, una fotografía tomada en 2020. Aun así, son útiles: muestran dónde se concentra la falta de conectividad y dónde el rezago sigue siendo de infraestructura hidráulica, y podrían orientar dónde invertir primero, ya sea en red de drenaje o en internet para las escuelas.

Detrás de este artículo hay un ejercicio más grande y totalmente verificable: el análisis completo, paso a paso, está publicado en un repositorio público del equipo, con los datos originales, el código y los resultados. Cualquier persona puede repetirlo y llegar a las mismas cifras. Esa es una de las mejores cualidades de la ciencia: que cualquiera pueda revisarla.
