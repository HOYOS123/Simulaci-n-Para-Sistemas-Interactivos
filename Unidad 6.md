# Unidad 6 - Simulación para sistemas interactivos: AGENTES

**Estudiante:** Juan José Hoyos Peláez  
**Curso:** Ingeniería en Diseño de Entretenimiento Digital — Universidad Pontificia Bolivariana  
**URL del Proyecto en Vivo:** [https://hoyos123.github.io/Simulaci-n_Unidad6_Easy_JJHP/](https://hoyos123.github.io/Simulaci-n_Unidad6_Easy_JJHP/)
**Repositorio GitHub:** [Simulaci-n_Unidad6_Easy_JJHP](https://github.com/HOYOS123/Simulaci-n_Unidad6_Easy_JJHP)

---

## Introducción y Selección Musical
Para este reto de diseño, desarrollé un instrumento visual interactivo para web concebido bajo la estética de **VJing para conciertos**. 

* **Pieza Musical Seleccionada:** *"Easy"* de la banda **No Doubt**.
* **Justificación Estética:** La canción combina una fuerte sección rítmica (bajo y batería marcados), quiebres dinámicos, pasajes atmosféricos en los versos y coros explosivos. El instrumento visual fue diseñado para traducir físicamente ese groove a través de un enjambre geométrico inteligente y reactivo.

---

## Definición del Sistema: Percepción, Límites y Reglas
El instrumento está construido exclusivamente con **Steering Behaviors** (Flocking: Separación, Alineación y Cohesión) combinados con renderizado de red geométrica tipo **Plexus** y aceleración por hardware en p5.js.

1. **Percepción Limitada:** Cada agente (*boid*) calcula su entorno inmediato evaluando a sus vecinos dentro de un radio de percepción local (`perceptionRadius = 60px`) y un radio de separación estricto (`sepRadius = 35px`). No conocen el estado global del canvas, solo su vecindario.
2. **Límites Físicos:** Cuentan con restricciones estrictas de velocidad máxima (`maxSpeed`) y fuerza de viraje máxima (`maxForce`), evitando desplazamientos abruptos y garantizando trayectorias orgánicas e inerciales.
3. **Cálculo de Acciones:** El sistema suma ponderadamente los tres vectores clásicos de Reynolds (Separación, Alineación y Cohesión) modificados en tiempo real por los estados del instrumento, además de permitir comportamientos emergentes avanzados como órbita, vórtice y formación tipográfica vectorial.

---

## Controles Expresivos en Tiempo Real
El instrumento se interpreta en vivo mediante el teclado y el mouse, permitiendo conducir el sistema sin depender de análisis automáticos de audio:

* **`[1]` Groove (Malla):** Comportamiento base de floco equilibrado, ideal para los versos y la sección rítmica constante.
* **`[2]` Explosión (Caos):** Incrementa drásticamente la separación y el límite de velocidad, desarmando la malla en fragmentos caóticos para los quiebres.
* **`[3]` Órbita (Mouse):** El enjambre persigue y orbita dinámicamente el cursor con un radio de seguridad anti-colapso.
* **`[4]` Esfera Energética:** Las partículas convergen y rotan de manera concéntrica simulando una esfera de plasma en el centro.
* **`[5]` Estático Neón:** Mantiene la malla rígida y brillante con alta velocidad lineal.
* **`[6]` Supernova (Fuegos Artificiales):** Comprime las partículas al centro para hacerlas estallar radialmente en los acentos de percusión.
* **`[7]` El Tornado:** Succiona a los agentes en un remolino vertical ascendente.
* **`[E]` Tipografía EASY:** Las partículas reorientan su vector de búsqueda para formar con precisión geométrica la palabra "EASY" en el centro de la pantalla.
* **`[G]` Modo Arcoíris:** Desata una gama cromática dinámica basada en la velocidad de los agentes.
* **`[C]` Ciclo de Fondo:** Altera el contraste global del lienzo (oscuro, claro, gris, rosa).
* **`[P]` Paleta de Color Fija:** Fija tonalidades de neón sólidas.
* **`[A]` Pulso Ambient:** Modula la transparencia del rastro (*trail fade*).
* **`[J]` Jitter Explosivo:** Aplica un impulso de fuerza aleatorio que sacude y fragmenta el enjambre.
* **`[Clic del Mouse]` Inversor de Fase:** Invierte instantáneamente el contraste de todo el instrumento mientras se mantenga presionado.

---

## Autoevaluación Sustentada con Evidencias

| Criterio de Evaluación | Calificación Propuesta | Sustentación y Evidencias |
| :--- | :---: | :--- |
| **1. Cumplimiento del encargo** | **25 / 25** | El instrumento fue desarrollado íntegramente con tecnologías web estándar (HTML5, CSS3 y p5.js), opera de forma fluida a 60 FPS en pantalla completa y está desplegado públicamente en GitHub Pages para su ejecución en vivo. |
| **2. Comprensión y verificación** | **25 / 25** | El código implementa formalmente las reglas de *steering* de Reynolds (separación, alineación, cohesión) combinadas con trigonometría vectorial segura (prevención de divisiones por cero en `seek`). Cada parámetro numérico tiene un impacto directo y predecible en el comportamiento físico de los agentes. |
| **3. Diseño e intención** | **25 / 25** | La selección de comportamientos (desde el floco de malla hasta la formación tipográfica vectorial de "EASY") responde directamente a la estructura dramática de la canción de No Doubt, logrando una sincronía estética entre la música pop-rock y el arte generativo. |
| **4. Interpretación humana** | **25 / 25** | El sistema no automatiza el análisis de audio; recae enteramente en la ejecución en tiempo real mediante un mapa de controles robusto por teclado y mouse, estructurado a través de un score visual validado en ensayos. |
| **TOTAL** | **100 / 100** | |
