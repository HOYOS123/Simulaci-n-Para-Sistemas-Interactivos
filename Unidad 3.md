# Actividad 03 · Instrumento de Fuerzas

## 1. Instrumento funcional y publicado

**Proyecto:** Force Field — Instrumento visual basado en fuerzas.

**URL pública:** https://hoyos123.github.io/RepositorioSimulacion/

El instrumento fue desarrollado con **Three.js, WebGPU, TSL, GPU Compute y Vite**, tomando como punto de partida el proyecto `forces-instrument-u3`.

El sistema funciona en tiempo real y permite conducir las partículas mediante diferentes controles:

* **SPACE:** expansión del campo.
* **V:** activa/desactiva el vórtice.
* **Q:** glitch.
* **B:** explosión/burst.
* **S:** estrellas fugaces.
* **D:** gusano de partículas que sigue el cursor.
* **C:** cambio de paleta de color.
* **R:** reinicio.
* **MOUSE:** modifica el atractor del sistema.

La publicación se realizó mediante **GitHub Actions y GitHub Pages**.

---

## 2. Mapa del sistema

### Estado

La simulación mantiene la posición, velocidad y vida de las partículas en buffers de GPU.

### Fuerzas principales

* **Atracción:** las partículas son atraídas hacia la posición del cursor.
* **Expansión:** una fuerza radial aleja las partículas del centro.
* **Gravedad central:** atrae las partículas hacia el centro durante el vórtice.
* **Vórtice:** combina atracción central con una fuerza tangencial.
* **Burst:** genera una dispersión rápida con variaciones aleatorias.
* **Glitch:** introduce fuerzas y desplazamientos aleatorios.
* **Worm:** concentra parte de las partículas alrededor del cursor.

### Integración

Las fuerzas modifican la velocidad y posteriormente la posición:

`velocidad → fuerza × dt → posición`

También existe un límite de velocidad y límites espaciales para evitar que las partículas abandonen completamente el campo.

### Render

Las partículas se representan mediante `InstancedMesh` y `SpriteNodeMaterial`.

### Archivos principales

* `src/main.js` → escena, cámara, controles, interacción y modos.
* `src/simulation/parameters.js` → parámetros y uniformes.
* `src/simulation/createSimulation.js` → estado de partículas, fuerzas, integración y GPU Compute.

---

## 3. Ficha de fuerzas

### Atracción

**Dirección:** desde la partícula hacia el cursor.

**Modelo simplificado:**

`F = dirección × fuerza / distancia²`

**Predicción:** al mover el cursor, las partículas cercanas deberían desplazarse hacia él.

**Decisión:** utilizar el mouse como instrumento principal de conducción porque permite intervenir directamente sobre el campo sin controlar manualmente la posición de cada partícula.

### Expansión

**Dirección:** desde el centro hacia afuera.

**Predicción:** al activar SPACE, el sistema debe expandirse rápidamente y producir una sensación de liberación de energía.

### Vórtice

Combina una fuerza hacia el centro con una fuerza tangencial.

**Predicción:** las partículas deberían comenzar a girar alrededor del centro mientras son atraídas hacia él.

### Burst

Combina la dirección de expansión con una variación aleatoria.

**Predicción:** las partículas se dispersan de manera rápida y menos predecible que con una expansión radial simple.

### Glitch

Utiliza direcciones aleatorias y desplazamientos bruscos.

**Predicción:** el campo deja de comportarse como una expansión uniforme y adquiere un comportamiento fragmentado e impredecible.

### Worm

Una selección de partículas recibe una atracción especial hacia el cursor.

**Predicción:** al mover el cursor, un grupo de partículas se concentra alrededor de él, mientras una estructura visual independiente genera la sensación de cabeza, cuerpo y cola.

---

## 4. Registro de pruebas

### Prueba 1 — Estado inicial

**Resultado:** las partículas aparecen distribuidas dentro del campo y permanecen contenidas por los límites.

### Prueba 2 — Atracción con mouse

**Resultado:** al mover el cursor, las partículas cercanas son atraídas hacia el punto de interacción.

### Prueba 3 — Expansión

**Acción:** SPACE.

**Resultado:** las partículas reciben una fuerza radial y se expanden desde el centro.

### Prueba 4 — Vórtice

**Acción:** V.

**Resultado:** aparece una dinámica de rotación alrededor del centro, combinando gravedad y fuerza tangencial.

