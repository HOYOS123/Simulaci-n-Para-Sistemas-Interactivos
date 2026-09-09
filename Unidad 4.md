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

## Código

- Index.html:

´´´
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jam Generativo - Kuramoto</title>
  
  <!-- 1. IMPORTAMOS P5.JS -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
  
  <!-- 2. IMPORTAMOS TONE.JS -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.8.49/Tone.js"></script>

  <style>
    body {
      margin: 0;
      padding: 0;
      background-color: #121212;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
      color: white;
      font-family: sans-serif;
    }
  </style>
</head>
<body>

  <!-- 3. CARGAMOS NUESTRO CÓDIGO DE JAVASCRIPT -->
  <script src="sketch.js"></script>

</body>
</html>
´´´

---


- sketch.js:

´´´
// ==========================================
// K-CLUSTER: SISTEMA AUDIOVISUAL DE KURAMOTO
// ==========================================

let synthBajo, synthPluck, synthPad, synthGlitch;
let reverb, delay;
let audioIniciado = false;

let agentes = [];
const NUM_AGENTES = 8;

// Variables del Modelo de Kuramoto
let K = 0.5;          
let globalOmega = 1.0; 
let rGlobal = 0;       

let sliderK, sliderOmega, btnEntropia;

const ESCALA_MODAL = ["C3", "D3", "Eb3", "G3", "A3", "C4", "Eb4", "G4"];

function setupAudio() {
  reverb = new Tone.Reverb({ decay: 3.5, wet: 0.4 }).toDestination();
  delay = new Tone.FeedbackDelay({ delayTime: "8n", feedback: 0.3, wet: 0.25 }).connect(reverb);

  synthBajo = new Tone.FMSynth({
    harmonicity: 1.5,
    modulationIndex: 2,
    envelope: { attack: 0.02, decay: 0.5, sustain: 0.2, release: 0.3 }
  }).connect(reverb);

  synthPluck = new Tone.PolySynth(Tone.Synth, {
    oscillator: { type: "triangle" },
    envelope: { attack: 0.005, decay: 0.2, sustain: 0.0, release: 0.1 }
  }).connect(delay);

  synthPad = new Tone.Synth({
    oscillator: { type: "sawtooth" },
    envelope: { attack: 0.8, decay: 0.5, sustain: 0.7, release: 1.2 }
  }).connect(reverb);

  synthGlitch = new Tone.NoiseSynth({
    noise: { type: "white" },
    envelope: { attack: 0.001, decay: 0.04, sustain: 0 }
  }).connect(delay);
}

function setup() {
  createCanvas(800, 650);
  setupAudio();

  createP("Fuerza de Acoplamiento (K):").position(20, height - 75).style('color', '#fff');
  sliderK = createSlider(0, 5, K, 0.01);
  sliderK.position(20, height - 40);
  sliderK.style('width', '200px');

  createP("Velocidad Natural Global (w):").position(250, height - 75).style('color', '#fff');
  sliderOmega = createSlider(0.2, 2.5, globalOmega, 0.05);
  sliderOmega.position(250, height - 40);
  sliderOmega.style('width', '200px');

  btnEntropia = createButton("¡Inyectar Pulso Entrópico!");
  btnEntropia.position(500, height - 40);
  btnEntropia.mousePressed(inyectarEntropia);
  btnEntropia.style('padding', '6px 12px');
  btnEntropia.style('background', '#ff4444');
  btnEntropia.style('color', '#fff');
  btnEntropia.style('border', 'none');
  btnEntropia.style('cursor', 'pointer');

  let centroX = width / 2;
  let centroY = (height - 100) / 2;
  let radioDistribucion = 180;

  for (let i = 0; i < NUM_AGENTES; i++) {
    let anguloPos = map(i, 0, NUM_AGENTES, 0, TWO_PI);
    let x = centroX + cos(anguloPos) * radioDistribucion;
    let y = centroY + sin(anguloPos) * radioDistribucion;

    let personalidad = "PLUCK";
    let omegaBase = 0.03;
    let notaAsignada = random(ESCALA_MODAL);

    if (i === 0 || i === 1) {
      personalidad = "BAJO";
      omegaBase = 0.015;
      notaAsignada = i === 0 ? "C2" : "G2";
    } else if (i === 5 || i === 6) {
      personalidad = "PAD";
      omegaBase = 0.010;
      notaAsignada = "C3";
    } else if (i === 7) {
      personalidad = "GLITCH";
      omegaBase = 0.080;
      notaAsignada = "C5";
    } else {
      personalidad = "PLUCK";
      omegaBase = 0.040;
    }

    agentes.push(new Agente(i, x, y, personalidad, omegaBase, notaAsignada));
  }
}

