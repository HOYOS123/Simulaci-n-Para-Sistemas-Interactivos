https://hoyos123.github.io/RepositorioSimulacion/


<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/cb1ea83f-3d4c-45a9-a07d-56b6732f89c1" />

Enlace al repo del profe: https://github.com/juanferfranco/forces-instrument-u3
Enlace a mi repo: https://github.com/HOYOS123/RepositorioSimulacion
Enlace al proyecto: https://hoyos123.github.io/RepositorioSimulacion/


# Instrumento de Fuerzas — Primera versión

## 1. Antes de tocar código

Antes de comenzar a modificar el código del proyecto base, decidí definir primero qué quiero lograr con el instrumento, cómo debería comportarse visualmente y cuáles serán las condiciones de la primera versión.

La intención es que el desarrollo no comience simplemente modificando parámetros o agregando funcionalidades, sino que exista una idea clara del comportamiento que se quiere construir y de la manera en que se va a controlar durante la interpretación.

---

## 2. Contexto del proyecto

Este proyecto corresponde a la **Unidad 3 · Fuerzas**, cuyo objetivo es diseñar un instrumento visual basado en sistemas de fuerzas.

Como referencia se está utilizando el proyecto **Forces Instrument**, que implementa una simulación de partículas utilizando **WebGPU, Three.js y compute shaders**.

El proyecto base permite trabajar con una gran cantidad de partículas y diferentes fuerzas que afectan su comportamiento. A partir de esta estructura se busca desarrollar una versión propia del instrumento, modificando progresivamente el comportamiento, los parámetros y la interacción.

La pieza musical que funcionará como restricción compartida para la interpretación es:

> **“LesAlpx” — Floating Points**

La música no será utilizada como una entrada automática para controlar la simulación. La intención es que la persona que interpreta el instrumento escuche la pieza y tome decisiones sobre las fuerzas y el comportamiento del sistema.

---

## 3. Idea general del instrumento

La idea principal es construir un sistema visual compuesto por muchas partículas que pueda ser **dirigido mediante fuerzas**.

Las partículas deben comportarse como un sistema físico, de manera que las modificaciones realizadas por el usuario produzcan cambios visibles en la organización, movimiento y energía del conjunto.

No se busca crear una animación completamente predeterminada.

En cambio, se busca construir un **instrumento visual** que pueda ser interpretado.

Esto significa que la música proporciona el contexto temporal y expresivo, mientras que el usuario controla el comportamiento del sistema de partículas.

---

## 4. Comportamiento visual inicial

Uno de los comportamientos visuales que se quiere conseguir para la primera versión es el siguiente:

### Estado inicial

Las partículas comienzan concentradas alrededor del centro del espacio.

Visualmente deben formar aproximadamente un **cubo pequeño**.

La intención es que el sistema inicialmente se vea compacto y relativamente estable.

---

### Expansión

A partir de una fuerza radial, las partículas comienzan a desplazarse hacia afuera.

El sistema pasa progresivamente de estar concentrado en el centro a ocupar una región cada vez mayor del espacio.

La intención visual es generar la sensación de que el pequeño cubo inicial **se expande hasta convertirse en un cubo mucho más grande**.

---

### Límites

El espacio de simulación tendrá unos límites definidos.

Cuando las partículas lleguen a estas márgenes, no deberían desaparecer.

En cambio, deben **rebotar contra los límites y cambiar de dirección**.

Esto permitirá mantener las partículas dentro del espacio de visualización y generar un comportamiento continuo.

---

## 5. Fuerzas que se utilizarán

El instrumento se construirá alrededor de diferentes fuerzas y parámetros físicos.

Entre las fuerzas y controles que ya están disponibles o que se consideran para la primera versión se encuentran:

* **Fuerza radial**
* **Vórtice**
* **Viento**
* **Atracción**
* **Drag**
* **Velocidad inicial**
* **Velocidad máxima**
* **Tamaño de los límites**
* **Escala temporal**

Estos elementos permitirán modificar el comportamiento del sistema sin tener que crear una animación completamente diferente para cada momento de la música.

La idea es que las fuerzas sean las herramientas de interpretación.

---

## 6. Primera versión: interacción con mouse y teclado

Para la primera versión decidí trabajar principalmente con **mouse y teclado**.

