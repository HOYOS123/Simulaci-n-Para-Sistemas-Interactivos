# Bitácora - Unidad 1

**Reto:** Navegar la Incertidumbre  
**Formato:** 9:16 Full Screen  
**Tecnologías:** p5.js + ml5.js (HandPose)  
**Festival escogido:** MUTEK - Festival internacional de creatividad digital, la musica electronica y el arte audiovisual.
---

## 1. Pregunta Orientadora y Concepto

**¿Cómo convertir diferentes formas de aleatoriedad en diferentes significados?**

El proyecto hace que el visitante con sus manos **modifique el campo de probabilidades**. que representa la mente humana y la formación de ideas a través de una red neuronal que reacciona a tus manos en tiempo real.

---

## 2. Implementación Visual de los 5 Momentos Conceptuales

1. **Posibilidad:** Vectors aleatorios uniformes (`p5.Vector.random2D()`). Las neuronas derivan sutilmente siguiendo el rumbo de lo que marquen las manos.
2. **Tendencia:** Campo de flujo con Ruido Perlin (`noise()`). Se generan corrientes orgánicas e invisibles de fondo que arrastran suavemente a grupos de neuronas.
3. **Normalidad:** Distribución Gaussiana (`randomGaussian()`). Micro-vibraciones sutiles donde la mayoría de las partículas permanece cerca de su trayectoria habitual.
4. **Excepción (Momento Eureka):** Vuelos de Lévy (`levyStep`). Con una probabilidad muy baja (~0.8%), una neurona realiza un salto drástico hacia un punto lejano, rompiendo el patrón.
5. **Influencia:** Rastreo por IA con `ml5.handPose`. Al juntar las manos, las neuronas se condensan en el centro, **creciendo hasta 8 veces su tamaño** en un **Mega Orbe dorado**.

---

## 3. Aspectos Técnicos y Optimización

* **Tecnologías:** `p5.js` para renderizado gráfico y `ml5.js (v1.2.0)` con backend WebGL para visión por computadora.
* **Optimización a 60 FPS:** Red de **28 neuronas** para mantener los cálculos sinápticos $O(N^2)$ fluidos y migración a modo RGB nativo para liberar carga en CPU.
* **Interacción Suavizada:** Implementación de interpolación lineal (`lerp`) en el rastreo de los puntos clave de los dedos para eliminar el salto del modelo de IA.

---

## 4. Uso de IA Generativa

* **Aportes de IA:** Refactorización de bucles para evitar bloqueos de p5.js, sintaxis de `ml5.js` v1.0+ e interpolación `lerp` para suavizar el rastreo de dedos.
* **Criterio Humano:** Dirección de arte (estética cósmica/dorada), calibración del factor de fuerza magnética y el diseño del concepto de condensación del pensamiento.

---

## 5. Tabla de Autoevaluación

| **1. Coherencia de la Pieza** | **CUMPLE** | Experiencia única e ininterrumpida en formato 9:16. |
| **2. Conceptos Estocásticos** | **CUMPLE** | Usa Perlin, Gaussiana, Lévy y Distribución Uniforme. |
| **3. Interacción en Probabilidades** | **CUMPLE** | La webcam altera las reglas y vectores de atracción, no dibuja directamente. |
| **4. Funcionamiento Autónomo** | **CUMPLE** | Sin usuario, la red flota orgánicamente movida por ruido Perlin. |
| **5. Identidad Visual con Variaciones** | **CUMPLE** | Es siempre una red neuronal, pero ninguna ejecución es igual a otra. |
| **6. Formato y Ejecución** | **CUMPLE** | Canvas vertical 9:16 responsivo corriendo a 60 FPS. |
| **7. Documentación y Commits** | **CUMPLE** | Proceso registrado en el repositorio de GitHub. |

Autoevaluacion: 5

---

