# Actividad 02: Bitácora de GitHub - K-Cluster

## Reto de diseño: Sistema audiovisual performativo con Kuramoto

- **Nombre del Proyecto:** K-Cluster: Ecosistemas de Fase
- **Descripción del Reto:** Desarrollo de una experiencia web interactiva en p5.js y Tone.js donde la organización temporal y rítmica no depende de un secuenciador rígido ni de un reloj global, sino de la autoorganización emergente de una red de osciladores acoplados.

## Implementación del Modelo
- **Ecuación Base:** Se programó estrictamente la ecuación diferencial de Kuramoto para calcular en tiempo real la evolución de fase de cada agente, ponderando su frecuencia natural frente a la influencia colectiva regulada por la fuerza de acoplamiento ($K$).
- **Variables Clave:**
  - **Fase ($\theta_i$):** Ciclo interno de actividad de cada agente (de $0$ a $2\pi$) que determina cuándo se dispara su evento audiovisual.
  - **Frecuencia Natural ($\omega_i$):** Velocidad intrínseca o tempo base del agente.
  - **Fuerza de Acoplamiento ($K$):** Variable interactiva que controla qué tan receptivo es cada agente a la influencia de sus vecinos.

## Arquitectura de Agentes y Personalidades
El sistema consta de **8 agentes** distribuidos en **4 personalidades audiovisuales** distintas:
1. **Bajos (2 Agentes):** Anclajes graves con síntesis FM y círculos rojos grandes y pesados.
2. **Plucks (3 Agentes):** Elementos melódicos con PolySynth y geometrías cian rotacionales.
3. **Pads (2 Agentes):** Atmósferas ambientales con síntesis de colchones y formas orgánicas violetas cuyo filtro responde a la fase.
4. **Glitch (1 Agente):** Pulso percusivo inestable de alta frecuencia con síntesis de ruido y forma triangular.

## Mecanismos Performativos y Perturbación
- **Control Global:** Modificación en tiempo real de la fuerza de acoplamiento ($K$) y la velocidad natural global ($\omega$) mediante sliders interactivos.
- **Interacción Individual:** Clic sobre un agente para alterar abruptamente su fase, o arrastre (*Drag & Drop*) para cambiar su posición espacial.
- **Pulso Entrópico:** Botón de perturbación global que inyecta ruido aleatorio a las fases de todo el conjunto para observar la reorganización del sistema.
- **Percepción de Estados:** Indicador central y cálculo del parámetro de orden global ($r$) para comunicar visual y sonoramente el tránsito entre desorden, organización parcial y organización estable.

---

# Actividad 03: Presentación Grupal y Autoevaluación

- **Cumplimiento de requisitos mínimos (25 / 25 puntos):** La aplicación cuenta con exactamente 8 agentes dinámicos, 4 personalidades audiovisuales diferenciadas por comportamiento y timbre, control interactivo de $K$, múltiples vías de intervención performativa (individual y global), un botón de perturbación y representación clara de los 3 estados colectivos.
- **Claridad en las variables del modelo (25 / 25 puntos):** Se define y comprende con precisión qué representa la fase ($\theta$) como el ciclo interno de actividad, la frecuencia natural ($\omega$) como el tempo intrínseco y la fuerza de acoplamiento ($K$) como la permeabilidad a la influencia de los vecinos.
- **Explicación del comportamiento observado (25 / 25 puntos):** Se justifica formalmente cómo el incremento de $K$ activa la sumatoria de senos de diferencia de fase, forzando matemáticamente la transición orgánica desde el caos entrópico hasta la sincronía armónica unificada.
- **Demostración de los objetivos pedagógicos (25 / 25 puntos):** El proyecto comprueba con éxito que Kuramoto no es reemplazable por un temporizador estático, ya que la cohesión musical y visual es un fenómeno genuinamente emergente de la red interactiva.

# Video Evidencia: 
[Video en Youtube](https://youtu.be/yAazCIvtvtU)