Esto permitirá concentrarnos primero en resolver correctamente el comportamiento del instrumento antes de agregar sistemas de interacción más complejos.

### Mouse

El mouse podrá utilizarse como una forma directa de interacción con el sistema.

La intención es explorar posteriormente posibilidades como:

* controlar una posición dentro del espacio;
* modificar una fuerza;
* atraer o desplazar partículas;
* controlar la dirección de una fuerza;
* interactuar directamente con el campo de partículas.

Todavía no se define que todas estas posibilidades deban estar presentes en la primera versión. Primero se evaluará cuáles producen una interacción clara y útil.

### Teclado

El teclado permitirá disponer de controles rápidos durante la interpretación.

Podría utilizarse para:

* activar o desactivar fuerzas;
* cambiar entre diferentes comportamientos;
* aumentar o disminuir la intensidad;
* activar estados específicos del sistema;
* reiniciar la simulación;
* controlar parámetros importantes sin tener que utilizar una interfaz gráfica constantemente.

La distribución definitiva de teclas se definirá durante el desarrollo y las pruebas.

---

## 7. La simulación como instrumento

Una decisión importante es que la simulación no debe entenderse solamente como una animación.

Una animación reproduce una secuencia previamente diseñada.

Un instrumento, en cambio, debe permitir que el intérprete tome decisiones y produzca diferentes resultados.

Por esta razón, el objetivo es que un mismo sistema pueda generar comportamientos diferentes dependiendo de cómo se utilicen las fuerzas.

Por ejemplo:

```text
                 MÚSICA
                    │
                    ▼
              INTERPRETACIÓN
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
       TECLADO               MOUSE
          │                   │
          └─────────┬─────────┘
                    ▼
              FUERZAS FÍSICAS
                    │
                    ▼
              PARTICULAS
                    │
                    ▼
             RESULTADO VISUAL
```

De esta manera, la música funciona como una restricción temporal y expresiva, pero no controla automáticamente el sistema.

---

## 8. Parámetros iniciales

El proyecto base cuenta con diferentes parámetros que pueden ser utilizados para controlar la simulación.

Entre ellos se encuentran:

| Parámetro         | Función                                    |
| ----------------- | ------------------------------------------ |
| `dt`              | Control del paso temporal de la simulación |
| `timeScale`       | Escala del tiempo                          |
| `initialSpeed`    | Velocidad inicial de las partículas        |
| `maxSpeed`        | Velocidad máxima                           |
| `boundsSize`      | Tamaño de los límites del espacio          |
| `particleSize`    | Tamaño visual de las partículas            |
| `windEnabled`     | Activación del viento                      |
| `wind`            | Dirección/intensidad del viento            |
| `radialEnabled`   | Activación de la fuerza radial             |
| `attractor`       | Posición del atractor                      |
| `radialStrength`  | Intensidad de la fuerza radial             |
| `softening`       | Suavizado de la fuerza                     |
| `vortexEnabled`   | Activación del vórtice                     |
| `vortexStrength`  | Intensidad del vórtice                     |
| `dragEnabled`     | Activación del drag                        |
| `dragCoefficient` | Intensidad del drag                        |

Estos parámetros serán evaluados durante las siguientes etapas para determinar cuáles realmente aportan al instrumento.

---

## 9. Cantidad de partículas

El proyecto utiliza una cantidad elevada de partículas para conseguir un comportamiento visual denso.

Como punto de partida se está utilizando:

```text
PARTICLE_COUNT = 131072
```

Es decir:

```text
2^17 = 131072 partículas
```

La cantidad es suficientemente grande para producir una visualización compleja, pero aumentar todavía más el número de partículas podría afectar el rendimiento.

Por esta razón, decidí **no aumentar inicialmente la cantidad de partículas**.

Primero se debe comprobar cómo se comporta la simulación y medir su rendimiento.

Solo después de comprobar que el sistema funciona correctamente concideraré aumentar la cantidad.

---

## 10. Prioridades de la primera versión

La primera versión no busca tener todas las funcionalidades posibles.

El objetivo es conseguir un prototipo funcional que permita comprobar si la idea del instrumento funciona.

Las prioridades son:

1. Tener un sistema de partículas estable.
2. Conseguir la formación inicial del cubo pequeño.
3. Conseguir la expansión de las partículas hacia afuera.
4. Implementar correctamente los límites.
5. Conseguir que las partículas reboten al tocar las márgenes.
6. Controlar las fuerzas de manera interactiva.
7. Utilizar mouse y teclado como métodos principales de interacción.
8. Comprobar que el sistema puede ser interpretado durante la música.
9. Mantener un rendimiento adecuado.
10. Documentar cada modificación y sus resultados.

---

## 11. Lo que NO se hará todavía

Para evitar complicar demasiado la primera versión, se decidió no implementar todavía sistemas adicionales que puedan distraer del objetivo principal.

Por ahora no se priorizarán:

* controles mediante dispositivos externos;
* interacción mediante sensores;
* control automático mediante análisis de audio;
* sincronización automática con la música;
* una interfaz gráfica demasiado compleja;
* una cantidad excesiva de parámetros;
* efectos visuales que no estén relacionados con las fuerzas;
* optimizaciones prematuras antes de comprobar el comportamiento.

Estas posibilidades podrán evaluarse posteriormente si la primera versión funciona correctamente.

---

## 12. Criterio para evaluar la primera versión

La primera versión se considerará exitosa si permite realizar una interpretación en la que el usuario pueda modificar el comportamiento del sistema de partículas de manera clara y perceptible.

No basta con que las partículas se muevan.

Debe ser posible reconocer una relación entre:

**acción del usuario → fuerza → comportamiento físico → resultado visual.**

Además, el sistema debe permitir suficiente libertad para que una misma pieza musical pueda producir diferentes interpretaciones.

---

## 13. Plan de trabajo inicial

Antes de realizar modificaciones importantes, se seguirá aproximadamente este proceso:

### Etapa 1 — Comprender el proyecto base

Revisar la estructura existente y entender cómo funcionan:

* `main.js`
* `createSimulation.js`
* `parameters.js`
* `labPanel.js`
* sistema de partículas;
* compute shaders;
* parámetros y uniforms.

### Etapa 2 — Construir el comportamiento físico básico

Modificar la simulación para conseguir:

**cubo pequeño → expansión → límites → rebote**

Este comportamiento será la base visual del instrumento.

### Etapa 3 — Probar las fuerzas

Experimentar con:

* radial;
* vortex;
* wind;
* attractor;
* drag.

Se buscará identificar qué combinaciones producen comportamientos interesantes y controlables.

### Etapa 4 — Incorporar interacción

Implementar progresivamente los controles mediante:

* mouse;
* teclado.

La intención es que los controles tengan una relación directa y comprensible con las fuerzas.

### Etapa 5 — Probar con la música

Una vez que el instrumento sea funcional, se probará mientras se escucha:

**“LesAlpx” — Floating Points**

El objetivo será comprobar si el sistema ofrece suficientes posibilidades expresivas para acompañar e interpretar la pieza.

### Etapa 6 — Documentar

Cada cambio importante se registrará en la bitácora de GitHub.

La documentación deberá mostrar:

* qué se intentó;
* por qué se hizo;
* qué resultado se esperaba;
* qué ocurrió realmente;
* qué problemas aparecieron;
* qué modificaciones se realizaron;
* qué se decidió mantener o descartar.

---

## 14. Primera hipótesis del proyecto

La hipótesis inicial es que un sistema relativamente sencillo de partículas puede convertirse en un instrumento visual expresivo si las fuerzas son suficientemente controlables y si la interacción permite modificar el comportamiento en tiempo real.

El objetivo no es conseguir una simulación físicamente perfecta, sino utilizar conceptos de física para construir un sistema visual que pueda ser **interpretado**.

La física será, por lo tanto, tanto el mecanismo que mueve las partículas como el lenguaje visual del instrumento.

---

## 15. Próximo paso

Con esta definición inicial terminada, el siguiente paso será comenzar a modificar el proyecto base.

La primera meta concreta será:

> **Conseguir que las partículas comiencen formando un cubo pequeño, se expandan hacia afuera, alcancen unos límites definidos y reboten contra ellos formando un cubo mayor.**

A partir de este comportamiento básico se comenzarán a incorporar las interacciones mediante mouse y teclado.

**Estado actual:** planificación previa al desarrollo.

**Siguiente etapa:** modificación de la simulación de partículas.
