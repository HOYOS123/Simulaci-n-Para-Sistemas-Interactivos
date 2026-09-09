# Unidad 2

---

## Actividad 04: Diseño Generativo

### **¿Qué es el diseño generativo?**

El diseño generativo consiste en diseñar un **sistema capaz de producir múltiples resultados**, en lugar de diseñar una única imagen o animación final.

Para esto, el diseñador no controla directamente cada elemento visual. En cambio, define una intención, un conjunto de entidades, las relaciones entre ellas y las reglas que determinan cómo evolucionará el sistema. 
De esta forma, cada ejecución puede producir un resultado diferente, pero todos conservan la misma identidad conceptual.

Como plantea Patrick Hübner, la unidad de diseño deja de ser la imagen y pasa a ser el **conjunto de relaciones** que generan esa imagen.

---

### **¿Qué es Particle Life desde el diseño generativo?**

Particle Life es un ejemplo claro de diseño generativo, donde en lugar de decidir manualmente la posición de cada partícula, el diseñador define:

- Las especies de partículas.
- Qué especies se atraen.
- Qué especies se repelen.
- La intensidad de esas fuerzas.
- La cantidad de partículas.

A partir de estas reglas, el sistema genera comportamientos emergentes de manera autónoma.

---

## Las ocho operaciones de la mentalidad generativa aplicadas a Particle Life

### 1. Intención

**¿Qué quiero comunicar?**

La intención es la idea, emoción o transformación que debe experimentar quien observa el sistema.

Ejemplos:

- Calma.
- Ansiedad.
- Cooperación.
- Conflicto.
- Evolución.
- Caos.
- Equilibrio.

---

### 2. Entidades

Las entidades son los elementos que existen dentro del sistema.

En Particle Life normalmente son diferentes especies de partículas.

Ejemplo:

- Roja (Personas) y Azul (Problemas): Los problemas atraen a las personas (las absorben), y las personas intentan repeler o huir de los problemas a cierta distancia.
- Roja (Personas) y Verde (Oportunidades): Las personas se sienten fuertemente atraídas por las oportunidades. Las oportunidades pueden ser estáticas o moverse hacia las personas.
- Amarilla (Esperanza): Podría actuar como un elemento neutralizador. Por ejemplo, la esperanza atrae a las personas y repele a los problemas, alejándolos de ellas.

Aunque es muy metafórico se podría ver de esta forma.

---

### 3. Relaciones

Las relaciones describen cómo interactúan las entidades.

Ejemplos:

- Las partículas rojas atraen a las verdes.
- Las rojas repelen a las azules.
- Las azules se atraen entre sí.
- Las verdes estabilizan el sistema.

Las relaciones son el corazón del diseño generativo.

---

### 4. Entradas

Son los elementos que modifican el comportamiento del sistema. Estos pueden ser:

- Tiempo.
- Mouse.
- Teclado.
- Audio.
- Datos.
- Aleatoriedad.

---

### 5. Reglas

Las reglas determinan cómo cambia el sistema en cada instante. Por ejemplo:

- Rojo → Verde = Atracción fuerte.
- Rojo → Azul = Repulsión.
- Azul → Azul = Atracción moderada.
- Verde → Todas = Estabilización.

---

### 6. Invariantes

Son las características que nunca cambian y conservan la identidad del sistema. Ejemplos:

- Siempre existen cuatro especies.
- Siempre hay fuerzas de atracción y repulsión.
- El sistema siempre produce agrupaciones.

---

### 7. Variabilidad

Son los aspectos que cambian en cada ejecución. Ejemplos:

- Posición inicial de las partículas.
- Cantidad de partículas.
- Semilla aleatoria.
- Velocidad inicial.

Gracias a esta variabilidad, cada simulación es diferente.

---

### 8. Curaduría y reflexión

Después de ejecutar el sistema, el diseñador analiza el resultado. Se pregunta:

- ¿El comportamiento comunica la intención?
- ¿El resultado es significativo?
- ¿Qué reglas deben modificarse?

El objetivo no es aceptar cualquier resultado, sino ajustar el sistema hasta lograr el comportamiento deseado.

---

# Actividad 05: Reto de diseño

## Intención - ¿Qué quería explorar?

Quise explorar la tensión entre **la cohesión y la fragmentación**.

Mi idea era que las partículas intentaran formar grupos, pero que esos grupos nunca pudieran quedarse iguales durante toda la simulación. 

Quería que siempre estuvieran cambiando, que unas partículas entraran, otras salieran y que el sistema nunca llegara a estar completamente quieto.

La intención no depende de los colores, sino de cómo se atraen o se rechazan entre ellas.

