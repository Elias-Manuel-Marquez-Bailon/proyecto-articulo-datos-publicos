# ¿Qué municipios del Estado de México se parecen entre sí? Una mirada con datos públicos

**Elias Manuel Marquez Bailon · Adrián Uxue Chavez Martínez · Cristian Amauri Gonzaga Castañeda · Viridiana Portilla Palestina**

Estudiantes de Ingeniería en Desarrollo y Gestión de Software, grupo 9°A.
Universidad Tecnológica de Emiliano Zapata (UTEZ).
Contacto: 20233tn068@utez.edu.mx · 20233tn093@utez.edu.mx · 20233tn102@utez.edu.mx · 20233tn092@utez.edu.mx
*(Los teléfonos de contacto se incluyen únicamente en el documento enviado a la revista.)*

Casi todos hemos hecho un viaje corto donde, al cruzar un límite municipal, el paisaje cambia de golpe: llega el pavimento, llegan las tiendas, llega el internet del celular… o todo eso desaparece. Esa sensación cotidiana tiene respaldo en los números. Nosotros nos preguntamos: si miramos los datos oficiales de vivienda, servicios y conectividad, ¿qué municipios del Estado de México se parecen realmente entre sí?

Para responderlo usamos información pública del Censo de Población y Vivienda 2020 del INEGI, que entrevista a los hogares de todo el país. De ahí tomamos, para cada uno de los 125 municipios del estado, datos sencillos pero reveladores: qué porcentaje de viviendas tiene agua entubada, drenaje, luz eléctrica, internet, computadora, celular o automóvil, además de los años de escuela promedio de sus habitantes.

Con esa tabla llena de porcentajes aplicamos una técnica llamada KMeans (un método que agrupa cosas parecidas). Funciona como ordenar frutas sin leer etiquetas: sin que nadie le diga cuáles son "las manzanas", junta a los elementos que más se parecen. Antes de agrupar igualamos la escala de todas las variables para que ninguna dominara la comparación.

Probamos varias cantidades de grupos y elegimos tres, porque era la división más clara de explicar. El resultado fueron tres "Méxicos" municipales conviviendo en un solo estado:

1. **Perfil alto (59 municipios):** más de la mitad de las viviendas con internet, drenaje y celular casi universales, alrededor de diez años de escuela.
2. **Perfil intermedio (50):** cerca de tres de cada diez viviendas con internet, buenos servicios básicos, ocho años y medio de escuela.
3. **Perfil bajo (16):** apenas una de cada ocho viviendas conectadas a internet, cuatro de cinco con drenaje, siete años de escuela.

La cifra más llamativa es la brecha digital: en Ixtapan del Oro solo 4 de cada 100 viviendas tienen internet; en Coacalco son 76 de cada 100. Veinte veces menos oportunidades de estudiar, trabajar o tramitar en línea.

Luego pedimos ayuda a otra herramienta, un árbol de decisión (una especie de lista de preguntas tipo "¿tiene celular la mayoría de las viviendas?"). Este árbol logró reproducir 95% de los grupos con reglas simples: la pregunta clave resultó ser el celular en la vivienda, seguida por el internet. Es decir, hoy la conectividad distingue mejor a los municipios que otros servicios que ya casi todos tienen, como agua entubada o electricidad.

Finalmente contrastamos nuestros grupos con los grados de marginación que calcula el CONAPO, un organismo oficial con su propia metodología. La coincidencia fue notable: los municipios de nuestro perfil alto están todos en el grado de marginación muy baja, y los del perfil bajo se concentran en marginación alta o media. Dos miradas independientes contaron una historia parecida.

¿Qué significa esto? Los grupos no son categorías oficiales ni calificaciones morales a los municipios: son patrones sugeridos por los datos, una fotografía tomada en 2020. Aun así, son útiles: muestran dónde se concentra la falta de conectividad y podrían orientar dónde invertir primero en internet, escuelas conectadas y trámites digitales.

Detrás de este artículo hay un ejercicio más grande y totalmente verificable: el análisis completo, paso a paso, está publicado en un repositorio público del equipo, con los datos originales, el código y los resultados. Cualquier persona puede repetirlo y llegar a las mismas cifras. Esa es una de las mejores cualidades de la ciencia: que cualquiera pueda revisarla.