[Video evidencia del proyecto funcionando](https://youtu.be/u6iM4aS71jY)

---

[Link al proyecto](https://editor.p5js.org/HOYOS123/sketches/DrCm7U7fk)

---

# Código utilizado en P5.js:

## Sketch.js

´´´
// noprotect
/**
 * Reto de Diseño: Navegar la Incertidumbre (Modo Poder Gigante / Mega Orbe)
 * Efecto: Crecimiento masivo de neuronas (hasta 8x), capas de resplandor (Glow)
 * y expansión de conexiones al juntar las manos.
 */

let handPose;
let video;
let rawHands = [];
let isIaReady = false;

// Suavizado de posiciones (Interpolación lerp)
let smoothKeypoints = [];

let neurons = [];
const NUM_NEURONS = 28; 
let canvasWidth, canvasHeight;

let isPinching = false;
let shockwaves = [];

// Variables para la Carga de Poder Gigante
let chargeFactor = 1.0;      // Factor de escala (1.0 = normal, hasta 8.0 = Gigante)
let chargeCenter = null;     // Centro de energía entre manos

function preload() {
  ml5.setBackend("webgl");
  handPose = ml5.handPose({ maxHands: 2 });
}

function setup() {
  calculateCanvasSize();
  let density = displayDensity();
  pixelDensity(density);
  createCanvas(canvasWidth, canvasHeight);

  colorMode(RGB, 255, 255, 255, 1);
  background(10, 12, 25);

  video = createCapture(VIDEO, function() {
    console.log("Cámara lista. Iniciando HandPose...");
    handPose.detectStart(video, gotHands);
  });
  
  video.size(width, height);
  video.hide();

  // Inicializar neuronas
  Array.from({ length: NUM_NEURONS }).forEach(() => {
    neurons.push(new NeuralImpulse(width / 2, height / 2));
  });
}

function gotHands(results) {
  rawHands = results;
  if (!isIaReady && rawHands) {
    isIaReady = true;
  }
}

function draw() {
  // Fondo oscuro con estela
  background(10, 12, 25, 0.18);

  // Cámara sutil de fondo
  push();
  tint(255, 0.08);
  image(video, 0, 0, width, height);
  pop();

  // 1. SUAVIZADO DE MANOS
  updateSmoothedKeypoints();

  // 2. CÁLCULO DE PODER GIGANTE
  calculatePowerCharge();

  // 3. DETECCIÓN DE PELLIZCO
  let wasPinching = isPinching;
  isPinching = false;

  if (rawHands && rawHands.length > 0) {
    rawHands.forEach(hand => {
      let thumb = hand.keypoints[4];
      let indexFinger = hand.keypoints[8];
      if (thumb && indexFinger) {
        let dx = thumb.x - indexFinger.x;
        let dy = thumb.y - indexFinger.y;
        if (dx * dx + dy * dy < 1225) { // < 35px
          isPinching = true;
          if (!wasPinching) {
            shockwaves.push(new Shockwave((thumb.x + indexFinger.x) / 2, (thumb.y + indexFinger.y) / 2));
          }
        }
      }
    });
  }

  // 4. PUENTE ELÉCTRICO REFORZADO
  if (rawHands.length >= 2) {
    drawInterHandBridge();
  }

  // 5. ONDAS DE CHOQUE
  shockwaves.forEach((sw, index) => {
    sw.update();
    sw.display();
    if (sw.isDead()) shockwaves.splice(index, 1);
  });

  // 6. HALOS EN YEMAS
  smoothKeypoints.forEach(k => {
    if (k.isTip) drawFingerAura(k.x, k.y);
  });

  // 7. ACTUALIZAR Y DIBUJAR RED NEURONAL GIGANTE
  neurons.forEach(n => n.update(smoothKeypoints, isPinching, chargeFactor, chargeCenter));
  drawSynapses();
  neurons.forEach(n => n.display(chargeFactor));

  // Guía visual en pantalla
  if (smoothKeypoints.length === 0) {
    fill(0, 180);
    noStroke();
    rect(10, height - 40, width - 20, 30, 6);
    fill(180, 210, 255);
    textAlign(CENTER, CENTER);
    textSize(11);
    let msg = isIaReady ? "Muestra tus manos a la cámara para activar la red" : "Cargando IA de manos...";
    text(msg, width / 2, height - 25);
  }
}

// Eleva el factor de carga hasta 8.0x (GIGANTE)
function calculatePowerCharge() {
  if (rawHands && rawHands.length >= 2) {
    let h1 = rawHands[0].keypoints[9];
    let h2 = rawHands[1].keypoints[9];

    if (h1 && h2) {
      let d = dist(h1.x, h1.y, h2.x, h2.y);
      // Mapea la cercanía: a < 30px se vuelve colosal (8.0x de escala)
      let targetCharge = map(constrain(d, 30, 320), 320, 30, 1.0, 8.0);
      chargeFactor = lerp(chargeFactor, targetCharge, 0.12);
      
      chargeCenter = createVector((h1.x + h2.x) / 2, (h1.y + h2.y) / 2);
      return;
    }
  }
  
  chargeFactor = lerp(chargeFactor, 1.0, 0.08);
  chargeCenter = null;
}

function updateSmoothedKeypoints() {
  let targetPoints = [];
  let tipIndices = [4, 8, 12, 16, 20];

  if (rawHands && rawHands.length > 0) {
    rawHands.forEach(hand => {
      if (hand.keypoints) {
        hand.keypoints.forEach((k, idx) => {
          targetPoints.push({ x: k.x, y: k.y, isTip: tipIndices.includes(idx) });
        });
      }
    });
  }

  while (smoothKeypoints.length < targetPoints.length) {
    smoothKeypoints.push({ x: width / 2, y: height / 2, isTip: false });
  }
  if (smoothKeypoints.length > targetPoints.length) {
    smoothKeypoints.length = targetPoints.length;
  }

  smoothKeypoints.forEach((sk, i) => {
    sk.x = lerp(sk.x, targetPoints[i].x, 0.35);
    sk.y = lerp(sk.y, targetPoints[i].y, 0.35);
    sk.isTip = targetPoints[i].isTip;
  });
}

function drawInterHandBridge() {
  let h1 = rawHands[0].keypoints[9];
  let h2 = rawHands[1].keypoints[9];

  if (h1 && h2) {
    push();
    let bridgeAlpha = map(chargeFactor, 1.0, 8.0, 0.4, 1.0);
    let bridgeWeight = map(chargeFactor, 1.0, 8.0, 2, 12);
    
    if (chargeFactor > 3.0) {
      stroke(255, 230, 110, bridgeAlpha);
    } else {
      stroke(120, 220, 255, bridgeAlpha);
    }
    
    strokeWeight(bridgeWeight);
    
    let steps = 8;
    let prevX = h1.x;
    let prevY = h1.y;
    let jitter = map(chargeFactor, 1.0, 8.0, 8, 35);

    for (let i = 1; i <= steps; i++) {
      let t = i / steps;
      let nextX = lerp(h1.x, h2.x, t) + (i < steps ? random(-jitter, jitter) : 0);
      let nextY = lerp(h1.y, h2.y, t) + (i < steps ? random(-jitter, jitter) : 0);
      line(prevX, prevY, nextX, nextY);
      prevX = nextX;
      prevY = nextY;
    }
    pop();
  }
}

class Shockwave {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.radius = 5;
    this.alpha = 1.0;
  }

  update() {
    this.radius += 8;
    this.alpha -= 0.035;
  }

  display() {
    push();
    noFill();
    stroke(255, 80, 200, this.alpha);
    strokeWeight(3);
    circle(this.x, this.y, this.radius * 2);
    pop();
  }

  isDead() {
    return this.alpha <= 0;
  }
}

function drawFingerAura(x, y) {
  push();
  noFill();
  let pulse = sin(frameCount * 0.1) * 4;
  let auraSize = 14 * Math.min(chargeFactor, 2.5);
  
  if (isPinching) {
    stroke(255, 60, 180, 0.6);
  } else if (chargeFactor > 3.0) {
    stroke(255, 230, 110, 0.85);
  } else {
    stroke(80, 180, 255, 0.6);
  }
  
  strokeWeight(2);
  circle(x, y, auraSize + pulse);
  pop();
}

function drawSynapses() {
  // Las líneas se conectan a mayor distancia durante el modo Gigante
  let maxDist = 75 * Math.min(chargeFactor, 2.2);
  let maxDistSq = maxDist * maxDist;

  neurons.forEach((p1, i) => {
    neurons.forEach((p2, j) => {
      if (j > i) {
        let dx = p1.pos.x - p2.pos.x;
        let dy = p1.pos.y - p2.pos.y;
        
        if (Math.abs(dx) <= maxDist && Math.abs(dy) <= maxDist) {
          let distSq = dx * dx + dy * dy;
          if (distSq < maxDistSq) {
            let alpha = 1.0 - (distSq / maxDistSq);
            let lineW = map(distSq, 0, maxDistSq, 2.5 * chargeFactor, 0.3);
            
            if (chargeFactor > 4.0) {
              stroke(255, 230, 120, alpha * 0.95);
            } else if (isPinching) {
              stroke(255, 70, 180, alpha * 0.85);
            } else {
              stroke(p1.r, p1.g, p1.b, alpha * 0.8);
            }
            
            strokeWeight(lineW);
            line(p1.pos.x, p1.pos.y, p2.pos.x, p2.pos.y);
          }
        }
      }
    });
  });
}

class NeuralImpulse {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.r = floor(random(100, 160));
    this.g = floor(random(140, 220));
    this.b = 255;
    this.targetKeypoint = null;
    this.isEureka = false;
  }

  update(keypoints, pinching, charge, centerOrb) {
    if (keypoints && keypoints.length > 0) {
      if (!this.targetKeypoint || random(1) < 0.04) {
        this.targetKeypoint = random(keypoints);
      }

      let normalOffset = createVector(randomGaussian(0, 1.2), randomGaussian(0, 1.2));
      let angle = noise(this.pos.x * 0.008, this.pos.y * 0.008, frameCount * 0.003) * TWO_PI * 2;
      let flow = p5.Vector.fromAngle(angle).mult(0.8);

      let pull = pinching ? 0.14 : 0.07;
      let dx = this.targetKeypoint.x - this.pos.x;
      let dy = this.targetKeypoint.y - this.pos.y;
      let attraction = createVector(dx * pull, dy * pull);

      // Fuerte atracción al centro del orbe cuando el poder es colosal
      if (centerOrb && charge > 1.3) {
        let orbPull = p5.Vector.sub(centerOrb, this.pos).mult(0.09 * charge);
        attraction.add(orbPull);
      }

      let uniformUncertainty = p5.Vector.random2D().mult(0.3);

      let levyProb = pinching ? 0.03 : 0.008;
      let levyStep = createVector(0, 0);
      
      if (random(1) < levyProb) {
        let randomPoint = random(keypoints);
        levyStep.set(randomPoint.x - this.pos.x, randomPoint.y - this.pos.y);
        this.isEureka = true;
      } else {
        this.isEureka = false;
      }

      this.vel.add(flow).add(normalOffset).add(attraction).add(uniformUncertainty).add(levyStep);
      this.vel.limit(pinching ? 6.0 : 3.8 + (charge * 0.6));
      this.pos.add(this.vel);

    } else {
      let angle = noise(this.pos.x * 0.003, this.pos.y * 0.003, frameCount * 0.001) * TWO_PI * 2;
      let flow = p5.Vector.fromAngle(angle).mult(0.5);
      let attraction = createVector((width / 2 - this.pos.x) * 0.01, (height / 2 - this.pos.y) * 0.01);
      
      this.vel.add(flow).add(attraction);
      this.vel.limit(2);
      this.pos.add(this.vel);
      this.isEureka = false;
    }

    this.pos.x = constrain(this.pos.x, 0, width);
    this.pos.y = constrain(this.pos.y, 0, height);
  }

  display(charge) {
    noStroke();
    let baseRadius = 7 * charge;
    let coreRadius = 2.5 * charge;

    // CAPA 1: Halo exterior expansivo (Aura/Glow)
    if (charge > 2.0) {
      let glowRadius = baseRadius * 2.2;
      fill(255, 200, 50, 0.12 * charge);
      circle(this.pos.x, this.pos.y, glowRadius);
    }

    // CAPA 2 & 3: Cuerpo y Núcleo
    if (this.isEureka) {
      fill(255, 235, 90, 0.95);
      circle(this.pos.x, this.pos.y, baseRadius * 1.4);
      fill(255, 255, 255, 1);
      circle(this.pos.x, this.pos.y, coreRadius * 1.5);
    } else if (isPinching) {
      fill(255, 60, 180, 0.45);
      circle(this.pos.x, this.pos.y, baseRadius);
      fill(255, 220, 240, 1);
      circle(this.pos.x, this.pos.y, coreRadius);
    } else if (charge > 3.0) {
      // Estado Incandescente Dorado
      fill(255, 200, 60, 0.55);
      circle(this.pos.x, this.pos.y, baseRadius);
      fill(255, 255, 230, 1);
      circle(this.pos.x, this.pos.y, coreRadius * 1.2);
    } else {
      // Estado Base Azul
      fill(this.r, this.g, this.b, 0.45);
      circle(this.pos.x, this.pos.y, baseRadius);
      fill(220, 240, 255, 0.95);
      circle(this.pos.x, this.pos.y, coreRadius);
    }
  }
}

function calculateCanvasSize() {
  let targetRatio = 9 / 16;
  let currentRatio = windowWidth / windowHeight;

  if (currentRatio < targetRatio) {
    canvasWidth = windowWidth;
    canvasHeight = windowWidth / targetRatio;
  } else {
    canvasHeight = windowHeight;
    canvasWidth = windowHeight * targetRatio;
  }
}

function windowResized() {
  calculateCanvasSize();
  resizeCanvas(canvasWidth, canvasHeight);
  if (video) video.size(width, height);
  background(10, 12, 25);
}
´´´

## Index.html

´´´
<!DOCTYPE html>
<html lang="es">
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/addons/p5.sound.min.js"></script>
    
    <!-- LIBRERÍA ML5.JS (IMPORTANTE PARA DETECCIÓN DE CUERPO) -->
    <script src="https://unpkg.com/ml5@1.2.0/dist/ml5.min.js"></script>

    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />
  </head>
  <body>
    <main>
    </main>
    <script src="sketch.js"></script>
  </body>
</html>

´´´