---

## Diseño del sistema

Utilicé **tres** tipos de partículas.

- Rojas
- Amarillas
- Azules

Cada una tiene un comportamiento diferente según la matriz de relaciones.

**¿Por qué?**

Seleccioné tres tipos porque quería que hubiera diferentes "roles" dentro del sistema y que no todas reaccionaran igual.

---

### Cantidad de partículas

Trabajé con aproximadamente **120 partículas**.

**¿Por qué?**

Al principio tenía más, pero era difícil entender qué estaba pasando. Con 120 todavía se veían muchos movimientos, pero era más fácil observar cómo se formaban y rompían los grupos.

---

### Matriz de relaciones

La matriz fue la parte más importante del ejercicio.

Hice que algunas partículas se atrajeran mucho, otras muy poco y otras se rechazaran.

La relación más importante fue entre las partículas rojas y amarillas.

Las amarillas buscan acercarse mucho a las rojas, pero las rojas no responden igual y tienden a rechazarlas.

Eso hace que nunca exista una estabilidad completa.

**¿Por qué?**

Quería que el comportamiento dependiera de las reglas y no de los colores.

---

### Intensidad de las relaciones

Fui probando diferentes intensidades.

Al principio casi todas estaban en atracción máxima y el sistema terminaba formando un solo grupo.

Después fui bajando algunas relaciones hasta encontrar un punto donde los grupos aparecían y desaparecían constantemente.

**¿Por qué?**

Porque quería que hubiera movimiento continuo sin que todo terminara completamente unido o completamente separado.

---

### Distancia de interacción

También probé cambiando el radio de interacción.

Cuando era muy pequeño las partículas casi no reaccionaban entre ellas.

Cuando lo aumenté empezaron a formarse agrupaciones más interesantes.

---

### Fricción

La fricción la dejé muy parecida a la original.

Hice algunas pruebas cambiándola, pero vi que afectaba más la velocidad del movimiento que la forma como se organizaban las partículas.

---

### Distribución inicial

Utilicé la distribución centrada. Así todas las partículas comenzaban bajo las mismas condiciones.

---

### Parámetros constantes

Durante la simulación mantuve:

- tres tipos de partículas,
- los límites periódicos,
- la forma circular de las partículas.

---

### Parámetros que fui cambiando

Durante las pruebas cambié principalmente:

- la cantidad de partículas,
- la matriz,
- el radio de interacción,
- la atracción entre las partículas rojas.

Fueron los parámetros que más cambiaban el comportamiento del sistema.

---

## Registro de pruebas

### Prueba 1

Comencé usando la configuración inicial del simulador.

Las partículas terminaban formando un grupo muy grande y después casi no cambiaban.

No era el comportamiento que buscaba.

<img width="1240" height="998" alt="image" src="https://github.com/user-attachments/assets/cafd1206-d6b3-4883-9d15-c199fe4c5f5a" />


---

### Prueba 2

Empecé a modificar la matriz.

Noté que pequeños cambios hacían una diferencia muy grande en el movimiento.

https://github.com/user-attachments/assets/ecf475ef-2d2c-49ee-b0f4-eb434458172c

---

### Prueba 3

Probé una relación asimétrica.

Las amarillas buscaban acercarse mucho a las rojas, mientras que las rojas no hacían lo mismo.

Ese cambio hizo que el sistema empezara a reorganizarse constantemente.

---

### Prueba 4

Bajé demasiado la atracción entre las partículas rojas.

Los grupos desaparecieron muy rápido y el sistema perdió la forma que tenía.

Por eso descarté esa configuración.

---

### Prueba 5 (resultado final)

Volví a aumentar un poco la cohesión entre las rojas.

Con ese cambio aparecieron grupos que duraban algunos segundos, luego se rompían y después se formaban otros diferentes.

Ese fue el resultado que decidí conservar.

[Video en Youtube](https://youtu.be/QXYXtTWGfmA)

---

### Lo que aprendí

Lo que más me sorprendió fue que cambiar un solo valor de la matriz podía cambiar completamente el comportamiento del sistema.

También entendí que el objetivo no era hacer una animación bonita, sino diseñar unas reglas que produjeran comportamientos interesantes.

---

### Autoevaluación

Creo que logré representar la idea que tenía al comienzo.

Durante el proceso hice varias pruebas, descarté configuraciones que no funcionaban y fui ajustando la matriz hasta encontrar un comportamiento que se mantuviera cambiando sin perder completamente su identidad.

Todavía siento que podría seguir mejorándolo, pero considero que el sistema cumple con la intención que me propuse y con los requisitos de la actividad.

Nota: 5.0
