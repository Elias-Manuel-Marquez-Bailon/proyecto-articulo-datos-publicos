# ¿Qué municipios de Morelos se parecen entre sí? Una mirada con datos públicos

**Elías Manuel Márquez Bailón · Adrián Uxue Chavez Martínez · Cristian Amauri Gonzaga Castañeda · Viridiana Portilla Palestina**

Estudiantes de Ingeniería en Desarrollo y Gestión de Software, 9.º semestre.
Universidad Tecnológica de Emiliano Zapata (UTEZ), Emiliano Zapata, Morelos.
Contacto: 20233tn068@utez.edu.mx · 20233tn093@utez.edu.mx · 20233tn102@utez.edu.mx · 20233tn092@utez.edu.mx
*(Los teléfonos de contacto se agregan únicamente al documento enviado a la revista.)*

Casi todos hemos hecho un viaje corto donde, al cruzar un límite municipal, el paisaje cambia de golpe: llega el pavimento, llegan las tiendas, llega el internet del celular… o todo eso desaparece. En Morelos ese contraste cabe en media hora de carretera: del corredor Cuernavaca–Jiutepec–Cuautla a las laderas del oriente o a los municipios altos del norte. Nosotros nos preguntamos: si miramos los datos oficiales, ¿qué municipios se parecen realmente entre sí?

Nuestro objetivo fue responder esa pregunta con números y no con impresiones. Analizamos los 36 municipios del estado —incluidos tres de nueva creación: Hueyapan, Xoxocotla y Coatetelco— con información pública del Censo 2020 del Instituto Nacional de Estadística y Geografía (INEGI). De cada municipio tomamos datos sencillos pero reveladores: qué porcentaje de viviendas tiene agua entubada, drenaje, luz eléctrica, internet, computadora, celular o automóvil, además de los años de escuela promedio de sus habitantes.

Con esa tabla aplicamos KMeans, una técnica que agrupa cosas parecidas sin que nadie le diga de antemano cuáles son "las manzanas" ni cuáles "las peras". Antes de agrupar igualamos la escala de todas las variables para que ninguna dominara la comparación. Probamos varias cantidades de grupos y elegimos tres, la división más clara de explicar. El resultado fueron tres "Morelos" conviviendo en un solo estado:

1. **Perfil alto (9 municipios):** el corredor urbano, con casi seis de cada diez viviendas conectadas a internet.
2. **Perfil intermedio (7):** la sorpresa. Ahí están Tepoztlán, Huitzilac y Tlayacapan, con buena escuela, pero donde solo ocho de cada diez viviendas tienen agua entubada, lo más bajo del estado.
3. **Perfil bajo (20):** un tercio de las viviendas con internet. Aquí está Hueyapan, caso extremo donde apenas la mitad tiene drenaje.

La cifra más llamativa es la brecha digital: en Hueyapan solo 23 de cada 100 viviendas tienen internet; en Cuernavaca son 73. Tres veces más oportunidades de estudiar, trabajar o tramitar en línea según el municipio donde se nazca.

Luego usamos un árbol de decisión, una especie de lista de preguntas tipo "¿el drenaje llega a casi todas las viviendas?", que reprodujo 97% de los grupos con solo dos preguntas: primero drenaje, después agua entubada. Es decir, hoy la plomería distingue mejor a los municipios de Morelos que el celular.

Al contrastar nuestros grupos con la medición oficial de marginación del Consejo Nacional de Población (CONAPO), la coincidencia fue parcial e interesante: todos los municipios del perfil alto están en marginación muy baja, pero buena parte del perfil bajo también figura en grados bajos oficiales. Dos miradas parecidas en los extremos, distintas en la franja media del estado.

Estos grupos no son categorías oficiales ni calificaciones morales: son patrones sugeridos por una fotografía tomada en 2020. Aun así, son útiles: muestran dónde falta conectividad y dónde el rezago sigue siendo de infraestructura hidráulica, y podrían orientar dónde invertir primero, si en red de drenaje o en internet para las escuelas.

Detrás del artículo hay un ejercicio totalmente verificable: el análisis completo, paso a paso, está publicado en un repositorio público del equipo, con los datos originales, el código y los resultados. Cualquier persona puede repetirlo y llegar a las mismas cifras. Esa es una de las mejores cualidades de la ciencia: que cualquiera pueda revisarla.