function draw() {
  background(15, 15, 22);

  K = sliderK.value();
  globalOmega = sliderOmega.value();

  let centroX = width / 2;
  let centroY = (height - 100) / 2;

  calcularParametroOrden();
  dibujarNucleoColectivo(centroX, centroY);
  dibujarAcoplamientos(centroX, centroY);

  for (let a of agentes) {
    a.calcularKuramoto(agentes);
  }

  for (let a of agentes) {
    a.actualizar();
    a.dibujar();
  }

  if (!audioIniciado) {
    fill(255, 220, 0);
    noStroke();
    textAlign(CENTER, CENTER);
    textSize(16);
    text("Haz clic en cualquier parte de la pantalla para activar el motor sonoro", width / 2, 30);
  }
}

function calcularParametroOrden() {
  let sumaCos = 0;
  let sumaSin = 0;

  for (let a of agentes) {
    sumaCos += cos(a.theta);
    sumaSin += sin(a.theta);
  }

  let promedioCos = sumaCos / NUM_AGENTES;
  let promedioSin = sumaSin / NUM_AGENTES;
  rGlobal = sqrt(promedioCos * promedioCos + promedioSin * promedioSin);
}

function dibujarNucleoColectivo(cx, cy) {
  push();
  noFill();
  
  let colorEstado;
  let estadoTexto = "";

  if (rGlobal < 0.35) {
    colorEstado = color(255, 70, 70);
    estadoTexto = "ESTADO: DESORDEN";
  } else if (rGlobal < 0.75) {
    colorEstado = color(255, 180, 50);
    estadoTexto = "ESTADO: ORGANIZACIÓN PARCIAL";
  } else {
    colorEstado = color(50, 220, 255);
    estadoTexto = "ESTADO: ORGANIZACIÓN ESTABLE";
  }

  stroke(colorEstado);
  strokeWeight(2);
  let diametroAnillo = map(rGlobal, 0, 1, 60, 150);
  circle(cx, cy, diametroAnillo);

  // CORRECCIÓN AQUÍ: Usando red(), green(), blue() en lugar de _getRed()
  fill(red(colorEstado), green(colorEstado), blue(colorEstado), 80);
  circle(cx, cy, 50);

  fill(255);
  noStroke();
  textSize(11);
  textAlign(CENTER, CENTER);
  text(`Sincronía (r): ${rGlobal.toFixed(2)}`, cx, cy - 2);
  text(estadoTexto, cx, cy + 90);
  pop();
}

function dibujarAcoplamientos(cx, cy) {
  strokeWeight(1);
  for (let i = 0; i < agentes.length; i++) {
    for (let j = i + 1; j < agentes.length; j++) {
      let a1 = agentes[i];
      let a2 = agentes[j];

      let difFase = cos(a1.theta - a2.theta);
      if (difFase > 0) {
        let opacidad = map(difFase, 0, 1, 0, 100);
        stroke(100, 200, 255, opacidad * (K / 2));
        line(a1.x, a1.y, a2.x, a2.y);
      }
    }
  }
}

function inyectarEntropia() {
  for (let a of agentes) {
    a.theta += random(-PI, PI);
  }
}

function mousePressed() {
  if (!audioIniciado) {
    Tone.start();
    audioIniciado = true;
  }

  for (let a of agentes) {
    let d = dist(mouseX, mouseY, a.x, a.y);
    if (d < 30) {
      a.theta = random(TWO_PI);
      a.brilloVisual = 255;
    }
  }
}

