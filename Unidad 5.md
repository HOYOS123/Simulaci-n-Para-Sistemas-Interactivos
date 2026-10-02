# Bitácora de Proyecto: Fórum UPB — "Relevo Generacional"

* **Autor:** Juan José Hoyos Peláez
* **Proyecto:** Presentación Generativa Interactiva para Fórum UPB
* **Charla:** *“Relevo generacional: la ventaja que nadie está aprovechando”*
* **Repositorio:** [ForumTEDTALK_JJHP](https://github.com/HOYOS123/ForumTEDTALK_JJHP)
* **Despliegue Web:** [Ver Presentación en Vivo](https://hoyos123.github.io/ForumTEDTALK_JJHP/)

---

<img width="1369" height="840" alt="image" src="https://github.com/user-attachments/assets/8cbac21c-2f37-4bdd-ab3c-c22bbfc28149" />

Link: https://hoyos123.github.io/ForumTEDTALK_JJHP/

## Actividad 02: Encargo de Diseño

### 1. Concepto y Gramática Visual

El objetivo fundamental de esta propuesta visual generativa es traducir la narrativa del discurso sobre el relevo generacional en un **sistema vivo de partículas en constante reconfiguración**. El movimiento y las relaciones entre elementos no existen como adorno o fondo estático, sino como una **gramática visual dinámica** donde la tensión, la densidad, el orden y el caos representan la evolución de la masa crítica, el talento y la colaboración intergeneracional.

Tomando como referente conceptual la visión de **Memo Akten**, el sistema utiliza las partículas como átomos de un lenguaje: elementos individuales que al organizarse bajo ciertas reglas físicas y geométricas construyen conceptos complejos, palabras tangibles y estructuras simbólicas.

---

### 2. Estructura del Sistema de Partículas y Relaciones

El sistema visual fue construido en HTML5 Canvas JavaScript orientado a objetos (`visualSystem.js`) y opera bajo las siguientes reglas estructurales:

* **Masa Crítica (2.000 Partículas):** Una población continua de 2.000 elementos que nunca desaparecen ni se destruyen, simbolizando la permanencia del ecosistema humano y del conocimiento.
* **Fuerzas de Steering / Atracción Orgánica:** Las partículas calculan su distancia respecto a coordenadas objetivo (*target vectors*), regulando su velocidad (`maxSpeed = 10`) y fuerza de viraje (`maxForce = 0.5`) con amortiguación (*damping*), simulando comportamientos orgánicos de fluidez y adaptación.
* **Red de Tensión y Vinculación E structural (`drawConnections`):** Cada grupo de partículas evalúa la proximidad con sus vecinas. Cuando la distancia es inferior a **32px**, se traza un enlace de tensión (*vector line*) cuya opacidad es inversamente proporcional a la distancia. Esto genera una red o "tejido" visual que visibiliza la cohesión estructural.
* **Paleta Cromática con Significado:**
  * **Azul / Cyan (`PALETTE.Ciudad` / `UPB`):** Representa la estabilidad, la infraestructura y el marco institucional.
  * **Verde / Neón (`PALETTE.Talento`):** Representa la frescura, el nuevo talento y el crecimiento del relevo generacional.
  * **Magenta / Coral (`PALETTE.Experiencia` / `Industria`):** Representa la chispa, la disrupción y la transformación activa.

---

### 3. Interpretación del Guion y Transformaciones del Movimiento

Cada momento de la presentación modifica el comportamiento físico y la organización de la masa de partículas para acompañar el significado del discurso:

1. **Morfogénesis del Lenguaje (Tipografía con Muestreo Offscreen):**
   * **Mecanismo:** El sistema dibuja las palabras del guion en un lienzo invisible (*Offscreen Canvas*) y realiza un escaneo de píxeles (`getImageData`) con un umbral de opacidad permisivo (`alpha > 20`). 
   * **Intención:** Las partículas abandonan el flujo caótico y son reclutadas a posiciones exactas para formar conceptos clave (`FÓRUM`, `TALENTO`, `ACADEMIA`, `CONFIANZA`). El lenguaje verbal literalmente "nace" de la estructura física de las partículas.

2. **Escala Global y Cohesión (Diapositiva 3 - Planeta Tierra):**
   * **Mecanismo:** El sistema mapea coordenadas polares e implementa un patrón de ruido tridimensional en tiempo real. Asigna tamaños de partículas aumentados (**8.0px**) para construir continentes (verde) y océanos (azul) dentro de una esfera que ocupa el 56% del alto de la pantalla.
   * **Intención:** Representa el alcance global y sistémico del relevo generacional, pasando de una idea abstracta a una realidad territorial definida.

3. **Morfosis Narrativa (Diapositiva 6 - COMUNIDAD a TRANSFORMACIÓN):**
   * **Mecanismo:** Un temporizador de transición reasigna los vectores de destino de las partículas de la palabra `COMUNIDAD` hacia las posiciones de `TRANSFORMACIÓN` tras 2.6 segundos.
   * **Intención:** Muestra cómo el grupo social unido no permanece estático, sino que su propio peso lo muta hacia un agente de cambio.

4. **Sincronía y Alineación (Diapositiva 10 - Coreografía Geométrica):**
   * **Mecanismo:** Las partículas abandonan la forma tipográfica y se organizan en 4 anillos concéntricos en rotación orbital con velocidades angulares alternadas y ondas senoidales.
   * **Intención:** Representa el momento cumbre de alineación estratégica entre la universidad, la empresa, el estado y el talento joven.

---

### 4. Composición e Interfaz de Pantalla Completa para Auditorio

* **Doble Capa de Composición:** Se implementó una arquitectura donde el canvas de partículas corre sobre una capa transparente (`clearRect`), permitiendo que fotografías de gran formato con degradado (`.moment-asset`) actúen como textura de fondo tenue (`opacity: 0.42`), logrando profundidad espacial sin contaminar la lectura de las partículas.
* **Escala Tipográfica de Gran Formato:** Títulos principales proyectados a `4.8rem` (mínimo $72px$) con *text-shadow* para garantizar visibilidad óptima desde las últimas filas de un auditorio.
* **Códigos QR de Enganche:** Integración de bloques QR en la diapositiva final estructurados a `230px` de dimensión para facilitar el escaneo directo a distancia.

---

## Actividad 03: Presentación Grupal y Autoevaluación

### Matriz de Autoevaluación (100 / 100 Puntos)

| Criterio de Evaluación | Puntaje Asignado | Justificación y Evidencia de Implementación |
| :--- | :---: | :--- |
| **1. Cumplimiento del encargo** | **25 / 25** | La presentación interpreta rigurosamente la secuencia narrativa del guion de Fórum UPB. Funciona de manera fluida en pantalla completa ($100vw \times 100vh$), adaptándose dinámicamente a resoluciones de proyección mediante el manejo de *event listeners* de redimensionamiento (`resize`). |
| **2. Relaciones estructurales** | **25 / 25** | Las relaciones están claramente definidas en el código (`visualSystem.js`): fuerzas de atracción *steer*, densidad por palabras, anillos orbitales en la coreografía y líneas de vinculación vectorial basadas en proximidad ($<32px$). Cada vínculo tiene un sentido explícito dentro de la metáfora de red humana e institucional. |
| **3. Comportamiento y significado** | **25 / 25** | Ningún movimiento es puramente decorativo. Los aumentos de radio ($3.5px \rightarrow 8.0px$), los cambios de velocidad, las transiciones de morphing (`COMUNIDAD` $\rightarrow$ `TRANSFORMACIÓN`) y la dispersión responden directamente a la intención comunicativa de cada diapositiva. |
| **4. Explicación y demostración** | **25 / 25** | El código está modularizado (`visualSystem.js`, `moments.js`, `config.js`), permitiendo justificar de forma precisa cómo los algoritmos de física vectorial y análisis de imágenes crean el lenguaje visual que soporta el discurso. |

---

## Pregunta Guía

> **¿Cómo puede una estructura de elementos relacionados y en movimiento convertirse en un lenguaje visual capaz de construir el significado de un discurso?**

Una estructura de elementos en movimiento se convierte en lenguaje cuando **deja de imitar la forma y pasa a simular el comportamiento**. 

En la comunicación tradicional, la imagen es estática o sirve como mera ilustración de la palabra. Sin embargo, en un sistema generativo, el movimiento actúa como **sintaxis**:
1. **La masa y la densidad** representan la fuerza o la urgencia de una idea.
2. **La tensión y la cohesión** (las líneas que unen a las partículas por proximidad) comunican la salud del tejido social e institucional.
3. **La velocidad y la trayectoria** transmiten la dirección del cambio, la alineación o el caos.

Al asociar estos comportamientos físicos a conceptos clave de un discurso (como el relevo generacional, la academia o la transformación), el espectador no solo "escucha" el mensaje, sino que **observa las leyes físicas del concepto manifestándose en tiempo real**. El código deja de ser un motor de renderizado para convertirse en una máquina semiótica que construye significado a través de la forma en que sus elementos convergen, se vinculan y se transforman.
