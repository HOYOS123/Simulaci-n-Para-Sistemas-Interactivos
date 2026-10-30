# WHY BOTHER?
Enlace al proyecto: https://hoyos123.github.io/Unidad-8-Simulacion-WHY-BOTHER-/

### Una exploración sobre la creación, el esfuerzo y la inteligencia artificial mediante simulación computacional.

## 1. Introducción

El proyecto WHY BOTHER? surge a partir de la pregunta propuesta en la actividad: ¿Para qué tomarnos el trabajo de crear, aprender y esforzarnos cuando actualmente podemos delegar muchas de esas tareas a sistemas de inteligencia artificial?

La intención de este ejercicio no es demostrar que la inteligencia artificial puede producir resultados, sino cuestionar qué sucede con el proceso creativo cuando tenemos la posibilidad de obtener esos resultados de manera casi inmediata.

A partir de esta reflexión, decidí desarrollar una simulación computacional interactiva basada en sistemas de partículas. Mediante diferentes comportamientos y formas de interacción, la obra explora tres maneras de relacionarse con la creación: la exploración libre, la búsqueda mediante experimentación y la generación inmediata de resultados.

La pregunta que atraviesa toda la experiencia es:

**¿Qué valor tiene el proceso de crear cuando podemos obtener el resultado sin recorrerlo?**

## 2. Concepto de la obra

La obra utiliza la frase WHY BOTHER? como elemento central de una simulación de partículas.

La palabra funciona como un objetivo visual que permite representar diferentes relaciones entre el proceso creativo y su resultado.

La experiencia está dividida en tres modos:

## 01. WANDER — Exploración sin destino

### Evolución del modo WANDER

Durante el desarrollo de la obra, uno de los aspectos que más necesité ajustar fue el comportamiento de las partículas en el modo WANDER.

Inicialmente, las partículas se desplazaban mediante movimientos aparentemente aleatorios, pero el resultado terminaba pareciéndose demasiado al comportamiento de SEARCH. Esto hacía que los dos modos no tuvieran una identidad suficientemente diferenciada.

Por eso decidí experimentar con nuevas formas de interacción entre las partículas. Incorporé comportamientos de cohesión, separación y alineación, además de fuerzas que permiten generar fenómenos temporales como vórtices, ondas, agrupaciones y filamentos.

También busqué que estos fenómenos no aparecieran todos al mismo tiempo. La intención fue que las partículas comenzaran explorando libremente el espacio y que, a medida que avanzara la simulación, surgieran comportamientos inesperados que posteriormente se transformaran o desaparecieran.

Este proceso me permitió entender que la exploración no consiste simplemente en generar movimientos aleatorios. También puede surgir de las relaciones entre elementos que, al interactuar, producen estructuras que no fueron definidas previamente.

El resultado es un modo que no busca construir una figura específica, sino experimentar con el movimiento, el azar y la aparición de formas temporales.

## 02. SEARCH — Crear mediante el proceso

Este modo representa la búsqueda de un resultado a través de diferentes intentos, errores y procesos de refinamiento.

Las partículas comienzan distribuidas aleatoriamente por el lienzo y atraviesan cinco etapas progresivas:

1. **Initial Chaos:** las partículas exploran libremente el espacio.
2. **Experimentation:** comienzan a agruparse y a formar estructuras abstractas.
3. **First Draft:** aparecen las primeras aproximaciones a las letras, todavía deformadas e imperfectas.
4. **Refinement:** las partículas empiezan a organizarse y a construir una versión más reconocible de la palabra.
5. **Final Result:** finalmente, las partículas alcanzan sus posiciones definitivas y forman WHY BOTHER? correctamente.

La intención de este modo surgió de observar cómo funcionan los procesos de generación mediante inteligencia artificial. Cuando solicitamos una imagen, podemos pasar por diferentes versiones, bocetos y correcciones antes de obtener un resultado satisfactorio.

Quise representar esa evolución mediante las partículas, haciendo que no llegaran directamente a la solución, sino que atravesaran diferentes estados antes de alcanzarla.

Este modo representa el valor del proceso, la experimentación y el aprendizaje que ocurre durante la construcción de algo.

## 03. GENERATE — Resultados inmediatos

El tercer modo representa una experiencia inspirada en las herramientas actuales de inteligencia artificial generativa.

A diferencia de SEARCH, aquí no observamos cómo se construye progresivamente la palabra. El sistema presenta una interfaz de generación que simula el procesamiento de una solicitud.

Durante este proceso aparece una ventana con:

- Una matriz de partículas azules animadas que representan el procesamiento.
- Mensajes que cambian según la etapa de generación.
- Un porcentaje de progreso.
- Una barra que indica el avance de la solicitud.

Al finalizar, aparece una nueva interpretación visual de WHY BOTHER?.

Cada nueva solicitud puede producir una propuesta diferente mediante cambios de tipografía, color, composición y efectos gráficos.

También incorporé una interrupción simulada por restricciones de seguridad. Mediante la tecla E es posible provocar que una generación sea bloqueada, mostrando un mensaje de error y permitiendo posteriormente realizar un nuevo intento.

Esta posibilidad representa que los sistemas generativos no siempre producen un resultado y que también existen restricciones, condiciones y limitaciones dentro de estos procesos.

La intención de GENERATE es contrastar la generación inmediata de resultados con el recorrido creativo que representa SEARCH.

## 3. Desarrollo y exploración técnica

Para desarrollar la obra utilicé JavaScript y la biblioteca p5.js, trabajando desde Visual Studio Code.

El elemento principal de la simulación es un sistema de partículas. Cada partícula posee una posición, una velocidad y diferentes posiciones objetivo, dependiendo del comportamiento que se esté ejecutando.

Durante el desarrollo exploré diferentes comportamientos:

- Movimiento autónomo mediante funciones de ruido.
- Desplazamiento aleatorio.
- Atracción hacia posiciones determinadas.
- Organización progresiva de partículas.
- Transformación entre diferentes conjuntos de posiciones.
- Animaciones mediante variaciones de tamaño, intensidad y movimiento.

Uno de los retos principales fue conseguir que las partículas no se limitaran a aparecer directamente en la posición final de la palabra.

En las primeras pruebas, las partículas se desplazaban demasiado rápido hacia su objetivo o generaban agrupaciones que nunca conseguían formar la frase. A partir de esas observaciones fui ajustando los movimientos, las fuerzas de atracción y los tiempos de transición.

También trabajé en la diferenciación de los tres modos para que cada uno representara una experiencia distinta y no solamente una variación de velocidad.

En GENERATE desarrollé una interfaz de procesamiento simulada, con animaciones, mensajes, porcentaje de progreso, diferentes estilos visuales y una condición de bloqueo que puede activarse mediante el teclado.

## 4. Interacción

La obra permite cambiar entre las tres experiencias mediante los botones de la interfaz o los siguientes controles:

| Tecla | Acción |
|---|---|
| 1 | Activar WANDER |
| 2 | Activar SEARCH |
| 3 | Activar GENERATE |
| ESPACIO | Solicitar una nueva generación |
| G | Solicitar una nueva generación |
| E | Simular una interrupción de seguridad |

En WANDER y SEARCH el usuario puede observar el comportamiento de las partículas. En GENERATE puede solicitar nuevas interpretaciones visuales y experimentar con el resultado de cada generación.

## 5. Reflexión: ¿Why Bother?

Durante el desarrollo de este proyecto, mi interpretación de la pregunta fue cambiando.

Inicialmente, la idea estaba relacionada con conseguir que un conjunto de partículas formara una palabra. Sin embargo, a medida que fui experimentando con los comportamientos, empecé a encontrar más interesante el recorrido que realizaban las partículas antes de llegar al resultado.

Esto me llevó a pensar en la diferencia entre obtener algo terminado y experimentar el proceso de construirlo.

La inteligencia artificial puede producir resultados en muy poco tiempo, explorar diferentes posibilidades y generar alternativas que anteriormente requerían una mayor intervención humana. Sin embargo, considero que esto no elimina necesariamente el valor de aprender, experimentar o crear por cuenta propia.

Durante este ejercicio, el código también fue una herramienta para explorar ideas. Utilicé asistencia de inteligencia artificial para desarrollar, corregir y ajustar diferentes partes de la programación, pero las decisiones conceptuales, la intención visual y los comportamientos que quería conseguir fueron surgiendo a partir de mi propia experimentación y de las pruebas realizadas.

Esto también me permitió reconocer algo importante: utilizar inteligencia artificial no significa necesariamente dejar de participar en el proceso creativo. Puede convertirse en una herramienta para desarrollar una idea, siempre que exista una intención, una dirección y una comprensión de lo que se está construyendo.

Finalmente, la obra no pretende responder definitivamente la pregunta WHY BOTHER?, sino abrir una reflexión sobre las diferentes maneras de crear y sobre el valor que puede tener el proceso, incluso cuando existe la posibilidad de obtener un resultado de manera inmediata.

**Tal vez el valor de crear no está únicamente en llegar al resultado, sino también en todo lo que descubrimos mientras intentamos alcanzarlo.**