function mouseDragged() {
  for (let a of agentes) {
    let d = dist(mouseX, mouseY, a.x, a.y);
    if (d < 40) {
      a.x = constrain(mouseX, 50, width - 50);
      a.y = constrain(mouseY, 50, height - 120);
    }
  }
}

class Agente {
  constructor(id, x, y, personalidad, omegaBase, nota) {
    this.id = id;
    this.x = x;
    this.y = y;
    this.personalidad = personalidad;
    this.omegaBase = omegaBase;
    this.nota = nota;

    this.theta = random(TWO_PI);
    this.faseAnterior = this.theta;
    this.dTheta = 0;
    this.brilloVisual = 0;
  }

  calcularKuramoto(todosLosAgentes) {
    let sumaSeno = 0;

    for (let otro of todosLosAgentes) {
      if (otro.id !== this.id) {
        sumaSeno += sin(otro.theta - this.theta);
      }
    }

    let omegaEfectiva = this.omegaBase * globalOmega;
    let delta = omegaEfectiva + (K / NUM_AGENTES) * sumaSeno;
    this.dTheta = constrain(delta, -0.2, 0.2);
  }

  actualizar() {
    this.faseAnterior = this.theta;
    this.theta += this.dTheta;

    while (this.theta >= TWO_PI) this.theta -= TWO_PI;
    while (this.theta < 0) this.theta += TWO_PI;

    if (this.personalidad === "PAD" && audioIniciado) {
      let valFiltro = map(sin(this.theta), -1, 1, 150, 1800);
      synthPad.frequency.rampTo(valFiltro, 0.05);
    }

    if (this.faseAnterior > TWO_PI * 0.75 && this.theta < TWO_PI * 0.25) {
      this.dispararSonido();
    }

    this.brilloVisual = max(0, this.brilloVisual - 12);
  }

  dispararSonido() {
    if (!audioIniciado) return;

    try {
      if (this.personalidad === "BAJO") {
        synthBajo.triggerAttackRelease(this.nota, "4n");
      } else if (this.personalidad === "PLUCK") {
        synthPluck.triggerAttackRelease(this.nota, "8n");
      } else if (this.personalidad === "PAD") {
        synthPad.triggerAttackRelease(this.nota, "2n");
      } else if (this.personalidad === "GLITCH") {
        synthGlitch.triggerAttackRelease("16n");
      }
    } catch (e) {}

    this.brilloVisual = 255;
  }

  dibujar() {
    push();
    translate(this.x, this.y);

    let colorBase;
    let tamanoBase = 35;

    if (this.personalidad === "BAJO") {
      colorBase = color(255, 70, 90);
      tamanoBase = 45;
    } else if (this.personalidad === "PLUCK") {
      colorBase = color(0, 200, 255);
      tamanoBase = 30;
    } else if (this.personalidad === "PAD") {
      colorBase = color(180, 100, 255);
      tamanoBase = 40;
    } else {
      colorBase = color(255, 230, 50);
      tamanoBase = 25;
    }

    fill(red(colorBase), green(colorBase), blue(colorBase), 160 + this.brilloVisual);
    stroke(255, 220);
    strokeWeight(1.5);

    if (this.personalidad === "GLITCH") {
      triangle(0, -tamanoBase/2, -tamanoBase/2, tamanoBase/2, tamanoBase/2, tamanoBase/2);
    } else if (this.personalidad === "PAD") {
      rectMode(CENTER);
      rect(0, 0, tamanoBase, tamanoBase, 8);
    } else {
      circle(0, 0, tamanoBase + (this.brilloVisual / 15));
    }

    if (!isNaN(this.theta)) {
      let px = cos(this.theta) * (tamanoBase * 0.35);
      let py = sin(this.theta) * (tamanoBase * 0.35);
      fill(255);
      noStroke();
      circle(px, py, 6);
    }

    pop();
  }
}
´´´

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