### Prueba 5 — Burst / Glitch

**Acciones:** B y Q.

**Resultado:** B produce una dispersión fuerte y Q introduce desplazamientos aleatorios que rompen el comportamiento regular del sistema.

### Prueba específica — Worm

**Acción:** D + movimiento del mouse.

**Resultado:** un grupo de partículas se concentra alrededor del cursor y se combina con una estructura de cabeza, cuerpo y cola que deja una trayectoria visual al desplazarse.

Las pruebas permitieron modificar parámetros de fuerza, tamaño, velocidad, atracción y comportamiento visual antes de llegar a la versión final.

---

## 5. Score visual e interpretación de *LesAlpx*

La interpretación no utiliza el audio como entrada automática. La música se escucha y las decisiones se realizan manualmente durante la presentación.

| Momento de la pieza | Intención                  | Acción              |
| ------------------- | -------------------------- | ------------------- |
| Inicio              | Organización / estabilidad | Mouse               |
| Acumulación         | Tensión                    | Atracción con mouse |
| Aumento de energía  | Expansión                  | SPACE               |
| Transformación      | Rotación / movimiento      | V                   |
| Ruptura             | Caos / imprevisibilidad    | Q                   |
| Liberación          | Dispersión                 | B                   |
| Cambio de textura   | Transformación visual      | C                   |
| Momento espacial    | Aparición / recorrido      | S                   |
| Concentración       | Reorganización             | D + mouse           |
| Resolución          | Regreso al estado base     | R                   |

La relación buscada durante la interpretación es:

**escucha → intención → decisión → control → fuerza → comportamiento emergente**

---

## 6. Bitácora de IA

La IA fue utilizada como herramienta de programación y experimentación, no como reemplazo del criterio de diseño.

El proceso utilizado fue:

1. Definir el comportamiento que quería conseguir.
2. Explicar qué fuerza debía producirlo.
3. Solicitar modificaciones localizadas dentro de la arquitectura existente.
4. Probar el comportamiento en el proyecto.
5. Detectar errores o resultados diferentes a lo esperado.
6. Modificar nuevamente los parámetros y el código.
7. Conservar únicamente las soluciones que producían el comportamiento buscado.

Entre las modificaciones realizadas estuvieron la expansión, el glitch, el burst, las estrellas fugaces y el sistema del worm.

Un ejemplo importante fue el sistema **Worm**: la primera versión hacía que demasiadas partículas cambiaran de color y el resultado parecía únicamente una acumulación. Se modificó el sistema para separar el comportamiento del worm del resto de partículas y construir visualmente una cabeza, cuerpo y cola.

La IA propuso código, pero las decisiones sobre qué conservar, modificar o descartar fueron realizadas mediante pruebas en el proyecto.

---

## 7. Autoevaluación ponderada

| Criterio                                  |    Peso | Valoración |         Puntos |
| ----------------------------------------- | ------: | ---------: | -------------: |
| Trazabilidad y comprensión del sistema    |      25 |         90 |           22,5 |
| Verificación del algoritmo de fuerzas     |      25 |         85 |          21,25 |
| Diseño de fuerzas e intención             |      20 |         95 |             19 |
| Instrumento, score e interpretación       |      15 |         95 |          14,25 |
| Experimentación y criterio frente a la IA |      10 |         95 |            9,5 |
| Entrega técnica y documentación           |       5 |        100 |              5 |
| **Total**                                 | **100** |            | **91,5 / 100** |

### Justificación breve

El proyecto cumple con el contrato técnico y está publicado mediante GitHub Pages. Las fuerzas principales pueden identificarse dentro del código y se pueden activar mediante pocos controles con significado. La interacción es manual y no depende de FFT, beat o amplitud de la música.

La mayor parte de la experimentación consistió en modificar las fuerzas, parámetros, tamaños, colores y comportamientos hasta obtener una dinámica que pudiera ser conducida durante la interpretación.

La IA fue utilizada durante el desarrollo, pero las propuestas fueron probadas, corregidas y modificadas antes de llegar a la versión final.

Enlace al proyecto: https://hoyos123.github.io/RepositorioSimulacion/


<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/cb1ea83f-3d4c-45a9-a07d-56b6732f89c1" />

Enlace al repo del profe: https://github.com/juanferfranco/forces-instrument-u3
Enlace a mi repo: https://github.com/HOYOS123/RepositorioSimulacion
